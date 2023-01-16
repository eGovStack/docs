# Employee Inbox UI Flow

Objective Provide employees with the scope to view the assigned applications and all the applications pending action.&#x20;

Route - https://egov-micro-uat.egovernments.org/employee/inbox&#x20;

Technical Implementation Details&#x20;

The inbox screen is loaded based on the file frontend/index.js at master · egovernments/frontend

The inbox screen can be divided into 4 sub-components as listed below

1. Sidebar
2. Quick Action Button
3. Service List
4. Inbox Worklist&#x20;

**Sidebar** - Action Menu is the component which shows the menu items in the sidebar response from - access/v1/actions/mdms/\_get&#x20;

Employee Inbox provides employees with the scope to view the assigned applications and all the applications pending action.  uat.egovernments.org/employee/inbox
