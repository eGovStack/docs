---
description: Configuration and setup details on registering vehicles in FSM module
---

# FSM Vehicle Registry v1.1

## Overview <a href="#overview" id="overview"></a>

Vehicle Registry is a system that enables ULB employees to create and search vehicle entities, schedule vehicle trips for received requests and track the trips. This document contains the details about how to set up the Vehicle details and describes the functionalities provided.

## Pre-requisites <a href="#pre-requisites" id="pre-requisites"></a>

Before you proceed with the configuration, make sure the following pre-requisites are met -

* Java 8
* Kafka server is up and running
* egov-persister service is running and has fsm-calculator-persister config path added in it
* PSQL server is running and a database is created to store FSM Application data
* Following services should be up and running:
  * egov-perister
  * egov-mdms
  * egov-workflow-v2
  * egov-idgen

## Deployment Details <a href="#deployment-details" id="deployment-details"></a>

1. Deploy the latest version of the vehicle
2. Add vehicle-persister.yml file in config folder in git and add that path in persister. _(The file path is to be added in environment yaml file in param called_ persist-yml-path_)_

## Configuration Details <a href="#configuration-details" id="configuration-details"></a>

### MDMS Configuration <a href="#mdms-configuration-hardbreak" id="mdms-configuration-hardbreak"></a>

Add master data in MDMS service with the module name as Vehicle.

Following is some sample master data for

**SuctionType**

```
{
    "tenantId": "pb",
    "moduleName": "Vehicle",
    "VehicleOwner": [{
            "name": "ULB",
            "code": "ULB",
            "active": true
        },
        {
            "name": "Private",
            "code": "Private",
            "active": true
        }
    ]
}
```

**VehicleMakeModel**

```
{
    "tenantId": "pb",
    "moduleName": "Vehicle",
    "VehicleMakeModel": [
        {
            "code": "MAHINDRA",
            "name": "Mahindra",
            "active": true
        },
        {
            "code": "MAHINDRA.BOLERO_PICKUP",
            "name": "Bolero Pickup",
            "active": true,
            "make": "MAHINDRA",
            "capacity": "5000",
            "amount": "500"
        },
        {
            "code": "TATA",
            "name": "TATA",
            "active": true
        },
        {
            "code": "TATA.LPT709/34",
            "name": "TATA LPT709/34",
            "active": true,
            "make": "TATA",
            "capacity": "2000",
            "amount": "200"
        },
        {
            "code": "TATA.407",
            "name": "TATA 407",
            "active": true,
            "make": "TATA",
            "capacity": "1000",
            "amount": "100"
        },
        {
            "code": "TAFE",
            "name": "TAFE",
            "active": true
        },
        {
            "code": "TAFE.TRACTOR_45DI",
            "name": "TAFE Tractor 45DI",
            "active": true,
            "make": "TAFE",
            "capacity": "10000",
            "amount": "1000"
        },
        {
            "code": "SONALIKA",
            "name": "Sonalika",
            "active": true
        },
        {
            "code": "SONALIKA.TRACTOR_35DI",
            "name": "Sonalika Tractor 35DI",
            "active": true,
            "make": "SONALIKA",
            "capacity": "8000",
            "amount": "1000"
        }
    ]
}
```

#### Business Service / Workflow Configuration <a href="#business-service-workflow-configuration" id="business-service-workflow-configuration"></a>

Workflow configuration for VehicleTrip of FSM

```
{
      "tenantId": "pb",
      "businessService": "FSM_VEHICLE_TRIP",
      "business": "vehicle",
      "businessServiceSla": 172800000,
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
              "action": "SCHEDULE",
              "nextState": "SCHEDULED",
              "roles": [
                "FSM_DSO"
              ]
            }
          ]
        },
        {
          "sla": null,
          "state": "SCHEDULED",
          "applicationStatus": "SCHEDULED",
          "docUploadRequired": false,
          "isStartState": true,
          "isTerminateState": false,
          "actions": [
            {
              "action": "READY_FOR_DISPOSAL",
              "nextState": "WAITING_FOR_DISPOSAL",
              "roles": [
                "FSM_DSO",
                "FSM_EDITOR_EMP"
              ]
            }
          ]
        },
        {
          "sla": null,
          "state": "WAITING_FOR_DISPOSAL",
          "applicationStatus": "WAITING_FOR_DISPOSAL",
          "docUploadRequired": false,
          "isStartState": true,
          "isTerminateState": false,
          "actions": [
            {
              "action": "DISPOSE",
              "nextState": "DISPOSED",
              "roles": [
                "FSM_EMP_FSTPO"
              ]
            }
          ]
        },
         {
          "sla": null,
          "state": "DISPOSED",
          "applicationStatus": "DISPOSED",
          "docUploadRequired": false,
          "isStartState": false,
          "isTerminateState": true,
          "isStateUpdatable": true
        }
      ]
    }
```

