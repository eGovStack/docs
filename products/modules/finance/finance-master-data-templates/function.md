# Function

## Introduction <a href="#introduction" id="introduction"></a>

Functions shall represent the various functions or services carried out by the ULBs. Functions are provided through various responsibilities centres called Departments.

Functions of the ULB can have three levels within it.

* The first level under this group represents various functions both obligatory and discretionary. Identified as 0 in the template.
* The second Level in function would represent the particular type of service under a function, known as “Function Description”. Identified as 1 in the template
* The third level will represent a particular cost centre, Known as “Cost Centre”, which provides the service. Identified as 2 in the template.

## Data Table <a href="#data-table" id="data-table"></a>

| \*Sr. No. | \*Name                                 | \*Code | \*Level | Parent Type                            | Parent Code |
| --------- | -------------------------------------- | ------ | ------- | -------------------------------------- | ----------- |
| 1         | General Administration                 | 10     | 0       | Nil                                    | Nil         |
| 2         | GENERAL ADMINISTRATION: Administration | 1011   | 1       | General Administration                 | 10          |
| 3         | General Department                     | 101100 | 2       | GENERAL ADMINISTRATION: Administration | 1011        |
| 4         | Public Works                           | 20     | 0       | Nil                                    | Nil         |
| 5         | PUBLIC WORKS: Roads and Pavement       | 2021   | 1       | Public Works                           | 20          |
| 6         | Roads and Building Maintenance         | 202101 | 2       | PUBLIC WORKS: Roads and Pavement       | 2021        |

The data given in the table is sample data.

## Procedure <a href="#procedure" id="procedure"></a>

### Data Definition <a href="#data-definition" id="data-definition"></a>

| Sr No | Column Name | Data Type    | Data Size | Is Mandatory? | Definition/ Description                                                                                                                                                                                                                           |
| ----- | ----------- | ------------ | --------- | ------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1     | Name        | Text         | 250       | Yes           | To indicate the Function name, User can select a particular function code while recording a transaction in the system. This will facilitate in generating a report at the function level                                                          |
| 2     | Code        | Alphanumeric | 50        | Yes           | The unique code is given to the individual function. Child functions have to follow number pattern starting with the parent code                                                                                                                  |
| 3     | Level       | Numeric      | 50        | Yes           | As per NMAM, the Function can be defined in the tree structure, so the Level indicates the structure in which the function would be setup. Root nodes will be level 0 and the next level funds will have value as 1 and the next level as value 2 |
| 4     | Parent Type | Text         | 250       | No            | If the ULB’s using multiple Functions then a Hierarchy of “Parent-Child “can be set up for the Function, so under each Parent Function a multiple child function can be set up                                                                    |
| 5     | Parent Code | Alphanumeric | 50        | No            | The unique code representing the parent type function                                                                                                                                                                                             |

### Steps to fill data <a href="#steps-to-fill-data" id="steps-to-fill-data"></a>

1. Download the data template attached to this page.
2. Have it open and go through all the headers and understand the meaning of them by referring 'Data Definition' section.
3. Make sure all the headers, its data type, field size and its definition/ description is understood properly. In case of any doubt, please reach out to the person who has shared this document with you to discuss the same and clear out the doubts.
4. Identify all different types of Function in the ULB.
5. Start filling the data starting from serial no. and complete a record at once. repeat this exercise until the entire data is filled into a template.
6. Verify the data once again by going through the checklist and taking care of each and every point mentioned in the checklist.

## Checklist <a href="#checklist" id="checklist"></a>

The checklist is a set of activities to be performed once the data is filled into a template to ensure data type, size, and format of data is as per the expectation. These activities have been divided into 2 groups as given below.

### Common Checklist <a href="#common-checklist" id="common-checklist"></a>

This checklist covers all the activities which are common across the entities.

| Sr. No | Checklist Parameter                                                                | Example                                                                                                                      |
| ------ | ---------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| 1      | Make sure that each and every point in this reference list has been taken care of. | ​[Checklist](https://docs.digit.org/configure-digit/configuring-master-data-templates/module-setup/common-config/checklist)​ |

### Entity Specific Checklist <a href="#entity-specific-checklist" id="entity-specific-checklist"></a>

This checklist covers the activities which are specific to the entity.

| Sr. No. | Checklist Parameter                                                                    | Example                                                                                  |
| ------- | -------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------- |
| 1       | The Function Name should not contain any special characters                            | <p>General Administration : [Allowed]</p><p>#General Administration! : [Not allowed]</p> |
| 2       | The Function Code that is defined by the state team should be alphanumeric and Unique. | 10, 1011 or 101100                                                                       |

## Attachments <a href="#attachments" id="attachments"></a>

{% file src="../../../../.gitbook/assets/Configuration Data Template - Function.xlsx" %}

{% file src="../../../../.gitbook/assets/Sample Confugration Data - Function.xlsx" %}

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation ](https://egov.org.in/)is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).
