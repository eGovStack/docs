# Boundary Data

## Introduction

This is the next step after collating all the boundary hierarchies which are being used in the state. In a hierarchy, there are certain types of boundary classification and in all the levels there will be a mapping which we could define as a parent-child mapping in order to link certain levels of the classification.

For example, a hierarchy could be:

Administration Hierarchy: City/ULB → Zone → Ward → Locality

In the above-mentioned hierarchy, a City/ULB is being divided into different into zones followed by zones into wards and at the end wards into the locality.

## Data Table

Data has to be collected for every boundary hierarchy type and boundary type with a mapping between the boundary code and its parent boundary code. Following is the table which is to be used across all the hierarchy types.

| Sr. No. | Boundary Code\* | Boundary Name\* \(In English\) | Boundary Name\* \( In Local Language\) | Parent Boundary Code\* | Boundary Type\* | Hierarchy Type Code\* |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | W1 | Ward no.1 | वार्ड नंबर 1 | Z1 | Ward | ADM |
| 2 | W2 | Ward no.2 | वार्ड नंबर 2 | Z1 | Ward | ADM |
| 3 | W3 | Ward no.3 | वार्ड नंबर 3 | Z2 | Ward | ADM |
| 4 | W4 | Ward no.4 | वार्ड नंबर 4 | Z3 | Ward | ADM |

{% hint style="info" %}
Data given in the table is a sample data.
{% endhint %}

## Procedure

### Data Definition

Following is the definition of the data columns which are being used in the template:

| Sr. No. | Column Name | Data Type | Data Size | Is Mandatory? | Description |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | Boundary Code | Alphanumeric | 64 | Yes | This is a code for the sub-classification for a particular boundary. Should be unique across all boundaries defined |
| 2 | Boundary Name \(In English\) | Text | 256 | Yes | The name of the boundary that is being defined in the English language |
| 3 | Boundary Name \(In Local Language\) | Text | 256 | Yes | The name of the boundary that is being defined in the local language of the state e.g. Telugu, Hindi etc. |
| 4 | Parent Boundary Code | Alphanumeric | 64 | Yes | This is the boundary code of the parent which identifies to which parent the child belongs to |
| 5 | Boundary Type | Text | 256 | Yes | The name of the boundary type i.e. Ward, Zone etc. |
| 6 | Hierarchy Type Code | Alphanumeric | 64 | Yes | The code of the [Boundary Hierarchies ](boundary-hierarchies.md)for which this particular boundary is defined |

### Steps to fill data

Following are the steps which should be used to fill the template:

1. Download the data template attached to this page.
2. Get a good understanding of all the headers in the template sheet, their data type, size, and definitions by referring to the ‘Data Definition’ section of this document.
3. In case of any doubt, please reach out to the person who has shared this template with you to discuss and clear your doubts.
4. After Identifying all the boundary hierarchy, get the sub-classification of all the hierarchies.
5. Figure out the codes for all the sub-classification for a particular city/ULB.
6. Start filling the template from the top of the hierarchy in a drill-down approach.
7. A parent-child mapping code has to be created for every boundary level except for the top level.
8. Follow the steps until you reach the last sub-classification.
9. Verify the data once again by going through the checklist and taking care of each and every point mentioned in the checklist.

## Checklist

The checklist is a set of activities to be performed one the data is filled into a template to ensure data type, size, and format of data is as per the expectation. These activities have been divided into 2 groups as given below.

### Common Checklist

This checklist covers all the activities which are common across the entities.

| Sr. No. | Activity | Example |
| :--- | :--- | :--- |
| 1 | Make sure that each and every point in this reference list has been taken care of | [Checklist](../../module-setup/common-config/checklist.md) |

### Entity Specific Checklist

This checklist covers the activities which are specific to the entity.

| Sr. No. | Activity | Example |
| :--- | :--- | :--- |
| 1 | Every boundary type of data should be filled separately | - |

## Attachments

{% file src="../../../../.gitbook/assets/configurable-data-template-boundary-data\_v1.xlsx" caption="Configuration Data Template" %}

{% file src="../../../../.gitbook/assets/configuration-sample-data-boundary-data.xlsx" caption="Sample Data Template" %}

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)​](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation](https://egov.org.in/) is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).

