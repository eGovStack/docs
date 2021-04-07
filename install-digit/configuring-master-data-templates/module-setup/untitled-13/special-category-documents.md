# Special Category Documents

## Introduction

In order to justify the Property[ Owner’s Special Category](owner-special-category.md) status, there are certain supporting documents that are required as the attachment of proof. These documents are crucial in terms of providing/ availing rebate on the property tax amount.

## Data Definition

| Sr. No. | Owner Type Code\* | Ownership Documents Description \(English\)\* | Ownership Documents Description \(Local Language\)\* |
| :--- | :--- | :--- | :--- |
| 1 | FREEDOMFIGHTER | Certificate issued by DC/ Competent Authority | डीसी / सक्षम प्राधिकारी द्वारा जारी प्रमाण पत्र |
| 2 | WIDOW | Death Certificate + Spouse proof | डेथ सर्टिफ़िकेट + जीवनसाथी प्रमाण |
| 3 | HANDICAPPED | Certificate of Handicap by a competent authority | सक्षम प्राधिकारी द्वारा विकलांग का प्रमाण पत्र |

{% hint style="info" %}
Data given in the table is a sample data.
{% endhint %}

## Procedure

| Sr. No. | Column Name | Data Type | Data Size | Mandatory | Description |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | Owner Type Code | Reference | 64 | Yes | Unique Identifier assigned for the [Owner Type](ownership-category.md). For example, Freedom Fighter is represented as FREEDOMFIGHTER |
| 2 | Ownership Documents Description \(English\) | Text | 256 | Yes | Nomenclature of “Owner Documents” in English. For ownership type Freedom Fighter, the document required is the certificate issued by DC/ Competent Authority |
| 3 | Ownership Documents Description \(Local Language\)\* | Text | 256 | Yes | Nomenclature of “Owner Documents” in Hindi |

### How to fill data

1. Download the data template attached to this page.
2. Get a good understanding of all the headers in the template sheet, their data type, size, and definitions by referring to the ‘Data Definition’ section of this document.
3. In case of any doubt, please reach out to the person who has shared this template with you to discuss and clear your doubts.
4. Identify the “Owner Categories” that exists at a ULB/ State level.
5. Add the “Owner Type Code” respectively. The predefined format of the Owner Type Code only must be used from the “[Owner Special Category](owner-special-category.md)” Master Sheet and not any random code. This will provide the base reference for the mapping of ownership type with the required documents.

## Checklist

The checklist is a set of activities to be performed one the data is filled into a template to ensure data type, size, and format of data is as per the expectation. These activities have been divided into 2 groups as given below.

### Common Checklist

This checklist covers all the activities which are common across the entities.

| Sr. No. | Checklist Parameter | Example |
| :--- | :--- | :--- |
| 1 | Make sure that each and every point in this reference list has been taken care of | [Checklist](../untitled-1/checklist.md) |

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
      <td style="text-align:left">The format of the Owner Type Code defined should be Text</td>
      <td style="text-align:left">War Widow is represented as WIDOW</td>
    </tr>
    <tr>
      <td style="text-align:left">2</td>
      <td style="text-align:left">Owner Type Code should not contain any special characters</td>
      <td style="text-align:left">
        <p>WIDOW: [Allowed]</p>
        <p>#WIDOW! : [Not allowed]</p>
      </td>
    </tr>
  </tbody>
</table>

## Attachments

{% file src="../../../../.gitbook/assets/configuration-data-template-pt-master-3- \(1\).xlsx" caption="Configuration Data Template" %}

{% file src="../../../../.gitbook/assets/configuration-sample-data-pt-master-3-.xlsx" caption="Sample Data" %}

