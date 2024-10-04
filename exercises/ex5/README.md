## Exercise 5 - Deploy an API Artefact to connect to an S/4HANA OData Service

In this exercise, we will deploy and manage an API Artefact to connect to a S/4HANA Business Partner OData Service. The metadata document for the said OData Service is provided in the ````resources```` folder of this exercise. Download the ````gwsample-metadata.edmx```` file from the resources folder

## Identity the S/4HANA OData Service

As a prerequisite, we must first identify the S/4HANA OData service we want to expose and manage as an API Artefact. Luckily, we don't have to look too far and the standard BEP namespace in a S/4HANA system enables standard content that we can use out of the box. 
> [!NOTE]
> Access to an onpremise S/4HANA system has not been provided as part of this TechEd exercise. The screenshot here is just for your information. 
> 
As seen in the screenshot, we will use the standard GWSAMPLE_BASIC Service. You can see that the Service is in an Activated state.

![](/exercises/ex5/images/ex5_0.png)

<br>As a test, we invoke the $metadata resource and can already see that the BusinessPartnerSet collection exists. 

![](/exercises/ex5/images/ex5_0_1.png)
> [!NOTE]
> The backend endpoint shown in the picture above can only be accessed in a network that the S/4HANA Onpremise system is installed into. 
> 

## Create an API Artefact
In this section, let us head back to the Integration Suite UI and deploy the 'API' artifact.

Go to the 'Integrations and API' section in the 'Design' tab. Get into the Package you previously created in Exercise 4. Go to the 'Artifacts' sub-tab and click 'Edit'.

![](/exercises/ex5/images/ex5_1.png)

<br>Click on 'Add' in the header region and select 'API'.

![](/exercises/ex5/images/ex5_2.png)

<br>In the 'Create API' dialog, select the 'Edge Integration Cell' from the Runtime Profile drop-down. Click on Next.

![](/exercises/ex5/images/ex5_3.png)

<br>There are multiple entry points to indicate the backend Service we want to manage as an API. Select 'URL' to proceed with the exercise and click 'Next'.

![](/exercises/ex5/images/ex5_4.png)

<br>Enter the following values as inputs for the 'API Details'.
| Field | Value |
| ----- | ----- |
| Name | BusinessPartnerAPI_UserXX (prefer to indicate your user name here) |
| ID | BusinessPartnerAPI_UserXX |
| URL | https://vhcals4hci.dummy.nodomain:44300/sap/opu/odata/IWBEP/GWSAMPLE_BASIC/ |
| Service Type | ODATA |
| File Name | Browse and select `gwsample-metadata.edmx` |
| API Base Path | /businesspartnerapi/user_XX |
| API State (select from dropdown) | Active |
| API Version | 1.0 |
| Runtime Profile (select from dropdown) | Edge Integration Cell - s4hana-onpremise-node |

<br>![](/exercises/ex5/images/ex5_5.png)

<br>Once the API is created, you will be taken to the 'Overview' tab. Verify your inputs and head over to the 'Resources' tab.

![](/exercises/ex5/images/ex5_6.png)

<br>Take a moment to familiarize yourself with the auto-generated Swagger UI / Open API specification rendition of Resources, Operations, and the corresponding documentation snippets.

![](/exercises/ex5/images/ex5_7.png)

## Configure the API Artefact
Now that the API is created, in this section we will configure the properties.

Double-click anywhere on the API edition screen to launch the policy editor sheet.

![](/exercises/ex5/images/ex5_8.png)

<br>Verify that the property editor screen shows up.

![](/exercises/ex5/images/ex5_9.png)

<br>Notice that the system has added an ODATA2 Sender Adapter and an ODATA Reciever Adapter connecting the Client and the Target respectively. 

![](/exercises/ex5/images/ex5_10.png)

<br>Click on 'Edit' to start editing. Select the OData adapter on the receiver side.

![](/exercises/ex5/images/ex5_11.png)

<br>Click on the `OData` Adapter that connects to the Reciver(Target) system. In the 'Connection' sub-pane, make sure you change the Authentication from 'None to 'Basic'. Enter `s4hanacredentials` as the value in the 'Credential Name' text box. You may verify subsequently that within the Security Material section, we have already created a Basic Authentication credential needed to access the S/4HANA OData Service. 

![](/exercises/ex5/images/ex5_12.png)

<br>Next, Click on the 'Authentication' step. Verify that the 'Client Certificate' and 'OAuth' are selected. 
> [!NOTE]
> Add 'Basic Authentication' to the supported type optionally if it is cumbersome to set up OAuth client credentials in the client tool (e.g. Postman) that you intend to test with, in the following section. 
>

![](/exercises/ex5/images/ex5_13.png)

<br>Look for 'Authorization' policy in the 'search and Add a Step' text area. In the next set of steps, we will add the policies to manage the behavior of the API.

![](/exercises/ex5/images/ex5_14.png)

## Add policies to manage the API Artefact

Drag and add the 'Authorization' policy step after the 'Authentication' step and before the 'Request-Reply' step. In the 'Scope' region within the Policy Settings sub-tab, add a scope called `APIArtifactUser`

![](/exercises/ex5/images/ex5_15.png)

<br>At this point, note that we have already created a User Role with the 'APIArtifactUser' name within the Tenant Administration settings page. To inspect this, launch a new browser window, head over to the 'Monitor' tab -> Integration and APIs section. Click on the 'User Roles' tile.

![](/exercises/ex5/images/ex5_2_1.png)

<br>Notice that 'APIArtifactUser' exists as a user role in addition to the default 'ESBMessaging.send'. 

![](/exercises/ex5/images/ex5_2_2.png)

<br>Head back the API artifact and click on (+) to add a flow step after the 'Authorization' step.

