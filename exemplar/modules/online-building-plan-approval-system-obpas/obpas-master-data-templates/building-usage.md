# Building Usage

## Introduction <a href="#introduction" id="introduction"></a>

The Building Usage data allows States/ULBs to classify the buildings based on occupancy types, sub-types and its actual usage. Permits and approval process are dependent on the Usage type. The Data Table provides the details required to configure the Building Usage types. Refer to the [National Bye-Laws](http://mohua.gov.in/upload/uploadfiles/files/Chap-4.pdf) to view the prescribed list of usage types.

## Data Table <a href="#data-table" id="data-table"></a>

| Sr. No. | Usage Code\* | Usage Name\* (In English) | Usage Name\* (In Local Language) | Sub Occupancy Code\* | Sub Occupancy Name |
| ------- | ------------ | ------------------------- | -------------------------------- | -------------------- | ------------------ |
| 1       | A-AF-AH      | Apartment type            | अपार्टमेंट प्रकार                | AF                   | Apartment/Flat     |
| 2       | A-AF-FR      | Family residential        | परिवार आवासीय                    | AF                   | Apartment/Flat     |
| 3       | A-AF-RF      | Residential flat          | आवासीय फ्लैट                     | AF                   | Apartment/Flat     |

Data given in the table is sample data for reference.

## Procedure <a href="#procedure" id="procedure"></a>

### Data Definition <a href="#data-definition" id="data-definition"></a>

| Sr. No. | Column Name                    | Data Type  | Data Size | Is Mandatory? | Description                                                                                                                           |
| ------- | ------------------------------ | ---------- | --------- | ------------- | ------------------------------------------------------------------------------------------------------------------------------------- |
| 1       | Usage Code                     | Alphameric | 7         | Yes           | Unique Code for listed Usage name. It can be a combination of alphabets and numbers                                                   |
| 2       | Usage Name (In English)        | Text       | 64        | Yes           | Type of usage of the building to be mentioned here                                                                                    |
| 3       | Usage Name (In Local Language) | Text       | 64        | Yes           | Type of usage of the building to be mentioned here                                                                                    |
| 4       | Sub Occupancy Code             | Alphameric | 7         | Yes           | [​Sub Occupancy ](building-sub-occupancy.md)code to be mentioned here. Maps the Building Usage details to specific sub occupancy type |
| 5       | Sub Occupancy Name             | Text       | 64        | No            | ​[Sub Occupancy](building-sub-occupancy.md) Name to be mentioned here. Maps the Building Usage details to specific sub occupancy type |

### Steps to fill data <a href="#steps-to-fill-data" id="steps-to-fill-data"></a>

1. Download the data template attached to this page.
2. Refer to the ‘Data Definition’ section of this document to understand the headers in the template sheet, their data type, size, and definitions.
3. Reach out to the person who shared the template for further details or to clear your doubts. Identify if the State/ULB has a provision for capturing pipe size for connections.
4. Identify all the building usage and its mapping with sub occupancy and then fill into the template.
5. Go through the checklist to verify the data. Make sure that each and every point mentioned in the checklist is covered.

## Checklist <a href="#checklist" id="checklist"></a>

The checklist is a set of activities to be performed once the data is filled into a template to ensure data entry requirements are met. These activities have been divided into 2 groups as given below.

### Common Checklist <a href="#common-checklist" id="common-checklist"></a>

This checklist covers all the activities which are common across the entities.

| Sr. No. | Checklist Parameter                                                               | Example                                                                                                                      |
| ------- | --------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| 1       | Make sure that each and every point in this reference list has been taken care of | ​[Checklist](https://docs.digit.org/configure-digit/configuring-master-data-templates/module-setup/common-config/checklist)​ |

### Entity Specific Checklist <a href="#entity-specific-checklist" id="entity-specific-checklist"></a>

There is no separate entity-specific checklist for this entity.

## Attachments <a href="#attachments" id="attachments"></a>

{% file src="../../../../.gitbook/assets/Configuration data template - Building Usage Type_V1.xlsx" %}

{% file src="../../../../.gitbook/assets/Sample configuration data - Building Usage Type (1).xlsx" %}

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation ](https://egov.org.in/)is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).[\
](https://docs.digit.org/configure-digit/configuring-master-data-templates/module-setup/obpas-data/building-sub-occupancy)
