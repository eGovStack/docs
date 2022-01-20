# Funds

## Introduction <a href="#introduction" id="introduction"></a>

A Fund is used to capture activities/ group of activities for which separate books of accounts are required to be maintained. The concept of Funds brings accountability and better transparency

Various Funds are set up in ULB for meeting certain objectives. Income and expenditure under these funds are to be identified and disclosed separately.

Fund Accounting is a self-contained accounting with its own assets, liabilities, revenues, expenditures and fund balance.

## Data Table <a href="#data-table" id="data-table"></a>

| Sr. No\* | Name\*         | Code\* | Identifier | Level\* | Parent Fund |
| -------- | -------------- | ------ | ---------- | ------- | ----------- |
| 1        | Municipal Fund | 01     | 1          | 0       | Nil         |
| 2        | Grant Fund     | 02     | 2          | 0       | Nil         |
| 3        | Public Fund    | 03     | 3          | 0       | Nil         |
| 4        | Pension Fund   | 04     | 4          | 0       | Nil         |

The data given in the table is sample data.

## Procedure <a href="#procedure" id="procedure"></a>

### Data Definition <a href="#data-definition" id="data-definition"></a>

| Sr No | Column Name | Data Type | Data Size | Is Mandatory? | Definition/ Description                                                                                                                                                                                                         |
| ----- | ----------- | --------- | --------- | ------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1     | Name        | Text      | 50        | Yes           | To indicate the Fund name, if there are multiple funds and by following the Fund Accounting method to record the transaction user can select a particular Fund                                                                  |
| 2     | Code        | Numeric   | 50        | Yes           | The unique code gives to the individual fund                                                                                                                                                                                    |
| 3     | Identifier  | Numeric   | 50        | No            | A single character or number which is used as a unique identification for the fund. This identifier is used in the voucher number format                                                                                        |
| 4     | Level       | Numeric   | 50        | Yes           | The Funds can be defined in the tree structure, so the Level indicates the structure in which the funds would be set up. Root nodes will be level 0 and the next level funds will have value as 1 and the next level as value 2 |
| 5     | Parent Fund | Text      | 50        | No            | If the ULB’s using multiple Funds then a Hierarchy of “Parent-Child “can be set up for the Fund, so under each Parent Fund multiple child funds can be set up                                                                   |

### Steps to fill data <a href="#steps-to-fill-data" id="steps-to-fill-data"></a>

1. Download the data template attached to this page.
2. Have it open and go through all the headers and understand the meaning of them by referring 'Data Definition' section.
3. Make sure all the headers, its data type, field size and its definition/ description is understood properly. In case of any doubt, please reach out to the person who has shared this document with you to discuss the same and clear out the doubts.
4. Identify all different types of Funds on the basis of ULB’s functions.
5. Start filling the data starting from serial no. and complete a record at once. repeat this exercise until the entire data is filled into a template.
6. Verify the data once again by going through the checklist and taking care of each and every point mentioned in the checklist.

## Checklist <a href="#checklist" id="checklist"></a>

The checklist is a set of activities to be performed once the data is filled into a template to ensure data type, size, and format of data is as per the expectation. These activities have been divided into 2 groups as given below.

### Common Checklist <a href="#common-checklist" id="common-checklist"></a>

This checklist covers all the activities which are common across the entities.

| Sr. No | Checklist Parameter                                                               | Example                                                                                                                      |
| ------ | --------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| 1      | Make sure that each and every point in this reference list has been taken care of | ​[Checklist](https://docs.digit.org/configure-digit/configuring-master-data-templates/module-setup/common-config/checklist)​ |

### Entity Specific Checklist <a href="#entity-specific-checklist" id="entity-specific-checklist"></a>

This checklist covers the activities which are specific to the entity.

| Sr. No. | Activity                                                                      | Example                                                                  |
| ------- | ----------------------------------------------------------------------------- | ------------------------------------------------------------------------ |
| 1       | The Fund Code that is defined by the state team should be numeric and Unique. | 01                                                                       |
| 2       | The Fund Name should not contain any special characters                       | <p>Municipal Fund : [Allowed]</p><p>#Municipal Fund! : [Not allowed]</p> |

## Attachments <a href="#attachments" id="attachments"></a>

[Configuration Data Templateconfiguration-data-template-fund.xlsx - 12KB](https://firebasestorage.googleapis.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-MERG\_iQW5oN4ukgXP8K%2Fsync%2Ff9dc86ca5ba0981b1306fb82a369fa2b36e3ab36.xlsx?generation=1602050611474699\&alt=media)

[Sample Datasample-confugration-data-fund.xlsx - 12KB](https://firebasestorage.googleapis.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-MERG\_iQW5oN4ukgXP8K%2Fsync%2F1ca40a1602d7e0a128c9334b527330ff0869e54c.xlsx?generation=1602050611469891\&alt=media)

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation ](https://egov.org.in)is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).
