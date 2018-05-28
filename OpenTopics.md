# Open Topics

## Tenant Mode in xs-security.jsons
The documentation of the tenant mode can be found [here](https://jam4.sapjam.com/blogs/show/OEEaZVIXHRDiJEsr9DvHR8). For 
multi-tenancy SaaS applications, the tenant mode "shared" is required. It is not clear to us which tenant mode we need to 
use for our multi-tenant ReUse Service (APIs). Normally we would assume that if the APIs will be consumed by multiple tenants, 
we would also need tenant mode "shared". But in the documentation it says tenant mode "dedicated" is the default value for XSUAA's 
which do not use the plan "application". This is the case for our APIs as they use the plan "broker". 

> Answer: For broker plan XSUAAs only the tenant-mode dedicated is supported right now.

## Creation/Update of xs-security.jsons

A Jenkins job for creating/updating the XSUAA service instances by uploading the respective `xs-security.jsons` is required. 
Depending on the changes to the security jsons, different mechanisms need to be used:
* `cf update-service ...` works only for certain cases which are documented 
[here](https://help.sap.com/viewer/65de2977205c403bbc107264b8eccf4b/Cloud/en-US/c3b892e703174badb93f1ab35f76c354.html)
* if an incompatible change was done, the whole service instance needs to be unbinded, deleted, created again. This 
requires a restart/restage of all bound applications 

## Authorization Flow on customer side
Customer has a global account and a super-user for that. How this user adds business-user and developer is not yet clarified.

## Which updates on XS-Security.json are allowed?
It is not clear which changes are allowed. The document behind this 
[link](https://help.sap.com/viewer/65de2977205c403bbc107264b8eccf4b/Cloud/en-US/c3b892e703174badb93f1ab35f76c354.html) 
describes in theory which changes are allowed. But in reality this list insufficient. For instance ist is only described 
what you can to with scopes and not general attributes like tenant-mode, xs-appname, etc.. And there are also failures 
which are totally random for instance you cannot create an instance of the XSUAA without an XS-Security.json and aftwards 
update this UAA instance with the actual XS-Security.json. 

> Answer: Exactly those changes are allowed in the xs-security.json. If an invalid update operation is done, the 
`cf update-service ...` command should fail with a comprehensible error message.

## Deployment lifecycle
The deployment lifecycle of the XS-Security.jsons and the Broker needs to be clarified as well the deployment strategy 
for Jupiter (do we have updates of the XSUAA which requires restaging of Jupiter). 

## Role-Templates
In order to keep the functionality of Yaas, that the customer tenant can assign scopes to a user role we have to provide a role template for every scope.

## Voyager / Local Development
How can we enable developers to develop their UIs and services locally? Previously this was done via Voyager (YaaS Login, 
mocking functionality, routing, feature toggling, ...).

## UAA of type Broker
Is it possible to update the API security json? Should be possible in theory but needs to be tested.

## Revenue Cloud service Broker
Is it necessary to restage the service Broker after the API xs-security.json has been updated? Should not be necessary in theory but needs to be tested.
