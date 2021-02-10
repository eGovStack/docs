# Suppliers

## Introduction

A supplier is a person or business that provides a product or service to another entity. The role of a supplier in business is to provide high-quality products.

A supplier may also be referred to as a vendor who supplies required materials or a product to the State or ULB for the works which need to be executed. \(Example: materials for street light, cable wires for street light etc\)

## Data Table

| Sr. No\* | Name\* | Permanent Address\* | Correspondence Address | Supplier Code\* | Contact Person\* | Email ID\* | Mobile No.\* | PAN No. | Registration No | GST/TIN No. | GST registered State/UT | Bank Name | Bank Account No. | IFSC Code |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | ABC Supplies | \#5 6th main cross opp to ICICI bank Punjab | NIL | ABC134 | Ramesh | abcsupplies@gmail.com | 98XXXXXX21 | APRFN9561B | Nil | 22AAAAA0000A1Z5 | NIL | ICICI | 2XXXX1234XX4 | ICICI00XXXX7 |
| 2 | Suresh Traders | 10 main road Punjab | \#62 5th main road ITPL Punjab | MB0099 | Rakesh | sureshtraders@xyz.com | 98XXXXXXX95 | ARIZG9874C | AYR145U | 22BBBBA0000A1Z5 | 22BBBBA0000A1Z5 | HDFC | 98XXXXX5X4 | HDFC00XXX51 |

{% hint style="info" %}
Data given in the table is a sample data.
{% endhint %}

## Procedure

### Data Definition

| Sr No | Column Name | Data Type | Data Size | Is Mandatory? | Definition/ Description |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | Name | Text | 250 | Yes | The register Name of the Company or an Individual Person Name, this will help the user to easily identify the supplier to raise a Purchase Order and also while generating the bills. |
| 2 | Permanent Address | Text | 250 | Yes | Company permanent address or an Individual Person permanent address, this will help the user to send the hard copy of a Purchase order to the Supplier. |
| 3 | Correspondence Address | Text | 250 | No | Alternative address of a Company or an Individual Person |
| 4 | Supplier Code | Text | 50 | Yes | A unique code that identifies the supplier of the goods |
| 5 | Contact Person: | Text | 250 | Yes | Details of a contact person of an individual or a Company, the user can contact the supplier to get the information and status of the delivery of the goods ordered. |
| 6 | Email ID | Text | 250 | Yes | Company email Id or an individual person email Id, with the email Id the supplier can receive the notification related to purchase order and payments. |
| 7 | Mobile No | Alphanumeric | 12 | Yes | Company Mobile number or an individual person mobile number, the supplier can receive SMS alerts after the bills are processed. |
| 8 | PAN No | Alphanumeric | 10 | No | Company registered PAN number or an individual person PAN number |
| 9 | Registration No | Alphanumeric | 21 | No | Company/Firm registered number, it’s a unique number assigned by the Registrar of Companies. |
| 10 | GST/TIN No | Alphanumeric | 15 | Yes | Company registered GST/TIN number is a Tax Identification Number is a unique 15-digit number. |
| 11 | GST registered State/UT | Alphanumeric | 15 | Yes | The company/Firm has multiple businesses with the state or union territory a separate registered GST number is a Tax Identification Number. |
| 12 | Bank Name | Text | 50 | No | Company Bank Name in which they hold the account or an individual person Bank account name which he/she holds the account |
| 13 | Bank Account No | Alphanumeric | 25 | No | Company Bank Account number or an individual person Bank Account number. With the bank account number, the bill payment can be made to the correct account, also while doing the RTGS fund transfer the amount can be transferred to the respective firms or individual account. |
| 14 | IFSC Code | Alphanumeric | 11 | No | The Bank IFSC code pertaining to the bank account of the Company or an Individual person holding a bank account, the IFSC code will be a validation check for the bank account provided by the contractor and useful for the user while doing a bill payment via RTGS. |

### Steps to fill data

1. Download the data template attached to this page.
2. Have it open and go through all the headers and understand the meaning of them by referring 'Data Definition' section.
3. Make sure all the headers, its data type, field size and its definition/ description is understood properly. In case of any doubt, please reach out to the person who has shared this document with you to discuss the same and clear out the doubts.
4. Identify all different types of suppliers.
5. Start filling the data starting from serial no. and complete a record at once. repeat this exercise until the entire data is filled into a template.
6. Verify the data once again by going through the checklist and taking care of each and every point mentioned in the checklist.

### Common Checklist

This checklist covers all the activities which are common across the entities.

| Sr. No | Checklist Parameter | Example |
| :--- | :--- | :--- |
| 1 | Make sure that each and every point in this reference list has been taken care of. | [Checklist](../untitled-1/checklist.md) |

### Entity Specific Checklist

This checklist covers the activities which are specific to the entity.

| Sr. No. | Activity | Example |
| :--- | :--- | :--- |
| 1 | The Supplier Code should be alphanumeric and unique | ABC134 |
| 2 | The Email ID should be valid Id, email Id should contain the Company/Firm name or an individual personal name before the “@” and the “[XXXXX.com](http://xxxxx.com/)” after the “@” | [abcsupplies@gmail.com](mailto:abcsupplies@gmail.com) |

## Attachments

{% file src="../../../../.gitbook/assets/configuration-data-template-supplier.xlsx" caption="Configuration Data Template" %}

{% file src="../../../../.gitbook/assets/sample-confugration-data-supplier.xlsx" caption="Sample Data" %}

