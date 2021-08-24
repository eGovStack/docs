---
description: Browse details on configuring master data template
---

# Grievance Sub Type

## Introduction <a id="introduction"></a>

The grievance sub-type defines the second level of classification of grievances which are related to ULB’s functions and adds detail to a grievance type.

## Data Table <a id="data-table"></a>

The data table below represents the structure of the template and given here to explain the template in detail.

| Sr. No. | Grievance Subtype Code\* | Grievance Subtype \* \(In English\) | Grievance Subtype\* \(In Local Language\) | Grievance Type Code\* | Department Code\* | SLA\* \(In Hours\) |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | SLS01 | No Street Light | कोई स्ट्रीट लाइट नहीं है | SLS | TP | 48 |
| 2 | SLS02 | Street Light Not Working | स्ट्रीट लाइट काम नहीं कर रही है | SLS | TP | 48 |
| 3 | WNS01 | Illegal Discharge of Sewage | सीवेज का अवैध निपटान | WNS | PHS | 48 |

The data given in the table is sample data.

## Procedure <a id="procedure"></a>

### Data Definition <a id="data-definition"></a>

| Sr. No. | Column Name | Data Type | Data Size | Is Mandatory? | Definition/ Description |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | Grievance Subtype Code | Alphanumeric | 64 | Yes | Unique code is given to the grievance subtype and is used to uniquely identify the complaint subtype. E.g. SLS01 given above in data table to identify Street Lights complaint subtype |
| 2 | Grievance Subtype \(In English\) | Text | 256 | Yes | This is the text or string stating grievance subtype in English |
| 3 | Grievance Subtype \(In Local Language\) | Text | 256 | Yes | This the text or string stating the grievance subtype in local language like Hindi, Telugu etc. whatever is applicable |
| 4 | Grievance Type Code | Reference | 64 | Yes | Reference to parent grievance type code from the[ Grievance Type](grievance-type.md) entity |
| 5 | Department Code | Reference | 64 | Yes | Unique department code from the [ULB's Departments](https://docs.digit.org/install-digit/configuring-master-data-templates/environment-setup/state-level-setup/ulb-departments) entity |
| 6 | SLA \(In Hours\) | Decimal | \(5,2\) | Yes | This field defined the service level agreements in hours. This the time within which a complaint raised to be resolved |

### Steps to fill data <a id="steps-to-fill-data"></a>

1. Download the data template attached to this page.
2. Have it open and go through all the headers and understand the meaning of them by referring 'Data Definition' section.
3. Make sure all the headers, its data type, field size and its definition/ description is understood properly. In case of any doubt, please reach out to the person who has shared this document with you to discuss the same and clear out the doubts.
4. Identify all different subtypes of grievances on the basis of ULB’s functions and grievance types.
5. Start filling the data starting from serial no. and complete a record at once. repeat this exercise until the entire data is filled into a template.
6. Verify the data once again by going through the checklist and taking care of each and every checklist point/ activity mentioned in the checklist.

## Checklist <a id="checklist"></a>

The checklist is a set of activities to be performed after the data is filled into a template to ensure data type, size, and format of data is as per the expectation. These activities have been divided into 2 groups as given below.

### Common Checklist <a id="common-checklist"></a>

This checklist covers all the activities which are common across the entities.

To see the common checklist refer to the page [Checklist](https://docs.digit.org/install-digit/configuring-master-data-templates/module-setup/untitled-1/checklist) consisting of all the activities which are to be followed to ensure complete and quality data.

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
      <td style="text-align:left">Grievance Subtype code should not have any special characters other than
        &#x2018;-&apos;, and &apos;_&#x2019;</td>
      <td style="text-align:left">
        <p>SLS01 - [Allowed]</p>
        <p>SLSA - [Allowed]</p>
        <p>SLS#1 - [Not Allowed]</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">2</td>
      <td style="text-align:left">Grievance Subtype should be text and should not contain special characters
        other than &#x2018;-&apos;, &apos;_&apos;, SPACE</td>
      <td style="text-align:left">
        <p>No Street Light - [Allowed]</p>
        <p>No Street Light# -[Not allowed]</p>
      </td>
    </tr>
  </tbody>
</table>

## Attachments <a id="attachments"></a>

{% file src="../../../../.gitbook/assets/grievance-subtype\_template\_v1 \(1\).xlsx" caption="Sample Data" %}

{% file src="../../../../.gitbook/assets/grievance-type-and-subtype\_configuraion-data-1-.xlsx" caption="Configuration Data Template" %}

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation ](https://egov.org.in/)is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).

