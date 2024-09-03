# IN180 - Future-proof your SAP PI/PO investments with SAP Integration Suite

## Description

This repository contains the material for the SAP TechEd 2024 session IN180 - Future-proof your SAP PI/PO investments with SAP Integration Suite. <br>
In this session, you will deep-dive into the solution components of SAP Integration Suite, primarily Cloud Integration, Integration Assessment, and Edge Integration cell, the next-generation hybrid integration runtime offered with SAP Integration Suite, which would enable you to manage APIs and run integration scenarios within your local landscape (private cloud or on-premise).

## Overview

Customers are looking at elevating and migrating their mature production-grade deployments of SAP Process Integration to SAP Integration Suite. This session will introduce you to simple ways of achieving so.<br>
We first look at a SAP Process Intgration (PI) landscape with a simple Integrated Configuration object (ICO) representing a Web Service-based Integration pattern to an OnPremise S/4HANA System. <br>
We then dive into migration assessment to assess the technical efforts involved in the migration process and evaluate how various integration scenarios might be migrated. After having finished the assessment of the current SAP Process Integration landscape and having estimated the effort needed to migrate with the Interface Migration Assessment capability, the next step is the actual migration. The goal of the migration tool is to provide a semi-automated migration where interfaces in SAP Cloud Integration will be automatically created based on SAP Process Integration information so that ideally 60-70% of technical migration efforts are automated. The migration of scenarios is based on a template approach, which means that integration flow templates are used as a skeleton to migrate the content and create the final integration flows, and maximize reusability.<br>
We then look at Edge Integration Cell, the next-generation hybrid integration runtime offered with SAP Integration Suite as a deployment vehicle for the migrated content. Our principal goal here is to demonstrate a 'Ground to Ground' integration pattern. We achieve this by putting the Edge Integration Cell runtime, the SAP PI system, and S/4HANA System in the same network zone as opposed to opening everything to the Internet.<br>
We finally look at deployment and managing an API Artefact, keeping the motivations for an API-centric integration in mind.  

## Requirements

The requirements to follow the exercises in this repository are...

## Exercises

Provide the exercise content here directly in README.md using [markdown](https://guides.github.com/features/mastering-markdown/) and linking to the specific exercise pages, below is an example.

- [Getting Started](exercises/ex0/)
- [Exercise 1 - First Exercise Description](exercises/ex1/)
    - [Exercise 1.1 - Exercise 1 Sub Exercise 1 Description](exercises/ex1#exercise-11-sub-exercise-1-description)
    - [Exercise 1.2 - Exercise 1 Sub Exercise 2 Description](exercises/ex1#exercise-12-sub-exercise-2-description)
- [Exercise 2 - Second Exercise Description](exercises/ex2/)
    - [Exercise 2.1 - Exercise 2 Sub Exercise 1 Description](exercises/ex2#exercise-21-sub-exercise-1-description)
    - [Exercise 2.2 - Exercise 2 Sub Exercise 2 Description](exercises/ex2#exercise-22-sub-exercise-2-description)

  
**OR** Link to the Tutorial Navigator for example...

Start the exercises [here](https://developers.sap.com/tutorials/abap-environment-trial-onboarding.html).

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
