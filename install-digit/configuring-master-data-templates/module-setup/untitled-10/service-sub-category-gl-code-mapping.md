# Service Sub Category GL Code Mapping

### Introduction

Service Subcategory is mapped to relevant GL code to help capture the accounting-related parameters for each service subcategory. The same is used to pass the accounting vouchers into accounting and finance system.

### Data Table

| Sr.No | Service Subcategory Code\* | Service Subcategory \(English\)\* | Service Subcategory \(Local Language\)\* | GLCODE\* | ULB CODE | DEPT CODE | FUND Code |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | PEF0478 | Parks Entry Fee | पार्क प्रवेश शुल्क | 1404007 | 1001 | DEPT\_1 | 01 |
| 2 | SANT0045 | Sanitation Tax | स्वच्छता कर | 1405010 | 1002 | DEPT\_2 | 01 |

{% hint style="info" %}
Data given in the table is a sample data.
{% endhint %}

### Procedure

#### Data Definition

| Sr. No. | Column Name | Data Type | Data Size | Is Mandatory? | Definition/ Description |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | Service Category | Text | 250 | Yes | The type of category which is to be mapped with the relevant service subcategory. Click[ here](service-category.md) for Service category reference |
| 2 | Service Subcategory \(English\) | Text | 250 | Yes | Name of “Service Sub-category” in English. This will help the user to select the Subcategory name while doing the collection. Click[ here](service-sub-category.md) for Service Subcategory reference |
| 3 | Service Subcategory \(local Language\) | Text | 250 | Yes | Name of “Service Sub-category” in Local Language. This will help the user to select the Subcategory name while doing the collection |
| 4 | GLCODE | Alphanumeric | 50 | Yes | General Ledger Code \(GL Code\) is a string of alphanumeric characters assigned to each Service. Click[ here](../untitled-6/sub-ledger-category.md) for the General Ledger Code Reference |
| 5 | ULB CODE | Alphanumeric | 50 | No | The CODE which is specified and assigned to each ULB. It refers to the [department](../../environment-setup/state-level-setup/ulb-departments.md) |
| 6 | DEPT CODE | Alphanumeric | 50 | No | The Master Department Code linked to the“Service Category” at the State Level. The Department Code can be ascertained from the ULB Departments master. Click[ here](../../environment-setup/state-level-setup/ulb-departments.md) to learn more about ULB Departments |
| 7 | FUND Code | Text | 250 | No | The type of fund allocated/associated with the respective service subcategory. Click [here](../untitled-6/funds.md) for Fund reference |

#### Steps to Fill Data

1. Download the data template attached to this page.
2. Have it open and go through all the headers and understand the meaning of them by referring 'Data Definition' section.
3. Make sure all the headers, its data type, field size and its definition/ description is understood properly. In case of any doubt, please reach out to the person who has shared this document with you to discuss the same and clear out the doubts.
4. Identify all different types of service subcategory GL code on the basis of ULB’s functions.
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

This checklist covers the activities which are specific to the entity. There is no entity-specific checklist activity applicable.

### Attachments

{% file src="../../../../.gitbook/assets/configuration-data-template-service-subcategory-gl-code-mapping.xlsx" caption="Configuration Data Template" %}

{% file src="../../../../.gitbook/assets/sample-confugration-data-service-subcategory-gl-code-mapping.xlsx" caption="Sample Data" %}

