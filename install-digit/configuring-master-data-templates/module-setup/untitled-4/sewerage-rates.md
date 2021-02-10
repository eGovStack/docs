# Sewerage Rates

## Introduction

Sewerage Charges are recurring charges levied for a pre-defined billing period. The billing period is configurable as per the state or ULB requirement. The rate for calculation of sewerage charges can vary widely and is dependent upon various parameters. For instance, they can be dependent either upon plot size slab combined with property usage type or solely dependent upon property usage type. In some cases, sewerage charges can also be levied as a percentage of water charges.

## Data Table

| Sr. No. | \*Property Usage Type | \*Property size slab from \(units\) | \*Property size slab to \(units\) | \*Percentage of water charges \(%\) | \*Flat fee \(in Rs\) | \*Rate |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | Residential | 1 | 150 | 30 | 200 | 5 |
| 2 | Residential | 151 | 300 | 40 | 500 | 10 |

{% hint style="info" %}
Data given in the table is sample data for reference.
{% endhint %}

## Procedure

### Data Definition

| Sr. No. | Column Name | Data Type | Data Size | Mandatory | Description |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | Property usage type | Text | 64 | Yes | Refer to[ property usage type](../untitled-11/building-usage-type.md) |
| 2 | Slab \(Property size value\) | Decimal | \(10,2\) | Yes | From and to value for property size |
| 3 | Flat fee | Decimal | \(3,2\) | Yes | Flat sewerage charges collected based on property usage type |
| 4 | Percentage of water charges | Decimal | \(3,2\) | Yes | Percent value |
| 5 | Rate | Decimal | \(3,2\) | Yes | Consumption charges per unit corresponding to the usage type |

### Steps to fill data

1. Download the data template attached to this page.
2. Refer to the ‘Data Definition’ section of this document to learn more about the template sheet, data type, size, and definitions.
3. Please reach out to the person who has shared this template with you to discuss and clear your doubts.
4. Select the relevant Property Usage Type from the available drop-down list.
5. Enter the From and To value for property size to specify the range applicable for the selected property.
6. Enter the Flat Fee applicable for the selected property and Slab.
7. Enter the applicable Percentage of Water Charges value. The sewerage charges will be calculated as a percentage of the water charges.
8. Enter the corresponding consumption Rate per unit.
9. Verify the data once again by going through the checklist and making sure that each and every point mentioned in the checklist is covered.

## Checklist

The checklist contains a set of activities to be performed once the data is filled into a template to ensure data entry requirements are met. These activities have been divided into 2 groups as given below.

### Common Checklist

This checklist covers all the activities which are common across the entities.

| Sr. No. | Checklist Parameter | Example |
| :--- | :--- | :--- |
| 1 | Make sure that each and every point in this reference list has been taken care of | [Checklist](../untitled-1/checklist.md) |

### Entity Specific Checklist

Separate Entity Specific Checklist is not required for this module data.

## Attachments

{% file src="../../../../.gitbook/assets/configuration-data-template-sewerage-rates.xlsx" caption="Configuration Data Template " %}

{% file src="../../../../.gitbook/assets/sample-configuration-data-sewerage-rates.xlsx" caption="Sample Data" %}

