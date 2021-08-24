# Service Sub Category GL Code Mapping

## Introduction <a id="introduction"></a>

Service Subcategory is mapped to relevant GL code to help capture the accounting-related parameters for each service subcategory. The same is used to pass the accounting vouchers into the accounting and finance system.

## Data Table <a id="data-table"></a>

| Sr.No | Service Subcategory Code\* | Service Subcategory \(English\)\* | Service Subcategory \(Local Language\)\* | GLCODE\* | ULB CODE | DEPT CODE | FUND Code |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | PEF0478 | Parks Entry Fee | पार्क प्रवेश शुल्क | 1404007 | 1001 | DEPT\_1 | 01 |
| 2 | SANT0045 | Sanitation Tax | स्वच्छता कर | 1405010 | 1002 | DEPT\_2 | 01 |

The data given in the table above is sample data.

## Procedure <a id="procedure"></a>

### Data Definition <a id="data-definition"></a>

| Sr. No. | Column Name | Data Type | Data Size | Is Mandatory? | Definition/ Description |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | Service Category | Text | 250 | Yes | The type of category which is to be mapped with the relevant service subcategory. Click[ here](service-category.md) for Service category reference |
| 2 | Service Subcategory \(English\) | Text | 250 | Yes | Name of “Service Sub-category” in English. This will help the user to select the Subcategory name while doing the collection. Click[ here](service-sub-category.md) for Service Subcategory reference |
| 3 | Service Subcategory \(local Language\) | Text | 250 | Yes | Name of “Service Sub-category” in Local Language. This will help the user to select the Subcategory name while doing the collection |
| 4 | GLCODE | Alphanumeric | 50 | Yes | General Ledger Code \(GL Code\) is a string of alphanumeric characters assigned to each Service. Click [here](https://docs.digit.org/configure-digit/configuring-master-data-templates/module-setup/finance-data/sub-ledger-category) for the General Ledger Code Reference |
| 5 | ULB CODE | Alphanumeric | 50 | No | The CODE which is specified and assigned to each ULB. It refers to the [department](https://docs.digit.org/configure-digit/configuring-master-data-templates/environment-setup/state-level-setup/ulb-departments)​ |
| 6 | DEPT CODE | Alphanumeric | 50 | No | The Master Department Code linked to the“Service Category” at the State Level. The Department Code can be ascertained from the ULB Departments master. Click [here](https://docs.digit.org/configure-digit/configuring-master-data-templates/environment-setup/state-level-setup/ulb-departments) to learn more about ULB Departments |
| 7 | FUND Code | Text | 250 | No | The type of fund allocated/associated with the respective service subcategory. Click[ here](../../finance/finance-master-data-templates/funds.md) for Fund reference |

### Steps to Fill Data <a id="steps-to-fill-data"></a>

1. Download the data template attached to this page.
2. Have it open and go through all the headers and understand the meaning of them by referring 'Data Definition' section.
3. Make sure all the headers, its data type, field size and its definition/ description is understood properly. In case of any doubt, please reach out to the person who has shared this document with you to discuss the same and clear out the doubts.
4. Identify all different types of service subcategory GL code on the basis of ULB’s functions.
5. Start filling the data starting from serial no. and complete a record at once. repeat this exercise until the entire data is filled into a template.
6. Verify the data once again by going through the checklist and taking care of each and every point mentioned in the checklist.

## Checklist <a id="checklist"></a>

The checklist is a set of activities to be performed once the data is filled into a template to ensure data type, size, and format of data is as per the expectation. These activities have been divided into 2 groups as given below.

### Common Checklist <a id="common-checklist"></a>

This checklist covers all the activities which are common across the entities.

| Sr. No | Checklist Parameter | Example |
| :--- | :--- | :--- |
| 1 | Make sure that each and every point in this reference list has been taken care of | ​[Checklist](https://docs.digit.org/configure-digit/configuring-master-data-templates/module-setup/common-config/checklist)​ |

### Entity Specific Checklist <a id="entity-specific-checklist"></a>

This checklist covers the activities which are specific to the entity. There is no entity-specific checklist activity applicable.

## Attachments <a id="attachments"></a>

[Configuration Data Templateconfiguration-data-template-service-subcategory-gl-code-mapping.xlsx - 11KB](https://firebasestorage.googleapis.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-MERG_iQW5oN4ukgXP8K%2Fsync%2F903003f5e9833d0d274c3bd60c00bc4bad607b81.xlsx?generation=1602050607397274&alt=media)

[Sample Datasample-confugration-data-service-subcategory-gl-code-mapping.xlsx - 11KB](https://firebasestorage.googleapis.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-MERG_iQW5oN4ukgXP8K%2Fsync%2F9ce715075400445059d67bddcf3c278e782485e8.xlsx?generation=1602050607472876&alt=media)

<<<<<<< HEAD
[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation ](https://egov.org.in/)is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).
=======
  


 [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation ](https://egov.org.in/)is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).
>>>>>>> 64dca8adbdf64336b1a8203199b3791fa23434fa

