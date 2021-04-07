# PGR Services

## Overview <a id="Overview"></a>

Public Grievances & Redressal \(PGR\) is a system that enables citizens to raise a complaint with there ULB’s. A citizen can track the complaint, upload image related to the complaint, re-open the complaint if he/she is not satisfied and rate the service. This document contains the details about how to setup PGR service and describes the functionalities it provides

## Pre-requisites <a id="Pre-requisites"></a>

Before you proceed with the configuration, make sure the following pre-requisites are met -

* Java 8
* Kafka server is up and running
* egov-persister service is running and has pgr-services persister config path added in it
* PSQL server is running and database is created to store complaint data
* _\(Optional\)_ Indexer config for pgr-services is added in egov-indexer yaml paths to index the generated data. Index is required for data visualisation in Kibana or in DSS.
* _\(Optional\)_ Report config for pgr-services is added in Report service config paths. Required if reports are to be provided to the user.
* Following services should be up and running:
  * egov-user
  * egov-workflow-v2
  * egov-perister
  * egov-localization
  * egov-notification-sms
  * egov-mdms
  * egov-idgen
  * egov-url-shortening
  * egov-hrms

## Key Functionalities <a id="Key-Functionalities"></a>

* A citizen can file, track and rate the complaint
* A citizen can add image and comments related to the complaint
* A citizen can re-open the complaint in a certain given period of time after resolution
* ULB can setup the complaint workflow according to their requirements and staff capacity
* ULB can track the SLA for resolving each complaint and can use it as a metric to streamline the process for resolving complaints
* Department wise assignment of the complaint to the LME

## Deployment Details <a id="Deployment-Details"></a>

1. Deploy the latest version of pgr-services
2. Add pgr-service-persister.yml file in config folder in git and add that path in persister. _\(The file path is to be added in environment yaml file in param called_ persist-yml-path _\)_
3. If any Report Config is created, the config should be added to the config folder in git and that path should be added in Report service. \(_The file path is to be added in a file called “reportFileLocationsv1.txt” in Config folder_\)
4. If index is to be created add the indexer config path in indexer service. \(_The file path is to be added in environment yaml file in param called_ egov-indexer-yaml-repo-path\)

## Configuration Details <a id="Configuration-Details"></a>

1. Add master data in MDMS service with the module name as RAINMAKER-PGR. Following is some sample master data for the service:

```text
{
  "tenantId": "pb",
  "moduleName": "RAINMAKER-PGR",
  "ServiceDefs": [
    {
      "serviceCode": "NoStreetlight",
      "keywords": "streetlight, light, repair, work, pole, electric, power, repair, damage, fix",
      "department": "Streetlights",
      "slaHours": 336,
      "menuPath": "StreetLights",
      "active": false,
      "order": 1
    },
    {
      "serviceCode": "StreetLightNotWorking",
      "keywords": "streetlight, light, repair, work, pole, electric, power, repair, fix",
      "department": "DEPT_1",
      "slaHours": 336,
      "menuPath": "StreetLights",
      "active": true,
      "order": 2
    },
    {
      "serviceCode": "GarbageNeedsTobeCleared",
      "keywords": "garbage, collect, litter, clean, door, waste, remove, sweeper, sanitation, dump, health, debris, throw",
      "department": "DEPT_25",
      "slaHours": 336,
      "menuPath": "Garbage",
      "active": true,
      "order": 3
    }
  ]
}
```

Create businessService \(workflow configuration\) using the \_\_/businessservice/\_create. Following is the product configuration for PGR:

