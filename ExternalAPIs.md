# External API Calls using the Service Broker Framework of SCP

External API Calls (or in SCP terminology App2Service Calls) are realized via the Service Broker Framework on Cloud Foundry. 

As Revenue Cloud also offers public APIs, the SCP provided broker framework needs to be evaluated. Then, it will be discussed how the framework 
might be integrated into our current [infrastructure setup](https://github.wdf.sap.corp/ngom-documents/deploy-with-confidence/blob/master/figures/TechnicalLandscapeFor1802.pdf).
Several approaches would be possible here and will therefore be mentioned. Limitations of the framework which we found during our 
analysis will also be documented here.

## Node Service Broker Framework

SCP provides a node application for creating a service broker in the Cloud Foundry environment. 
* [App2Service Calls explained](https://jam4.sapjam.com/blogs/show/2dxT4cVGxTXZRJT0D1DQQM)
* [node-sbf repository](https://github.wdf.sap.corp/xs2/node-sbf)
* [Working example for a java reuse service](https://github.wdf.sap.corp/xs2/node-sbf/tree/master/examples/java/technical-user-flow)

By using the XSUAA service broker plan, 
OAuth2 authentication via JWT tokens can be enabled for two different flows:
* Named user via `user_token` flow
* Technical user via `client_credentials` flow

## API entry points

It needs to be decided what the entry point of public APIs for Revenue Cloud will be. The two obvious choices would be: either 
each microservice has an own service broker instance and gets propagated on SCP individually or Jupiter will serve as our common entry pointfor APIs
which will then route the requests to the correct microservice (using our landscape-router).

Option 1 would have the disadvantage that each microservice team would need their own xsuaa binding and would need to implement Spring Security
for validating JWT tokens, etc. As this would result in huge efforts for the microservice development teams and seems out of scope until Release 1802,
we decided for Option 2. Jupiter will then function as our reuse service propagated on SCP.

The URL for now will be `https://revenue.cloud.sap/api` . With further activities on EU Data Center move and SCP move, this could again change 
(e.g.`api.revenue.cloud.sap`, `api.eu10.revenue.cloud.sap`, `api.us10.revenue.cloud.sap`, ...).

## Integration Options

### 1. Deploy the node sbf with our reuse service (Jupiter)

The node service broker framework can be deployed with the reuse service. Specific configuration in the `manifest.yml` is required. This solution
worked very good in the example project.

With this option, we would need to invest into adapting the pipeline scripts of Jupiter so that the node sbf gets deployed containing necessary
information in its manifest.yml. An advantage is that Jupiter will not be directly dependent on the node sbf. Even if the service broker is not
starting or runs into an error, Jupiter would not be directly affected.

### 2. Integrate the node sbf into Jupiter

The node service broker framework can be used as middleware in node and could therefore also be integrated in Jupiter. Via `app.use(route, module)` 
the broker could be registered in Jupiter, e.g. `https://revenue.cloud.sap/broker` protected with specific broker credentials. 

With this option the pipeline scripts could remain mostly untouched. Some small changes in Jupiter would be necessary. A disadvantage of this 
option is that Jupiter would have a hard dependency on the node sbf. If an error occurs in the framework which leads to a crashing instance,
Jupiter would be affected as well.

### 3. Implement the Service Broker API ourselves

Would bear the most effort. If the service broker framework of SCP already provides sufficient functionality, this would only create overhead. 
Therefore, this was not considered an option.

### 4. Decision

After taking a look at the node-sbf code and evaluating the different options, the decision was taken to deploy the sbf in addition
to Jupiter/our reuse service. The main advantage is that Jupiter will still continue to work if the sbf crashes or runs into errors 
as it only handles the implementation of the Open Service Broker API on CF (creation & deletion of service instances, etc.). 


## Propagation of the reuse service on CF

Reuse services are registered in CF just like other SaaS applications with two small differences. You can find a detailed
description here: 
[SaaS Application Registration in CF](https://wiki.wdf.sap.corp/wiki/display/CPC15N/SaaS+Application+Registration+in+CF#SaaSApplicationRegistrationinCF-SaaSReuseServices).

The commercialization process for reuse services can be found here: 
[CF Product Commercialization in CIS](https://wiki.wdf.sap.corp/wiki/display/CPC15N/CF+Product+Commercialization+in+CIS).

## Specific topics

### Restrict granted scopes of service instance

There needs to be the possibility to restrict the scopes which are granted to consuming applications (both for binding apps and service keys).
This can be done by specifying a `parameters.json` when creating the reuse service instance which contains only the scopes that shall be granted when requesting
a token from the uaa for this specific service.

* [Issue on the node-sbf which requests a quite similar feature](https://github.wdf.sap.corp/xs2/node-sbf/issues/136)
* [Pull request explaining the feature](https://git.wdf.sap.corp/#/c/2776995/)

If the master xs-security.json specifies authorities, each clone instance will automatically get those. Clones can then request further
authorities by specifying them in the clone xs-security.json (they must be a subset of the scopes of the master).

Example: 

xs-security.json of the xsuaa broker instance:
```json
{
  "xsappname": "reuse-service-123",
  "scopes" : ["$XSAPPNAME.scope1", "$XSAPPNAME.scope2"]
}
```

parameters.json of the reuse service instance:
```json
{
  "xs-security" : {
    "xsappname": "reuse-service-123-consumer",
    "authorities" : ["$XSMASTERAPPNAME.scope1"]
  }
}
```
With this configuration, a token which is requested by the consumer for the reuse service instance can only contain scope1 or less.

> Caution: Using this concept the consumer of our API will always have to specify a `parameters.json` (valid xs-security.json) or
else he will get no scopes granted.

## Limitations

### Naming of the service broker

After creating a service broker via `cf create-service-broker`, the name will be reserved. Therefore, we should try to 
be cautious when randomly creating brokers, because in the future we might need the name for productive use.

### Update catalog.json
If the service broker ever updates its catalog of services and plans (catalog.json) then a ticket has to be created in order to ask Cloud Foundry to update the catalog/marketplace.

### Update service instance (client)
During the creation of the service instance (client) scopes are assigned to the service instance with the parameter.json. After the ceation of the instance there is no possibility to change the number of assigned scopes e.g. with cf update-service <instance name> -c parameter.json. 
