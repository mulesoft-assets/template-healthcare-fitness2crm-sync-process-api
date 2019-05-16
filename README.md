# Template Healthcare Fitness to CRM Sync Process API

# License Agreement

This template is subject to the conditions of the [MuleSoft License Agreement](https://s3.amazonaws.com/templates-examples/AnypointTemplateLicense.pdf). Review the terms of the license before downloading and using this template. You can use this template for free with the Mule Enterprise Edition, CloudHub, or as a trial in Anypoint Studio. 

# Use Case

As a FitBit user I want a microservice to synchronize Device and Observation data between FitBit system and CRM (for example, Salesforce Health Cloud).

Fitness to CRM Sync Process API is part of the Healthcare Templates Solution. This template calls FitBit System API to register Patient on Fitbit system. After Patient is registered, data are migrated and scheduler once a day retrieve required data from FitBit through the FitBit System API and migrate them to CRM system using the standardized FHIR structures [version 3.0.1 STU3](https://www.hl7.org/FHIR/index.html).

# Considerations

To make this Anypoint Template run, there are certain preconditions that must be considered. Failing to do so could lead to unexpected behavior of the template.

Use Anypoint Studio v7.1.4+ and Mule Runtime 4.1.2+ to run this template.

### Register your Fitbit Application

Firstly you need to ensure the developer app is created at http://dev.fitbit.com/ as  the OAuth 2.0 Application Type “Server”. Define the Callback URL too.

### Running the application

Fitbit’s OAuth login has to be initiated from a web browser.

Use:

https://www.fitbit.com/oauth2/authorize?response_type=code&client_id=<your-client-id>&redirect_uri=<your-redirect-uri>&scope=activity%20profile%20settings%20sleep%20weight&prompt=login 
	
This URL gets you to the login landing page where you can fill in your email and password. After the successful login you are redirected to the URL specified in the app at http://dev.fitbit.com/. Note the access code in the URL.

To register patient to this FitBit account you need to do create the request, use:

GET https://<your-app-domain>.cloudhub.io/patients/{id}/register?code=<your-access-code>
	
Where {id} represents the Patient ID of who wants to authorize to FitBit account and access code is the one obtained after login with FitBit credentials.


# Run it!
Simple steps to get Healthcare Fitness to CRM Sync Process API running.


## Run On Premises
In this section we detail the way you should run your Anypoint Template on your computer.

### Where to Download Mule Studio and Mule ESB
If you are new to Mule, download this software:

- [Download Anypoint Studio](https://www.mulesoft.com/platform/studio)
- [Download Mule runtime](https://www.mulesoft.com/lp/dl/mule-esb-enterprise)

### Import Template in Studio

In Studio, click the Exchange X icon in the upper left of the taskbar, log in with your
Anypoint Platform credentials, search for the template, and click **Open**.

### Run in Studio

After opening your template in Anypoint Studio, follow these steps to run it:

1. Locate the properties file `mule.dev.properties`, in src/main/resources.
2. Complete all the properties in the "Properties to Configure" section.
3. Right click the template project folder.
4. Hover your mouse over `Run as`.
5. Click `Mule Application (configure)`.
6. Inside the dialog, select Environment and set the variable `mule.env` to the value `dev`.
7. Click `Run`.

### Run in Mule Stand Alone 
Fill in all the properties in one of the property files, for example in mule.prod.properties and run your app with the corresponding environment variable to use it. To follow the example, use `mule.env=prod`.

## Run in CloudHub
After adding your application to Runtime Manager, go to **Manage Application** > **Properties** to set the environment variables listed in the "Properties to Configure" section.

### Deploy in CloudHub

In Studio, right click your project name in Package Explorer and select **Anypoint Platform** > **Deploy on CloudHub**.

## Properties to Configure
To use this template you need to configure properties (APIs, Credentials, API Autodiscovery, etc.) either in properties file or in CloudHub as Environment Variables. The Fitbit System API is using secured connection. Detail list with examples.
### Application properties
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
