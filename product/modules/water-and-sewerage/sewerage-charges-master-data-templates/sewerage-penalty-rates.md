# Sewerage Penalty Rates

## Introduction <a id="introduction"></a>

The penalty is levied on the consumer if the consumer fails to make the payment for the bill raised before a specified due date. The consumer has to make the full payment before the due date to avoid penalty charges. The number of days after which the penalty is applicable should be configurable at the ULB level.

The penalty can be -

1. Fixed amount; or
2. Percentage: In case of percentage, it can be levied on either
   1. Entire bill amount; or
   2. Balance pending when partial payments have been made

## Data Table <a id="data-table"></a>

| Sr. No. | \*Penalty based on \(Bill amount/Balance pending\) | \*Grace period \(days\) | Penalty flat amount \(Rs\) | Penalty \(%\) |
| :--- | :--- | :--- | :--- | :--- |
| 1 | Balance Pending | 15 | 40 | 10 |

The data given in the table is sample data for reference.

## Procedure <a id="procedure"></a>

### Data Definition <a id="data-definition"></a>

| Sr. No. | Column Name | Data Type | Data Size | Mandatory | Description |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | Grace period | Integer | 2 | Yes | After the bill is generated, certain days are provided to the citizen for making the payment |
| 2 | Penalty flat amount | Decimal | \(3,2\) | Yes | If the penalty is not levied on a percentage basis, it is generally a flat fee which is penalty charges amount |
| 3 | Penalty based on | Text | 64 | Yes | The penalty can be a certain percentage of the bill amount or balance pending if partial payments are made against the bill |
| 4 | Penalty \(%\) | Decimal | \(3,2\) | Yes | The penalty is calculated as a percentage amount based on either Bill amount or Balance pending |

### Steps to fill data <a id="steps-to-fill-data"></a>

1. Download the data template attached to this page.
2. Refer to the ‘Data Definition’ section of this document to learn more about the template sheet, data type, size, and definitions.
3. Please reach out to the person who has shared this template with you to discuss and clear your doubts.
4. Enter the applicable value for the Grace Period.
5. Enter the corresponding Penalty Flat Amount.
6. Select the relevant parameter for Penalty Based On to specify if the calculation of the penalty is based on the bill amount or the pending balance.
7. Enter the applicable percentage value for calculating the Penalty amount.
8. Verify the data once again by going through the checklist and making sure that each and every point mentioned in the checklist is covered.

## Checklist <a id="checklist"></a>

The checklist contains a set of activities to be performed once the data is filled into a template to ensure data entry requirements are met. These activities have been divided into 2 groups as given below.

### Common Checklist <a id="common-checklist"></a>

This checklist covers all the activities which are common across the entities.

| Sr. No. | Checklist Parameter | Example |
| :--- | :--- | :--- |
| 1 | Make sure that each and every point in this reference list has been taken care of | ​[Checklist](https://digit-discuss.atlassian.net/wiki/spaces/DO/pages/502203140/Checklist)​ |

### Entity Specific Checklist <a id="entity-specific-checklist"></a>

Separate Entity Specific Checklist is not required for this module data.

## Attachments <a id="attachments"></a>

[Configuration Data Templateconfiguration-data-template-penalty-rates \(1\).xlsx - 10KB](https://firebasestorage.googleapis.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-MERG_iQW5oN4ukgXP8K%2Fsync%2F6736a6d4f73473589648d1cac7799a75b414ef84.xlsx?generation=1602050610927197&alt=media)

[Sample Datasample-configuration-data-penalty-rates \(1\).xlsx - 9KB](https://firebasestorage.googleapis.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-MERG_iQW5oN4ukgXP8K%2Fsync%2F4f4334b9ecc2770e7469692f2e0b785d430c51be.xlsx?generation=1602050610993712&alt=media)

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation ](https://egov.org.in/)is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).

