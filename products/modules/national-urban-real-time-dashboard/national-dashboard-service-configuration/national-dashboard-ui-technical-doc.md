# National Dashboard - UI Technical Doc

## **Overview**

A decision support system (DSS) is a composite tool that collects, organizes and analyzes business data to facilitate quality decision-making for management, operations and planning. A well-designed DSS aids decision makers in compiling a variety of data from many sources: raw data, documents, personal knowledge from employees, management, executives and business models. DSS analysis helps organizations to identify and solve problems, and make decisions.

Code Git Repos: [<img src="https://github.com/fluidicon.png" alt="" data-size="line">DIGIT-OSS/frontend/micro-ui/web/micro-ui-internals at master · egovernments/DIGIT-OSS](https://github.com/egovernments/DIGIT-OSS/tree/master/frontend/micro-ui/web/micro-ui-internals)

Enable National Dashboard: MDMS details

```
[
  {
    "moduleName": "tenant",
    "masterDetails": [
      {
        "name": "citymodule"
      }
    ]
  },
]
```

Enable the NDSS in the city module.

```
{
  active: true
  code: "NDSS"
  module: "NDSS"
}
```

**Type Of Users**

1. National Level Admin (NATADMIN)
2. State Level Admin (STADMIN)

**Dashboard List**

There are three type of dashboards -

1. Home page (**refer figure 1**).
2. Overview page (**refer figure 2**).
3. Module-level dashboard (**refer figure 3**).&#x20;

**Home page**

The home page contains multiple cards - each card is clickable.

![](<../../../../.gitbook/assets/image (110).png>)

There are two types of cards, i.e, Overview card and module level card.

Overview and Module level card is differentiated by vizType,

1. Overview card: Clicking on the Overview card, redirects users to the overview page. vizType for Overview is collection.
2. Module Level card: Clicking on the Module level card, redirects users to the Module level dahsboard. vizType is module (i.e Property Tax, Trade License etc).
3. Map chart: This entity displays the total , active ULBs within states where DIGIT is live.\
   State names are configured in the dashboard-config.\
   [<img src="https://github.com/fluidicon.png" alt="" data-size="line">egov-mdms-data/dashboard-config.json at DEV · egovernments/egov-mdms-data](https://github.com/egovernments/egov-mdms-data/blob/DEV/data/pb/dss-dashboard/dashboard-config.json)

**Request Payload For Dashboard Config**

`https://qa.digit.org/dashboard-analytics/dashboard/getDashboardConfig/NURT_DASHBOARD`

**auth-token:** authenticates the request and fetches from the local storage key called **Employee.token**

**DashboardConfig API Response**

&#x20;

![](<../../../../.gitbook/assets/image (93).png>)

![](<../../../../.gitbook/assets/image (321).png>)

Visualizations: Key contains all configuration for displaying the visualization like rows with charts etc. - refer **figure  1.3**. In Figure 1.3, **vizType** key defines the module UI.&#x20;

For Collection Chart & Module Chart **refer figure 1**

![Overview dashboard](<../../../../.gitbook/assets/image (198).png>)

![Module level dashboard](<../../../../.gitbook/assets/image (57).png>)

**Visualizations List**

In dashboardConfig response **visualizations** key contains all rows & charts details(refer **figure 1.3**).

Each row contains the visual details like name, vizType, noUnit, charts etc.(refer **figure 1.3**).

name - name of visualization

vizType - type of visualization like COLLECTION,MODULE,METRIC-COLLECTION, PERFORMING-METRIC,CHART

* COLLECTION - contains collection data and displayed on the home page (refer **figure 1**)
* MODULE - contains module level data and displayed on the home page (refer **figure 1**)
* METRIC-COLLECTION - contains collection data and displayed on Overview/Module level page (refer **figure 2.1**)
* PERFORMING-METRIC - contains top/bottom performing data displayed on Overview/Module level page (refer **figure 2.2).**
* CHART - contains the below visualizations displayed on Overview/Module level page (refer **figure 2.3 to figure 2.7).**
  1. PIE CHART (refer **figure 2.3**)
  2. LINE CHART (refer **figure 2.4**)
  3. BAR CHART (refer **figure 2.5**)
  4. HORIZONTAL BAR CHART (refer **figure 2.6**)
  5. TABLE CHART (refer **figure 2.7**)

**List of visualizations**

<img src="../../../../.gitbook/assets/image (334).png" alt="" data-size="original">

&#x20;Figure: 2.1 Collection Metric

![](<../../../../.gitbook/assets/image (60).png>)

Figure: 2.2 Performance Metric

![](<../../../../.gitbook/assets/image (314).png>)

Figure: 2.3 Pie Chart

![](<../../../../.gitbook/assets/image (311).png>)

Figure: 2.4 Line Chart

![](<../../../../.gitbook/assets/image (319).png>)

Figure: 2.5 Bar Chart&#x20;

![](<../../../../.gitbook/assets/image (88).png>)

Figure: 2.6 Horizontal Bar Chart

![](<../../../../.gitbook/assets/image (320).png>)

Figure: 2.7 Table Chart

![](<../../../../.gitbook/assets/image (324).png>)

Figure: 2.8 Global Filters

![](<../../../../.gitbook/assets/image (285).png>)

Figure: 2.9 Download & Share Button

**Global Filters (figure 2.8)**

Filters are loaded from MDMS API - [https://egov-micro-dev.egovernments.org/egov-mdms-service/v1/\_search](https://egov-micro-dev.egovernments.org/egov-mdms-service/v1/\_search)

[egov-mdms-data/nationalInfo.json at QA · egovernments/egov-mdms-data (github.com)](https://github.com/egovernments/egov-mdms-data/blob/QA/data/pb/tenant/nationalInfo.json)

State is fetched from `stateCode`\
ULB from `code`

```
  {
        "stateCode": "Punjab",
        "stateName": "Punjab",
        "code": "pb.amritsar",
        "name": "Amritsar",
        "active": true,
        "module": "NationalDashboard"
      },
```

Denomination filter: Denomination filter offers three options to display the amount and number in a particular format.

1. Crore
2. Lakh
3. Unit

Denomination filter is not applied on the percentage and text (**figure 2.10**). Type of data is identified by symbol in plots of charts API.

![](<../../../../.gitbook/assets/image (109).png>)

Figure 2.10

**Custom Date Filter**

&#x20;If duration < 15 days, data is displayed days wise.

If duration <= 30 days, data is displayed week-wise.

If duration >30, data is displayed monthly wise.

**Tabs**

Currently dashboard is having two types of tabs -

1. Revenue (figure: 4.1)
2. Service (figure: 4.1)

Tabs are identified by name in visualizations of config API.

![](<../../../../.gitbook/assets/image (83).png>)

**Table chart with drilldown**

Table chart visualizations has normal material UI data table features like search, sort etc.

![](<../../../../.gitbook/assets/image (86).png>)

In table response filter key & drillDownChartId has a value that indicates it is a drill-down table.

**Cards**

1. Each card header is localized and has an info icon with a tooltip option which displays the header and the description.
2. Number of cards in rows on the page is driven by the backend. The backend provides a row number to each card where it should be displayed.
3. Card contains an option icon that contains the image download and image share option.
4. Image download and share option use id from vizArray in order to differentiate each card on a page.

**Download and Share (figure 2.9)**

Download has two options - download as Image or PDF

Share: Share creates the Image/PDF and uploads it S3 using the below API and returns file id - [/filestore/v1/files](https://mseva-uat.lgpunjab.gov.in/filestore/v1/files)

Using file Id calls the following API - [/filestore/v1/files/url](https://mseva-uat.lgpunjab.gov.in/filestore/v1/files/url)

Each S3 image is shortened using the following API - [/egov-url-shortening/shortener](https://mseva-uat.lgpunjab.gov.in/egov-url-shortening/shortener)

Upload localization keys:

&#x20;![](<../../../../.gitbook/assets/image (323).png>)

**code:** pre-defined key for back-end

**message:** message contains the value for the key

**module:** rainmaker-dss

**locale:** contains locale data

Contact eGov team for more details

Module name: rainmaker-dss

**NPM Module Used**

```
    "react-date-range": "1.3.0",
    "react-hook-form": "^6.7.0",
    "react-i18next": "^11.7.3",
    "react-query": "3.6.1",
    "react-redux": "^7.2.1",
    "react-router-dom": "^5.2.0",
    "react-table": "^7.6.1",
    "react-time-picker": "4.2.1",
    "recharts": "^2.0.9",
```

{% hint style="info" %}
**Note:: Consider this while pushing new State data - **_**both MDMS state names and codes should be in sync**_
{% endhint %}

1\. Map component : [https://raw.githubusercontent.com/egovernments/egov-mdms-data/DEV/data/pb/dss-dashboard/dashboard-config.json](https://raw.githubusercontent.com/egovernments/egov-mdms-data/DEV/data/pb/dss-dashboard/dashboard-config.json)

```
 {
              "type": "Polygon",
              "id": "MP",
              "properties": { "name": "Madhya Pradesh" },
              "arcs": [[-39, 142, -127, -66, -86]]
            },
```

Where id is state code and name is state name.

2\. Global Filter: [https://raw.githubusercontent.com/egovernments/egov-mdms-data/QA/data/pb/tenant/nationalInfo.json](https://raw.githubusercontent.com/egovernments/egov-mdms-data/QA/data/pb/tenant/nationalInfo.json)

```
   {
        "stateCode": "Punjab",
        "stateName": "Punjab",
        "code": "pb.amritsar",
        "name": "Amritsar",
        "active": true,
        "module": "NationalDashboard"
      },
```

If the values are pushed under different names then the existing file is updated accordingly.

**Steps to setup DSS in local**

Step 1: Run as independent , switch to micro-ui-internals folder

Step 2: Run _yarn install_ and _yarn start:dev_ to start working on dss in local setup.

## **API Call Role Action Mapping**

| **API**                                                                   | **Roles**  |
| ------------------------------------------------------------------------- | ---------- |
| `/localization/messages/v1/_search`                                       |            |
| `/egov-mdms-service/v1/_search`                                           |            |
| `/dashboard-analytics/dashboard/getDashboardConfig/national-ws`           | `NATADMIN` |
| `/dashboard-analytics/dashboard/getDashboardConfig/national-tradelicense` | `NATADMIN` |
| `/dashboard-analytics/dashboard/getDashboardConfig/national-propertytax`  | `NATADMIN` |
| `/dashboard-analytics/dashboard/getDashboardConfig/national-pgr`          | `NATADMIN` |
| `/dashboard-analytics/dashboard/getDashboardConfig/NURT_DASHBOARD`        | `NATADMIN` |
| `/dashboard-analytics/dashboard/getDashboardConfig/nss-obps`              | `NATADMIN` |
| `/dashboard-analytics/dashboard/getDashboardConfig/national-firenoc`      | `NATADMIN` |
| `/dashboard-analytics/dashboard/getDashboardConfig/national-mcollect`     | `NATADMIN` |
| `/dashboard-analytics/dashboard/getDashboardConfig/national-overview`     | `NATADMIN` |

**Supporting links**

1. [DSS](dss-ui-flow.md)
2. [National Dashboard Technical Documentation](./)

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_ ](https://egov.org.in/)_is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
