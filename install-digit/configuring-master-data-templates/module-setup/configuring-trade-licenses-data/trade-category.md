# Trade Category

### Introduction

The Trade Category List can be defined as the primary or the 1st level classification “head” for trade\(s\) defined at a ULB/State Level.

### Data Table

| Sr.No. | Trade Category Code\* | Trade Category Name\* \(In English\) | Trade Category Name\* \(In Local Language\) |
| :--- | :--- | :--- | :--- |
| 1 | TC1 | Goods | सामग्री |
| 2 | TC2 | Services | सर्विस |

{% hint style="info" %}
The table above contains sample Trade Category data.
{% endhint %}

### Procedure

#### Data Definition

| Sr. No. | Column Name | Data Type | Data Size | Is Mandatory? | Description |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | Trade Category Code | Alphameric |  64 | Yes | The Code assigned to the Trade Category. Eg: TC1 For Goods, TC2 for Services |
| 2 | Trade Category Name \(In English\) | Text | 256  | Yes | Name of the Trade Category in English. Eg: Goods, Services etc. |
| 3 | Trade Category Name \(In Local Language\) | Text | 256  | Yes | Name of the Trade Category in Local Language \(as decided\). Eg: Service is described as “सर्विस” in Hindi |

#### Steps to fill data

1. Download the data template attached to this page.
2. Refer to the ‘Data Definition’ section of this document to learn more about the template sheet, data type, size, and definitions.
3. Enter a unique Trade Category Code for each trade head.
4. Enter the Trade Category Name. Some trade categories are already defined in the master. Add new categories as required.
5. Enter the Trade Category Name \(Local Language\).

### Checklist

The checklist contains a set of activities to be performed once the data is filled into a template to ensure data entry requirements are met. These activities have been divided into 2 groups as given below.

#### Common Checklist

This checklist covers all the activities which are common across the entities.

| Sr. No. | Checklist Parameter | Example |
| :--- | :--- | :--- |
| 1 | Make sure that each and every point in this reference list has been taken care of | [Checklist](../untitled-1/checklist.md) |

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
      <td style="text-align:left">The format of the Trade Category Code defined should be alphanumeric and
        unique</td>
      <td style="text-align:left">
        <p>TC1: Goods</p>
        <p>TC2: Services</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">2</td>
      <td style="text-align:left">Trade Category Name (In either Language) should not contain any special
        characters</td>
      <td style="text-align:left">
        <p>Goods: [Allowed]</p>
        <p>#Goods! : [Not allowed]</p>
      </td>
    </tr>
  </tbody>
</table>

### Attachments

{% file src="../../../../.gitbook/assets/configuration-data-template-trade-master-2-.xlsx" caption="Configuration Data Template" %}

{% file src="../../../../.gitbook/assets/sample-configuration-data-template-trade-master-filled-2-.xlsx" caption="Sample Data Template" %}

