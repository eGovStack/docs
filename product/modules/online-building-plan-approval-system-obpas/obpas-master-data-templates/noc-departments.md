# NOC Departments

## Introduction <a id="introduction"></a>

No objection certificates \(NOC\) are certifications or permissions acquired from various bodies like Airport authority, monument authority, etc before any construction activities actually take place.

To acquire a building permit, an applicant needs to acquire NOC from the concerned authorities. Add the specific authorities at the State/ULB level in the NOC Departments master list for automated processing of NOCs. Refer to the [National Bye-Laws](http://mohua.gov.in/upload/uploadfiles/files/Chap-4.pdf) for details on State/ULB specific NOC requirements.

## Data Table <a id="data-table"></a>

| Sr. No. | Government Department\* | Application type\* | Integration Type\* | SLA |
| :--- | :--- | :--- | :--- | :--- |
| 1 | Airport Authority of India \(AAI\) | Permit | Web API | 15 |
| 2 | National Monument Authority \(NMA\) | Occupancy certificate | Manual | 15 |

The data given in the table is sample data for reference.

## Procedure <a id="procedure"></a>

### Data Definition <a id="data-definition"></a>

| Sr. No. | Column Name | Data Type | Data Size | Is Mandatory? | Description |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | Government Department | Text | 256 | Yes | Name of the department from where a NOC has to be acquired. This needs to be provided and uploaded into the system |
| 2 | Application Type | Text | 256 | Yes | The type of applications for which NOC is required. Check the Data Table for illustration |
| 3 | Integration Type | Text | 256 | Yes | This is about the approach of integration to be adopted with government departments systems |
| 4 | SLA | Integer | 2 | No | Timelines required \(if any\) for the NOC to be acquired. This information needs to be updated in the SLA column |

### Steps to fill data <a id="steps-to-fill-data"></a>

1. Download the data template attached to this page.
2. Refer to the ‘Data Definition’ section of this document to understand the headers in the template sheet, their data type, size, and definitions.
3. Reach out to the person who shared the template for further details or to clear your doubts. Identify if the State/ULB has a provision for capturing pipe size for connections.
4. Identify all the departments, services and the approach on integration and then fill into the given template.
5. Go through the checklist to verify the data. Make sure that each and every point mentioned in the checklist is covered.

## Checklist <a id="checklist"></a>

The checklist is a set of activities to be performed once the data is filled into a template to ensure data requirements are met. These activities have been divided into 2 groups as given below.

### Common Checklist <a id="common-checklist"></a>

This checklist covers all the activities which are common across the entities.

| Sr. No. | Checklist Parameter | Example |
| :--- | :--- | :--- |
| 1 | Make sure that each and every point in this reference list has been taken care of | ​[Checklist](https://docs.digit.org/configure-digit/configuring-master-data-templates/module-setup/common-config/checklist)​ |

### Entity Specific Checklist <a id="entity-specific-checklist"></a>

There is no separate entity-specific checklist for this entity.

## Attachments <a id="attachments"></a>

[Configuration Data Templateconfigurable-data-template-noc-departments\_v1.xlsx - 10KB](https://firebasestorage.googleapis.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-MERG_iQW5oN4ukgXP8K%2Fsync%2F8b1686fc0d5aaaa522eb396c917c3817d5907f07.xlsx?generation=1602050612582182&alt=media)

<<<<<<< HEAD
[Sample Datanoc-department-sample.xlsx - 10KB](https://firebasestorage.googleapis.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-MERG_iQW5oN4ukgXP8K%2Fsync%2F2d5f4218da09b30fbe52fec5aaf8502d436cc000.xlsx?generation=1602050612588742&alt=media)[    
](https://docs.digit.org/configure-digit/configuring-master-data-templates/module-setup/obpas-data/town-planning-schemes)

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation ](https://egov.org.in/)is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).
=======
[Sample Datanoc-department-sample.xlsx - 10KB](https://firebasestorage.googleapis.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-MERG_iQW5oN4ukgXP8K%2Fsync%2F2d5f4218da09b30fbe52fec5aaf8502d436cc000.xlsx?generation=1602050612588742&alt=media)[  
](https://docs.digit.org/configure-digit/configuring-master-data-templates/module-setup/obpas-data/town-planning-schemes)

 [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation ](https://egov.org.in/)is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).
>>>>>>> 64dca8adbdf64336b1a8203199b3791fa23434fa

