# Search Employee By Multiple Criteria UI Flow

URL - digit-ui/employee/hrms/inbox

Admin can able to search Employee bases on multiple Filters and search Parameters

Filter By

* ULB
* Department
* Status

Search

* Name
* Employee ID
* Mobile Number

Has a pagination feature

![](<../../../.gitbook/assets/image (165).png>)

**On Hover** **of Roles Count**

Logged User can able see the detail assigned roles

![](<../../../.gitbook/assets/image (141).png>)

On click upon Employee Id Logged User are routed to Employee Detail screen

|           |                                |                                                                                                                          |             |               |
| --------- | ------------------------------ | ------------------------------------------------------------------------------------------------------------------------ | ----------- | ------------- |
| **SL.No** | **API**                        | **Paramaters**                                                                                                           | **Role**    | **Access ID** |
| 1         | `egov-hrms/employees/_search?` | <ul><li>tendantId</li><li>limit</li><li>orderby</li><li>offset</li><li>{Filter Params}</li><li>{Search Params}</li></ul> | HRMS\_ADMIN | `1752`        |

Primary Files

[https://github.com/egovernments/digit-ui-internals/blob/development/packages/modules/hrms/src/pages/Inbox.js](https://github.com/egovernments/digit-ui-internals/blob/development/packages/modules/hrms/src/pages/Inbox.js)

Secondary Files

[https://github.com/egovernments/digit-ui-internals/blob/development/packages/modules/hrms/src/components/inbox/DesktopInbox.js](https://github.com/egovernments/digit-ui-internals/blob/development/packages/modules/hrms/src/components/inbox/DesktopInbox.js)

[https://github.com/egovernments/digit-ui-internals/blob/development/packages/modules/hrms/src/components/inbox/search.js](https://github.com/egovernments/digit-ui-internals/blob/development/packages/modules/hrms/src/components/inbox/search.js)

[https://github.com/egovernments/digit-ui-internals/blob/development/packages/modules/hrms/src/components/inbox/ApplicationCard.js](https://github.com/egovernments/digit-ui-internals/blob/development/packages/modules/hrms/src/components/inbox/ApplicationCard.js)

[https://github.com/egovernments/digit-ui-internals/blob/development/packages/modules/hrms/src/components/inbox/ApplicationTable.js](https://github.com/egovernments/digit-ui-internals/blob/development/packages/modules/hrms/src/components/inbox/ApplicationTable.js)

[https://github.com/egovernments/digit-ui-internals/blob/development/packages/modules/hrms/src/components/inbox/ApplicationLinks.js](https://github.com/egovernments/digit-ui-internals/blob/development/packages/modules/hrms/src/components/inbox/ApplicationLinks.js)
