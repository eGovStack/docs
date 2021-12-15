---
description: WhatsApp channel v2 release details
---

# WhatsApp Channel Release Notes

## Overview

This release leverages the capabilities of WhatsApp as an additional channel for citizens to access/ pay bills for revenue modules like property tax and water/sewerage. With the improved user experience in terms of messaging and overall application flow, WhatsApp (V2) aims to strengthen the ease of service access for citizens at the last mile.

## Release Highlights

**Improvements in Public Grievance Redressal Module**

* Enhancements in messaging language.
* NLP Inclusion (For City & Boundary Selection).

**Improvements in Bill Payments**

* Enhancements in messaging language.
  * Inclusion of call to action buttons (for certain messages).
* For Linked Mobile Numbers
  * Single-click access to bills (for PT and W\&S)
* For Non-Linked Mobile Numbers
  * Provision of Search & Pay (If Property/Connection Details are known).
  * Inclusion of Open Search Links (If Property/ Connection Details are unknown).

**Improvements in Payment History**

* Enhancements in messaging language and flow.
  * Inclusion of call to action buttons (for certain messages).
* For Linked Mobile Numbers
  * Access to view the last three payments made (for PT & W\&S)
  * Provision to download the last three payment receipts
* For Non-Linked Mobile Numbers
  * Access control to view payments history only.

## Release Features

|                                                                                 |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| ------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Key Feature**                                                                 | **Description**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| Call to action (CTA) Buttons                                                    | <p>Call to action buttons (CTA) is an interactive message template that aims to provide an improved conversational experience. For WhatsApp V2, certain endpoints have called to action buttons included.</p><p>Instead of citizens typing for a reply, CTA buttons allow citizens to select the option and perform action instantly. The CTAs are applicable to the following scenarios :</p><ul><li>Pay Bills.</li><li>Return to Main Menu.</li><li>View Payment Receipts.</li></ul>                                                                                                                                                              |
| <p>Provision For Search &#x26; Pay Bills.</p><p>(Non-Linked Mobile Numbers)</p> | <p>As part of the WhatsApp V2, citizens :</p><ol><li>whose mobile numbers are not linked with DIGIT.</li><li>are aware of the account details (PT ID/ Connection No).</li></ol><p>can now search and pay the outstanding bills.</p><p>This feature encourages citizens to have access to outstanding bills on DIGIT even if the mobile number is not registered on the platform.</p>                                                                                                                                                                                                                                                                |
| Inclusion of Open Search Links                                                  | <p>As part of the WhatsApp V2, citizens :</p><ol><li>whose mobile numbers are not linked with DIGIT</li><li>not aware of the account details (PT ID/ Connection No)</li></ol><p>can now use the open search and pay the outstanding bills.</p><p>The open search allows citizens to fetch outstanding bills using other parameters (like door no/ name etc). In this case, the citizens will be redirected to the open search webpage and all the further interactions are exclusive of WhatsApp Chatbot.</p><p>This feature encourages citizens to have an access gateway to pay outstanding bills even when the required details are unknown.</p> |
| View Payment History                                                            | <p>View Payment History feature allows citizens to view the last three payments made for revenue service.</p><p>Further, in order to comply with data privacy :</p><ul><li>Only linked mobile numbers are allowed to download the past payment receipts.</li><li>Non-Linked Mobile numbers cannot access the receipts and only have provision to view payments history.</li></ul>                                                                                                                                                                                                                                                                   |
| NLP Inclusion                                                                   | <p>As part of the WhatsApp V2, citizens can now type and submit the :</p><ul><li>City Name</li><li>Locality Details</li></ul><p>while filing a complaint on PGR.</p><p>This feature is a major enhancement to the older version as now citizens don't have to be redirected outside the chatbot to select details.</p><p>Instead, citizens can now type and submit the information. Even when the information entered is incorrect, the NLP engine provides a suggestion for citizens to make corrections and proceed.</p>                                                                                                                          |

## Limitations

As an **external independent** environment, WhatsApp has the following limitations (applicable for current and future initiatives) :

|                                             |                                                                                                                                                                                                                                                                                                                                                      |
| ------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Limitation**                              | **Description**                                                                                                                                                                                                                                                                                                                                      |
| Access Control On Template Messages         | <ul><li>Only messages that <strong>are approved by WhatsApp</strong> can be part of the chatbot.</li><li>Post-approval only, internal development/ configuration can take place.</li></ul>                                                                                                                                                           |
| No Alteration/External Development Allowed. | <ul><li>WhatsApp <strong>does not allow the alteration</strong> such as chat inbox or message pad.</li></ul>                                                                                                                                                                                                                                         |
| **Access control** over the User Experience | <ul><li><p>We cannot control UX Aspects such as :</p><ul><li>Messaging Alignment (Auto-adjusted by WhatsApp as per Device).</li><li>Resolution Adjustment (Image &#x26; Multimedia Files).</li><li>Font Size &#x26; Style.</li><li>Message Character Length.</li><li>Message Delivery Speed (Not Fully)</li><li>Message Ordering</li></ul></li></ul> |

## Upcoming Release Features

* Water & Sewerage Open Search Infographic (For New UI).
* Integrate common pay new UI.
* DIGIT Platform Enhancements
  * Update a non linked mobile number as an alternate number (post payments).
  * Access control on payment recipients (owner vs others).

> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_ ](https://egov.org.in)_is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
