# ULB Bank Accounts

### Introduction

It is a ULB bank account which is operative at least to receive or deposit the day to day revenue collection done by the ULB. It is used by online payment integrator to disburse the amount in ULBs accounts which have been collected through a payment gateway into a pool account managed by the payment gateway.

### Data Table

Below given data table represents the excel template attached. Data given in the table is a sample data.

| Sr. No. | Code\*   | ULB Name\*                     | Bank Name\* | Branch Name\* | Account Number\* | Account Type\* | IFSC\*   |
| ------- | -------- | ------------------------------ | ----------- | ------------- | ---------------- | -------------- | -------- |
| 1       | dehradun | Dehradun Municipal Corporation | SBI         | Rajpur        | XXXX0082XX01     | Saving         | SBIX0921 |
| 2       | haridwar | Haridwar Municipal Corporation | PNB         | Chauk         | XXXX9820XX9      | Saving         | PNBX8320 |

{% hint style="info" %}
Data given in the table is sample data.
{% endhint %}

### Procedure

#### Data Definition

| Sr. No. | Column Name    | Data Type    | Data Size | Is Mandatory | Definition/ Description                                      |
| ------- | -------------- | ------------ | --------- | ------------ | ------------------------------------------------------------ |
| 1       | Code           | Alphanumeric | 64        | Yes          | Unique code is given to the bank detail record e.g. dehradun |
| 2       | ULB Name       | Text         | 256       | Yes          | Name of Urban Local Body                                     |
| 3       | Bank Name      | Text         | 256       | Yes          | Name of the bank where the account exists                    |
| 4       | Branch Name    | Text         | 256       | Yes          | Name of the bank branch where the account exists             |
| 5       | Account Number | Alphanumeric | 64        | Yes          | Bank account number to be used to transfer the amount        |
| 6       | Account Type   | Text         | 256       | Yes          | Account type. e.g. Saving, Current etc.                      |
| 7       | IFSC           | Alphanumeric | 64        | Yes          | IFS code of branch as per FBI guidelines                     |

#### Steps to fill data

1. Download the data template attached to this page.
2. Have it open and go through all the headers and understand the meaning of them by referring 'Data Definition' section.
3. Make sure all the headers, its data type, field size and its definition/ description is understood properly. In case of any doubt, please reach out to the person who has shared this document with you to discuss the same and clear out the doubts.
4. Identify the bank account which is to be used to transfer the amount which is collected online for various services.
5. Start filling the data starting from serial no. and complete a record at once. repeat this exercise until the entire data is filled into a template.
6. Verify the data once again by going through the checklist and taking care of each and every checklist point/ activity mentioned in the checklist.

### Checklist

The checklist is a set of activities to be performed after the data is filled into a template to ensure data type, size, and format of data is as per the expectation. These activities have been divided into 2 groups as given below.

### Common Checklist <a href="#common-checklist" id="common-checklist"></a>

This checklist covers all the activities which are common across the entities.

To see the common checklist refer to the page [Checklist](../../module-setup/common-config/checklist.md) consisting of all the activities which are to be followed to ensure complete and quality data.

#### Entity Specific Checklist

This checklist covers the activities which are specific to the entity.

|             |                                                                  |                                                        |
| ----------- | ---------------------------------------------------------------- | ------------------------------------------------------ |
| **Sr. No.** | **Activity**                                                     | **Example**                                            |
| 1           | Code should not consist of any special characters                | E.g. dehradun is allowed but dehradun@1 is not allowed |
| 2           | The account number should not consist of any special characters. | As issued by the bank                                  |

### Attachments

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)​](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation](https://egov.org.in/) is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).
