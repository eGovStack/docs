# Access Control Services

## Overview

DIGIT is an API-based platform where each API denotes a DIGIT resource. Access Control Service's (ACS) primary job is to authorise end-user based on their roles and provide access to the DIGIT platform resources. Access control functionality basically works based on the below points:

**Actions:** Actions are events which are performed by a user. This can be an API end-point or a Frontend event. This is the MDMS master.

**Roles:** Roles are assigned to the user, a user can hold multiple roles. Roles are defined in MDMS masters.

**Role-Action:** Role action is the mapping between actions and roles. Based on the role, the action mapping access control service identifies applicable actions for the role.

## Pre-requisites

Before you proceed with the configuration, make sure the following pre-requisites are met -

* Java 8
* MDMS service is up and running

## Key Functionalities

* Serve the applicable actions for a user based on user role (To print menu three).
* On each action which is performed by a user, access control looks at the roles for the user and validates actions mapping with the role.
* Support tenant-level role-action. For instance, an employee from Amritsar can have the role of APPROVER for other ULBs like Jalandhar and hence will be authorised to act as APPROVER in Jalandhar.

## Deployment Details

1. Deploy the latest version of the Access Control Service
2. Deploy MDMS service to fetch the Role Action Mappings

## Configuration Details

Define the roles

```
{
      "code": "EMPLOYEE",
      "name": "Employee",
      "description": "Default role for all employees"
}
```

Add the Actions (URL)

```
{
      "id": {{ACTION_ID}},
      "name": "Create TradeLicense",
      "url": "/tl-services/v1/_create",
      "parentModule": "",
      "displayName": "Create TradeLicense",
      "orderNumber": 0,
      "enabled": false,
      "serviceCode": "tl-services",
      "code": "null",
      "path": ""
}
```

Add the role action mapping

```
{
      "rolecode": "EMPLOYEE",
      "actionid": {{ACTION_ID}},
      "actioncode": "",
      "tenantId": "pb"
    }
```

_(The details about the fields in the configuration can be found in the swagger contract)_

## Integration Details

### Integration Scope

Any microservice which requires authorisation can leverage the functionalities provided by the access control service.

### Integration Benefits

Any new microservice that is to be added to the platform won’t have to worry about authorisation. It can just add its role action mapping in the master data and Access Control Service will perform authorisation whenever API for the microservice is called.

### Steps to Integration

1. To integrate with Access Control Service the role action mapping has to be configured(added) in the MDMS service.
2. The service needs to call /actions/\_authorize API of Access Control Service to check for authorisation of any request

## Interaction Diagram

![](<../../../.gitbook/assets/image (78).png>)

## Reference Docs

### Doc Links

| Description  | Link                                                                                                                                                                                                                                 |
| ------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| API Contract | [https://raw.githubusercontent.com/egovernments/egov-services/master/docs/egov-accesscontrol/contracts/v1-0-1.yml](https://raw.githubusercontent.com/egovernments/egov-services/master/docs/egov-accesscontrol/contracts/v1-0-1.yml) |

### API List

| Description | Link |
| ----------- | ---- |
|             |      |

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation ](https://egov.org.in/)is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).
