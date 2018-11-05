# Template Healthcare SFHC HealthCloud Experience API

+ [License Agreement](#licenseagreement)
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
	* [Properties to be configured (With examples)](#propertiestobeconfigured)

# License Agreement <a name="licenseagreement"/>
Note that using this template is subject to the conditions of this [License Agreement](AnypointTemplateLicense.pdf).
Please review the terms of the license before downloading and using this template. In short, you are allowed to use the template for free with Mule ESB Enterprise Edition, CloudHub, or as a trial in Anypoint Studio.

# Use Case <a name="usecase"/>

As a Salesforce Health Cloud user I want a service to request Clinical data from an EHR system to be updated in my Salesforce instance.

This template should serve as a foundation for implementing an API that connects Salesforce Health Cloud with the EHR FHIR System API and EHR to CRM Sync Process API that are provided as part of the Healthcare Templates Solution. The API is defined using [RAML](https://docs.mulesoft.com/anypoint-platform-for-apis/walkthrough-design-existing#about-raml) and this implementation uses [APIkit](https://docs.mulesoft.com/apikit/4.x/apikit-4-index). SFHC Experience API triggers clinical data migration from the underlying microservices defined in EHR FHIR System API in JSON (FHIR specification [version 3.0.1 (STU)](http://hl7.org/fhir/)).

SFHC Experience API is part of the Healthcare Templates Solution and it is interconnected with EHR FHIR System API(used for retrieving EHR data) and EHR to CRM Sync Process API(used for migrating Clinical data in SFHC Health Cloud). However it is designed to be exposed externally and triggered by SFDC Health Cloud.

# Considerations <a name="considerations"/>

To make this Anypoint Template run, there are certain preconditions that must be considered. **Failing to do so could lead to unexpected behavior of the template.**

## APIs security considerations <a name="apissecurityconsiderations"/>
This Experience API is meant to be deployed to CloudHub and managed using the API Platform Manager.

### Exposing external endpoints with HTTP
+ It is triggered by SFHC Health Cloud using HTTP

### Exposing internal endpoints with RAML and HTTP
+ It is interconnected internally with EHR to CRM Sync Process API and EHR FHIR System API, which are deployed within a CloudHub.

# Run it! <a name="runit"/>
Simple steps to get Healthcare SFHC Experience API running.
See below.

## Running on premise <a name="runonopremise"/>
In this section we detail the way you should run your Anypoint Template on your computer.


### Where to Download Mule Studio and Mule ESB
First thing to know if you are a newcomer to Mule is where to get the tools.

+ You can download Mule Studio from this [Location](http://www.mulesoft.com/platform/mule-studio)
+ You can download Mule ESB from this [Location](http://www.mulesoft.com/platform/soa/mule-esb-open-source-esb)

### Importing an Anypoint Template into Studio
Anypoint Studio offers several ways to import a project into the workspace, for instance: 

+ Anypoint Studio Project from File System
+ Packaged mule application (.jar)

You can find a detailed description on how to do so in this [Documentation Page](https://docs.mulesoft.com/studio/7.2/import-export-packages).

### Running on Studio <a name="runonstudio"/>
Once you have imported you Anypoint Template into Anypoint Studio you need to follow these steps to run it:

+ Locate the properties file `mule-<env>.properties`, in src/main/app/resources
+ Complete all the properties required as per the examples in the section [Properties to be configured](#propertiestobeconfigured)
+ Once that is done, right click on you Anypoint Template project folder 
+ Hover you mouse over `"Run as"`
+ Click on  `"Mule Application"`

### Running on Mule ESB stand alone <a name="runonmuleesbstandalone"/>
Complete all properties in one of the property files, for example in mule.prod.properties, and run your app with the corresponding environment variable to use it. To follow the example, this will be `mule.env=prod`. 

## Running on CloudHub <a name="runoncloudhub"/>
While creating your application on CloudHub (or you can do it later as a next step), go to Runtime Manager > Manage Application > Properties to set the environment variables listed in "Properties to Configure" as well as the mule.env.
Follow other steps defined [here](#runonpremise) and once your app is all set and started, there is no need to do anything else.

### Deploying your Anypoint Template on CloudHub <a name="deployingyouranypointtemplateoncloudhub"/>
Mule Studio provides you with really easy way to deploy your Template directly to CloudHub, for the specific steps to do so please check this [link](https://docs.mulesoft.com/runtime-manager/deploying-to-cloudhub)

## Properties to be configured (With examples) <a name="propertiestobeconfigured"/>
In order to use this Mule Anypoint Template you need to configure properties (Credentials, configurations, etc.) either in properties file or in CloudHub as Environment Variables. Detailed list with examples:
### Application properties

####HTTP configuration
+ http.port `8081`

####EHR2FHIR System API configuration
+ ehr2fhir.system.api.host `api_ehr_hostname`
+ ehr2fhir.system.api.port `8081` 
+ ehr2fhir.system.api.basePath `/api`

####EHR2CRM Process API configuration
+ ehr2crm.process.api.host `api_ehr2crm_hostname`
+ ehr2crm.process.api.port `8081` 
+ ehr2crm.process.api.basePath `/api`
+ ehr2crm.process.api.protocol `HTTP`