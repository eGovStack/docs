# Building Occupancy

## Introduction

Building Occupancy classifications help in categorizing structures based on the proposed use of the building. Occupancy categories determine the required permits and approvals. The Building Occupancy types data is hence a vital parameter used to define approval workflows in the OBPS module. Refer to the [National Bye-Laws](http://mohua.gov.in/upload/uploadfiles/files/Chap-4.pdf) to view the prescribed list of occupancy types.

## Data Table

| Sr. No. | Occupancy Code\* | Occupancy Name \(In English\)\* | Occupancy Name \(In Local Language\) |
| :--- | :--- | :--- | :--- |
| 1 | R1 | Residential | आवासीय |
| 2 | E1 | Educational | शैक्षिक |
| 3 | I1 | Institutional | संस्थागत |

{% hint style="info" %}
Data given in the table is sample data for reference.
{% endhint %}

## Procedure

### Data Definition

| Sr. No. | Column Name | Data Type | Data Size | Is Mandatory? | Description |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | Occupancy Code | Alphameric | 2 | Yes | Unique Code provided with respect to occupancy name. It can be numeric and alphanumeric as well |
| 2 | Occupancy Name \(In English\) | Text | 64 | Yes | Name provided for occupancy name which is used to configure in the OBPAS module. Refer to [National Bye-Laws](http://mohua.gov.in/upload/uploadfiles/files/Chap-4.pdf) for more details |
| 3 | Occupancy Name \(In Local Language\) | Text | 64 | No | Occupancy Name in the local language. e.g. Hindi, Telugu, etc. |

### Steps to fill data

1. Download the data template attached to this page.
2. Refer to the ‘Data Definition’ section of this document to understand the headers in the template sheet, their data type, size, and definitions.
3. Reach out the person who shared the template for further details or to clear your doubts. Identify if the State/ULB has a provision for capturing pipe size for connections.
4. Identify the occupancy which is applicable. Refer to [National Bye-Laws](http://mohua.gov.in/upload/uploadfiles/files/Chap-4.pdf) to learn more about occupancy types and names.
5. Go through the checklist to verify the data. Make sure that each and every point mentioned in the checklist is covered.

## Checklist

The checklist is a set of activities to be performed one the data is filled into a template to ensure data entry requirements are met. These activities have been divided into 2 groups as given below.

### Common Checklist

This checklist covers all the activities which are common across the entities.

| Sr. No. | Checklist Parameter | Example |
| :--- | :--- | :--- |
| 1 | Make sure that each and every point in this reference list has been taken care of | [Checklist](../untitled-1/checklist.md) |

### Entity Specific Checklist

There is no separate entity-specific checklist for this entity.

## Attachments

{% file src="../../../../.gitbook/assets/configuration-data-template-building-occupancy\_v1.xlsx" caption="Configauration Data Template" %}

{% file src="../../../../.gitbook/assets/sample-occupancy.xlsx" caption="Sample Data" %}

