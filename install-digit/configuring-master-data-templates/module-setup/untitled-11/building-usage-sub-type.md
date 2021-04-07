# Building Sub Usage Type

### Introduction

After the building usage types are identified, the next activity is to identify the building sub usage types.

Buildings types can be further classified into various subcategories to go into the granular level of their usage details. The National Building Code of India \(NBC\) also classifies the building's usage type into the sub usage types which can be seen in the attachment.

### Data Table 

| Sr. No. | \*Building Usage Type Code | \*Sub Type Code | \*Building Sub Usage Type | \*Sub Divison \(as per NBC\) | \*Building Sub Usage Type \(as per NBC\) |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 |  BU01 | BSU01 | Hotel | A4 | Hotel |
| 2 |  BU01 | BSU02 | Apartment | A5 | Apartment House |

{% hint style="info" %}
Data given in the above table is a sample data.
{% endhint %}

### Procedure

#### Data Definitions

| Sr. No. | Column Name | Data Type | Data Size | Mandatory | Description |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | Building Usage Type Code | Reference |  64 | Yes | The codes are given to the building usage type in the[ building usage type master](building-usage-type.md) |
| 2 | Sub Type Code | Alphameric |  64 | Yes | The code is given to the building sub usage type by the Fire Station. Eg: BSU01 for Hotel, BSU02 for Apartment Houses |
| 3 | Building Sub Usage Type | Text | 256  | Yes | Name of subcategories within each building usage type as per the fire station. Eg: Hotel, Apartment Houses |
| 4 | Sub Divison \(as per NBC\) | Alphameric | 64  | Yes | The code is given to the building sub usage type as per NBC. Eg: Subdivision A4, A5 |
| 5 | Building Sub Usage Type \(as per NBC\) | Text | 256 | Yes | Name of subcategories within each building usage type as per NBC. Eg: Hotel, Apartment House |

#### How to fill data

1. Download the data template attached to this page.
2. Get a good understanding of all the headers in the template sheet, their data type, size, and definitions by referring to the ‘Data Definition’ section of this document.
3. In case of any doubt, please reach out to the person who has shared this template with you to discuss and clear your doubts.
4. Identify and add all the different sub usage types for each building group that are being catered by the fire station in the Building Sub Usage Type column.
5. Next, give each building Sub Usage type a unique code and enter the code in the Sub Usage Type Code column, next to the Building Sub Usage type.
6. Map the data filled in the building sub usage type column to the building sub usage type and Subdivision as per the national building code.
7. Record the appropriate subdivision and building sub usage type from NBC in the Subdivision \(as per NBC\) and Building Sub Usage Type \(as per NBC\) respectively.
8. Verify the data once again by going through the checklist and making sure that each and every point mentioned in the checklist is covered.

### Checklist

The checklist is a set of activities to be performed one the data is filled into a template to ensure data type, size, and format of data is as per the expectation. These activities have been divided into 2 groups as given below.

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
      <td style="text-align:left">The Building Usage Type Code should be similar to the ones defined in
        the<a href="building-usage-type.md"> building usage type maste</a>r</td>
      <td
      style="text-align:left">
        <p>BU01: Residential</p>
        <p>BU02: Educational</p>
        </td>
    </tr>
    <tr>
      <td style="text-align:left">2</td>
      <td style="text-align:left">Building Sub Usage Type Codes that are defined by the Fire Station should
        be alphanumeric and unique</td>
      <td style="text-align:left">
        <p>BSU01: Hotel</p>
        <p>BSU02: Apartment</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">3</td>
      <td style="text-align:left">Building Sub Usage Type should not contain any special characters</td>
      <td
      style="text-align:left">
        <p>Hotel : [Allowed]</p>
        <p>#Hotel! : [Not allowed]</p>
        </td>
    </tr>
  </tbody>
</table>

### Attachments

{% file src="../../../../.gitbook/assets/configuration-data-template-building-sub-usage-type.xlsx" caption="Configuration Data Template" %}

{% file src="../../../../.gitbook/assets/sample-configuration-data-building-sub-usage-type.xlsx" caption="Sample Data" %}

{% file src="../../../../.gitbook/assets/nbc-building-sub-usage-type.xlsx" caption="NBC Classification" %}



