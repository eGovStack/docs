# Adding New Language

### Overview

Digit system supports multiple languages.  
To add a new language, it should be configured in MDMS.

### Pre-requisites

Before proceeding with the configuration, following are the pre-requisites -

* Knowledge of json and how to write a json is required.
* Knowledge of MDMS is required.
* User with permissions to edit the git repository where MDMS data is configured.

### Key Functionalities

* Users can view the web page of digit application in the language of their choice by selecting it from the available languages.
* SMS and Emails of information about the transactions on digit application, can be received in languages based on the selection.

### Deployment Details

After adding the new language, the MDMS service needs to be restarted to read the newly added data.

### Configuration Details

A new language is added in StateInfo.json  
In MDMS, file **StateInfo.json**, under **common-masters** folder holds the details of language to be added.

```text
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
The label’s text is displayed in UI for language selection.  
The value text is used as key to refer the language.
{% endhint %}

Language is added as an array element under the array named “languages”. Each language element is a label and value pair. By default English language is added. Other languages can be added as an additional/new language which system will support. System to support multiple ie., more than one language, those languages are added in StateInfo.json as below.

```text
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
"हिंदी" and "ಕನ್ನಡ",”language3” are more than one languages\(Hindi,Kannada,somelangauge\) added other than "ENGLISH".
{% endhint %}

In UI the labels and master values that populates in dropdown or textboxes are added as a key for localization. For eg., when a user logs in, at the top of inbox page, a welcome message in English language shows as “Welcome User name“. The text “Welcome” is English localization for the Key “CS\_LANDING\_PAGE\_WELCOME\_TEXT”.

For all the labels or master value keys, localization should be pushed to the database through the endpoints for all the languages added in system.The SMS/Email are also added as keys for which values are pushed in all the languages to the data base.

**Localization format for** **keys**

```text
{
  "code": "unique key referred ",
  "message": "Value to be shown in UI or send in SMS/Email",
  "module": "rainmaker-<modulename>",
  "locale": "<language key>"
}
```

**Sample of localization**

In Hindi language

```text
{
  "code": "CS_LANDING_PAGE_WELCOME_TEXT",
  "message": "आपका स्वागत है ",
  "module": "rainmaker-pgr",
  "locale": "hi_IN"
}
```

In English language

```text
{
  "code": "CS_LANDING_PAGE_WELCOME_TEXT",
  "message": "Welcome",
  "module": "rainmaker-pgr",
  "locale": "en_IN"
}
```

For the languages added in the system if values are not pushed to database then for the labels or master data, key will appear in UI. If values for SMS/Email is missed to pushed the SMS/Email can’t be received.

Any one language from the multiple added language, can be set as default. For example if English, Hindi, Kannada are three languages added in the StateInfo.json and kannada is required to be set as a default language then in StateInfo.json for the text "defaultLanguage" the language key is need to be set as its value.

```text
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

### Reference Docs

#### Doc Links

| **Title** | **Link** |
| :--- | :--- |
| StateInfo.json | [https://github.com/egovernments/ukd-mdms-data/blob/DEV/data/uk/common-masters/StateInfo.json](https://github.com/egovernments/ukd-mdms-data/blob/DEV/data/uk/common-masters/StateInfo.json) |

