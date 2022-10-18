# Impact Of Heavy Reports On Platform

## Overview <a href="#overview" id="overview"></a>

Rainmaker has a reporting framework to configure new reports. As part of the report configuration, we have to write a native SQL query to get the required data for the report. So if the query takes huge time to execute or the query result has huge data, then it will impact the whole application's performance.

## Root Cause <a href="#root-cause" id="root-cause"></a>

The following are cases where we can see the application performance issue because of heavy reports.

* Filtering with long date range data or applying fewer filters which in turn returns huge data
* Join the multiple tables for getting required data and missing creating index on join columns
* Implementing conditional logic inside the queries itself
* Writing multiple sub-queries inside a single query for getting the required data

## Impact <a href="#impact" id="impact"></a>

Because of heavy reporting, the following things impact the platform -

* When we execute a complex query on the database, a thread from the connection pool blocks the query execution.
* When threads from the connection pool are blocked completely, the application becomes very slow for incoming requests
* When the max request timeout is crossed, the API gateway returns a timeout error. But still, the connection thread on the database is active. Then all these types of idle threads occupy the database resources like memory, and the CPU which in turn increases the load on the database.
* Sometimes when running huge queries, the time taken by the query leads to a broken pipe issue which causes more memory leaks and out-of-heap memory type issues. Because of this, the service frequently restarts automatically.
* If a query returns huge data, the browser becomes unresponsive and the application becomes unresponsive.



[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)​](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation](https://egov.org.in/) is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).
