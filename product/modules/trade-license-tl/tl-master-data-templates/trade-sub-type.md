# Trade Sub Type

## Introduction <a href="#introduction" id="introduction"></a>

Trade Type can be further sub-classified into Trade Sub Type depending on the trade ontology existing in the ULBs or States. Hence, Hotels can be further classified into Dhabas in North India or Udupis in South India.

Once the[ Trade Type(s)](trade-type.md) are defined, the next task is to -

* Define Trade Sub Types
* Map Trade Types to corresponding Trade Sub Types

## Data Table <a href="#data-table" id="data-table"></a>

| Sr. No. | Trade Sub Type Code\*  | Trade Sub Type Name\* (In English) | Trade Sub Type Name\* (In Local Language) | Trade Type Code\*    |
| ------- | ---------------------- | ---------------------------------- | ----------------------------------------- | -------------------- |
| 1       | TRADE\_SUBTYPE\_CLINIC | Clinic                             | क्लिनिक                                   | TRADE\_TYPE\_MEDICAL |
| 2       | TRADE\_SUBTYPE\_DHABA  | Dhaba                              | ढाबा                                      | TRADE\_TYPE\_HOTEL   |

The table above contains sample data.

## Procedure <a href="#procedure" id="procedure"></a>

### Data Definition <a href="#data-definition" id="data-definition"></a>

| Sr. No. | Column Name                             | Data Type    | Data Size | Is Mandatory? | Description                                                                                             |
| ------- | --------------------------------------- | ------------ | --------- | ------------- | ------------------------------------------------------------------------------------------------------- |
| 1       | Trade Sub Type Code                     | Alphanumeric | 64        | Yes           | The Code assigned to the Trade Sub Type. Eg: TRADE\_TYPE\_Dhaba is assigned to Hotels                   |
| 2       | Trade Sub Type Name (In English)        | Text         | 256       | Yes           | Name of the Trade Sub Type in English. Eg: Clinic                                                       |
| 3       | Trade Sub Type Name (In Local Language) | Text         | 256       | Yes           | Name of the Trade Sub Type in Local Language (as decided). Eg: Dhaba is described as “ढाबा” in Hindi    |
| 4       | Trade Type Code                         | Reference    | 64        | Yes           | The Code assigned to the [Trade Type.](trade-type.md) Eg: TRADE\_TYPE\_MEDICAL is assigned to Hospitals |

### Steps to fill data <a href="#steps-to-fill-data" id="steps-to-fill-data"></a>

1. Download the data template attached to this page.
2. Refer to the ‘Data Definition’ section of this document to learn more about the template sheet, data type, size, and definitions.
3. Select the relevant Trade Type Code from the Trade Type master data. This will map the listed Trade Sub Type to the selected Trade Type.
4. Enter a unique value for Trade Sub Type Code.
5. Enter the English name for Trade Sub Type Name (English).
6. Enter the local name for the Trade Sub Type Name (Local Language).

## Checklist <a href="#checklist" id="checklist"></a>

The checklist contains a set of activities to be performed once the data is filled into a template to ensure data entry requirements are met. These activities have been divided into 2 groups as given below.

### Common Checklist <a href="#common-checklist" id="common-checklist"></a>

This checklist covers all the activities which are common across the entities.

| Sr. No. | Checklist Parameter                                                               | Example                                                                                                                      |
| ------- | --------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| 1       | Make sure that each and every point in this reference list has been taken care of | ​[Checklist](https://docs.digit.org/configure-digit/configuring-master-data-templates/module-setup/common-config/checklist)​ |

### Entity Specific Checklist <a href="#entity-specific-checklist" id="entity-specific-checklist"></a>

This checklist covers the activities which are specific to the entity.

| Sr. No. | Checklist Parameter                                                            | Example                                                 |
| ------- | ------------------------------------------------------------------------------ | ------------------------------------------------------- |
| 1       | The format of the Trade Sub Type Code defined should be text and unique        | TRADE\_SUBTYPE\_CLINIC                                  |
| 2       | Trade Type Name (in either language) should not contain any special characters | <p>Clinic: [Allowed]</p><p>#Clinic! : [Not allowed]</p> |

## Attachments <a href="#attachments" id="attachments"></a>

[Configuration Data Templateconfiguration-data-template-trade-master-3- (1).xlsx - 17KB](https://firebasestorage.googleapis.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-MERG\_iQW5oN4ukgXP8K%2Fsync%2Fe9770eb56cc2e51a013d1df84d2db6092d01f17b.xlsx?generation=1602050605603605\&alt=media)

[Sample Data Templatesample-configuration-data-template-trade-master-filled-3-.xlsx - 19KB](https://firebasestorage.googleapis.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-MERG\_iQW5oN4ukgXP8K%2Fsync%2F790e93a747bfd659fd37fcc836eec0aab074bf79.xlsx?generation=1602050605673696\&alt=media)

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in/) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
