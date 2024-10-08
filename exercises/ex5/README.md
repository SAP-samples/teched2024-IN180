# Exercise 5 - Deploy an API Artifact to connect to an S/4HANA OData Service

In this exercise, we will deploy and manage an API Artifact to connect to a S/4HANA Business Partner OData Service. The metadata document for the said OData Service is provided in the `resources` folder of this exercise. Download the `gwsample-metadata.edmx` file from the resources folder.
<br> Also, you will need a modified version of the OpenAPI spec definition in the YAML format that gets internally generated from the said EDMX file for the API artifact. Download the `gwsample-basic.yaml` file from the [resources](/exercises/ex5/resources) folder.

## Identity the S/4HANA OData Service

As a prerequisite, we must first identify the S/4HANA OData service we want to expose and manage as an API Artifact. Luckily, we don't have to look too far and the standard BEP namespace in a S/4HANA system enables standard content that we can use out of the box.

> [!NOTE]
> Access to an on-premise S/4HANA system has not been provided as part of this TechEd exercise. The screenshot here is just for your information. 

As seen in the screenshot, we will use the standard GWSAMPLE_BASIC Service. You can see that the Service is in an Activated state.

![](/exercises/ex5/images/ex5_0.png)

<br>As a test, we invoke the $metadata resource and can already see that the BusinessPartnerSet collection exists. 

![](/exercises/ex5/images/ex5_0_1.png)
> [!NOTE]
> The backend endpoint shown in the picture above can only be accessed in a network that the S/4HANA Onpremise system is installed into. 
> 

## Create an API Artifact
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

## Configure the API Artifact
Now that the API is created, in this section we will configure the properties.

Double-click anywhere on the API edition screen to launch the policy editor sheet.

![](/exercises/ex5/images/ex5_8.png)

<br>Verify that the property editor screen shows up.

![](/exercises/ex5/images/ex5_9.png)

<br>Notice that the system has added an ODATA2 Sender Adapter and an ODATA Reciever Adapter connecting the Client and the Target respectively. 

![](/exercises/ex5/images/ex5_10.png)

<br>Click on 'Edit' to start editing. Select the OData adapter on the receiver side.

![](/exercises/ex5/images/ex5_11.png)

<br>Click on the `OData` Adapter that connects to the Receiver (Target) system. In the 'Connection' sub-pane, make sure you change the Authentication from 'None to 'Basic'. Enter `s4hanacredentials` as the value in the 'Credential Name' text box. You can verify later that within the Security Material section, we have already created a Basic Authentication credential needed to access the S/4HANA OData Service. 

![](/exercises/ex5/images/ex5_12.png)

<br>Next, Click on the 'Authentication' step. Verify that the 'Client Certificate' and 'OAuth' are selected.
> [!NOTE]
> Add 'Basic Authentication' to the supported type optionally if it is cumbersome to set up OAuth client credentials in the client tool (e.g. Postman) that you intend to test with, in the following section. 
>

![](/exercises/ex5/images/ex5_13.png)

<br>Look for the 'Authorization' policy in the 'Search and Add a Step' text area. In the next set of steps, we will add the policies to manage the behavior of the API.

![](/exercises/ex5/images/ex5_14.png)

## Add policies to manage the API Artifact

Drag and add the 'Authorization' policy step after the 'Authentication' step and before the 'Request-Reply' step. In the 'Scope' region within the Policy Settings sub-tab, add a scope called `APIArtifactUser`

![](/exercises/ex5/images/ex5_15.png)

<br>At this point, note that we have already created a User Role with the 'APIArtifactUser' name within the Tenant Administration settings page. To inspect this, launch a new browser window, and head over to the 'Monitor' tab -> Integration and APIs section. Click on the 'User Roles' tile.

![](/exercises/ex5/images/ex5_2_1.png)

<br>Notice that 'APIArtifactUser' exists as a user role in addition to the default 'ESBMessaging.send'. 

