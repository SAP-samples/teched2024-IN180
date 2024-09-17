## Exercise 5 - Deploy an API Artefact to connect to an S/4HANA OData Service

In this exercise, we will deploy and manage an API Artefact to connect to an S/4HANA Business Partner OData Service. The metadata document for the said OData Service is provided in the ````resources```` folder of this exercise. Download the ````gwsample-metadata.edmx```` file from the resources folder

## Identity the S/4HANA OData Service

As a pre-requisite, we must first identity the S/4HANA OData service that we want to expose and manage as an API Artefact. Luckily, we don't have to look too far and the standard BEP namespace in a S/4HANA system enables standard content that we can use out-of-the-box. 
As can be seen in the screenshot, we will use the stadard GWSAMPLE_BASIC Service. You can see that the Service in Activated.
![](/exercises/ex5/images/ex5_0.png)

As a test, we invoke the $metadata resource and we can already see that the BusinessPartnerSet collection exists. 
![](/exercises/ex5/images/ex5_0_1.png)
> [!NOTE]
> The backend endpoint shown in the picture above can only be accessed from a network that the S/4HANA Onpremise system is installed in. 
> 

## Create an API Artefact
In this section, let us get back to the Integration Suite UI and deploy the 'API' artifact.

Go to the 'Integrations and API' section in the 'Design' tab. Get into the Package you previously created in Excerise 4. Go to the 'Artifacts' sub-tab and click 'Edit'.
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
| Name | Teched2023 API Artifact userxx |
| ID | Teched2023 API Artifact userxx |
| URL | https://vhcals4hci.dummy.nodomain:44300/sap/opu/odata/IWBEP/GWSAMPLE_BASIC/ |
| Service Type | ODATA |
| File Name | Browse and select `gwsample-metadata.edmx` |
| API Base Path | /apiuserxx |
| API State (select from dropdown) | Active |
| API Version | 1.0 |
| Runtime Profile (select from dropdown) | Edge Integration Cell - s4hana-onpremise-node |

![](/exercises/ex5/images/ex5_5.png)

Once the API is create, you will be taken to the 'Overview' tab. Verify your inputs and head over the 'Resources' tab.
![](/exercises/ex5/images/ex5_6.png)

Take a moment to familiarize yourself with the auto-generated Swagger UI / Open API specification rendition of Resources, Operations and the corresponding documentation snippets.  
![](/exercises/ex5/images/ex5_7.png)

## Configure the API Artefact

![](/exercises/ex5/images/ex5_8.png)

![](/exercises/ex5/images/ex5_9.png)

![](/exercises/ex5/images/ex5_10.png)

![](/exercises/ex5/images/ex5_11.png)

![](/exercises/ex5/images/ex5_12.png)

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
