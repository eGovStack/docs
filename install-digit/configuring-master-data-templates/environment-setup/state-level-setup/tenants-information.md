# Tenants Information

### Introduction

An Urban Local Body \(ULB\) is defined as a tenant. The information which describes the various attributes of a ULB is known as tenant information. This detail is required to add the ULB into the system.

### Data Table

| S. No. | ULB Name\* | ULB Code\* | ULB Grade\* | City Name\* | City Local Name | District Name\* | District Code\* | Region Name | Region Code |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
|  1 | Sonepur Nagar Panchayat | 47 | Corp | Sonepur | Sonepur | Banka | BN47 | Bihar | BBD47 |

| Contact Number\* | Address\* | ULB Website\* | Latitude | Longitude | Email Address | GIS Location Link | Call Center No. | Facebook Link | Twitter Link | Logo file Path\* |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 98362532657 | Main Hall, Sonepur | [nagarsewa.sonepur.com](http://nagarsewa.sonepur.com/) | 24.8874° N | 86.9198° E | snp@bihar.gov.in |  |  |  |  |  [Logo](https://drive.google.com/drive/folders/1mDosChmhu-RO6O3Z5FlmSJR_VWbb8oxR) |

{% hint style="info" %}
Data given in the table is a sample data.
{% endhint %}

### Procedure

#### Data Definition

| Sr. No. | Column Name  | Data Type | Data Size | Is Mandatory? | Definition/ Description |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | ULB Name | Text | 256 | Yes | Name of ULB. E.g. Kannur Municipal Corporation/ Saptarishi Municipal Council |
| 2 | ULB Code  | Alphanumeric | 64 | Yes | It is a unique identifier which is assigned to each ULB. LGD \(Local Government Directory\) has already assigned a code urban local bodies and the same is used here |
| 3 | ULB Grade | Alphanumeric | 64 | Yes | Grade of ULB. e.g. Corporation, Municipality, Nagar Panchayat etc |
| 4 | City Name | Text | 256 | Yes | Name of city/ town which is covered by the ULB. E.g. Kannur/ Saptarishi |
| 5 | City Local Name | Text | 256 | No | Name of the city in the local language. e.g Telugu, Hindi etc |
| 6 | District Name | Text | 256 | Yes | Name of the District where the city is situated |
| 7 | District Code  | Alphanumeric | 64 | Yes | It is a unique identifier which is assigned to each district. LGD \(Local Government Directory\) has already assigned code districts and the same is used here |
| 8 | Region Name  | Text | 256 | No | Name of the region the listed district belongs to |
| 9 | Region Code  | Alphanumeric | 64 | No | Unique code of the region to uniquely identify it |
| 10 | Contact Number | Alphanumeric | 10 | Yes |  Contact person phone no. of ULB |
| 11 | Address | Text | 256 | Yes |  Postal address of the ULB for the correspondence |
| 12 | ULB Website | Alphanumeric | 256 | Yes | URL address of the website for the ULB |
| 13 | Email Address | Alphanumeric | 64 | No | Email of the address of ULB where the email from the citizen can be received |
| 14 | Latitude  | Alphanumeric | 64 | No | Latitude part of coordinates of the centroid of the city |
| 15 | Longitude  | Alphanumeric | 64 | No | Longitude part of coordinates of the centroid of the city |
| 16 | GIS Location Link  | Text | NA | No |  GIS Location link of the ULB |
| 17 | Call Center No | Alphanumeric | 10 | No | Call centre contact number of ULB |
| 18 | Facebook Link  | Text | NA | No | Face book page link of ULB |
| 19 | Twitter Link  | Text | NA | No | Twitter page link of the ULB |
| 20 | Logo file Path  | Document | NA | Yes | URL of logo file path to download the logo of ULB  |

### Steps to fill data <a id="Steps-to-fill-data"></a>

1. Download the data template attached to this page.
2. Have it open and go through all the headers and understand the meaning as given in this document under section 'Data Definition'.
3. Make sure all the headers, its data type, field size and its definition/ description are understood properly.
4. In case of any doubt, please reach out to the person who has shared this document with you and discuss the same to clear out the doubts.
5. Start filling the data starting from serial no. and complete a record at once. repeat this exercise until the entire data is filled into a template.
6. Verify the data once again by going through the checklist by taking care of each and every point mentioned in the checklist.

### Checklist

The checklist is a set of activities to be performed once the data is filled into a template to ensure data type, size, and format of data is as per the expectation. These activities have been divided into 2 groups as given below.

#### Common Checklist

This checklist covers all the activities which are common across the entities.

To see common checklist refer to the page [Checklist](../../module-setup/untitled-1/checklist.md) consisting of all the activities which are to be followed to ensure completeness and quality of data.

#### Entity Specific Checklist

This checklist covers the activities which are specific to the entity. There are no checklist activities exists which are specific to the entity.

### Attachments

{% file src="../../../../.gitbook/assets/confiruation-data-template-tenant-information\_v1.xlsx" caption="Configuration Data Template" %}

{% file src="../../../../.gitbook/assets/sample-configuration-data-tenant-information.xlsx" caption="Sample Data Template" %}



