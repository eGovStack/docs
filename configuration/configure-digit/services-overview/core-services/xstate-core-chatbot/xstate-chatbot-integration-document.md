# XState-Chatbot Integration Document

## Overview

[XState-Chatbot](https://github.com/egovernments/core-services/tree/xstate-chatbot/xstate-chatbot) is a revamped version of the [chatbot](https://github.com/egovernments/core-services/tree/master/chatbot), which provides functionality to the user to access PGR module services like file complaint, track complaint, notifications from whats app,  
It allows the user to view receipts and pay the bills for Property, Trade Licence, FireNOC, Water and Sewerage and BPA service module.

## Key Functionalities

* File PGR complaint
* Track PGR complaint
* Support images when filing complaints
* Notifications to citizen when an employee performs any action on the complaint
* Allow user to search and pay bills of different modules.
* Allow user to search and view receipts of different modules.
* Allow user to change the language of their choice to have a better experience.
* Put user interactions on an elastic search for Telemetry.

## Integration

#### Integration Scope <a id="Integration-Scope"></a>

XState chatbot can be integrated with any other module to improve the ease of search and view bills/past payment receipts and to improve speed and convenience for bill payment. It can be integrated with the PGR module for easiness of creation and tracking of the complaint.

### Integration Benefits

* Increase in convenience and ease of making the bill payment.
* Increase in no. of users opting for online payment.
* Improvement in demand collection efficiency
* Creating an additional channel for payment.
* Remove dependency on mobile/web app or counter.

### Integration Details <a id="Integration-Details"></a>

#### Integration of New Whatsapp Provider <a id="Integration-of-New-Whatsapp-Provider-:"></a>

Whatsapp provider is a third-party service that works in the middle of a user's WhatsApp client and  XState-Chatbot server. All messages coming/going to/from user pass through WhatsApp provider. Chatbot calls WhatsApp provider to send messages to the user. When a user responds with any WhatsApp message the WhatsApp provider calls Chatbot service’s configured endpoint with details ex:- user sent message, sender’s number etc.

 If any new WhatsApp provider is to be used with a chatbot, code must be written to convert the provider’s incoming messages to the format that the chatbot understands and also final output from the chatbot should be converted to WhatsApp provider’s API request format.

Currently, the XState-Chatbot service is using ValueFirst as the WhatsApp Provider. This will require provider-specific environment variable to be configured. If the provider changes then, all these environment variable will also change. Few of those environment variables are stored as secrets, so these values need to be configured in _env_-secrets.yaml.

As this is a revamped version of the chatbot service, all of the secrets should already be present. There is no need to create new secrets.

#### Integration of PGR complaint feature in XState-Chatbot <a id="Integration-of-PGR-complaint-feature-in-XState-Chatbot:"></a>

The integration of PGR with a chatbot can be enabled and disabled by making changes in this [file](https://github.com/egovernments/core-services/blob/xstate-chatbot/xstate-chatbot/nodejs/src/machine/service/service-loader.js).  
By exporting the respective PGR service file, the PGR service feature can be sable and vice versa.

**Configuration of PGR version in chatbot**

To configure the PGR module to use in Xstate-chatbot - the below variable values need to change in the [environment file](https://github.com/egovernments/eGov-infraOps/blob/master/helm/environments/qa.yaml#L207) as per the requirement.

* pgrVersion
* pgrUpdateTopic

To configure PGR v2 in XState chatbot then pgrVersion should be ‘v2' and pgrUpdateTopic should be 'update-pgr-request’.

**Adding Information Image in PGR complaint creation**

To configure the filestoreid for informational image follow the steps mention below

1. Download this [image](https://qa.digit.org/egov-dev-assets/Share_Location_Information_Image.png)
2. Upload the image into filestore server. Use the upload file API from this postman collection\([https://www.getpostman.com/collections/bdb059c5af698f0d81d6\)](https://www.getpostman.com/collections/bdb059c5af698f0d81d6)
3. Mention the filestore id [here](https://github.com/egovernments/eGov-infraOps/blob/master/helm/environments/qa.yaml#L209) in the environment file.

**Configuration of Compliant status template messages**

For Compliant status update notifications to citizen when an employee performs any action on the complaint.

Xstate chatbot is maintaining the template id of each message which gets triggered on the respective status or action performed on the complaint. The template ids are maintained in the [environment file](https://github.com/egovernments/eGov-infraOps/blob/master/helm/environments/qa.yaml#L198). For any new notification, its template id has to mention in the above file.

Each notification in a different language will have different template ids. For example, the complaint resolve notification in English will have template-id as ‘12345' and the same notification in Hindi will have template-id as ‘6789’. The order of mentioning the template id must be the same as the order of the supported locale mentioned in [env-variable.js file](https://github.com/egovernments/core-services/blob/xstate-chatbot/xstate-chatbot/nodejs/src/env-variables.js#L20).

**For example:**

a\) if supportedLocales: process.env.SUPPORTED\_LOCALES \|\| 'en\_IN,hi\_IN'

then valuefirst-notification-resolved-templateid: "12345,6789"

b\) if supportedLocales: process.env.SUPPORTED\_LOCALES \|\| 'hi\_IN,en\_IN'

then valuefirst-notification-resolved-templateid: "6789,12345"

{% hint style="info" %}
_\(Note: Both the list should not be empty, it must contain at least one element\)_
{% endhint %}

#### Integration of Bill Payment and Receipt Search feature in Xstate-Chatbot <a id="Integration-of-Bill-Payment-and-Receipt-Search-feature-in-Xstate-Chatbot:"></a>

The integration of the Bill payment and receipt search feature with a chatbot can be enabled and disabled by making changes in this [file](https://github.com/egovernments/core-services/blob/xstate-chatbot/xstate-chatbot/nodejs/src/machine/service/service-loader.js). By exporting the respective bill service and receipt service file, the payment and receipt search feature can be enabled and vice versa.  
  
**Configuration of module for Bill payment and Receipt search**

To configure the list of modules to appear as an option for payment and receipt, Add the module business service code in the list present in the [environment](https://github.com/egovernments/eGov-infraOps/blob/master/helm/environments/qa.yaml#L206) file.

**For example:**  
 If `bill-supported-modules: "WS, PT, TL`"  
 then Water and Sewerage, Property, Trade license module would appear for bill payment and  
 receipt search.

Also add the message bundle, validation and service code for locality searcher in [egov-bill](https://github.com/egovernments/core-services/blob/xstate-chatbot/xstate-chatbot/nodejs/src/machine/service/egov-bill.js) and [egov-receipt](https://github.com/egovernments/core-services/blob/xstate-chatbot/xstate-chatbot/nodejs/src/machine/service/egov-receipts.js) file.  
  
**Configuration of Xstate-Chatbot localisation message**

XState-Chatbot does not have any MDMS data, nor does it store any messages in localization-service. If any message needs to be modified, the changes will have to be made in the source code, then build the new docker image and deploy it.  
For Configuration details of the XState-chatbot localisation message please refer to the links in Reference Docs.  
  
The table below contains the details about some environment variables use in XState-Chatbot service which is present in this [file](https://github.com/egovernments/core-services/blob/xstate-chatbot/xstate-chatbot/nodejs/src/env-variables.js):

| **Environment Variables** | **Description** |
| :--- | :--- |
| WHATSAPP\_BUSINESS\_NUMBER |  The mobile number to be used on the server |
| VALUEFIRST\_USERNAME | Username for a  configured number for sending messages to the user through WhatsApp provider API calls |
| VALUEFIRST\_PASSWORD | Password for a configured number for sending messages to the user through WhatsApp provider API calls |
| GOOGLE\_MAPS\_API\_KEY | Maps API key to access geocoding feature |
| ROOT\_TENANTID | Contains state-level tenantid value |
| SUPPORTED\_LOCALES | This variable contains the list of supported language in the chatbot. If there is a need to add a new language in the chatbot, then its respective locale has to be added to this list. |
| PGR\_VERSION | Contains PGR version value to use \(i.e v1 or v2\) |
| PGR\_UPDATE\_TOPIC | Depends on the PGR version respective PGR update kafka topic name should mention here. Example: If PGR\_VERSION: 'v2' then PGR\_UPDATE\_TOPIC: 'update-pgr-request' |
| BILL\_SEARCH\_LIMIT | Limit for showing a maximum number of bills on search. |
| RECEIPT\_SEARCH\_LIMIT | Limit for showing a maximum number of receipts on search. |
| COMPLAINT\_SEARCH\_LIMIT | Limit for showing a maximum number of complaints on search. |
| BILL\_SUPPORTED\_MODULES | Contains the list of modules to be used for bill payment and receipts search. |
| INFORMATION\_IMAGE\_FILESTORE\_ID | Contains the filestoreid of informational image, which shows how to share the user current location. |
| USER\_SERVICE\_HARDCODED\_PASSWORD | This variable contains the fixed value of login password and OTP. This value has to be configured in _env_-secrets.yaml.  |

#### Configuration of Telemetry File <a id="Configuration-of-Telemetry-File"></a>

Add this [telemetry file](https://github.com/egovernments/configs/pull/629/files) in the [config repo](https://github.com/egovernments/configs/tree/DEV/egov-indexer) and mention the filename in the respective [environment yaml file](https://github.com/egovernments/eGov-infraOps/blob/master/helm/environments/qa.yaml#L248).

## Reference Docs

#### Doc Links <a id="Doc-Links"></a>

| **Title** | **Link** |
| :--- | :--- |
| Chatbot Message Localisation | [Chatbot Message Localisation Doc](https://digit-discuss.atlassian.net/wiki/spaces/DD/pages/1174306907/Xstate-Chatbot+Message+Localisation?atlOrigin=eyJpIjoiOTg3NTVmYTRhYTgzNDE3ODliODIzN2E1ODIxNmFkNmYiLCJwIjoiYyJ9) |

#### API List <a id="API-List"></a>

| **Title** | **Link** |
| :--- | :--- |
| /xstate-chatbot/message | [https://www.getpostman.com/collections/57615217a846330672c6](https://www.getpostman.com/collections/57615217a846330672c6) |

