## Exercise 5 - Deploy an API Artefact to connect to an S/4HANA OData Service

In this exercise, we will deploy and manage an API Artefact to connect to an S/4HANA Business Partner OData Service. The metadata document for the said OData Service is provided in the ````resources```` folder of this exercise. Download the ````gwsample-metadata.edmx```` file from the resources folder

## Identity the S/4HANA OData Service

As a pre-requisite, we must first identity the S/4HANA OData service that we want to expose and manage as an API Artefact. Luckily, we don't have to look too far and the standard BEP namespace in a S/4HANA system enables standard content that we can use out-of-the-box. 
As can be seen in the screenshot, we will use the stadard GWSAMPLE_BASIC Service. You can see that the Service in Activated.

![](/exercises/ex5/images/ex5_0.png)
As a test, we invoke the $metadata resource and we can already see that the BusinessPartnerSet collection exists.
![](/exercises/ex5/images/ex5_0_1.png)

## Create an API Artefact

## Configure the API Artefact

## Add policies to manage the API Artefact

## Test the API