### Actions & Role Action Mapping <a href="#actions-and-role-action-mapping" id="actions-and-role-action-mapping"></a>

**Actions**

```
{
      "id": {{PLACEHOLDER1}},
      "name": "Create Vehicle Application",
      "url": "/vehicle/v1/_create",
      "displayName": "Create Vehicle",
      "orderNumber": 0,
      "enabled": false,
      "serviceCode": "vehicle",
      "code": "null",
      "path": ""
    },
    {
      "id":  {{PLACEHOLDER2}},
      "name": "Search Vehicle Application",
      "url": "/vehicle/v1/_search",
      "displayName": "Search  Vehicle",
      "orderNumber": 1,
      "enabled": false,
      "serviceCode": "vehicle",
      "code": "null",
      "path": ""
    },
    {
      "id": {{PLACEHOLDER3}},
      "name": "Vehicle Trip Search",
       "url": "/vehicle/trip/v1/_search",
      "displayName": "Vehicle Trip Search",
      "orderNumber": 1,
      "parentModule": "",
      "enabled": false,
      "serviceCode": "",
      "code": "null",
      "path": ""
    },
    {
      "id": {{PLACEHOLDER4}},
      "name": "Vehicle Trip Update",
       "url": "/vehicle/trip/v1/_update",
      "displayName": "Vehicle Trip Update",
      "orderNumber": 1,
      "parentModule": "",
      "enabled": false,
      "serviceCode": "",
      "code": "null",
      "path": ""
    }
```

**Role Action Mapping**

```
[
  {
    "rolecode": "FSM_ADMIN",
    "actionid": {{PLACEHOLDER1}},
    "actioncode": "",
    "tenantId": "pb"
  },
  {
    "rolecode": "FSM_ADMIN",
    "actionid": {{PLACEHOLDER2}},
    "actioncode": "",
    "tenantId": "pb"
  },
  {
    "rolecode": "FSM_DSO",
    "actionid":  {{PLACEHOLDER2}},
    "actioncode": "",
    "tenantId": "pb"
  },
  {
    "rolecode": "FSM_EDITOR_EMP",
    "actionid":  {{PLACEHOLDER2}},
    "actioncode": "",
    "tenantId": "pb"
  },
  {
    "rolecode": "FSM_VIEW_EMP",
    "actionid":  {{PLACEHOLDER2}},
    "actioncode": "",
    "tenantId": "pb"
  },
  {
    "rolecode": "FSM_EMP_FSTPO",
    "actionid":  {{PLACEHOLDER2}},
    "actioncode": "",
    "tenantId": "pb"
  },
  {
    "rolecode": "FSM_EMP_FSTPO",
    "actionid": {{PLACEHOLDER3}},
    "actioncode": "",
    "tenantId": "pb"
  },
  {
    "rolecode": "FSM_EMP_FSTPO",
    "actionid":{{PLACEHOLDER4}},
    "actioncode": "",
    "tenantId": "pb"
  }
]
```

### **Infra Ops Configuration**

Configurations that we can manage through values.yml vehicle in infraops repo are **** listed below. \
values.yml for the vehicle can be found.

|                                                                                |                                                   |                                                              |
| ------------------------------------------------------------------------------ | ------------------------------------------------- | ------------------------------------------------------------ |
| **Description**                                                                | **name in values.yml**                            | **Current Value**                                            |
| id-gen host, to generate the application number                                | EGOV\_IDGEN\_HOST                                 | egov-idgen from egov-service-host                            |
| mdms service host                                                              | EGOV\_MDMS\_HOST                                  | egov-mdms-service from egov-service-host                     |
| workflow v2 service host                                                       | WORKFLOW\_CONTEXT\_PATH                           | egov-workflow-v2 from egov-service-host                      |
| user service host, to get the locale data                                      | EGOV\_USER\_HOST                                  | egov-user from egov-service-host                             |
| Kafka Consumer Group                                                           | SPRING\_KAFKA\_CONSUMER\_GROUP\_ID                | egov-vehicle-services                                        |
| kafka topic to which service push data to save new vehicle application         | PERSISTER\_SAVE\_VEHICLE\_TOPIC                   | save-vehicle-application                                     |
| kafka topic to which service push data of the vehicleTrip to save              | PERSISTER\_SAVE\_VEHICLE\_TRIP\_TOPIC             | save-vehicle-trip                                            |
| kafka topic to which service push data of the vehicleTrip to update            | PERSISTER\_UPDATE\_VEHICLE\_TRIP\_TOPIC           | update-vehicle-trip                                          |
| kafka topic to which service push data of the vehicleTrip to update the status | PERSISTER\_UPDATE\_VEHICLE\_TRIP\_WORKFLOW\_TOPIC | update-workflow-vehicle-trip                                 |
| VehicleTrip Appilcatiion Number format\`                                       | egov.idgen.vehicle.trip.applicationNum.format     | "\[CITY.CODE]-VT-\[cy:yyyy-MM-dd]-\[SEQ\_EGOV\_VEHICLETRIP]" |

**Configurations sample in Values.yml**

```
egov.idgen.vehicle.trip.applicationNum.format: "[CITY.CODE]-VT-[cy:yyyy-MM-dd]-[SEQ_EGOV_VEHICLETRIP]"

