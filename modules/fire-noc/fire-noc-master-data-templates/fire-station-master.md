# Fire Station Master

## Introduction <a id="introduction"></a>

The first step is to identify all the fire stations within the state. It is important to note that all the ULBs may not have a fire department. Generally, the bigger ULBs of the state have a fire department that caters to that ULB at the same time to all the surrounding smaller ULBs and rural areas as well.

## Data Table <a id="data-table"></a>

| Sr. No. | \*Fire Station Code | \*Fire Station Name |
| :--- | :--- | :--- |
| 1 | FS01 | Patiala |
| 2 | FS02 | Amritsar |

The data given in the above table is sample data.

## Procedure <a id="procedure"></a>

### Data Definitions <a id="data-definitions"></a>

| Sr. No. | Column Name | Data Type | Data Size | Mandatory | Description |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | Fire Station Code | Alphameric | 64 | Yes | The code is given to the fire station by the state team. Eg: FS01 For Patiala Fire station, FS02 for Amritsar Fire station |
| 2 | Fire Station Name | Text | 256 | Yes | Name of the fire station. Eg: Patiala, Amritsar |

### How to fill data <a id="how-to-fill-data"></a>

1. Download the data template attached to this page.
2. Get a good understanding of all the headers in the template sheet, their data type, size, and definitions by referring to the ‘Data Definition’ section of this document.
3. In case of any doubt, please reach out to the person who has shared this template with you to discuss and clear your doubts.
4. Identify all the fire stations operating in the state and enter their names in the Fire Station Name column
5. Next, give each fire station a unique code and enter that code in the Fire Station Code column.
6. Verify the data once again by going through the checklist and making sure that each and every point mentioned in the checklist is covered.

## Checklist <a id="checklist"></a>

The checklist is a set of activities to be performed once the data is filled into a template to ensure data type, size, and format of data is as per the expectation. These activities have been divided into 2 groups as given below.

### Common Checklist <a id="common-checklist"></a>

This checklist covers all the activities which are common across the entities.

| Sr. No. | Checklist Parameter | Example |
| :--- | :--- | :--- |
| 1 | Make sure that each and every point in this reference list has been taken care of | ​[Checklist](https://docs.digit.org/configure-digit/configuring-master-data-templates/module-setup/common-config/checklist)​ |

### Entity Specific Checklist <a id="entity-specific-checklist"></a>

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
      <td style="text-align:left">Fire Station Codes that are defined by the state team should be alphanumeric
        and Unique</td>
      <td style="text-align:left">
        <p>FS01: Amritsar</p>
        <p>FS02: Jalandhar</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">2</td>
      <td style="text-align:left">Fire station Name should not contain any special characters</td>
      <td style="text-align:left">
        <p>Amritsar : [Allowed]</p>
        <p>#Amritsar! : [Not allowed]</p>
      </td>
    </tr>
  </tbody>
</table>

## Attachments <a id="attachments"></a>

[Configuration Data Templatesample-configuration-data-fire-noc-master.xlsx - 9KB](https://firebasestorage.googleapis.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-MERG_iQW5oN4ukgXP8K%2Fsync%2F1bb2e72496f7d0ea96ff6079accd757ea2c11b0f.xlsx?generation=1602050605752534&alt=media)

[Sample Dataconfiguration-data-template-fire-noc-fee.xlsx - 13KB](https://firebasestorage.googleapis.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-MERG_iQW5oN4ukgXP8K%2Fsync%2F1816fc80bb5a933cc1c0867e367df35e2b607073.xlsx?generation=1602050605641823&alt=media)

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation ](https://egov.org.in/)is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).

