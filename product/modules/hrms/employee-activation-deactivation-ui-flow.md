# Employee Activation-Deactivation UI Flow

Logged in users can activate or deactivate employees as required.

## **Deactivate Employee**

If Employee status is Active. Users can Deactivate Employee by clicking on the Take Action button placed on Employee Detail Screen.

On the click of Deactivate Employee button, a PopUp appears where users should provide necessary details such as

Mandatory

* Reason for Deactivation 
* Effective Date 

Optional

* Order No.
* Supported Documents \(File Upload\)
* Remarks

![](../../../.gitbook/assets/image%20%28145%29.png)

On Deactivation User will be navigated to the Acknowledgement screen

## **Activation Employee**

If employee status is inactive, users can reactivate employees by clicking on the Take Action button placed on Employee Detail Screen.

On the click of Deactivate Employee button, a popup appears where users should provide necessary details such as

Mandatory

* Reason for Reactivation 
* Effective Date 

Optional

* Order No.
* Supported Documents \(File Upload\)
* Remarks

![](../../../.gitbook/assets/image%20%28140%29.png)

On reactivation, users are routed to the Acknowledgement screen

| **SL No** | **API** | **Details** |
| :--- | :--- | :--- |
| 1 | `/egov-hrms/employees/_update` | `1 let documents = { 2 referenceType: "ACTIVATION", 3 documentId: uploadedFile, 4 documentName: file.name, 5 }; 6 applicationData.Employees[0]["documents"].push(documents); 7 } 8 9 Employees[0]["reactivationDetails"].push(data); 10 Employees[0].isActive = true;` |
| 2 | `/egov-hrms/employees/_update` | `1 let documents = { 2 referenceType: "DEACTIVATION", 3 documentId: uploadedFile, 4 documentName: file.name, 5 }; 6 applicationData.Employees[0]["documents"].push(documents); 7 } 8 Employees[0]["deactivationDetails"].push(data); 9 Employees[0].isActive = false; 10 history.push("/digit-ui/employee/hrms/response", { Employees, key: "UPDATE", action: "DEACTIVATION" });` |

Primary Files

[https://github.com/egovernments/digit-ui-internals/blob/development/packages/modules/hrms/src/components/EmployeeAction.js](https://github.com/egovernments/digit-ui-internals/blob/development/packages/modules/hrms/src/components/EmployeeAction.js)

Secondary Files

[https://github.com/egovernments/digit-ui-internals/blob/development/packages/modules/hrms/src/components/Modal/index.js](https://github.com/egovernments/digit-ui-internals/blob/development/packages/modules/hrms/src/components/Modal/index.js) 

[https://github.com/egovernments/digit-ui-internals/blob/development/packages/modules/hrms/src/components/Modal/EmployeeActivation.js](https://github.com/egovernments/digit-ui-internals/blob/development/packages/modules/hrms/src/components/Modal/EmployeeActivation.js) 

[https://github.com/egovernments/digit-ui-internals/blob/development/packages/modules/hrms/src/components/Modal/EmployeeAppliaction.js](https://github.com/egovernments/digit-ui-internals/blob/development/packages/modules/hrms/src/components/Modal/EmployeeAppliaction.js)

##  MDMS Hook

```text
const { isLoading, isError, errors, data, ...rest } = Digit.Hooks.hrms.useHrmsMDMS(tenantId, "egov-hrms", "DeactivationReason");
```