![](/exercises/ex5/images/ex5_2_2.png)

<br>Head back to the API artifact and click on (+) to add a flow step after the 'Authorization' step.

![](/exercises/ex5/images/ex5_2_base.png)

<br>Add a 'Surge Protection' policy step from the canvas.

![](/exercises/ex5/images/ex5_2_3.png)

<br>Click on the step and it opens up the property sheet. Protect against a surge of '10' calls within a duration of '60' 'seconds' of duration unit.

![](/exercises/ex5/images/ex5_2_4.png)

<br> Next, let's add a quota policy to assign a call quota to unique clients. Click on (+) to add a flow step after the 'SurgeProtection' step. 

![](/exercises/ex5/images/ex5_2_5.png)

<br>Select the quota policy, and under Policy Settings, fill in the details shown in the screenshot below. For the start time, click on the data picker and select a date that is before the current timestamp. We assign the caller a quota of 5 calls within one minute's duration. Note that this value is lesser than the 'surge' we protected against in the previous step. Enter Quota Identifier as `${request.header['X-Forwarded-For']}`.

![](/exercises/ex5/images/ex5_2_6.png)

This identifier needs to resolve to a value that is unique to the caller, hence we have resorted to the 'x-forwarded-for' header, which has the details of the originating IP.
Though we don't cover this explicitly in the exercise, during the Edge Integration Cell setup time, we did enable the option to retain the client IP in the request header during Istio configuration. Look at the picture below to see how the configuration screen for the EIC node stands.

![](/exercises/ex5/images/ex5_2_4_4.png)

<br>Save and deploy the API.

<br>Select Yes on the confirmation dialog.

![](/exercises/ex5/images/ex5_20.png)

<br>Status of the artifact should be  STARTED.

![](/exercises/ex5/images/ex5_21.png)

<br>Navigate back to the Monitor -> Integrations and APIs. Select **Manage Integration Content** tile and then Select Runtime as **Edge Integration Cell**. Your deployed Integration flow should be in the 'started' state. Copy the API Endpoint URL.

![](/exercises/ex5/images/ex5_22.png)


## Test the API
Now that the API is deployed, in this section we will Test the API and adjust the policies to handle a unique situation we will discover during testing.

We will continue using Bruno for testing, the tool used in ex4 as well. Create a New Request.

![](/exercises/ex5/images/ex5_1_1.png)

<br>Give the Request a name. Let's call it 'BusinessPartnerAPI' and paste the API URL copied from the previous step. Select the 'GET' Operation.

![](/exercises/ex5/images/ex5_1_2.png)

<br>Head over to the 'Auth' section.

![](/exercises/ex5/images/ex5_1_3.png)

<br> Select 'OAuth 2.0' from the auth drop-down.

![](/exercises/ex5/images/ex5_1_4.png)

<br> Now refer back to the TenantBooker app and the credentials we did save earlier. Copy the Token URL and client credentials for the 'Process Integration' section.

![](/exercises/ex5/images/tenantbooker_1.png)

<br> Select the 'Client Credentials' grant type and copy the token URL and client credentials in the respective fields. Invoke the 'Get Access Token' button.

![](/exercises/ex5/images/ex5_1_5.png)

<br> Copy the contents of the `access_token` atribute from the Response section. Make a mental note of the `scope` attribute. It points to 'ESBMessaging.send', the default role mapped to the client credentials.

![](/exercises/ex5/images/ex5_1_6.png)

<br> In the Auth section, change the type  from 'OAuth 2.0' to 'Bearer Token',  paste the access token copied from the previous step, and click on the -> Send icon at the right side of the screen.

![](/exercises/ex5/images/ex5_1_7.png)

<br> As expected, you should be presented with a 403 Forbidden HTTP response code with the message stating that authorizations did not match.

![](/exercises/ex5/images/ex5_1_8.png)

