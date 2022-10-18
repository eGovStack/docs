---
description: v2 configuration details
---

# Collection Service

## **Overview**

The Collection Service serves as a revenue collection platform for all the billing systems through cash, cheque, demand drafts, or the swipe machine. It enables payment for all services provided by the eGov platform at a single point directly from the citizen or over-the-counter collection within municipalities.

## **Pre-requisites**

* Prior Knowledge of Java/J2EE
* Prior Knowledge of SpringBoot
* Prior Knowledge of REST APIs and related concepts like path parameters, headers, JSON, etc
* Prior Knowledge of Kafka and related concepts like Producer, Consumer, Topic, etc.
* The following services must be up and running:
  * egov-localization
  * egov-mdms
  * egov-idgen
  * egov-url-shortening
  * billing-service

## **Key Functionalities**

* Allows citizens to create a payment.
* Allows employees to create the payment for the citizen indirectly.
* Provides facilities to capture partial and advanced payments based on configs.
* Allows payment cancellation to help with scenarios of bad checks and other failed payment scenarios.
* Integrates with billing service for demand back-update of payment.

## **Deployment Details**

* deploy the latest version of the collection-services docker builds.

## **Configuration Details** <a href="#configuration-details" id="configuration-details"></a>

The MDMS data configuration uses the same data updated by the Billing-Service.

[Billing Service | Configuration-Details:](../billing-service/#configuration-details) Refer to the MDMS data configuration here.

The table below lists the application properties.

| Property                                                                               | Value                                                          | Remarks                                                                                                                                                                                 |
| -------------------------------------------------------------------------------------- | -------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `collection.receipts.search.paginate`                                                  | true/false                                                     | By setting this property true, show you the search result of receipt in a bucket(page) which contains a certain number of records.                                                      |
| `is.payment.search.uri.modulename.mandatory=true`                                      | TRUE/FALSE                                                     | Make module name in URI path mandatory                                                                                                                                                  |
| `collection.receipts.search.default.size`                                              | Certain number (say 30)                                        | Give the 30 records at a time and next 30 results are in the next page.                                                                                                                 |
| `collection.is.user.create.enabled`                                                    | true/false                                                     | By setting this property true, enabling the creation of user with receipt creation                                                                                                      |
| `receiptnumber.idname`                                                                 | [receipt.id - Registered at Namecheap.com](http://receipt.id/) | This property is used for creation of receipt number using ID-GEN service                                                                                                               |
| `receiptnumber.servicebased`                                                           | true/false                                                     | If servicebased is set to false, use default state level format for the format of receipt number and if it is set to true the format for the receipt number has to be mentioned in MDMS |
| `receiptnumber.state.level.format`                                                     | \[cy:MM]/\[fy:yyyy-yy]/\[SEQ\_COLL\_RCPT\_NUM]                 | Default state level format for the receipt number.                                                                                                                                      |
| `collection.payments.search.paginate`                                                  | true/false                                                     | By setting this property true, show you the search result of payment records in a bucket(page) which contains a certain number of records.                                              |
| \`\`[`kafka.topics.payment.create.name`](http://kafka.topics.payment.create.name/)\`\` | egov.collection.payment-create                                 | The kafka topic on which the record has to push/pull when payment is created.                                                                                                           |
| \`\`[`kafka.topics.payment.cancel.name`](http://kafka.topics.payment.cancel.name/)\`\` | egov.collection.payment-cancel                                 | The kafka topic on which the record has to push/pull when payment is cancelled.                                                                                                         |
| [`kafka.topics.payment.update.name`](http://kafka.topics.payment.update.name/)\`\`     | egov.collection.payment-update                                 | The kafka topic on which the record has to push/pull when payment is updated.                                                                                                           |

## Integration

### Integration Scope

Collection service can be integrated with any organization or system that requires a payment system to keep track of its payments. Organizations can customize part of the application or its functionalities based on their requirements.

### Integration Benefits

* Easy payments and tracking of payments.
* Configurable functionalities according to client requirement

### Steps to Integration

1. Customers can create a payment using the /payments/\_create
2. Actors on the system can keep track of payments using /payments/\_searchendpoint
3. Once the payment is done and it encounters a technical issue that is beyond the system - the payment can be cancelled with /payments/\_workflow
4. For employees to access the payments API the respective module name should be appended to the payment API path - /payments/PT/\_workflow. Here PT refers to the property module.

### **Interaction Diagram**

[Billing-Collection-Integration](../billing-collection-integration.md#integration-details) - Refer to the integration details.

## **Reference Docs**

**Doc Links**

| Description     | Link                                                                                                   |
| --------------- | ------------------------------------------------------------------------------------------------------ |
| Billing-service | [Billing Service](https://digit-discuss.atlassian.net/wiki/spaces/DD/pages/1620672528/Billing+Service) |
| Id-Gen service  |                                                                                                        |
| url-shortening  |                                                                                                        |
| MDMS            |                                                                                                        |

**API List**

| Description          | Link                                                                                                                       |
| -------------------- | -------------------------------------------------------------------------------------------------------------------------- |
| /payments/\_create   | [https://www.getpostman.com/collections/824d6b50b728bccd86d4](https://www.getpostman.com/collections/824d6b50b728bccd86d4) |
| /payments/\_update   | [https://www.getpostman.com/collections/824d6b50b728bccd86d4](https://www.getpostman.com/collections/824d6b50b728bccd86d4) |
| /payments/\_workflow | [https://www.getpostman.com/collections/824d6b50b728bccd86d4](https://www.getpostman.com/collections/824d6b50b728bccd86d4) |

> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)\_\_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_ ](https://egov.org.in/)_is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
