# Workflow Process

### Introduction

The workflow process is a set of steps through which information flows in sequence and the [workflow roles](https://digit-discuss.atlassian.net/wiki/spaces/DO/pages/537624711/Workflow+Actions) which derives the actors are assigned to a step to complete the work defined for that [level](https://digit-discuss.atlassian.net/wiki/spaces/DO/pages/537690461/Workflow+Levels). The states of each level are derived based on the information received from the previous step.

### Data Table

| Sr. No. | Current State        | Workflow Actions       | Next State           | Role Name  | SLA |
| ------- | -------------------- | ---------------------- | -------------------- | ---------- | --- |
| 1       |                      | Create and Approve     | Approved             | Assistant  | NA  |
| 2       |                      | Forward                | Pending for Approval | Assistant  | NA  |
| 3       | Pending for Approval | Verify and Approve     | Approved             | Supervisor | NA  |
| 4       | Pending for Approval | Save                   | Pending for Approval | Supervisor | NA  |
| 5       | Pending for Approval | Reject                 | Rejected             | Supervisor | NA  |
| 6       | Pending for Approval | Send Back to Assistant | Rejected for Review  | Supervisor | NA  |
| 7       | Rejected for Review  | Forward                | Pending for Approval | Assistant  | NA  |
| 8       | Rejected for Review  | Cancel                 | Rejected             | Assistant  | NA  |

{% hint style="info" %}
Data given in the above table is sample data.
{% endhint %}

### Procedure

#### Data Definition

| Sr. No. | Column Name   | Data Type | Data Size | Is Mandatory? | Definition/ Description                                                                                                                                                                 |
| ------- | ------------- | --------- | --------- | ------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1       | Current State | Text      | 256       | Yes           | The Current State indicates the stage at which the process of the workflow in progress                                                                                                  |
| 2       | Action        | Reference | 64        | Yes           | The Action indicates the activity that can be performed at the respective stage in the workflow. This refers to Workflow Actions                                                        |
| 3       | Next State    | Text      | 256       | Yes           | The Next State is the state in the workflow that gets updated to in the respective stage on performing the action. (Example: assigning the for approval from one person to next person) |
| 4       | Role Name     | Reference | 64        | Yes           | The role is the different hierarchy of people with designation who are authorized to initiate, approval or rejecting the process. It refers to Workflow Levels                          |
| 5       | SLA           | Integer   | 2         | No            | The SLA indicates the time-frame within which the action to be completed                                                                                                                |

#### Step to fill data

1. Download the data template attached to this page.
2. Have it open and go through all the headers and understand the meaning of them by referring 'Data Definition' section.
3. Make sure all the headers, its data type, field size and its definition/ description is understood properly. In case of any doubt, please reach out to the person who has shared this document with you to discuss the same and clear out the doubts.
4. Start filling the data starting from serial no. and complete a record at once. repeat this exercise until the entire data is filled into a template.
5. Verify the data once again by going through the checklist and taking care of each and every point mentioned in the checklist.

### Checklist

The checklist is a set of activities to be performed once the data is filled into a template to ensure data type, size, and format of data is as per the expectation. These activities have been divided into 2 groups as given below.

#### Common Checklist

This checklist covers all the activities which are common across the entities.

| Sr. No | Checklist Parameter                                                               | Example                                    |
| ------ | --------------------------------------------------------------------------------- | ------------------------------------------ |
| 1      | Make sure that each and every point in this reference list has been taken care of | [Checklist](../common-config/checklist.md) |

#### Entity Specific Checklist

Please discuss with a relevant department head before finalizing the workflow.

### Attachments

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)​](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation](https://egov.org.in/) is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).