<br> It's always a good practice to look up the monitoring logs to inspect the exact erroneous steps. Head back to the 'Overview' -> 'Monitoring Message Processing Logs' section in the Integration Suite UI. Look for Failed messages and trace your API.

![](/exercises/ex5/images/ex5_1_9.png)

<br> Click on the 'Info' Log Level link. 

![](/exercises/ex5/images/ex5_1_10.png)

<br> You are led to the 'Authorization' step that failed. 

![](/exercises/ex5/images/ex5_1_11.png)

<br> Click on the 'Log Content' and you can see the actual message stating that it was unable to validate the scope in the token.

![](/exercises/ex5/images/ex5_1_12.png)

<br>Of course, we need to head back to the tenant booker app and now copy the right set of client credentials labeled 'API Management API Access...'

![](/exercises/ex5/images/tenantbooker_2.png)

<br> Hit your testing client again, only this time with the right set of credentials. The scope (APIArtefactUser) attached to the access token will indicate so. 

![](/exercises/ex5/images/ex5_1_13.png)

<br> Bingo, if everything was done correctly up to this point. We have our first success! We are presented with HTTP status code 200 and the OData service document is back as our response payload.

![](/exercises/ex5/images/ex5_1_14.png)

> [!NOTE]
> A word of caution though. Some testing clients (e.g. Postman) could probably report a strange client-side Decompression failed error. The reason for the error is that the client tool was unable to match the content encoding to what it expects. You can see that Postman injects `gzip, deflate, br` within the `Accept-Encoding` header.
> 
> <br> We have a trick later in the exercise to deal with this error using the API Schema validation policy.
> 

![](/exercises/ex5/images/ex5_2_7.png)

For now, to deal with this erroneous situation, a simple fix would be to drop `br` from the `Accept-Encoding` header. Simply pass `gzip, deflate` alone. Doing so should give you a successful response back.

![](/exercises/ex5/images/ex5_2_8.png)

An interesting thing to note is that though Bruno client succeeded in making a request at the `/` root OData service document level, when we append the resource `/BusinessPartnerSet` to our URL segment, we start seeing the same 'Decompression Failure' error message here as well. Notice that this error happens only when the `br` segment is included in the `Accept-Encoding` header.

![](/exercises/ex5/images/ex5_2_14.png)

<br> Again, we resort to our fix to deal with this situation. Simply strip off the `br` segment from the header and you will be back on track.

![](/exercises/ex5/images/ex5_2_9.png)

<br> Now, we are at the point of verifying the 'Quota Policy' step we added to our API. Make > 5 requests to the API within a short span (< 60 seconds). You will eventually violate the quota check and be presented with the `QuotaExceeded` HTTP 429 error code.

![](/exercises/ex5/images/ex5_2_10.png)

<br> Navigate to the 'Header' tab.

![](/exercises/ex5/images/ex5_2_30.png)

<br> Inspect the value of the `x-forwarded-for` header. You should see an IP string that is unique to your Client from where the request was dispatched.

![](/exercises/ex5/images/ex5_2_29.png)

<br> A simple step would be to go to any IP reporting website and match the value of the header with that of the IP of your client machine.

![](/exercises/ex5/images/ex5_2_28.png)

<br> In the next step, we will connect to a VPN device (instead of direct internet) to make a request. Of course, this step is optional and makes sense only if you have the means to connect to a different Internet Gateway. 

![](/exercises/ex5/images/ex5_2_11.png)

<br> Right after the network switch and within the timespan of a minute, make a few calls to the API and you will no longer see the Quota errors. That's because you will recall that we used the `x-forwarded-for` header as the attribute in the policy to uniquely discern between calls for quota determination. 

![](/exercises/ex5/images/ex5_2_12.png)

<br> To make sure that this indeed is the case, make a note of your newly assigned IP after the network switch.

![](/exercises/ex5/images/ex5_2_26.png)

<br> Go to the 'Headers' section of your testing client and match the value of the new IP with the `x-forwarded-for` header.

