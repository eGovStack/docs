# Usage Category Detail

### Introduction

The Usage category could be more detailed out on classifying them further and detailing more specifically on what kind of usage it is such as hotel, shops, community centre etc.

### Data Table

Below mentioned is the definition of the template which is used in data gathering:

| Sr.No. | Usage Category Detail Code\* | Usage Category Sub Minor Code\* | Usage Category Detail \(In English\)\* | Usage Category Detail \(In Local Language\)\* | Effective From Financial Year\* |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1. | RED | RESIDENTIAL |  | आवासीय | 2019-20 |
| 2. | NONRED | HOTELS |  | होटल पेईग गेस्ट हाउस 10 कमरों तक\(बेगैर वातानुकूलित\) | 2018-19 |

{% hint style="info" %}
 Data given in the table is a sample data.
{% endhint %}

### Procedure

#### Data Definition

| Sr. No. | Column Name | Data Type | Data Size | Mandatory | Description |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | Usage Category Detail Code | Alphanumeric | 64 | Yes | This column ideally contains the code for which the Usage Category Detail is being categorized |
| 2 | Usage Category Sub Minor Code  | Alphanumeric | 64 | Yes | This is the mapping between detail and Sub Minor Code. Refer [Sub Minor ](usage-category-sub-minor.md)entity for more detail |
| 3 | Usage Category Detail Description \(English\)  | Text | 256 | Yes | Description/ Detail of the detail code in which the category is being classified in the English Language |
| 4 | Usage Category Detail Description \(Local Language\)  | Text | 256 | No | Description/ Detail of the detail code in which the category is being classified in Local Language. e.g. Hindi, Telugu etc. |
| 5 | Effective From Financial Year | Numeric |  \(12,2\) | Yes | This is the year from which the category detail has come into effect for property tax |

#### Steps to Fill Data

1. Download the data template attached to this page.
2. Get a good understanding of all the headers in the template sheet, their data type, size, and definitions by referring to the ‘Data Definition’ section of this document.
3. In case of any doubt, please reach out to the person who has shared this template with you to discuss and clear your doubts.
4. Gather all the details for this last classification of Usage Category Detail.
5. Figure out the codes, if not present abbreviate the description so that it creates relevancy between code and description.
6. Get the relations to the sub minor, minor and major.
7. Start filling the template with the codes and description of the usage Category detail and then followed by relative sub minor codes.
8. In the active column fill up weather the category is still active or not.
9. Verify the data once again by going through the checklist and making sure that each and every point mentioned in the checklist is covered.

### Checklist

The checklist is a set of activities to be performed on the data is filled into a template to ensure data type, size, and format of data is as per the expectation. These activities have been divided into 2 groups as given below.

#### Common Checklist

This checklist covers all the activities which are common across the entities.

| Sr. No. | Checklist Parameter | Example |
| :--- | :--- | :--- |
| 1 | Make sure that each and every point in this reference list has been taken care of | [Checklist](../untitled-1/checklist.md) |

#### Entity Specific Checklist

This checklist covers the activities which are specific to the entity.

### Attachments

{% file src="../../../../.gitbook/assets/configurable-data-template-usagetypedetail-v1.xlsx" caption="Configuration Data Template" %}

{% file src="../../../../.gitbook/assets/configurable-sample-data-usagetypedetail-v1.xlsx" caption="Sample Data" %}

