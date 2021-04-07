# SMS Account Configuration

### Introduction

The SMS service is a way of communicating necessary information/updates to the users on their various transactions on DIGIT applications.

In order to update the users, there are certain notification parameters that are system configured for various steps in the application process. These configurations can be changed/reconfigured based upon the ULB requirements.

### Data Table

We have the below-mentioned parameters which we use for configuration:

| Sr. No. | Parameter | Value |
| :--- | :--- | :--- |
| 1 | sms.provider.url | www.xyz.com |
| 2 | sms.username.parameter | mnsbihar@001 |
| 3 | sms.username.value | \*\*\* |

{% hint style="info" %}
The data given in the above table is sample data. The parameters and its values are SMS service provided specific and may vary accordingly.
{% endhint %}

### Procedure

For the SMS service to be integrated there are various things for which the vendor more or less guides us for the steps to be followed but below mentioned are a few basic steps and the generic data definitions which could be followed.

#### Data Definition

Below mentioned are the descriptions of the parameters which are needed for configuration:

| Sr. No. | Column Name | Data Type | Data Size | Mandatory | Description |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | Parameter | Alphanumeric | 64 | Yes | The parameter required to be configured |
| 2 | Value | Alphanumeric | 64 | Yes | The corresponding value of the parameter |

{% hint style="info" %}
Parameter names could differ from vendor to vendor.
{% endhint %}

#### Steps to fill Data

Since the SMS service is a vendor delivered service for which the below steps would have to be followed:

1. Download the data template attached to this page.
2. Get a good understanding of all the headers in the template sheet, their data type, size, and definitions by referring to the ‘Data Definition’ section of this document.
3. In case of any doubt, please reach out to the person who has shared this template with you to discuss and clear your doubts.
4. The SMS vendor has to provide the data in the data template attached.
5. Verify the data once again by going through the checklist and making sure that each and every point mentioned in the checklist is covered.

### Checklist

The checklist is a set of activities to be performed one the data is filled into a template to ensure data type, size, and format of data is as per the expectation. These activities have been divided into 2 groups as given below.

#### Common Checklist

This checklist covers all the activities which are common across the entities.

| Sr. No. | Checklist Parameter | Example |
| :--- | :--- | :--- |
| 1 | Make sure that each and every point in this reference list has been taken care of. | [Checklist](../../module-setup/common-config/checklist.md) |

#### Entity Specific Checklist

This checklist covers the activities which are specific to the entity.

| Sr. No. | Checklist Parameter | Example |
| :--- | :--- | :--- |
| 1 | Make sure that the vendor should support multiple language functionality and especially the local language of the state. | - |

### Attachments

{% file src="../../../../.gitbook/assets/configurable-data-template-sms\_configuration\_v1.xlsx" caption="Configuration Data Template" %}

{% file src="../../../../.gitbook/assets/configurable-sample-data-template-sms-account-configuration\_v1.xlsx" caption="Sample Data Template" %}

