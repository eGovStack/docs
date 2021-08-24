# Usage Category Minor

## Introduction <a id="introduction"></a>

Usage Category Minor is nothing but a further classification of [Usage Category Major](usage-category-major.md), which can be explained as a broad diversification of the usage of your property.

This broad diversification is ideally used to classify the tax amount to which a property could be exempted from.

## Data Table <a id="data-table"></a>

Below mentioned is the data table that is used for collecting data:

| Sr. No | Usage Category Minor Code\* | Usage Category Minor\* \(In English\)\* | Usage Category Minor\* \(In Local Language\) | Exemption Rate \(In %\)\* | Max Exemption Amount | Flat Exemption Amount | Usage Category Major Code\* |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1. | RESIDENTIAL | Residential | आवासीय | NA | 0 | 0 | RESIDENTIAL |
| 2. | COMMERCIAL | Commercial | व्यावसायिक | NA | 0 | 0 | NONRESIDENTIAL |
| 3. | INDUSTRIAL | Industrial | औद्योगिक | NA | 0 | 0 | NONRESIDENTIAL |

Please note that the data mentioned in the table is sample data, however, the state might further update this on the basis of their requirements.

## Procedure <a id="procedure"></a>

### Data Definition <a id="data-definition"></a>

| Sr. No. | Column Name | Data Type | Data Size | Is Mandatory? | Description |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | Usage Category Minor Code | Alphanumeric | 64 | Yes | This is the unique identifier that is given to every category. |
| 2 | Usage Category Minor \(In English\) | Text | 256 | Yes | This is the description of the Minor category in English. |
| 3 | Usage Category Minor \(In Local Language\) | Text | 256 | Yes | This is the description of the Minor Category in the Local Language. |
| 4 | Exemption Rate \(in % \) | Decimal | \(12,2\) | No | This column defines the % to which the property could be exempted. |
| 5 | Max Exemption Amount | Decimal | \(12,2\) | No | This is the maximum amount which the property can be exempted from. |
| 6 | Flat Exemption Amount | Decimal | \(12,2\) | No | The amount that should be exempted for a particular category from the property tax. |
| 7 | Usage Category Major Code | Reference | 256 | Yes | This is the mapping between the minor’s and major’s of the usage category which can be found in [Usage Category Major](usage-category-major.md)​ |

### Steps to fill Data <a id="steps-to-fill-data"></a>

1. Download the data template attached to this page.
2. Get a good understanding of all the headers in the template sheet, their data type, size, and definitions by referring to the ‘Data Definition’ section of this document.
3. In case of any doubt, please reach out to the person who has shared this template with you to discuss and clear your doubts.
4. Gather all the details available for the usage category minor type.
5. Start collecting the codes for the same, if not available abbreviate the description to create a relevant code.
6. Start filling the template with the codes and descriptions for details in the relevant columns.
7. After that start mapping them with the relevant Usage Category major codes.
8. Get the rates as well as amounts for the exemption if any.
9. Verify the data once again by going through the checklist and making sure that each and every point mentioned in the checklist is covered.

## Checklist <a id="checklist"></a>

The checklist is a set of activities to be performed once the data is filled into a template to ensure data type, size, and format of data is as per the expectation. These activities have been divided into 2 groups as given below.

### Common Checklist <a id="common-checklist"></a>

This checklist covers all the activities which are common across the entities.

| Sr. No. | Checklist Parameter | Example |
| :--- | :--- | :--- |
| 1 | Make sure that each and every point in this reference list has been taken care of. | ​[Checklist](https://digit-discuss.atlassian.net/wiki/spaces/DO/pages/502203140/Checklist)​ |

### Entity Specific Checklist <a id="entity-specific-checklist"></a>

Not Applicable

## Attachments <a id="attachments"></a>

[Configuration Data Templateconfigurable-template-pt-usage-type-minor.xlsx - 9KB](https://firebasestorage.googleapis.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-MERG_iQW5oN4ukgXP8K%2Fsync%2F9974ade6753dc7436836b1219ba67e3b6f778340.xlsx?generation=1602050606879651&alt=media)

[Sample Dataconfigurable-sample-data-usage-category-minor.xlsx - 9KB](https://firebasestorage.googleapis.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-MERG_iQW5oN4ukgXP8K%2Fsync%2F0fcd3e83c33a49fa16973195ee31d2af79559692.xlsx?generation=1602050606899959&alt=media)





> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_ ](https://egov.org.in/)_is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._

