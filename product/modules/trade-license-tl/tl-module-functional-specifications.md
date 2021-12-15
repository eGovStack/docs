---
description: Functional overview for stakeholders
---

# TL Module Functional Specifications

## Introduction

The Trade License product provides a digital interface, allowing citizens to apply for the Trade License and subsequently make the trade license fee payment online.

The Trade License product enables:

* Ease of doing business — Traders can apply for new licenses, renewals, amendments, and supplemental licenses
* Regulatory Tracking — Administrators can track and manage regulatory processes
* Shorter Timelines — It streamlines and automates business licensing processes and helps a business to be set up quickly
* Data-driven decision making — The application collates valuable information on the economic activity and employment opportunities in a ULB

## Functional Scope

The list below summarizes the key features supported by the TL module -

1. Registration, Login and Creation of User Profile
2. Applying for a Trade License
3. Trade License Issue
4. Modifications to a Trade License
5. Renewal of Trade License
6. Payments and Fee
7. Dashboards and Reports
8. General Features

### Registration, Login and Creation of User Profile

{% hint style="warning" %}
Key capabilities offered by this functional component -

* OTP Based Login for Citizen via Web/Mobile App
* OTP Based Login for Employee via Web/Mobile App
* Provision for language selection during first time registration for both Employee and citizens
* Provision of creating a personalized Profile for Citizens and employees on Web App
* Login Credentials for the various hierarchies of employees
* Role-based access for performing different actions relating to Trade License modules
{% endhint %}

### Applying for a Trade License

User can apply for a new TL from the system. User can select the type of license to apply. The user enters trade details, owner details and documents after which application can be reviewed and submitted. Similarly, a counter employee can also apply for TL on behalf of the citizen. The system has a workflow integration which enables stage-wise approval before Approval for issuing the Trade License.

{% hint style="warning" %}
Key capabilities offered by this functional component -

* Citizen can Apply for a new Trade License through mobile app/ Web
* Citizen/CSC can capture Trade details, Trade Units, Accessories, Owner Details, Address, purpose, Date of issuance, License number etc.
* Citizen/CSC Upload Documents
* Citizen/CSC can calculate Breakup Based on Selected Trade
* Citizen/CSC can select Multiple Accessories for the Trade
* Citizen/CSC can Apply for Multiple Trade Licenses
* Citizen/CSC can Download/Print Application Summary
* Citizen/CSC can Download/Print Trade Reference No
* Citizen/CSC can View the applied licenses
* The system has the facility to deliver the service online & through SEWA KENDRA.
* The portal displays all the information including the processes and documents required for the convenience of the citizen.
* The system has the facility to assign a unique identification number based on the license type, which will be used for all future transactions of the license.
{% endhint %}

### Trade License Issue

The system has the facility to assign the application to the respective Inspector for survey and verification. After the application is submitted, it goes to the document verifier. The next step after document verification is field inspection. After the field inspector’s approval, the TL is approved by the approver.

{% hint style="warning" %}
Key capabilities offered by this functional component -

* Document Verifier, Verifies & Forwards or Rejects the application
* Licensing Inspector, Verifies and Forward the Application
* Licensing Inspector, Sends Back or Rejects the Application
* Licensing Inspectors Approves the Application
* Citizen, Pays for the license post verification process online or at the CSC
* CSC, Collects Fee post verification.
* The system allows the printing of license and sending the license through e-mail.
* The system allows the SMS alerts to the applicant regarding the date of inspection/visit by the inspector, approval/rejection of the application.
* The system allows the inspector to enter the field visit details and a field visit report is generated and automatically routed to the superintendent.
{% endhint %}

### Modifications to a Trade License

The system has the facility to edit/update the Application based on the Inspection report against the application.

### Renewal of a Trade License

The system has the facility to provide a hassle-free renewal process for citizen and employee ease, leading to increased revenues, by reducing unlicensed trades. The system allows sending of SMS and Email notifications and reminders based on the renewal cycle.

### Payment and Fee

{% hint style="warning" %}
Key capabilities offered by this functional component -

* The citizen can pay for the license post verification process
* CSC, Collects Fee post verification.
* The system allows intimating the applicant about the payment of the license fee through SMS/ e-Mail.
* The system allows the Generation of receipt for the payment
* The payment modes enabled are Card(offline), cash, cheque, DD
{% endhint %}

### Dashboards and Reports

{% hint style="warning" %}
Following reports offered by the module -

* Cancelled Receipt Register Report
* TL Collection
* TL Application Status- showing the number of licenses approved/rejected.
* TL ULB Wise Status
* State Dashboard: View Reports for Total Licenses, Licenses Issued, Payment Collected, Payment Distribution
{% endhint %}

### General Features

