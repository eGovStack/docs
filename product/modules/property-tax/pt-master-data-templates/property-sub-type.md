# Property Sub Type

## Introduction <a href="#introduction" id="introduction"></a>

The Property Sub Type represents 2nd level classification to the [Property Type ](property-type.md)and provides the option to further classify the property type in sub types. For example property type ‘Built-up’ is further classified into Independent House, A Flat In Apartment and Half Constructed Half Open and considered differently on tax calculation procedure.

## Data Table <a href="#data-table" id="data-table"></a>

| Sr. No. | Property Sub Type Code\* | Property Sub Type\* (In English)   | Property Sub Type\* (In Local Language) | Property Type Code\* |
| ------- | ------------------------ | ---------------------------------- | --------------------------------------- | -------------------- |
| 1       | SHAREDPROPERTY           | Flat / Part of the building        | फ्लैट / भवन का हिस्सा                   | BUILTUP              |
| 2       | INDEPENDENTPROPERTY      | Independent House / Whole Building | स्वतंत्र घर / पूरी इमारत                | BUILTUP              |

The data described in the above table is sample.

## Procedure <a href="#procedure" id="procedure"></a>

| Sr. No. | Column Name                           | Data Type    | Data Size | Is Mandatory? | Description                                                                                                                                                             |
| ------- | ------------------------------------- | ------------ | --------- | ------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1       | Property Sub Type Code                | Alphanumeric | 64        | Yes           | Unique Identifier for property sub type record                                                                                                                          |
| 2       | Property Sub Type (In English)        | Text         | 256       | Yes           | Nomenclature of “Property Sub Type” in English                                                                                                                          |
| 3       | Property Sub Type (In Local Language) | Text         | 256       | Yes           | Nomenclature of “Property Sub Type” in local language e.g. Telugu, Hindi etc.                                                                                           |
| 4       | Property Type Code                    | Reference    | 64        | Yes           | Property Type code referring to the [Property Type](https://docs.digit.org/configure-digit/configuring-master-data-templates/module-setup/prop-tax-data/property-type)​ |

### Steps to fill data <a href="#steps-to-fill-data" id="steps-to-fill-data"></a>

1. Download the data template attached to this page.
2. Refer to the ‘Data Definition’ section of this document to understand the headers in the template sheet, their data type, size, and definitions.
3. Reach out to the person who shared the template for further details or to clear your doubts. Identify if the State/ULB has a provision for capturing pipe size for connections.
4. Identify all the property sub types applicable and fill into the given template.
5. Go through the checklist to verify the data. Make sure that each and every point mentioned in the checklist is covered.

## Checklist <a href="#checklist" id="checklist"></a>

The checklist is a set of activities to be performed once the data is filled into a template to ensure data type, size, and format of data is as per the expectation. These activities have been divided into 2 groups as given below.

### Common Checklist <a href="#common-checklist" id="common-checklist"></a>

This checklist covers all the activities which are common across the entities.

| Sr. No. | Checklist Parameter                                                               | Example                                                                                                                      |
| ------- | --------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| 1       | Make sure that each and every point in this reference list has been taken care of | ​[Checklist](https://docs.digit.org/configure-digit/configuring-master-data-templates/module-setup/common-config/checklist)​ |

### Entity Specific Checklist <a href="#entity-specific-checklist" id="entity-specific-checklist"></a>

There is no separate checklist is applicable to this entity.

## Attachments <a href="#attachments" id="attachments"></a>

[Configuration Data Templateconfiguration-data-template-pt-master-2-.xlsx - 10KB](https://firebasestorage.googleapis.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-MERG\_iQW5oN4ukgXP8K%2Fsync%2Faf47c79c944c953aed463cd5067940fc54d68630.xlsx?generation=1602050605757319\&alt=media)

[Sample Dataconfiguration-sample-data-pt-master-2-.xlsx - 15KB](https://firebasestorage.googleapis.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-MERG\_iQW5oN4ukgXP8K%2Fsync%2Fd22df176b956ad1f9ae35b34ad36e9e12fd6db38.xlsx?generation=1602050605800117\&alt=media)

> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_ ](https://egov.org.in/)_is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
