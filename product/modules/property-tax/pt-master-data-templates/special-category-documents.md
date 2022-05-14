# Special Category Documents

## Introduction <a href="#introduction" id="introduction"></a>

In order to justify the Property [Owner’s Special Category](owner-special-category.md) status, there are certain supporting documents that are required as the attachment of proof. These documents are crucial in terms of providing/ availing rebate on the property tax amount.

## Data Definition <a href="#data-definition" id="data-definition"></a>

| Sr. No. | Owner Type Code\* | Ownership Documents Description (English)\*      | Ownership Documents Description (Local Language)\* |
| ------- | ----------------- | ------------------------------------------------ | -------------------------------------------------- |
| 1       | FREEDOMFIGHTER    | Certificate issued by DC/ Competent Authority    | डीसी / सक्षम प्राधिकारी द्वारा जारी प्रमाण पत्र    |
| 2       | WIDOW             | Death Certificate + Spouse proof                 | डेथ सर्टिफ़िकेट + जीवनसाथी प्रमाण                  |
| 3       | HANDICAPPED       | Certificate of Handicap by a competent authority | सक्षम प्राधिकारी द्वारा विकलांग का प्रमाण पत्र     |

The data given in the table is sample data.

## Procedure <a href="#procedure" id="procedure"></a>

| Sr. No. | Column Name                                        | Data Type | Data Size | Mandatory | Description                                                                                                                                                  |
| ------- | -------------------------------------------------- | --------- | --------- | --------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 1       | Owner Type Code                                    | Reference | 64        | Yes       | Unique Identifier assigned for the [Owner Type](ownership-category.md). For example, Freedom Fighter is represented as FREEDOMFIGHTER                        |
| 2       | Ownership Documents Description (English)          | Text      | 256       | Yes       | Nomenclature of “Owner Documents” in English. For ownership type Freedom Fighter, the document required is the certificate issued by DC/ Competent Authority |
| 3       | Ownership Documents Description (Local Language)\* | Text      | 256       | Yes       | Nomenclature of “Owner Documents” in Hindi                                                                                                                   |

### How to fill data <a href="#how-to-fill-data" id="how-to-fill-data"></a>

1. Download the data template attached to this page.
2. Get a good understanding of all the headers in the template sheet, their data type, size, and definitions by referring to the ‘Data Definition’ section of this document.
3. In case of any doubt, please reach out to the person who has shared this template with you to discuss and clear your doubts.
4. Identify the “Owner Categories” that exists at a ULB/ State level.
5. Add the “Owner Type Code” respectively. The predefined format of the Owner Type Code only must be used from the “[Owner Special Category](owner-special-category.md)” Master Sheet and not any random code. This will provide the base reference for the mapping of ownership type with the required documents.

## Checklist <a href="#checklist" id="checklist"></a>

The checklist is a set of activities to be performed once the data is filled into a template to ensure data type, size, and format of data is as per the expectation. These activities have been divided into 2 groups as given below.

### Common Checklist <a href="#common-checklist" id="common-checklist"></a>

This checklist covers all the activities which are common across the entities.

| Sr. No. | Checklist Parameter                                                               | Example                                                                                                                      |
| ------- | --------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| 1       | Make sure that each and every point in this reference list has been taken care of | ​[Checklist](https://docs.digit.org/configure-digit/configuring-master-data-templates/module-setup/common-config/checklist)​ |

### Entity Specific Checklist <a href="#entity-specific-checklist" id="entity-specific-checklist"></a>

This checklist covers the activities which are specific to the entity.

| Sr. No. | Checklist Parameter                                       | Example                                               |
| ------- | --------------------------------------------------------- | ----------------------------------------------------- |
| 1       | The format of the Owner Type Code defined should be Text  | War Widow is represented as WIDOW                     |
| 2       | Owner Type Code should not contain any special characters | <p>WIDOW: [Allowed]</p><p>#WIDOW! : [Not allowed]</p> |

## Attachments <a href="#attachments" id="attachments"></a>

[Configuration Data Templateconfiguration-data-template-pt-master-3- (1).xlsx - 10KB](https://firebasestorage.googleapis.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-MERG\_iQW5oN4ukgXP8K%2Fsync%2Faf47c79c944c953aed463cd5067940fc54d68630.xlsx?generation=1602050605757319\&alt=media)

[Sample Dataconfiguration-sample-data-pt-master-3-.xlsx - 15KB](https://firebasestorage.googleapis.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-MERG\_iQW5oN4ukgXP8K%2Fsync%2Fd22df176b956ad1f9ae35b34ad36e9e12fd6db38.xlsx?generation=1602050605800117\&alt=media)

> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_ ](https://egov.org.in/)_is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
