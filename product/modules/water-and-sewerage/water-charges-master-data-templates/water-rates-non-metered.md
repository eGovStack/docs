# Water Rates (Non-Metered)

## Introduction <a href="#introduction" id="introduction"></a>

Water Charges are recurring charges levied for a pre-defined billing period. The billing period is configurable as per the state or ULB requirement. The rate for calculation of water charges vary widely and is dependent upon various parameters. Charges for water are dependent upon either plot size slab or No. of taps combined with property usage type. In some cases, they can also be solely dependent upon the property usage type.

## Data Table <a href="#data-table" id="data-table"></a>

| Sr. No. | Property Usage Type\* | Property size value from (units) | Property size value to (units) | No. of taps | Rate |
| ------- | --------------------- | -------------------------------- | ------------------------------ | ----------- | ---- |
| 1       | Residential           | 1                                | 150                            | 1           | 200  |
| 2       | Residential           | 151                              | 200                            | 1           | 300  |

The data given in the table is sample data for reference.

## Procedure <a href="#procedure" id="procedure"></a>

### Data Definition <a href="#data-definition" id="data-definition"></a>

| Sr. No. | Column Name                | Data Type    | Data Size | Mandatory | Description                                                                                                |
| ------- | -------------------------- | ------------ | --------- | --------- | ---------------------------------------------------------------------------------------------------------- |
| 1       | Property usage type        | Alphanumeric | 64        | Yes       | Specifies the [property usage type](../../fire-noc/fire-noc-master-data-templates/building-usage-type.md)​ |
| 2       | Slab (Property size value) | Decimal      | (10,2)    | Yes       | From and to value for property size                                                                        |
| 3       | No. of Taps                | Integer      | 2         | Yes       | No. of Taps to be recorded for calculation of water charges                                                |
| 4       | Rate                       | Decimal      | (3,2)     | Yes       | Consumption charges per unit corresponding to the usage type                                               |

### Steps to fill data <a href="#steps-to-fill-data" id="steps-to-fill-data"></a>

1. Download the data template attached to this page.
2. Refer to the ‘Data Definition’ section of this document to learn more about the template sheet, data type, size, and definitions.
3. Please reach out to the person who has shared this template with you to discuss and clear your doubts.
4. Select the property type from the drop-down list available in the Property Usage Type column.
5. Enter the Slab (property size value) range details in the From and To Value for property size.
6. Enter the value for No. of Taps. The water charges will be calculated on the number of taps.
7. Enter the Rate or the per-unit water consumption charges that will be applicable for the listed parameters.
8. Verify the data once again by going through the checklist and making sure that each and every point mentioned in the checklist is covered.

## Checklist <a href="#checklist" id="checklist"></a>

The checklist contains a set of activities to be performed once the data is filled into a template to ensure data entry requirements are met. These activities have been divided into 2 groups as given below.

### Common Checklist <a href="#common-checklist" id="common-checklist"></a>

This checklist covers all the activities which are common across the entities.

| Sr. No. | Checklist Parameter                                                               | Example                                                                                                                      |
| ------- | --------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| 1       | Make sure that each and every point in this reference list has been taken care of | ​[Checklist](https://docs.digit.org/configure-digit/configuring-master-data-templates/module-setup/common-config/checklist)​ |

### Entity Specific Checklist <a href="#entity-specific-checklist" id="entity-specific-checklist"></a>

Separate Entity Specific Checklist is not required for this module data.

## Attachments <a href="#attachments" id="attachments"></a>

[Sample Datasample-configuration-data-water-rates-non-metered-.xlsx - 11KB](https://firebasestorage.googleapis.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-MERG\_iQW5oN4ukgXP8K%2Fsync%2F0f55d992a6fcab23778c55dcc024f79a23e03e34.xlsx?generation=1602050612039921\&alt=media)

[Configuration Data Templateconfiguration-data-template-water-rates-non-metered-.xlsx - 10KB](https://firebasestorage.googleapis.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-MERG\_iQW5oN4ukgXP8K%2Fsync%2F7b5ab0def057cb720d71e3d8498bbef69cf99ded.xlsx?generation=1602050612085919\&alt=media)

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation ](https://egov.org.in)is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).
