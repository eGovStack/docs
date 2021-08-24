# Usage Category Detail

## Introduction <a id="introduction"></a>

The Usage category could be more detailed out on classifying them further and detailing more specifically on what kind of usage it is such as hotel, shops, community centre etc.

## Data Table <a id="data-table"></a>

Below mentioned is the definition of the template which is used in data gathering:

| Sr.No. | Usage Category Detail Code\* | Usage Category Sub Minor Code\* | Usage Category Detail \(In English\)\* | Usage Category Detail \(In Local Language\)\* | Effective From Financial Year\* |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1. | RED | RESIDENTIAL | ​ | आवासीय | 2019-20 |
| 2. | NONRED | HOTELS | ​ | होटल पेईग गेस्ट हाउस 10 कमरों तक\(बेगैर वातानुकूलित\) | 2018-19 |

The data given in the table is sample data.

## Procedure <a id="procedure"></a>

### Data Definition <a id="data-definition"></a>

| Sr. No. | Column Name | Data Type | Data Size | Mandatory | Description |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | Usage Category Detail Code | Alphanumeric | 64 | Yes | This column ideally contains the code for which the Usage Category Detail is being categorized |
| 2 | Usage Category Sub Minor Code | Alphanumeric | 64 | Yes | This is the mapping between detail and Sub Minor Code. Refer [Sub Minor](usage-category-sub-minor.md) entity for more detail |
| 3 | Usage Category Detail Description \(English\) | Text | 256 | Yes | Description/ Detail of the detail code in which the category is being classified in the English Language |
| 4 | Usage Category Detail Description \(Local Language\) | Text | 256 | No | Description/ Detail of the detail code in which the category is being classified in Local Language. e.g. Hindi, Telugu etc. |
| 5 | Effective From Financial Year | Numeric | \(12,2\) | Yes | This is the year from which the category detail has come into effect for property tax |

### Steps to Fill Data <a id="steps-to-fill-data"></a>

1. Download the data template attached to this page.
2. Get a good understanding of all the headers in the template sheet, their data type, size, and definitions by referring to the ‘Data Definition’ section of this document.
3. In case of any doubt, please reach out to the person who has shared this template with you to discuss and clear your doubts.
4. Gather all the details for this last classification of Usage Category Detail.
5. Figure out the codes, if not present abbreviate the description so that it creates relevancy between code and description.
6. Get the relations to the sub minor, minor and major.
7. Start filling the template with the codes and description of the usage Category detail and then followed by relative sub minor codes.
8. In the active column fill up whether the category is still active or not.
9. Verify the data once again by going through the checklist and making sure that each and every point mentioned in the checklist is covered.

## Checklist <a id="checklist"></a>

The checklist is a set of activities to be performed on the data that is filled into a template to ensure data type, size, and format of data is as per the expectation. These activities have been divided into 2 groups as given below.

### Common Checklist <a id="common-checklist"></a>

This checklist covers all the activities which are common across the entities.

| Sr. No. | Checklist Parameter | Example |
| :--- | :--- | :--- |
| 1 | Make sure that each and every point in this reference list has been taken care of | ​[Checklist](https://docs.digit.org/configure-digit/configuring-master-data-templates/module-setup/common-config/checklist)​ |

### Entity Specific Checklist <a id="entity-specific-checklist"></a>

This checklist covers the activities which are specific to the entity.

## Attachments <a id="attachments"></a>

[Configuration Data Templateconfigurable-data-template-usagetypedetail-v1.xlsx - 10KB](https://firebasestorage.googleapis.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-MERG_iQW5oN4ukgXP8K%2Fsync%2F6942cf6eb9a3a155480fc89f6271a56d025d04a8.xlsx?generation=1602050610030130&alt=media)

[Sample Dataconfigurable-sample-data-usagetypedetail-v1.xlsx - 10KB](https://firebasestorage.googleapis.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-MERG_iQW5oN4ukgXP8K%2Fsync%2Fa14493959f0f79290a17dc024f39ffecaa73b68f.xlsx?generation=1602050610091898&alt=media)





> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_ ](https://egov.org.in/)_is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._

