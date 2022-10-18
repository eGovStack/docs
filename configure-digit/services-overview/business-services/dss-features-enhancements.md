---
description: V2 Technical Document for UI
---

# DSS Features Enhancements

## Overview

This release for DSS focuses on improving user experience and the ability given to the user to get deeper insights using drill-through and comparison indicators in tables.

The release includes the following features:

* Breadcrumbs for better navigation
* Drill through options in tables and charts
* Comparison indicators in Table

### **Breadcrumbs For Navigation**

In addition to the left navigation panel, the addition of breadcrumbs is also useful to provide a better sense of the current page insight. It is also very much helpful for mobile navigation. The user can navigate using the breadcrumbs by clicking on the required parent menu.

_Technical Implementation Details_

It Works based on the Current Route URL and previous Route URL

File Details - [https://github.com/egovernments/frontend/blob/master/web/dss-dashboard/src/Breadcrumbs.js](https://github.com/egovernments/frontend/blob/master/web/dss-dashboard/src/Breadcrumbs.js)

### **Drill through options in tables and charts**

The ability provided in DSS to configure the drill through for required options in tables as well as charts. The drill through options is useful in configuring the required hierarchy of data set. This helps users to go up to 'N' levels to get deeper insights

**Technical Implementation Details:**

Drill down/drill through in tables, is based on the drillDownChartId and filter.

Here chart id is used for the subsequent call to fetch the next table along with the applied/selected filters.

File Details - [https://github.com/egovernments/frontend/blob/master/web/dss-dashboard/src/components/Charts/TableChart.js](https://github.com/egovernments/frontend/blob/master/web/dss-dashboard/src/components/Charts/TableChart.js)

Drill throughs in piecharts:

It is similar to the drill-down in tables. Here drill through in piecharts are based on the drillDownChartId field in the parent piechart.

File Details - [https://github.com/egovernments/frontend/blob/master/web/dss-dashboard/src/components/Charts/DonutChart.js](https://github.com/egovernments/frontend/blob/master/web/dss-dashboard/src/components/Charts/DonutChart.js)

### **Comparison Indicators in Tables**

Providing better insights about the metric performances of different dimensions, a comparison indicator is required inside data tables comparing usually with a different time range (last year/last month) and what is percentage change with time.

**Technical Implementation Details:**

Comparison with the previous year's data in every table data uses the same request object by changing the time range to the previous year/month/week.

File Details - [https://github.com/egovernments/frontend/blob/master/web/dss-dashboard/src/components/Charts/TableChart.js](https://github.com/egovernments/frontend/blob/master/web/dss-dashboard/src/components/Charts/TableChart.js)

The following method along with parameters is used to fetch the previous year's data.

```
getLastYearRequest(calledFrom, visualcode, active, filterList) 
```

After receiving last year's data it is compared with the current year's data. The comparison is shown as insight data. The comparison logic is present in uiTable.js -&#x20;

[https://github.com/egovernments/frontend/blob/master/web/dss-dashboard/src/components/common/UiTable/UiTable.js](https://github.com/egovernments/frontend/blob/master/web/dss-dashboard/src/components/common/UiTable/UiTable.js)

**TimeFilter**

The current time component is not very intuitive and user-friendly. So a new library react-date range is used to enhance the time filter.

File Details - [https://github.com/egovernments/frontend/blob/master/web/dss-dashboard/src/components/common/DateRange/index.js](https://github.com/egovernments/frontend/blob/master/web/dss-dashboard/src/components/common/DateRange/index.js)

**Event Duration Graphs**

Ability to generate graphs showcasing time spent between multiple events like average turnaround time, complaint assigning time, etc.

A DSS\_EVENT\_DURATION\_GRAPH is added in the PGR config

```
{

    "id": 412,

    "name": "DSS_EVENT_DURATION_GRAPH",

    "dimensions": {

        "height": 350,

        "width": 7

    },

    "vizType": "chart",

    "isCollapsible": false,

    "label": "",

    "charts": [

        {

            "id": "eventDurationGraph",

            "name": "Monthly",

            "code": "",

            "chartType": "line",

            "filter": "",

            "headers": []

        }

    ]

}
```

## **API Call Role Action Mapping**

| API                                                            | Action ID | Roles                                                                  |
| -------------------------------------------------------------- | --------- | ---------------------------------------------------------------------- |
| /localization/messages/v1/\_search                             | 1531      | SUPERUSER,EMPLOYEE,CITIZEN,GRO,DGRO,                                   |
| /egov-mdms-service/v1/\_search                                 | 954       | LOA\_CREATOR,SUPERUSER,WO\_CREATOR,AE\_CREATOR,WORKS\_MASTER\_CREATOR, |
| /dashboard-analytics/dashboard/getDashboardConfig/propertytax  | 1892      | STADMIN                                                                |
| /dashboard-analytics/dashboard/getDashboardConfig/home         | 1889      | STADMIN                                                                |
| /dashboard-analytics/dashboard/getDashboardConfig/tradelicense | 1893      | STADMIN                                                                |
| /dashboard-analytics/dashboard/getDashboardConfig/pgr          | 1894      | STADMIN                                                                |
| /dashboard-analytics/dashboard/getDashboardConfig/ws           | 2010      | STADMIN                                                                |
| /dashboard-analytics/dashboard/getChartV2                      | 1890      | STADMIN, EMPLOYEE                                                      |

> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)\_\_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_ ](https://egov.org.in/)_is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
