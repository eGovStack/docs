# Mapping Roles With APIs

## Overview <a href="#overview" id="overview"></a>

Roles define the permissions of a user to perform a group of tasks. The tasks are created as API calls to do certain actions when a request for those calls is sent by the system. For example, the key tasks for a Trade License application include initiate/apply, forward, approve or payment. For Trade License initiate two API calls, “create” and “update” is required. Create API creates and saves the application in the database and returns an application number. Update API saves the required attached documents in the file store and returns the success acknowledgement message of the application created. These create and update API access permission is granted to the roles named Citizen and TL counter employee.&#x20;

Access permission is granted by mapping roles with APIs. Users assigned with the citizen or TL counter employee roles can initiate/apply the Trade License application.

## Pre-requisites <a href="#pre-requisites" id="pre-requisites"></a>

Before proceeding with the configuration, make sure the following pre-requisites are met -

* Knowledge of DIGIT applications is required.
* Users should be aware of transactional steps in the DIGIT application.
* Knowledge of json and how to write a json is required.
* Knowledge of MDMS is required.
* User with permission to edit the git repository where MDMS data is configured.

## Key Functionalities <a href="#key-functionalities" id="key-functionalities"></a>

In mapping roles with APIs, permission to perform a certain task can be restricted based on the requirement. For example, only the user with Role TL Counter Employee or Citizen can initiate the Trade License applications.

## Deployment Details <a href="#deployment-details" id="deployment-details"></a>

After mapping roles with APIs, the MDMS service needs to be restarted to read the newly added data.

## Configuration Details <a href="#configuration-details" id="configuration-details"></a>

APIs are added in **actions-test.json** and termed as action.\
In MDMS, file **actions-test.json**, under **ACCESSCONTROL-ACTIONS-TEST** folder APIs are added.\
**API Sample:**

```
{
  "tenantId": "uk",
  "moduleName": "ACCESSCONTROL-ACTIONS-TEST",
  "actions-test": [
    {
      "id": 1685,  //<Unique identifier>
      "name": "Create TradeLicense",
      "url": "/tl-services/v1/_create", //<url of the feature>
      "parentModule": "",
      "displayName": "Create TradeLicense",
      "orderNumber": 0,
      "enabled": false,
      "serviceCode": "tl-services",
      "code": "null",
      "path": ""
     },
     {
      "id": 1686,
      "name": "Update TradeLicense",
      "url": "/tl-services/v1/_update",
      "parentModule": "",
      "displayName": "Update TradeLicense",
      "orderNumber": 0,
      "enabled": false,
      "serviceCode": "tl-services",
      "code": "null",
      "path": ""
    }
   ]
  }   
```

APIs are added as action array elements with the request URL and other required details for the array "actions-test"

Each action is defined as a key-value pair:

| key         | Data Type | Is Mandatory? | Definition/ Description                   |
| ----------- | --------- | ------------- | ----------------------------------------- |
| id          | Numeric   | Yes           | A unique id that identifies an action.    |
| name        | Text      | No            | A short narration provided to the action. |
| url         | Text      | Yes           | It is the request URL of API call.        |
| displayName | Text      | No            | It is the display name.                   |
| enabled     | boolean   | Yes           | To enable or disable display in UI.       |
| servicecode | Text      | No            | Code of the service to which API belongs. |

Roles are added in **roles.json**\
In MDMS, file **roles.json**, under **ACCESSCONTROL-ROLES** folder roles are added.\
More about roles can be checked in the below link:\
[Adding roles to System](adding-roles-to-system.md)

Mapping of roles and APIs/actions is added in **roleactions.json**, under the folder\
**ACCESSCONTROL-ROLEACTIONS**.\
**Sample mapping:**

```
{
  "tenantId": "uk",
  "moduleName": "ACCESSCONTROL-ROLEACTIONS",
  "roleactions": [
    {
      "rolecode": "TL_CEMP",
      "actionid": 1685,
      "actioncode": "",
      "tenantId": "uk"
    },
    {
      "rolecode": "CITIZEN",
      "actionid": 1685,
      "actioncode": "",
      "tenantId": "uk"
    }
  ]
}
```

Role and API/action mapping is added as an array element under array roleactions.\
Each mapping is defined with key-value pairs. keys are rolecode, actionid, actioncode and tenantId.

| key        | Is Mandatory? | Definition/ Description                                                                                                 |
| ---------- | ------------- | ----------------------------------------------------------------------------------------------------------------------- |
| rolecode   | Yes           | The unique code of the role which is defined in roles.json and which required mapping for API.                          |
| actionid   | Yes           | The unique id of the API/action which is defined in actions-test.json and which is required to be mapped with the role. |
| actioncode | No            | The code of the API/action which is defined in actions-test.json and which is required to be mapped with the role.      |
| tenantid   | Yes           | tenant id of state.                                                                                                     |

### Reference Docs <a href="#reference-docs" id="reference-docs"></a>

#### Doc Links <a href="#doc-links" id="doc-links"></a>

| Description                                | Link                                                                                                                                                                                                                       |
| ------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Sample actions-test.json                   | [https://github.com/egovernments/ukd-mdms-data/blob/SDC/data/uk/ACCESSCONTROL-ACTIONS-TEST/actions-test.json](https://github.com/egovernments/ukd-mdms-data/blob/SDC/data/uk/ACCESSCONTROL-ACTIONS-TEST/actions-test.json) |
| Sample roles.json                          | [https://github.com/egovernments/ukd-mdms-data/blob/SDC/data/uk/ACCESSCONTROL-ROLES/roles.json](https://github.com/egovernments/ukd-mdms-data/blob/SDC/data/uk/ACCESSCONTROL-ROLES/roles.json)                             |
| Sample roleactions.json Roles APIs mapping | [https://github.com/egovernments/ukd-mdms-data/blob/SDC/data/uk/ACCESSCONTROL-ROLEACTIONS/roleactions.json](https://github.com/egovernments/ukd-mdms-data/blob/SDC/data/uk/ACCESSCONTROL-ROLEACTIONS/roleactions.json)     |

#### Videos

{% embed url="https://youtu.be/GcadlCpQG-o" %}



[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)​](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation](https://egov.org.in/) is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).
