# Open Issues to be improved related to SCP/Platform


## Development Tenant onboarding:
- Create Subaccount via api with Global account username and password  
- Enable CF via api  
- Subscribe to Applications
- Create Role Collections
- Assign Role collections to users/user group
- Segregation of Duties / Audit Trail, see more below...
- implicit grant flow for local development scenarios (required for integration testing)
- For internal development access to microservices must be possible without productive credentials (internal scopes)

## Operations/Further development:  
-	Poor availability, no stable upgrade of underlaying backing services (reds, mongo, postgresql)
-	lifecycle support of permissions/scopes/xssecurity
-   subdomains (logical tenant ids, this is name end users need to know)
    - currently scoped per data center => not a good idea, as this prohibits geo routing. Revenue Cloud therefore does not allow reusing same subdomain in multiple data centers
    - Namespacing of subdomains: global namespace, what if multiple accounts want to use same subdomain

## Managing Clients/Service Keys:  
-	Updating permissions (set of scopes) of existing service keys is not possible, instances must be deleted and recreated
-	Not possible to see set of assigned persmissions(scopes) in service instance view of cockpit
-	Creating a client/service instance via cockpit ( without creating org and space)
-	Segregation of duty:
    -	Assigning permissions to create service instances (clients) with dedicated scopes
    -	Audit Log for client creation, token retrieval, creating tokens based on principal or based on trust
    -	Four eye principle (assignment of permissions via workflow)

## User experience:  
-	Login flow without specifying subaccount (e.g. via 2-stage login flow as implemented by Microsoft or Google)  -> Get all tenants for a user 
    - Current "subdomain URLs" violate information disclosure standard, testing if subdomain exists or not is possible for any (anonymous) user
-	SAML SSO flow for internal dev tenants (SAP employees)
-	Possibility for Endusers to let us create/manage/assign roles for users to ease onborading/usage (e.g. via Resource Owner grant flow)
-	Trial Accounts: Ability to do one-click tenant creation (i.e. from Revenue Cloud landing page) -> same use case also in Transportation Management
    -	User self registration (no customer IDP required)
    -	Without subaccount/org/space/service instance workflow
    - automatic scripting of account setup (subscriptions, entitlements, quotas, permissions, audits, ...)
- Single User, multiple tenants
    - one login for all apps of all tenants the current user is authorized to use
    - switching from one tenant to another (same identityzone) => common use case
    - switching from one tenant to another (same identityzone) => potential use case
- logoff flows
    - direct back to where the user was before
    - browser back either to login or to web page user was on before logging in

## Re-use service and SaaS application provisioning:  
-	Too many bindings to backing services (2*saas-registry (ui/api) 2*xsuaa (ui/api)) for exposing of SaaS solution and API necessary
    - see also [Jupiter manifest EU](https://github.wdf.sap.corp/ngom-infrastructure/Jupiter/blob/scp-auth/manifest.eu10.yml)
    - see also [Jupiter manifest US](https://github.wdf.sap.corp/ngom-infrastructure/Jupiter/blob/scp-auth/manifest.us10.yml)
    - see also [Sequence Diagrams](https://github.wdf.sap.corp/ngom-documents/scp/tree/master/diagrams)
-	The whole process of exposing and subscribing to applications is far to complicated not at all user friendly
    -	Large organizational overhead with a mandatory ticket process
    -	Distributed documentation 
