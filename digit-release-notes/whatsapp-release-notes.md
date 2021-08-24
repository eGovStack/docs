---
description: WhatsApp channel v2 release details
---

# WhatsApp Channel Release Notes

<<<<<<< HEAD
### Overview <a id="Overview"></a>

This release leverages the capabilities of WhatsApp as an additional channel for citizens to view bills/ make payments for a particular module service. Extended capabilities include improvements in the Public Grievance Redressal module and localization support to assist ease of use.

### Release Highlights <a id="Release-Highlights"></a>

1. **Search and View Bill \`**
   1. View my Bills
   2. Search Bills Based on 
      1. Consumer Number
      2. Application Number
      3. Mobile Number etc
   3. View Bill
      1. Amount Due
      2. Bill copy \(PDF\) 
2. **Payment** 
   1. Pay bills through quick payment links
   2. Payment confirmation/failure notification
   3. Payment receipt \(PDF\)  on successful payment
3. **Multi-Language Support**
   1. Hindi Localization \(For Chats\)
4. **Improvements in Public Grievance Redressal Module**
   1. Two-Step Complaint List \(By Type & Subtype\)
   2. Geo-Location Tagging

### Release Features <a id="Release-Features"></a>
=======
## Overview

This release leverages the capabilities of WhatsApp as an additional channel for citizens to access/ pay bills for revenue modules like property tax and water/sewerage. With the improved user experience in terms of messaging and overall application flow, WhatsApp \(V2\) aims to strengthen the ease of service access for citizens at the last mile.

## Release Highlights

**Improvements in Public Grievance Redressal Module**

* Enhancements in messaging language.
* NLP Inclusion \(For City & Boundary Selection\).

**Improvements in Bill Payments**

* Enhancements in messaging language.
  * Inclusion of call to action buttons \(for certain messages\).
* For Linked Mobile Numbers
  * Single-click access to bills \(for PT and W&S\)
* For Non-Linked Mobile Numbers
  * Provision of Search & Pay \(If Property/Connection Details are known\).
  * Inclusion of Open Search Links \(If Property/ Connection Details are unknown\).

 **Improvements in Payment History**

* Enhancements in messaging language and flow.
  * Inclusion of call to action buttons \(for certain messages\).
* For Linked Mobile Numbers
  * Access to view the last three payments made \(for PT & W&S\)
  * Provision to download the last three payment receipts
* For Non-Linked Mobile Numbers
  * Access control to view payments history only.

## Release Features
>>>>>>> 64dca8adbdf64336b1a8203199b3791fa23434fa

<table>
  <thead>
    <tr>
      <th style="text-align:left"><b>Key Feature</b>
      </th>
      <th style="text-align:left"><b>Description</b>
      </th>
    </tr>
  </thead>
  <tbody>
    <tr>
<<<<<<< HEAD
      <td style="text-align:left">Selection of Desired Service</td>
      <td style="text-align:left">
        <p></p>
        <p>Allows Citizen to select the following via WhatsApp Chat :</p>
        <ul>
          <li>File Complaint</li>
          <li>Track Complaint</li>
          <li>Pay Bills and Fees</li>
          <li>View Payments Receipts</li>
          <li>Change Language</li>
=======
      <td style="text-align:left">Call to action (CTA) Buttons</td>
      <td style="text-align:left">
        <p>Call to action buttons (CTA) is an interactive message template that aims
          to provide an improved conversational experience. For WhatsApp V2, certain
          endpoints have called to action buttons included.</p>
        <p>Instead of citizens typing for a reply, CTA buttons allow citizens to
          select the option and perform action instantly. The CTAs are applicable
          to the following scenarios :</p>
        <ul>
          <li>Pay Bills.</li>
          <li>Return to Main Menu.</li>
          <li>View Payment Receipts.</li>
>>>>>>> 64dca8adbdf64336b1a8203199b3791fa23434fa
        </ul>
      </td>
    </tr>
    <tr>
<<<<<<< HEAD
      <td style="text-align:left">Pay Bills &amp; Fees</td>
      <td style="text-align:left">
        <p></p>
        <p>Allows Citizen to view the current outstanding bills with respect to applicable
          the modules, where his/ her mobile number is linked. The following information
          is displayed in the message :</p>
        <ul>
          <li>Module Name</li>
          <li>Amount to be paid</li>
          <li>Due Date</li>
          <li>Payment Link</li>
=======
      <td style="text-align:left">
        <p>Provision For Search &amp; Pay Bills.</p>
        <p>(Non-Linked Mobile Numbers)</p>
      </td>
      <td style="text-align:left">
        <p>As part of the WhatsApp V2, citizens :</p>
        <ol>
          <li>whose mobile numbers are not linked with DIGIT.</li>
          <li>are aware of the account details (PT ID/ Connection No).</li>
        </ol>
        <p>can now search and pay the outstanding bills.</p>
        <p>This feature encourages citizens to have access to outstanding bills on
          DIGIT even if the mobile number is not registered on the platform.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Inclusion of Open Search Links</td>
      <td style="text-align:left">
        <p>As part of the WhatsApp V2, citizens :</p>
        <ol>
          <li>whose mobile numbers are not linked with DIGIT</li>
          <li>not aware of the account details (PT ID/ Connection No)</li>
        </ol>
        <p>can now use the open search and pay the outstanding bills.</p>
        <p>The open search allows citizens to fetch outstanding bills using other
          parameters (like door no/ name etc). In this case, the citizens will be
          redirected to the open search webpage and all the further interactions
          are exclusive of WhatsApp Chatbot.</p>
        <p>This feature encourages citizens to have an access gateway to pay outstanding
          bills even when the required details are unknown.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">View Payment History</td>
      <td style="text-align:left">
        <p>View Payment History feature allows citizens to view the last three payments
          made for revenue service.</p>
        <p>Further, in order to comply with data privacy :</p>
        <ul>
          <li>Only linked mobile numbers are allowed to download the past payment receipts.</li>
          <li>Non-Linked Mobile numbers cannot access the receipts and only have provision
            to view payments history.</li>
>>>>>>> 64dca8adbdf64336b1a8203199b3791fa23434fa
        </ul>
      </td>
    </tr>
    <tr>
<<<<<<< HEAD
      <td style="text-align:left">View Payment Receipts</td>
      <td style="text-align:left">
        <p></p>
        <p>Allows Citizens to view past payment receipts with respect to applicable
          modules, linked with the current mobile number. In case, the current mobile
          number is not linked with the module, still citizen can proceed to search
          for the receipts via the following :</p>
        <ul>
          <li>Registered Mobile Number</li>
          <li>Module Specific ID (Property ID/ Water Connection ID etc)</li>
          <li>Consumer Number</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Two-Step Complaint List (By Type &amp; Subtype)</td>
      <td style="text-align:left">Allows Citizens to now browse complaints by Complaint Type (The Master
        List) and select the relevant subtype</td>
    </tr>
    <tr>
      <td style="text-align:left">Geo-Location Tagging</td>
      <td style="text-align:left">Allows Citizens to add the location of the grievance site via WhatsApp
        while lodging the complaint</td>
    </tr>
    <tr>
      <td style="text-align:left">Change Language</td>
      <td style="text-align:left">Allows Citizens to change the language of chat from English to Hindi and
        vice versa</td>
=======
      <td style="text-align:left">NLP Inclusion</td>
      <td style="text-align:left">
        <p>As part of the WhatsApp V2, citizens can now type and submit the :</p>
        <ul>
          <li>City Name</li>
          <li>Locality Details</li>
        </ul>
        <p>while filing a complaint on PGR.</p>
        <p>This feature is a major enhancement to the older version as now citizens
          don&apos;t have to be redirected outside the chatbot to select details.</p>
        <p>Instead, citizens can now type and submit the information. Even when the
          information entered is incorrect, the NLP engine provides a suggestion
          for citizens to make corrections and proceed.</p>
      </td>
    </tr>
  </tbody>
</table>

## Limitations

As an **external independent** environment, WhatsApp has the following limitations \(applicable for current and future initiatives\) : 

<table>
  <thead>
    <tr>
      <th style="text-align:left"><b>Limitation</b>
      </th>
      <th style="text-align:left"><b>Description</b>
      </th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Access Control On Template Messages</td>
      <td style="text-align:left">
        <ul>
          <li>Only messages that <b>are approved by WhatsApp</b> can be part of the chatbot.</li>
          <li>Post-approval only, internal development/ configuration can take place.</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">No Alteration/External Development Allowed.</td>
      <td style="text-align:left">
        <ul>
          <li>WhatsApp <b>does not allow the alteration</b> such as chat inbox or message
            pad.</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Access control</b> over the User Experience</td>
      <td style="text-align:left">
        <ul>
          <li>We cannot control UX Aspects such as :
            <ul>
              <li>Messaging Alignment (Auto-adjusted by WhatsApp as per Device).</li>
              <li>Resolution Adjustment (Image &amp; Multimedia Files).</li>
              <li>Font Size &amp; Style.</li>
              <li>Message Character Length.</li>
              <li>Message Delivery Speed (Not Fully)</li>
              <li>Message Ordering</li>
            </ul>
          </li>
        </ul>
      </td>
>>>>>>> 64dca8adbdf64336b1a8203199b3791fa23434fa
    </tr>
  </tbody>
</table>

<<<<<<< HEAD
### Known Issues <a id="Known-Issues"></a>

Emojis are not supported as the input for chat responses

### Upcoming Release Features <a id="Upcoming-Release-Features"></a>

* Improvement in Messaging Language & Flow
* NLP Inclusion \(For City & Locality Selection\)
* Referral, Rating & Help Mechanism
* Privacy Enhancements

### Reference Doc Links <a id="Reference-Doc-Links"></a>

| **Doc Links** | **Description** |
| :--- | :--- |
|  |  |
=======
## Upcoming Release Features

* Water & Sewerage Open Search Infographic \(For New UI\).
* Integrate common pay new UI.
* DIGIT Platform Enhancements
  * Update a non linked mobile number as an alternate number \(post payments\).
  * Access control on payment recipients \(owner vs others\).
>>>>>>> 64dca8adbdf64336b1a8203199b3791fa23434fa

 



> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_ ](https://egov.org.in/)_is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._

