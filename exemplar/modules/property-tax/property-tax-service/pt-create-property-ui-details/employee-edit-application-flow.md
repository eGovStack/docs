# Employee Edit Application Flow

**Objective:** To provide employees with the ability to Edit property Details (except Owner Details).

## **Edit Application**

The Edit form can be used to update the details of an approved property, or whenever an application is in a workflow state that allows/require employees to make changes.

![](<../../../../../.gitbook/assets/image (241).png>)

All the updatable Input fields are enabled, and all the fields related to owner details are disabled.

After editing and clicking submit when the user is successful the user is redirected to a success screen similar to that in Employee Create.

## **Technical details**

Edit Form implementation file link: [<img src="https://github.com/fluidicon.png" alt="" data-size="line">digit-ui-internals/index.js at main · egovernments/digit-ui-internals](https://github.com/egovernments/digit-ui-internals/blob/main/packages/modules/pt/src/pages/employee/EditApplication/index.js)

The implementation details are similar to the create application and uses the same MDMS configurations.

APIs called:`1property-services/property/_update`

The Update API is supplied with updated property values from the form. All units that are added at the time of creation are set to `active` : `false` . The new units are set to `active` : `true.` This applies even when no changes are made to the units.

**Acknowledgement Screen**

If the Property Update is successful. then the employee is directed to the Acknowledgement screen. The screen displays the Acknowledgement Id and the option to download a pdf copy of the acknowledgement containing property details.

![](<../../../../../.gitbook/assets/image (212).png>)

## **Role Action Mapping**

|                                      |           |               |
| ------------------------------------ | --------- | ------------- |
| **Url**                              | **Roles** | **Action Id** |
| `property-services/property/_update` | `PT-CEMP` | `1896`        |

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation ](https://egov.org.in/)is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).
