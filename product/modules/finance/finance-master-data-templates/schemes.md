# Schemes

## Introduction <a id="introduction"></a>

The Center or State comes up with various government programs called schemes \(Yojana\) from time to time. These schemes could be either Central, state-specific or joint collaboration between the Centre and the states.

Schemes and sub-schemes defined by the Centre or state government to be associate with a fund and for a time. Similar Sub schemes can be defined under a scheme.

## Data Table <a id="data-table"></a>

| Sr. No\* | Scheme Code\* | Scheme Name\* | Fund\* | Description | Start Date\* | End Date\* |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | 10 | AMRUT | Grant Fund | Amrut | 01/05/2018 | 01/06/2021 |
| 2 | 20 | Swachh Bharat Mission | Grant Fund | Swachh Bharat Mission | 01/06/2017 | 01/07/2020 |
| 3 | 30 | Finance Commission | Municipal Fund | Finance Commission | 01/03/2016 | 30/04/2019 |
| 4 | 40 | Housing for All | Municipal Fund | Municipal Fund | 01/04/2016 | 31/03/2021 |

The data given in the table is sample data.

## Procedure <a id="procedure"></a>

### Data Definition <a id="data-definition"></a>

| Sr. No. | Column Name | Data Type | Data Size | Is Mandatory? | Definition/ Description |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | Scheme Code | Numeric | 50 | Yes | A unique code assigned to individual Scheme |
| 2 | Scheme Name | Text | 250 | Yes | The indicate Name of the Scheme, this will facilitate the user to record the transaction against the individual scheme and also helps in tracking the utilization of the Scheme |
| 3 | Fund | Text | 250 | Yes | To indicate the Fund name against each scheme. This will facilitate in support to track the scheme funds, receipts and utilization by attaching scheme code to the financial transaction. Click on [Funds](funds.md) to view the Fund master data |
| 4 | Description | Text | 250 | No | A Short description provided to individual schemes |
| 5 | Start Date | Date | N/A | Yes | The Date on which the Scheme Started, will help to facilitate the receiving of funds from Central Sponsored Schemes and State-Sponsored Schemes |
| 6 | End Date | Date | N/A | Yes | The Date on which the Scheme will End, will help to facilitate the end date by when the funds from Central Sponsored Schemes and State-Sponsored Schemes need to be utilized |

### Steps to fill data <a id="steps-to-fill-data"></a>

1. Download the data template attached to this page.
2. Have it open and go through all the headers and understand the meaning of them by referring 'Data Definition' section.
3. Make sure all the headers, its data type, field size and its definition/ description is understood properly. In case of any doubt, please reach out to the person who has shared this document with you to discuss the same and clear out the doubts.
4. Identify all different types of Schemes on the basis of ULB’s functions.
5. Start filling the data starting from serial no. and complete a record at once. repeat this exercise until the entire data is filled into a template.
6. Verify the data once again by going through the checklist and taking care of each and every point mentioned in the checklist.

## Checklist <a id="checklist"></a>

The checklist is a set of activities to be performed once the data is filled into a template to ensure data type, size, and format of data is as per the expectation. These activities have been divided into 2 groups as given below.

### Common Checklist <a id="common-checklist"></a>

This checklist covers all the activities which are common across the entities.

| Sr. No | Checklist Parameter | Example |
| :--- | :--- | :--- |
| 1 | Make sure that each and every point in this reference list has been taken care of | ​[Checklist](https://digit-discuss.atlassian.net/wiki/spaces/DO/pages/502203140/Checklist)​ |

### Entity Specific Checklist <a id="entity-specific-checklist"></a>

This checklist covers the activities which are specific to the entity.

<table>
  <thead>
    <tr>
      <th style="text-align:left">Sr. No.</th>
      <th style="text-align:left">Activity</th>
      <th style="text-align:left">Example</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">1</td>
      <td style="text-align:left">The date format should be as per example and the Start date should be
        greater than the current date and end date</td>
      <td style="text-align:left">
        <p>DD/MM/YYYY : [Allowed]</p>
        <p>YYYY/DD/MM : [Not allowed]</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">2</td>
      <td style="text-align:left">The name should be unique and should not contain any special characters</td>
      <td
      style="text-align:left">
        <p>AMRUT : [Allowed]</p>
        <p>#AMRUT! : [Not allowed]</p>
        </td>
    </tr>
  </tbody>
</table>

## Attachments <a id="attachments"></a>

[Configuration Data Templateconfiguration-data-template-schemes.xlsx - 9KB](https://firebasestorage.googleapis.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-MERG_iQW5oN4ukgXP8K%2Fsync%2F5ddde45b102c9f9460d3d5f405ece12f6606c7a3.xlsx?generation=1602050611767046&alt=media)

[Sample Datasample-confugration-data-schemes.xlsx - 9KB](https://firebasestorage.googleapis.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-MERG_iQW5oN4ukgXP8K%2Fsync%2F1becdcae012164a5fcbf77e0113474c07fb6709b.xlsx?generation=1602050611572188&alt=media)

<<<<<<< HEAD
[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation ](https://egov.org.in/)is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).
=======


 [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation ](https://egov.org.in/)is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).
>>>>>>> 64dca8adbdf64336b1a8203199b3791fa23434fa

