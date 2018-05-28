# Security Descriptors on SCP CF

The XSUAA instances on SCP CF are configured using a security descriptor commonly referred to as `xs-security.json`.
The file is uploaded via the `-c` parameter to CF when creating the service instance.
Each security file required at least an `xsappname` property. Further fields are optional and sometimes even service
plan specific.

A complete overview of the `xs-security.json` structure can be found [here](https://jam4.sapjam.com/blogs/show/OEEaZVIXHRDiJEsr9DvHR8).

## Updating the xs-security.json

As the configuration of the XSUAA instance is uploaded when creating the service instance, there needs to be a way to 
update the file after creation. In [this document](https://help.sap.com/viewer/65de2977205c403bbc107264b8eccf4b/Cloud/en-US/c3b892e703174badb93f1ab35f76c354.html),
the allowed update operations on the `xs-security.json` are described. Still, some properties are not considered (e.g. 
tenant-mode, authorities, ...). 

## Security Descriptors in Revenue Cloud

As Revenue Cloud offers a UI, which requires an XSUAA instance of plan application, as well as public APIs, which require 
the broker plan of the XSUAA, at least two security descriptor files are required.
The process of creating and uploading them can partly be automated (via Jenkins builds). The scope and endpoint definitions 
still need to be done manually.

### Endpoint/Scope definitions

As our move from YaaS to SCP is done in quite a short timeframe, it was decided that for now feature parity is in focus. 
For the configuration of the XSUAA instances this means that we try to stick mostly to the configuration that is already 
available in YaaS. 

Therefore, the endpoint definitions from YaaS were extracted to a usable JSON format and saved in our central 
[landscape configuration](https://github.wdf.sap.corp/ngom-infrastructure/landscape-configuration/tree/master/services). 
Here the maintenance will still be done centrally by a responsible person but the teams are able to take a look at the 
definitions (compared to YaaS where everything was hidden from the teams).

To make editing of the service endpoint definitions clearer, they are all stored in separate files following the naming 
convention `<service-name>.<version>.json`. In the build of the landscape-configuration, they then get summarized into 
one big `services.json` file. Several validations are running before saving the file so that they do not contain any errors. 

The `services.json` will then be uploaded to [Themisto](https://github.wdf.sap.corp/ngom-infrastructure/Themisto) on the 
landscape-configuration reference. From there, an application can just access it when needed. For example, the landscape 
router uses the endpoint definitions from the `services.json` to authorize requests based on the scopes contained in the JWT.

### xs-security.json Creation

Also in the build of the landscape-configuration, the `xs-security.json` is created based on the previously 
defined `services.json`. Fields like the xsappname and the tenant-mode are already defined in a [template](https://github.wdf.sap.corp/ngom-infrastructure/landscape-configuration/blob/master/build/config.js) while the scopes 
will be dynamically added to the file based on the available scopes in the `services.json`.

As we need two security descriptors, one for UI and one for APIs, the build generates the two files `xs-ui-security.json` 
and `xs-api-security.json`. As the names already indicate, the UI descriptor contains all scopes from the UI endpoint 
definitions and the API descriptor contains all scopes from public endpoint definitions. 

The two security descriptors also get uploaded to Themisto. Currently there is no automatic update of the XSUAA service 
instances based on the newly uploaded descriptors. On the one hand because the correct lifecycle of these files still needs 
to be defined and on the other hand because there are certain update restrictions and with the current upload process we 
cannot be sure which part of the security descriptor was changed. More about the update restrictions of the files can be 
found under [open topics](/OpenTopics.md).

#### Role Templates

As the `xs-security.json` also needs to contain the role templates, which the customer is allowed to use to configure 
his roles, they also need to be generated into the security descriptor. Therefore we have [role template files](https://github.wdf.sap.corp/ngom-infrastructure/landscape-configuration/tree/master/roles) in addition 
to the services files. Currently, there is only an example role template which we use for development. Later, these will 
need to be defined by someone from the product team (e.g. CPO, APO, etc.).
