# Fee Structure

## Introduction <a id="introduction"></a>

The Fee Structure masters list contains the fee details applicable for processing specific services. All fee-related information collected by the authorities during the course of building plan approval is maintained in this masters.

## Data Table <a id="data-table"></a>

| Sr No. | Service Type\* | Application Type\* | Application Subtype | Fee Subtype\* | BPA Fees\* | Amount\* | Calculation Logic |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | new construction | PERMIT APPLICATION | ​ | application fee | Application Fees | 50 | ​ |
| 2 | new construction | PERMIT APPLICATION | Medium Risk | sanction fee | Additional Fees | 0 | ​ |
| 3 | new construction | PERMIT APPLICATION | Low Risk | application fee | Land Development Charges | 50 | ​ |
| 4 | new construction | OCCUPANCY CERTIFICATE | High Risk | sanction fee | Charges for Well | 50 | ​ |

The data given in the table is sample data for reference.

## Procedure <a id="procedure"></a>

### Data Definition <a id="data-definition"></a>

| Sr. No. | Column Name | Data Type | Data Size | Is Mandatory? | Description |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | Service type | Text | 256 | Yes | The type of OBPS service for which the fees is to be collected. Refer to the Data Table above for illustration |
| 2 | Application Type | Text | 256 | Yes | List of application types for which the fees are to be calculated. Refer to the Data Table above for illustration |
| 3 | Application Subtype | Text | 56 | No | Application subtype is mentioned here such as type of risk |
| 4 | Fee Subtype | Text | 256 | Yes | Type of fees so collected to be mentioned here. Refer to the Data Table above for illustration |
| 5 | BPA Fee | Text | 56 | Yes | The type of OBPS service for which the fees is to be collected. Refer to the Data Table above for illustration |
| 6 | Amount | Integer | 6 | Yes | Fee Amount collected is mentioned here. Refer to the Data Table above for illustration |
| 7 | Calculation Logic | Text | 1024 | No | Fees calculation logic if any is mentioned here |

### Steps to fill data <a id="steps-to-fill-data"></a>

1. Download the data template attached to this page.
2. Refer to the ‘Data Definition’ section of this document to understand the headers in the template sheet, their data type, size, and definitions.
3. Reach out to the person who shared the template for further details or to clear your doubts. Identify if the State/ULB has a provision for capturing pipe size for connections.
4. Identify the combination of attributes for with the fee is defined and then fill into the given template.
5. Go through the checklist to verify the data. Make sure that each and every point mentioned in the checklist is covered.

## Checklist <a id="checklist"></a>

The checklist is a set of activities to be performed once the data is filled into a template to ensure data entry requirements are met. These activities have been divided into 2 groups as given below.

### Common Checklist <a id="common-checklist"></a>

This checklist covers all the activities which are common across the entities.

| Sr. No. | Checklist Parameter | Example |
| :--- | :--- | :--- |
| 1 | Make sure that each and every point in this reference list has been taken care of | ​[Checklist](https://docs.digit.org/configure-digit/configuring-master-data-templates/module-setup/common-config/checklist)​ |

### Entity Specific Checklist <a id="entity-specific-checklist"></a>

There is no separate entity-specific checklist for this entity.

## Attachments <a id="attachments"></a>

[Configuration Data Templatefee-structure-template.xlsx - 10KB](https://firebasestorage.googleapis.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-MERG_iQW5oN4ukgXP8K%2Fsync%2Fd19e12b3afdc577209dba70914f0d4e894f82060.xlsx?generation=1602050613594898&alt=media)

[Sample Datafee-structure-sample-data.xlsx - 10KB](https://firebasestorage.googleapis.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-MERG_iQW5oN4ukgXP8K%2Fsync%2Fcc6066f52129bfc25ed8207305d9112f9ce8ee07.xlsx?generation=1602050613362778&alt=media)

<<<<<<< HEAD
[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation ](https://egov.org.in/)is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).[    
=======


 [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation ](https://egov.org.in/)is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).[  
>>>>>>> 64dca8adbdf64336b1a8203199b3791fa23434fa
](https://docs.digit.org/configure-digit/configuring-master-data-templates/module-setup/obpas-data/noc-departments)

