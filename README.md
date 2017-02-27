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
	* [Applying policies on CloudHub](#applyingpolicies)
	* [Properties to be configured (With examples)](#propertiestobeconfigured)

# License Agreement <a name="licenseagreement"/>
Note that using this template is subject to the conditions of this [License Agreement](AnypointTemplateLicense.pdf).
Please review the terms of the license before downloading and using this template. In short, you are allowed to use the template for free with Mule ESB Enterprise Edition, CloudHub, or as a trial in Anypoint Studio.

# Use Case <a name="usecase"/>

As a Salesforce Health Cloud user I want a service to request Clinical data from an EHR system to be updated in my Salesforce instance.

This template should serve as a foundation for implementing an API that connects Salesforce Health Cloud with the EHR FHIR System API and EHR to CRM Sync Process API that are provided as part of the Healthcare Templates Solution. The API is defined using [RAML](https://docs.mulesoft.com/anypoint-platform-for-apis/walkthrough-design-existing#about-raml) and this implementation uses [APIkit](https://docs.mulesoft.com/anypoint-platform-for-apis/apikit-basic-anatomy#basic-anatomy). SFHC Experience API triggers clinical data migration from the underlying microservices defined in EHR FHIR System API in JSON (FHIR specification [version 1.0.2 DSTU2](https://www.hl7.org/FHIR/DSTU2/index.html)).

SFHC Experience API is part of the Healthcare Templates Solution and it is interconnected with EHR FHIR System API(used for retrieving EHR data) and EHR to CRM Sync Process API(used for migrating Clinical data in SFHC Health Cloud). However it is designed to be exposed externally and triggered by SFDC Health Cloud.

# Considerations <a name="considerations"/>

To make this Anypoint Template run, there are certain preconditions that must be considered. **Failling to do so could lead to unexpected behavior of the template.**

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
Mule Studio offers several ways to import a project into the workspace, for instance: 

+ Anypoint Studio generated Deployable Archive (.zip)
+ Anypoint Studio Project from External Location
+ Maven-based Mule Project from pom.xml
+ Mule ESB Configuration XML from External Location

You can find a detailed description on how to do so in this [Documentation Page](http://www.mulesoft.org/documentation/display/current/Importing+and+Exporting+in+Studio).

### Running on Studio <a name="runonstudio"/>
Once you have imported you Anypoint Template into Anypoint Studio you need to follow these steps to run it:

+ Locate the properties file `mule-<env>.properties`, in src/main/app/resources
+ Complete all the properties required as per the examples in the section [Properties to be configured](#propertiestobeconfigured)
+ Once that is done, right click on you Anypoint Template project folder 
+ Hover you mouse over `"Run as"`
+ Click on  `"Mule Application"`

### Running on Mule ESB stand alone <a name="runonmuleesbstandalone"/>
Complete all properties in one of the property files, for example in [mule.prod.properties](../master/src/main/resources/mule.prod.properties) and run your app with the corresponding environment variable to use it. To follow the example, this will be `mule.env=prod`. 

## Running on CloudHub <a name="runoncloudhub"/>
While [creating your application on CloudHub](http://www.mulesoft.org/documentation/display/current/Hello+World+on+CloudHub) (Or you can do it later as a next step), you need to go to `"Manage Application"` > `"Properties"` to set all environment variables detailed in **Properties to be configured**.
Follow other steps defined [here](#runonpremise) and once your app is all set and started, there is no need to do anything else.

### Deploying your Anypoint Template on CloudHub <a name="deployingyouranypointtemplateoncloudhub"/>
Mule Studio provides you with really easy way to deploy your Template directly to CloudHub, for the specific steps to do so please check this [link](http://www.mulesoft.org/documentation/display/current/Deploying+Mule+Applications#DeployingMuleApplications-DeploytoCloudHub)

### Applying policies on CloudHub <a name="applyingpolicies"/>
When a Mule application is deployed using the Mule API Gateway Runtime, the API Platform allows to dinamically apply different policies that can be used for securizing the application, among many other cases. More information can be found in [Anypoint Platform for APIs](https://docs.mulesoft.com/anypoint-platform-for-apis/applying-runtime-policies)

## Properties to be configured (With examples) <a name="propertiestobeconfigured"/>
In order to use this Mule Anypoint Template you need to configure properties (Credentials, configurations, etc.) either in properties file or in CloudHub as Environment Variables. To run the MUnit tests, the configuration file is located in the [mule.test.properties](../src/test/resources/mule.test.properties). Detailed list with examples:
### Application properties

####HTTP configuration
+ http.port `8081`

####API calls configuration

+ api.ehr.host `api_ehr_hostname`
+ api.ehr.basepath `/api`
+ api.ehr.port `8081`

+ api.ehr2crm.host `api_ehr2crm_hostname`
+ api.ehr2crm.basepath `/api`
+ api.ehr2crm.port `8082`

