# Funds

### Introduction

A Fund is used to capture activities/ group of activities for which separate books of accounts are required to be maintained. The concept of Funds brings accountability and better transparency

Various Funds are set up in ULB for meeting certain objectives. Income and expenditure under these funds are to be identified and disclosed separately.

Fund Accounting is a self-contained accounting with its own assets, liabilities, revenues, expenditures and fund balance.

### Data Table

| Sr. No\* | Name\* | Code\* | Identifier | Level\* | Parent Fund |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | Municipal Fund | 01 | 1 | 0 | Nil |
| 2 | Grant Fund | 02 | 2 | 0 | Nil |
| 3 | Public Fund | 03 | 3 | 0 | Nil |
| 4 | Pension Fund | 04 | 4 | 0 | Nil |

{% hint style="info" %}
Data given in the table is a sample data.
{% endhint %}

### Procedure

#### Data Definition

| Sr No | Column Name | Data Type | Data Size | Is Mandatory? | Definition/ Description |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | Name | Text | 50 | Yes | To indicate the Fund name, if there are multiple funds and by following the Fund Accounting method to record the transaction user can select a particular Fund |
| 2 | Code | Numeric | 50 | Yes | The unique code gives to the individual fund |
| 3 | Identifier | Numeric | 50 | No | A single character or number which is used as a unique identification for the fund. This identifier is used in the voucher number format |
| 4 | Level | Numeric | 50 | Yes | The Funds can be defined in the tree structure, so the Level indicates the structure in which the funds would be set up. Root nodes will be level 0 and the next level funds will have value as 1 and the next level as value 2 |
| 5 | Parent Fund | Text | 50 | No | If the ULB’s using multiple Funds then a Hierarchy of “Parent-Child “can be set up for the Fund, so under each Parent Fund multiple child funds can be set up |

#### Steps to fill data

1. Download the data template attached to this page.
2. Have it open and go through all the headers and understand the meaning of them by referring 'Data Definition' section.
3. Make sure all the headers, its data type, field size and its definition/ description is understood properly. In case of any doubt, please reach out to the person who has shared this document with you to discuss the same and clear out the doubts.
4. Identify all different types of Funds on the basis of ULB’s functions.
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
      <td style="text-align:left">The Fund Code that is defined by the state team should be numeric and
        Unique.</td>
      <td style="text-align:left">01</td>
    </tr>
    <tr>
      <td style="text-align:left">2</td>
      <td style="text-align:left">The Fund Name should not contain any special characters</td>
      <td style="text-align:left">
        <p>Municipal Fund : [Allowed]</p>
        <p>#Municipal Fund! : [Not allowed]</p>
      </td>
    </tr>
  </tbody>
</table>

### Attachments

{% file src="../../../../.gitbook/assets/configuration-data-template-fund.xlsx" caption="Configuration Data Template" %}

{% file src="../../../../.gitbook/assets/sample-confugration-data-fund.xlsx" caption="Sample Data" %}



