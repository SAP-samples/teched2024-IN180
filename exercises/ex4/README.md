# Exercise 4 - Migrate and test a simple SOAP to SOAP scenario

In this exercise, we will create and migrate a simple SOAP to SOAP scenario to request credit data from SAP S/4HANA.


## Create an Integration Package

The first step is to create an integration package where the automatically generated integration flows are created.

1. Switch back to the SAP Integration Suite landing page by pressing the SAP logo.

<br>![](/exercises/ex4/images/Navigate_Back.png)

2. Navigate to <b>Design > Integrations and APIs</b>, and select  <b>Create</b>.

<br>![](/exercises/ex4/images/Create_Pack.png)
   
3. Fill in the <b>Name</b> of the integration package, e.g. **User XX** where <b>XX</b> is your user number from 00 to 99, and a short <b>Description</b>. The technical name is automatically set. Then click <b>Save</b>.

<br>![](/exercises/ex4/images/SavePackage.png)


## Run the Migration Wizard

Every Integrated Configuration Object (ICO) that can be migrated has an associated pattern in the migration tooling. Based on these patterns, the migration tooling creates equivalent integration flows in the SAP Integration Suite. Let's start with the actual migration.


1. In your previously created package, and switch to the <b>Artifacts</b> and click on  <b>Migrate</b> to start the migration wizard.

<br>![image](/exercises/ex4/images/StartMigration.png)
   
   
2. Select the SAP Process Orchestration system for which the assessment was previously done. For this, expand the Name section and select your system from the drop-down menu. Click <b>Next Step</b> to proceed with configuring the scenario.

<br>![](/exercises/ex4/images/PO_Sys.png)
   
3. Currently, only Integrated Configuration Objects (ICO) are supported. You can use the filter to filter out the list of ICOs and choose the appropriate scenario. Click on <b>Show Filters</b>. 

<br>![image](/exercises/ex4/images/ShowFilters.png)

4. In the filter, fill in **SI_Credit** as <b>Interface</b>. The filter reduces the number of entries in the **Name** drop down list. Choose the interface **SI_CreditManagementAccountRead_Outbound**. Click <b>Next Step</b>.

<br>![image](/exercises/ex4/images/ChooseScenario.png)

5. The best-fit pattern is identified by the migration framework and will be automatically filled in for you. In this case, it will be **Point-to-Point Synchronous**. Click <b>Next Step</b>.

<br>![](/exercises/ex4/images/P2PSyncPattern.png)

6. In the next step, you can choose whether you create reusable message mapping artifacts or not. In this exercise, let's opt for using local resources. So, **unselect** the **Enable Reusable Message Mapping Artifacts** flag. Then, click <b>Next Step</b>

<br>![](/exercises/ex4/images/NoReusableArtifacts.png)

7. Maintain any **Name** for your integration flow, e.g. following the pattern: **CreditManagementAccountRead_UserXX** where <b>XX</b> is your user id from 00 to 99. Note, that the ID of your integration flow needs to be unique across all integration flows on the tenant. Click on <b>Review</b>.

<br>![](/exercises/ex4/images/Int_Name_Review.png)
    
8. Verify the information and then click on <b>Migrate</b>.

<br>![](/exercises/ex4/images/Final_Migrate.png)
    
9. A new integration flow has been generated within your package. Click on the artifact to take a closer look at each individual step. The required information is automatically populated such as the connection information. Click on <b>View Artifact</b>.

<br> ![image](/exercises/ex4/images/ViewArtifact.png)


## Deploy migrated artifacts

After completing these steps you will be able to deploy the Integration flow and monitor your scenario.
    
1.  Click on the <b>SOAP Adapter</b> and view the <b>Connection</b> details. You can see that the endpoint address has been automatically set based on the integration flow name that you have entered. For this particular scenario, we need to configure the credentials. Select **Configure** to adjust the flow.


<br>![](/exercises/ex4/images/Open_Iflow.png)

2. Switch to tab **Receiver**. Enter **s4hanacredentials** as Credential Name. Press **Save**.

<br>![](/exercises/ex4/images/Configure_Iflow.png)

3. **Close** the Message Dialog. Press **Deploy** to deploy to Integration Flow.

<br>![](/exercises/ex4/images/Deploy_Flow.png)

4. Via the Runtime Profile you can decide whether the Integration Flow should be deployed in the native Cloud Runtime or to the Edge Integration Cell. For this exercise choose **Edge Integration Cell** and press **Yes**.

<br>![](/exercises/ex4/images/RuntimeProfile.png)

5. Confirm that the deployment has been triggered.

