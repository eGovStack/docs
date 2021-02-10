# Adding New APIs For Access

### Overview <a id="Overview"></a>

Roles define the permissions of a user to perform a group of tasks. The tasks are created as API calls to do certain actions when a request for those calls is sent by the system. Access permission is grated by mapping roles with API. User assigned with the roles to provide access for the API

### Pre-requisites <a id="Pre-requisites"></a>

Before proceeding with the configuration, make sure the following pre-requisites are met -

* Knowledge of DIGIT applications is required.
* User should be aware of transactional steps in the DIGIT application.
* Knowledge of json and how to write a json is required.
* Knowledge of MDMS is required.
* Knowledge on how to create a new API.
* APIs developed on digit follow certain conventions and principles. The aim of this document is to provide some do’s and don’ts while following those principles
  * APIs path should be standardised as follows:
    * **/{service}/{entity}/{version}/\_create**: This endpoint should be used to create the entity
    * **/{service}/{entity}/{version}/\_update**: This endpoint should be used to edit an entity which is already existing
    * **/{service}/{entity}/{version}/\_search**: This endpoint should be used to provide search on the entity based on certain criteria
    * **/{service}/{entity}/{version}/\_count**: This endpoint should be provided to give a count of entities that match a given search criteria
  * Always use POST for each of the endpoints
  * Take most search parameters in POST body only
* For further more information about how new API is developed could be referred in this link[ API Do's and Don'ts](https://digit-discuss.atlassian.net/wiki/spaces/DD/pages/686719019/API+Do%27s+and+Don%27ts)

### Key Functionalities <a id="Key-Functionalities"></a>

* Adding New APIs\(actions\) and Mapping Roles with that APIs provides permission to perform certain task can be restricted based on the requirement.

### Deployment Details <a id="Deployment-Details"></a>

* After mapping Roles with APIs, the MDMS service needs to be restarted to read the newly added data.

### Configuration Details <a id="Configuration-Details"></a>

1. APIs are added in **actions-test.json** and called as action. In MDMS, file **actions-test.json**, under **ACCESSCONTROL-ACTIONS-TEST** folder APIs are added. **API Sample:**`1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20 21 22` `{ "tenantId": "uk", "moduleName": "ACCESSCONTROL-ACTIONS-TEST", "actions-test": [ { "id": <unique and sequential to previous id>, "name": "rainmaker-common-propertytax", "url": "card", "displayName": "Property Tax", "orderNumber": 2, "parentModule": "", "enabled": true, "serviceCode": "", "code": "", "path": "", "navigationURL": "property-tax", "leftIcon": "action:store", "rightIcon": "", "queryParams": "" }, ] }`
2. APIs are added as action array element with the request url and other required details for the array "actions-test"
3. Each action is defined as key-value pair:

| Sr. No. | key | Data Type | Is Mandatory? | Definition/ Description |
| :--- | :--- | :--- | :--- | :--- |
| 1 | id | Numeric | Yes | A unique id that identifies action. |
| 2 | name | Text | No | A short narration provided to the action. |
| 3 | url | Text | Yes | It is the endpoint of API or type like url or card. |
| 4 | displayName | Text | No | It is the display name. |
| 5 | orderNumber | Numeric | Yes | A number to represent order to display in UI |
| 6 | parentModule | Text | No | Code of the service referred to as parent |
| 7 | enabled | boolean | Yes | To enable or disable display in UI. |
| 8 | serviceCode | Text | No | Code of the service to which API belongs. |
| 9 | code | Text | No |  |
| 10 | path | Text | No |  |
| 11 | navigationUrl | Text | Yes | Url to navigate in UI |
| 12 | leftIcon | Icon | No |  |
| 13 | rightIcon | Icon | No |  |

4. Roles are added in **roles.json**  
In MDMS, file **roles.json**, under **ACCESSCONTROL-ROLES** folder roles are added.  
 More about roles can be checked in the below link:  
[Adding roles to System](https://digit-discuss.atlassian.net/wiki/spaces/DD/pages/717946899/Adding+roles+to+System)

5. Mapping of Roles and APIs/action is added in **roleactions.json**, under the folder  
**ACCESSCONTROL-ROLEACTIONS**.  
**Sample mapping:**`1 2 3 4 5 6 7 8 9 10 11 12` `{ "tenantId": "uk", "moduleName": "ACCESSCONTROL-ROLEACTIONS", "roleactions": [ { "rolecode": <specific code defined in roles.json>, "actionid": <id of an action>, "actioncode": "", "tenantId": <state notation of tenantId>(like uk,pb etc) } ] }`

6. Role and API/action mapping is added as an array element under array roleactions.  
 7. Each mapping is defined with key-value pairs. keys are rolecode, actionid, actioncode and tenantId.

| Sr. No. | key | Is Mandatory? | Definition/ Description |
| :--- | :--- | :--- | :--- |


| Sr. No. | key | Is Mandatory? | Definition/ Description |
| :--- | :--- | :--- | :--- |
| 1 | rolecode | Yes | The unique code of the role which is defined in roles.json and which required mapping for API. |
| 2 | actionid | Yes | The unique id of the API/action which is defined in actions-test.json and which is required to be mapped with the role. |
| 3 | actioncode | No | The code of the API/action which is defined in actions-test.json and which is required to be mapped with the role. |
| 4 | tenantid | Yes | tenant id of state. |

### Reference Docs <a id="Reference-Docs"></a>

#### Doc Links <a id="Doc-Links"></a>

| **Title**  | **Link** |
| :--- | :--- |
| Sample actions-test.json | [https://github.com/egovernments/ukd-mdms-data/blob/SDC/data/uk/ACCESSCONTROL-ACTIONS-TEST/actions-test.json](https://github.com/egovernments/ukd-mdms-data/blob/SDC/data/uk/ACCESSCONTROL-ACTIONS-TEST/actions-test.json) |
|  Sample roles.json | [https://github.com/egovernments/ukd-mdms-data/blob/SDC/data/uk/ACCESSCONTROL-ROLES/roles.json](https://github.com/egovernments/ukd-mdms-data/blob/SDC/data/uk/ACCESSCONTROL-ROLES/roles.json) |
| Sample roleactions.json Roles APIs mapping | [https://github.com/egovernments/ukd-mdms-data/blob/SDC/data/uk/ACCESSCONTROL-ROLEACTIONS/roleactions.json](https://github.com/egovernments/ukd-mdms-data/blob/SDC/data/uk/ACCESSCONTROL-ROLEACTIONS/roleactions.json) |

