# Property Tax - Search Applications

**Objective:** To provide employees with the functionality to search Applications (whether Active or in workflow) based on

1. &#x20;Application No.
2. Property ID
3. &#x20;Owner’s Mobile No.
4. Application Type
5. &#x20;Application Status
6. &#x20;Create Between Dates

![](<../../../../../.gitbook/assets/Screenshot from 2022-03-02 20-22-59.png>)

Users can view the application details page by clicking on the application number. The details page allows the employees to initiate and perform different workflow actions.

## **Technical Details**

Search application file link: [https://github.com/egovernments/DIGIT-Dev/blob/develop/frontend/micro-ui/web/micro-ui-internals/packages/modules/pt/src/components/SearchApplication.js](https://github.com/egovernments/DIGIT-Dev/blob/develop/frontend/micro-ui/web/micro-ui-internals/packages/modules/pt/src/components/SearchApplication.js)

The below hook is used to call the Property Search API and load the search result:

`1const { isLoading, isSuccess, isError, error, data: {Properties: searchReult, Count: count} = {} } = Digit.Hooks.pt.usePropertySearch( 2 { tenantId, 3 filters: payload 4 }, 5 config, 6 );`

Hook file path: [https://github.com/egovernments/DIGIT-Dev/blob/develop/frontend/micro-ui/web/micro-ui-internals/packages/modules/pt/src/pages/employee/SearchApp.js](https://github.com/egovernments/DIGIT-Dev/blob/develop/frontend/micro-ui/web/micro-ui-internals/packages/modules/pt/src/pages/employee/SearchApp.js)

## &#x20;**Role Action Mapping**

| <p><strong></strong></p><p><strong>Url</strong></p> | **Role**                | **Action Id** |
| --------------------------------------------------- | ----------------------- | ------------- |
| `/egov-location/location/v11/boundarys/_search`     | `PTCEMP,FI,APPROVER,DV` | `1429`        |
| `/property-services/property/_search`               | `PTCEMP,FI,APPROVER,DV` | `1897`        |

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation ](https://egov.org.in/)is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).