![](/exercises/ex5/images/ex5_2_27.png)

<br> Great going so far! Continue making a few more requests in the same short period and now you are presented with a `surgeProtecttionLimitExceeded` failure. This is different from the Quota error we faced earlier. You will recall that we placed a surge protection policy before the quota step could be inspected. Given that now we have had 2 sets of IPs calling the same API 5 times each, the surge protection kicks in. 

![](/exercises/ex5/images/ex5_2_13.png)

<br>So far so good. Now let us elegantly handle the `Accept-Encoding` header error by ensuring the Client always passes the right value. 
<br>One way to do this would be to make this definition part of the API schema itself. To do so, let us head back to the API and click 'Edit'.

![](/exercises/ex5/images/ex5_2_15.png)

<br> Click on 'Switch to API Specification'.

![](/exercises/ex5/images/ex5_2_16.png)

<br> This opens up the OpenAPI spec file. 
<br>Take a backup of this file in your local file system. Make sure you copy the `title` and `url` attributes from the Spec file as indicated in the screenshot. You will need this in the next step.

![](/exercises/ex5/images/ex5_2_17.png)

<br> Clear the text area and paste the contents of the `gwsample-basic.YAML` file you downloaded earlier from the [resources](/exercises/ex5/resources) folder.
<br> Make sure to paste back the values of the `title` and `url` attributes from your original spec file.

![](/exercises/ex5/images/ex5_2_18.png)

<br> Pay close attention to the snippet in the enhanced YAML. You will see that we have a new segment for the `Accept-Encoding` header that accepts values only specified in the containing `enum`. We accept `gzip`, `deflate`, and a combination of both these together. We have eliminated `br`. 
<br> Save the definition and 'Switch to API Details'.

![](/exercises/ex5/images/ex5_2_19.png)

<br> Navigate to the 'Policies' tab.

![](/exercises/ex5/images/ex5_2_20.png)

<br> Click on (+) to add a new policy flow step after the 'Authorization' step.

![](/exercises/ex5/images/ex5_2_21.png)

<br> Add the 'API Validation' flow step.

![](/exercises/ex5/images/ex5_2_22.png)

<br> Click and open the Property page section of the step. Check the 'Headers' box. We can leave the others unchecked. This enforces the validation of the HTTP headers in an incoming client request. 
<br> Save the changes and 'Deploy'.

![](/exercises/ex5/images/ex5_2_23.png)

<br> Head back to your testing client and make a request with the `Accept-Encoding` value as `gzip, deflate, br`.
You should see a failure message coming from the API Validation step.

![](/exercises/ex5/images/ex5_2_24.png)

<br> Strip off `br` from the header and make a new request. You should see the call getting successfully executed. 

![](/exercises/ex5/images/ex5_2_25.png)

## Troubleshooting tips

Here are few common pitfalls to avoid.

<br>Do you see a 500 Internal Server Error like so? If that's the case, chances are that you haven't copied over the Open API Spec file (and have just manually enhanced the OpenAPI spec definitions.)

![](/exercises/ex5/images/ex5_2_4_3.png)

> [!TIP]
> Though this is not covered in the scope of this hands-on exercise, a recommended step for troubleshooting would be to look at the Grafana Logging dashboard, for additional insights. This is accessible from the Edge Lifecycle Management page.
> 
![](/exercises/ex5/images/ex5_2_4_1.png)


> [!TIP]
> A Look at the policyengine logs from the `edge-icell` namespace tells us that the internal server error was caused due to incorrect typecasting between INT and Float values from the OpenAPI Spec file.
> 
![](/exercises/ex5/images/ex5_2_4_2.png)

## Summary

Congratulations! You have successfully completed the Exercise **Deploy an API Artefact to connect to an S/4HANA Odata.**

Many congratulations for participating and completing the Teched Jumpstart session **IN180 - Future-proof your SAP PI/PO investments with SAP Integration Suite.** 

