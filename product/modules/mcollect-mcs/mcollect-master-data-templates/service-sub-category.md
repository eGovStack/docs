# Service Sub Category

## Introduction <a href="#introduction" id="introduction"></a>

The Service Subcategory refers to the secondary level of services. For instance, the Sanitation Tax service describes the specific tax collection service existing at the ULB level.

Before creating the Service Subcategory make sure you have created the [Service Category](service-category.md) list. Map the Service Subcategory to the corresponding Service Category.

## Data Table <a href="#data-table" id="data-table"></a>

| Sr. No. | Service Subcategory Code\* | Service Subcategory (In English)\* | Service Subcategory (In Local Language)\* | Service Category Code\* | Service Category |
| ------- | -------------------------- | ---------------------------------- | ----------------------------------------- | ----------------------- | ---------------- |
| 1       | SANT0045                   | Sanitation Tax                     | स्वच्छता कर                               | TAX00147                | Taxes            |
| 2       | PEF0478                    | Parks Entry Fee                    | पार्क प्रवेश शुल्क                        | EFEE0785                | Entry Fee        |

The data given in the table is sample data.

## Procedure <a href="#procedure" id="procedure"></a>

### Data Definition <a href="#data-definition" id="data-definition"></a>

| Sr. No. | Column Name                          | Data Type    | Data Size | Is Mandatory? | Definition/ Description                                                                                                                       |
| ------- | ------------------------------------ | ------------ | --------- | ------------- | --------------------------------------------------------------------------------------------------------------------------------------------- |
| 1       | Service Subcategory Code             | Alphanumeric | 50        | Yes           | Unique Identifier for “Service Subcategory”.                                                                                                  |
| 2       | Service Subcategory (English)        | Text         | 250       | Yes           | Name of “Service Subcategory” in English. This will help the user to select the Subcategory name for processing the payment collection        |
| 3       | Service Subcategory (Local Language) | Text         | 250       | Yes           | Name of “Service Subcategory” in Local Language. This will help the user to select the Subcategory name for processing the payment collection |
| 4       | Service Category Code                | Alphanumeric | 50        | Yes           | Unique Identifier for “Service Category”                                                                                                      |
| 5       | Service Category                     | Text         | 250       | No            | The listed Service Subcategory is mapped to the appropriate Service Category                                                                  |

### Steps to Fill Data <a href="#steps-to-fill-data" id="steps-to-fill-data"></a>

1. Download the data template attached to this page.
2. Have it open and go through all the headers and understand the meaning of them by referring 'Data Definition' section.
3. Make sure all the headers, its data type, field size and its definition/ description is understood properly. In case of any doubt, please reach out to the person who has shared this document with you to discuss the same and clear out the doubts.
4. Identify all different types of service subcategory on the basis of ULB’s functions.
5. Start filling the data starting from serial no. and complete a record at once. repeat this exercise until the entire data is filled into a template.
6. Verify the data once again by going through the checklist and taking care of each and every point mentioned in the checklist.

## Checklist <a href="#checklist" id="checklist"></a>

The checklist is a set of activities to be performed once the data is filled into a template to ensure data type, size, and format of data is as per the expectation. These activities have been divided into 2 groups as given below.

### Common Checklist <a href="#common-checklist" id="common-checklist"></a>

This checklist covers all the activities which are common across the entities.

| Sr. No | Checklist Parameter                                                               | Example                                                                                     |
| ------ | --------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------- |
| 1      | Make sure that each and every point in this reference list has been taken care of | ​[Checklist](https://digit-discuss.atlassian.net/wiki/spaces/DO/pages/502203140/Checklist)​ |

### Entity Specific Checklist <a href="#entity-specific-checklist" id="entity-specific-checklist"></a>

This checklist covers the activities which are specific to the entity.

| Sr. No. | Checklist Parameter                                                               | Example                                                                            |
| ------- | --------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------- |
| 1       | The Service Category & Subcategory Name should not contain any special characters | <p>Other Fee and Fines : [Allowed]</p><p>#Other Fee and Fines! : [Not allowed]</p> |

## Attachments <a href="#attachments" id="attachments"></a>

[Configuration Data Templateconfiguration-data-template-service-subcategory.xlsx - 14KB](https://firebasestorage.googleapis.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-MERG\_iQW5oN4ukgXP8K%2Fsync%2F96dcf38f191030c96f69947e33fee5e1d112502c.xlsx?generation=1602050606698292\&alt=media)

[Sample Datasample-confugration-data-service-subcategory.xlsx - 14KB](https://firebasestorage.googleapis.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-MERG\_iQW5oN4ukgXP8K%2Fsync%2Ffc4eef9aa1e71bedd6b65520b393a5daa9f9a06f.xlsx?generation=1602050606698911\&alt=media)

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation ](https://egov.org.in/)is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).