```text
{
      "tenantId": "pb",
      "businessService": "PGR",
      "business": "pgr-services",
      "businessServiceSla": 432000000,
      "states": [
        {
          "sla": null,
          "state": null,
          "applicationStatus": null,
          "docUploadRequired": false,
          "isStartState": true,
          "isTerminateState": false,
          "isStateUpdatable": true,
          "actions": [
            {
              "action": "APPLY",
              "nextState": "PENDINGFORASSIGNMENT",
              "roles": [
                "CITIZEN",
                "CSR"
              ]
            }
          ]
        },
        {
          "sla": null,
          "state": "PENDINGFORASSIGNMENT",
          "applicationStatus": "PENDINGFORASSIGNMENT",
          "docUploadRequired": false,
          "isStartState": false,
          "isTerminateState": false,
          "isStateUpdatable": false,
          "actions": [
            {
              "action": "ASSIGN",
              "nextState": "PENDINGATLME",
              "roles": [
                "GRO",
                "DGRO"
              ]
            },
            {
              "action": "REJECT",
              "nextState": "REJECTED",
              "roles": [
                "GRO",
                "DGRO"
              ]
            }
          ]
        },
        {
          "sla": null,
          "state": "PENDINGFORREASSIGNMENT",
          "applicationStatus": "PENDINGFORREASSIGNMENT",
          "docUploadRequired": false,
          "isStartState": false,
          "isTerminateState": false,
          "isStateUpdatable": false,
          "actions": [
            {
              "action": "REASSIGN",
              "nextState": "PENDINGATLME",
              "roles": [
                "GRO",
                "DGRO"
              ]
            },
            {
              "action": "REJECT",
              "nextState": "REJECTED",
              "roles": [
                "GRO",
                "DGRO"
              ]
            }
          ]
        },

        {
          "sla": 259200000,
          "state": "PENDINGATLME",
          "applicationStatus": "PENDINGATLME",
          "docUploadRequired": false,
          "isStartState": false,
          "isTerminateState": false,
          "isStateUpdatable": false,
          "actions": [
            {
              "action": "RESOLVE",
              "nextState": "RESOLVED",
              "roles": [
                "PGR_LME"
              ]
            },
            {
              "action": "REASSIGN",
              "nextState": "PENDINGFORREASSIGNMENT",
              "roles": [
                "PGR_LME"
              ]
            }
          ]
        },
        {
          "sla": null,
          "state": "REJECTED",
          "applicationStatus": "REJECTED",
          "isStateUpdatable": false,
          "docUploadRequired": false,
          "isStartState": false,
          "isTerminateState": true,
          "actions": [
            {
              "action": "REOPEN",
              "nextState": "PENDINGFORASSIGNMENT",
              "roles": [
                "CFC",
                "CSR",
                "CITIZEN"
              ]
            },
            {
              "action": "RATE",
              "nextState": "CLOSEDAFTERREJECTION",
              "roles": [
                "CFC",
                "CITIZEN"
              ]
            }
          ]
        },
        {
          "sla": null,
          "state": "RESOLVED",
          "applicationStatus": "RESOLVED",
          "isStateUpdatable": false,
          "docUploadRequired": false,
          "isStartState": false,
          "isTerminateState": true,
          "actions": [
            {
              "action": "REOPEN",
              "nextState": "PENDINGFORASSIGNMENT",
              "roles": [
                "CFC",
                "CSR",
                "CITIZEN"
              ]
            },
            {
              "action": "RATE",
              "nextState": "CLOSEDAFTERRESOLUTION",
              "roles": [
                "CFC",
                "CITIZEN"
              ]
            }
          ]
        },
        {
          "sla": null,
          "state": "CLOSEDAFTERREJECTION",
          "applicationStatus": "CLOSEDAFTERREJECTION",
          "isStateUpdatable": false,
          "docUploadRequired": false,
          "isStartState": false,
          "isTerminateState": true
        },
        {
          "sla": null,
          "state": "CLOSEDAFTERRESOLUTION",
          "applicationStatus": "CLOSEDAFTERRESOLUTION",
          "isStateUpdatable": false,
          "docUploadRequired": false,
          "isStartState": false,
          "isTerminateState": true
        }
      ]
    }
```

Using /localization/messages/v1/\_upsert , add localisation \(templates\) for notification messages to be sent. Following are the product notification templates:

```text
{
  "messages": [
       {
            "code": "PGR_APPLY_PENDINGFORASSIGNMENT_SMS_MESSAGE",
            "message": "Dear Citizen, Your complaint for <complaint_type> has been submitted with ID <id> on <date>. You can track your complaint status on the mSeva Punjab mobile App (download here - <download link>) or your local municipal web portal.",
            "module": "rainmaker-pgr",
            "locale": "en_IN"
        },
        {
            "code": "PGR_RESOLVE_RESOLVED_SMS_MESSAGE",
            "message": "Dear Citizen, Your complaint for <complaint_type> with ID <id> submitted on <date> has been resolved by <emp_name>. If you are not satisfied with service you can REOPEN complaint through mSeva Punjab mobile App (download here - <download_link>) or your local municipal web portal or by calling our CSR.",
            "module": "rainmaker-pgr",
            "locale": "en_IN"
        },
        {
            "code": "PGR_REOPEN_PENDINGFORASSIGNMENT_SMS_MESSAGE",
            "message": "Dear Citizen, Your complaint for <complaint_type> with ID <id> submitted on <date> has been RE-OPEN as per your request. You can track your complaint status and connect with our officials on the mSeva Punjab mobile App (download here - <download_link>) or your local municipal web portal.",
            "module": "rainmaker-pgr",
            "locale": "en_IN"
        },
        {
            "code": "PGR_REJECT_REJECTED_SMS_MESSAGE",
            "message": "Dear Citizen, Your complaint for <complaint_type> with ID <id> submitted on <date> has been rejected. Reason for Rejection: <reason>, Additional Comments: <additional_comments> If you wish to re-open the complaint, you can download the mSeva Punjab mobile app (download here - <download_link>) or visit your local municipal website.",
            "module": "rainmaker-pgr",
            "locale": "en_IN"
        },
        {
            "code": "PGR_REASSIGN_PENDINGATLME_SMS_MESSAGE",
            "message": "Dear Citizen, Your complaint for <complaint_type> with ID <id> submitted on <date> has been re-assigned to <reassign_emp_name>, <emp_designation>, <emp_department>. You can track your complaint status and connect with our officials on the mSeva Punjab mobile App (download here - <download_link>) or your local municipal web portal.",
            "module": "rainmaker-pgr",
            "locale": "en_IN"
        }      
    ]
}
```

