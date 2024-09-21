# IN180 - Future-proof your SAP PI/PO investments with SAP Integration Suite

## Description

This repository contains the material for the SAP TechEd 2024 session IN180 - Future-proof your SAP PI/PO investments with SAP Integration Suite. <br>
In this session, you will deep-dive into the solution components of SAP Integration Suite, primarily Cloud Integration, Migration Assessment, and Edge Integration cell, the next-generation hybrid integration runtime offered with SAP Integration Suite, which would enable you to manage APIs and run integration scenarios within your local landscape (private cloud or on-premise).

## Overview

Customers want to elevate and migrate their mature production-grade SAP Process Integration and Process Orchestration deployments to SAP Integration Suite. This session will introduce you to simple ways of achieving so.<br><br>
We first look at a SAP Process Integration (PI) landscape with a simple Integrated Configuration object (ICO) representing a Web Service-based Integration pattern to an OnPremise S/4HANA System. <br><br>
We then dive into migration assessment to assess the technical efforts involved in the migration process and evaluate how various integration scenarios might be migrated. After having finished the assessment of the current SAP Process Integration landscape and having estimated the effort needed to migrate with the Interface Migration Assessment capability, the next step is the actual migration. The goal of the migration tool is to provide a semi-automated migration where interfaces in SAP Cloud Integration will be automatically created based on SAP Process Integration information so that ideally 60-70% of technical migration efforts are automated. The migration of scenarios is based on a pattern approach, which means that integration flow patterns are used as a skeleton to migrate the content and create the final integration flows, and maximize reusability.<br><br>
We then look at Edge Integration Cell, the next-generation hybrid integration runtime offered with SAP Integration Suite as a deployment vehicle for the migrated content. Our principal goal is to demonstrate a 'Ground to Ground' integration pattern. We achieve this by putting the Edge Integration Cell runtime, the SAP PI system, and S/4HANA System in the same network zone as opposed to opening everything to the Internet.<br><br>
In the leg of the exercise, we look at deployment and managing an API Artifact as a proxy to S/4HANA OData Service, keeping the motivations for an API-centric integration in mind.  

## Pre-requisites

There are no functional prerequisites for this hands-on session. You can perform it even if you do not have any experience with integration solutions. However, you will be able to derive a lot of value from it if you have some knowledge of what SAP Integration Suite is all about and how it helps with enterprise-wide integration needs.
Here is a mission that can help you get started with SAP Integration Suite:

• [Get Started with Integration Suite!](https://discovery-center.cloud.sap/protected/index.html#/missiondetail/3258/3327/)

You will need a user account (S/P/I/D/C User) that authenticates to SAP Cloud Identity Service


## Requirements

The requirements to follow the exercises in this repository are...

## Exercises

Provide the exercise content here directly in README.md using [markdown](https://guides.github.com/features/mastering-markdown/) and linking to the specific exercise pages, below is an example.

- [Getting Started](exercises/ex0/)
- [Exercise 1 - Access and explore SAP Integration Suite](exercises/ex1/)
- [Exercise 2 - SAP Process Integration Walkthrough](exercises/ex2/)
- [Exercise 3 - Migration Assessment](exercises/ex3/)
- [Exercise 4 - Migrate and test a simple SOAP to SOAP scenario](exercises/ex4/)
- [Exercise 5 - Deploy an API Artefact to connect to a S/4HANA OData Service](exercises/ex5/)


**IMPORTANT**

Your repo must contain the .reuse and LICENSES folder and the License section below. DO NOT REMOVE the section or folders/files. Also, remove all unused template assets(images, folders, etc) from the exercises folder. 

## Contributing
Please read the [CONTRIBUTING.md](./CONTRIBUTING.md) to understand the contribution guidelines.

## Code of Conduct
Please read the [SAP Open Source Code of Conduct](https://github.com/SAP-samples/.github/blob/main/CODE_OF_CONDUCT.md).

## How to obtain support

Support for the content in this repository is available during the actual time of the online session for which this content has been designed. Otherwise, you may request support via the [Issues](../../issues) tab.

## License
Copyright (c) 2024 SAP SE or an SAP affiliate company. All rights reserved. This project is licensed under the Apache Software License, version 2.0 except as noted otherwise in the [LICENSE](LICENSES/Apache-2.0.txt) file.
