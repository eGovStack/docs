# Usage Category Sub Minor

## Introduction

This is a further sub-classification of the usage types into sub minor category. Here the properties can be further classified such as commercial food joints etc.

## Data Table

Below mentioned is the data table from the template used to collect the data:

| Sr. No. | Usage Category Sub Minor Code\* | Usage Category Minor Code\* | Usage Category Sub Minor\* \(In English\) | Usage Category Sub Minor\* \(In Local Language\) | Exemption Rate\(In %\) | Max Exemption Amount | Flat Exemption Amount | Effective From Date |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | RESIDENTIAL | RESIDENTIAL | Residential | निवास | 2 | 100 | 200 | 01-04-2020 |
| 2 | RETAIL | COMMERCIAL | Retail | खुदरा | 3 | 300 | 200 | 01-04-2020 |
| 3 | HOTELS | COMMERCIAL | Hotels | होटल | 5.1 | 200 | 300 | 01-04-2020 |

{% hint style="info" %}
Data given in the table is a sample data.
{% endhint %}

## Procedure

### Data Definition

| Sr. No. | Column Name | Data Type | Data Size | Is Mandatory? | Description |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | Usage Category Sub Minor Code | Alphanumeric | 64 | Yes | This is the unique code given to every category |
| 2 | Usage Category Minor Code | Alphanumeric | 64 | Yes | This is the relationship between sub minor and [minor usage categories.](usage-category-minor.md) |
| 3 | Usage Category Sub Minor \(In English\) | Text | 256 | Yes | This is the description of the sub minor category in English |
| 4 | Usage Category Sub Minor \(In Local Language\) | Text | 256 | Yes | This is the description of the sub minor category in Local Language |
| 5 | Exemption Rate \(in % \) | Decimal | \(5,2\) | No | This column defines the % to which the property could be exempted |
| 6 | Max Exemption Amount | Decimal | \(5,2\) | No | This is the maximum amount which the property can be exempted from |
| 7 | Flat Exemption Amount | Decimal | \(5,2\) | No | This is the flat amount by which the property owner can be exempted |
| 8 | Effective From Date | Date | NA | Yes | This the date from which the exemption is applicable. |

### Steps to Fill Data

1. Download the data template attached to this page.
2. Get a good understanding of all the headers in the template sheet, their data type, size, and definitions by referring to the ‘Data Definition’ section of this document.
3. In case of any doubt, please reach out to the person who has shared this template with you to discuss and clear your doubts.
4. Identify all the sub minor categories used across the state.
5. After which identify the codes of all the sub minor categories, if not present abbreviate the description.
6. Get the details\(description\) of these codes.
7. Start filling the template with the codes and description in English and one native language would be helpful.
8. Get the exemption maximum amounts and their respective percentages.
9. Most importantly do get a mapping of these sub minor codes to their parent which is minor usage type.
10. Verify the data once again by going through the checklist and making sure that each and every point mentioned in the checklist is covered.

## Checklist

The checklist is a set of activities to be performed on the data is filled into a template to ensure data type, size, and format of data is as per the expectation. These activities have been divided into 2 groups as given below.

### Common Checklist

This checklist covers all the activities which are common across the entities.

| Sr. No. | Checklist Parameter | Example |
| :--- | :--- | :--- |
| 1 | Make sure that each and every point in this reference list has been taken care of | [Checklist](../untitled-1/checklist.md) |

### Entity Specific Checklist

Not Applicable

## Attachments

{% file src="../../../../.gitbook/assets/configurable-data-template-pt-usagetypesubminor.xlsx" caption="Configuration Data Template" %}

{% file src="../../../../.gitbook/assets/sample-configurable-data-pt-usagetype-minor.xlsx" caption="Sample Data" %}

