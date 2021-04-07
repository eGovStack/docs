# Access Control Services

### Overview

DIGIT is API based Platform here each API is denoting to a DIGIT resource. Access Control Service \(ACS\) primary job is to authorise end-user based on their roles and provide access to the DIGIT platform resources. Access control functionality basically works based on below points:

**Actions:** Actions are events which are performed by a user. This can be an API end-point or Frontend event. This is MDMS master

**Roles:** Role are assigned to the user, a user can hold multiple roles. Roles are defined in MDMS masters.

**Role-Action:** Role actions are mapping b/w Actions and Roles. Based on role, action mapping access control service identifies applicable action for the role.

### Pre-requisites

Before you proceed with the configuration, make sure the following pre-requisites are met -

* Java 8
* MDMS service is up and running

### Key Functionalities

* Serve the applicable actions for a user based on user role \(To print menu three\).
* On each action which is performed by a user, access control looks at the roles for the user and validate actions mapping with the role.
* Support tenant-level role-action. For instance, an employee from Amritsar can have a role of APPROVER for other ULB like Jalandhar and hence will be authorised to act as APPROVER in Jalandhar.

### Deployment Details

1. Deploy the latest version of Access Control Service
2. Deploy MDMS service to fetch the Role Action Mappings

### Configuration Details

Define the roles

```text
{
      "code": "EMPLOYEE",
      "name": "Employee",
      "description": "Default role for all employees"
}
```

Add the Actions \(URL\)

```text
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

```text
{
      "rolecode": "EMPLOYEE",
      "actionid": {{ACTION_ID}},
      "actioncode": "",
      "tenantId": "pb"
    }
```

_\(The details about the fields in the configuration can be found in the swagger contract\)_

### Integration Details

#### Integration Scope

Any microservice which requires authorisation can leverage the functionalities provided by access control service.

#### Integration Benefits

Any new microservice that is to be added in the platform won’t have to worry about authorisation. It can just add it’s role action mapping in the master data and Access Control Service will perform authorisation whenever API for the microservice is called.

#### Steps to Integration

1. To integrate with Access Control Service the role action mapping has to be configured\(added\) in the MDMS service.
2. The service needs to call /actions/\_authorize API of Access Control Service to check for authorisation of any request

#### Interaction Diagram

![](../../../.gitbook/assets/image%20%2878%29.png)

### Reference Docs

#### Doc Links

| **Title** | **Link** |
| :--- | :--- |
| API Contract | [https://raw.githubusercontent.com/egovernments/egov-services/master/docs/egov-accesscontrol/contracts/v1-0-1.yml](https://raw.githubusercontent.com/egovernments/egov-services/master/docs/egov-accesscontrol/contracts/v1-0-1.yml) |

#### API List

| Title | **Link** |
| :--- | :--- |
|  |  |
|  |  |

