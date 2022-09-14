# Employee - Search Property, Property Details Page & Assessment

**Objective:** To provide employees with the functionality to search properties (either in active or in workflow status) based on locality, owner mobile, or unique Property Id.

![](<../../../../../.gitbook/assets/image (172).png>)

The employee also can see the dues for property within the search results and can choose to pay the dues if any, by clicking on collect tax.

Users can also view the current property Details page, to view Property Details, where employees can perform actions like assessment, Updation and Mutation, on an approved active Property.

## **Technical Details**

The file for search can be found in: [<img src="https://github.com/fluidicon.png" alt="" data-size="line">digit-ui-internals/Inbox.js at main · egovernments/digit-ui-internals](https://github.com/egovernments/digit-ui-internals/blob/main/packages/modules/pt/src/pages/employee/Inbox.js)

**APIs**

```
/egov-location/location/v11/boundarys/_search
/property-services/property/_search
/billing-service/bill/v2/_fetchbill
```

The 1st API is used to fetch all the localities, based on the logged in tenant.

The 2nd API is used to fetch the search results of the table data.

The 3rd API is used to fetch the bills showing the taxes due details in search results.

**Property Details Page**

This page is visible to the employee when they click on the property ID of the property in search.

Here employees can see the latest approved property details. The employee also has the option to start property assessment, transfer ownership, and edit property details.

![](<../../../../../.gitbook/assets/image (115) (1).png>)

![](<../../../../../.gitbook/assets/image (160).png>)

The employee also has the option to view history - this enables the users to view the owner details within the history of the property.

![](<../../../../../.gitbook/assets/image (218).png>)

**Payment History**

Users can access the payment history of a specific property as well as download the receipt for the same.

![](<../../../../../.gitbook/assets/Screenshot from 2022-03-11 16-11-32.png>)

## **Technical Implementation**

The code details can be found in:[<img src="https://github.com/fluidicon.png" alt="" data-size="line">digit-ui-internals/PropertyDetails.js at main · egovernments/digit-ui-internals](https://github.com/egovernments/digit-ui-internals/blob/main/packages/modules/pt/src/pages/employee/PropertyDetails.js)

**APIs**

Same as in the case of application details. The latest approved data is shown and any data which is not in the workflow is filtered out.

**Assessment Popup**

The popup is displayed when an employee chooses to assess property from the property details page of active property.

The popup displays the list of financial years to select from:-

![](<../../../../../.gitbook/assets/image (199).png>)

A financial year is selected for the assessment of the property.

**Technical Details**

The financial year list is fetched from the MDMS:[<img src="https://github.com/fluidicon.png" alt="" data-size="line">egov-mdms-data/FinancialYear.json at DEV · egovernments/egov-mdms-data](https://github.com/egovernments/egov-mdms-data/blob/DEV/data/pb/egf-master/FinancialYear.json)

**Assessment Screen**

Clicking on the Assess Property button displays the Property Assessment screen.

![](<../../../../../.gitbook/assets/image (194).png>)

This screen gives the assessment details of the selected financial year from the popup. It also provides an overview of the property as well as the total calculation details. This value is fetched from the MDMS.

It also provides the counter employee with a chance to add penalty or rebate in the current bill and accordingly the total value is calculated. The counter employee needs to click on the Add Rebate/Penalty button that opens a popup containing the penalty and rebate details.![](<../../../../../.gitbook/assets/Screenshot from 2022-03-11 16-16-16.png>)\


![](<../../../../../.gitbook/assets/Screenshot from 2022-03-02 20-46-49.png>)

After clicking on Assess Property, the button changes to Proceed To Pay that redirects the employee to the common pay screen.

**Technical Details**

The file for the assessment Details page can be found here: [<img src="https://github.com/fluidicon.png" alt="" data-size="line">digit-ui-internals/AssessmentDetails.js at main · egovernments/digit-ui-internals](https://github.com/egovernments/digit-ui-internals/blob/main/packages/modules/pt/src/pages/employee/AssessmentDetails.js)

The following hook is used to retrieve the charge slabs from the MDMS call

```
  const { data: ChargeSlabsMenu, isLoading: isChargeSlabsLoading } = Digit.Hooks.pt.usePropertyMDMS(stateId, "PropertyTax", "ChargeSlabs");
```

**API Used**

```
/pt-calculator-v2/propertytax/v2/_estimate
/property-services/property/_search
/property-services/assessment/_create
```

The 1st API is provided with the financial year and property Id as parameters to get the payment estimations for the property.

The 2nd API is used to fetch property details.

The 3rd API is used to create an assessment of the property - this provides the estimated tax value for the property.

## **Role Action Mapping**

| **Url**                                         | **Role**                | **Action Id** |
| ----------------------------------------------- | ----------------------- | ------------- |
| `/egov-location/location/v11/boundarys/_search` | `PTCEMP,FI,APPROVER,DV` | `1429`        |
| `/property-services/property/_search`           | `PTCEMP,FI,APPROVER,DV` | `1897`        |
| `/billing-service/bill/v2/_fetchbill`           | `PTCEMP,FI,APPROVER,DV` | `1862`        |
| `/pt-calculator-v2/propertytax/v2/_estimate`    | `PT-CEMP`               | `1962`        |
| `/property-services/property/_search`           | `PT-CEMP`               | `1897`        |
| `/property-services/assessment/_create`         | `PT-CEMP`               | `1933`        |

&#x20;

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation ](https://egov.org.in/)is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).
