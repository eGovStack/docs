# Areas Served Master

## Introduction

In all most all the states fire stations serve both the urban as well as the rural areas, therefore we need to prepare the masters for both urban areas as well as the rural areas being served in the state.

## Data Table

### Urban Area Master

| Sr. No. | \*District Code | \*District Name | \*ULB Code | \*ULB Name |
| :--- | :--- | :--- | :--- | :--- |
| 1 | DC01 | Amritsar | ULB01 | Amritsar |
| 2 | DC01 | Amritsar | ULB02 | Ajnala |

### Rural Area Master

| Sr. No. | \*District Code | \*District Name | \*Sub District Code | **\***Sub District Name |
| :--- | :--- | :--- | :--- | :--- |
| 1 | DC02 | Patiala | SDC01 | Jhabal |
| 2 | DC02 | Patiala | SDC02 | Patran |

{% hint style="info" %}
Data given in the above table is a sample data.
{% endhint %}

## Procedure

### Data Definitions

**Urban Area**

| Sr. No. | Column Name | Data Type | Data Size | Mandatory | Description |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | District Code | Alphameric | 64 | Yes | The code is given to the district by the state team. Eg: DC01 for Amritsar, DC02 Patiala. |
| 2 | District Name | Text | 256 | Yes | Name of the district Eg: Amritsar, Patiala |
| 3 | ULB Code | Text | 256 | Yes | The code is given to the district by the state team. Eg: ULB01 for Amritsar, ULB02 Ajnala |
| 4 | ULB Name | Alphameric | 64 | Yes | Name of the ULB Eg: Amritsar, Ajnala |

**Rural Area**

| Sr. No. | Column Name | Data Type | Data Size | Mandatory | Description |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | District Code | Alphameric | 64 | Yes | The code is given to the district by the state team. Eg: DC01 for Amritsar, DC02 Patiala |
| 2 | District Name | Text | 256 | Yes | Name of the district Eg: Amritsar, Patiala |
| 3 | Sub-district Code | Text | 256 | Yes | The code is given to the subdistrict by the state team. Eg: SDC01 for Jhabal, SDC02 Patran |
| 4 | Sub-district Name | Alphameric | 64 | Yes | Name of the sub-district Eg: Jhabal, Patran |

### How to fill data

**Urban Areas**

1. Download the data template attached to this page.
2. Get a good understanding of all the headers in the template sheet, their data type, size, and definitions by referring to the ‘Data Definition’ section of this document.
3. In case of any doubt, please reach out to the person who has shared this template with you to discuss and clear your doubts.
4. Identify the districts where fire services are provided and enter their names in the District Name column.
5. Give each district a unique code and enter the code in the District Code column, next to the District Name.
6. Identify all the ULBs within each district where fire services are provided and enter their name in the ULB Name column next to it's District Name.
7. Give each ULB a unique code and enter the code in the ULB Code column.
8. Verify the data once again by going through the checklist and making sure that each and every point mentioned in the checklist is covered.

**Rural Areas**

1. Download the data template attached to this page.
2. Get a good understanding of all the headers in the template sheet, their data type, size, and definitions by referring to the ‘Data Definition’ section of this document.
3. In case of any doubt, please reach out to the person who has shared this template with you to discuss and clear your doubts.
4. Identify the districts where fire services are provided and enter their names in the District Name column.
5. Give each district a unique code and enter the code in the District Code column, next to the District Name.
6. Identify all the Sub District within each district where fire services are provided and enter their name in the Sub District Name column next to it's District Name.
7. Give each Sub District a unique code and enter the code in the Sub District Code column.
8. Verify the data once again by going through the checklist and making sure that each and every point mentioned in the checklist is covered.

## Checklist

The checklist is a set of activities to be performed one the data is filled into a template to ensure data type, size, and format of data is as per the expectation. These activities have been divided into 2 groups as given below.

### Common Checklist

This checklist covers all the activities which are common across the entities.

| Sr. No. | Checklist Parameter | Example |
| :--- | :--- | :--- |
| 1 | Make sure that each and every point in this reference list has been taken care of. | [Checklist](https://digit-discuss.atlassian.net/wiki/spaces/DO/pages/502203140/Checklist) |

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
      <td style="text-align:left">District Codes, Sub District Codes, and ULB Codes should be alphanumeric
        and Unique.</td>
      <td style="text-align:left">
        <p>ULB01: Amritsar</p>
        <p>SDC01: Jhabal</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">2</td>
      <td style="text-align:left">District Name, Sub District Name, and ULB Name should not contain any
        special characters.</td>
      <td style="text-align:left">
        <p>Amritsar : [Allowed]</p>
        <p>#Amritsar! : [Not allowed]</p>
      </td>
    </tr>
  </tbody>
</table>

## Attachments

{% file src="../../../../.gitbook/assets/configuration-data-area-master.xlsx" caption="Configuration Date Template" %}

{% file src="../../../../.gitbook/assets/sample-data-template-area-master.xlsx" caption="Sample Data" %}

