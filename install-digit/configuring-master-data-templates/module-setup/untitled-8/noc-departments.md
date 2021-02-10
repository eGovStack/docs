# NOC Departments

### Introduction

No objection certificates \(NOC\) are certifications or permissions acquired from various bodies like Airport authority, monument authority, etc before any construction activities actually take place.

To acquire a building permit, an applicant needs to acquire NOC from the concerned authorities. Add the specific authorities at the State/ULB level in the NOC Departments master list for automated processing of NOCs. Refer to the [National Bye-Laws](http://mohua.gov.in/upload/uploadfiles/files/Chap-4.pdf) for details on State/ULB specific NOC requirements.

### Data Table

| Sr. No. | Government Department\* | Application type\* | Integration Type\* | SLA |
| :--- | :--- | :--- | :--- | :--- |
| 1 | Airport Authority of India \(AAI\) | Permit | Web API | 15 |
| 2  | National Monument Authority \(NMA\) | Occupancy certificate | Manual | 15 |

{% hint style="info" %}
Data given in the table is sample data for reference.
{% endhint %}

### Procedure

#### Data Definition

| Sr. No. | Column Name | Data Type | Data Size | Is Mandatory? | Description |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | Government Department | Text | 256 | Yes | Name of the department from where a NOC has to be acquired. This needs to be provided and uploaded into the system |
| 2 | Application Type | Text | 256 | Yes | The type of applications for which NOC is required. Check the Data Table for illustration |
| 3 | Integration Type | Text | 256 | Yes | This is about the approach of integration to be adopted with government departments systems |
| 4 | SLA | Integer | 2 | No | Timelines required \(if any\) for the NOC to be acquired. This information needs to be updated in the SLA column |

#### Steps to fill data

1. Download the data template attached to this page.
2. Refer to the ‘Data Definition’ section of this document to understand the headers in the template sheet, their data type, size, and definitions.
3. Reach out the person who shared the template for further details or to clear your doubts. Identify if the State/ULB has a provision for capturing pipe size for connections.
4. Identify all the departments, services and the approach on integration and then fill into the given template.
5. Go through the checklist to verify the data. Make sure that each and every point mentioned in the checklist is covered.

### Checklist

The checklist is a set of activities to be performed one the data is filled into a template to ensure data requirements are met. These activities have been divided into 2 groups as given below.

#### Common Checklist

This checklist covers all the activities which are common across the entities.

| Sr. No. | Checklist Parameter | Example |
| :--- | :--- | :--- |
| 1 | Make sure that each and every point in this reference list has been taken care of | [Checklist](../untitled-1/checklist.md) |

#### Entity Specific Checklist

There is no separate entity-specific checklist for this entity.

### Attachments

{% file src="../../../../.gitbook/assets/configurable-data-template-noc-departments\_v1.xlsx" caption="Configuration Data Template " %}

{% file src="../../../../.gitbook/assets/noc-department-sample.xlsx" caption="Sample Data" %}