{% hint style="warning" %}
**Notifications -** The system has the capability to send notifications to citizens. These notifications can be sent for various steps like - verification completion, payment reminder, payment confirmation. These notifications can be sent in the language chosen by the ULB through all channels - SMS, Whatsapp, Email.

**Configurable Masters** - The system provides the following masters that can be configured as per the State’s requirements:

* Charges & Calculation : Calculation Engine, Rebate, Penalty,
* Rate Master
* State Masters: Trade Ontology, Documents List, Accessories, Ownership, Employee Data Mapping, Boundary Data Mapping, Fee Matrix (License Fees)
{% endhint %}

System specification in compliance with the Ease of Doing Business (EODB) BRAP 2019

|            |                 |                   |                                                                                                                                                                                                                                                                                                                                                                                                                                        |                                 |
| ---------- | --------------- | ----------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------- |
| Reform No. | Reform Area     | Weightage (score) | Recommendation                                                                                                                                                                                                                                                                                                                                                                                                                         | <p>Remarks<br></p>              |
| 80         | Sector Specific | 2                 | <p>Implement an online application system with the following features:</p><p>i. Online submission of application without the need to submit physical copy of application</p><p>ii. Eliminate physical touchpoint for document submission</p><p>iii. Allow option of online payment of application fee</p><p>iv. Allow applicant to track status of application online</p><p>v. Applicant can download the final certificate online</p> | Already available in the system |

### List of Features- Trade License

| List of Functionalities                                                                                    | Corresponding Features                                                               |
| ---------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------ |
| Registration, Login, Creation of User Profile                                                              | Provision for Language Selection during first-time registration via Mobile/ Web App. |
| OTP Based Login for Citizen/ Employee via Mobile/ Web App                                                  |                                                                                      |
| Login Credentials for the various hierarchy of employees                                                   |                                                                                      |
| Provision of Personalized Profile for Citizen/ Employee on Web App                                         |                                                                                      |
| Applying for a Trade License                                                                               | Citizen/CSC: Enters Trade Details, Trade Units, Accessories, Owner Details.          |
| Citizen/CSC: Upload Documents                                                                              |                                                                                      |
| Citizen/CSC: ULB Wise Trade Selection                                                                      |                                                                                      |
| Citizen/CSC: Calculation Breakup Based on Selected Trade                                                   |                                                                                      |
| Citizen/CSC: Multiple Accessories Field Count                                                              |                                                                                      |
| Citizen/CSC: Multiple Trade License.                                                                       |                                                                                      |
| Citizen/CSC: Download/Print Application Summary                                                            |                                                                                      |
| Citizen/CSC: Download/PRINT Trade Reference No                                                             |                                                                                      |
| Citizen/CSC: View the applied licenses.                                                                    |                                                                                      |
| Citizen: Pays for the license post verification process.                                                   |                                                                                      |
| CSC: Collects Fee post verification.                                                                       |                                                                                      |
| Trade Licence Issue                                                                                        | Document Verifier : Verify & Forward/ Reject the application                         |
| Licensing Inspector: Verify and Forward/ Send back/ Reject the Application.                                |                                                                                      |
| Licensing Officer: Approve/ Send back the Application                                                      |                                                                                      |
| Licensing Officer: Reject/ Cancel the Application                                                          |                                                                                      |
| Modification to a Trade License                                                                            | Edit/ Update the Application based on the Inspection report against the application. |
| Renewal of a Trade Licence                                                                                 | Renew trade license.                                                                 |
| Payment and Fee                                                                                            | Configurable Workflow Rights : Edit & Payment Collection                             |
| Payments & Collection : Various Payment Modes                                                              |                                                                                      |
| Dashboards and reports                                                                                     | Cancelled Receipt Register Report                                                    |
| TL Collection                                                                                              |                                                                                      |
| TL Application Status- showing the number of licenses approved/rejected.                                   |                                                                                      |
| TL ULB Wise Status                                                                                         |                                                                                      |
| State Dashboard: View Reports for Total Licenses, Licenses Issued, Payment Collected, Payment Distribution |                                                                                      |
| General features                                                                                           | Notifications : SMS Notifications                                                    |
| Charges & Calculation : Calculation Engine                                                                 |                                                                                      |
| Charges & Calculation : Rebate/ Penalty- Date Based                                                        |                                                                                      |
| Charges & Calculation : Ad-Hoc Rebate/ Penalty                                                             |                                                                                      |
| Charges & Calculation : Exemptions Trade Type & Owner Type                                                 |                                                                                      |
| Configuration masters                                                                                      | Configurable Workflow Rights : Edit & Payment Collection                             |
| Configurable Verification & Approval                                                                       |                                                                                      |

> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)_​_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
