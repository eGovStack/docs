# Structure Sub Type

## Introduction <a href="#introduction" id="introduction"></a>

Structure sub type is the second level of classification of the premises where the trade has to be established and conducted. This is mostly used as management information in the trade detail.

## Data Table <a href="#data-table" id="data-table"></a>

| Sr. No. | Code\* | Structure Sub Type\* (In English) | Structure Sub Type\* (In Local Language) | Structure Type Code\* |
| ------- | ------ | --------------------------------- | ---------------------------------------- | --------------------- |
| 1       | PUCCA  | Pucca                             | पक्का                                    | IMMOVABLE             |
| 2       | KUTCHA | Kutcha                            | कच्चा                                    | IMMOVABLE             |
| 3       | HDV    | Hand Driven Vehicle               | हाथ चालित वाहन                           | MOVABLE               |
| 4       | MDV    | Motor-Driven Vehicle              | मोटर चालित वाहन                          | MOVABLE               |

The table above contains sample data.

## Procedure <a href="#procedure" id="procedure"></a>

### Data Definition <a href="#data-definition" id="data-definition"></a>

| Sr. No. | Column Name                              | Data Type    | Data Size | Is Mandatory? | Definition/ Description                                                                          |
| ------- | ---------------------------------------- | ------------ | --------- | ------------- | ------------------------------------------------------------------------------------------------ |
| 1       | Code                                     | Alphanumeric | 64        | Yes           | Unique code to identify each and every record uniquely                                           |
| 2       | Structure Sub Type\* (In English)        | Text         | 256       | Yes           | Structure sub type in English                                                                    |
| 3       | Structure Sub Type\* (In Local Language) | Text         | 256       | Yes           | Structure sub type in local language e.g. in Hindi, Telugu etc.                                  |
| 4       | Structure Type Code\*                    | Reference    | 64        | Yes           | Unique code of structure type to establish the mapping with [Structure Type](structure-type.md)​ |

### Steps to fill data <a href="#steps-to-fill-data" id="steps-to-fill-data"></a>

1. Download the data template attached to this page.
2. Refer to the ‘Data Definition’ section of this document for more details on data type, size, and definitions.
3. Contact the person who shared this template with you to discuss and clear your doubts.
4. Enter the relevant structure sub types with its proper mapping with structure type.
5. Verify the data once again by going through the checklist and making sure that each and every point mentioned in the checklist is covered.

## Checklist <a href="#checklist" id="checklist"></a>

The checklist is a set of activities to be performed once the data is filled into a template to ensure data type, size, and format of data is as per specifications. These activities have been divided into 2 groups as given below.

### Common Checklist <a href="#common-checklist" id="common-checklist"></a>

This checklist covers all the activities which are common across the entities.

| Sr. No. | Checklist Parameter                                                                | Example                                                                                                                      |
| ------- | ---------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| 1       | Make sure that each and every point in this reference list has been taken care of. | ​[Checklist](https://docs.digit.org/configure-digit/configuring-master-data-templates/module-setup/common-config/checklist)​ |

### Entity Specific Checklist <a href="#entity-specific-checklist" id="entity-specific-checklist"></a>

A separate entity-specific checklist is not needed for this entity data template.

## Attachments <a href="#attachments" id="attachments"></a>

[Configuration Data Templateconfiguration-data-template-structure-subtype\_v1-1-.xlsx - 10KB](https://firebasestorage.googleapis.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-MERG\_iQW5oN4ukgXP8K%2Fsync%2F22b0351de7b97362c96dc5633fd44b0313b227ae.xlsx?generation=1602050605311724\&alt=media)

[Sample Datasample-configuraion-data-structure-type-and-subtype-2-.xlsx - 9KB](https://firebasestorage.googleapis.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-MERG\_iQW5oN4ukgXP8K%2Fsync%2F478873bdc35f083420d570fd5618be561e495cb8.xlsx?generation=1602050605458562\&alt=media)

> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_ ](https://egov.org.in/)_is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
