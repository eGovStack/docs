# Workflow Levels

## Introduction

Workflow levels are defined for a service with Rights/Role to perform a set of Workflow Actions. There would one or more than one levels involved in a workflow process. This page helps to understand and then define all the levels with its job description and fill in a standard template.

## Data Table

| Sr. No. | Module | Service | Workflow Level | Task | Role |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | Finance | Bill Accounting | Level 1 | Create Bill | Accounts Clerk |
| 2 | Finance | Bill Accounting | Level 2 | Create and Approve | Accounts Clerk |
| 3 | Finance | Bill Accounting | Level 3 | Forward for Approval | Chief Accountant |
| 4 | Finance | Bill Accounting | Level 4 | Verify the Bill | Chief Accountant |
| 5 | Finance | Bill Accounting | Level 5 | Approval | Approver |

{% hint style="info" %}
Data given in the above table is sample data.
{% endhint %}

## Procedure

### Data Definition

| Sr. No. | Column Name | Data Type | Data Size | Is Mandatory? | Definition/ Description |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | Module | Text | 64 | Yes | The module indicates for which the user would be mapped for a specific module to perform the action |
| 2 | Service | Text | 64 | Yes | The service indicates the type of process which the user performs in a particular module |
| 3 | Workflow Level | Integer | 2 | Yes | The workflow level indicates when a process has executed the level at which the flow of the process in progress |
| 4 | Task | Text | 64 | Yes | The task refers to which state the action is in progress during the workflow |
| 5 | Job Description | Text | 256 | Yes | A short description provided for the role \(Example: Designation of the Role\) |

### Step to fill data

1. Download the data template attached to this page.
2. Have it open and go through all the headers and understand the meaning of them by referring 'Data Definition' section.
3. Make sure all the headers, its data type, field size and its definition/ description is understood properly. In case of any doubt, please reach out to the person who has shared this document with you to discuss the same and clear out the doubts.
4. Identify all different types of services on the basis of ULB’s functions to create a workflow.
5. Start filling the data starting from serial no. and complete a record at once. repeat this exercise until the entire data is filled into a template.
6. Verify the data once again by going through the checklist and taking care of each and every point mentioned in the checklist.

## Checklist

The checklist is a set of activities to be performed once the data is filled into a template to ensure data type, size, and format of data is as per the expectation. These activities have been divided into 2 groups as given below.

### Common Checklist

This checklist covers all the activities which are common across the entities.

| Sr. No | Checklist Parameter | Example |
| :--- | :--- | :--- |
| 1 | Make sure that each and every point in this reference list has been taken care of | [Checklist](https://digit-discuss.atlassian.net/wiki/spaces/DO/pages/502203140/Checklist) |

### Entity Specific Checklist

Please discuss with a relevant department head before finalizing the workflow.

## Attachments

{% file src="../../../../.gitbook/assets/workflowtemplate\_v2.xlsx" caption="Workflow Template" %}

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)​](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation](https://egov.org.in/) is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).

