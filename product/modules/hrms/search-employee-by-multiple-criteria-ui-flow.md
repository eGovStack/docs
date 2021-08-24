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

![](../../../.gitbook/assets/image%20%28165%29.png)

**On Hover** **of Roles Count**

 Logged User can able see the detail assigned roles

![](../../../.gitbook/assets/image%20%28141%29.png)

On click upon Employee Id Logged User are routed to Employee Detail screen

<table>
  <thead>
    <tr>
      <th style="text-align:left"><b>SL.No</b>
      </th>
      <th style="text-align:left"><b>API</b>
      </th>
      <th style="text-align:left"><b>Paramaters</b>
      </th>
      <th style="text-align:left"><b>Role</b>
      </th>
      <th style="text-align:left"><b>Access ID</b>
      </th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">1</td>
      <td style="text-align:left"><code>egov-hrms/employees/_search?</code>
      </td>
      <td style="text-align:left">
        <ul>
          <li>tendantId</li>
          <li>limit</li>
          <li>orderby</li>
          <li>offset</li>
          <li>{Filter Params}</li>
          <li>{Search Params}</li>
        </ul>
      </td>
      <td style="text-align:left">HRMS_ADMIN</td>
      <td style="text-align:left"><code>1752</code>
      </td>
    </tr>
  </tbody>
</table>

Primary Files

[https://github.com/egovernments/digit-ui-internals/blob/development/packages/modules/hrms/src/pages/Inbox.js](https://github.com/egovernments/digit-ui-internals/blob/development/packages/modules/hrms/src/pages/Inbox.js)

Secondary Files

[https://github.com/egovernments/digit-ui-internals/blob/development/packages/modules/hrms/src/components/inbox/DesktopInbox.js](https://github.com/egovernments/digit-ui-internals/blob/development/packages/modules/hrms/src/components/inbox/DesktopInbox.js)

[https://github.com/egovernments/digit-ui-internals/blob/development/packages/modules/hrms/src/components/inbox/search.js](https://github.com/egovernments/digit-ui-internals/blob/development/packages/modules/hrms/src/components/inbox/search.js)

[https://github.com/egovernments/digit-ui-internals/blob/development/packages/modules/hrms/src/components/inbox/ApplicationCard.js](https://github.com/egovernments/digit-ui-internals/blob/development/packages/modules/hrms/src/components/inbox/ApplicationCard.js)

[https://github.com/egovernments/digit-ui-internals/blob/development/packages/modules/hrms/src/components/inbox/ApplicationTable.js](https://github.com/egovernments/digit-ui-internals/blob/development/packages/modules/hrms/src/components/inbox/ApplicationTable.js)

[https://github.com/egovernments/digit-ui-internals/blob/development/packages/modules/hrms/src/components/inbox/ApplicationLinks.js](https://github.com/egovernments/digit-ui-internals/blob/development/packages/modules/hrms/src/components/inbox/ApplicationLinks.js)







