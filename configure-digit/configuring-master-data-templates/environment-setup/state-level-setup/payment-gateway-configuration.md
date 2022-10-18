# Payment Gateway Configuration

### Introduction

DIGIT has modules which require the user to pay for the service that he/ she is availing for example property tax, trade license etc. . In order to achieve the functionality, we have a common payment gateway developed which acts a liaison between DIGIT apps and external payment gateways (which depends on the client requirements).

This module facilitates payments and lookup of transaction status.

### Data Table

Following are the details required from the payment gateway vendor in order to configure the payment gateway:

| Sr. No | Integration Kit | API Documentation | Redirect Working Key | Merchant Id | Test credential of Debit Card/ Net banking |
| ------ | --------------- | ----------------- | -------------------- | ----------- | ------------------------------------------ |
| 1.     | File Name       | File Name         | XYZ#123              | UDDUK       | File Name                                  |

{% hint style="info" %}
Data given in the table is a sample data.
{% endhint %}

### Procedure

#### Data Definition

| Sr. No. | Column Name                                | Data Type    | Data Size | Is Mandatory? | Definition/ Description                                                                                                                                                            |
| ------- | ------------------------------------------ | ------------ | --------- | ------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1       | Integration Kit                            | Document     | NA        | Yes           | This is a document that is sent by the vendor which contains information on how to integrate the service                                                                           |
| 2       | API Documentation                          | Document     | NA        | Yes           | This is a separate document which is sent by the vendor in order to help ideally helps us to retrieve the transaction status                                                       |
| 3       | Redirect Working Key                       | Alphanumeric | 64        | Yes           | The working key is provided by the vendor for the generation of the redirection URL                                                                                                |
| 4       | Merchant Id                                | Alphanumeric | 64        | Yes           | Merchant id provided by the vendor                                                                                                                                                 |
| 5       | Test credential of Debit Card/ Net Banking | Document     | NA        | Yes           | <p>These are the details of the debit/credit card or net banking credentials which would help us test the gateway</p><p>This contains the card number/Code/Account number etc.</p> |

#### Steps to fill data

The payment gateway is a vendor oriented service that is integrated with different modules in order to facilitate the transactions. Below mentioned are the steps which are followed:

1. The client has to finalize a payment gateway vendor (for example PAYU, Paytm, HDFC, AXIS atc.) depending upon the requirements.
2. Get a good understanding of all the headers in the template sheet, their data type, size, and definitions by referring to the ‘Data Definition’ section of this document.
3. In case of any doubt, please reach out to the person who has shared this template with you to discuss and clear your doubts.
4. After which the details/ documents mentioned in the template would be provided by the vendor.
5. These details are to be received separately for both prods as well as UAT.
6. Get the IP address for UAT and Production environments whitelisted from the vendor.
7. Verify the data once again by going through the checklist and making sure that each and every point mentioned in the checklist is covered.

### Checklist

The checklist is a set of activities to be performed one the data is filled into a template to ensure data type, size, and format of data is as per the expectation. These activities have been divided into 2 groups as given below.

#### Common Checklist

This checklist covers all the activities which are common across the entities.

| Sr. No. | Checklist Parameter                                                               | Example                                                    |
| ------- | --------------------------------------------------------------------------------- | ---------------------------------------------------------- |
| 1       | Make sure that each and every point in this reference list has been taken care of | [Checklist](../../module-setup/common-config/checklist.md) |

#### Entity Specific Checklist

This checklist covers the activities which are specific to the entity.

| Sr. No. | Checklist Parameter                                                                                                                                                    | Example |
| ------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------- |
| 1       | While finalizing a payment gateway vendor make sure that the vendor should support transactions into multiple bank accounts based on the key( which would be tenantid) | -       |
| 2       | Do get the details for both the environments separately i.e UAT and Production                                                                                         | -       |

### Attachments

{% file src="../../../../.gitbook/assets/configurable-data-template-payment-gateway-configuration-v1.xlsx" %}
Configuration Data Template
{% endfile %}

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)​](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation](https://egov.org.in/) is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).
