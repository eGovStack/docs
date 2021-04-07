# List Of Services

## Introduction

The list of services in the OBPS module refers to the various types of services offered to citizens or end-users. The Data Table below contains an indicative list of services and details required to configure the building plan approval module.

## Data Table

| Sr. No. | Service Code\* | Service Name\* \(In English\) | Service Name \(In Local Language\) | Plan required for service \* | Occupancy Certificate applicable for service | Plan Validity of this service \(In Years\)\* | Renewal Validity of the service \(in Years\) |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | NC | New Construction |  | Yes | No | 2 | 2 |
| 2 | ADD | Addition |  | Yes | Yes | 1 | 1 |

{% hint style="info" %}
Data given in the table is sample data for reference.
{% endhint %}

## Procedure

### Data Definition <a id="Data-Definition"></a>

| Sr. No. | Column Name | Data Type | Data Size | Is Mandatory? | Description |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | Service Code | Alphanumeric | 64 | Yes | Unique Identifier for the listed services for reference |
| 2 | Service Name \(In English\) | Text | 64 | Yes | Names of applicable services such as Permit for New Construction, Reconstruction, Alteration, or Demolition |
| 3 | Service Name \(In Local Language\) | Text | 64 | No | Service names in Local language |
| 4 | The plan required for service | Text | 3 | Yes | Building drawing \(Plan\) required to submit for the listed services. The radio button for marking Yes or No |
| 5 | Occupancy Certificate applicable for service | Text | 3 | No | Whether Occupancy Certificate requires to be generated for this service. Radio button to mark Yes or No |
| 6 | Plan validity for this service \(In Years\) | Integer | 2 | Yes | Define the validity period of the permit order generated for the listed service |
| 7 | Renewal Validity of the service \(in Years\) | Integer | 2 | No | It can be 1 or 2 or 3 years based on the State/ULB needs |

### Steps to fill data

1. Download the data template attached to this page.
2. Refer to the ‘Data Definition’ section of this document to understand the headers in the template sheet, their data type, size, and definitions.
3. Reach out the person who shared the template for further details or to clear your doubts. Identify if the State/ULB has a provision for capturing pipe size for connections.
4. Identify the services provided by DIGIT OBPAS system and enter then into the template with other configurable parameters given in the template.
5. Go through the checklist to verify the data. Make sure that each and every point mentioned in the checklist is covered.

## Checklist

The checklist is a set of activities to be performed once the data is filled into a template to ensure data entry requirements are met. These activities have been divided into 2 groups as given below.

### Common Checklist

This checklist covers all the activities which are common across the entities.

| Sr. No. | Checklist Parameter | Example |
| :--- | :--- | :--- |
| 1 | Make sure that each and every point in this reference list has been taken care of | [Checklist](../common-config/checklist.md) |

### Entity Specific Checklist

There is no separate entity-specific checklist for this entity.

## Attachments

{% file src="../../../../.gitbook/assets/configuration-data-template-list-of-services-2-.xlsx" caption="Configuration Data Template" %}

{% file src="../../../../.gitbook/assets/sample-configuration-data-list-of-services.xlsx" caption="Sample Data" %}

