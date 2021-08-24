# Building Sub Occupancy

## Introduction <a id="introduction"></a>

Building Sub Occupancy details refer to sub-categorization of primary occupancy types. For instance, residential buildings can be further classified as apartments or old age homes depending on the specific usage of the buildings. Refer to the [National Bye-Laws](http://mohua.gov.in/upload/uploadfiles/files/Chap-4.pdf) to view the prescribed list of sub-occupancy types.

## Data Table <a id="data-table"></a>

| Sr. No. | Sub Occupancy Code\* | Sub Occupancy Name\* \(In English\) | Sub Occupancy Name\* \(In Local Language\) | Occupancy Code\* |
| :--- | :--- | :--- | :--- | :--- |
| 1 | OAH | Old Age Home | वृद्धाश्रम | R1 |
| 2 | AF | Apartment/Flat | अपार्टमेंट/ फ्लैट | R1 |
| 3 | FH | Farm House | फार्म हाउस | R1 |

The data given in the table is sample data for reference.

## Procedure <a id="procedure"></a>

### Data Definition <a id="data-definition"></a>

| Sr. No. | Column Name | Data Type | Data Size | Is Mandatory? | Description |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | Sub Occupancy code | Alphameric | 3 | Yes | A unique identifier for the given sub occupancy type |
| 2 | Sub Occupancy Name \(In English\) | Text | 64 | Yes | Names for sub occupancy types. For example - Old age home, apartments, farmhouse |
| 3 | Sub Occupancy Name \(In Local Language\) | Text | 64 | Yes | Names for sub occupancy types in local language e.g. in Hindi, Telugu etc. |
| 4 | Occupancy Code | Reference | 3 | Yes | Corresponding [Building Occupancy](building-occupancy.md) for the given sub occupancy type |

### Steps to fill data <a id="steps-to-fill-data"></a>

1. Download the data template attached to this page.
2. Refer to the ‘Data Definition’ section of this document to understand the headers in the template sheet, their data type, size, and definitions.
3. Reach out to the person who shared the template for further details or to clear your doubts. Identify if the State/ULB has a provision for capturing pipe size for connections.
4. Identify the sub occupancy which is applicable. Refer to [National Bye-Laws](http://mohua.gov.in/upload/uploadfiles/files/Chap-4.pdf) to learn more about occupancy types and names.
5. Go through the checklist to verify the data. Make sure that each and every point mentioned in the checklist is covered.

## Checklist <a id="checklist"></a>

The checklist is a set of activities to be performed once the data is filled into a template to ensure data entry requirements are met. These activities have been divided into 2 groups as given below.

### Common Checklist <a id="common-checklist"></a>

This checklist covers all the activities which are common across the entities.

| Sr. No. | Checklist Parameter | Example |
| :--- | :--- | :--- |
| 1 | Make sure that each and every point in this reference list has been taken care of | ​[Checklist](https://digit-discuss.atlassian.net/wiki/spaces/DO/pages/502203140/Checklist)​ |

### Entity Specific Checklist <a id="entity-specific-checklist"></a>

There is no separate entity-specific checklist for this entity.

## Attachment <a id="attachment"></a>

[Configuration Data Templateconfiguration-data-template-building-sub-occupancy\_v1.xlsx - 10KB](https://firebasestorage.googleapis.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-MERG_iQW5oN4ukgXP8K%2Fsync%2F9623c9b39bae40ecb316f8c20624b8254f5d684f.xlsx?generation=1602050610590764&alt=media)

[Sample Datasub-occupancy-sample-data.xlsx - 10KB](https://firebasestorage.googleapis.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-MERG_iQW5oN4ukgXP8K%2Fsync%2F982704018bd32de71795ae018366ecdd30cb7654.xlsx?generation=1602050610842385&alt=media)

<<<<<<< HEAD
[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation ](https://egov.org.in/)is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).[    
=======


 [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation ](https://egov.org.in/)is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).[  
>>>>>>> 64dca8adbdf64336b1a8203199b3791fa23434fa
](https://docs.digit.org/configure-digit/configuring-master-data-templates/module-setup/obpas-data/building-occupancy)

