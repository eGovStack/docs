# Trade Category

## Introduction <a id="introduction"></a>

The Trade Category List can be defined as the primary or the 1st level classification “head” for trade\(s\) defined at a ULB/State Level.

## Data Table <a id="data-table"></a>

| Sr.No. | Trade Category Code\* | Trade Category Name\* \(In English\) | Trade Category Name\* \(In Local Language\) |
| :--- | :--- | :--- | :--- |
| 1 | TC1 | Goods | सामग्री |
| 2 | TC2 | Services | सर्विस |

The table above contains sample Trade Category data.

## Procedure <a id="procedure"></a>

### Data Definition <a id="data-definition"></a>

| Sr. No. | Column Name | Data Type | Data Size | Is Mandatory? | Description |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | Trade Category Code | Alphameric | 64 | Yes | The Code assigned to the Trade Category. Eg: TC1 For Goods, TC2 for Services |
| 2 | Trade Category Name \(In English\) | Text | 256 | Yes | Name of the Trade Category in English. Eg: Goods, Services etc. |
| 3 | Trade Category Name \(In Local Language\) | Text | 256 | Yes | Name of the Trade Category in Local Language \(as decided\). Eg: Service is described as “सर्विस” in Hindi |

### Steps to fill data <a id="steps-to-fill-data"></a>

1. Download the data template attached to this page.
2. Refer to the ‘Data Definition’ section of this document to learn more about the template sheet, data type, size, and definitions.
3. Enter a unique Trade Category Code for each trade head.
4. Enter the Trade Category Name. Some trade categories are already defined in the master. Add new categories as required.
5. Enter the Trade Category Name \(Local Language\).

## Checklist <a id="checklist"></a>

The checklist contains a set of activities to be performed once the data is filled into a template to ensure data entry requirements are met. These activities have been divided into 2 groups as given below.

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

## Attachments <a id="attachments"></a>

[Configuration Data Templateconfiguration-data-template-trade-master-2-.xlsx - 17KB](https://firebasestorage.googleapis.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-MERG_iQW5oN4ukgXP8K%2Fsync%2Fe9770eb56cc2e51a013d1df84d2db6092d01f17b.xlsx?generation=1602050605603605&alt=media)

[Sample Data Templatesample-configuration-data-template-trade-master-filled-2-.xlsx - 19KB](https://firebasestorage.googleapis.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-MERG_iQW5oN4ukgXP8K%2Fsync%2F790e93a747bfd659fd37fcc836eec0aab074bf79.xlsx?generation=1602050605673696&alt=media)

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation ](https://egov.org.in/)is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).

