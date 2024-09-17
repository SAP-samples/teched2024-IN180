## Exercise 5 - Deploy an API Artefact to connect to an S/4HANA OData Service

In this exercise, we will deploy and manage an API Artefact to connect to a S/4HANA Business Partner OData Service. The metadata document for the said OData Service is provided in the ````resources```` folder of this exercise. Download the ````gwsample-metadata.edmx```` file from the resources folder

## Identity the S/4HANA OData Service

As a pre-requisite, we must first identify the S/4HANA OData service we want to expose and manage as an API Artefact. Luckily, we don't have to look too far and the standard BEP namespace in a S/4HANA system enables standard content that we can use out of the box. 
As seen in the screenshot, we will use the standard GWSAMPLE_BASIC Service. You can see that the Service is in an Activated state.
![](/exercises/ex5/images/ex5_0.png)

As a test, we invoke the $metadata resource and can already see that the BusinessPartnerSet collection exists. 
![](/exercises/ex5/images/ex5_0_1.png)
> [!NOTE]
> The backend endpoint shown in the picture above can only be accessed in a network that the S/4HANA Onpremise system is installed into. 
> 

## Create an API Artefact
In this section, let us head back to the Integration Suite UI and deploy the 'API' artifact.

Go to the 'Integrations and API' section in the 'Design' tab. Get into the Package you previously created in Exercise 4. Go to the 'Artifacts' sub-tab and click 'Edit'.
![](/exercises/ex5/images/ex5_1.png)

Click on 'Add' in the header region and select 'API'.
![](/exercises/ex5/images/ex5_2.png)

In the 'Create API' dialog, select the 'Edge Integration Cell' from the Runtime Profile drop-down. Click on Next.
![](/exercises/ex5/images/ex5_3.png)

There are multiple entry points to indicate the backend Service we want to manage as an API. Select 'URL' to proceed with the exercise and click 'Next'.
![](/exercises/ex5/images/ex5_4.png)

Enter the following values as inputs for the 'API Details'.
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

![](/exercises/ex5/images/ex5_5.png)

Once the API is created, you will be taken to the 'Overview' tab. Verify your inputs and head over to the 'Resources' tab.
![](/exercises/ex5/images/ex5_6.png)

Take a moment to familiarize yourself with the auto-generated Swagger UI / Open API specification rendition of Resources, Operations, and the corresponding documentation snippets.
![](/exercises/ex5/images/ex5_7.png)

## Configure the API Artefact
Now that the API is created, in this section we will configure the properties.

Double-click anywhere on the API edition screen to launch the property editor sheet.
![](/exercises/ex5/images/ex5_8.png)

Verify that the property editor screen shows up.
![](/exercises/ex5/images/ex5_9.png)

Notice that the system has added an ODATA2 Sender Adapter and an ODATA Reciever Adapter connecting the Client and the Target respectively. 
![](/exercises/ex5/images/ex5_10.png)

Click on 'Edit' to start editing.
![](/exercises/ex5/images/ex5_11.png)

In the 'Connection' sub-pane, make sure you change the Authentication from 'None to 'Basic'. Enter `s4hanacredentials` as the value in the 'Credential Name' text box. You may verify subsequently that within the Security Material section, we have already created a Basic Authentication credential needed to access the S/4HANA OData Service. 
![](/exercises/ex5/images/ex5_12.png)

Next, Click on the 'Authentication' step. Verify that the 'Client Certificate' and 'OAuth' are selected. 
> [!NOTE]
> Add 'Basic Authentication' to the supported type optionally if it is cumbersome to set up OAuth client credentials in the client tool (e.g. Postman) that you intend to test with, in the following section. 
>
![](/exercises/ex5/images/ex5_13.png)

![](/exercises/ex5/images/ex5_14.png)

## Add policies to manage the API Artefact

![](/exercises/ex5/images/ex5_15.png)

![](/exercises/ex5/images/ex5_16.png)

![](/exercises/ex5/images/ex5_17.png)

![](/exercises/ex5/images/ex5_18.png)

![](/exercises/ex5/images/ex5_19.png)

![](/exercises/ex5/images/ex5_20.png)

![](/exercises/ex5/images/ex5_21.png)

![](/exercises/ex5/images/ex5_22.png)


## Test the API
