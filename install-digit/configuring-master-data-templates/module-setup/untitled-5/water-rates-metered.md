# Water Rates \(Metered\)

## Introduction

Water Charges are levied for metered connections based on consumption. The rate for calculation of water charges varies widely and is dependent upon various parameters. In DIGIT W&S module, water charges defined are based on actual consumption and property usage type.

## Data Table

| Sr. No. | \*Property Usage Type | \*Water consumed value from \(units\) | \*Water consumed value to \(units\) | \*Rate \(in Rs/ unit\) |
| :--- | :--- | :--- | :--- | :--- |
| 1 | Residential | 1 | 150 | 3 |
| 2 | Residential | 151 | 300 | 4 |

{% hint style="info" %}
Data given in the table is sample data for reference.
{% endhint %}

## Procedure

### Data Definition

| Sr. No. | Column Name | Data Type | Data Size | Mandatory | Description |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | Property usage type | Alphanumeric | 64 | Yes | Refer [Usage Category Major](../untitled-13/usage-category-major.md) |
| 2 | Water consumed value from | Decimal | \(5,3\) | Yes | From value for water consumed |
| 3 | Water consumed value to | Decimal | \(5,3\) | Yes | To value for water consumed |
| 4 | Rate | Decimal | \(3,3\) | Yes | Consumption charges per unit corresponding to the usage type |

### Steps to fill data

1. Download the data template attached to this page.
2. Refer to the ‘Data Definition’ section of this document to learn more about the template sheet, data type, size, and definitions.
3. Please reach out to the person who has shared this template with you to discuss and clear your doubts.
4. Select the property type from the drop-down list available in the Property Usage Type column.
5. Enter the Slab \(water consumed\) range details in the From and To Value for water consumed.
6. Enter the Rate for the specified slab range and property type.
7. Verify the data once again by going through the checklist and making sure that each and every point mentioned in the checklist is covered.

## Checklist

The checklist is a set of activities to be performed one the data is filled into a template to ensure data type, size, and format of data is as per the expectation. These activities have been divided into 2 groups as given below.

### Common Checklist

This checklist covers all the activities which are common across the entities.

| Sr. No. | Checklist Parameter | Example |
| :--- | :--- | :--- |
| 1 | Make sure that each and every point in this reference list has been taken care of | [Checklist](../untitled-1/checklist.md) |

### Entity Specific Checklist

Separate Entity Specific Checklist is not required for this module data.

## Attachments

{% file src="../../../../.gitbook/assets/configuration-data-template-water-rates-metered-.xlsx" caption="Configuration Data Template " %}

{% file src="../../../../.gitbook/assets/sample-configuration-data-water-rates-metered-.xlsx" caption="Sample Data" %}

