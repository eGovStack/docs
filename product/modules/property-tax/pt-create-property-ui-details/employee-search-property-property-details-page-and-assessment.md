# Employee - Search Property, Property Details Page & Assessment

**Objective:** To provide employees with the functionality to search property \(whether Active or in workflow\). based on locality, owner mobile, or unique Property Id.

![](../../../../.gitbook/assets/image%20%28172%29.png)

The employee also can see the dues for property within the search results and can choose to pay the dues if any, by clicking on collect tax.

Users can also view the current property Details page, to view Property Details, where employees can perform actions like assessment, Updation and Mutation, on an approved active Property.

## **Technical Details**

_The file for search can be found in:_

[![](https://github.com/fluidicon.png)digit-ui-internals/Inbox.js at main · egovernments/digit-ui-internals](https://github.com/egovernments/digit-ui-internals/blob/main/packages/modules/pt/src/pages/employee/Inbox.js)

**APIs**

```text
/egov-location/location/v11/boundarys/_search
/property-services/property/_search
/billing-service/bill/v2/_fetchbill
```

The 1st API is used to fetch all the localities, based on the logged**-**in tenant.

The 2nd API is used to fetch the search Table data.

The 3rd API is used to fetch the bills for showing the due taxes present in search results.

**Property Details Page**

This page is visible to the employee when he clicks the property Id of property in search.

Here employees can see the latest approved Property Details. The employee also has the option to start property assessment, transfer ownership, and Edit Property details flow.

![](../../../../.gitbook/assets/image%20%28115%29.png)

![](../../../../.gitbook/assets/image%20%28160%29.png)

The employee also has the option to view history - this enables the users to view the owner details within the history of the property.

![](../../../../.gitbook/assets/image%20%28218%29.png)

## **Technical Implementation**

_The code details can be found in:_

[![](https://github.com/fluidicon.png)digit-ui-internals/PropertyDetails.js at main · egovernments/digit-ui-internals](https://github.com/egovernments/digit-ui-internals/blob/main/packages/modules/pt/src/pages/employee/PropertyDetails.js)

**APIs**

Same as in the case of Application details, But here, The latest approved data is shown and any data which is not in the workflow is filtered out.

**Assessment Popup**

When an employee selects the action to assess property from the  property details page of active property,

A popup is shown having a list of Financial Years:-

![](../../../../.gitbook/assets/image%20%28199%29.png)

A financial Year is selected for the assessment of the property.

**Technical Details**

_The Financial Years are fetched from the MDMS:_

[![](https://github.com/fluidicon.png)egov-mdms-data/FinancialYear.json at DEV · egovernments/egov-mdms-data](https://github.com/egovernments/egov-mdms-data/blob/DEV/data/pb/egf-master/FinancialYear.json)

**Assessment Screen**

When selected and clicked on Assess Property the Property Assessment Screen is displayed.

![](../../../../.gitbook/assets/image%20%28194%29.png)

This screen gives the assessment details of the selected financial year from the popup. After clicking on Assess Property, the button changes to “Proceed To Pay” which takes the employee to the common pay screen for employees.

**Technical Details**

The file for the assessment Details page can be found at the following link :

[![](https://github.com/fluidicon.png)digit-ui-internals/AssessmentDetails.js at main · egovernments/digit-ui-internals](https://github.com/egovernments/digit-ui-internals/blob/main/packages/modules/pt/src/pages/employee/AssessmentDetails.js)

**API Used**

```text
/pt-calculator-v2/propertytax/v2/_estimate
/property-services/property/_search
/property-services/assessment/_create
```

The 1st API is provided with financial Year and property Id as parameter**s** to get the payment estimations for the Property.

The 2nd API is used to fetch Property Details.

The 3rd API is used to create an Assessment of the property. Which marks property with the estimated tax.

## **Role Actions**

| **Url** | **Role** | **Action Id** |
| :--- | :--- | :--- |
| `/egov-location/location/v11/boundarys/_search` | `All Roles` | `1429` |
| `/property-services/property/_search` | `All Roles` | `1897` |
| `/billing-service/bill/v2/_fetchbill` | `All Roles` | `1862` |
| `/pt-calculator-v2/propertytax/v2/_estimate` | `PT-CEMP` | `1962` |
| `/property-services/property/_search` | `PT-CEMP` | `1897` |
| `/property-services/assessment/_create` | `PT-CEMP` | `1933` |





