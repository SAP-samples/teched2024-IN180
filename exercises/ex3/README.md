# Exercise 2 - Migration Assessment

In this exercise, you will learn how to migrate your existing integration scenarios to SAP Integration Suite with the Migration Assessment capability of SAP Integration Suite. This offering helps you estimate the technical efforts involved in the migration process and evaluates how various integration scenarios might be migrated. Once you've extracted your integration scenarios and executed a scenario evaluation, you can find the modernization recommendations in the downloadable reports and the dashboard.

## Access Migration Assessment capabilities

In the SAP Integration Suite landing page, scroll down to Capabilities, and select Create Requests from the Assess Migration Scenarios tile.

<be>![](./images/AssessMigrationScenario.png)

## Checkout Configuration for Process Orchestration System

After completing these steps you will be able to test the connection to your SAP Process Orchestration(PO) system. Additionally, we will also walk you through the steps on how to set up your own PO system. This will help you to do the setup on your own landscape. <br><br>

Note: For this exercise, the connection to a cloud connector has been established, the PO system is connected to the SAP Integration Suite tenant and you do not have Admin roles to add a new system. <br><br>

1. Navigate to **Settings > Integrations**, under System, select J2E System to view the details. <br><be>

<be>![](/exercises/ex2/images/TestPOSystem.png)

For this exercise, the system setup is already done and you can click on Test Connection to check the connection to PO system. <br><br>

Note: In the Migration Assessment Application, the page now displays information about the Integration Directory and, optionally, the Enterprise Services Repository you connected to your previously created system. <br><br>

2. In the Migration Assessment Application, navigate to **Configure > Rules** <br><be>

<be>![](/exercises/ex3/images/ConfigureRules.png)

Here you can find a list of rules predefined by SAP. Rules are a set of characteristics according to which the application evaluates whether an integration scenario can be migrated and what effort you can expect. <br><br>

Note: Currently, you can’t add custom rules or edit the standard rules. You can only view the standard rules. <br><br>

As an example, select the rule SenderAdapterType <br><br>

3. Open the variant MAIN_SenderAdapterType <br><be>

<be>![](/exercises/ex3/images/SenderAdapterType.png)

## Optional - Walkthrough of adding a Process Orchestration System
Optionally you can try out this section to add the PO system in your own landscape. For this exercise, you do not have the roles to Add the system but we want to walk you through the steps so that you can do it on your landscape. <br><br>

Navigate back to Settings and click on '+' <br><br>


Fill in the details and click on Add. <br><br>


You will be able to see the newly added systems and additionally you can check the connection by clicking on the Test Connection <br><br>


## Reuse or Create a new Data Extraction Request
Usually, the data extraction takes some time depending on the number of integration scenarios configured on SAP Process Orchestration. For our exercise, we have configured a handful of scenarios in the SAP Process Orchestration system, so that the extraction runs fast. A recommendation from our side would be to reuse the already created Data Extraction Request. If you still want to create a new one, please follow the below steps. <br><br>

1. In the Migration Assessment Application, navigate to **Request>Data Extraction**. <br><br>

<be>![](/exercises/ex3/images/RequestDataExtraction.png)

2. We recommend you reuse the already existing request as creating a new one would take a few minutes. If you want to create a new request, Click on Create. Otherwise, you can continue with Create a Scenario Evaluation Request. <br><br>

<be>![](/exercises/ex3/images/CreateDE.png)

3. Enter a Request Name (append with your unique identifier maybe UserXX-Extraction where XX is your userid), and select the System you want to connect to (in our case it is J2E from the drop-down). Click on Create. <br><br>

<be>![](/exercises/ex3/images/DENameCreate.png)

4. The data extraction starts. It should show the status In Process. From time to time, you can refresh to check if the request has been completed. <br><be>

<be>![](/exercises/ex2/images/DEInProgress.png)