<br>![](/exercises/ex4/images/Deploy_Con2.png)
  
4. You can check the deployment status via the monitor dashboard. Navigate to <b>Monitor > Integrations and APIs</b>.

<br>![](/exercises/ex4/images/Monitor_Int.png)

5. Change the Monitoring Runtime to **Edge Integration Cell**.

<br>![](/exercises/ex4/images/runtime_change.png)

6. Select the <b>Manage Integration Content</b> tile.

<br>![](/exercises/ex4/images/ManageIntContentTile.png)
   
6. Search your Integration Flow. It should be in status <b>Started</b>. From here, you get the endpoint that you need to call to test the scenario. <b>Copy the endpoint</b> as we will use it in the next step.

<br>![](/exercises/ex4/images/Copy_endpoint.png)
   
Now you are all set to test your scenario!

## Verify the Interface via REST Client

Having completed these steps, you are now ready to test the interface. To do this, you will need a REST client, such as [Bruno](https://www.usebruno.com/downloads). 

1. Open Bruno and click on <b>Create Collection</b>.

<br>![image](/exercises/ex4/images/Create_Coll.png)  

2. Provide a Name, e.g. **SAP Integration Suite Exercise**, enter a Folder Location on your device and press <b>Create</b>.

<br>![image](/exercises/ex4/images/Create_Coll2.png)  

3. Click on the three dots next to your created package and press<b>New Request</b>. 

<br>![image](/exercises/ex4/images/New_Request.png)  

4. Provide a Name, e.g. **Exercise 4 - SOAP to SOAP scenario** and past the endpoint URL noted in previous exercise. Press **Create**.

<br>![image](/exercises/ex4/images/New_Request2.png)  


5. In case there pops-up a dialog for JavaScript execution, you can choose **Safe Mode** as there is no Javascript required for this exercise.

<br>![image](/exercises/ex4/images/SafeMode.png)

6. Switch to tab **Body**, Choose Content-Type **XML** and provide following payload:

```xml
<?xml version="1.0" encoding="utf-8"?>
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:cm="http://demo.sap.com/cm">
   <soapenv:Header/>
   <soapenv:Body>
      <cm:MT_CreditManagementAccountRequest>
         <!--Optional:-->
         <DebtorPartyInternalID>MDG_CU01</DebtorPartyInternalID>
         <!--Optional:-->
         <CreditsegmentInternalID>0002</CreditsegmentInternalID>
      </cm:MT_CreditManagementAccountRequest>
   </soapenv:Body>
</soapenv:Envelope>
```

7. Switch to tab **Auth** and choose **OAuth 2.0**. Grant Type must be set to **Client Credentials**. The authentication details can be found in the booker application. Past them and press **Get Access Token**.

<br>![image](/exercises/ex4/images/Auth_Bruno.png)  
<br>![image](/exercises/ex4/images/Auth_Booker.png) 


4. <b>Paste the endpoint</b> from you integration flow as URL.  

<br>![image](/exercises/ex4/images/Insomnia-4.png)  

5. Add a <b>Body</b> of type XML.

<br>![image](/exercises/ex4/images/Insomnia-5.png)  

6. Provide following payload:

```xml
<soapenv:Envelope
    xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/"
    xmlns:pi="http://pi-elevation.bootcamp.com">
    <soapenv:Header />
    <soapenv:Body>
        <pi:MT_NumberConversion_REQ>
            <number>1389</number>
        </pi:MT_NumberConversion_REQ>
    </soapenv:Body>
</soapenv:Envelope>
```

<br>![image](/exercises/ex4/images/Insomnia-6.png)  

7. Switch to tab <b>Auth</b> and choose <b>Basic Auth</b>.

<br>![image](/exercises/ex4/images/Insomnia-7.png)  

8. Provide following credentials:<br>


<br>![image](/exercises/ex4/images/Insomnia-8.png)  

9. Click <b>Send</b>. The request should return HTTP code 200 and a response with the converted text.

<br>![image](/exercises/ex4/images/Insomnia-9.png)  

10. Navigate back to the monitoring page, and click the **Monitor Message Processing** link below the **Artifact Details** of your deployed SOAP to SOAP integration flow.

<br>![image](/exercises/ex4/images/Monitoring_Navigate_To_MPL.png)

11. In the message monitor, you should see one new log in status **Completed**.

<br>![image](/exercises/ex4/images/Monitoring_MPL_Completed.png)

## Summary

Congratulations. You have successfully migrated and tested your scenario now.

Continue to - [Exercise 5 - Deploy an API Artefact to connect to an S/4HANA OData Service](../ex5/README.md)