![](/exercises/ex5/images/ex5_2_base.png)

<br>Add a 'Surge Protection' policy step from the canvas.

![](/exercises/ex5/images/ex5_2_3.png)

<br>Click on the step and it opens up the property sheet. Protect against a surge of '10' calls within a duration of '60' 'seconds' of duration unit.

![](/exercises/ex5/images/ex5_2_4.png)

<br> Next, let's add a quota policy to assign a call quota to unique clients. Click on (+) to add a flow step after the 'SurgeProtection' step. 

![](/exercises/ex5/images/ex5_2_5.png)

<br>Select the quota policy, and under Policy Settings, fill in the details shown in the screenshot below. For the start time, click on the data picker and select a date that is prior to the current timestamp. We assign the caller a quota of 5 calls within a minute's duration. Note that this value is lesser than the 'surge' we protected against in the previous step. Enter Quota Identifier as `${request.header['X-Forwarded-For']}`. 

<br>This identifier needs to resolve to a value that is unique to the caller, hence we have resorted to the 'x-forwarded-for' header, which has the details of the originating IP.
Though we don't show this explicity in the exercise, during the setup time, we did enable the option to retain the client IP in the request header.

<br>Save and deploy the API.

![](/exercises/ex5/images/ex5_2_6.png)

<br>Select Yes on the confirmation dialog.

![](/exercises/ex5/images/ex5_20.png)

<br>Status of the artifact should be  STARTED

![](/exercises/ex5/images/ex5_21.png)

<br>Navigate back to the Monitor -> Integrations and APIs. Select **Manage Integration Content** tile and then Select Runtime as **Edge Integration Cell**. Your deployed Integration flow should be in started state. Copy the API Endpoint URL.

![](/exercises/ex5/images/ex5_22.png)


## Test the API
Now that the API is deployed, in this section we will Test the API and adjust the policies to handle a unique situation we will discover during testing.

We will continue using Bruno for testing, the tool used in ex4 as well. Create a New Request. 

![](/exercises/ex5/images/ex5_1_1.png)

<br>Give the Request a name. Let's call it 'BusinessPartnerAPI' and and paste the API URL copied from the previous step. Select the 'GET' Operation.

![](/exercises/ex5/images/ex5_1_2.png)

<br>Head over to the 'Auth' section.

![](/exercises/ex5/images/ex5_1_3.png)

<br> Select 'OAuth 2.0' from the auth drop-down.

![](/exercises/ex5/images/ex5_1_4.png)

<br> Now refer back to the TenantBooker app and the credentials we had saved earlier. Copy the Token URL and client credentials for the 'Process Integration' section.

![](/exercises/ex5/images/tenantbooker_1.png)

<br> Select 'Client Credentials' grant type and copy the token URL and client credentials in the respective fields. Invoke the 'Get Access Token' button.

![](/exercises/ex5/images/ex5_1_5.png)

<br> Copy the contents of the `access_token` atribute from the Response section. Make a mental note of the `scope` attribute. It points to 'ESBMessaging.send', the default role mapped to the client credentials.

![](/exercises/ex5/images/ex5_1_6.png)

<br> In the Auth section, change the type  from 'OAuth 2.0' to 'Bearer Token',  paste the access token copied from the previous step and click on the -> Send icon at the right side of the screen.

![](/exercises/ex5/images/ex5_1_7.png)

<br> As expected, you should be presented with a 403 Forbidden HTTP response code with the message stating that authorizations did not match.

![](/exercises/ex5/images/ex5_1_8.png)

![](/exercises/ex5/images/ex5_1_9.png)

![](/exercises/ex5/images/ex5_1_10.png)

![](/exercises/ex5/images/ex5_1_11.png)

![](/exercises/ex5/images/ex5_1_12.png)

![](/exercises/ex5/images/tenantbooker_2.png)

![](/exercises/ex5/images/ex5_1_13.png)

![](/exercises/ex5/images/ex5_1_14.png)

![](/exercises/ex5/images/ex5_2_7.png)

![](/exercises/ex5/images/ex5_2_8.png)

![](/exercises/ex5/images/ex5_2_14.png)

![](/exercises/ex5/images/ex5_2_9.png)

![](/exercises/ex5/images/ex5_2_10.png)

![](/exercises/ex5/images/ex5_2_30.png)

![](/exercises/ex5/images/ex5_2_29.png)

![](/exercises/ex5/images/ex5_2_28.png)

![](/exercises/ex5/images/ex5_2_11.png)

![](/exercises/ex5/images/ex5_2_12.png)

![](/exercises/ex5/images/ex5_2_26.png)

![](/exercises/ex5/images/ex5_2_27.png)

![](/exercises/ex5/images/ex5_2_13.png)

![](/exercises/ex5/images/ex5_2_15.png)

![](/exercises/ex5/images/ex5_2_15.png)

![](/exercises/ex5/images/ex5_2_16.png)

![](/exercises/ex5/images/ex5_2_17.png)

![](/exercises/ex5/images/ex5_2_18.png)

![](/exercises/ex5/images/ex5_2_19.png)

![](/exercises/ex5/images/ex5_2_20.png)

![](/exercises/ex5/images/ex5_2_21.png)

![](/exercises/ex5/images/ex5_2_22.png)

![](/exercises/ex5/images/ex5_2_23.png)

![](/exercises/ex5/images/ex5_2_24.png)

![](/exercises/ex5/images/ex5_2_25.png)

## Summary

Congratulations! You have successfully completed the Exercise **Deploy an API Artefact to connect to an S/4HANA Odata.**

Many congratulations for participating and completing the Teched Jumpstart session **IN180 - Future-proof your SAP PI/PO investments with SAP Integration Suite.** 

