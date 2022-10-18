# Localization

### Introduction

Localization is a practice to localize various UI visible data into the local wordings according to the client's requirements. This practice of localization is enforced on various clients so that it becomes easier for the people using the service to understand the common terminology and make the best use of the available system.

The following texts (but not limited to) on the web page can be localized:

1. Labels
2. Messages: Alert messages, success messages, validation messages and other notifications etc.
3. Help Texts

{% hint style="info" %}
The module-specific master data would already have been made available in the localized form while collecting the data for the respective module-specific configuration.
{% endhint %}

### Data Table

| Sr. No. | Code\*                    | Module\*      | Message (In English)\* | Message (In Local Language)\* |
| ------- | ------------------------- | ------------- | ---------------------- | ----------------------------- |
| 1       | ACTION\_TEXT\_APPLICATION | Trade License | Search Trade Licenses  | व्यापार लाइसेंस खोजें         |
| 2       | ACTION\_TEST\_TL\_REPORTS | Trade License | Trade License Reports  | ट्रेड लाइसेंस रिपोर्ट         |
| 3       | CORE\_COMMON\_CITY        | Property Tax  | City                   | शहर                           |

{% hint style="info" %}
Data mentioned in the data table is a sample data.
{% endhint %}

### Procedure

#### Data Definition

| Sr. No. | Column Name                | Data Type    | Data Size | Is Mandatory? | Description                                                          |
| ------- | -------------------------- | ------------ | --------- | ------------- | -------------------------------------------------------------------- |
| 1       | Code                       | Alphanumeric | 64        | Yes           | The code for which the localized language is to be provided          |
| 2       | Module                     | Alphanumeric | 64        | Yes           | The module in which the code belongs to                              |
| 3       | Message(In English)        | Text         | 256       | Yes           | The English language that is being displayed on the UI               |
| 4       | Message(In Local Language) | Text         | 256       | Yes           | The text in the local language that the client wants to be displayed |

#### Steps to fill Data

1. Download the data template attached to this page.
2. Get a good understanding of all the headers in the template sheet, their data type, size, and definitions by referring to the ‘Data Definition’ section of this document.
3. In case of any doubt, please reach out to the person who has shared this template with you to discuss and clear your doubts.
4. Present the client the full sheet of codes as well as the English language for which the localized texts are required.
5. Ask the client to fill the localized text in the last column which is the message(local language) column.
6. Verify the data once again by going through the checklist and making sure that each and every point mentioned in the checklist is covered.

### Checklist

This checklist covers all the activities which are common across the entities.

| Sr. No. | Checklist Parameter                                                               | Example                                                    |
| ------- | --------------------------------------------------------------------------------- | ---------------------------------------------------------- |
| 1       | Make sure that each and every point in this reference list has been taken care of | [Checklist](../../module-setup/common-config/checklist.md) |

#### Entity Specific Checklist

Not Applicable

### Attachments

{% file src="../../../../.gitbook/assets/configurable-data-template-localization-v1.xlsx" %}
Configuration Data Template
{% endfile %}

{% file src="../../../../.gitbook/assets/configurable-sample-data-localization-v1.xlsx" %}
Sample Data Template
{% endfile %}

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)​](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation](https://egov.org.in/) is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).
