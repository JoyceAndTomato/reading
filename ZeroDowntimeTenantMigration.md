# Zero Downtime Tenant Migration

As we transition from yaas to scp, we need to move existing yaas tenants to scp without loss of data. Most prominent production tenant requiring such a migration is Venezia.

We initially discussed doing this in manual steps, but at the end opted to build tooling to allow doing this in an automated fashion.
A major question/risk is if there is the need for a planned downtime. It was agreed, that we would attempt to find a solution, which allows:
- migrating from yaas to scp without downtime
- access to the tenant with both yaas credentials as well as scp credentials simultaneously
- maintaining access via both yaas and scp for a transition period based on customer/tenant requirements. Venezia requires a transition phase of at least 4 weeks.
- currently, it is sufficient to migrate a tenant within one data center only. At a later phase, it will also be desirable to migrate tenants from one DC to another, but this is currently out of scope.

## Flow (customer point of view)
A productive tenant has a certain number of users and a certain number of client credentials in place, and accesses Revenue Cloud via UI as well as API.
The customer may either have:
a. a yaas account with a high-touch project in yaas with a subscription to Revenue Cloud 
b. an SCP Global Account with a subaccount containing an onboarded and running subscription to Revenue Cloud (UI application plan as well as API service broker plan)

In either of these cases, the customer may create a new subaccount in SCP (even in another Global Account), to which the previous yaas project or scp subaccount will be migrated.

#### Steps:  
- create or provide SCP account (must not have a subscription to Revenue Cloud)
- Create Ticket to Revenue Cloud to
    - (optional) request transfer of existing entitlements to new Global Account
    - provide tenant id and subdomain of new subaccount
- Revenue Cloud will prepare and enable Revenue Cloud Subscription (Tile) in Marketplace
- customer can subscribe to Revenue Cloud
- this subaccount will immediately be bound to the existing tenant/data of the (previous) account, either yaas (a) or scp (b), as described above
- the customer can sign in either with the previous credentials (old tenant) or with the new credentials (new tenant), the data will in both cases be the same.
- Revenue Cloud will internally migrate the tenant ids used in the databases without requiring downtimes
- once finished, the customer is notified, so that the old tenant can be decommissioned. A transition phase is defined based on customer requirements
- once the customer no longer uses the tenant, the Revenue Cloud subscription can be deleted. Revenue Cloud will automatically clean up the old tenant metadata.

## Flow (Revenue Cloud Development point of view)
From development point of view, three dedicated phases are supported, which will be implemented independently in the following sequence. Phase 1 and 3 may take an arbitrary amount of time (even weeks), whereas Phase 2 must be issued as fast as possible (less than 20 seconds) in order to assure zero-downtime for consumers. 

Phase 1. Allow mapping multiple (sub)accounts to one single tenant id
Phase 2. Automate zero downtime migration of tenant's data (migrate old tenant id to new tenant id)
Phase 3. Allow offboarding old tenant by the customer

