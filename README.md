# Template Healthcare SFHC HealthCloud Experience API

# License Agreement

This template is subject to the conditions of the [MuleSoft License Agreement](https://s3.amazonaws.com/templates-examples/AnypointTemplateLicense.pdf). Review the terms of the license before downloading and using this template. You can use this template for free with the Mule Enterprise Edition, CloudHub, or as a trial in Anypoint Studio. 

# Use Case

As a Salesforce Health Cloud user I want a service to request Clinical data from an EHR system to be updated in my Salesforce instance.

This template should serve as a foundation for implementing an API that connects Salesforce Health Cloud with the EHR FHIR System API and EHR to CRM Sync Process API that are provided as part of the Healthcare Templates Solution. The API is defined using [RAML](https://docs.mulesoft.com/anypoint-platform-for-apis/walkthrough-design-existing#about-raml) and this implementation uses [APIkit](https://docs.mulesoft.com/apikit/4.x/apikit-4-index). SFHC Experience API triggers clinical data migration from the underlying microservices defined in EHR FHIR System API in JSON (FHIR specification [version 3.0.1 (STU)](http://hl7.org/fhir/)).

SFHC Experience API is part of the Healthcare Templates Solution and it is interconnected with EHR FHIR System API(used for retrieving EHR data) and EHR to CRM Sync Process API(used for migrating Clinical data in SFHC Health Cloud). However it is designed to be exposed externally and triggered by SFDC Health Cloud.

# Considerations

To make this Anypoint Template run, there are certain preconditions that must be considered. Failing to do so could lead to unexpected behavior of the template.

## API Security Considerations
This Experience API is meant to be deployed to CloudHub and managed using the API Manager.

### Expose External Endpoints with HTTP
- Trigger using SFHC Health Cloud over HTTP

### Expose Internal Endpoints with RAML and HTTP
- Interconnect internally with EHR to CRM Sync Process API and EHR FHIR System API, which are deployed within  CloudHub.

# Run it!
Simple steps to get Healthcare SFHC Experience API running.

## Running On Premises
In this section we detail the way you should run your Anypoint Template on your computer.


### Where to Download Anypoint Studio and the Mule Runtime

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

### Run with Mule Stand Alone

Complete all properties in one of the property files, for example in `mule.prod.properties` and run your app with the corresponding environment variable to use it. To follow the example, use `mule.env=prod`.

## Run in CloudHub
After adding your application to Runtime Manager, go to **Manage Application** > **Properties** to set the environment variables listed in the "Properties to Configure" section.

### Deploy in CloudHub

In Studio, right click your project name in Package Explorer and select **Anypoint Platform** > **Deploy on CloudHub**.

## Properties to Configure
To use this template, you need to configure properties (Credentials, configurations, etc.) either in properties file or in CloudHub as Environment Variables. 

### Application Properties

#### HTTP Configuration

- http.port `8081`

#### EHR2FHIR System API Configuration

- ehr2fhir.system.api.host `api_ehr_hostname`
- ehr2fhir.system.api.port `8081` 
- ehr2fhir.system.api.basePath `/api`

#### EHR2CRM Process API configuration

- ehr2crm.process.api.host `api_ehr2crm_hostname`
- ehr2crm.process.api.port `8081` 
- ehr2crm.process.api.basePath `/api`
- ehr2crm.process.api.protocol `HTTP`
