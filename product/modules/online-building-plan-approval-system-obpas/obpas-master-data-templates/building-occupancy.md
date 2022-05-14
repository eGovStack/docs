# Building Occupancy

## Introduction <a href="#introduction" id="introduction"></a>

Building Occupancy classifications help in categorizing structures based on the proposed use of the building. Occupancy categories determine the required permits and approvals. The Building Occupancy types data is hence a vital parameter used to define approval workflows in the OBPS module. Refer to the [National Bye-Laws](http://mohua.gov.in/upload/uploadfiles/files/Chap-4.pdf) to view the prescribed list of occupancy types.

## Data Table <a href="#data-table" id="data-table"></a>

| Sr. No. | Occupancy Code\* | Occupancy Name (In English)\* | Occupancy Name (In Local Language) |
| ------- | ---------------- | ----------------------------- | ---------------------------------- |
| 1       | R1               | Residential                   | आवासीय                             |
| 2       | E1               | Educational                   | शैक्षिक                            |
| 3       | I1               | Institutional                 | संस्थागत                           |

The data given in the table is sample data for reference.

## Procedure <a href="#procedure" id="procedure"></a>

### Data Definition <a href="#data-definition" id="data-definition"></a>

| Sr. No. | Column Name                        | Data Type  | Data Size | Is Mandatory? | Description                                                                                                                                                                             |
| ------- | ---------------------------------- | ---------- | --------- | ------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1       | Occupancy Code                     | Alphameric | 2         | Yes           | Unique Code provided with respect to occupancy name. It can be numeric and alphanumeric as well                                                                                         |
| 2       | Occupancy Name (In English)        | Text       | 64        | Yes           | Name provided for occupancy name which is used to configure in the OBPAS module. Refer to [National Bye-Laws](http://mohua.gov.in/upload/uploadfiles/files/Chap-4.pdf) for more details |
| 3       | Occupancy Name (In Local Language) | Text       | 64        | No            | Occupancy Name in the local language. e.g. Hindi, Telugu, etc.                                                                                                                          |

### Steps to fill data <a href="#steps-to-fill-data" id="steps-to-fill-data"></a>

1. Download the data template attached to this page.
2. Refer to the ‘Data Definition’ section of this document to understand the headers in the template sheet, their data type, size, and definitions.
3. Reach out the person who shared the template for further details or to clear your doubts. Identify if the State/ULB has a provision for capturing pipe size for connections.
4. Identify the occupancy which is applicable. Refer to [National Bye-Laws](http://mohua.gov.in/upload/uploadfiles/files/Chap-4.pdf) to learn more about occupancy types and names.
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

[Configauration Data Templateconfiguration-data-template-building-occupancy\_v1.xlsx - 10KB](https://firebasestorage.googleapis.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-MERG\_iQW5oN4ukgXP8K%2Fsync%2F3e0a5de0ab13c9a90abbe5e381b49bf9fd7b535c.xlsx?generation=1602050610332168\&alt=media)

[Sample Datasample-occupancy.xlsx - 11KB](https://firebasestorage.googleapis.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-MERG\_iQW5oN4ukgXP8K%2Fsync%2F3ddb8ba34c232b84662dfe3d0a79a891fd175139.xlsx?generation=1602050610205168\&alt=media)

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation ](https://egov.org.in/)is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).[\
](https://docs.digit.org/configure-digit/configuring-master-data-templates/module-setup/obpas-data/service-wise-documents)
