# Contractors

## Introduction <a href="#introduction" id="introduction"></a>

A contractor is a person or firm who undertakes a contract to provide materials or labour to perform a service or do a job.

Contractors are basically who takes up the works which are awarded by the State or a ULB for a set period. For Example Construction of New Roads/Bridges, Maintenance of Parks etc.

## Data Table <a href="#data-table" id="data-table"></a>

| Sr. No\* | Name\*            | Contractor Code\* | Permanent Address\*                     | Correspondence Address                        | Registration No.\*    | Contact Person\* | Email ID                    | Mobile No.\* | PAN No.    | GST/TIN No.     | GST registered State/UT | Bank Name | Bank Account No. | IFSC Code    |
| -------- | ----------------- | ----------------- | --------------------------------------- | --------------------------------------------- | --------------------- | ---------------- | --------------------------- | ------------ | ---------- | --------------- | ----------------------- | --------- | ---------------- | ------------ |
| 1        | Rakesh            | RAK00123          | #141/25 2nd Cross koramangala Bangalore | <p>#62 5th main road</p><p>ITPL Bangalore</p> | NIL                   | Rakesh           | Rakesh@gmail.com            | 98XXXXXX45   | AFRXXXX64N | NIL             | NIL                     | ICICI     | 000XXXX1234      | ICICI0XXXX97 |
| 2        | ABC Constructions | ABC00143          | #1/1 8th Main JP Nagar Bangalore        | NIL                                           | Z12345KA2020PTC097654 | Mahesh           | contact@abcconstruction.com | 987XXXXXX65  | PNBXXXX78U | 22AAAAA0000A1Z5 | 22AAAAA0000A1Z5         | HDFC      | 987XXXXX64       | HDFC0XXXX51  |

Data given in the table is a sample data.

## Procedure <a href="#procedure" id="procedure"></a>

### Data Definition <a href="#data-definition" id="data-definition"></a>

| Sr No | Column Name             | Data Type    | Data Size | Is Mandatory? | Definition/ Description                                                                                                                                                                                                                                                              |
| ----- | ----------------------- | ------------ | --------- | ------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 1     | Name                    | Text         | 50        | Yes           | The register Name of the Company/Firm or an Individual Person Name, this will help the user to easily identify the contract assigned and also while generating the bills                                                                                                             |
| 2     | Contractor Code         | Alphanumeric | 50        | Yes           | A unique code that identifies the contractor of the works                                                                                                                                                                                                                            |
| 3     | Permanent Address       | Alphanumeric | 250       | Yes           | Company/Firm permanent address or an Individual Person permanent address, this will help the user to send the hard copy document to the contractor. Example, A signed hard copy of the contract                                                                                      |
| 4     | Correspondence Address  | Alphanumeric | 250       | No            | Alternative address of a Company/Firm or an Individual Person Alternative address                                                                                                                                                                                                    |
| 5     | Registration No         | Alphanumeric | 21        | Yes           | Company/Firm registered number, it’s a unique number assigned by the Registrar of Companies                                                                                                                                                                                          |
| 6     | Contact Person          | Text         | 100       | Yes           | Details of a contact person of an individual or a Company/Firm. This will help the user to contact a person in case of any information required                                                                                                                                      |
| 7     | Email ID                | Alphanumeric | 250       | No            | Company/Firm email Id or an individual person email Id, with the email Id the contractor, can receive the notification related to works and payments                                                                                                                                 |
| 8     | Mobile No               | Alphanumeric | 12        | Yes           | Company/Firm Mobile number or an individual person mobile number, the contractor can receive SMS alerts after the bills are processed                                                                                                                                                |
| 9     | PAN No                  | Alphanumeric | 10        | No            | Company/Firm registered PAN number or an individual person PAN number                                                                                                                                                                                                                |
| 10    | GST/TIN No              | Alphanumeric | 15        | Yes           | GST/TIN No: Company/Firm registered GST/TIN number is a Tax Identification Number                                                                                                                                                                                                    |
| 11    | GST registered State/UT | Alphanumeric | 15        | Yes           | The company/Firm has multiple businesses with the state or union territory a separate registered GST number is a Tax Identification Number                                                                                                                                           |
| 12    | Bank Name               | Text         | 50        | No            | Company/Firm Bank Name in which they hold the account or an individual person Bank account name which he/she holds the account                                                                                                                                                       |
| 13    | Bank Account No         | Alphanumeric | 25        | No            | Company/Firm Bank Account number or an individual person Bank Account number. With the bank account number, the bill payment can be made to the correct account, also while doing the RTGS fund transfer the amount can be transferred to the respective firms or individual account |
| 14    | IFSC Code               | Alphanumeric | 11        | No            | The Bank IFSC code pertaining to the bank account of the Company/Firm or an Individual person holding a bank account, the IFSC code will be a validation check for the bank account provided by the contractor and useful for the user while doing a bill payment via RTGS           |

### Steps to fill data <a href="#steps-to-fill-data" id="steps-to-fill-data"></a>

1. Download the data template attached to this page.
2. Have it open and go through all the headers and understand the meaning of them by referring 'Data Definition' section.
3. Make sure all the headers, its data type, field size and its definition/ description is understood properly. In case of any doubt, please reach out to the person who has shared this document with you to discuss the same and clear out the doubts.
4. Identify all different types of contractors.
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

| Sr. No. | Activity                                                                                                                                                       | Example          |
| ------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------- |
| 1       | The Contractors Code should be alphanumeric and unique                                                                                                         | RAK00123         |
| 2       | The Email ID should be valid Id, email Id should contain the Company/Firm name or an individual personal name before the “@” and the “XXXXX.com” after the “@” | ABCLtd@xeror.com |

## Attachments <a href="#attachments" id="attachments"></a>

{% file src="../../../../.gitbook/assets/Configuration Data Template - Contractor.xlsx" %}

{% file src="../../../../.gitbook/assets/Sample Confugration Data - Contractor.xlsx" %}

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation ](https://egov.org.in/)is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).
