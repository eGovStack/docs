# Sewerage Interest Rates

## Introduction <a href="#introduction" id="introduction"></a>

Interest is levied on the consumer if the consumer fails to make the bill payment before a specified due date. The consumer has to make the full payment before the due date to avoid interest charges. The number of days after which the interest is applicable is configurable at the ULB level. The interest amount is charged to the consumer on a daily basis once the specified grace period is over and till the bill payment is done.

Interest rate: The interest rate on a daily basis can be levied on -

1. Entire bill amount
2. Balance pending when partial payments have been made

## Data Table <a href="#data-table" id="data-table"></a>

| Sr. No. | \*Interest based on (Bill amount/Balance pending) | \*Grace Period (days) | \*Interest rate |
| ------- | ------------------------------------------------- | --------------------- | --------------- |
| 1       | Balance Pending                                   | 15                    | 5               |

Data given in the table is sample data for reference.

## Procedure <a href="#procedure" id="procedure"></a>

### Data Definition <a href="#data-definition" id="data-definition"></a>

| Sr. No. | Column Name       | Data Type | Data Size | Mandatory | Description                                                                                                   |
| ------- | ----------------- | --------- | --------- | --------- | ------------------------------------------------------------------------------------------------------------- |
| 1       | Grace period      | Integer   | 2         | Yes       | After the bill is generated, certain days are provided to the citizen for making the payment                  |
| 2       | Interest-based on | Text      | 64        | Yes       | Interest can be levied on either bill amount or balance pending if partial payments are made against the bill |
| 3       | Interest rate     | Decimal   | (3,2)     | Yes       | Time-based Interest percentage                                                                                |

### Steps to fill data <a href="#steps-to-fill-data" id="steps-to-fill-data"></a>

1. Download the data template attached to this page.
2. Refer to the ‘Data Definition’ section of this document to learn more about the template sheet, data type, size, and definitions.
3. Please reach out to the person who has shared this template with you to discuss and clear your doubts.
4. Enter the applicable Grace Period for calculating interest.
5. Select the relevant parameter for Interest-Based On to specify if the interest is applied to the bill amount or pending balance.
6. Enter the applicable percentage value for Interest Rate that will be used to calculate the interest amount.
7. Verify the data once again by going through the checklist and making sure that each and every point mentioned in the checklist is covered.

## Checklist <a href="#checklist" id="checklist"></a>

The checklist contains a set of activities to be performed once the data is filled into a template to ensure data entry requirements are met. These activities have been divided into 2 groups as given below.

### Common Checklist <a href="#common-checklist" id="common-checklist"></a>

This checklist covers all the activities which are common across the entities.

| Sr. No. | Checklist Parameter                                                               | Example                                                                                     |
| ------- | --------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------- |
| 1       | Make sure that each and every point in this reference list has been taken care of | ​[Checklist](https://digit-discuss.atlassian.net/wiki/spaces/DO/pages/502203140/Checklist)​ |

### Entity Specific Checklist <a href="#entity-specific-checklist" id="entity-specific-checklist"></a>

Separate Entity Specific Checklist is not required for this module data.

## Attachments <a href="#attachments" id="attachments"></a>

{% file src="../../../../.gitbook/assets/Configuration data template - Interest rate (1).xlsx" %}

{% file src="../../../../.gitbook/assets/Sample configuration data - Interest rate (1).xlsx" %}

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation ](https://egov.org.in/)is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).
