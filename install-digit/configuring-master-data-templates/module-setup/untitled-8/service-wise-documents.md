# Service-Wise Documents

### Introduction

Service-wise documents list tells about the documents required for processing of listed services. Citizens can view the checklist based on the selected service. States/ULBs can configure the list of supporting documents required for each service.

### Data Table

| Sr. No. | Service Code\* | Service Name | Document Name\* | Is Mandatory?\* |
| :--- | :--- | :--- | :--- | :--- |
| 1 | NC | New Construction | Aadhar Card | No |
| 2 | NC | New Construction | Fire NOC | Yes |

{% hint style="info" %}
Data given in the table is sample data for reference.
{% endhint %}

### Procedure

#### Data Definition

| Sr. No. | Column Name | Data Type | Data Size | Is Mandatory? | Description |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | Service Code | Alphanumeric | 64 | Yes | Code of service - Refer to the [service list ](list-of-services.md)to understand in detail |
| 2 | Service Name | Text | 64 | No | Name of service - Refer to the [service list](list-of-services.md) to understand in detail |
|  | Document Name\* | Text | 256 | Yes | Name of documents which are needed to avail the service |
| 3 | Is Mandatory? | Text | 3 | Yes | It indicates if the provided document is mandatory or not to avail the service |

#### Steps to fill data

1. Download the data template attached to this page.
2. Refer to the ‘Data Definition’ section of this document to understand the headers in the template sheet, their data type, size, and definitions.
3. Reach out the person who shared the template for further details or to clear your doubts. Identify if the State/ULB has a provision for capturing pipe size for connections.
4. Identify the documents which are needed to avail the services and fill into the given template.
5. Go through the checklist to verify the data. Make sure that each and every point mentioned in the checklist is covered.

### Checklist

The checklist is a set of activities to be performed one the data is filled into a template to ensure data entry requirements are met. These activities have been divided into 2 groups as given below.

#### Common Checklist

This checklist covers all the activities which are common across the entities.

| Sr. No. | Checklist Parameter | Example |
| :--- | :--- | :--- |
| 1 | Make sure that each and every point in this reference list has been taken care of | [Checklist](https://digit-discuss.atlassian.net/wiki/spaces/DO/pages/502203140/Checklist) |

#### Entity Specific Checklist

There is no separate entity-specific checklist for this entity.

### Attachments

{% file src="../../../../.gitbook/assets/sample-configuration-data-service-documents.xlsx" caption="Sample Data" %}

{% file src="../../../../.gitbook/assets/configuration-data-template-service-documents\_v1.xlsx" caption="Configuration data template" %}

