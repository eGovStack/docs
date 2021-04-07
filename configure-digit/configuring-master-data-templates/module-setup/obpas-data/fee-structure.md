# Fee Structure

## Introduction

Fee Structure masters list contains the fee details applicable for processing specific services. All fee-related information collected by the authorities during the course of building plan approval is maintained in this masters.

## Data Table

| Sr No. | Service Type\* | Application Type\* | Application Subtype | Fee Subtype\* | BPA Fees\* | Amount\* | Calculation Logic |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | new construction | PERMIT APPLICATION |  | application fee | Application Fees | 50 |  |
| 2 | new construction | PERMIT APPLICATION | Medium Risk | sanction fee | Additional Fees | 0 |  |
| 3 | new construction | PERMIT APPLICATION | Low Risk | application fee | Land Development Charges | 50 |  |
| 4 | new construction | OCCUPANCY CERTIFICATE | High Risk | sanction fee | Charges for Well | 50 |  |

{% hint style="info" %}
Data given in the table is sample data for reference.
{% endhint %}

## Procedure

### Data Definition

| Sr. No. | Column Name | Data Type | Data Size | Is Mandatory? | Description |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | Service type | Text | 256 | Yes | The type of OBPS service for which the fees is to be collected. Refer to the Data Table above for illustration |
| 2 | Application Type | Text | 256 | Yes | List of application types for which the fees are to be calculated. Refer to the Data Table above for illustration |
| 3 | Application Subtype | Text | 56 | No | Application subtype is mentioned here such as type of risk |
| 4 | Fee Subtype | Text | 256 | Yes | Type of fees so collected to be mentioned here. Refer to the Data Table above for illustration |
| 5 | BPA Fee | Text | 56 | Yes | The type of OBPS service for which the fees is to be collected. Refer to the Data Table above for illustration |
| 6 | Amount | Integer | 6 | Yes | Fee Amount collected is mentioned here. Refer to the Data Table above for illustration |
| 7 | Calculation Logic | Text | 1024 | No | Fees calculation logic if any is mentioned here |

### Steps to fill data

1. Download the data template attached to this page.
2. Refer to the ‘Data Definition’ section of this document to understand the headers in the template sheet, their data type, size, and definitions.
3. Reach out the person who shared the template for further details or to clear your doubts. Identify if the State/ULB has a provision for capturing pipe size for connections.
4. Identify the combination of attributes for with the fee is defined and then fill into the given template.
5. Go through the checklist to verify the data. Make sure that each and every point mentioned in the checklist is covered.

## Checklist

The checklist is a set of activities to be performed one the data is filled into a template to ensure data entry requirements are met. These activities have been divided into 2 groups as given below.

### Common Checklist

This checklist covers all the activities which are common across the entities.

| Sr. No. | Checklist Parameter | Example |
| :--- | :--- | :--- |
| 1 | Make sure that each and every point in this reference list has been taken care of | [Checklist](../common-config/checklist.md) |

### Entity Specific Checklist

There is no separate entity-specific checklist for this entity.

## Attachments

{% file src="../../../../.gitbook/assets/fee-structure-template.xlsx" caption="Configuration Data Template " %}

{% file src="../../../../.gitbook/assets/fee-structure-sample-data.xlsx" caption="Sample Data" %}

