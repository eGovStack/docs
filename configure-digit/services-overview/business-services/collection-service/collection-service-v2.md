# Collection Service V2

## **Overview**

The Collection service is to serve as a revenue collection platform for all the billing systems through cash, cheque, demand draft, and swipe machines. It enables payment for all services provided by the eGov platform at a single point for the citizen and counter collection in municipal alike.

## **Pre-requisites**

* Prior knowledge of Java/J2EE
* Prior knowledge of SpringBoot
* Prior knowledge of REST APIs and related concepts like path parameters, headers, JSON, etc
* Prior knowledge of Kafka and related concepts like Producer, Consumer, Topic, etc.
* The following services should be up and running:
  * egov-localization
  * egov-mdms
  * egov-idgen
  * egov-url-shortening
  * billing-service

## **Key Functionalities**

* Allows citizens to create a payment.
* Allows employees to create the payment for the citizen indirectly.
* provides facilities to capture partial and advanced payments based on configs.
* allows payment cancellation to help with scenarios of bad checks and other failed payment scenarios.
* Integrates with billing service for demand back-update of payment.

## **Deployment Details**

* deploy the latest version of the collection-services docker builds.

## **Configuration Details**

The MDMS data configuration uses the same data updated by Billing-Service

[Billing Service | Configuration-Details: ](../billing-service/)Refer to the MDMS data config from here.

Following are the properties in the application.properties

| Property                                                                     | Value                                                          | Remarks                                                                                                                                                                                 |
| ---------------------------------------------------------------------------- | -------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| collection.receipts.search.paginate                                          | true/false                                                     | By setting this property true, show you the search result of receipt in a bucket(page) which contains a certain number of records.                                                      |
| `is.payment.search.uri.modulename.mandatory=true`                            | TRUE/FALSE                                                     | Make module name in URI path mandatory                                                                                                                                                  |
| collection.receipts.search.default.size                                      | Certain number (say 30)                                        | Give the 30 records at a time and next 30 results are in the next page.                                                                                                                 |
| collection.is.user.create.enabled                                            | true/false                                                     | By setting this property true, enabling the creation of user with receipt creation                                                                                                      |
| receiptnumber.idname                                                         | [receipt.id - Registered at Namecheap.com](http://receipt.id/) | This property is used for creation of receipt number using ID-GEN service                                                                                                               |
| receiptnumber.servicebased                                                   | true/false                                                     | If servicebased is set to false, use default state level format for the format of receipt number and if it is set to true the format for the receipt number has to be mentioned in MDMS |
| receiptnumber.state.level.format                                             | \[cy:MM]/\[fy:yyyy-yy]/\[SEQ\_COLL\_RCPT\_NUM]                 | Default state level format for the receipt number.                                                                                                                                      |
| collection.payments.search.paginate                                          | true/false                                                     | By setting this property true, show you the search result of payment records in a bucket(page) which contains a certain number of records.                                              |
| [kafka.topics.payment.create.name](http://kafka.topics.payment.create.name/) | egov.collection.payment-create                                 | The kafka topic on which the record has to push/pull when payment is created.                                                                                                           |
| [kafka.topics.payment.cancel.name](http://kafka.topics.payment.cancel.name/) | egov.collection.payment-cancel                                 | The kafka topic on which the record has to push/pull when payment is cancelled.                                                                                                         |
| [kafka.topics.payment.update.name](http://kafka.topics.payment.update.name/) | egov.collection.payment-update                                 | The kafka topic on which the record has to push/pull when payment is updated.                                                                                                           |

## Integration Details

### Integration Scope

Collection service can be integrated with any organization or system that wants a payment system to keep track of its payments. Organizations can customize part of the application or its functionality based on their requirements.

### Integration Benefits

* Easy payments and tracking of payments.
* Configurable functionalities according to client requirements.

### Steps to Integration

* Customers can create a payment using the `/payments/_create.`
* Actors on the system can keep track of payments using `/payments/_search`endpoint.
* Once the payment is done but it encounters a technical issue outside of the system then it can be cancelled with `/payments/_workflow.`
* For employees to access the payments API the respective module name should be appended after the payment API path - `/payments/PT/_workflow` - here PT refers to the property module.

### **IFSC Code Migration - Collection Service**

* Port forward the collection service to the current environment where the IFSC CODE bank details data is to be migrated. Sample command - `1kubectl port-forward collection-services-76b775f976-xcbt2 8055:8080 -n egov`
* Import postman collection from API list which refers as `/preexistpayments/_update` and runs with the same localhost to where we port forwarded using the above command.
*   Expected result.\
    In the EGCL\_PAYMET table where IFSCODE data is present for those records, EGCL\_PAYMET.ADDITIONALDETAILS bankdetails will be updated.

    Ex: For IFSCCODE : UCBA0003047\
    Response from API [https://ifsc.razorpay.com/UCBA0003047](https://ifsc.razorpay.com/UCBA0003047) is updated in EGCL\_PAYMET.ADDITIONALDETAILS\
    as {"bankDetails": {"UPI": true, "BANK": "UCO Bank", "CITY": "BHIKHI", "IFSC": "UCBA0003047", "IMPS": true, "MICR": "151028452", "NEFT": true, "RTGS": true, "STATE": "PUNJAB", "SWIFT": "", "BRANCH": "BHIKHI", "CENTRE": "MANSA", "ADDRESS": "ADJOINING HP PETROL PUMP MANSA ROADDISTRICT MANSA","BANKCODE":"UCBA","DISTRICT":"MANSA","CONTACT":"+918288822548"}

## **Interaction Diagram**

[Billing-Collection-Integration](../billing-collection-integration.md) Refer to the integration with details and explanation.

## **Reference Docs**

### **Doc Links**

| Description     | Link                                   |
| --------------- | -------------------------------------- |
| Billing-service | [Billing Service](../billing-service/) |
| Id-Gen service  |                                        |
| url-shortening  |                                        |
| MDMS            |                                        |

### **API List**

| Description                | Link                                                                                                                       |
| -------------------------- | -------------------------------------------------------------------------------------------------------------------------- |
| /payments/\_create         | [https://www.getpostman.com/collections/824d6b50b728bccd86d4](https://www.getpostman.com/collections/824d6b50b728bccd86d4) |
| /payments/\_update         | [https://www.getpostman.com/collections/824d6b50b728bccd86d4](https://www.getpostman.com/collections/824d6b50b728bccd86d4) |
| /payments/\_workflow       | [https://www.getpostman.com/collections/824d6b50b728bccd86d4](https://www.getpostman.com/collections/824d6b50b728bccd86d4) |
| /preexistpayments/\_update | [https://www.getpostman.com/collections/261c1f0b520cf5aabc93](https://www.getpostman.com/collections/261c1f0b520cf5aabc93) |

\
​​[​![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)​](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation ](https://egov.org.in/)is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).
