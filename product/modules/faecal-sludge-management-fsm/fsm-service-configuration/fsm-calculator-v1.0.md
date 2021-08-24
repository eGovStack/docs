---
description: Details for setting up FSM calculator service
---

# FSM Calculator v1.0

## Overview <a id="Overview"></a>

FSM Calculator is a system that enables FSM Admin to create billing slab for the FSM application\(s\) with different combination of propertyType , slum , tank capacity and etc..

Generates the Demand after calculating the charges for the given application using the billing slab already configured. This document contains the details about how to setup the fsm-calculator service and description the functionalities it provides.

## Pre-requisites <a id="Pre-requisites"></a>

Before you proceed with the configuration, make sure the following pre-requisites are met -

* _Java 8_
* Kafka server is up and running
* egov-persister service is running and has fsm-calculator-persister config path added in it
* PSQL server is running and database is created to store FSM Application data
* Following services should be up and running:
  * egov-perister
  * egov-mdms
  * fsm
  * billing-service

## Key Functionalities <a id="Key-Functionalities"></a>

* FSM Admin an Employee of ULB with FSM Admin role can create, update billing slab\(s\)
* ULB Employee with FSM\_CREATOR and FSM\_EDITOR can search billing slab\(s\)
* ULB Employee Citizen can file, track and rate the application for cleaning septic tank
* ULB Employee can get the estimate for FSM Application
* FSM service internally call fsm-calculator to generate a demand

## Deployment Details <a id="Deployment-Details"></a>

1. Deploy the latest version of fsm
2. Add fsm-calculator-persister.yml file in config folder in git and add that path in persister . _\(The file path is to be added in environment yaml file in param called_ persist-yml-path _\)_

## Configuration Details <a id="Configuration-Details"></a>

### MDMS Configuration <a id="MDMS-Configuration[hardBreak]"></a>

FSM MDMS Configuration is sufficient

### Business Service / Workflow Configuration <a id="Business-Service-/-Workflow-Configuration"></a>

NA

### Actions & Role Action Mapping <a id="Actions-&amp;-Role-Action-Mapping"></a>

**Actions**

```text
[
  {
    "id": {{PLACEHOLDER1}},
    "name": "FSM BillingSlab Create",
    "url": "/fsm-calculator/v1/billingSlab/_create",
    "displayName": "FSM BillingSlab Create",
    "orderNumber": 1,
    "parentModule": "",
    "enabled": false,
    "serviceCode": "",
    "code": "null",
    "path": ""
  },
  {
    "id": {{PLACEHOLDER2}},
    "name": "FSM BillingSlab Update",
    "url": "/fsm-calculator/v1/billingSlab/_update",
    "displayName": "FSM BillingSlab Update",
    "orderNumber": 1,
    "parentModule": "",
    "enabled": false,
    "serviceCode": "",
    "code": "null",
    "path": ""
  },
  {
    "id": {{PLACEHOLDER3}},
    "name": "FSM BillingSlab Search",
    "url": "/fsm-calculator/v1/billingSlab/_search",
    "displayName": "FSM BillingSlab Search",
    "orderNumber": 1,
    "parentModule": "",
    "enabled": false,
    "serviceCode": "",
    "code": "null",
    "path": ""
  },
  {
    "id": {{PLACEHOLDER4}},
    "name": "FSM Estimate",
    "url": "/fsm-calculator/v1/_estimate",
    "displayName": "FSM Estimate",
    "orderNumber": 1,
    "parentModule": "",
    "enabled": false,
    "serviceCode": "",
    "code": "null",
    "path": ""
  }
]
```

**Role Action Mapping**

```text
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
    "rolecode": "FSM_CREATOR_EMP",
    "actionid": "{{PLACEHOLDER3}}",
    "actioncode": "",
    "tenantId": "pb"
  },
  {
    "rolecode": "FSM_EDITOR_EMP",
    "actionid": "{{PLACEHOLDER3}}",
    "actioncode": "",
    "tenantId": "pb"
  },
  {
    "rolecode": "FSM_ADMIN",
    "actionid": "{{PLACEHOLDER3}}",
    "actioncode": "",
    "tenantId": "pb"
  },
  {
    "rolecode": "FSM_DSO",
    "actionid": "{{PLACEHOLDER3}}",
    "actioncode": "",
    "tenantId": "pb"
  },
  {
    "rolecode": "FSM_CREATOR_EMP",
    "actionid": "{{PLACEHOLDER4}}",
    "actioncode": "",
    "tenantId": "pb"
  },
  {
    "rolecode": "FSM_EDITOR_EMP",
    "actionid": "{{PLACEHOLDER4}}",
    "actioncode": "",
    "tenantId": "pb"
  },
  {
    "rolecode": "FSM_ADMIN",
    "actionid": "{{PLACEHOLDER4}}",
    "actioncode": "",
    "tenantId": "pb"
  }
]
```

**Infra Ops Configuration**

