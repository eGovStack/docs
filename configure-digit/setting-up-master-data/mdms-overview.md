# MDMS Overview

### Overview

MDMS stands for Master Data Management Service. MDMS is One of the applications in the eGov DIGIT core group of services. This service aims to reduce the time spent by developers on writing codes to store and fetch master data ( primary data needed for module functionality ) which doesn’t have any business logic associated with them.

### Pre-requisites

Before you proceed with the configuration, make sure the following pre-requisites are met -

* Prior Knowledge of Java/J2EE.
* Prior Knowledge of Spring Boot.
* Prior Knowledge of REST APIs and related concepts like path parameters, headers, JSON, etc.
* Prior knowledge of Git.
* Advanced knowledge on how to operate JSON data would be an added advantage to understand the service.

### Key Functionalities

* The MDMS service reads the data from a set of JSON files from a pre-specified location.
* It can either be an online location (readable JSON files from online) or offline (JSON files stored in local memory).
* The JSON files will be in a prescribed format and store the data on a map. The **tenantID** of the file serves as a key and a map of master data details as values.
* Once the data is stored in the map the same can be retrieved by making an API request to the MDMS service. Filters can be applied in the request to retrieve data based on the existing fields of JSON.

### Deployment Details

* For deploying the changes in MDMS data, the service needs to be restarted.
* The changes in MDMS data could be adding new data, updating existing data, or deletion.

### Configuration Details

The config JSON files to be written should follow the listed rules

* The config files should have JSON extension
* The file should mention the tenantId, module name, and the master name first before defining the data

```
{
  "tenantId": "uk",
  "moduleName": "BillingService",
  "{$MasterName}":[ ]
}
```

|            |                                                                                                                                  |
| ---------- | -------------------------------------------------------------------------------------------------------------------------------- |
| **Title**  | **Description**                                                                                                                  |
| tenantId   | Serves as a Key                                                                                                                  |
| moduleName | Name of the module to which the master data belongs                                                                              |
| MasterName | The Master Name will be substituted by the actual name of the master data. The array succeeding it will contain the actual data. |

Example Config JSON for “Billing Service”

```
{
  "tenantId": "pb",
  "moduleName": "BillingService",
 "BusinessService": 
 [
    {
      "businessService": "PropertyTax",
      "code": "PT",
      "collectionModesNotAllowed": [ "DD" ],
      "partPaymentAllowed": true,
      "isAdvanceAllowed": true,
      "isVoucherCreationEnabled": true
    }
]
}
```

### Reference Docs

#### Doc Links

|                      |                |
| -------------------- | -------------- |
| **Title**            | **Link**       |
| Reference Doc Link 1 | MDMS-Service   |
| Reference Doc Link 2 | MDMS-Rewritten |

#### API List

|                        |                                                                                                                                                                                                        |
| ---------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
|                        | **Link**                                                                                                                                                                                               |
| API Contract Reference | [https://raw.githubusercontent.com/egovernments/egov-services/master/docs/mdms/contract/v1-0-0.yml](https://raw.githubusercontent.com/egovernments/egov-services/master/docs/mdms/contract/v1-0-0.yml) |

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation ](https://egov.org.in/)is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).
