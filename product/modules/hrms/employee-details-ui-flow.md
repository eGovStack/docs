# Employee Details UI Flow

URL- digit-ui/employee/hrms/details/{Employee Id}

Logged User should able to see details of Employee

* **Employment Status**
* **Personal Details**
* **Employee Details**
* **Jurisdiction Details**
* **Assignment Details**

![](../../../.gitbook/assets/image%20%28291%29.png)

![](../../../.gitbook/assets/image%20%28279%29.png)

**Supported Documents**

If User has uploaded any Documents against Employment Status. Those Documents should be one click Downloadable

![](../../../.gitbook/assets/image%20%28277%29.png)

**API details**

| **SL No** | **API** | **Role** | **Access ID** |
| :--- | :--- | :--- | :--- |
| 1 | `/egov-hrms/employees/_search` | HRMS\_ADMIN | `1752` |

Primary Files

[https://github.com/egovernments/digit-ui-internals/blob/development/packages/modules/hrms/src/pages/EmployeeDetails.js](https://github.com/egovernments/digit-ui-internals/blob/development/packages/modules/hrms/src/pages/EmployeeDetails.js)

