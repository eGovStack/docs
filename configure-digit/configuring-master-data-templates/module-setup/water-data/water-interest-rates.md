# Water Interest Rates

## Introduction

Interest is levied from the consumer in case the consumer fails to make the payment of the bill before the specified due date. The consumer has to make the full payment before the due date to avoid interest charges. The number of days after which the interest is applicable is configurable at the ULB level. Interest Rates are calculated essentially on a daily percentage basis.

The interest rate on a daily basis can be levied on -

1. Entire bill amount
2. Balance pending when partial payments have been made

## Data Table

| Sr. No. | \*Interest based on \(Bill amount/Balance pending\) | \*Grace Period \(days\) | \*Interest rate \(%\) |
| :--- | :--- | :--- | :--- |
| 1 | Bill Amount | 15 | 5 |

{% hint style="info" %}
Data given in the table is sample data for reference.
{% endhint %}

## Procedure

### Data Definition

| Sr. No. | Column Name | Data Type | Data Size | Mandatory | Description |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | Grace period | Integer | 2 | Yes | After the bill is generated, certain days are provided to the citizen for making the payment |
| 2 | Interest-based on | Text | 64 | Yes | Interest can be levied on either bill amount or balance pending if partial payments are made against the bill. |
| 3 | Interest rate | Decimal | \(3,2\) | Yes | Time-based Interest percentage |

### Steps to fill data

1. Download the data template attached to this page.
2. Refer to the ‘Data Definition’ section of this document to learn more about the template sheet, data type, size, and definitions.
3. Please reach out to the person who has shared this template with you to discuss and clear your doubts.
4. Enter the Grace Period.
5. Select the relevant Interest-based On parameter.
6. Enter the Interest Rate.
7. Verify the data once again by going through the checklist and making sure that each and every point mentioned in the checklist is covered.

## Checklist

The checklist contains a set of activities to be performed once the data is filled into a template to ensure data entry requirements are met. These activities have been divided into 2 groups as given below.

### Common Checklist

This checklist covers all the activities which are common across the entities.

| Sr. No. | Checklist Parameter | Example |
| :--- | :--- | :--- |
| 1 | Make sure that each and every point in this reference list has been taken care of | [Checklist](https://digit-discuss.atlassian.net/wiki/spaces/DO/pages/502203140/Checklist) |

### Entity Specific Checklist

Separate Entity Specific Checklist is not required for this module data.

## Attachments

{% file src="../../../../.gitbook/assets/configuration-data-template-interest-rate.xlsx" caption="Configuration Data Template " %}

{% file src="../../../../.gitbook/assets/sample-configuration-data-interest-rate.xlsx" caption="Sample Data" %}

