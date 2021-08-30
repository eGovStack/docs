# Unit Rates

## Introduction <a id="introduction"></a>

Unit rates are also an important part of property tax. The property tax for a property is calculated on the area covered by the property. These unit rates could differ from ULB to ULB, Ward to Ward, Mohalla to Mohalla and then can be based on different parameters such as Road Type, Property Construction Type etc.

## Data Table <a id="data-table"></a>

| Sr. No. | Boundary Code\* | Boundary Name\* | Parameter 1\* | Parameter 2 | Unit Rate\* |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | M001 | Haldwani Mandir | PUCCA | &lt; 12 m | 1.50 |
| 2 | M001 | Haldwani Mandir | SEMIPUCCA | &gt;= 12 m and &lt;= 24 m | 1.75 |
| 3 | M001 | Haldwani Mandir | KUCCHA | &gt; 24 m | 2.00 |
| 4 | M002 | Kali Mata Mandir Road | SEMIPUCCA | &lt; 12 m | 3.00 |
| 5 | M002 | Kali Mata Mandir Road | SEMIPUCCA | &gt;= 12 m and &lt;= 24 m | 10.00 |
| 6 | M002 | Kali Mata Mandir Road | SEMIPUCCA | &gt; 24 m | 20.00 |

The data given in the table is sample data.

## Procedure <a id="procedure"></a>

### Data Definition <a id="data-definition"></a>

| Sr. No. | Column Name | Data Type | Data Size | Is Mandatory? | Description |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | Boundary Code | Alphanumeric | 64 | Yes | The code of the boundary that is being used, depending upon the client's requirement it could be Mohalla or Ward but has to be from the data collected [here](https://docs.digit.org/configure-digit/configuring-master-data-templates/environment-setup/ulb-level-setup/boundary-data)​ |
| 2 | Boundary Name \(In English\) | Text | 256 | Yes | The name/description of the boundary that is being used for the classification. The names have to be from the data collected [here](https://docs.digit.org/configure-digit/configuring-master-data-templates/environment-setup/ulb-level-setup/boundary-data)​ |
| 3 | Parameter 1 | Alphanumeric | 64 | Yes | This has to be the parameter 1 code on the basis of which the unit rates are being defined |
| 4 | Parameter 2 | Alphanumeric | 64 | No | This is the second parameter\(if available\) on the basis of which the unit rates are being defined |
| 5 | Unit rates | Decimal | \(5,2\) | Yes | The unit rate |

### Steps to fill the data <a id="steps-to-fill-the-data"></a>

1. Download the data template attached to this page.
2. Get a good understanding of all the headers in the template sheet, their data type, size, and definitions by referring to the ‘Data Definition’ section of this document.
3. In case of any doubt, please reach out to the person who has shared this template with you to discuss and clear your doubts.
4. Figure out on what boundary types are the property tax unit rates being defined and start filling that with its code and its name in English in the boundary code and boundary code name column.
5. In case there are more parameters on which the unit rates are being classified such as road type, construction type is being classified, start making a different column for the same starting from parameter 1, parameter 2…
6. Make sure you replace the column name from parameter 1 to the classification on which it is being classified.
7. At the end fill up the unit rates column.
8. Verify the data once again by going through the checklist and making sure that each and every point mentioned in the checklist is covered.

## Checklist <a id="checklist"></a>

The checklist is a set of activities to be performed once the data is filled into a template to ensure data type, size, and format of data is as per the expectation. These activities have been divided into 2 groups as given below.

### Common Checklist <a id="common-checklist"></a>

This checklist covers all the activities which are common across the entities.

| Sr. No. | Checklist Parameter | Example |
| :--- | :--- | :--- |
| 1 | Make sure that each and every point in this reference list has been taken care of | ​[Checklist](https://docs.digit.org/configure-digit/configuring-master-data-templates/module-setup/common-config/checklist)​ |

### Entity Specific Checklist <a id="entity-specific-checklist"></a>

Not Applicable

## Attachments <a id="attachments"></a>

[Configuration Data Templateconfigurable-data-template-property-tax-unit-rate-v1.xlsx - 9KB](https://firebasestorage.googleapis.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-MERG_iQW5oN4ukgXP8K%2Fsync%2F31bcc6aa4444e0a4f89a51dff1e8e6db755a8390.xlsx?generation=1602050608577259&alt=media)

[Sample Dataconfigurable-sample-data-property-tax-unit-rate-v1.xlsx - 10KB](https://firebasestorage.googleapis.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-MERG_iQW5oN4ukgXP8K%2Fsync%2Fa4b79c530ea173efbc465ff0f5034bd917925007.xlsx?generation=1602050608605057&alt=media)

> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_ ](https://egov.org.in/)_is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._

