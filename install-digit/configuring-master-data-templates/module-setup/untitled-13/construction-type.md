# Construction Type

## Introduction

The Construction Type refers to the list of Building construction types in the ULB limits considered for tax calculation.

DIGIT Property Tax system has certain pre-defined categories namely :

* Pucca
* Semi Pucca
* Kuccha

## Data Table

| Sr. No. | Construction Type Code\* | Construction Type \(In English\)\* | Construction Type \(In Local Language\)\* |
| :--- | :--- | :--- | :--- |
| 1 | PUCCA | Pakka Building With R.C.C. Roof or R.B. Roof | पक्का भवन, आर0सी0सी0छत या आर0बी0 छत सहित |
| 2 | SEMIPUCCA | Any Other Pakka Building | अन्य पक्का भवन |
| 3 | KUCCHA | Kuccha building that is all other building not covered in clauses \(a\) and \(b\) | कच्चा भवन अर्थात समस्त अन्य भवन जो \(एक\) और \(दो\) में अच्छादित नही है |

{% hint style="info" %}
The data described in the above table is a sample.
{% endhint %}

## Procedure

| Sr. No. | Column Name | Data Type | Data Size | Is Mandatory? | Description |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | Construction Type Code | Alphanumeric | 64 | Yes | Unique Identifier for Construction Type as defined in the Property Master. |
| 2 | Construction Type \( In English\) | Text | 256 | Yes | Nomenclature of “Construction Type” in English. |
| 3 | Construction Type \(In Local Language\) | Text | 256 | Yes | Nomenclature of “Construction Type” in the local language as Telugu, Hindi etc. |

### Steps to fill data

1. Download the data template attached to this page.
2. Refer to the ‘Data Definition’ section of this document to understand the headers in the template sheet, their data type, size, and definitions.
3. Reach out the person who shared the template for further details or to clear your doubts. Identify if the State/ULB has a provision for capturing pipe size for connections.
4. Identify the construction types applicable and fill into the given template.
5. Go through the checklist to verify the data. Make sure that each and every point mentioned in the checklist is covered.

## Checklist

The checklist is a set of activities to be performed once the data is filled into a template to ensure data type, size, and format of data is as per the expectation. These activities have been divided into 2 groups as given below.

### Common Checklist

This checklist covers all the activities which are common across the entities.

| Sr. No. | Checklist Parameter | Example |
| :--- | :--- | :--- |
| 1 | Make sure that each and every point in this reference list has been taken care of | [Checklist](../untitled-1/checklist.md) |

### Entity Specific Checklist

There is no checklist applicable separately to this entity.

## Attachments

{% file src="../../../../.gitbook/assets/configuration-data-template-pt-master.xlsx" caption="Configuration Data Template" %}

{% file src="../../../../.gitbook/assets/configuration-sample-data-pt-master.xlsx" caption="Sample Data" %}

