# Employee Edit Application Flow

**Objective:** To provide employees with the ability to Edit property Details \(except Owner Details\).

## **Edit Application**

The Edit form can be used to update the details of an approved property, or whenever an application is in a workflow state that allows/require employees to make changes.

![](../../../../.gitbook/assets/image%20%28241%29.png)

All the updatable Input fields are enabled, and all the fields related to owner details are disabled.

After editing and clicking submit when the user is successful the user is redirected to a success screen similar to that in Employee Create.

## **Technical details**

_The implementation of the Edit Form can be found in:_

[![](https://github.com/fluidicon.png)digit-ui-internals/index.js at main · egovernments/digit-ui-internals](https://github.com/egovernments/digit-ui-internals/blob/main/packages/modules/pt/src/pages/employee/EditApplication/index.js)

The document details are implemented similar to the create application and uses the same MDMS configurations.

**APIs Called:**`1property-services/property/_update`

\*\* The Update API is supplied with updated property values from the form, and also all the units that were added at the time of creation are set with `active` : `false` , while the new units are set to be `active` : `true`

even if no change is made to the units.

**Acknowledgement Screen**

If the Property Update is successful. then the employee is directed to this screen that shows the Acknowledgement Id and option to download a pdf of the acknowledgement containing property details.

![](../../../../.gitbook/assets/image%20%28212%29.png)

## **Role Actions**

| **Url** | **Roles** | **Action Id** |
| :--- | :--- | :--- |
| `property-services/property/_update` | `PT-CEMP` | `1896` |