Add Role-Action mapping for the APIs in MDMS. Following are the required entries. They should be mapped to both CITIZEN and appropriate employee roles.

```text
{
  {
      "id": {{ID_PLACEHOLDER}},
      "name": "Create PGR Request",
      "url": "/pgr-services/v2/requests/_create",
      "parentModule": "",
      "displayName": "Create PGR Request",
      "orderNumber": 0,
      "enabled": false,
      "serviceCode": "pgr-services",
      "code": "null",
      "path": ""
    },
    {
      "id": {{ID_PLACEHOLDER}},
      "name": "Update PGR Request",
      "url": "/pgr-services/v2/requests/_update",
      "parentModule": "",
      "displayName": "Update PGR Request",
      "orderNumber": 0,
      "enabled": false,
      "serviceCode": "pgr-services",
      "code": "null",
      "path": ""
    },
    {
      "id": {{ID_PLACEHOLDER}},
      "name": "Search PGR Request",
      "url": "/pgr-services/v2/requests/_search",
      "parentModule": "",
      "displayName": "Search PGR Request",
      "orderNumber": 0,
      "enabled": false,
      "serviceCode": "pgr-services",
      "code": "null",
      "path": ""
    },
    {
      "id": {{ID_PLACEHOLDER}},
      "name": "Search PGR Request",
      "url": "/pgr-services/v2/requests/_count",
      "parentModule": "",
      "displayName": "Count PGR Request",
      "orderNumber": 0,
      "enabled": false,
      "serviceCode": "pgr-services",
      "code": "null",
      "path": ""
    }
```

## Integration <a id="Integration"></a>

### Integration Scope <a id="Integration-Scope"></a>

PGR service can be integrated with any organisation or system which wants to track customer queries or complaint. The organisations can customise the workflow depending on their product requirements.

### Integration Benefits <a id="Integration-Benefits"></a>

* Easy tracking and resolution of complaints
* Configurable workflow according to client requirement

### Steps to Integration <a id="Steps-to-Integration"></a>

1. Customer can raise a complaint using the `/requests/_create`.
2. Organisation or System can search the complaint using `/requests/_searchendpoint`.
3. Once the complaint is raised the organisation or system can call `/requests/_update` endpoint to move the application further in workflow until it gets resolved.

## Interaction Diagram <a id="Interaction-Diagram"></a>

![](../../../.gitbook/assets/image%20%2877%29.png)

## Reference Docs <a id="Interaction-Diagram"></a>

### Doc Links <a id="Doc-Links"></a>

| **Title** | **Link** |
| :--- | :--- |
| Workflow Technical Document | [Workflow Service](../core-service/workflow-service.md) |
| User Technical Document | [User Service](../core-service/user-service.md) |
| MDMS Technical Document | NEEDS TO BE UPDATED |
| IDGen Technical Document | NEEDS TO BE UPDATED |
| Localization Technical Document | NEEDS TO BE UPDATED |
| Persister Technical Document | NEEDS TO BE UPDATED |
| SMS Notification Technical Document | NEEDS TO BE UPDATED |
| HRMS Technical Document | NEEDS TO BE UPDATED |

### API List <a id="API-List"></a>

|  | **Link** |
| :--- | :--- |
| /requests/\_create | [https://www.getpostman.com/collections/09154f94d2c291a96777](https://www.getpostman.com/collections/09154f94d2c291a96777) |
| /requests/\_update | [https://www.getpostman.com/collections/09154f94d2c291a96777](https://www.getpostman.com/collections/09154f94d2c291a96777) |
| /requests/\_search | [https://www.getpostman.com/collections/09154f94d2c291a96777](https://www.getpostman.com/collections/09154f94d2c291a96777) |
| /requests/\_count | [https://www.getpostman.com/collections/09154f94d2c291a96777](https://www.getpostman.com/collections/09154f94d2c291a96777) |