Configurations that we can manage through values.yml fsm-calculator in infraops repo as follows  
values.yml for fms-calculator can be found [here](https://github.com/egovernments/eGov-infraOps/blob/master/helm/charts/municipal-services/fsm-calculator/values.yaml)

| **Description** | **name in values.yml** | **Current Value** |
| :--- | :--- | :--- |
| contextPath of the api’s | SERVER\_CONTEXTPATH | /fsm-calculator |
| Kafka Consumer Group | SPRING\_KAFKA\_CONSUMER\_GROUP\_ID | fsm-calculator |
| kafka topic to which service push data to save new billing slab | PERSISTER\_SAVE\_BILLING\_SLAB\_TOPIC | save-fsm-billing-slab |
| kafka topic to which service push data to update the existing billing slab | PERSISTER\_UPDATE\_BILLING\_SLAB\_TOPIC | update-fsm-billing-slab |
| mdms service host | EGOV\_MDMS\_HOST | egov-mdms-service from egov-service-host |
| billing-service host | EGOV\_BILLINGSERVICE\_HOST | billing-service from egov-service-host |
| fsm service host | EGOV\_FSM\_HOST | fsm from egov-service-host |

**Configurations sample in Values.yml**

```text
  - name: SERVER_CONTEXTPATH
    value: /fsm-calculator
  - name: SPRING_KAFKA_CONSUMER_GROUP_ID
    value: fsm-calculator
  - name: PERSISTER_SAVE_BILLING_SLAB_TOPIC
    value: save-fsm-billing-slab
  - name: PERSISTER_UPDATE_BILLING_SLAB_TOPIC
    value: update-fsm-billing-slab
  - name: SPRING_KAFKA_PRODUCER_KEY_SERIALIZER
    value: org.apache.kafka.common.serialization.StringSerializer
  - name: SPRING_KAFKA_PRODUCER_VALUE_SERIALIZER
    value: org.springframework.kafka.support.serializer.JsonSerializer
  - name: EGOV_MDMS_HOST
    valueFrom:
      configMapKeyRef:
        name: egov-service-host
        key: egov-mdms-service
  - name: EGOV_BILLINGSERVICE_HOST
    valueFrom:
      configMapKeyRef:
        name: egov-service-host
        key: billing-service
  - name: EGOV_FSM_HOST
    valueFrom:
      configMapKeyRef:
        name: egov-service-host
        key: fsm
```

## Data Setup <a id="Data-Setup"></a>

### Billing Slab Setup <a id="Billing-Slab-Setup"></a>

Create Billing Slab with _\*\*_a combination of PropertyType refer values form [PropertyType Mdms](https://github.com/egovernments/egov-mdms-data/blob/DEV/data/pb/FSM/PropertyType.json), Slum \( YES/NO\), capacityFrom and capacityTo refers to Vehicle Tank Capacity.

Sample Curl

```text
curl --location --request POST 'http://localhost:9098/fsm-calculator/v1/billingSlab/_create' \
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
   "billingSlab":{
            "tenantId": "pb.amritsar",
            "capacityFrom": 1000.00,
            "capacityTo": 50000.00,
            "propertyType": "RESIDENTIAL.ROW_HOUSES",
            "slum": "NO",
            "price": 9000.00,
            "status": "ACTIVE"
        },
    "workflow": null
}'
```

## Integration <a id="Integration"></a>

### Integration Scope <a id="Integration-Scope"></a>

FSM-calculator will be integrated with FSM Application. FSM Application internally invokes the fsm-calculator service to calculate and generate demand for the charges.

### Integration Benefits <a id="Integration-Benefits"></a>

* Calculation and demand generation logic will be separated from the FSM service. For each implementation, calculation implementation can be changed if required without modifying the fsm service.

### Steps to Integration <a id="Steps-to-Integration"></a>

1. FSM application to call fsm-calulator/v1/\_calculate to calculate and generate the demand for the fsm application
2. ULB Employee can call fsm-calculator/v1/\_estimate to get the estimates for the fsm application
3. ULB Employee can create billing slab calling fsm-calculator/v1/billingSlab/\_create
4. ULB Employee can update billing slab calling fsm-calculator/v1/billingSlab/\_update
5. ULB Employee can search billing slab calling fsm-calculator/v1/billingSlab/\_search

## Interaction Diagram <a id="Interaction-Diagram"></a>

TBD

## Reference Docs <a id="Reference-Docs"></a>

### Doc Links <a id="Doc-Links"></a>

| **Title** | **Link** |
| :--- | :--- |
| Workflow Technical Document | [Workflow Service](https://digit-discuss.atlassian.net/wiki/spaces/DD/pages/664174657/Workflow+Service) |
| User Technical Document | [User Service](https://digit-discuss.atlassian.net/wiki/spaces/DD/pages/669450371/User+Service) |
| MDMS Technical Document | **NEEDS TO BE UPDATED** |
| IDGen Technical Document | **NEEDS TO BE UPDATED** |
| Localization Technical Document | **NEEDS TO BE UPDATED** |
| Persister Technical Document | **NEEDS TO BE UPDATED** |
| SMS Notification Technical Document | **NEEDS TO BE UPDATED** |
| API Contract | [API Contract](https://editor.swagger.io/?url=https://raw.githubusercontent.com/egovernments/municipal-services/master/docs/fsm/Fsm_Apply_Contract.yaml) |
| Postman Scripts | [Postman Scripts](https://www.getpostman.com/collections/8b9eb951a810486f41a4) |

### API List <a id="API-List"></a>

| Title | **Link** |
| :--- | :--- |
| fsm-calulator/v1/\_calculate | [https://www.getpostman.com/collections/8b9eb951a810486f41a4](https://www.getpostman.com/collections/8b9eb951a810486f41a4) |
| fsm-calculator/v1/\_estimate | [https://www.getpostman.com/collections/8b9eb951a810486f41a4](https://www.getpostman.com/collections/8b9eb951a810486f41a4) |
| fsm-calculator/v1/billingSlab/\_create | [https://www.getpostman.com/collections/8b9eb951a810486f41a4](https://www.getpostman.com/collections/8b9eb951a810486f41a4) |
| fsm-calculator/v1/billingSlab/\_update | [https://www.getpostman.com/collections/8b9eb951a810486f41a4](https://www.getpostman.com/collections/8b9eb951a810486f41a4) |
| fsm-calculator/v1/billingSlab/\_search | [https://www.getpostman.com/collections/8b9eb951a810486f41a4](https://www.getpostman.com/collections/8b9eb951a810486f41a4) |

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation ](https://egov.org.in/)is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).

