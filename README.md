# Template Healthcare Fitness to CRM Sync Process API

+ [License Agreement](#licenseagreement)# Template Healthcare Fitness to CRM Sync Process API

# License Agreement 
This template is subject to the conditions of the [MuleSoft License Agreement](https://s3.amazonaws.com/templates-examples/AnypointTemplateLicense.pdf). Review the terms of the license before downloading and using this template. You can use this template for free with the Mule Enterprise Edition, CloudHub, or as a trial in Anypoint Studio. 

# Use Case 
As a FitBit user I want a microservice to synchronize Device and Observation data between FitBit system and CRM (e.g. Salesforce Health Cloud).
Fitness to CRM Sync Process API is part of the Healthcare Templates Solution. This template calls FitBit System API to register Patient on Fitbit system. After Patient is registered, data are migrated and scheduler once a day retrieve required data from FitBit through the FitBit System API and migrate them to CRM system using the standardized FHIR structures [version 3.0.1 STU3](https://www.hl7.org/FHIR/index.html).

# Considerations 
To make this template run, there are certain preconditions that must be considered. Failing to do so could lead to unexpected behavior of the template.
Use Anypoint Studio v7.1.4+ and Mule ESB 4.1.2+ to run this template.

### Register your Fitbit Application
Firstly you need to ensure the developer app is created at http://dev.fitbit.com/ as  the OAuth 2.0 Application Type “Server”. Note that you will need to define the Callback URL too.

### Run the Application
Fitbit’s OAuth login has to be initiated from a web-browser.
https://www.fitbit.com/oauth2/authorize?response_type=code&client_id=<your-client-id>&redirect_uri=<your-redirect-uri>&scope=activity%20profile%20settings%20sleep%20weight&prompt=login would get you to the login landing page where you will fill in your email and password. After the successful login you will be redirected to the URL specified in the app at http://dev.fitbit.com/. You can notice the access code in the URL.
To register patient to this FitBit account you need to do create the request GET https://<your-app-domain>.cloudhub.io/patients/{id}/register?code=<your-access-code> where {id} represents Patient ID, who wants to authorize to FitBit account and access code is the one obtained after login with FitBit credentials.

# Run it! 
Simple steps to get Healthcare Fitness to CRM Sync Process API running.
See below.

## Run On Premises
In this section we detail the way you should run your template on your computer.

### Where to Download Anypoint Studio and the Mule Runtime
If you are new to Mule, download this software:

- [Download Anypoint Studio](https://www.mulesoft.com/platform/studio)
- [Download Mule runtime](https://www.mulesoft.com/lp/dl/mule-esb-enterprise)

- You can download Anypoint Studio from this [Location](http://www.mulesoft.com/platform/studio)
- You can download Mule ESB from this [Location](http://www.mulesoft.com/platform/soa/mule-esb-open-source-esb)

### Import a Template into Studio
Anypoint Studio offers several ways to import a project into the workspace, for instance:

- Anypoint Studio Project from File System
- Packaged mule application (.jar)

You can find a detailed description on how to do so in this [Documentation Page](http://www.mulesoft.org/documentation/display/current/Importing+and+Exporting+in+Studio).

### Run in Studio
After opening your template in Anypoint Studio, follow these steps to run it:

1. Locate the properties file `mule.dev.properties`, in src/main/resources.
2. Complete all the properties in the "Properties to Configure" section.
3. Right click the template project folder.
4. Hover your mouse over `Run as`.
5. Click `Mule Application (configure)`.
6. Inside the dialog, select Environment and set the variable `mule.env` to the value `dev`.
7. Click `Run`.

### Run on Mule Runtime Stand Alone 
Fill in all the properties in one of the property files, for example in [mule.prod.properties](../master/src/main/resources/mule.prod.properties) and run your app with the corresponding environment variable to use it. To follow the example, this will be `mule.env=prod`.

## Run on Runtime Manager
When creating your application in Runtime Manager, click an application and click **Manage Application > Properties** to set the environment variables described in the Properties to Configure section.

## Deploy in CloudHub
In Studio, right click your project name in Package Explorer and select Anypoint Platform > Deploy on CloudHub.

### Properties to Configure
To use this template, configure properties in a properties file or in Runtime Manager as environment variables.

### Application Properties

- https.port `443`

- fitbit2fhir.system.api.port `443`
- fitbit2fhir.system.api.host `fitbit-system-api.host.cloudhub.io`
- fitbit2fhir.system.api.basePath `/api`

- sfdc.system.api.port `80`
- sfdc.system.api.host `crm-system-api.host.cloudhub.io`
- sfdc.system.api.basePath `/api`

- keystore.location `keystore.jks`
- keystore.password `password123`
- key.password `password123`
- key.alias `1`

- api.id `api_id`
- anypoint.platform.client_id `anypoint_platform_client_id`
- anypoint.platform.client_secret `anypoint_platform_client_secret`

+ [Use Case](#usecase)
+ [Considerations](#considerations)
	* [Cloudhub security considerations](#cloudhubsecurityconsiderations)
	* [APIs security considerations](#apissecurityconsiderations)
+ [Run it!](#runit)
	* [Running on premise](#runonopremise)
	* [Running on Studio](#runonstudio)
	* [Running on Mule ESB stand alone](#runonmuleesbstandalone)
	* [Running on CloudHub](#runoncloudhub)
	* [Deploying your Anypoint Template on CloudHub](#deployingyouranypointtemplateoncloudhub)
	* [Creating externally reachable proxy and applying policies](#proxy)
	* [Properties to be configured (With examples)](#propertiestobeconfigured)

# License Agreement <a name="licenseagreement"/>
Note that using this template is subject to the conditions of this [License Agreement](AnypointTemplateLicense.pdf).
Please review the terms of the license before downloading and using this template. In short, you are allowed to use the template for free with Mule ESB Enterprise Edition, CloudHub, or as a trial in Anypoint Studio.

# Use Case <a name="usecase"/>

As a FitBit user I want a microservice to synchronize Device and Observation data between FitBit system and CRM (e.g. Salesforce Health Cloud).

Fitness to CRM Sync Process API is part of the Healthcare Templates Solution. This template calls FitBit System API to register Patient on Fitbit system. After Patient is registered, data are migrated and scheduler once a day retrieve required data from FitBit through the FitBit System API and migrate them to CRM system using the standardized FHIR structures [version 3.0.1 STU3](https://www.hl7.org/FHIR/index.html).

# Considerations <a name="considerations"/>

To make this Anypoint Template run, there are certain preconditions that must be considered. **Failing to do so could lead to unexpected behavior of the template.**
Use Anypoint Studio v7.1.4+ and Mule ESB 4.1.2+ to run this template.

### Register your Fitbit Application

Firstly you need to ensure the developer app is created at http://dev.fitbit.com/ as  the OAuth 2.0 Application Type “Server”. Note that you will need to define the Callback URL too.

### Running the application

Fitbit’s OAuth login has to be initiated from a web-browser.
**https://www.fitbit.com/oauth2/authorize?response_type=code&client_id=<your-client-id>&redirect_uri=<your-redirect-uri>&scope=activity%20profile%20settings%20sleep%20weight&prompt=login** would get you to the login landing page where you will fill in your email and password. After the successful login you will be redirected to the URL specified in the app at http://dev.fitbit.com/. You can notice the access code in the URL.

To register patient to this FitBit account you need to do create the request **GET https://<your-app-domain>.cloudhub.io/patients/{id}/register?code=<your-access-code>** where {id} represents Patient ID, who wants to authorize to FitBit account and access code is the one obtained after login with FitBit credentials.


# Run it! <a name="runit"/>
Simple steps to get Healthcare Fitness to CRM Sync Process API running.
See below.

## Running on premise <a name="runonopremise"/>
In this section we detail the way you should run your Anypoint Template on your computer.

### Where to Download Mule Studio and Mule ESB
First thing to know if you are a newcomer to Mule is where to get the tools.

+ You can download Anypoint Studio from this [Location](http://www.mulesoft.com/platform/studio)
+ You can download Mule ESB from this [Location](http://www.mulesoft.com/platform/soa/mule-esb-open-source-esb)

### Importing an Anypoint Template into Studio
Anypoint Studio offers several ways to import a project into the workspace, for instance:

+ Anypoint Studio Project from File System
+ Packaged mule application (.jar)

You can find a detailed description on how to do so in this [Documentation Page](http://www.mulesoft.org/documentation/display/current/Importing+and+Exporting+in+Studio).

### Running on Studio <a name="runonstudio"/>
Once you have imported you Anypoint Template into Anypoint Studio you need to follow these steps to run it:

+ Generate keystore and set up the truststore (You can find a detailed description on how to do so in this [Documentation Page](https://docs.mulesoft.com/mule4-user-guide/v/4.1/tls-configuration#keystores-and-truststores))
+ Locate the properties file `mule.dev.properties`, in src/main/resources
+ Complete all the properties required as per the examples in the section [Properties to be configured](#propertiestobeconfigured)
+ Once that is done, right click on you Anypoint Template project folder
+ Hover you mouse over `"Run as"`
+ Click on  `"Mule Application"`

### Running on Mule ESB stand alone <a name="runonmuleesbstandalone"/>
Fill in all the properties in one of the property files, for example in [mule.prod.properties](../master/src/main/resources/mule.prod.properties) and run your app with the corresponding environment variable to use it. To follow the example, this will be `mule.env=prod`.

## Running on CloudHub <a name="runoncloudhub"/>
While [creating your application on CloudHub](https://docs.mulesoft.com/runtime-manager/hello-world-on-cloudhub) (Or you can do it later as a next step), you need to go to `"Manage Application"` > `"Properties"` to set all environment variables detailed in **Properties to be configured**.
Follow other steps defined [here](#runonpremise) and once your app is all set and started, there is no need to do anything else.

### Deploying your Anypoint Template on CloudHub <a name="deployingyouranypointtemplateoncloudhub"/>
Anypoint Studio provides you with really easy way to deploy your Template directly to CloudHub, for the specific steps to do so please check this [link](http://www.mulesoft.org/documentation/display/current/Deploying+Mule+Applications#DeployingMuleApplications-DeploytoCloudHub)

## Properties to be configured (With examples) <a name="propertiestobeconfigured"/>
In order to use this Mule Anypoint Template you need to configure properties (APIs, Credentials, API Autodiscovery, etc.) either in properties file or in CloudHub as Environment Variables. The Fitbit System API is using secured connection. Detail list with examples:
### Application properties
+ https.port `443`

+ fitbit2fhir.system.api.port `443`
+ fitbit2fhir.system.api.host `fitbit-system-api.host.cloudhub.io`
+ fitbit2fhir.system.api.basePath `/api`

+ sfdc.system.api.port `80`
+ sfdc.system.api.host `crm-system-api.host.cloudhub.io`
+ sfdc.system.api.basePath `/api`

+ keystore.location `keystore.jks`
+ keystore.password `password123`
+ key.password `password123`
+ key.alias `1`

+ api.id `api_id`
+ anypoint.platform.client_id `anypoint_platform_client_id`
+ anypoint.platform.client_secret `anypoint_platform_client_secret`
