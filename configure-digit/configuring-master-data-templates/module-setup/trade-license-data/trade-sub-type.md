# Trade Sub Type

### Introduction

Trade Type can be further sub-classified into Trade Sub Type depending on the trade ontology existing in the ULBs or States. Hence, Hotels can be further classified into Dhabas in North India or Udupis in South India.

Once the [Trade Type\(s\)](trade-type.md) are defined, the next task is to -

* Define Trade Sub Types
* Map Trade Types to corresponding Trade Sub Types

### Data Table

| Sr. No. | Trade Sub Type Code\* | Trade Sub Type Name\* \(In English\) | Trade Sub Type Name\* \(In Local Language\) | Trade Type Code\* |
| :--- | :--- | :--- | :--- | :--- |
| 1 | TRADE\_SUBTYPE\_CLINIC | Clinic | क्लिनिक | TRADE\_TYPE\_MEDICAL |
| 2 | TRADE\_SUBTYPE\_DHABA | Dhaba | ढाबा | TRADE\_TYPE\_HOTEL |

{% hint style="info" %}
The table above contains sample data.
{% endhint %}

### Procedure

#### Data Definition

| Sr. No. | Column Name | Data Type | Data Size | Is Mandatory? | Description |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | Trade Sub Type Code | Alphanumeric | 64 | Yes | The Code assigned to the Trade Sub Type. Eg: TRADE\_TYPE\_Dhaba is assigned to Hotels |
| 2 | Trade Sub Type Name \(In English\) | Text | 256  | Yes | Name of the Trade Sub Type in English. Eg: Clinic |
| 3 | Trade Sub Type Name \(In Local Language\) | Text | 256  | Yes | Name of the Trade Sub Type in Local Language \(as decided\). Eg: Dhaba is described as “ढाबा” in Hindi |
| 4 | Trade Type Code | Reference | 64 | Yes | The Code assigned to the [Trade Type](trade-type.md). Eg: TRADE\_TYPE\_MEDICAL is assigned to Hospitals |

#### Steps to fill data

1. Download the data template attached to this page.
2. Refer to the ‘Data Definition’ section of this document to learn more about the template sheet, data type, size, and definitions.
3. Select the relevant Trade Type Code from the Trade Type master data. This will map the listed Trade Sub Type to the selected Trade Type.
4. Enter a unique value for Trade Sub Type Code.
5. Enter the English name for Trade Sub Type Name \(English\).
6. Enter the local name for the Trade Sub Type Name \(Local Language\).

### Checklist

The checklist contains a set of activities to be performed once the data is filled into a template to ensure data entry requirements are met. These activities have been divided into 2 groups as given below.

#### Common Checklist

This checklist covers all the activities which are common across the entities.

| Sr. No. | Checklist Parameter | Example |
| :--- | :--- | :--- |
| 1 | Make sure that each and every point in this reference list has been taken care of | [Checklist](../common-config/checklist.md) |

#### Entity Specific Checklist

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
      <td style="text-align:left">The format of the Trade Sub Type Code defined should be text and unique</td>
      <td
      style="text-align:left">TRADE_SUBTYPE_CLINIC</td>
    </tr>
    <tr>
      <td style="text-align:left">2</td>
      <td style="text-align:left">Trade Type Name (in either language) should not contain any special characters</td>
      <td
      style="text-align:left">
        <p>Clinic: [Allowed]</p>
        <p>#Clinic! : [Not allowed]</p>
        </td>
    </tr>
  </tbody>
</table>

### Attachments

{% file src="../../../../.gitbook/assets/configuration-data-template-trade-master-3- \(1\).xlsx" caption="Configuration Data Template" %}

{% file src="../../../../.gitbook/assets/sample-configuration-data-template-trade-master-filled-3-.xlsx" caption="Sample Data Template" %}

