# Employee - Inbox & Application Details

**Objective:** To provide employees with the functionality to search for created applications.

## **Employee Inbox**

The employee inbox screen shows all created applications in workflow and requires action from the logged-in employee.

The employee has the ability to search for specific applications based on application number, property ID, or mobile number. Filters can be applied based on the business service (create, edit, or update), application status, locality, and assigned applications.

Clicking on the application number hyperlink in the inbox redirects the user to the application details page. The user can take the required action on the application to push it forward or backwards in the workflow.

### **Technical Details**

File path for inbox: [<img src="https://github.com/fluidicon.png" alt="" data-size="line">digit-ui-internals/Inbox.js at main · egovernments/digit-ui-internals](https://github.com/egovernments/digit-ui-internals/blob/main/packages/modules/pt/src/pages/employee/Inbox.js)

**API Used**

Below is the API used for searching the inbox:

```
/inbox/v1/_search
```

The above API is used to fetch the Inbox results based on the selected filters and search criteria.

### **Customizations**

The inbox screen offers customization for the fields in the inbox table. The fields inside the inbox table are exposed in the component registry service as in the file:

[<img src="https://github.com/fluidicon.png" alt="" data-size="line">digit-ui-internals/inbox-table-config.js at main · egovernments/digit-ui-internals](https://github.com/egovernments/digit-ui-internals/blob/main/packages/modules/pt/src/config/inbox-table-config.js)

It is exposed as `PTInboxTableConfig` key in component registry service, and can be redefined to reset the columns. The function returns an object of the following structure:-

```
{
     PT: {
      inboxColumns: (props) => [
        {
           Header: t("ES_INBOX_UNIQUE_PROPERTY_ID"),
           Cell: ({ row }) => {
             return (
               <div>
                 <span className="link">
                   <Link to={`${props.parentRoute}/application-details/` + row.original?.searchData?.["propertyId"]}>
                     {row.original?.searchData?.["propertyId"]}
                   </Link>
                 </span>
               </div>
             );
           },
         },
       ],
       searchColumns: (props) => [
        {
          Header: t("ES_INBOX_UNIQUE_PROPERTY_ID"),
          accessor: "searchData.propertyId",
          Cell: ({ row }) => {
            return (
              <div>
                <span className="link">
                  <Link to={`${props.parentRoute}/property-details/` + row.original?.searchData?.["propertyId"]}>
                    {row.original?.searchData?.["propertyId"]}
                  </Link>
                </span>
              </div>
            );
          },
        }
      ]
     },
}
```

The `object.PT` contains 2 keys- `inboxColumns` and `searchColumns.` These are functions that contain `props` as an argument. These props are supplied to the component called `DesktopInbox` as seen in the following file:-[<img src="https://github.com/fluidicon.png" alt="" data-size="line">digit-ui-internals/Inbox.js at main · egovernments/digit-ui-internals](https://github.com/egovernments/digit-ui-internals/blob/main/packages/modules/pt/src/pages/employee/Inbox.js)

`inboxCloumns` and `searchColumns` functions return an array of objects where each object represents a column.

The `inboxCloumns` is used for setting columns in the Inbox, while `searchColumns` is used for setting columns.

Every column has the following properties:-

1. `Header` is the heading that is used in the `head` of the column (basically name of the column).
2. `accessor` is `.` separated string value that specifies the path within each row to be followed in order to display the value of the column. The structure of the row object is similar to `row.original` explained below.
3. `Cell` is a function returning a valid JSX. In case some complex component requires to be rendered, the function is supplied an object with `row` property. Each row contains property details, with `row.original` being the actual data for the property row. The `searchData` contains search-related results associated with the property, while `workflowData` contains workflow related data associated with property.

```
{
  searchData : {...},
  workflowData : {...}
}
```

For further enquiry on how to set columns check out the link here- [![](https://react-table.tanstack.com/\_next/static/images/favicon-07c3e551b48272d4685be76a6a7fb11c.png)Getting Started: Overview](https://react-table.tanstack.com/docs/overview)

## **Application Details Page**

This page is where the employee is redirected after clicking on the application number in the inbox. The user finds the Take Action button at the bottom of the screen and performs actions based on the employee's role and the state of the application in the workflow. Users can also view the timeline where they can see the updates by other employees and the actions taken on the application so far.

The employee views details like owner details, address along with the documents attached at the time of creation. In the case of mutation applications, the employee can see transferer and transferee details.

While performing the action users can upload docs, add comments for the next employee in workflow, or they can assign them to a specific employees in the action resultant workflow.

If a particular workflow is completed then, the application is said to be completed and the status of property changes to `ACTIVE` .

![](<../../../../../.gitbook/assets/image (114).png>)

![](<../../../../../.gitbook/assets/image (228) (1).png>)

![](<../../../../../.gitbook/assets/image (213).png>)

### **Technical Details**

Code for the application details available here - [<img src="https://github.com/fluidicon.png" alt="" data-size="line">digit-ui-internals/ApplicationDetails.js at main · egovernments/digit-ui-internals](https://github.com/egovernments/digit-ui-internals/blob/main/packages/modules/pt/src/pages/employee/ApplicationDetails.js)

**APIs Called**

The application details page calls the following APIs.

```
egov-workflow-v2/egov-wf/process/_search?tenantId=pb.amritsar&history=true
/property-services/property/_search
/egov-workflow-v2/egov-wf/businessservice/_search
/filestore/v1/files/url
```

the 1st API is called to fetch the timeline processed through the process instance.

The 2nd API is called to fetch address, owner-details, and document `fileStoreId` for all the documents associated with the property.

The 3rd API is called to get current performable actions based on the existing process instance. This is then filtered through as per the actions performable by the employee’s role.

The 4th API is called to fetch all the documents for the file store ids.

## **Role Action Mapping**

| **Url**                                             | **Roles**               | **Action Id** |
| --------------------------------------------------- | ----------------------- | ------------- |
| `egov-workflow-v2/egov-wf/process/_search`          | `PTCEMP,FI,APPROVER,DV` | `1730`        |
| `/property-services/property/_search`               | `PTCEMP,FI,APPROVER,DV` | `1897`        |
| `/egov-workflow-v2/egov-wf/businessservice/_search` | `PTCEMP,FI,APPROVER,DV` | `1743`        |
| `/filestore/v1/files/url`                           | `PTCEMP,FI,APPROVER,DV` | `1528`        |

&#x20;

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation ](https://egov.org.in/)is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).
