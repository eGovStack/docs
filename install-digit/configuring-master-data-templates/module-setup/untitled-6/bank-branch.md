# Bank Branch

### Introduction

A Bank branch, banking centre is a retail location where a bank offers a wide array of face-to-face and automated services to its customers.

The list of banks branches\(under Bank list from master\) in which the ULB would have an account in will have to be created here.

### Data Table

| Sr. No. | Bank\* | Bank Code\* | Branch Name/Location\* | Branch Code\* | MICR | Address\* | Contact Person | Phone Number | Narration |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | STATE BANK OF INDIA | SBI | SBI Treasury Branch, Kurnool | 006305 | 518002007 | COLLECTOR COMPLEX DISTT KURNOOL ANDHRA PRADESH | Branch Manager | 0408743462 | Operating Current Accounts |
| 2 | KOTAK MAHINDRA BANK | KKBK | Ucon Plaza Kurnool | 7849 | 518064002 | Ucon Plaza, Park Road Kurnool | Branch Manager | 0812756943 | Nationalized Bank |
| 3 | ANDHRA BANK | ANDB | KRISHNANAGAR \(KURNOOL\) | 001430 | 518011010 | 80/112 Aabbas Nagarabbasnagar,Kurnool 518002 | Branch Manager | 022-2261759 | Nationalized Bank |

{% hint style="info" %}
Data given in the table is a sample data.
{% endhint %}

### Procedure

#### Data Definition

| Sr No | Column Name | Data Type | Data Size | Is Mandatory? | Definition/ Description |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | Bank | Text | 100 | Yes | The Bank Name defines the name of the bank in which the individual or an organization hold the different type of accounts. Click [here](https://m.rbi.org.in/scripts/bs_viewcontent.aspx?Id=3657) for the list of RBI published banks |
| 2 | Bank Code | Alphanumeric | 50 | Yes | The Unique code which represents each bank |
| 3 | Branch Name/Location | Text | 50 | Yes | The Branch Name/Location is the name of the branch of the bank which is registered with Central Bank. It helps to identify any specific branch of the bank |
| 4 | Branch Code | Alphanumeric | 50 | Yes | A unique code that identifies the bank branch, this will help the user to easily identify the bank branch |
| 5 | MICR | Alphanumeric | 50 | No | The MICR Code is used in Local clearing \(this will be in the bottom portion of the cheque\). IFSC Code used for RTGS, IMPS and NEFT transactions in India |
| 6 | Address | Alphanumeric | 50 | Yes | It's the address of the bank where the account is held by the State, the address is likely printed on a bank statement or in the cheque book |
| 7 | Contact Person | Text | 100 | No | A contact person who acts as a channel of communication between the bank and the customer, a contact person is the one who provides relevant information as and when required by the customer |
| 8 | Phone Number | Alphanumeric | 12 | No | A phone number is the registered number of the bank, wherein a customer can contact a bank representative for any kind of banking-related information |
| 9 | Narration | Text | 250 | No | A short narration which represents the bank and branch |

#### Steps to fill data

1. Download the workflow template attached to this page.
2. Have it open and go through all the headers and understand the meaning of them by referring 'Data Definition' section.
3. Make sure all the headers, its data type, field size and its definition/ description is understood properly. In case of any doubt, please reach out to the person who has shared this document with you to discuss the same and clear out the doubts.
4. Identify all bank branches in the state which holds the bank account.
5. Start filling the data starting from serial no. and complete a record at once. repeat this exercise until the entire data is filled into a template.
6. Verify the data once again by going through the checklist and taking care of each and every point mentioned in the checklist.

### Checklist

The checklist is a set of activities to be performed once the data is filled into a template to ensure data type, size, and format of data is as per the expectation. These activities have been divided into 2 groups as given below.

#### Common Checklist

This checklist covers all the activities which are common across the entities.

| Sr. No | Checklist Parameter | Example |
| :--- | :--- | :--- |
| 1 | Make sure that each and every point in this reference list has been taken care of | [Checklist](../untitled-1/checklist.md) |

#### Entity Specific Checklist

This checklist covers the activities which are specific to the entity.

| Sr. No. | Activity | Example |
| :--- | :--- | :--- |
| 1 | The Branch Code should be unique | 006305, 7849 |

### Attachments

{% file src="../../../../.gitbook/assets/configuration-data-template-bank-branch.xlsx" caption="Configuration Data Template" %}

{% file src="../../../../.gitbook/assets/sample-confugration-data-bank-branch.xlsx" caption="Sample Data" %}



