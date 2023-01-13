# Opening Balances

## Introduction <a href="#introduction" id="introduction"></a>

The debit or credit balance of a ledger account brought forward from the old accounting period to the new accounting period is called the opening balance. This will be the first entry in a ledger account at the beginning of an accounting period. The opening balance is being captured based on Department, fund, function etc are based on how the system is configured.

If a ULB is using another accounting system, firstly ULB should close financial statements in that system. Then the closing balance of the accounts should be updated as an opening balance in the new application.

## Data Table <a href="#data-table" id="data-table"></a>

| Sr No\* | Financial Year\* | Department\*   | Fund Code\* | Function Code\* | Account Code\* | Subledger Category | Entity | Debit   | Credit  |
| ------- | ---------------- | -------------- | ----------- | --------------- | -------------- | ------------------ | ------ | ------- | ------- |
| 1       | 2020-21          | Account Branch | 01          | 000300          | 4101010        | NIL                | NIL    | 1000000 | ​       |
| 2       | 2020-21          | Street Light   | 01          | 202406          | 3301010        | NIL                | NIL    | ​       | 2000000 |
| 3       | 2020-21          | Street Light   | 01          | 202406          | 3401002        | Contractor         | MH003  | ​       | 1000000 |

The data given in the table is sample data.

## Procedure <a href="#procedure" id="procedure"></a>

### Data Definition <a href="#data-definition" id="data-definition"></a>

| Sr No | Column Name        | Data Type    | Data Size | Is Mandatory? | Definition/ Description                                                                                                                                                                                                                                                                         |
| ----- | ------------------ | ------------ | --------- | ------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1     | Financial Year     | Number       | 10        | Yes           | The Financial year indicates the year for the which the opening balances will be entered for the GL accounts. This can be the opening balance of the year or the date from which the system is going live                                                                                       |
| 2     | Department         | Text         | 250       | Yes           | A department indicates to which the GL code is linked, the user while entering the opening balance can select a particular department to which amount will be entered                                                                                                                           |
| 3     | Fund Code          | Alphanumeric | 50        | Yes           | A GL Code can be linked for the validation of the Fund Code, the user while entering the opening balance can select a particular fund code to which amount will be entered                                                                                                                      |
| 4     | Function Code      | Alphanumeric | 50        | Yes           | A GL Code can be linked for the validation of the Function Code, the user while entering the opening balance can select a particular function Code to which amount will be entered                                                                                                              |
| 5     | Account Code       | Alphanumeric | 50        | Yes           | A General Ledger Code (GL Code) is a string of 7 to 9 digit numeric characters assigned to each financial entry in a State/ULB ledger. A GL Code can be assigned to different debit or credit entries to make opening balances. A detailed GL code to be provided to update the opening balance |
| 6     | Subledger Category | Text         | 250       | No            | The Sub Ledger type indicates if the GL code is linked to a sub-ledger account which is contractor, supplier and employee then the user can select the sub-ledger type while entering the opening balances. Click [SubLedger Category ](sub-ledger-category.md)for the master details           |
| 7     | Entity             | Alphanumeric | 50        | No            | When the Sub Ledger is linked to the individual entity, the user can select an entity while entering the opening balances. So when a sub-ledger is “Contractor” then the value here will be “Contractor code”                                                                                   |
| 8     | Credit             | Number       | 50        | No            | If the opening balance for a Financial year or a period of a particular GL account is a credit Balance then the user needs to update the amount under the Credit column                                                                                                                         |
| 9     | Debit              | Number       | 50        | No            | If the opening balance for a Financial year or a period of a particular GL account is a Debit Balance then the user needs to update the amount under the Debit column                                                                                                                           |

### Steps to fill data <a href="#steps-to-fill-data" id="steps-to-fill-data"></a>

1. Download the data template attached to this page.
2. Have it open and go through all the headers and understand the meaning of them by referring 'Data Definition' section.
3. Make sure all the headers, its data type, field size and its definition/ description is understood properly. In case of any doubt, please reach out to the person who has shared this document with you to discuss the same and clear out the doubts.
4. Identify all the Ledger Codes for which opening balance need to be entered.
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

| Sr. No. | Activity                                                                                                                     | Example                                                                                                         |
| ------- | ---------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------- |
| 1       | The Amount cannot be entered in both the Debit and Credit column for a particular GL code.                                   | <p>Debit:100000 [Allowed]</p><p>Debit:10000 Credit:10000 [Not Allowed]</p>                                      |
| 2       | If for a particular account code the data is captured at sub-ledger level then the Sub-ledger and entity should be selected, | <p>Account Head: Security Deposit</p><p>Subledger Type: Contractor:</p><p>Entity: Cont003 (Test Contractor)</p> |

## Attachments <a href="#attachments" id="attachments"></a>

{% file src="../../../../.gitbook/assets/Configuration Data Template - Opening Balance.xlsx" %}

{% file src="../../../../.gitbook/assets/Sample Confugration Data - Opening Balance.xlsx" %}

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation ](https://egov.org.in/)is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).