# Additional Container Envs
env: |
  - name: EGOV_IDGEN_HOST
    valueFrom:
      configMapKeyRef:
        name: egov-service-host
        key: egov-idgen
  - name: EGOV_HRMS_HOST
    valueFrom:
      configMapKeyRef:
        name: egov-service-host
        key: egov-hrms
  - name: EGOV_MDMS_HOST
    valueFrom:
      configMapKeyRef:
        name: egov-service-host
        key: egov-mdms-service
  - name: EGOV_USER_HOST
    valueFrom:
      configMapKeyRef:
        name: egov-service-host
        key: egov-user
  - name: WORKFLOW_CONTEXT_PATH
    valueFrom:
      configMapKeyRef:
        name: egov-service-host
        key: egov-workflow-v2
  - name: WORKFLOW_TRANSITION_PATH
    value: "egov-workflow-v2/egov-wf/process/_transition"
  - name: EGOV_IDEN_VEHICLE_TRIP_APPLICATIONNUM_FORMAT
    value: "[CITY.CODE]-VT-[cy:yyyy-MM-dd]-[SEQ_EGOV_VEHICLETRIP]"
  - name: SPRING_KAFKA_CONSUMER_GROUP_ID
    value: egov-vehicle-services
  - name: PERSISTER_SAVE_VEHICLE_TOPIC
    value: save-vehicle-application
  - name: PERSISTER_UPDATE_VEHICLE_TOPIC
    value: update-vehicle-application
  - name: PERSISTER_SAVE_VEHICLE_TRIP_TOPIC
    value: save-vehicle-trip
  - name: PERSISTER_UPDATE_VEHICLE_TRIP_TOPIC
    value: update-vehicle-trip
  - name: PERSISTER_UPDATE_VEHICLE_TRIP_WORKFLOW_TOPIC
    value: update-workflow-vehicle-trip 
  - name: SPRING_KAFKA_PRODUCER_KEY_SERIALIZER
    value: org.apache.kafka.common.serialization.StringSerializer
  - name: SPRING_KAFKA_PRODUCER_VALUE_SERIALIZER
    value: org.springframework.kafka.support.serializer.JsonSerializer
  - name: JAVA_OPTS
    value: {{ index .Values "heap" | quote }}
  - name: JAVA_ARGS
    value: {{ index .Values "java-args" | quote }}
  - name: SERVER_PORT
    value: "8080"
  - name: SECURITY_BASIC_ENABLED
    value: "false"  
  - name: MANAGEMENT_SECURITY_ENABLED
    value: "false"
  {{- if index .Values "tracing-enabled" }}
  - name: TRACER_OPENTRACING_ENABLED
    value: "true" 
  {{- end }}
