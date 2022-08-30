---
description: Details for registering new vendors
---

# FSM Vendor Registry v1.1

## Overview <a href="#overview" id="overview"></a>

Vendor Registry is a system that enables ULB Employees to create and search for vendors i.e Desludging Operators (DSO), drivers linked to appropriate vehicle entities for FSM Application. This document contains details about how to set up the vendors and describes the functionalities provided.

## Pre-requisites <a href="#pre-requisites" id="pre-requisites"></a>

Before you proceed with the configuration, make sure the following pre-requisites are met -

* Java 8
* Kafka server is up and running
* egov-persister service is running and has fsm-calculator-persister config path added in it
* PSQL server is running and a database is created to store FSM Application data
* Following services should be up and running:
  * egov-mdms-service
  * egov-user-service
  * boundary-service
  * vehicle

## Key Functionalities <a href="#key-functionalities" id="key-functionalities"></a>

1. Added payment preference and agency attributes for DSO
2. Added gender attribute in the create and update APIs for Vendor
3. Updated the Vendor search API to add vehicle capacity in the search parameter - this will enable users to search vendors matching the vehicle capacity specified in the search parameter.

## Deployment Details <a href="#deployment-details" id="deployment-details"></a>

1. Deploy the latest version of FSM
2. Add vehicle-persister.yml file in config folder in git and add that path in persister. _(The file path is to be added in the environment yaml file in param called_ persist-yml-path _)_

## Configuration Details <a href="#configuration-details" id="configuration-details"></a>

### MDMS Configuration

NA

### Business Service / Workflow Configuration <a href="#business-service-workflow-configuration" id="business-service-workflow-configuration"></a>

NA

### Actions & Role Action Mapping <a href="#actions-and-role-action-mapping" id="actions-and-role-action-mapping"></a>

After adding Actions and role-action mappings, restart the `egov-mdms-service`

**Actions**

```
{
      "id": {{PLACEHOLDER1}},
      "name": "Create Vendor/DSO",
      "url": "/vendor/v1/_create",
      "displayName": "Create Vehicle",
      "orderNumber": 0,
      "enabled": false,
      "serviceCode": "vendor",
      "code": "null",
      "path": ""
    },
    {
      "id": {{PLACEHOLDER1}},
      "name": "Search Vendor/DSO",
      "url": "/vendor/v1/_search",
      "displayName": "Search  Vendor",
      "orderNumber": 1,
      "enabled": false,
      "serviceCode": "vendor",
      "code": "null",
      "path": ""
    },
```

**Role Action Mapping**

```
[
  {
    "rolecode": "FSM_ADMIN",
    "actionid": "{{PLACEHOLDER1}}",
    "actioncode": "",
    "tenantId": "pb"
  },
  {
    "rolecode": "FSM_ADMIN",
    "actionid": "{{PLACEHOLDER2}}",
    "actioncode": "",
    "tenantId": "pb"
  },
  {
    "rolecode": "FSM_DSO",
    "actionid": "{{PLACEHOLDER2}}",
    "actioncode": "",
    "tenantId": "pb"
  },
  {
    "rolecode": "FSM_EDITOR_EMP",
    "actionid": "{{PLACEHOLDER2}}",
    "actioncode": "",
    "tenantId": "pb"
  },
  {
    "rolecode": "FSM_VIEW_EMP",
    "actionid": "{{PLACEHOLDER2}}",
    "actioncode": "",
    "tenantId": "pb"
  },
  {
    "rolecode": "FSM_EMP_FSTPO",
    "actionid": "{{PLACEHOLDER2}}",
    "actioncode": "",
    "tenantId": "pb"
  },
  {
    "rolecode": "CITIZEN",
    "actionid": "{{PLACEHOLDER2}}",
    "actioncode": "",
    "tenantId": "pb"
  }
]
```

### **Infra Ops Configuration**

Configurations that we can manage through values.yml vehicle in infraops repo are listed below.\
values.yml for the vehicle is available below.

|                                                           |                                    |                                          |
| --------------------------------------------------------- | ---------------------------------- | ---------------------------------------- |
| **Description**                                           | **name in values.yml**             | **Current Value**                        |
| Kafka Consumer Group                                      | SPRING\_KAFKA\_CONSUMER\_GROUP\_ID | egov-vendor-services                     |
| kafka topic to which service push data to save new Vendor | PERSISTER\_SAVE\_VENDOR\_TOPIC     | save-vendor-application                  |
| mdms service host                                         | EGOV\_MDMS\_HOST                   | egov-mdms-service from egov-service-host |
| Vehicle Service host                                      | EGOV\_VEHICLE\_HOST                | vehicle from egov-service-host           |
| User service host                                         | EGOV\_USER\_HOST                   | egov-user-service from egov-service-host |
| Location Service Host                                     | EGOV\_LOCATION\_HOST               | egov-location from egov-service-host     |

