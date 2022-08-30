# HRMS Employee Create-Edit UI Flow

### Case: **Create**

URL- digit-ui/employee/hrms/create

Logged User can able to Create Employee by providing necessary Details

If a user enters a mobile number that already exists in the system - Then the application will give an error message.

The Boundary is auto-filled with current `TenantId`. The user is able to add Multiple Jurisdictions and Assignments.

![](<../../../.gitbook/assets/image (256) (1).png>)

![](<../../../.gitbook/assets/image (258) (1).png>)

![](<../../../.gitbook/assets/image (179).png>)

![](<../../../.gitbook/assets/image (171).png>)

|           |                                |             |               |
| --------- | ------------------------------ | ----------- | ------------- |
| **SL No** | **API**                        | **ROLE**    | **Access Id** |
| 1         | `/egov-hrms/employees/_create` | HRMS\_ADMIN | 1750          |
| 2         | `/egov-hrms/employees/_search` | HRMS\_ADMIN | `1752`        |

Primary Files

[https://github.com/egovernments/digit-ui-internals/blob/development/packages/modules/hrms/src/pages/createEmployee.js](https://github.com/egovernments/digit-ui-internals/blob/development/packages/modules/hrms/src/pages/createEmployee.js)

### Case: **Edit**

URL- digit-ui/employee/hrms/edit/{Employee Id}

Logged User can able to Edit Employee Details. Employee Id is disabled.

|           |                                |             |               |
| --------- | ------------------------------ | ----------- | ------------- |
| **SL No** | **API**                        | **Role**    | **Access Id** |
| 1.        | `/egov-hrms/employees/_update` | HRMS\_ADMIN | `1751`        |

Primary Files

[https://github.com/egovernments/digit-ui-internals/blob/development/packages/modules/hrms/src/pages/EditEmployee/EditForm.js](https://github.com/egovernments/digit-ui-internals/blob/development/packages/modules/hrms/src/pages/EditEmployee/EditForm.js)

[https://github.com/egovernments/digit-ui-internals/blob/development/packages/modules/hrms/src/pages/EditEmployee/index.js](https://github.com/egovernments/digit-ui-internals/blob/development/packages/modules/hrms/src/pages/EditEmployee/index.js)

### MDMS API

```
 moduleDetails: [
    {
      moduleName: "common-masters",
      masterDetails: [
        { name: "Department", filter: "[?(@.active == true)]" },
        { name: "Designation", filter: "[?(@.active == true)]" },
      ],
    },
    {
      moduleName: "tenant",
      masterDetails: [{ name: "tenants" }],
    },
    {
      moduleName: "ACCESSCONTROL-ROLES",
      masterDetails: [{ name: "roles", filter: "$.[?(@.code!='CITIZEN')]" }],
    },
    { moduleName: "egov-location", masterDetails: [{ name: "TenantBoundary" }] },
  ]
```
