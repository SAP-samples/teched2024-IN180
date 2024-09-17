## Exercise 5 - Deploy an API Artefact to connect to an S/4HANA OData Service

In this exercise, we will deploy and manage an API Artefact to connect to an S/4HANA Business Partner OData Service. The metadata document for the said OData Service is provided in the ````resources```` folder of this exercise. Download the ````gwsample-metadata.edmx```` file from the resources folder

## Identity the S/4HANA OData Service

As a pre-requisite, we must first identity the S/4HANA OData service that we want to expose and manage as an API Artefact. Luckily, we don't have to look too far and the standard BEP namespace in a S/4HANA system enables standard content that we can use out-of-the-box. 
As can be seen in the screenshot, we will use the stadard GWSAMPLE_BASIC Service. You can see that the Service in Activated.

![](/exercises/ex5/images/ex5_0.png)
As a test, we invoke the $metadata resource and we can already see that the BusinessPartnerSet collection exists.
![](/exercises/ex5/images/ex5_0_1.png)

## Create an API Artefact
![](/exercises/ex5/images/ex5_1.png)

![](/exercises/ex5/images/ex5_2.png)

![](/exercises/ex5/images/ex5_3.png)

![](/exercises/ex5/images/ex5_4.png)

![](/exercises/ex5/images/ex5_5.png)

![](/exercises/ex5/images/ex5_6.png)

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
