# IN180 - Future-proof your SAP PI/PO investments with SAP Integration Suite

## Description

This repository contains the material for the SAP TechEd 2024 session IN180 - Future-proof your SAP PI/PO investments with SAP Integration Suite. <br>
In this session, you will deep-dive into the solution components of **SAP Integration Suite**, primarily Cloud Integration, Migration Assessment, and Edge Integration cell, the next-generation hybrid integration runtime offered with SAP Integration Suite, which would enable you to manage APIs and run integration scenarios within your local landscape (private cloud or on-premise).

## Overview

Customers want to elevate and migrate their mature production-grade SAP Process Integration and Process Orchestration deployments to SAP Integration Suite. This session will introduce you to simple ways of achieving so.<br><br>
We first look at a **SAP Process Integration (PI)** landscape with a simple Integrated Configuration object (ICO) representing a Web Service-based Integration pattern to an OnPremise S/4HANA System. <br><br>
We then dive into **migration assessment** to assess the technical efforts involved in the migration process and evaluate how various integration scenarios might be migrated. After having finished the assessment of the current SAP Process Integration landscape and having estimated the effort needed to migrate with the Interface Migration Assessment capability, the next step is the actual migration. The goal of the migration tool is to provide a semi-automated migration where interfaces in **SAP Cloud Integration** will be automatically created based on SAP Process Integration information so that ideally 60-70% of technical migration efforts are automated. The migration of scenarios is based on a pattern approach, which means that integration flow patterns are used as a skeleton to migrate the content and create the final integration flows, and maximize reusability.<br><br>
We then look at **Edge Integration Cell**, the next-generation hybrid integration runtime offered with SAP Integration Suite as a deployment vehicle for the migrated content. Our principal goal is to demonstrate a 'Ground to Ground' integration pattern. We achieve this by putting the Edge Integration Cell runtime, the SAP PI system, and S/4HANA System in the same network zone as opposed to opening everything to the Internet.<br><br>
In the leg of the exercise, we look at deployment and managing an **API Artifact** as a proxy to S/4HANA OData Service, keeping the motivations for an API-centric integration in mind. 

![](/images/future-proof.png)

## Pre-requisites

There are no functional prerequisites for this hands-on session. You can perform it even if you do not have any experience with integration solutions. However, you will be able to derive a lot of value from it if you have some knowledge of what SAP Integration Suite is all about and how it helps with enterprise-wide integration needs.
Here is a mission that can help you get started with SAP Integration Suite:

• [Get Started with Integration Suite!](https://discovery-center.cloud.sap/protected/index.html#/missiondetail/3258/3327/)

You will be provided with a user account (***UserXX***) that authenticates to SAP Cloud Identity Service to log in to the SAP Integration Suite sandbox Account set up for you. 

> [!IMPORTANT]
> Your instructor will provide you with the tenant URL, username, and password to access the tenant. 

You will also need a testing tool installed on your local machine to connect to the IFlows and API. In this hands-on, we will be referencing screenshots executed in [Bruno](https://www.usebruno.com/) as the testing client. You are free to use any tool of your choice, e,g, Postman, Insomnia, SOAPUI etc. 

> [!NOTE]
> You will not be able to use your existing SAP BTP Trial Account or the BTP Free Tier Account to run this exercise as we need connections to an existing SAP Process Orchestration system and an instance of Edge Integration Cell.
>
> We have set up the tenants for you to explore during the IN180 jump-start session. The systems will be available for 10 days after the TechEd hands-on lab event.

## Exercises

Here is a summary of the exercises we will be covering in this hands-on session.

- [Getting Started - An overview of SAP Integration Suite](exercises/ex0/)
- [Exercise 1 - Access and explore SAP Integration Suite](exercises/ex1/)
- [Exercise 2 - SAP Process Integration Walkthrough](exercises/ex2/)
- [Exercise 3 - Migration Assessment](exercises/ex3/)
- [Exercise 4 - Migrate and test a simple SOAP to SOAP scenario](exercises/ex4/)
- [Exercise 5 - Deploy an API Artefact to connect to a S/4HANA OData Service](exercises/ex5/)

## Further learning

Here are some additional resources that you can refer to for further learning:
- Migration Guide for SAP Process Orchestration: https://help.sap.com/docs/migration-guide-po/migration-guide-for-sap-process-orchestration/migration-guide-sap-process-orchestration?locale=en-US
- SAP Integration Suite Documentation: https://help.sap.com/docs/integration-suite?locale=en-US
- SAP TechEd 2024 sessions (on-demand replays):
  - [IN100 | Innovate now with a modern, AI-assisted integration suite](https://www.sap.com/events/teched/virtual/flow/sap/te24/catalog/page/catalog/session/1720287755996001aemK)
  - [IN103 | Modernize and elevate to the cloud with SAP Integration Suite](https://www.sap.com/events/teched/virtual/flow/sap/te24/catalog/page/catalog/session/1721791179096001rRx3)
  - [IN202 | Gain flexibility and scalability with a hybrid integration platform](https://www.sap.com/events/teched/virtual/flow/sap/te24/catalog/page/catalog/session/1721792860703001Vo9V)

## Contributing
Please read the [CONTRIBUTING.md](./CONTRIBUTING.md) to understand the contribution guidelines.

## Code of Conduct
Please read the [SAP Open Source Code of Conduct](https://github.com/SAP-samples/.github/blob/main/CODE_OF_CONDUCT.md).

## How to obtain support

Support for the content in this repository is available during the actual time of the online session for which this content has been designed. Otherwise, you may request support via the [Issues](../../issues) tab.

## License
Copyright (c) 2024 SAP SE or an SAP affiliate company. All rights reserved. This project is licensed under the Apache Software License, version 2.0 except as noted otherwise in the [LICENSE](LICENSES/Apache-2.0.txt) file.
