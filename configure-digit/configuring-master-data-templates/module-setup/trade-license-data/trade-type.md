# Trade Type

### Introduction

Once the [Trade Categories](trade-category.md) are defined, the next task is to -

* Define Trade Types
*  Map Trade Category to listed Trade Types

The Trade Type can be defined as the next \(2nd\) level classification of Trade. There can be multiple trade types and the list may vary from one State/ULB to another.

### Data Table

| Sr. No. | Trade Type Code\* | Trade Type Name\* \(In English\) | Trade Type Name\* \(In Local Language\) | Trade Category Code\* |
| :--- | :--- | :--- | :--- | :--- |
| 1 | TRADE\_TYPE\_MEDICAL | Hospital | अस्पताल | TC1 |
| 2 | TRADE\_TYPE\_HOTEL | Hotels | होटल | TC2 |

{% hint style="info" %}
The table above contains sample Trade Type data.
{% endhint %}

### Procedure

#### Data Definition

| Sr. No. | Column Name | Data Type | Data Size | Is Mandatory? | Description |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | Trade Type Code | Alphanumeric | 64 | Yes | The Code assigned to the Trade Type. Eg: TRADE\_TYPE\_MEDICAL is assigned to Hospitals |
| 3 | Trade Type Name \(In English\) | Text | 256  | Yes | Name of the Trade Type in English. Eg: Goods, Services etc. |
| 3 | Trade Type Name \(In Local Language\) | Text | 256  | Yes | Name of the Trade Type in Local Language \(as decided\). Eg: Service is described as “सर्विस” in Hindi |
| 4 | Trade Category Code | Reference |  64 | Yes | The Code assigned to the[ Trade Category](trade-category.md). Eg: TC1 For Goods, TC2 for Services |

#### Steps to fill data

1. Download the data template attached to this page.
2. Refer to the ‘Data Definition’ section of this document to learn more about the template sheet, data type, size, and definitions.
3. Select the relevant Trade Category Code from the available drop-down list of Trade Category. This will map the listed Trade Type to the corresponding Trade Category.
4. Enter a unique Trade Type Code to identify the type of trade.
5. Enter a Trade Type Name \(In English\).
6. Enter the Trade Type Name \(In Local Language\).

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
      <td style="text-align:left">The format of the Trade Type Code defined should be alphanumeric and unique</td>
      <td
      style="text-align:left">
        <p>TRADE_TYPE_MEDICAL</p>
        <p>TRADE_TYPE_HOTELS</p>
        </td>
    </tr>
    <tr>
      <td style="text-align:left">2</td>
      <td style="text-align:left">Trade Type Name (in either language) should not contain any special characters</td>
      <td
      style="text-align:left">
        <p>Hospital: [Allowed]</p>
        <p>#Hospital! : [Not allowed]</p>
        </td>
    </tr>
  </tbody>
</table>

### Attachments

{% file src="../../../../.gitbook/assets/configuration-data-template-trade-master-3-.xlsx" caption="Configuration Data Template" %}

{% file src="../../../../.gitbook/assets/sample-configuration-data-template-trade-master-filled-3- \(1\).xlsx" caption="Sample Data Template" %}



