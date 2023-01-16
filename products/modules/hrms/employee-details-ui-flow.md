# Employee Details UI Flow

URL- digit-ui/employee/hrms/details/{Employee Id}

Logged in users should able to see details of employees

* **Employment Status**
* **Personal Details**
* **Employee Details**
* **Jurisdiction Details**
* **Assignment Details**

![](<../../../.gitbook/assets/image (291).png>)

![](<../../../.gitbook/assets/image (279).png>)

**Supported Documents**

If the user has uploaded any documents against Employment Status. Those documents are downloadable in one click.

![](<../../../.gitbook/assets/image (277).png>)

**API details**

| API                            | Role        | Access ID |
| ------------------------------ | ----------- | --------- |
| `/egov-hrms/employees/_search` | HRMS\_ADMIN | `1752`    |

Primary Files: [https://github.com/egovernments/digit-ui-internals/blob/development/packages/modules/hrms/src/pages/EmployeeDetails.js](https://github.com/egovernments/digit-ui-internals/blob/development/packages/modules/hrms/src/pages/EmployeeDetails.js)
