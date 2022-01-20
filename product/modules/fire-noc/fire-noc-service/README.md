---
description: Service configuration
---

# Fire NOC Service

## Overview

The main objective of the Fire-NOC module is to provide a **No Objection Certificate** indicating that the building is designed as per fire safety norms and regulation.

## Pre-requisites

Before you proceed with the documentation, make sure the following pre-requisites are met -

* Prior knowledge of JavaScript.
* Prior knowledge of Node.js platform.
* Kafka server is up and running
* JSONPath for filtering required data from json objects.
* Prior Knowledge of REST APIs and related concepts like path parameters, headers, JSON etc.
* egov-persister service is running and has firenoc-services persister config path added in it
* PSQL server is running and database is created
* Prior knowledge of eGov-mdms service, eGov-persister, eGov-user, eGov-location, eGov-localization, eGov-idgen

## Key Functionalities

* Used for No Objection Certificate generations indicating that the building is designed as per fire safety norms and regulation.
* Generate application number and fire noc number
* Support workflow
* Provide notification on various status changes for an application

## Deployment Details

1. Add mdms configs required for firenoc service and restart mdms service.
2. Deploy the latest version of firenoc-services service.
3. Add firenoc-services persister yaml path in persister configuration and restart persister service.
4. Add Role-Action mapping for API’s.
5. Create businessService (workflow configuration) according to firenoc registration.

## Configuration Details

Following are the properties in application.properties file in trade firenoc-service which are configurable.

|                                  |                                            |                                                                                        |
| -------------------------------- | ------------------------------------------ | -------------------------------------------------------------------------------------- |
| **Property**                     | **Value**                                  | **Remarks**                                                                            |
| EGOV\_APPLICATION\_FORMATE       | PB-FN-\[cy:yyyy-MM-dd]-\[SEQ\_EG\_TL\_APL] | The format of the firenoc application number                                           |
| EGOV\_CIRTIFICATE\_FORMATE       | PB-FN-\[cy:yyyy-MM-dd]-\[SEQ\_EG\_PT\_LN]  | The format of the firenoc certificate number                                           |
| EGOV\_DEFAULT\_STATE\_ID         | pb                                         | Variable store the default value of state tenantid                                     |
| EGOV\_FN\_DEFAULT\_LIMIT         | 100                                        | Max number of records to be returned                                                   |
| KAFKA\_TOPICS\_FIRENOC\_CREATE   | save-fn-firenoc                            | The name of kafka topic on which create request is published                           |
| KAFKA\_TOPICS\_FIRENOC\_UPDATE   | update-fn-firenoc                          | The name of kafka topic on which update request is published                           |
| KAFKA\_TOPICS\_FIRENOC\_WORKFLOW | update-fn-workflow                         | The name of kafka topic on which status update request is published                    |
| ACTION\_PAY                      | PAY                                        | This is workflow action for making payment against the application                     |
| SENDBACK                         | SENDBACK                                   | This is workflow action for sending application to the previous state of the workflow. |
| SENDBACKTOCITIZEN                | SENDBACKTOCITIZEN                          | This is a workflow action for sending application to the citizen for correction.       |

**MDMS Configuration**

Firenoc service makes calls to egov-mdms-service to fetch required masters. These are significant in validations of application.

