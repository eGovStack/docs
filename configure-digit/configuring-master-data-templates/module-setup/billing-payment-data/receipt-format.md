# Receipt Format

### Introduction

Tax is levied by the government in certain brackets, i.e there are certain components of a tax which sum up and make the final trans-actionable amount. For example, a property tax could have swatch-ta tax, fire cess and certain other components which sum up and make a final amount.

### Data Table

| Sr. No. | Code\* | Service\* | Category\* | Name\* | Is Debit\* | Is Actual Demand\* | Order\* |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | PT\_UNIT\_PENALTY | PT | Penalty | PT Penalty | FALSE | FALSE | 1 |
| 2 | PT\_UNIT\_EXEMPTION | PT | Exemption | PT Exemption | TRUE | TRUE | 2 |

{% hint style="info" %}
Data given in the table is sample data for reference.
{% endhint %}

### Procedure

#### Data Definition

| Sr. No. | Column Name | Data Type | Data Size | Is Mandatory? | Description |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1. | Code | Alphanumeric | 64 | Yes | The code for the tax that is being levied |
| 2. | Service | Text | 256 | Yes | This is the module or the name of the service for which the tax head is being mentioned |
| 3. | Category | Text | 256 | Yes | The category to which the tax head belongs such as Penalty or exemption or cess |
| 4. | Name | Text | 256 | Yes | This is the name/description of the tax head |
| 5. | Is Debit | Text | NA | Yes | In case the tax head is an amount that needs to be added up to the property tax, then this needs to be TRUE else FALSE |
| 6. | Is Actual Demand | Text | NA | Yes | In case the tax head is an amount that needs to be subtracted from the property tax, then this needs to be TRUE else FALSE |
| 7 | Order | Integer | 5 | Yes | The order in which the mentioned tax head should appear on the screen |

#### Steps to fill data

1. Download the data template attached to this page.
2. Get a good understanding of all the headers in the template sheet, their data type, size, and definitions by referring to the ‘Data Definition’ section of this document.
3. In case of any doubt, please reach out to the person who has shared this template with you to discuss and clear your doubts.
4. Get all the tax heads for a particular module and then proceed to the next module.
5. Verify the data once again by going through the checklist and making sure that each and every point mentioned in the checklist is covered.

### Checklist

The checklist is a set of activities to be performed on the data is filled into a template to ensure data type, size, and format of data is as per the expectation. These activities have been divided into 2 groups as given below.

#### Common Checklist

This checklist covers all the activities which are common across the entities.

| Sr. No. | Checklist Parameter | Example |
| :--- | :--- | :--- |
| 1 | Make sure that each and every point in this reference list has been taken care of | [Checklist](../common-config/checklist.md) |

#### Entity Specific Checklist

Not Applicable

### Attachments

{% file src="../../../../.gitbook/assets/configurable-data-template-tax-heads-v1 \(1\).xlsx" caption="Configuration Data Template " %}

{% file src="../../../../.gitbook/assets/configurable-sample-data-tax-heads-v1 \(1\).xlsx" caption="Sample Data" %}

