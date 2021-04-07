# Sub Schemes

### Introduction

Sub schemes are defined under the schemes by the Centre or state government to be associate with a fund and for a time. The Sub scheme shall be defined under a scheme.

### Data Table

| Sr. No. | Scheme Code\* | Sub Scheme Name \* | Sub Scheme Code \* | Valid From \* | Valid To \* | Department Code | Initial Estimate Amount |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | 10 | Storm Water Drains | 1003 | 01/05/2018 | 01/06/2021 | PHS | 2500000 |
| 2 | 20 | Solid Waste Management- SWM | SBM02 | 01/06/2017 | 01/07/2020 | TP | 1000000 |
| 3 | 30 | Street Lights | 5001 | 01/03/2016 | 30/04/2019 | TP | 2000000 |

{% hint style="info" %}
Data given in the table is a sample data.
{% endhint %}

### Procedure

#### Data Definition

| Sr No | Column Name | Data Type | Data Size | Is Mandatory? | Definition/ Description |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | Scheme Code | Alphanumeric | 50 | Yes | A unique code assigned to individual Scheme, this will facilitate the user to assign the sub-scheme under the individual scheme and also helps in tracking the utilization of the Scheme. Click on [Schemes ](schemes.md)to view the scheme master data |
| 2 | Sub Scheme Name | Text | 50 | Yes | The Sub Scheme Name will facilitate the user to record the transaction against the individual sub-scheme and also helps in tracking the utilization of the sub-scheme |
| 3 | Sub Scheme Code | Alphanumeric | 50 | Yes | A unique code assigned to individual Sub Scheme |
| 4 | Valid From | Date | N/A | Yes | The Date on which the Scheme Started, this will help to facilitate the receiving of funds from Central Sponsored Schemes and State-Sponsored Schemes |
| 5 | Valid To | Date | N/A | Yes | The Date on which the Scheme will End, this will help to facilitate the end date by when the funds from Central Sponsored Schemes and State-Sponsored Schemes need to be utilized |
| 6 | Department Code | Text | 250 | No | The sub-scheme can be linked to the individual department, so user while recording the transaction can assign the department. Click [ULB's Departments ](../../environment-setup/state-level-setup/ulb-departments.md)for the master data |
| 7 | Initial Estimate Amount | Numeric | 50 | No | The initial Estimate Amount approved amount under the sub-scheme can be updated while creating the sub-scheme master record. This will facilitate the user in utilizing the amount within the estimated amount |

#### Steps to fill data

1. Download the workflow template attached to this page.
2. Have it open and go through all the headers and understand the meaning of them by referring 'Data Definition' section.
3. Make sure all the headers, its data type, field size and its definition/ description is understood properly. In case of any doubt, please reach out to the person who has shared this document with you to discuss the same and clear out the doubts.
4. Identify all sub schemes with the State.
5. Start filling the data starting from serial no. and complete a record at once. repeat this exercise until the entire data is filled into a template.
6. Verify the data once again by going through the checklist and taking care of each and every point mentioned in the checklist.

### Checklist

The checklist is a set of activities to be performed once the data is filled into a template to ensure data type, size, and format of data is as per the expectation. These activities have been divided into 2 groups as given below.

#### Common Checklist

This checklist covers all the activities which are common across the entities.

| Sr. No | Checklist Parameter | Example |
| :--- | :--- | :--- |
| 1 | Make sure that each and every point in this reference list has been taken care of | [Checklist](../untitled-1/checklist.md) |

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
        greater than the current date and end date.</td>
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
    <tr>
      <td style="text-align:left">3</td>
      <td style="text-align:left">The scheme name mapped should be as per the scheme master entity</td>
      <td
      style="text-align:left">AMRUT, SWM</td>
    </tr>
  </tbody>
</table>

### Attachments

{% file src="../../../../.gitbook/assets/configuration-data-template-sub-schemes.xlsx" caption="Configuration Data Template" %}

{% file src="../../../../.gitbook/assets/sample-confugration-data-sub-schemes.xlsx" caption="Sample Data" %}



