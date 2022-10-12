# Adding Roles To System

## Overview <a href="#overview" id="overview"></a>

Roles define the permissions of a user to perform a group of tasks. For example for a Trade License application initiate, forward, approve or payment are tasks that require permission.\
Users assigned to the citizen or counter-employee role can perform initiation and payment. TL Document Verifier can forward the application and the only user assigned with the role named TLApprover can approve the application.

## Pre-requisites <a href="#pre-requisites" id="pre-requisites"></a>

Before proceeding with the configuration, make sure the following pre-requisites are met -

* Knowledge of DIGIT applications is required.
* Users should be aware of transactional steps in the DIGIT application.
* Knowledge of json and how to write a json is required.
* Knowledge of MDMS is required.
* User with permission to edit the git repository where MDMS data is configured.

## Key Functionalities <a href="#key-functionalities" id="key-functionalities"></a>

* Roles provide users with permission to perform certain tasks and restrict too based on the requirement. For example, only users with Role TLApprover can approve the Trade License-initiated application.
* While creating an employee in the system from HRMS Admin, the roles can be assigned to the employees based on the requirement. The roles added in MDMS will show in the “roles drop down” in the employee create screen.
* In the DIGIT system workflow for a module is implemented based on roles. For example, the roles for the Trade License module in a Trade License application workflow are - CounterEmployee/Citizen>TLDocVerifier>TLApprover>CounterEmployee/Citizen. The table below lists the Trade License application workflows based on the defined roles.

| Role            | Workflow in Trade License                                                                                                                                                                                                                 |
| --------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| CounterEmployee | Initiates the TL application for Citizen from counter. Initiated TL application goes to TLDocVerifier inbox.                                                                                                                              |
| Citizen         | Initiates the TL application. Initiated TL application goes to TLDocVerifier inbox.                                                                                                                                                       |
| TLDocVerifier   | User with role TLDocVerifier can forward or reject the TL application after verifying the initiated application. The rejected application shows for re-submission in initiator inbox. The forwarded application goes to TLApprover inbox. |
| TLApprover      | TLApprover can approve or reject based on the requirement. The rejected application goes back to TLDocVerifer for re-verification. The approved application shows for payment pending in initiator inbox.                                 |
| CounterEmployee | Once the initiated application is approved by the user with role TLApprover, CounterEmployee can do the payment and download the receipt.                                                                                                 |
| Citizen         | Once the initiated application is approved by the user with role TLApprover, Citizen can do the payment and download the receipt.                                                                                                         |

## Deployment Details <a href="#deployment-details" id="deployment-details"></a>

After adding the new role, the MDMS service needs to be restarted to read the newly added data.

## Configuration Details <a href="#configuration-details" id="configuration-details"></a>

Roles are added in **roles.json** In MDMS, file **roles.json**, under **ACCESSCONTROL-ROLES** folder roles are added. **Sample roles:**

```
{
  "tenantId": "uk",
  "moduleName": "ACCESSCONTROL-ROLES",
  "roles": [
    {
      "code": "CITIZEN",
      "name": "Citizen",
      "description": "Citizen who can raise complaint"
    },
    {
      "code": "TL_CEMP",
      "name": "TL Counter Employee",
      "description": "Who has a access to Trade License Services"
    },
    {
      "code": "TL_DOC_VERIFIER",
      "name": "Trade License Document verifier",
      "description": "Trade License Document verifier"
    },
    {
      "code": "TL_APPROVER",
      "name": "TL Approver",
      "description": "Who has a access to Trade License Workflow"
    }
  ]
}
```

A role is added as an array element under the array named “roles”.

Each role is defined with three key-value pairs. keys are “code”, ”name” and “description”.

| key         | Data Type    | Data Size | Is Mandatory? | Definition/ Description                                                                                       |
| ----------- | ------------ | --------- | ------------- | ------------------------------------------------------------------------------------------------------------- |
| code        | Alphanumeric | 64        | Yes           | A unique code that identifies the user role name.                                                             |
| name        | Text         | 256       | Yes           | The Name indicates the User Role while creating an employee a role can be assigned to an individual employee. |
| description | Text         | 256       | No            | A short narration provided to the user role name.                                                             |

Localization needs to be pushed for all the roles added in roles.json

**Sample** **Localization for** **roles**\
In English:

```
 {
  "code": "ACCESSCONTROL_ROLES_ROLES_TL_CEMP",  // <"ACCESSCONTROL_ROLES_ROLES_" should be appended before role code>
  "message": "TL Counter Employee",             // English Value to be shown in UI
  "module": "rainmaker-common",                 // module is added with rainmaker-common
  "locale": "en_IN"                             // English language key
}
```

In Hindi:

```
{
  "code": "ACCESSCONTROL_ROLES_ROLES_TL_CEMP",  // <"ACCESSCONTROL_ROLES_ROLES_" should be appended before role code>
  "message": "टीएल काउंटर कर्मचारी",               // Hindi value to be shown in UI
  "module": "rainmaker-common",                // module is added with rainmaker-common
  "locale": "hi_IN"                            // Hindi language key
}
```

{% hint style="info" %}
* code "code": "ACCESSCONTROL\_ROLES\_ROLES\_TL\_CEMP", is the localization key for role.&#x20;
* The key has three parts:&#x20;
  * a) ACCESSCONTROL\_ROLES: It is the folder and module name of MDMS, file **roles.json** in which roles are added. The hyphen (- ) in the name "ACCESSCONTROL-ROLES" is replaced with an underscore ( \_ ).&#x20;
  * b) ROLES: It is the role.json file name and array name under which roles as array elements are added.&#x20;
  * c)TL\_CEMP: It is the unique role code.
* If localization is not pushed for the roles then the key will appear in UI.
{% endhint %}

## Reference Docs <a href="#reference-docs" id="reference-docs"></a>

#### Doc Links <a href="#doc-links" id="doc-links"></a>

| Description       | Link                                                                                                                                                                                           |
| ----------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Sample roles.json | [https://github.com/egovernments/ukd-mdms-data/blob/SDC/data/uk/ACCESSCONTROL-ROLES/roles.json](https://github.com/egovernments/ukd-mdms-data/blob/SDC/data/uk/ACCESSCONTROL-ROLES/roles.json) |
| Reference link    | [User Roles](https://digit-discuss.atlassian.net/wiki/spaces/DO/pages/428769455/User+Roles)                                                                                                    |



[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)​](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation](https://egov.org.in/) is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).
