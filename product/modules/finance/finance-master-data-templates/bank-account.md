# Bank Account

## Introduction <a href="#introduction" id="introduction"></a>

A bank account is a financial account maintained by a State in which the financial transactions between the bank and a customer are recorded. Each bank sets the terms and conditions for each type of account it offers, which are classified into commonly understood types, such as deposit accounts, credit card accounts, current accounts, loan accounts or many other types of account.

The list of banks account in which the ULB holds an account in various banks will have to be created here.

## Data Table <a href="#data-table" id="data-table"></a>

| Sr. No.\* | Bank Branch\*                | Bank Branch Code\* | Account number\* | Fund\*         | Account Type (COA Grouping)\*                    | Description                   | Usage Type\*       | Pay to            |
| --------- | ---------------------------- | ------------------ | ---------------- | -------------- | ------------------------------------------------ | ----------------------------- | ------------------ | ----------------- |
| 1         | HDFC Bank - Main City        | HDFC147            | 00063897421      | Municipal Fund | 45020 - Balance with Banks – Main Municipal Fund | 45022 - Other Scheduled Banks | RECEIPTS\_PAYMENTS | Commissioner      |
| 2         | SBI Treasury Branch, Kurnool | SB0012             | 844102001001VN   | Municipal Fund | 45021 - Nationalised Banks                       | PD Account-001                | RECEIPTS\_PAYMENTS | Commissioner, KMC |
| 3         | ICICI Bank                   | ICIC550            | 02042417454076   | Municipal Fund | 45021 - Nationalised Banks                       | P.F. Secondary Edn.Staff      | RECEIPTS\_PAYMENTS | Commissioner      |

The data given in the table is sample data.

## Procedure <a href="#procedure" id="procedure"></a>

### Data Definition <a href="#data-definition" id="data-definition"></a>

| Sr No | Column Name                 | Data Type    | Data Size | Is Mandatory? | Definition/ Description                                                                                                                                                                                                                                                                 |
| ----- | --------------------------- | ------------ | --------- | ------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1     | Bank Branch                 | Text         | 50        | Yes           | The Bank Branch location is the name of the branch of the bank which is registered with Central Bank. It helps to identify any specific branch of the bank                                                                                                                              |
| 2     | Bank Branch Code            | Alphanumeric | 50        | Yes           | A unique code that identifies the bank branch, this will help the user to easily identify the bank branch                                                                                                                                                                               |
| 3     | Account number              | Alphanumeric | 20        | Yes           | The Account number is a Bank Account number in which State holds a bank account. With the bank account number, the bill payment can be made to the correct account, also while doing the RTGS fund transfer the amount can be transferred to the respective firms or individual account |
| 4     | Fund                        | Text         | 50        | Yes           | The Fund indicate the Fund name against each bank account. This will facilitate in support to track the fund amount, receipts and utilization by individual bank account. Click on [Funds ](funds.md)to view the Fund master data                                                       |
| 5     | Account Type (COA Grouping) | Alphanumeric | 250       | Yes           | The Account Type indicates the type of account which the state hold an account in a particular branch of the bank. This is also selected from the list of minor or sub minor codes under “450” Major head                                                                               |
| 6     | Description                 | Text         | 250       | No            | A short description is given to the account type                                                                                                                                                                                                                                        |
| 7     | Usage Type                  | Text         | 250       | Yes           | The Usage type indicates a bank account is used for, whether a particular account is used to make payments or used for collection purpose and used for both receipt & payment purpose                                                                                                   |
| 8     | Pay To                      | Text         | 100       | No            | The “Pay To” indicates payments to be made to a particular bill or paying the relevant government department all the statutory remittances like Provident fund, TDS, etc using the particular bank account                                                                              |

### Steps to fill data <a href="#steps-to-fill-data" id="steps-to-fill-data"></a>

1. Download the workflow template attached to this page.
2. Have it open and go through all the headers and understand the meaning of them by referring 'Data Definition' section.
3. Make sure all the headers, its data type, field size and its definition/ description is understood properly. In case of any doubt, please reach out to the person who has shared this document with you to discuss the same and clear out the doubts.
4. Identify all bank branch within the State.
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

| Sr. No. | Activity                                                | Example                                                                  |
| ------- | ------------------------------------------------------- | ------------------------------------------------------------------------ |
| 1       | The Fund Name should not contain any special characters | <p>Municipal Fund : [Allowed]</p><p>#Municipal Fund! : [Not allowed]</p> |

## Attachments <a href="#attachments" id="attachments"></a>

[Configuration Data Templateconfiguration-data-template-bank-account.xlsx - 10KB](https://firebasestorage.googleapis.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-MERG\_iQW5oN4ukgXP8K%2Fsync%2Fb4b435df2ae3fb65ee73ed7084cea4e009ef65ce.xlsx?generation=1602050611054696\&alt=media)

[Sample Datasample-confugration-data-bank-account.xlsx - 10KB](https://firebasestorage.googleapis.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-MERG\_iQW5oN4ukgXP8K%2Fsync%2F725c1414647abdd95ef1dad7cabd90704b04a59e.xlsx?generation=1602050610998691\&alt=media)

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation ](https://egov.org.in)is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).
