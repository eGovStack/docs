# Penalty Rates

## Introduction

The penalty is defined as an amount which is charged to the citizen in violation of any rule. There would be multiple penalties defined associated with different rules and acts. Penalty rate decides on how and what amount to be calculated for a penalty.

Within DIGIT, the calculation of the penalty amount is configurable at both the State & ULB level.

## Data Table

| Sr. No. | Penalty Head | \*Penalty Rate \(In % \) | Minimum Penalty Amount | \*Flat Amount | \*From Financial Year | \*Start Date |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | Late assessment | 12.5 | 1000 | 500 | 2019-20 | 01-04-2019 |
| 2 | Unauthorized Construction | 100 | 5000 | 5000 | 2019-20 | 01-04-2019 |

## Procedure

### Data Definition

| Sr. No. | Column Name | Data Type | Data Size | Is Mandatory? | Description |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | Penalty Rate | Decimal | \(12,2\) | Yes | The Penalty charged by percentage |
| 2 | Min Penalty Amount | Decimal | \(12,2\) | No | The Minimum amount charged as penalty |
| 3 | Flat Amount | Decimal | \(12,2\) | Yes | The pre-decided amount that must be charged as penalty on the amount |
| 4 | From Financial Year | Decimal | \(12,2\) | Yes | The year from which the penalty rate begins |
| 5 | Penalty Start Date | Decimal | \(12,2\) | Yes | The Date from which the penalty amount will be applicable within a financial year |

### Steps to fill Data

1. Download the data template attached to this page.
2. Get a good understanding of all the headers in the template sheet, their data type, size, and definitions by referring to the ‘Data Definition’ section of this document.
3. In case of any doubt, please reach out to the person who has shared this template with you to discuss and clear your doubts.
4. Identify all the different types of penalty amounts \(by percentage/ by a flat amount\) etc and fill them in the provided columns respectively.
5. Fill in the details of the financial year/ date from which the type of defined penalties will be applicable.

## Checklist

The checklist is a set of activities to be performed one the data is filled into a template to ensure data type, size, and format of data is as per the expectation. These activities have been divided into 2 groups as given below.

### Common Checklist

This checklist covers all the activities which are common across the entities.

| Sr. No. | Checklist Parameter | Example |
| :--- | :--- | :--- |
| 1 | Make sure that each and every point in this reference list has been taken care of | [Checklist](../common-config/checklist.md) |

### Entity Specific Checklist

Not Applicable

## Attachments

{% file src="../../../../.gitbook/assets/configuration-data-template-pt-master-4-.xlsx" caption="Configuration Data Template" %}

{% file src="../../../../.gitbook/assets/configuration-sample-data-pt-master-4-.xlsx" caption="Sample Data" %}

