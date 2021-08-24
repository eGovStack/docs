# Ownership Sub Category

## Introduction <a id="introduction"></a>

This is a further sub-classification of the ownership which details what is the ownership sub category, whether there is a single owner, multiple owner etc. . An example has been given in the attachments section of the page.

## Data Table <a id="data-table"></a>

The data has to be collected for all the subcategories of ownership type present in the state. Below mentioned is the table of the template that is being used to gather data:

| Sr. No | Ownership Sub Category Code\* | Ownership Category Code\* | Ownership Sub Category\* \(In English\) | Ownership Sub Category\* \(In Local Language\) |
| :--- | :--- | :--- | :--- | :--- |
| 1. | SO | INDIVIDUAL | Single Owner | एकल स्वामी |
| 2. | MO | INDIVIDUAL | Multiple Owner | मल्टीपल ओनर |

## Procedure <a id="procedure"></a>

### Data Definition <a id="data-definition"></a>

| Sr. No. | Column Name | Data Type | Data Size | Is Mandatory? | Description |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | Ownership Sub Category Code | Alphanumeric | 64 | Yes | This is the code that is being used to categorize the sub type |
| 2 | Ownership Category Code | Alphanumeric | 64 | Yes | This is the mapping between the [Ownership Category](https://docs.digit.org/configure-digit/configuring-master-data-templates/module-setup/prop-tax-data/ownership-category) and Sub category |
| 3 | Ownership Sub Category \(In English\) | Text | 256 | Yes | Description of the ownership Sub type in the English Language |
| 4 | Ownership Sub Category \(In Local Language\) | Text | 256 | Yes | Description of the ownership Sub type in Native Language |

### Steps to fill Data <a id="steps-to-fill-data"></a>

1. Download the data template attached to this page.
2. Get a good understanding of all the headers in the template sheet, their data type, size, and definitions by referring to the ‘Data Definition’ section of this document.
3. In case of any doubt, please reach out to the person who has shared this template with you to discuss and clear your doubts.
4. Download the data template attached to this page.
5. Get a good understanding of all the headers in the template sheet, their data type, size, and definitions by referring to the ‘Data Definition’ section of this document.
6. In case of any doubt, please reach out to the person who has shared this template with you to discuss and clear your doubts. First, get all the sub classifications for the listed category.
7. Get the codes and start filling the template.
8. Fill in the codes for the sub category in the 2nd column with the proper mapping of Ownership Type category \(Parent level\).
9. Repeat the steps for all the ownership type categories\(Parent Level\).
10. Verify the data once again by going through the checklist and making sure that each and every point mentioned in the checklist is covered.

## Checklist <a id="checklist"></a>

The checklist is a set of activities to be performed once the data is filled into a template to ensure data type, size, and format of data is as per the expectation. These activities have been divided into 2 groups as given below.

### Common Checklist <a id="common-checklist"></a>

This checklist covers all the activities which are common across the entities.

| Sr. No. | Checklist Parameter | Example |
| :--- | :--- | :--- |
| 1 | Make sure that each and every point in this reference list has been taken care of | ​[Checklist](https://digit-discuss.atlassian.net/wiki/spaces/DO/pages/502203140/Checklist)​ |

### Entity Specific Checklist <a id="entity-specific-checklist"></a>

This checklist covers the activities which are specific to the entity.

| Sr. No. | Checklist Parameter | Example |
| :--- | :--- | :--- |
| 1 | There should be a mapping code between the sub category \(child\) and Property Tax: Ownership Category \(parent level\), no child can be left without a parent | - |
| 2 | Make sure that no code which is not mentioned in the ownership category classification \(parent\) can be used | - |

## Attachments <a id="attachments"></a>

[Configuration Data Templateconfigurable-data-template-pt-ownership-sub-type.xlsx - 9KB](https://firebasestorage.googleapis.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-MERG_iQW5oN4ukgXP8K%2Fsync%2F20020632ba50a7839b6c77f88efb18a1e7c9b416.xlsx?generation=1602050608606474&alt=media)

[Sample Dataconfigurable-sample-data-ownership-sub-category.xlsx - 11KB](https://firebasestorage.googleapis.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-MERG_iQW5oN4ukgXP8K%2Fsync%2F002b181ed44a562658cb2d4b26de33647e6e9feb.xlsx?generation=1602050608757874&alt=media)





> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_ ](https://egov.org.in/)_is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._

