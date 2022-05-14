# Sub Ledger Master

## Introduction <a href="#introduction" id="introduction"></a>

Once the[ SubLedger Category](sub-ledger-category.md) is created the Subledger master need to be defined. The Subledger master will help to record the transaction at the most detailed level. Subledger category is referred to as “Account detail type” here.

By recording the transaction at the Subledger level, detailed reports can be generated.

## Data Table <a href="#data-table" id="data-table"></a>

| Sr. No | Account detail type\* | Name\*               | Code\*       | Narration        |
| ------ | --------------------- | -------------------- | ------------ | ---------------- |
| 1      | Telephone             | 0999784563           | 001          | Telephone Number |
| 2      | Other Creditors       | Park Welfare Society | Park Welfare | Park Welfare     |

The data given in the table is sample data.

## Procedure <a href="#procedure" id="procedure"></a>

### Data Definition <a href="#data-definition" id="data-definition"></a>

| Sr No | Column Name         | Data Type    | Data Size | Is Mandatory? | Definition/ Description                                                                                                                                              |
| ----- | ------------------- | ------------ | --------- | ------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1     | Account Detail Type | Text         | 100       | Yes           | The Account detail type indicates the name of the subledger category name, this will help the user to identify the subledger account while recording the transaction |
| 2     | Name                | Alphanumeric | 50        | Yes           | The name of the subledger master, wherein the user will record the transaction at the most detailed level                                                            |
| 3     | Code                | Alphanumeric | 50        | Yes           | The unique code gives to the Subledger master                                                                                                                        |
| 4     | Narration           | Text         | 250       | No            | A short narration provided to the subledger master                                                                                                                   |

### Steps to fill data <a href="#steps-to-fill-data" id="steps-to-fill-data"></a>

1. Download the workflow template attached to this page.
2. Have it open and go through all the headers and understand the meaning of them by referring 'Data Definition' section.
3. Make sure all the headers, its data type, field size and its definition/ description is understood properly. In case of any doubt, please reach out to the person who has shared this document with you to discuss the same and clear out the doubts.
4. Identify all subledger master details.
5. Start filling the data starting from serial no. and complete a record at once. repeat this exercise until the entire data is filled into a template.
6. Verify the data once again by going through the checklist and taking care of each and every point mentioned in the checklist.

## Checklist <a href="#checklist" id="checklist"></a>

The checklist is a set of activities to be performed once the data is filled into a template to ensure data type, size, and format of data is as per the expectation. These activities have been divided into 2 groups as given below.

### Common Checklist <a href="#common-checklist" id="common-checklist"></a>

This checklist covers all the activities which are common across the entities.

| Sr. No | Checklist Parameter                                                               | Example                                                                                     |
| ------ | --------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------- |
| 1      | Make sure that each and every point in this reference list has been taken care of | ​[Checklist](https://digit-discuss.atlassian.net/wiki/spaces/DO/pages/502203140/Checklist)​ |

### Entity Specific Checklist <a href="#entity-specific-checklist" id="entity-specific-checklist"></a>

This checklist covers the activities which are specific to the entity.

| Sr. No. | Activity                                                                | Example                                                        |
| ------- | ----------------------------------------------------------------------- | -------------------------------------------------------------- |
| 1       | The name should be unique and should not contain any special characters | <p>Telephone : [Allowed]</p><p>#Telephone! : [Not allowed]</p> |

## Attachments <a href="#attachments" id="attachments"></a>

[Configuration Data Templateconfiguration-data-template-subledger-master.xlsx - 12KB](https://firebasestorage.googleapis.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-MERG\_iQW5oN4ukgXP8K%2Fsync%2Fa9db4315805722e39b3da2eb70ea53f1e52dd91a.xlsx?generation=1602050611779355\&alt=media)

[Sample Datasample-confugration-data-subledger-master.xlsx - 12KB](https://firebasestorage.googleapis.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-MERG\_iQW5oN4ukgXP8K%2Fsync%2F5d1e0b4bffa41d1a848cb23d1e18dc7c60c337b7.xlsx?generation=1602050611888534\&alt=media)

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation ](https://egov.org.in/)is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).