| Fire-NOC masters                                                                                                                  | Description                                                                                             |
| --------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------- |
| [Application Type](https://github.com/egovernments/egov-mdms-data/blob/master/data/pb/firenoc/ApplicationType.json)               | This master contains the list of application type.                                                      |
| [Building Type](https://github.com/egovernments/egov-mdms-data/blob/master/data/pb/firenoc/BuildingType.json)                     | This master contains the details about which unit of measurement is use for a particular building type. |
| [FireStations](https://github.com/egovernments/egov-mdms-data/blob/master/data/pb/firenoc/FireStations.json)                      | This master contains the list of firestation present in city.                                           |
| [PropertyType](https://github.com/egovernments/egov-mdms-data/blob/master/data/pb/firenoc/PropertyType.json)                      | This master contains the list of property type.                                                         |
| [FireNocULBConstats](https://github.com/egovernments/egov-mdms-data/blob/master/data/pb/amritsar/firenoc/FireNocULBConstats.json) | This master contains the list of minimum charges of each application type.                              |

Create businessService (workflow configuration) using the \_\_/businessservice/\_create. Following is the product configuration for firenoc service

```
"BusinessServices": [
    {
      "tenantId": "pb",
      "businessService": "FIRENOC",
      "business": "fireNoc",
      "businessServiceSla": 172800000,
      "states": [
        {
          "sla": null,
          "state": null,
          "applicationStatus": null,
          "docUploadRequired": false,
          "isStartState": true,
          "isTerminateState": false,
          "actions": [
            {
              "action": "INITIATE",
              "nextState": "INITIATED",
              "roles": [
                "CITIZEN",
                "NOC_CEMP"
              ]
            }
          ]
        },
        {
          "sla": null,
          "state": "INITIATED",
          "applicationStatus": "INITIATED",
          "docUploadRequired": false,
          "isStartState": true,
          "isTerminateState": false,
          "actions": [
            {
              "action": "APPLY",
              "nextState": "PENDINGPAYMENT",
              "roles": [
                "CITIZEN",
                "NOC_CEMP"
              ]
            },
            {
              "action": "INITIATE",
              "nextState": "INITIATED",
              "roles": [
                "CITIZEN",
                "TL_CEMP"
              ]
            }
          ]
        },
        {
          "sla": null,
          "state": "PENDINGPAYMENT",
          "applicationStatus": "PENDINGPAYMENT",
          "docUploadRequired": false,
          "isStartState": false,
          "isTerminateState": false,
          "isStateUpdatable": false,
          "actions": [
            {
              "action": "PAY",
              "nextState": "DOCUMENTVERIFY",
              "roles": [
                "CITIZEN",
                "NOC_CEMP"
              ]
            },
            {
              "action": "ADHOC",
              "nextState": "PENDINGPAYMENT",
              "roles": [
                "NOC_CEMP"
              ]
            }
          ]
        },
        {
          "sla": 86400000,
          "state": "DOCUMENTVERIFY",
          "applicationStatus": "DOCUMENTVERIFY",
          "docUploadRequired": false,
          "isStartState": false,
          "isTerminateState": false,
          "isStateUpdatable": false,
          "actions": [
            {
              "action": "REJECT",
              "nextState": "REJECTED",
              "roles": [
                "NOC_DOC_VERIFIER"
              ]
            },
            {
              "action": "FORWARD",
              "nextState": "FIELDINSPECTION",
              "roles": [
                "NOC_DOC_VERIFIER"
              ]
            },
            {
              "action": "REFER",
              "nextState": "DOCUMENTVERIFY",
              "roles": [
                "NOC_DOC_VERIFIER"
              ]
            },
            {
              "action": "SENDBACKTOCITIZEN",
              "nextState": "CITIZENACTIONREQUIRED-DV",
              "roles": [
                "NOC_DOC_VERIFIER"
              ]
            }
          ]
        },
        {
          "sla": null,
          "state": "REJECTED",
          "applicationStatus": "REJECTED",
          "docUploadRequired": false,
          "isStartState": false,
          "isTerminateState": true
        },
        {
          "sla": 86400000,
          "state": "FIELDINSPECTION",
          "applicationStatus": "FIELDINSPECTION",
          "docUploadRequired": false,
          "isStartState": false,
          "isTerminateState": false,
          "isStateUpdatable": false,
          "actions": [
            {
              "action": "REJECT",
              "nextState": "REJECTED",
              "roles": [
                "NOC_FIELD_INSPECTOR"
              ]
            },
            {
              "action": "SENDBACK",
              "nextState": "DOCUMENTVERIFY",
              "roles": [
                "NOC_FIELD_INSPECTOR"
              ]
            },
            {
              "action": "FORWARD",
              "nextState": "PENDINGAPPROVAL",
              "roles": [
                "NOC_FIELD_INSPECTOR"
              ]
            },
            {
              "action": "REFER",
              "nextState": "FIELDINSPECTION",
              "roles": [
                "NOC_FIELD_INSPECTOR"
              ]
            },
            {
              "action": "SENDBACKTOCITIZEN",
              "nextState": "CITIZENACTIONREQUIRED",
              "roles": [
                "NOC_FIELD_INSPECTOR"
              ]
            }
          ]
        },
        {
          "sla": 43200000,
          "state": "PENDINGAPPROVAL",
          "applicationStatus": "PENDINGAPPROVAL",
          "docUploadRequired": false,
          "isStartState": false,
          "isTerminateState": false,
          "isStateUpdatable": false,
          "actions": [
            {
              "action": "SENDBACK",
              "nextState": "FIELDINSPECTION",
              "roles": [
                "NOC_APPROVER"
              ]
            },
            {
              "action": "REFER",
              "nextState": "PENDINGAPPROVAL",
              "roles": [
                "NOC_APPROVER"
              ]
            },
            {
              "action": "APPROVE",
              "nextState": "APPROVED",
              "roles": [
                "NOC_APPROVER"
              ]
            },
            {
              "action": "REJECT",
              "nextState": "REJECTED",
              "roles": [
                "NOC_APPROVER"
              ]
            }
          ]
        },
        {
          "sla": null,
          "state": "APPROVED",
          "applicationStatus": "APPROVED",
          "docUploadRequired": false,
          "isStartState": false,
          "isTerminateState": false,
          "isStateUpdatable": false,
          "actions": [
            {
              "action": "CANCEL",
              "nextState": "CANCELLED",
              "roles": [
                "NOC_APPROVER"
              ]
            }
          ]
        },
        {
          "sla": null,
          "state": "CANCELLED",
          "applicationStatus": "CANCELLED",
          "docUploadRequired": false,
          "isStartState": false,
          "isTerminateState": true,
          "isStateUpdatable": false,
          "actions": null
        },
        {
          "sla": null,
          "state": "CITIZENACTIONREQUIRED",
          "applicationStatus": "CITIZENACTIONREQUIRED",
          "docUploadRequired": false,
          "isStartState": false,
          "isTerminateState": false,
          "isStateUpdatable": true,
          "actions": [
              {
                  "action": "RESUBMIT",
                  "nextState": "FIELDINSPECTION",
                  "roles": [
                      "CITIZEN",
                      "NOC_CEMP"
                  ]
              }
          ]
      },
      
      {
          "sla": null,
          "state": "CITIZENACTIONREQUIRED-DV",
          "applicationStatus": "CITIZENACTIONREQUIRED-DV",
          "docUploadRequired": false,
          "isStartState": false,
          "isTerminateState": false,
          "isStateUpdatable": true,
          "actions": [
              {
                  "action": "RESUBMIT",
                  "nextState": "DOCUMENTVERIFY",
                  "roles": [
                      "CITIZEN",
                      "NOC_CEMP"
                  ]
              }
          ]
      }

      ]
    }
  ]
```

**Persister Config**

[https://github.com/egovernments/configs/blob/DEV/egov-persister/firenoc\_persiter.yaml](https://github.com/egovernments/configs/blob/DEV/egov-persister/firenoc\_persiter.yaml)

**Id Gen Config**

[https://github.com/egovernments/egov-services/blob/noc/core/egov-idgen/src/main/resources/db/migration/main/V20190517152600\_\_create\_fn\_sequence\_ddl.sql](https://github.com/egovernments/egov-services/blob/noc/core/egov-idgen/src/main/resources/db/migration/main/V20190517152600\_\_create\_fn\_sequence\_ddl.sql)

#### API Details <a href="#api-details" id="api-details"></a>

BasePath /firenoc-services/v1/\[API endpoint]

**Method**

a) \_create

Create API call is called with INITIATED action to create new application. In this API call we validate request body(using ajv module for contract specific validation and explicit checking for user related validation checks), enrich audit details, generate application no using idgen, persist data using persister and return response.

**Allowed user roles:** NOC\_CEMP, CITIZEN

b) \_update

Once application is created it can be updated by citizen or employee while taking action on application

**Allowed user roles:** NOC\_CEMP, CITIZEN, NOC\_DOC\_VERIFIER, NOC\_FIELD\_INSPECTOR, NOC\_APPROVER

c) \_search

Search API call is used to search for application. If search call is being made by CITIZEN then only his application would be fetched applying other search filters. For employee search based on search filter will return data.

**Allowed user roles:** NOC\_CEMP, CITIZEN, NOC\_DOC\_VERIFIER, NOC\_FIELD\_INSPECTOR, NOC\_APPROVER, EMPLOYEE

## Integration Details

### Integration Scope

The Fire-Noc service is used to provide a **No Objection Certificate** indicating that the building is designed as per fire safety norms and regulation.

### Integration Benefits

* Provide backend support for the No Objection Certificate registration process for a different building.
* SMS notifications on application status changes.
* Supports workflow which is configurable

### Steps to Integration

To integrate, host of firenoc-services service should be overwritten in helm chart.

1. firenoc-services/v1/\_create should be added as the create endpoint for creating fire noc application in the system.
2. firenoc-services/v1/\_search should be added as the search endpoint. This method handles all requests to search existing records depending on different search criteria.
3. firenoc-services/v1/\_update should be added as the update endpoint. This method is used to update fields in existing records or to update the status of the application based on workflow.

### Interaction Diagram

To Do

## Reference Docs

#### Doc Links <a href="#doc-links" id="doc-links"></a>

|                              |                                                                                                                                                                                             |
| ---------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Title**                    | **Link**                                                                                                                                                                                    |
| API Swagger Documentation    | [Swagger Documentation](https://editor.swagger.io/?url=https://raw.githubusercontent.com/egovernments/municipal-services/master/firenoc-services/docs/contract/fire\_noc\_contract.yaml#!/) |
| Firer Noc Calculator Service | [Fire Noc Calculator Service](https://digit-discuss.atlassian.net/l/c/28H8m1B9)                                                                                                             |

#### API List <a href="#api-list" id="api-list"></a>

|                                |                                                                                                                            |
| ------------------------------ | -------------------------------------------------------------------------------------------------------------------------- |
| Title                          | **Link**                                                                                                                   |
| _firenoc-services/v1/\_create_ | [https://www.getpostman.com/collections/093e28bb4e341770b6c7](https://www.getpostman.com/collections/093e28bb4e341770b6c7) |
| _firenoc-services/v1/\_search_ | [https://www.getpostman.com/collections/093e28bb4e341770b6c7](https://www.getpostman.com/collections/093e28bb4e341770b6c7) |
| _firenoc-services/v1/\_update_ | [https://www.getpostman.com/collections/093e28bb4e341770b6c7](https://www.getpostman.com/collections/093e28bb4e341770b6c7) |

_(Note: All the API’s are in the same postman collection therefore same link is added in each row)_

\_\_

\_\_

> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)\_\_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_ ](https://egov.org.in)_is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
