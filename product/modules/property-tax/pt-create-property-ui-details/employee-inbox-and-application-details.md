# Employee - Inbox & Application Details

**Objective:** To provide the employee with the functionality to search the created Applications.

## **Employee Inbox**

The employee inbox screen shows all the created applications which are in the workflow and requires action from that particular employee.

The employee has the ability to search any application based on Application no, Property Id, or mobile number, or he can apply filters, based on the business service (create, edit, or update), application status, locality, and application assigned specifically to him.

By clicking on the /application no in the inbox user goes to the application details page. where he can take action on the application to push it forward or backwards in the workflow.

### **Technical Details**

_The file path for inbox can be found in:_

[![](https://github.com/fluidicon.png)digit-ui-internals/Inbox.js at main · egovernments/digit-ui-internals](https://github.com/egovernments/digit-ui-internals/blob/main/packages/modules/pt/src/pages/employee/Inbox.js)

**API Used**

_The API used for searching the Inbox is_

```
/inbox/v1/_search
```

The above API is used to fetch the Inbox results based on filters and search criteria.

### **Customizations**

Inbox Screen offers customization for the fields in the inbox table. The fields inside the inbox table are exposed in the component registry service as in the file:

[![](https://github.com/fluidicon.png)digit-ui-internals/inbox-table-config.js at main · egovernments/digit-ui-internals](https://github.com/egovernments/digit-ui-internals/blob/main/packages/modules/pt/src/config/inbox-table-config.js)

It is exposed as `PTInboxTableConfig` key in component registry service, and can be redefined to reset the columns.

the function returns an object of the following structure:-

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

the `object.PT` contains 2 keys `inboxCloumns` and `searchColumns` , which are yet again functions.

These functions are provided with `props` as an argument, which are props supplied to the component called `DesktopInbox` as can be seen in the following file:-

[![](https://github.com/fluidicon.png)digit-ui-internals/Inbox.js at main · egovernments/digit-ui-internals](https://github.com/egovernments/digit-ui-internals/blob/main/packages/modules/pt/src/pages/employee/Inbox.js)

`inboxCloumns` and `searchColumns` functions return an array of objects, each object represents a column.

The `inboxCloumns` is used for setting columns in the Inbox, while `searchColumns` is used for setting columns

every column has the following properties:-

1. `Header` is the head that is used in `thead` of the column (basically name of the column).
2. `accessor` is `.` separated string value that specifies the path within each row to be followed in order to display the value of the column. The structure of the row object is similar to `row.original` explained below.
3. `Cell` is function returning a valid JSX, in case some complex component is needed to be rendered. The function is supplied an object with `row` property, each row containing property details , with `row.original` being the actual data for the property row which is of the form. The `searchData` contains search related result associated with the property, while `workflowData` contains workflow related data associated with property

```
{
  searchData : {...},
  workflowData : {...}
}
```

For further enquiry on how to set columns, you can check \_\_out the link:- [![](https://react-table.tanstack.com/\_next/static/images/favicon-07c3e551b48272d4685be76a6a7fb11c.png)Getting Started: Overview](https://react-table.tanstack.com/docs/overview)

## **Application Details Page**

This page is where the Employee visits after clicking on desired Application No. in the inbox. The user can find a “take action” button at the bottom of the screen and can perform actions, based on the role the employee profile has and the state of the application in the workflow. He can also view the timeline in which he can see which employee made what update in the workflow.

The employee can see details like owner details, address etc, along with the documents attached at the time of creation, and while action performing by any other employee in the workflow. In the case of mutation Application, the employee can see transferer and transferee details.

While performing the action user can upload docs, comments for the next employee in workflow, or they can assign them to a specific employee in the action resultant workflow.

If a particular workflow is completed then, the application is said to be completed and the status of property changes to `ACTIVE` .![](blob:https://digit-discuss.atlassian.net/46368eb0-1300-41f9-ac13-7499ad9e3abd#media-blob-url=true\&id=78b55505-bcbe-40a9-9056-41529894bf70\&collection=contentId-1850277933\&contextId=1850277933\&mimeType=image%2Fpng\&name=image-20210729-040720.png\&size=201303\&width=1920\&height=1080)

![](<../../../../.gitbook/assets/image (114).png>)

![](<../../../../.gitbook/assets/image (228).png>)

![](<../../../../.gitbook/assets/image (213).png>)

### **Technical Details**

_The code for the application details can be found in_

[![](https://github.com/fluidicon.png)digit-ui-internals/ApplicationDetails.js at main · egovernments/digit-ui-internals](https://github.com/egovernments/digit-ui-internals/blob/main/packages/modules/pt/src/pages/employee/ApplicationDetails.js)

**APIs Called**

The application details page calls the following APIs.

```
egov-workflow-v2/egov-wf/process/_search?tenantId=pb.amritsar&history=true
/property-services/property/_search
/egov-workflow-v2/egov-wf/businessservice/_search
/filestore/v1/files/url
```

the 1st API is called to fetch the timeline, through which the Process Instance has gone through.

The 2nd API is called to fetch address, owner-details, and document `fileStoreId` for all the documents associated with the property.

The 3rd API is called to get current performable actions based on the current state of the process Instance, which is then filtered through according to actions performable by the employee’s role.

The 4th API is called to fetch all the documents for the file store ids.

## **Role Actions**

|                                                     |             |               |
| --------------------------------------------------- | ----------- | ------------- |
| **Url**                                             | **Roles**   | **Action Id** |
| `egov-workflow-v2/egov-wf/process/_search`          | `All Roles` | `1730`        |
| `/property-services/property/_search`               | `All Roles` | `1897`        |
| `/egov-workflow-v2/egov-wf/businessservice/_search` | `All Roles` | `1743`        |
| `/filestore/v1/files/url`                           | `All Roles` | `1528`        |
