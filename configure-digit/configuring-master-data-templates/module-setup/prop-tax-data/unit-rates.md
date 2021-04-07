# Unit Rates

### Introduction

Unit rates are also an important part of property tax. The property tax for a property is counted on the are that the property is covering. These unit rates could differ from ULB to ULB, Ward to Ward, Mohalla to Mohalla and then can be based on different parameters such as Road Type, Property Construction Type etc.

### Data Table

| Sr. No. | Boundary Code\* | Boundary Name\* | Parameter 1\* | Parameter 2 | Unit Rate\* |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | M001 | Haldwani Mandir | PUCCA | &lt; 12 m | 1.50 |
| 2 | M001 | Haldwani Mandir | SEMIPUCCA | &gt;= 12 m and &lt;= 24 m | 1.75 |
| 3  | M001 | Haldwani Mandir | KUCCHA | &gt; 24 m | 2.00 |
| 4 | M002 | Kali Mata Mandir Road | SEMIPUCCA | &lt; 12 m | 3.00 |
| 5  | M002 | Kali Mata Mandir Road | SEMIPUCCA | &gt;= 12 m and &lt;= 24 m | 10.00 |
| 6  | M002 | Kali Mata Mandir Road | SEMIPUCCA | &gt; 24 m | 20.00 |

{% hint style="info" %}
 Data given in the table is a sample data.
{% endhint %}

### Procedure

#### Data Definition

| Sr. No. | Column Name | Data Type | Data Size | Is Mandatory? | Description |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | Boundary Code | Alphanumeric | 64 | Yes | The code of the boundary that is being used, depending upon the client's requirement it could be Mohalla or Ward but has to be from the data collected [here](../../environment-setup/ulb-level-setup/boundary-data.md) |
| 2 | Boundary Name \(In English\) | Text | 256 | Yes | The name/description of the boundary that is being used for the classification. The names have to be from the data collected [here](../../environment-setup/ulb-level-setup/boundary-data.md) |
| 3 | Parameter 1 | Alphanumeric | 64 | Yes | This has to be the parameter 1 code on the basis of which the unit rates are being defined |
| 4 | Parameter 2 | Alphanumeric | 64 | No | This is the second parameter\(if available\) on the basis of which the unit rates are being defined |
| 5 | Unit rates | Decimal | \(5,2\) | Yes | The unit rate |

#### Steps to fill the data

1. Download the data template attached to this page.
2. Get a good understanding of all the headers in the template sheet, their data type, size, and definitions by referring to the ‘Data Definition’ section of this document.
3. In case of any doubt, please reach out to the person who has shared this template with you to discuss and clear your doubts.
4. Figure out on what boundary types are the property tax unit rates being defined and start filling that with its code and its name in English in the boundary code and boundary code name column.
5. In case there are more parameters on which the unit rates are being classified such as road type, construction type is being classified, start making a different column for the same starting from parameter 1, parameter 2…
6. Make sure you replace the column name from parameter 1 to the classification on which it is being classified.
7. At the end fill up the unit rates column.
8. Verify the data once again by going through the checklist and making sure that each and every point mentioned in the checklist is covered.

### Checklist

The checklist is a set of activities to be performed one the data is filled into a template to ensure data type, size, and format of data is as per the expectation. These activities have been divided into 2 groups as given below.

#### Common Checklist

This checklist covers all the activities which are common across the entities.

| Sr. No. | Checklist Parameter | Example |
| :--- | :--- | :--- |
| 1 | Make sure that each and every point in this reference list has been taken care of | [Checklist](../common-config/checklist.md) |

#### Entity Specific Checklist

Not Applicable

### Attachments

{% file src="../../../../.gitbook/assets/configurable-data-template-property-tax-unit-rate-v1.xlsx" caption="Configuration Data Template" %}

{% file src="../../../../.gitbook/assets/configurable-sample-data-property-tax-unit-rate-v1.xlsx" caption="Sample Data" %}



