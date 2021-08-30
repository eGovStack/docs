# Sewerage Rates

## Introduction <a id="introduction"></a>

Sewerage Charges are recurring charges levied for a pre-defined billing period. The billing period is configurable as per the state or ULB requirement. The rate for calculation of sewerage charges can vary widely and is dependent upon various parameters. For instance, they can be dependent either upon plot size slab combined with property usage type or solely dependent upon property usage type. In some cases, sewerage charges can also be levied as a percentage of water charges.

## Data Table <a id="data-table"></a>

| Sr. No. | \*Property Usage Type | \*Property size slab from \(units\) | \*Property size slab to \(units\) | \*Percentage of water charges \(%\) | \*Flat fee \(in Rs\) | \*Rate |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | Residential | 1 | 150 | 30 | 200 | 5 |
| 2 | Residential | 151 | 300 | 40 | 500 | 10 |

The data given in the table is sample data for reference.

## Procedure <a id="procedure"></a>

### Data Definition <a id="data-definition"></a>

| Sr. No. | Column Name | Data Type | Data Size | Mandatory | Description |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | Property usage type | Text | 64 | Yes | Refer to [property usage type](https://docs.digit.org/configure-digit/configuring-master-data-templates/module-setup/fire-noc-data/building-usage-type)​ |
| 2 | Slab \(Property size value\) | Decimal | \(10,2\) | Yes | From and to value for property size |
| 3 | Flat fee | Decimal | \(3,2\) | Yes | Flat sewerage charges collected based on property usage type |
| 4 | Percentage of water charges | Decimal | \(3,2\) | Yes | Percent value |
| 5 | Rate | Decimal | \(3,2\) | Yes | Consumption charges per unit corresponding to the usage type |

### Steps to fill data <a id="steps-to-fill-data"></a>

1. Download the data template attached to this page.
2. Refer to the ‘Data Definition’ section of this document to learn more about the template sheet, data type, size, and definitions.
3. Please reach out to the person who has shared this template with you to discuss and clear your doubts.
4. Select the relevant Property Usage Type from the available drop-down list.
5. Enter the From and To value for property size to specify the range applicable for the selected property.
6. Enter the Flat Fee applicable for the selected property and Slab.
7. Enter the applicable Percentage of Water Charges value. The sewerage charges will be calculated as a percentage of the water charges.
8. Enter the corresponding consumption Rate per unit.
9. Verify the data once again by going through the checklist and making sure that each and every point mentioned in the checklist is covered.

## Checklist <a id="checklist"></a>

The checklist contains a set of activities to be performed once the data is filled into a template to ensure data entry requirements are met. These activities have been divided into 2 groups as given below.

### Common Checklist <a id="common-checklist"></a>

This checklist covers all the activities which are common across the entities.

| Sr. No. | Checklist Parameter | Example |
| :--- | :--- | :--- |
| 1 | Make sure that each and every point in this reference list has been taken care of | ​[Checklist](https://docs.digit.org/configure-digit/configuring-master-data-templates/module-setup/common-config/checklist)​ |

### Entity Specific Checklist <a id="entity-specific-checklist"></a>

Separate Entity Specific Checklist is not required for this module data.

## Attachments <a id="attachments"></a>

[Configuration Data Templateconfiguration-data-template-sewerage-rates.xlsx - 10KB](https://firebasestorage.googleapis.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-MERG_iQW5oN4ukgXP8K%2Fsync%2F80deceb62c2e8d189568a594d1a7c037948ef63e.xlsx?generation=1602050613065495&alt=media)

[Sample Datasample-configuration-data-sewerage-rates.xlsx - 11KB](https://firebasestorage.googleapis.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-MERG_iQW5oN4ukgXP8K%2Fsync%2F8d525959729aa74d781b5003f44eaf7520b7e4d2.xlsx?generation=1602050613111052&alt=media)

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation ](https://egov.org.in/)is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).

