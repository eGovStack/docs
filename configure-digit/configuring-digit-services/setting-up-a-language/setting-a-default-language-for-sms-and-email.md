# Setting Up Default Language For SMS & Emails

## Overview

SMS and Email communicate the necessary information/updates to the users regarding the multiple transactions on DIGIT applications.\
For example, when a Trade License application is initiated or forwarded or approved or payment is done in the DIGIT system, the applicant and payer (if the payer is other than the applicant) are informed about the status of the Trade License application through SMS/Email.\
The language for SMS and Email can be set as per requirement/choice.

## Pre-requisites

Before proceeding with the configuration, make sure the following pre-requisites are met -

* Knowledge of DIGIT applications is required.
* User should be aware of transactional steps in the DIGIT application.

## Key Functionalities

* Users can receive Emails and SMS with necessary information/updates in the decided language.
* The language can be decided by the end-users (citizens or employees). End-users can select the language before logging in or after logging in from the inbox page.
* If the language is not chosen by the end-user, then SMS/Email is received in the language of, State requirement-based state-level configured language.

## Configuration Details

Sms and Email localization are pushed to the database through the endpoints for all the languages added to the system.\
**Localization format for SMS/Email**

```
{
     "code": "unique key referred for sms or email",
     "message": "sms value or email to be received",
     "module": "rainmaker-<modulename>",
     "locale": "<language key>"
  }
```

**Sample of SMS localisation for Trade License application initiation**\
**English localization**

```
{
  "code": "tl.en.counter.initiate",
  "message": "Dear <1>, Your Trade License application number for <2> has been generated. Your application no. is <3> You can use this application number to know your application status. Thank You. NagarSewa.",
  "module": "rainmaker-tl",
  "locale": "en_IN"
}
```

**Hindi localization**

```
{
  "code": "tl.en.counter.initiate",
  "message": "प्रिय <1>, <2> के व्यापार लाइसेंस के आवेदन के लिए आपका व्यापार लाइसेंस आवेदन संख्या <3> है। आप इस आवेदन संख्या का उपयोग अपनी आवेदन स्थिति जानने के लिए कर सकते हैं। धन्यवाद। नगरसेवा।",
  "module": "rainmaker-tl",
  "locale": "hi_IN"
}
```

{% hint style="info" %}
The placeholder <1>,<2>,<3> are replaced by the actual required value which gives important information to the applicant.\
For example\*\*,\*\* the message will be received by the applicant as:\
Dear Kamal, Your Trade License application number for Ramjhula Provisional Store has been generated. Your application no. is UK-TL-2020-07-10-002058 You can use this application number….
{% endhint %}

The default language for SMS and Email can be set by

* Clicking on the preferred language from the available language button, on the language selection page, which opens before the login page.
* On the citizen or employee inbox page, the language can be selected from the drop-down, available in the right corner of the inbox title bar.
* If the language is not chosen by the citizen or employee, then SMS/Email is received in the default configured language. For example, Hindi, English and Kannada are added as three languages in the system for a specific state. In case the state decides that out of these three languages, Kannada should be configured as the default language. In such case Kannada is set as the default language in the MDMS. So when the end-user does not choose any language then SMS/Email is sent in the Kannada language.

The selected language key is sent as a parameter along with other required transaction parameters to the back-end code.

In the back end, to send SMS/Email logic, the language key is checked and based on the language key and SMS unique key, the message is fetched from the database.



[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)​](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation](https://egov.org.in/) is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).
