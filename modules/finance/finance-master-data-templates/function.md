# Function

## Introduction <a id="introduction"></a>

Functions shall represent the various functions or services carried out by the ULBs. Functions are provided through various responsibilities centres called Departments.

Functions of the ULB can have three levels within it.

* The first level under this group represents various functions both obligatory and discretionary. Identified as 0 in the template.
* The second Level in function would represent the particular type of service under a function, known as “Function Description”. Identified as 1 in the template
* The third level will represent a particular cost centre, Known as “Cost Centre”, which provides the service. Identified as 2 in the template.

## Data Table <a id="data-table"></a>

| \*Sr. No. | \*Name | \*Code | \*Level | Parent Type | Parent Code |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | General Administration | 10 | 0 | Nil | Nil |
| 2 | GENERAL ADMINISTRATION: Administration | 1011 | 1 | General Administration | 10 |
| 3 | General Department | 101100 | 2 | GENERAL ADMINISTRATION: Administration | 1011 |
| 4 | Public Works | 20 | 0 | Nil | Nil |
| 5 | PUBLIC WORKS: Roads and Pavement | 2021 | 1 | Public Works | 20 |
| 6 | Roads and Building Maintenance | 202101 | 2 | PUBLIC WORKS: Roads and Pavement | 2021 |

The data given in the table is sample data.

## Procedure <a id="procedure"></a>

### Data Definition <a id="data-definition"></a>

| Sr No | Column Name | Data Type | Data Size | Is Mandatory? | Definition/ Description |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | Name | Text | 250 | Yes | To indicate the Function name, User can select a particular function code while recording a transaction in the system. This will facilitate in generating a report at the function level |
| 2 | Code | Alphanumeric | 50 | Yes | The unique code is given to the individual function. Child functions have to follow number pattern starting with the parent code |
| 3 | Level | Numeric | 50 | Yes | As per NMAM, the Function can be defined in the tree structure, so the Level indicates the structure in which the function would be setup. Root nodes will be level 0 and the next level funds will have value as 1 and the next level as value 2 |
| 4 | Parent Type | Text | 250 | No | If the ULB’s using multiple Functions then a Hierarchy of “Parent-Child “can be set up for the Function, so under each Parent Function a multiple child function can be set up |
| 5 | Parent Code | Alphanumeric | 50 | No | The unique code representing the parent type function |

### Steps to fill data <a id="steps-to-fill-data"></a>

1. Download the data template attached to this page.
2. Have it open and go through all the headers and understand the meaning of them by referring 'Data Definition' section.
3. Make sure all the headers, its data type, field size and its definition/ description is understood properly. In case of any doubt, please reach out to the person who has shared this document with you to discuss the same and clear out the doubts.
4. Identify all different types of Function in the ULB.
5. Start filling the data starting from serial no. and complete a record at once. repeat this exercise until the entire data is filled into a template.
6. Verify the data once again by going through the checklist and taking care of each and every point mentioned in the checklist.

## Checklist <a id="checklist"></a>

The checklist is a set of activities to be performed once the data is filled into a template to ensure data type, size, and format of data is as per the expectation. These activities have been divided into 2 groups as given below.

### Common Checklist <a id="common-checklist"></a>

This checklist covers all the activities which are common across the entities.

| Sr. No | Checklist Parameter | Example |
| :--- | :--- | :--- |
| 1 | Make sure that each and every point in this reference list has been taken care of. | ​[Checklist](https://docs.digit.org/configure-digit/configuring-master-data-templates/module-setup/common-config/checklist)​ |

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
      <td style="text-align:left">The Function Name should not contain any special characters</td>
      <td style="text-align:left">
        <p>General Administration : [Allowed]</p>
        <p>#General Administration! : [Not allowed]</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">2</td>
      <td style="text-align:left">The Function Code that is defined by the state team should be alphanumeric
        and Unique.</td>
      <td style="text-align:left">10, 1011 or 101100</td>
    </tr>
  </tbody>
</table>

## Attachments <a id="attachments"></a>

[Configuration Data Templateconfiguration-data-template-function.xlsx - 10KB](https://firebasestorage.googleapis.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-MERG_iQW5oN4ukgXP8K%2Fsync%2F69336db3791d249000a0456d4a9dfdeea18b4218.xlsx?generation=1602050612969897&alt=media)

[Sample Datasample-confugration-data-function.xlsx - 10KB](https://firebasestorage.googleapis.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-MERG_iQW5oN4ukgXP8K%2Fsync%2F66930cfe921b19bf32bd056c8dc5508b8f256533.xlsx?generation=1602050612991349&alt=media)

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation ](https://egov.org.in/)is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).