5. Once the extraction finishes, the new request appears in the list of data extraction requests with the status Completed. Choose the Check extraction logs icon to view the data extraction log which provides you with details about the data extraction. <br><be>

<be>![](/exercises/ex2/images/DEComplete.png)

6. The log shows you the different steps of the data extraction, its progress if still In Progress, warnings and errors during the extraction, etc. In the log, you can filter on the log level. Furthermore, you can download the log in Excel format. <br><br>

<be>![](/exercises/ex2/images/DELogs.png)

## Create a Scenario Evaluation Request
Assess your integration scenarios using the information from the data extraction requests. The prerequisite is that you have at least one data extraction request in status Completed. <br><br>


1. In the Migration Assessment application, navigate to **Request>Scenario Evaluation**. <br><br>

<be>![](/exercises/ex3/images/RequestScenarioEvaluation.png)

2. Select Create <br><be>

<be>![](/exercises/ex3/images/ScenarioEvaluationCreate.png)

3. Enter a Request Name as DemoXX (where XX is your userid)and choose a Data Extraction Request from the drop-down or the one you executed previously. For this specific run of your scenario evaluation, enter an Evaluation Run Name as DemoXX (where XX is your userid)and a Description. <br><br>

<be>![](/exercises/ex3/images/ScenarioEvaluationDetails.png)

Note: You usually run a new evaluation request for a new data extraction whereas you run a new evaluation run whenever the assessment rules have been changed. <br><br>

4. The new request appears in the list of scenario evaluation requests in Status In Progress. <br><be>

<be>![](/exercises/ex2/images/ScenarioEvaluationInProgress.png)

5. Refresh and wait until the request changes to status Completed. Different Actions can be performed for a scenario evaluation request. <br><be>

<be>![](/exercises/ex2/images/ScenarioEvaluationCompleted.png)


## View Generated Reports
Access and download analysis of your scenario evaluation runs with details specific to your integration scenarios, for example, adapters and an overview of the rules used in the evaluation. Further, you can download details about the latest evaluation run in one of two formats .xlsx file and .pdf file <br><br>

1. Let’s start with opening the dashboard. Select the Open Dashboard icon. <br><br>

<be>![](/exercises/ex3/images/DashboardOverview.png)

2. The dashboard shows you an analysis of your scenario evaluation runs with details specific to your integration scenarios, i.e., scenarios grouped by assessment categories, scenarios grouped by rough t-shirt effort estimation, statistics about adapters used in your integration scenarios, etc. You can switch between the data of all runs performed for the scenario evaluation request so far (note, if you haven’t triggered another analysis, there is only one entry in the drop-down menu). <br><be>
<be>![](/exercises/ex3/images/DEInProgress.png)

3. Switch to the Integration Scenarios tab, and you will see the list of all integration scenarios, including effort size and assessment category. <br><br>

<be>![](/exercises/ex3/images/IntegrationScenarioTab.png)

4. Switch back to the list of Scenario Evaluation requests. From the Additional Options menu, you can select Trigger Analysis to schedule a new evaluation run based on the most recent data extraction. Let's skip this for now as data did not change. <br><br>
Furthermore, you have the option to download details about the latest evaluation run either in an Excel format or as a PDF file. <br><be>

<be>![](/exercises/ex3/images/DEInProgress.png)

5. The option as .xlsx file lists all integration scenarios that were part of the request with migration effort and status as well as the rules applied to them. <br><be>

<be>![](/exercises/ex3/images/ExcelReport.png)

. The option as .pdf file features the previously mentioned details about the integration scenarios while also providing a written summary of adapters and the assessment in general, with charts and tables as visual aids. It also maps the t-shirt effort estimation to effort estimation in person days based on project experience. This file is suited as a summarizing report, that can be used for example for management. <br><be>

<be>![](/exercises/ex3/images/pdfReport.png)

## Summary

You've now ...

Continue to - [Exercise 3 - Excercise 3 ](../ex3/README.md)
