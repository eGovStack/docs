---
description: V2 Technical Document for UI
---

# DSS Features Enhancements

## **Description**

This release for DSS focuses on improving user experience and ability given to the user to get deeper insights using drill through and comparison indicators in tables.

The release includes the following features:

* Breadcrumbs for better navigation
* Drill through options in tables and charts
* Comparison indicators in Table

### **Breadcrumbs for Navigation**

In addition to the left navigation panel, the addition of breadcrumbs is also useful to provide a better sense of the current page insight. It is also very much helpful for mobile navigation. The user can navigate using the breadcrumbs by clicking on the required parent menu.

_Technical Implementation Details_

It Works based on the Current Route URL and previous Route URL

File Details

[https://github.com/egovernments/frontend/blob/master/web/dss-dashboard/src/Breadcrumbs.js](https://github.com/egovernments/frontend/blob/master/web/dss-dashboard/src/Breadcrumbs.js)

### **Drill through options in tables and charts**

The ability provided in DSS to configure the drill through for required options in tables as well as charts. The drill through options is useful in configuring the required hierarchy of data set. This helps users to go up to 'N' levels to get deeper insights

_Technical Implementation Details:_

Drill down /Drill through in Tables, is based on the drillDownChartId and filter.

Here chart id is used for the subsequent call to fetch the next table along with the applied/selected filters.

File Details

[https://github.com/egovernments/frontend/blob/master/web/dss-dashboard/src/components/Charts/TableChart.js](https://github.com/egovernments/frontend/blob/master/web/dss-dashboard/src/components/Charts/TableChart.js)

Drill throughs in piecharts :

It is Similar to Dilldown in tables, here Drill through in piecharts are based on the drillDownChartId field in the parent piechart

File Details,

[https://github.com/egovernments/frontend/blob/master/web/dss-dashboard/src/components/Charts/DonutChart.js](https://github.com/egovernments/frontend/blob/master/web/dss-dashboard/src/components/Charts/DonutChart.js)

### **Comparison Indicators in Tables**

Providing better insights about the metric performances of different dimensions, a comparison indicator is required inside data tables comparing usually with a different time range (last year/last month) and what is percentage change with time.

_Technical Implementation Details:_

For Comparing with previous year data in every table data, the same request object will be used by changing the time range to the previous year/month/week.

File Details

[https://github.com/egovernments/frontend/blob/master/web/dss-dashboard/src/components/Charts/TableChart.js](https://github.com/egovernments/frontend/blob/master/web/dss-dashboard/src/components/Charts/TableChart.js)

The following Method along with parameters is used to fetch the previous year data.

```
getLastYearRequest(calledFrom, visualcode, active, filterList) 
```

after receiving last year data it is compared with current year data and will be shown insight data will be shown, comparison logic is present in uiTable.js

[https://github.com/egovernments/frontend/blob/master/web/dss-dashboard/src/components/common/UiTable/UiTable.js](https://github.com/egovernments/frontend/blob/master/web/dss-dashboard/src/components/common/UiTable/UiTable.js)

**TimeFilter**

The current time component is not very intuitive and user friendly. So New library react-date-range was used to enhance the time filter.

File Details

[https://github.com/egovernments/frontend/blob/master/web/dss-dashboard/src/components/common/DateRange/index.js](https://github.com/egovernments/frontend/blob/master/web/dss-dashboard/src/components/common/DateRange/index.js)

**Event Duration Graphs**

Ability to generate graphs showcasing time spent between multiple events like average turnaround time, complaint assigning time, etc.

A DSS\_EVENT\_DURATION\_GRAPH was added in the PGR config

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

|                       |                                                                |           |                                                                        |
| --------------------- | -------------------------------------------------------------- | --------- | ---------------------------------------------------------------------- |
| [S.No](http://s.no/). | API                                                            | Action id | Roles                                                                  |
| 1                     | /localization/messages/v1/\_search                             | 1531      | SUPERUSER,EMPLOYEE,CITIZEN,GRO,DGRO,                                   |
| 2                     | /egov-mdms-service/v1/\_search                                 | 954       | LOA\_CREATOR,SUPERUSER,WO\_CREATOR,AE\_CREATOR,WORKS\_MASTER\_CREATOR, |
| 3                     | /dashboard-analytics/dashboard/getDashboardConfig/propertytax  | 1892      | STADMIN                                                                |
| 4                     | /dashboard-analytics/dashboard/getDashboardConfig/home         | 1889      | STADMIN                                                                |
| 5                     | /dashboard-analytics/dashboard/getDashboardConfig/tradelicense | 1893      | STADMIN                                                                |
| 6                     | /dashboard-analytics/dashboard/getDashboardConfig/pgr          | 1894      | STADMIN                                                                |
| 7                     | /dashboard-analytics/dashboard/getDashboardConfig/ws           | 2010      | STADMIN                                                                |
| 8                     | /dashboard-analytics/dashboard/getChartV2                      | 1890      | STADMIN, EMPLOYEE                                                      |

> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)\_\_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_ ](https://egov.org.in/)_is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
