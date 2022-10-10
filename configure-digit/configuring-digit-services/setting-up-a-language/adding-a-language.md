# Adding New Language

## Overview

The DIGIT system supports multiple languages.\
To add a new language, it should be configured in the MDMS.

## Pre-requisites

Before you proceed with the configuration, make sure the following pre-requisites are met -

* Knowledge of json and how to write a json is required.
* Knowledge of MDMS is required.
* User with permission to edit the git repository where MDMS data is configured.

## Key Functionalities

* Users can view the web page of the DIGIT application in the language of their choice by selecting it from the available languages.
* SMS and Emails of information about the transactions on the DIGIT application can be received in languages based on the selection.

## Deployment Details

After adding the new language, the MDMS service needs to be restarted to read the newly added data.

## Configuration Details

A new language is added in StateInfo.json\
In MDMS, the file **StateInfo.json**, under **common-masters** folder holds the details of the language to be added.

```
{
  "tenantId": "uk", //<ReplaceWithDesiredTenantId>
  "moduleName": "common-masters",
  "StateInfo": [
    {
      "languages": [
        {
          "label": "ENGLISH",  
          "value": "en_IN"   
        },
        {
          "label": "हिंदी",     // <ReplaceWithTheRequiredLanguageName>
          "value": "hi_IN"   // <ReplaceWithTheRequiredLanguageKey>
        }
      ]
    }
  ]
}
```

{% hint style="info" %}
The label’s text is displayed in UI for language selection.\
The value text is used as the key to refer to the language.
{% endhint %}

Language is added as an array element under the array named “languages”. Each language element is a label and value pair. By default English language is added. Other languages can be added as an additional/new language which the system will support. System to support multiple ie., more than one language, those languages are added in StateInfo.json as below.

```
"languages": [
        {
          "label": "ENGLISH",  
          "value": "en_IN"   
        },
        {
          "label": "हिंदी",     // <ReplaceWithTheRequiredLanguageName>
          "value": "hi_IN"   // <ReplaceWithTheRequiredLanguageKey>
        },
        {
          "label": "ಕನ್ನಡ", // <ReplaceWithTheRequiredLanguageName>
          "value": "kn_IN" <ReplaceWithTheRequiredLanguageKey>
        },
        {
          "label": "language3", // <ReplaceWithTheRequiredLanguageName>
          "value": "language3key" <ReplaceWithTheRequiredLanguageKey>
        }
      ]
```

{% hint style="info" %}
"हिंदी" and "ಕನ್ನಡ",”language3” are more than one language (Hindi, Kannada, some language) added other than "ENGLISH".
{% endhint %}

In UI the labels and master values that populate in dropdown or textboxes are added as a key for localization. For eg., when a user logs in, at the top of the inbox page, a welcome message in the English language shows as “Welcome User name“. The text “Welcome” in English localization for the Key “CS\_LANDING\_PAGE\_WELCOME\_TEXT”.

For all the labels or master value keys, localization should be pushed to the database through the endpoints for all the languages added to the system. The SMS/Email are also added as keys for which values are pushed in all the languages to the database.

**Localization format for** **keys**

```
{
  "code": "unique key referred ",
  "message": "Value to be shown in UI or send in SMS/Email",
  "module": "rainmaker-<modulename>",
  "locale": "<language key>"
}
```

**Sample of localization**

In the Hindi language

```
{
  "code": "CS_LANDING_PAGE_WELCOME_TEXT",
  "message": "आपका स्वागत है ",
  "module": "rainmaker-pgr",
  "locale": "hi_IN"
}
```

In the English language

```
{
  "code": "CS_LANDING_PAGE_WELCOME_TEXT",
  "message": "Welcome",
  "module": "rainmaker-pgr",
  "locale": "en_IN"
}
```

For the languages added in the system if values are not pushed to the database then for the labels or master data, the key will appear in UI. If values for SMS/Email are not pushed, the SMS/Email will not be received.

Any one language from the multiple added language can be set as default. For example, if English, Hindi and Kannada are three languages added in the StateInfo.json and Kannada has to be set as the default language. Set the language key in the text "defaultLanguage" in the StateInfo.json as the value.

```
{
  "tenantId": "uk",   //<ReplaceWithDesiredTenantId>
  "moduleName": "common-masters",
  "StateInfo": [
    {
      "defaultLanguage": "kn_IN",  //<ReplaceWithTheLanguageKey>
        "languages": [
        {
          "label": "ENGLISH",  
          "value": "en_IN"   
        },
        {
          "label": "हिंदी",     
          "value": "hi_IN"   
        },
        {
          "label": "ಕನ್ನಡ", // <ReplaceWithTheRequiredLanguageName>
          "value": "kn_IN" <ReplaceWithTheRequiredLanguageKey>
        }
      ]
    }
  ]
}
```

## Reference Docs

#### Doc Links

| Description    | Link                                                                                                                                                                                         |
| -------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| StateInfo.json | [https://github.com/egovernments/ukd-mdms-data/blob/DEV/data/uk/common-masters/StateInfo.json](https://github.com/egovernments/ukd-mdms-data/blob/DEV/data/uk/common-masters/StateInfo.json) |

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)​](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation](https://egov.org.in/) is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).