```

### Data Setup <a href="#data-setup" id="data-setup"></a>

#### Create Vehicle <a href="#create-vehicle" id="create-vehicle"></a>

Create Vehicle with one of the vehicle types available in the VehicleMakeModel MDMS

**Sample Curl**

```
curl --location --request POST 'https://dev.digit.org/vehicle/v1/_create' \
--header 'Content-Type: application/json' \
--data-raw '{
    "RequestInfo": {
        "apiInfo": {
            "id": "string",
            "version": "string",
            "path": "string"
        },
        "deviceDetail": {
            "id": "string",
            "signature": "string"
        },
        "ts": 0,
        "action": "string",
        "key": "string",
        "msgId": "string",
        "requesterId": "string",
        "authToken": "a35b5ba7-2d5f-4272-8a67-0303cfab2c9f"
    },
    "vehicle": {
        "tenantId": "pb.amritsar",
        "registrationNumber": "TS 09 PA 2466",
        "model":"1998",
        "type":"TRUCK",
        "tankCapacity":"2000",
        "suctionType":"SEWER_SUCTION_MACHINE",
        "vehicleOwner": "ULB",
        "pollutionCertiValidTill":1611584416772,
        "InsuranceCertValidTill":1611584416772,
        "fitnessValidTill":1611584416772,
        "roadTaxPaidTill":1611584416772,
        "gpsEnabled":true,
        "source":"Municipal records",
        "owner": {

            "tenantId": "pb.amritsar",
            "name": "DSO1",
            "fatherOrHusbandName": "Phani",
            "relationship": "FATHER",
            "gender": "MALE",
            "dob": 550261800000,
            "emailId": "test@dso.test",
            "correspondenceAddress": "KPHB",
            "mobileNumber": 8919146630
        }
    }
}'
```

## Integration <a href="#integration" id="integration"></a>

### Integration Scope <a href="#integration-scope" id="integration-scope"></a>

Integrated with Application through REST API to create, and search vehicles. For any module where vehicle Trip is required, can integrate REST API trip/v1/create, update, search

### Integration Benefits <a href="#integration-benefits" id="integration-benefits"></a>

* Vehicle Managed would become easy
* Trip Management would become easy

### Steps to Integration <a href="#steps-to-integration" id="steps-to-integration"></a>

* FSM Application can vehicle/v1/\_search to validate the **FSM** vehicle assignment
* FSM Application call vehicle/trip/v1/\_create on assigning vehicle to the Application
* FSTP operator can mark the vehicleTrip as DISPOSED.

### Interaction Diagram <a href="#interaction-diagram" id="interaction-diagram"></a>

coming up....

## Reference Docs <a href="#reference-docs" id="reference-docs"></a>

### Doc Links <a href="#doc-links" id="doc-links"></a>

|                                     |                                                                                                                                                                   |
| ----------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Title**                           | **Link**                                                                                                                                                          |
| Workflow Technical Document         | [Workflow Service](../../../../platform/configure-digit/services-overview/core-services/workflow-services.md)                                                     |
| User Technical Document             | User Service                                                                                                                                                      |
| MDMS Technical Document             | **NEEDS TO BE UPDATED**                                                                                                                                           |
| IDGen Technical Document            | **NEEDS TO BE UPDATED**                                                                                                                                           |
| Localization Technical Document     | **NEEDS TO BE UPDATED**                                                                                                                                           |
| Persister Technical Document        | **NEEDS TO BE UPDATED**                                                                                                                                           |
| SMS Notification Technical Document | **NEEDS TO BE UPDATED**                                                                                                                                           |
| API Contract                        | [API Contract](https://editor.swagger.io/?url=https://raw.githubusercontent.com/egovernments/municipal-services/master/docs/fsm/Vehicle\_Registry\_Contract.yaml) |
| Postman Scripts                     | [Postman Collection](https://www.getpostman.com/collections/d2541409b9570e53ed26)                                                                                 |

### API List <a href="#api-list" id="api-list"></a>

|                               |                                                                                                                                                    |
| ----------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------- |
| Title                         | **Link**                                                                                                                                           |
| vehicle/v1/\_create           | [https://www.getpostman.com/collections/6d99bb40022396f848b2](https://www.getpostman.com/collections/6d99bb40022396f848b2)                         |
| vehicle/v1/\_search           | [https://www.getpostman.com/collections/6d99bb40022396f848b2](https://www.getpostman.com/collections/6d99bb40022396f848b2)                         |
| /vehicle/v1/\_plainsearch     | [https://www.getpostman.com/collections/6d99bb40022396f848b2](https://www.getpostman.com/collections/6d99bb40022396f848b2)                         |
| vehicle/trip/v1/\_create      | <p><a href="https://www.getpostman.com/collections/6d99bb40022396f848b2">	<br>https://www.getpostman.com/collections/6d99bb40022396f848b2</a></p> |
| vehicle/trip/v1/\_update      | [https://www.getpostman.com/collections/6d99bb40022396f848b2](https://www.getpostman.com/collections/6d99bb40022396f848b2)                         |
| vehicle/trip/v1/\_search      | [https://www.getpostman.com/collections/6d99bb40022396f848b2](https://www.getpostman.com/collections/6d99bb40022396f848b2)                         |
| vehicle/trip/v1/\_plainsearch | [https://www.getpostman.com/collections/6d99bb40022396f848b2](https://www.getpostman.com/collections/6d99bb40022396f848b2)                         |

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation ](https://egov.org.in/)is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).
