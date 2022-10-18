# Boundary Hierarchies

### Introduction

A ULB is divided into certain categories of boundaries by ULB administrative authorities in order to carry out ULB’s functions better. A ULB/City could be divided by a different set of delimitation of boundaries based on functions as given below.

1. Revenue - Delimitation of ULB into boundaries to perform the target setting and collection of revenue.
2. Administration - Delimitation of ULB into boundaries for the better administration of ULB.
3. Locality/ Location - Delimitation of ULB into boundaries based on the places known to citizen with names and easily identifiable by the common person.

All these authorities have designated certain levels of boundary classification for a certain ULB.

### Data Table

The below mention table is used to collect data for the types of hierarchy being followed:

| Sr. No. | Code\* | Boundary Hierarchy Type\* | Description                                                                                                                                                                                                                                                   |
| ------- | ------ | ------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1       | ADM    | Administration            | Administration level boundary classified on the basis of administrative functions such as scrutinize certain rules and regulations                                                                                                                            |
| 2       | REV    | Revenue                   | Revenue-based classification of a ULB is done on the basis of revenue collection                                                                                                                                                                              |
| 3       | LOC    | Locality                  | <p>Location-based classification could be done in order to identify a certain place.<br>For example, Locality of a house of a citizen could follow the below hierarchy:</p><ol><li>House no.</li><li>Mohalla</li><li>Area</li><li>Ward</li><li>City</li></ol> |

{% hint style="info" %}
The above-mentioned data for the boundary hierarchy is sample data.
{% endhint %}

### Procedure

#### Data Definition

| Sr. No. | Column Name             | Data Type    | Data Size | Is Mandatory? | Definition/ Description                                                               |
| ------- | ----------------------- | ------------ | --------- | ------------- | ------------------------------------------------------------------------------------- |
| 1       | Code                    | Alphabet     | 64        | Yes           | Code is used to identify a certain classification of the type of boundary hierarchy   |
| 2       | Boundary Hierarchy Type | Alphanumeric | 256       | Yes           | The meaningful name to define one group of boundaries defined to perform one function |
| 3       | Description             | Alphanumeric | 256       | Yes           | A brief description of the boundary hierarchy                                         |

#### Steps to fill data

1. Download the data template attached to this page.
2. Get a good understanding of all the headers in the template sheet, their data type, size, and definitions by referring to the ‘Data Definition’ section of this document.
3. In case of any doubt, please reach out to the person who has shared this template with you to discuss and clear your doubts.
4. Identify all the types of boundaries which are being used in the state in order to carry out various administrative/revenue functions.
5. Start filling the data starting from serial no. and complete a record at once. repeat this exercise until the entire data is filled into a template.
6. Then fill up the hierarchy types and the codes in the respective columns in the template.
7. Code should be created for the type of boundary being classified.
8. A brief description of the boundary hierarchy type would be helpful.
9. Verify the data once again by going through the checklist and taking care of each and every point mentioned in the checklist.

### Checklist

The checklist is a set of activities to be performed one the data is filled into a template to ensure data type, size, and format of data is as per the expectation. These activities have been divided into 2 groups as given below.

#### Common Checklist

This checklist covers all the activities which are common across the entities.

| Sr. No. | Checklist Parameter                                                               | Example                                                    |
| ------- | --------------------------------------------------------------------------------- | ---------------------------------------------------------- |
| 1       | Make sure that each and every point in this reference list has been taken care of | [Checklist](../../module-setup/common-config/checklist.md) |

#### Entity Specific Checklist

This checklist covers the activities which are specific to the entity.

| Sr. No. | Checklist Parameter                                                                              | Example |
| ------- | ------------------------------------------------------------------------------------------------ | ------- |
| 1       | Make sure that the hierarchies types should be uniform across all the ULB’s /cities in the state | -       |
| 2       | Only 3 types of boundary hierarchies are allowed                                                 | -       |

### Attachments

{% file src="../../../../.gitbook/assets/configurable-data-template-boundary-hierachies-v1.xlsx" %}
Configuration Data Template
{% endfile %}

{% file src="../../../../.gitbook/assets/confugurable-sample-data-boundary-hierarchy-v1.xlsx" %}
Sample Data Template
{% endfile %}

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)​](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation](https://egov.org.in/) is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).
