# Town Planning Schemes

## Introduction <a href="#introduction" id="introduction"></a>

Town Planning Schemes masters list contains all building plan approval schemes and sub-schemes available for the benefits of the citizens. Create a list of the available schemes and map these schemes to specific Occupancy Types.

## Data Table <a href="#data-table" id="data-table"></a>

| Sr. No. | Code | Sub Scheme\*                | Scheme\*                  | Occupancy Code\* | Occupancy Name |
| ------- | ---- | --------------------------- | ------------------------- | ---------------- | -------------- |
| 1       | SCM1 | Sub scheme 1 for Ward No. 1 | DTP Scheme for Ward No. 1 | R1               | Residential    |
| 2       | SCM2 | Sub scheme 2 for Ward No. 1 | DTP Scheme for Ward No. 1 | C1               | Commercial     |
| 3       | SCM3 | Sub scheme 1 for Ward No. 7 | DTP Scheme for Ward No. 7 | C1               | Commercial     |

Data given in the table is sample data for reference.

## Procedure <a href="#procedure" id="procedure"></a>

### Data Definition <a href="#data-definition" id="data-definition"></a>

| Sr. No. | Column Name    | Data Type    | Data Size | Is Mandatory? | Description                                                                                 |
| ------- | -------------- | ------------ | --------- | ------------- | ------------------------------------------------------------------------------------------- |
| 1       | Code           | Alphanumeric | 64        | Yes           | Unique code to record                                                                       |
| 2       | Sub scheme     | Text         | 256       | Yes           | Sub scheme name                                                                             |
| 3       | Scheme         | Text         | 256       | Yes           | Name of the schemes available at a ULB/state level                                          |
| 4       | Occupancy Code | Alphanumeric | 64        | Yes           | Occupancy code - Refer to [Building Occupancy](building-occupancy.md) to know more about it |
| 5       | Occupancy Name | Text         | 64        | No            | Name provided for occupancy in [Building Occupancy](building-occupancy.md)​                 |

### Steps to fill data <a href="#steps-to-fill-data" id="steps-to-fill-data"></a>

1. Download the data template attached to this page.
2. Refer to the ‘Data Definition’ section of this document to understand the headers in the template sheet, their data type, size, and definitions.
3. Reach out to the person who shared the template for further details or to clear your doubts. Identify if the State/ULB has a provision for capturing pipe size for connections.
4. Identify all the scheme and sub-schemes and fill into the given template.
5. Go through the checklist to verify the data. Make sure that each and every point mentioned in the checklist is covered.

## Checklist <a href="#checklist" id="checklist"></a>

The checklist is a set of activities to be performed once the data is filled into a template to ensure data entry requirements are met. These activities have been divided into 2 groups as given below.

### Common Checklist <a href="#common-checklist" id="common-checklist"></a>

This checklist covers all the activities which are common across the entities.

| Sr. No. | Checklist Parameter                                                               | Example                                                                                     |
| ------- | --------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------- |
| 1       | Make sure that each and every point in this reference list has been taken care of | ​[Checklist](https://digit-discuss.atlassian.net/wiki/spaces/DO/pages/502203140/Checklist)​ |

### Entity Specific Checklist <a href="#entity-specific-checklist" id="entity-specific-checklist"></a>

There is no separate entity-specific checklist for this entity.

## Attachments <a href="#attachments" id="attachments"></a>

{% file src="../../../../.gitbook/assets/Configurable Data Template  - Scheme_V1.xlsx" %}

{% file src="../../../../.gitbook/assets/Town Planning scheme Sample.xlsx" %}

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation ](https://egov.org.in/)is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).[\
](https://docs.digit.org/configure-digit/configuring-master-data-templates/module-setup/obpas-data/stakeholders-type)
