# Sub Ledger Category

### Introduction

The Sub-ledger category provides details behind entries in the general ledger used in accounting, which is also called subsidiary ledgers. The total of the Sub-ledger would match the line item amount on the general ledger. This corresponding line item in the general ledger is referred to as the controlling account.

Any other type of Sub-ledgers other than standard Sub-ledgers available in the system is to be created here. Standard sub-ledger available in the system is Contractor, Supplier and Employee.

### Data Table

| Sr No. | Name\* | Description\* |
| :--- | :--- | :--- |
| 1 | Telephone | Telephone |
| 2 | Other Creditors | Other Creditors |
| 3 | ULB and Other Dept | ULB and Other Departments |

### Procedure

#### Data Definition

| Sr. No. | Column Name | Data Type | Data Size | Is Mandatory? | Definition/ Description |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | Name | Text | 50 | Yes | The Name indicates the sub-ledger category, this will facilitate the user to record the transaction at the Sub-ledger level. \(Example: While creating a bill, user can select the Sub-ledger details as a contractor to whom the bill need to be paid and the same can be recorded under the sub-ledger GL code which is mapped to the contractor\) |
| 2 | Description | Text | 50 | Yes | A short description provided to the name of the Sub-ledger |

#### Steps to fill data

1. Download the data template attached to this page.
2. Have it open and go through all the headers and understand the meaning of them by referring 'Data Definition' section.
3. Make sure all the headers, its data type, field size and its definition/ description is understood properly. In case of any doubt, please reach out to the person who has shared this document with you to discuss the same and clear out the doubts.
4. Identify all different types of sub-ledger category.
5. Start filling the data starting from serial no. and complete a record at once. repeat this exercise until the entire data is filled into a template.
6. Verify the data once again by going through the checklist and taking care of each and every point mentioned in the checklist.

### Checklist

The checklist is a set of activities to be performed once the data is filled into a template to ensure data type, size, and format of data is as per the expectation. These activities have been divided into 2 groups as given below.

#### Common Checklist

This checklist covers all the activities which are common across the entities.

| Sr. No | Checklist Parameter | Example |
| :--- | :--- | :--- |
| 1 | Make sure that each and every point in this reference list has been taken care of | [Checklist](../common-config/checklist.md) |

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
      <td style="text-align:left">The name should be unique and should not contain any special characters</td>
      <td
      style="text-align:left">
        <p>Contractor : [Allowed]</p>
        <p>#Contractor! : [Not allowed]</p>
        </td>
    </tr>
  </tbody>
</table>

### Attachments

{% file src="../../../../.gitbook/assets/configuration-data-template-subledger-category.xlsx" caption="Configuration Data Template" %}

{% file src="../../../../.gitbook/assets/sample-confugration-data-subledger-category.xlsx" caption="Sample Data" %}



