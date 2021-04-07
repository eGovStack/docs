# Schemes

### Introduction

The Center or State comes up with various government programs called schemes \(Yojana\) from time to time. These schemes could be either Central, state-specific or joint collaboration between the Centre and the states.

Schemes and sub-schemes defined by the Centre or state government to be associate with a fund and for a time. Similar Sub scheme shall be defined under a scheme.

### Data Table

| Sr. No\* | Scheme Code\* | Scheme Name\* | Fund\* | Description | Start Date\* | End Date\* |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | 10 | AMRUT | Grant Fund | Amrut | 01/05/2018 | 01/06/2021 |
| 2 | 20 | Swachh Bharat Mission | Grant Fund | Swachh Bharat Mission | 01/06/2017 | 01/07/2020 |
| 3 | 30 | Finance Commission | Municipal Fund | Finance Commission | 01/03/2016 | 30/04/2019 |
| 4 | 40 | Housing for All | Municipal Fund | Municipal Fund | 01/04/2016 | 31/03/2021 |

{% hint style="info" %}
Data given in the table is a sample data.
{% endhint %}

### Procedure

#### Data Definition

| Sr. No. | Column Name | Data Type | Data Size | Is Mandatory? | Definition/ Description |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | Scheme Code | Numeric | 50 | Yes | A unique code assigned to individual Scheme |
| 2 | Scheme Name | Text | 250 | Yes | The indicate Name of the Scheme, this will facilitate the user to record the transaction against the individual scheme and also helps in tracking the utilization of the Scheme |
| 3 | Fund | Text | 250 | Yes | To indicate the Fund name against each scheme. This will facilitate in support to track the scheme funds, receipts and utilization by attaching scheme code to the financial transaction. Click on[ Funds](funds.md) to view the Fund master data |
| 4 | Description | Text | 250 | No | A Short description provided to individual schemes |
| 5 | Start Date | Date | N/A | Yes | The Date on which the Scheme Started, this will help to facilitate the receiving of funds from Central Sponsored Schemes and State-Sponsored Schemes |
| 6 | End Date | Date | N/A | Yes | The Date on which the Scheme will End, this will help to facilitate the end date by when the funds from Central Sponsored Schemes and State-Sponsored Schemes need to be utilized |

#### Steps to fill data

1. Download the data template attached to this page.
2. Have it open and go through all the headers and understand the meaning of them by referring 'Data Definition' section.
3. Make sure all the headers, its data type, field size and its definition/ description is understood properly. In case of any doubt, please reach out to the person who has shared this document with you to discuss the same and clear out the doubts.
4. Identify all different types of Schemes on the basis of ULB’s functions.
5. Start filling the data starting from serial no. and complete a record at once. repeat this exercise until the entire data is filled into a template.
6. Verify the data once again by going through the checklist and taking care of each and every point mentioned in the checklist.

### Checklist

The checklist is a set of activities to be performed once the data is filled into a template to ensure data type, size, and format of data is as per the expectation. These activities have been divided into 2 groups as given below.

#### Common Checklist

This checklist covers all the activities which are common across the entities.

| Sr. No | Checklist Parameter | Example |
| :--- | :--- | :--- |
| 1 | Make sure that each and every point in this reference list has been taken care of | [Checklist](https://digit-discuss.atlassian.net/wiki/spaces/DO/pages/502203140/Checklist) |

#### Entity Specific Checklist

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

### Attachments

{% file src="../../../../.gitbook/assets/configuration-data-template-schemes.xlsx" caption="Configuration Data Template" %}

{% file src="../../../../.gitbook/assets/sample-confugration-data-schemes.xlsx" caption="Sample Data" %}



