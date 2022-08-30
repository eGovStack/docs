# Usage Category Sub Minor

## Introduction <a href="#introduction" id="introduction"></a>

This is a further or third level sub-classification of the property usage types into sub minor category. Here the properties can be further classified such as commercial food joints etc.

## Data Table <a href="#data-table" id="data-table"></a>

Below mentioned is the data table from the template used to collect the data:

| Sr. No. | Usage Category Sub Minor Code\* | Usage Category Minor Code\* | Usage Category Sub Minor\* (In English) | Usage Category Sub Minor\* (In Local Language) | Exemption Rate(In %) | Max Exemption Amount | Flat Exemption Amount | Effective From Date |
| ------- | ------------------------------- | --------------------------- | --------------------------------------- | ---------------------------------------------- | -------------------- | -------------------- | --------------------- | ------------------- |
| 1       | RESIDENTIAL                     | RESIDENTIAL                 | Residential                             | निवास                                          | 2                    | 100                  | 200                   | 01-04-2020          |
| 2       | RETAIL                          | COMMERCIAL                  | Retail                                  | खुदरा                                          | 3                    | 300                  | 200                   | 01-04-2020          |
| 3       | HOTELS                          | COMMERCIAL                  | Hotels                                  | होटल                                           | 5.1                  | 200                  | 300                   | 01-04-2020          |

The data given in the table is sample data.

## Procedure <a href="#procedure" id="procedure"></a>

### Data Definition <a href="#data-definition" id="data-definition"></a>

| Sr. No. | Column Name                                  | Data Type    | Data Size | Is Mandatory? | Description                                                                                        |
| ------- | -------------------------------------------- | ------------ | --------- | ------------- | -------------------------------------------------------------------------------------------------- |
| 1       | Usage Category Sub Minor Code                | Alphanumeric | 64        | Yes           | This is the unique code given to every category                                                    |
| 2       | Usage Category Minor Code                    | Alphanumeric | 64        | Yes           | This is the relationship between sub minor and [minor usage categories.](usage-category-minor.md)​ |
| 3       | Usage Category Sub Minor (In English)        | Text         | 256       | Yes           | This is the description of the sub minor category in English                                       |
| 4       | Usage Category Sub Minor (In Local Language) | Text         | 256       | Yes           | This is the description of the sub minor category in Local Language                                |
| 5       | Exemption Rate (in % )                       | Decimal      | (5,2)     | No            | This column defines the % to which the property could be exempted                                  |
| 6       | Max Exemption Amount                         | Decimal      | (5,2)     | No            | This is the maximum amount which the property can be exempted from                                 |
| 7       | Flat Exemption Amount                        | Decimal      | (5,2)     | No            | This is the flat amount by which the property owner can be exempted                                |
| 8       | Effective From Date                          | Date         | NA        | Yes           | This the date from which the exemption is applicable.                                              |

### Steps to Fill Data <a href="#steps-to-fill-data" id="steps-to-fill-data"></a>

1. Download the data template attached to this page.
2. Get a good understanding of all the headers in the template sheet, their data type, size, and definitions by referring to the ‘Data Definition’ section of this document.
3. In case of any doubt, please reach out to the person who has shared this template with you to discuss and clear your doubts.
4. Identify all the sub minor categories used across the state.
5. After which identify the codes of all the sub minor categories, if not present abbreviate the description.
6. Get the details(description) of these codes.
7. Start filling the template with the codes and description in English and one native language would be helpful.
8. Get the exemption maximum amounts and their respective percentages.
9. Most importantly do get a mapping of these sub minor codes to their parent which is minor usage type.
10. Verify the data once again by going through the checklist and making sure that each and every point mentioned in the checklist is covered.

## Checklist <a href="#checklist" id="checklist"></a>

The checklist is a set of activities to be performed on the data that is filled into a template to ensure data type, size, and format of data is as per the expectation. These activities have been divided into 2 groups as given below.

### Common Checklist <a href="#common-checklist" id="common-checklist"></a>

This checklist covers all the activities which are common across the entities.

| Sr. No. | Checklist Parameter                                                               | Example                                                                                                                      |
| ------- | --------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| 1       | Make sure that each and every point in this reference list has been taken care of | ​[Checklist](https://docs.digit.org/configure-digit/configuring-master-data-templates/module-setup/common-config/checklist)​ |

### Entity Specific Checklist <a href="#entity-specific-checklist" id="entity-specific-checklist"></a>

Not Applicable

## Attachments <a href="#attachments" id="attachments"></a>

{% file src="../../../../.gitbook/assets/Configurable Data Template PT UsageTypeSubMinor.xlsx" %}

{% file src="../../../../.gitbook/assets/Sample Configurable Data PT UsageType Minor.xlsx" %}

> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_ ](https://egov.org.in/)_is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