**Configurations sample in Values.yml**

```
# Common Labels
labels:
  app: "vendor"
  group: "rainmaker"

# Ingress Configs
ingress:
  enabled: true
  zuul: true
  context: "vendor"

# Init Containers Configs
initContainers:
  dbMigration:
    enabled: true
    schemaTable: "vendor_schema"
    image:
      repository: "vendor-db"

# Container Configs
image:
  repository: "vendor"
replicas: "1"
healthChecks:
  enabled: true
  livenessProbePath: "/vendor/health"
  readinessProbePath: "/vendor/health"
appType: "java-spring"
tracing-enabled: true
heap: "-Xmx256m -Xms256m"
java-args: "-Dspring.profiles.active=monitoring"

# Additional Container Envs
env: |
  - name: EGOV_VEHICLE_HOST
    valueFrom:
      configMapKeyRef:
        name: egov-service-host
        key: vehicle
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
  - name: EGOV_LOCATION_HOST
    valueFrom:
      configMapKeyRef:
        name: egov-service-host
        key: egov-location
  - name: EGOV_HRMS_HOST
    valueFrom:
      configMapKeyRef:
        name: egov-service-host
        key: egov-hrms
  - name: SPRING_KAFKA_CONSUMER_GROUP_ID
    value: egov-vendor-services
  - name: PERSISTER_SAVE_VENDOR_TOPIC
    value: save-vendor-application
  - name: PERSISTER_UPDATE_VENDOR_TOPIC
    value: update-vendor-application
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

DSO for FSM System is a vendor. For every city/ULB, DSO is created with the representative details as owner, associated vehicles and drivers.

Sample Curl

```
curl --location --request POST 'https://dev.digit.org/vendor/v1/_create' \
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
    "vendor": {
        "tenantId": "pb.amritsar",
        "name": "DSO TATA1",
        "address": { 
            "tenantId": "pb.amritsar",
            "doorNo": "my door",
            "plotNo": "my plot",
            "landmark": "my landmark",
            "city": "amritsar",
            "district": "amritsar",
            "region": "amritsar",
            "state": "punjab",
            "country": "in",
            "pincode": "143001",
            "additionDetails": null,
            "buildingName": "my building",
            "street": "my streat",
            "locality": {
                "code": "SUN178",
                "name": "Mohalla Singh kia - Area2",
                "label": "Locality",
                "latitude": null,
                "longitude": null,
                "area": "Area2",
                "pincode": null,
                "boundaryNum": 1,
                "children": []
            },
            "geoLocation": {
                "latitude": 0,
                "longitude": 0,
                "additionalDetails": {}
            }
        },
        "owner": {

            "tenantId": "pb.amritsar",
            "name": "DSOc4",
            "fatherOrHusbandName": "Phani",
            "relationship": "FATHER",
            "gender": "MALE",
            "dob": 550261800000,
            "emailId": "test@dso.test",
            "correspondenceAddress": "KPHB",
            "mobileNumber": 8919146603
        },
        "vehicles": [{
        "tenantId": "pb.amritsar",
        "registrationNumber": "TS 09 PA 3586",
        "model":"1998",
        "type":"TATA.407",
        "tankCapacity":"2000",
        "suctionType":"SEWER_SUCTION_MACHINE",
        "pollutionCertiValidTill":1611584416772,
        "InsuranceCertValidTill":1611584416772,
        "fitnessValidTill":1611584416772,
        "roadTaxPaidTill":1611584416772,
        "gpsEnabled":true,
        "source":"Municipal records",
        "owner": {

            "tenantId": "pb.amritsar",
            "name": "DSOc4",
            "fatherOrHusbandName": "Phani",
            "relationship": "FATHER",
            "gender": "MALE",
            "dob": 550261800000,
            "emailId": "test@dso.test",
            "correspondenceAddress": "KPHB",
            "mobileNumber": 8919146617
        }
    },{
        "tenantId": "pb.amritsar",
        "registrationNumber": "TS 09 PA 2584",
        "model":"1998",
        "type":"MAHINDRA.BOLERO_PICKUP",
        "tankCapacity":"2000",
        "suctionType":"SEWER_SUCTION_MACHINE",
        "pollutionCertiValidTill":1611584416772,
        "InsuranceCertValidTill":1611584416772,
        "fitnessValidTill":1611584416772,
        "roadTaxPaidTill":1611584416772,
        "gpsEnabled":true,
        "source":"Municipal records",
        "owner": {

            "tenantId": "pb.amritsar",
            "name": "DSOc3",
            "fatherOrHusbandName": "Phani",
            "relationship": "FATHER",
            "gender": "MALE",
            "dob": 550261800000,
            "emailId": "test@dso.test",
            "correspondenceAddress": "KPHB",
            "mobileNumber": 8919146617
        }
    }],
        "drivers": [{

            "tenantId": "pb.amritsar",
            "name": "DriverDSO4",
            "fatherOrHusbandName": "Phani",
            "relationship": "FATHER",
            "gender": "MALE",
            "dob": 550261800000,
            "emailId": "test@dso.test",
            "correspondenceAddress": "KPHB",
            "mobileNumber": 8919146216
        },{

            "tenantId": "pb.amritsar",
            "name": "DriverDSO3",
            "fatherOrHusbandName": "Phani",
            "relationship": "FATHER",
            "gender": "MALE",
            "dob": 550261800000,
            "emailId": "test@dso.test",
            "correspondenceAddress": "KPHB",
            "mobileNumber": 8919146216
        }],
        "source": "WhatsApp"
    }
}'
```

## Integration <a href="#integration" id="integration"></a>

### Integration Scope <a href="#integration-scope" id="integration-scope"></a>

Any system or digit module can be integrated with Vendor Service. It helps manage the Vendor with the vehicles, drivers and owners for the representative and login for the representative/owner to login into the system to carry out role-specific operations.

### Integration Benefits <a href="#integration-benefits" id="integration-benefits"></a>

* Validation of DSO/Vendor availability
* Fetch the vehicle assigned to the DSO
* Fetch the Drivers assigned to the DSO

### Steps to Integration <a href="#steps-to-integration" id="steps-to-integration"></a>

* FSM to call vendor/v1/\_search to fetch the DSOs
* FSM can call vendor/v1/\_search to fetch the DSOs and the respective vehicles and drivers

### Interaction Diagram <a href="#interaction-diagram" id="interaction-diagram"></a>

TBD

## Reference Docs <a href="#reference-docs" id="reference-docs"></a>

### Doc Links <a href="#doc-links" id="doc-links"></a>

|                                     |                                                                                                                                                                                       |
| ----------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Title**                           | **Link**                                                                                                                                                                              |
| Workflow Technical Document         | [Workflow Service](../../../../configure-digit/services-overview/core-services/workflow-services.md)                                                                                  |
| User Technical Document             | [User Service](../../../../configure-digit/services-overview/core-services/user-services.md)                                                                                          |
| MDMS Technical Document             | **NEEDS TO BE UPDATED**                                                                                                                                                               |
| IDGen Technical Document            | **NEEDS TO BE UPDATED**                                                                                                                                                               |
| Localization Technical Document     | **NEEDS TO BE UPDATED**                                                                                                                                                               |
| Persister Technical Document        | **NEEDS TO BE UPDATED**                                                                                                                                                               |
| SMS Notification Technical Document | **NEEDS TO BE UPDATED**                                                                                                                                                               |
| API Contract                        | [API Contract](https://editor.swagger.io/?url=https://raw.githubusercontent.com/egovernments/DIGIT-OSS/master/municipal-services/docs/fsm/Vendor\_Registration\_Contract-v1.1.0.yaml) |
| Postman Scripts                     | [Postman Collection](https://www.getpostman.com/collections/c79e98843bcdcc873d09)                                                                                                     |

#### API List <a href="#api-list" id="api-list"></a>

|                          |                                                                                                                            |
| ------------------------ | -------------------------------------------------------------------------------------------------------------------------- |
| Title                    | **Link**                                                                                                                   |
| /vendor/v1/\_create      | [https://www.getpostman.com/collections/c79e98843bcdcc873d09](https://www.getpostman.com/collections/c79e98843bcdcc873d09) |
| /vendor/v1/\_search      | [https://www.getpostman.com/collections/c79e98843bcdcc873d09](https://www.getpostman.com/collections/c79e98843bcdcc873d09) |
| /vendor/v1/\_plainsearch | [https://www.getpostman.com/collections/c79e98843bcdcc873d09](https://www.getpostman.com/collections/c79e98843bcdcc873d09) |

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation ](https://egov.org.in/)is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).
