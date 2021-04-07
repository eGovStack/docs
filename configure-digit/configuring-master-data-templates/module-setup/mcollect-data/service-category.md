# Service Category

## Introduction

Service Category is a comprehensive list of services existing for the specific State/ULB. Service Category basically defines the miscellaneous revenue collection heads. Example - Rental, Entry Fees, User Charges etc.

Service categories are defined at a global level for different types of revenues. Payment collection and processing for certain services like property tax and trade licenses are done through the individual modules. The mCollect module processes payments for other miscellaneous services.

The Service Category masters list allows States/ULBs to identify the miscellaneous services for which payments and collections can be processed.

## Data Table

| Sr. No. | Service Category Code\* | Service Category \(In English\)\* | Service Category \(In Local Language\)\* |
| :--- | :--- | :--- | :--- |
| 1 | OFF00034 | Other Fee and Fines | अन्य शुल्क और जुर्माना |
| 2 | SAC00456 | Service and Administration Charges | सेवा और प्रशासन प्रभार |

{% hint style="info" %}
Data given in the table is a sample data.
{% endhint %}

## Procedure

### Data Definition

| Sr. No. | Column Name | Data Type | Data Size | Is Mandatory? | Definition/ Description |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | Service Category Code | Alphanumeric | 50 | Yes | Unique Identifier for “Service Category” and also a reference for the child mapping |
| 2 | Service Category \(English\) | Text | 250 | Yes | Name of “Service Category” in English. This will help the user select the category name to process the payment collection |
| 3 | Service Category \(Local Language\) | Text | 250 | Yes | Name of “Service Category” in Local Language. This will help the user select the category name to process the payment collection |

### Steps to Fill Data

1. Download the data template attached to this page.
2. Have it open and go through all the headers and understand the meaning of them by referring 'Data Definition' section.
3. Make sure all the headers, its data type, field size and its definition/ description is understood properly. In case of any doubt, please reach out to the person who has shared this document with you to discuss the same and clear out the doubts.
4. Identify all different types of service categories on the basis of ULB’s functions.
5. Start filling the data starting from serial no. and complete a record at once. repeat this exercise until the entire data is filled into a template.
6. Verify the data once again by going through the[ checklist ](../common-config/checklist.md)and taking care of each and every point mentioned in the checklist.

## Checklist

The checklist is a set of activities to be performed once the data is filled into a template to ensure data type, size, and format of data is as per the expectation. These activities have been divided into 2 groups as given below.

### Common Checklist

This checklist covers all the activities which are common across the entities.

| Sr. No | Checklist Parameter | Example |
| :--- | :--- | :--- |
| 1 | Make sure that each and every point in this reference list has been taken care of | [Checklist](../common-config/checklist.md) |

### Entity Specific Checklist

This checklist covers the activities which are specific to the entity.

<table>
  <thead>
    <tr>
      <th style="text-align:left">Sr. No.</th>
      <th style="text-align:left">Checklist Parameter</th>
      <th style="text-align:left">Example</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">1</td>
      <td style="text-align:left">The Service Category should not contain any special characters</td>
      <td
      style="text-align:left">
        <p>Other Fee and Fines : [Allowed]</p>
        <p>#Other Fee and Fines! : [Not allowed]</p>
        </td>
    </tr>
  </tbody>
</table>

## Attachments

{% file src="../../../../.gitbook/assets/configuration-data-template-service-category.xlsx" caption="Configuration Data Template" %}

{% file src="../../../../.gitbook/assets/sample-confugration-data-service-category.xlsx" caption="Sample Data" %}

