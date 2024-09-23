# Exercise 2 - SAP Process Integration walkthrough

In this exercise, you will

- take a virtual walkthrough of a SAP Process Integration system and look at an ICO (Integration Configuration Object) definition of an interface that exposes a simple SOAP-to-SOAP Integration.
- note that there is no hands-on for this exercise as there are logistical challenges in enabling each participant to access an onpremise system, so we have decided to enable a virtual walkthrough by looking at screenshots alone.

## Access a virtual machine (or a physical server) connected to the SAP Process Integration instance
To begin, let us initiate an RDP connection to a Windows virtual machine that lets us connect to the SAP Process Integration Java Server. <br> Here we are using SAP Cloud Appliance Library (SAP Cal) https://cal.sap.com/ to install and manage an instance of SAP Process Integration 7.5 SP28. 
![](/exercises/ex2/images/ex2_14.png)

## Connect to the Integration Directory
Let us launch the start page of the Java instance (J2E), the entry point for us to get into the Process Integration tools. Click on Integration Builder to staring building an ICO in the Integration Directory section.
![](/exercises/ex2/images/ex2_1.png)
<br> This launches a swing client. Login to the server by supplying 

<br>![](/exercises/ex2/images/ex2_2.png)

<br>![](/exercises/ex2/images/ex2_3.png)

<br>![](/exercises/ex2/images/ex2_4.png)

<br>![](/exercises/ex2/images/ex2_5.png)

<br>![](/exercises/ex2/images/ex2_6.png)

<br>![](/exercises/ex2/images/ex2_7.png)


## Connect to the Enterprise Service Repository

<br>![](/exercises/ex2/images/ex2_8.png)

<br>![](/exercises/ex2/images/ex2_9.png)

<br>![](/exercises/ex2/images/ex2_10.png)

<br>![](/exercises/ex2/images/ex2_11.png)

<br>![](/exercises/ex2/images/ex2_12.png)

<br>![](/exercises/ex2/images/ex2_13.png)

## Testing the Web Service Interface
Let us now look at ways to test the Interface. Given that this is a SOAP Service, we will use SoapUI (https://www.soapui.org/downloads/soapui/), the open source tool to test the interface. You may use any other tool (e.g. Postman)of your choice.
<br>![](/exercises/ex2/images/ex2_15.png)

<br>![](/exercises/ex2/images/ex2_16.png)

<br>![](/exercises/ex2/images/ex2_17.png)

<br>![](/exercises/ex2/images/ex2_18.png)

<br>![](/exercises/ex2/images/ex2_19.png)

<br>![](/exercises/ex2/images/ex2_20.png)

<br>![](/exercises/ex2/images/ex2_22.png)



## Summary

You've now ...

Continue to - [Exercise 3 - Migration Assessment](../ex3/README.md)