### Phase 1. Allow mapping multiple (sub)accounts to one single tenant id  
A subaccount is identified by its subdomain, but also has a tenant id (zid). The zid is used when persisting data of the tenant, wheras the subdomain is used to identify and authenticate users and clients and is also the property by which Jupiter/Landscape Router route requests. Ths zid is set by the Landscape Router based on the given JWT token (UI: stored in user session, API: provided in client's JWT). In this phase, two subaccounts/subdomains must share the same tenantId=zid. This is achieved by overriding the zid defined in the JWT token.
Example:
- Subaccount A:    subdomain=A   tenantId=guidA  
- Subaccount B:    subdomain=B   tenantId=guidB  
Important: subaccount B may not be used immediately, it must be prevented that data with guidB is created. To ensure this, a ticket must be created on behalf of Subaccount B to request a mapping to subaccount A! This should be done before allowing Subaccount B to subscribe to Hybris Revenue Cloud!

Proposed solution:
- add tenant B to tenants.json in landscape configuration (if not already existant)  
- add additional property to tenants.json called **onboardWithMappingToTenant**, "onboardWithMappingToTenant":"A"  
- When Subaccount B subscribes to Hybris Revenue cloud, in onboarding callback, check if tenantB.json in Themisto exists, and if it has any mapping properties. This should be done for all tenant onboardings (simple check each time a tenant subscribes). If the onboardWithMappingToTenant Properties exist, the onboarding routine should update the onboarded-tenants file in Themisto. This onboarded-tenants file is NOT part of the landscape configuration, but is managed dynamically via Themisto api only. The controller logic for onboarding callbacks can be found here: https://github.wdf.sap.corp/ngom-infrastructure/Jupiter/blob/scp-auth/src/controllers/saas-registry/registry-ctrl.js  

Here is a sample json entry:  

onboarded-tenants / B.json (this is the file which is used for the onboarding infos, such as the DataCenter and channel to use)  
```javascript  
{
  "id":"guidB",               // these values are determined by the onboarding parameters
  "subdomain":"B",
  "datacenter":"US10",
  "channel":"BETA",
  "mapToTenant":"A",          // this value is determined by looking at the onboardWithMappingToTenant property in the tenants.json
  "mapToTenantId":"guidA"     // this value is determined by looking at the onboardWithMappingToTenantId property in the tenants.json
}
```

Later, in Phase 2, when the data is migrated from guidA to guidB the above entry must be replaced with the following entry:  

onboarded-tenants / A.json
```javascript
{
  "id":"guidA",               // the two values are simply switched (guidB <=> guidA)
  "mapToTenant":"B",          // the two values are simply switched (B <=> A)
  "mapToTenantId":"guidB"     // the two values are simply switched (guidA <=> guidB)
}
```
This assures, that users still logged in with Tenant A will continue to work properly after the data migration is done.  


### Phase 2. Automate zero downtime migration of tenant's data (migrate old tenant id to new tenant id)  
This phase will be triggered via a jenkins job. This jenkins job can be triggered at any time as long as phase 1 is completed. Completion of phase 1 is verified by the jenkins job, by checking if an entry in the onboarded tenant file exists for the tenant from/to which will be migrated. The jenkins job will take the following parameters:  
- migrateDBFromTenant        // "A"  
- migrateDBToTenant          // "B"  

This job needs to do the following steps:  
- preflight checks, e.g. make sure no issues in the target landscape, e.g. health checks all green, rabbit queues in tact with no messages older than 5 seconds  
- check that parameters (migrateDBFromTenant, migrateDBToTenant) exist in onboarded-tenants.json  
- block all requests for both tenants in landscapeRouter. Also make sure, that no more requests are still open. Open Question: Do we have something like a per tenant request counter? E.g. each time a request comes in ++1, each time the response is returned --1  
- If all requests are blocked, initiate tenant id migration in all µ-services. TODO: clarify how to trigger this in various µ-services with Ralf/Patric  
- Open: how to assure atomic migration? All DBs need to be successful. If one DB fails, we have an issue and need to rollback!  
- If successful, onboarded-tenants.json needs to be updated as described above (in Phase 1).  
- Unblock requests in landscapeRouter.  
- Done!  

Questions: RabbitMQ (Rater service has schedulded tasks, Bill service (but should not be affected) -> after the requests get blocked by the router wait before migration

### Phase 3. Allow offboarding old tenant by the customer  
We now have the situation, that the old tenant (A) still exists, but is being mapped to the new tenant ID (guidB). The old tenant can now gracefully be decommissioned. This is in the interest of the owner of tenant A, as a double entitlement is needed (which creates cost). The technique to do this will normally be to unsubscribe Revenue Cloud in Tenant A (if tenant A is an SCP subaccount):

#### If tenant A is an SCP tenant:  
In the offboarding callback, simply update the onboarded-tenants.json. This logic already exists, see [here](https://github.wdf.sap.corp/ngom-infrastructure/Jupiter/blob/scp-auth/src/controllers/saas-registry/registry-ctrl.js)

#### If tenant A is a yaas tenant:  
it is not worth to do this automatically, instead, we will trigger the tenant decommissioning manually. This also works for SCP tenants, but is not the preferred method, as it requires manual maintenance. The tenants.json is updated as follows:
- Add entry for tenant A to tenants.json (if not already existant)  
- Add property to tenantA: "decommissioned":"true"  
- If Jupiter/LandscapeRouter detect this property, then requests/sessions will no longer be accepted.  
