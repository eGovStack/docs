# Trade Type

## Introduction <a href="#introduction" id="introduction"></a>

Once the [Trade Categories](trade-category.md) are defined, the next task is to -

* Define Trade Types
* Map Trade Category to listed Trade Types

The Trade Type can be defined as the next (2nd) level classification of Trade. There can be multiple trade types and the list may vary from one State/ULB to another.

## Data Table <a href="#data-table" id="data-table"></a>

| Sr. No. | Trade Type Code\*    | Trade Type Name\* (In English) | Trade Type Name\* (In Local Language) | Trade Category Code\* |
| ------- | -------------------- | ------------------------------ | ------------------------------------- | --------------------- |
| 1       | TRADE\_TYPE\_MEDICAL | Hospital                       | अस्पताल                               | TC1                   |
| 2       | TRADE\_TYPE\_HOTEL   | Hotels                         | होटल                                  | TC2                   |

The table above contains sample Trade Type data.

## Procedure <a href="#procedure" id="procedure"></a>

### Data Definition <a href="#data-definition" id="data-definition"></a>

| Sr. No. | Column Name                         | Data Type    | Data Size | Is Mandatory? | Description                                                                                          |
| ------- | ----------------------------------- | ------------ | --------- | ------------- | ---------------------------------------------------------------------------------------------------- |
| 1       | Trade Type Code                     | Alphanumeric | 64        | Yes           | The Code assigned to the Trade Type. Eg: TRADE\_TYPE\_MEDICAL is assigned to Hospitals               |
| 3       | Trade Type Name (In English)        | Text         | 256       | Yes           | Name of the Trade Type in English. Eg: Goods, Services etc.                                          |
| 3       | Trade Type Name (In Local Language) | Text         | 256       | Yes           | Name of the Trade Type in Local Language (as decided). Eg: Service is described as “सर्विस” in Hindi |
| 4       | Trade Category Code                 | Reference    | 64        | Yes           | The Code assigned to the [Trade Category](trade-category.md). Eg: TC1 For Goods, TC2 for Services    |

### Steps to fill data <a href="#steps-to-fill-data" id="steps-to-fill-data"></a>

1. Download the data template attached to this page.
2. Refer to the ‘Data Definition’ section of this document to learn more about the template sheet, data type, size, and definitions.
3. Select the relevant Trade Category Code from the available drop-down list of Trade Category. This will map the listed Trade Type to the corresponding Trade Category.
4. Enter a unique Trade Type Code to identify the type of trade.
5. Enter a Trade Type Name (In English).
6. Enter the Trade Type Name (In Local Language).

## Checklist <a href="#checklist" id="checklist"></a>

The checklist contains a set of activities to be performed once the data is filled into a template to ensure data entry requirements are met. These activities have been divided into 2 groups as given below.

### Common Checklist <a href="#common-checklist" id="common-checklist"></a>

This checklist covers all the activities which are common across the entities.

| Sr. No. | Checklist Parameter                                                               | Example                                                                                                                      |
| ------- | --------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| 1       | Make sure that each and every point in this reference list has been taken care of | ​[Checklist](https://docs.digit.org/configure-digit/configuring-master-data-templates/module-setup/common-config/checklist)​ |

### Entity Specific Checklist <a href="#entity-specific-checklist" id="entity-specific-checklist"></a>

This checklist covers the activities which are specific to the entity.

| Sr. No. | Checklist Parameter                                                            | Example                                                     |
| ------- | ------------------------------------------------------------------------------ | ----------------------------------------------------------- |
| 1       | The format of the Trade Type Code defined should be alphanumeric and unique    | <p>TRADE_TYPE_MEDICAL</p><p>TRADE_TYPE_HOTELS</p>           |
| 2       | Trade Type Name (in either language) should not contain any special characters | <p>Hospital: [Allowed]</p><p>#Hospital! : [Not allowed]</p> |

## Attachments <a href="#attachments" id="attachments"></a>

[Configuration Data Templateconfiguration-data-template-trade-master-3-.xlsx - 17KB](https://firebasestorage.googleapis.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-MERG\_iQW5oN4ukgXP8K%2Fsync%2Fe9770eb56cc2e51a013d1df84d2db6092d01f17b.xlsx?generation=1602050605603605\&alt=media)

[Sample Data Templatesample-configuration-data-template-trade-master-filled-3- (1).xlsx - 19KB](https://firebasestorage.googleapis.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-MERG\_iQW5oN4ukgXP8K%2Fsync%2F790e93a747bfd659fd37fcc836eec0aab074bf79.xlsx?generation=1602050605673696\&alt=media)

> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_ ](https://egov.org.in/)_is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
