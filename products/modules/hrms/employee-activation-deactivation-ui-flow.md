# Employee Activation-Deactivation UI Flow

Logged-in users can activate or deactivate employees as required.

## **Deactivate Employee**

If the employee Status is Active - Users can deactivate the employee by clicking on the Take Action button available in the Employee Detail screen.

On the click of Deactivate Employee button, a PopUp appears where users should provide necessary details such as

Mandatory

* Reason for Deactivation
* Effective Date

Optional

* Order No.
* Supported Documents (File Upload)
* Remarks

![](<../../../.gitbook/assets/image (145).png>)

On deactivation, users will be re-directed to the Acknowledgement screen

## **Activation Employee**

If an employee status is inactive, users can reactivate employees by clicking on the Take Action button placed on the Employee Detail screen.

On the click of Deactivate Employee button, a popup appears where users should provide necessary details such as

Mandatory

* Reason for Reactivation
* Effective Date

Optional

* Order No.
* Supported Documents (File Upload)
* Remarks

![](<../../../.gitbook/assets/image (140).png>)

On reactivation, users are routed to the Acknowledgement screen

| API                            | Details                                                                                                                                                                                                                                                                                                                                                                           |
| ------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `/egov-hrms/employees/_update` | `1 let documents = { 2 referenceType: "ACTIVATION", 3 documentId: uploadedFile, 4 documentName: file.name, 5 }; 6 applicationData.Employees[0]["documents"].push(documents); 7 } 8 9 Employees[0]["reactivationDetails"].push(data); 10 Employees[0].isActive = true;`                                                                                                            |
| `/egov-hrms/employees/_update` | `1 let documents = { 2 referenceType: "DEACTIVATION", 3 documentId: uploadedFile, 4 documentName: file.name, 5 }; 6 applicationData.Employees[0]["documents"].push(documents); 7 } 8 Employees[0]["deactivationDetails"].push(data); 9 Employees[0].isActive = false; 10 history.push("/digit-ui/employee/hrms/response", { Employees, key: "UPDATE", action: "DEACTIVATION" });` |

Primary Files: [https://github.com/egovernments/digit-ui-internals/blob/development/packages/modules/hrms/src/components/EmployeeAction.js](https://github.com/egovernments/digit-ui-internals/blob/development/packages/modules/hrms/src/components/EmployeeAction.js)

Secondary Files: [https://github.com/egovernments/digit-ui-internals/blob/development/packages/modules/hrms/src/components/Modal/index.js](https://github.com/egovernments/digit-ui-internals/blob/development/packages/modules/hrms/src/components/Modal/index.js)

[https://github.com/egovernments/digit-ui-internals/blob/development/packages/modules/hrms/src/components/Modal/EmployeeActivation.js](https://github.com/egovernments/digit-ui-internals/blob/development/packages/modules/hrms/src/components/Modal/EmployeeActivation.js)

[https://github.com/egovernments/digit-ui-internals/blob/development/packages/modules/hrms/src/components/Modal/EmployeeAppliaction.js](https://github.com/egovernments/digit-ui-internals/blob/development/packages/modules/hrms/src/components/Modal/EmployeeAppliaction.js)

## MDMS Hook

```
const { isLoading, isError, errors, data, ...rest } = Digit.Hooks.hrms.useHrmsMDMS(tenantId, "egov-hrms", "DeactivationReason");
```
