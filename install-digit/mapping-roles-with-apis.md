# Mapping Roles With APIs

## Overview <a id="Overview"></a>

Roles define the permissions of a user to perform a group of tasks. The tasks are created as API calls to do certain actions when a request for those calls is sent by the system. For example, the key tasks for a Trade License application include initiate/apply, forward, approve or payment. For Trade License initiate two API calls, “create” and “update” is required. Create API creates and save the application in the database and return an application number. Update API saves the required attached documents in the file store and return the success acknowledgement message of the application created. These create and update API access permission is granted to the roles named Citizen and TL counter employee. Access permission is grated by mapping roles with API. User assigned with the roles Citizen or TL counter employee can initiate/apply the Trade License application.

## Pre-requisites <a id="Pre-requisites"></a>

Before proceeding with the configuration, make sure the following pre-requisites are met -

* Knowledge of DIGIT applications is required.
* User should be aware of transactional steps in the DIGIT application.
* Knowledge of json and how to write a json is required.
* Knowledge of MDMS is required.
* User with permissions to edit the git repository where MDMS data is configured.

## Key Functionalities <a id="Key-Functionalities"></a>

* Mapping Roles with APIs, permission to perform a certain task can be restricted based on the requirement. For example, only the user with Role TL Counter Employee or Citizen can initiate the Trade License applications.

## Deployment Details <a id="Deployment-Details"></a>

* After mapping Roles with APIs, the MDMS service needs to be restarted to read the newly added data.

## Configuration Details <a id="Configuration-Details"></a>

1. APIs are added in **actions-test.json** and called as action. In MDMS, file **actions-test.json**, under **ACCESSCONTROL-ACTIONS-TEST** folder APIs are added. **API Sample:**`1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25 26 27 28 29 30` `{ "tenantId": "uk", "moduleName": "ACCESSCONTROL-ACTIONS-TEST", "actions-test": [ { "id": 1685, //<Unique identifier> "name": "Create TradeLicense", "url": "/tl-services/v1/_create", //<url of the feature> "parentModule": "", "displayName": "Create TradeLicense", "orderNumber": 0, "enabled": false, "serviceCode": "tl-services", "code": "null", "path": "" }, { "id": 1686, "name": "Update TradeLicense", "url": "/tl-services/v1/_update", "parentModule": "", "displayName": "Update TradeLicense", "orderNumber": 0, "enabled": false, "serviceCode": "tl-services", "code": "null", "path": "" } ] }`
2. APIs are added as action array element with the request url and other required details for the array "actions-test"
3. Each action is defined as key-value pair:

| Sr. No. | key | Data Type | Is Mandatory? | Definition/ Description |
| :--- | :--- | :--- | :--- | :--- |
| 1 | id | Numeric | Yes | A unique id that identifies action. |
| 2 | name | Text | No | A short narration provided to the action. |
| 3 | url | Text | Yes | It is the request url of API call. |
| 4 | displayName | Text | No | It is the display name. |
| 5 | enabled | boolean | Yes | To enable or disable display in UI. |
| 6 | servicecode | Text | No | Code of the service to which API belongs. |

1. Roles are added in **roles.json** In MDMS, file **roles.json**, under **ACCESSCONTROL-ROLES** folder roles are added. More about roles can be checked in the below link: [Adding roles to System](https://digit-discuss.atlassian.net/wiki/spaces/DD/pages/717946899/Adding+roles+to+System)
2. Mapping of Roles and APIs/action is added in **roleactions.json**, under the folder **ACCESSCONTROL-ROLEACTIONS**. **Sample mapping:**`1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18` `{ "tenantId": "uk", "moduleName": "ACCESSCONTROL-ROLEACTIONS", "roleactions": [ { "rolecode": "TL_CEMP", "actionid": 1685, "actioncode": "", "tenantId": "uk" }, { "rolecode": "CITIZEN", "actionid": 1685, "actioncode": "", "tenantId": "uk" } ] }`
3. Role and API/action mapping is added as an array element under array roleactions. 7. Each mapping is defined with key-value pairs. keys are rolecode, actionid, actioncode and tenantId.

| Sr. No. | key | Is Mandatory? | Definition/ Description |
| :--- | :--- | :--- | :--- |
| 1 | rolecode | Yes | The unique code of the role which is defined in roles.json and which required mapping for API. |
| 2 | actionid | Yes | The unique id of the API/action which is defined in actions-test.json and which is required to be mapped with the role. |
| 3 | actioncode | No | The code of the API/action which is defined in actions-test.json and which is required to be mapped with the role. |
| 4 | tenantid | Yes | tenant id of state. |

## Reference Docs <a id="Reference-Docs"></a>

### Doc Links <a id="Doc-Links"></a>

| **Title** | **Link** |
| :--- | :--- |
| Sample actions-test.json | [https://github.com/egovernments/ukd-mdms-data/blob/SDC/data/uk/ACCESSCONTROL-ACTIONS-TEST/actions-test.json](https://github.com/egovernments/ukd-mdms-data/blob/SDC/data/uk/ACCESSCONTROL-ACTIONS-TEST/actions-test.json) |
| Sample roles.json | [https://github.com/egovernments/ukd-mdms-data/blob/SDC/data/uk/ACCESSCONTROL-ROLES/roles.json](https://github.com/egovernments/ukd-mdms-data/blob/SDC/data/uk/ACCESSCONTROL-ROLES/roles.json) |
| Sample roleactions.json Roles APIs mapping | [https://github.com/egovernments/ukd-mdms-data/blob/SDC/data/uk/ACCESSCONTROL-ROLEACTIONS/roleactions.json](https://github.com/egovernments/ukd-mdms-data/blob/SDC/data/uk/ACCESSCONTROL-ROLEACTIONS/roleactions.json) |

