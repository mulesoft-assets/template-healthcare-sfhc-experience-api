# Template Healthcare SFDC HealthCloud to FHIR EHR Experience API

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

This template should serve as a foundation for implementing an API that connects Salesforce Health Cloud with the FHIR Process APIs that are provided as part of the Healthcare Templates Solution. The API is defined using [RAML](https://docs.mulesoft.com/anypoint-platform-for-apis/walkthrough-design-existing#about-raml) and this implementation uses [APIkit](https://docs.mulesoft.com/anypoint-platform-for-apis/apikit-basic-anatomy#basic-anatomy). EHR Experience API retrieves data from the microservices defined in FHIR Process APIs in JSON (FHIR specification [version 1.0.2 DSTU2](https://www.hl7.org/FHIR/DSTU2/index.html)) and transforms them to the SFDC HealthCloud structures.

SFDC HealthCloud to FHIR Experience API is part of the Healthcare Templates Solution and it is interconnected with FHIR Process APIs(used for retrieving Clinical data) and EHR System API(used for persisting Clinical data in SFDC Health Cloud). However it is designed to be exposed externally and triggered by SFDC Health Cloud. For this purpose it is using HTTPS endpoint with basic authentication for external calls, HTTPS calls are used to FHIR Process APIs and HTTP calls to EHR System API. For more information see [API Security Considerations](#apissecurityconsiderations).

# Considerations <a name="considerations"/>

To make this Anypoint Template run, there are certain preconditions that must be considered. **Failling to do so could lead to unexpected behavior of the template.**

## Cloudhub security considerations <a name="cloudhubsecurityconsiderations"/>

+ When VPC is configured in a Cloudhub account, two additional **ports** are available **for internal calls: 8091 and 8092**
+ ${http.port} and ${https.port} are still reserved for external endpoints and should not be used for setting internal port values
+ Internal endpoints **can be configured using** proposed placeholders: **${http.internal.port}** and **${https.internal.port}**
+ There is a URL naming convention for **calls between applications within the same VPC: mule-worker-internal-<appname\>.cloudhub.io**
+ **Cloudhub will not replace provided SSL certificates for internal calls**, therefore they should be valid for the mentioned URL naming convention

## APIs security considerations <a name="apissecurityconsiderations"/>
This Experience API is meant to be deployed to CloudHub and managed using the API Platform Manager.

### Exposing external endpoints with HTTPS and basic authentication
+ It is triggered by SFDC Health Cloud using HTTPS
+ It is secured using basic authentication policy on API Platform. For more information see [Applying policies on API Platform](#applyingpolicies).

### Exposing internal endpoints with RAML and HTTPS
+ It is interconnected internally with FHIR Process APIs, which are deployed within a CloudHub VPC.

# Run it! <a name="runit"/>
Simple steps to get Healthcare SFDC HealthCloud to FHIR EHR Experience API running.
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

+ Generate keystore and truststore (You can find a detailed description on how to do so in this [Documentation Page](https://docs.mulesoft.com/mule-user-guide/v/3.7/tls-configuration#generating-keystores-and-truststores))
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
In order to use this Mule Anypoint Template you need to configure properties (Credentials, configurations, etc.) either in properties file or in CloudHub as Environment Variables. Detailed list with examples:
### Application properties



####API Platform Organization

####API calls configuration

