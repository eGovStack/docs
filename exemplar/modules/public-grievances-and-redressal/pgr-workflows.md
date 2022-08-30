---
description: Learn more about PGR workflows and its configuration
---

# PGR Workflows

### Workflow Overview

Workflows are a series of steps that moves a process from one state to another state by actions performed by different kinds of Actors - Humans, Machines, Time based events etc. to achieve a goal like onboarding an employee, or approve an application or grant a resource etc.

### PGR Workflow Requirement

The workflow services contribute to adding a flexible and dynamic approach to using the modules in the long run. PGR workflows cater to the evolving requirements as we introduce new features in PGR like escalation and routing. These features are also useful in other modules like Trade License and Fire NoC.

### Intended Audience & Objectives

This document is meant for the Tech team to understand the requirement of workflows in PGR. And to come at a conclusion whether it is possible to fulfil the requirement of workflow through workflow service available at eGov.

### Workflow Specifics

1. Role-Action Mapping:
   1. Citizen- Submit a complaint, Re-open complaint, Rate (not a workflow feature)
   2. CSR- Submit a complaint, Re-open complaint
   3. GRO- Reject Complaint, Assign complaint
   4. LME- Request for Re-assign, Resolve complain
2. Actions and their Meaning

| S. N. | Action                | Description                                                                                                               |
| ----- | --------------------- | ------------------------------------------------------------------------------------------------------------------------- |
| 1     | Submit                | This action will raise the complaint                                                                                      |
| 2     | Re-open complaint     | Once a complaint is resolved or rejected, this action will re-submit the complaint and it will go through the workflow    |
| 3     | Reject Complaint      | This action will reject the complaint and then gives the option to citizen/CSR to RE-OPEN within 5 days                   |
| 4     | Assign complaint      | This action will help GRO/DGRO to assign the complaint to last mile employee (LME) by giving them LME list to choose from |
| 5     | Request for Re-assign | This action will send back complaint to GRO/DGRO for reassignment                                                         |
| 6     | Resolve complaint     | This action resolves the complaint then gives the option to citizen/CSR to RE-OPEN within 5 days                          |
| 7     | Re-assign complaint   | This action will help GRO to re-assign complaint if assignment made by him is not accurate or any other reason            |

1. Workflow:

![](https://lh6.googleusercontent.com/vQA7dYAam0HqiL1wik27kpwurgTHWZ1NA8\_zzD0DlE\_nrYEeT3XVzqzLUUJh1dasmwIxijHdL32ZtyuDvwsMatTDGfo4cTTp-60hlOxE\_k-pWmIL5oWsNOMbiELY8hyvWti1GYFb)

\*Green color shows the ideal process for workflow

1. Configuration:

| Sr. No | Current State  | Action            | Next State     | Actors      |
| ------ | -------------- | ----------------- | -------------- | ----------- |
| 1      | Initiated      | Submit Complaint  | Pending at GRO | Citizen/CSR |
| 2      | Rejected       | Re-open           | Pending at GRO | Citizen/CSR |
| 3      | Resolved       | Re-open           | Pending at GRO | Citizen/CSR |
| 4      | Pending at GRO | Assign complaint  | Pending at LME | GRO/DGRO    |
| 5      | Pending at GRO | Reject            | Rejected       | GRO/DGRO    |
| 6      | Pending at LME | Re-assign         | Pending at LME | GRO/DGRO    |
| 7      | Pending at LME | Request Re-assign | Pending at GRO | LME         |
| 8      | Pending at LME | Resolve complaint | Resolved       | LME         |
| 9      | Pending at LME | Reject            | Rejected       | LME         |

### Impacts

1. Employee Inbox UI: Web and Mobile
2. SLA: configuration at ULB level

### Other Features and Functionalities in PGR

All other features and functionalities should remain unaffected like complaint types, uploading a photo, capturing address, UI for the citizen, search complaint, complaint history, comments etc.

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation ](https://egov.org.in/)is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).
