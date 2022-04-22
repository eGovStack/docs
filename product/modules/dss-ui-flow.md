# DSS UI Flow

Individual DSS configurations like FSM - DSS configuration is built on the DSS module where configuration and data are received from a set of APIs which can be accessed by users with specific user roles.

## Module-wise Role Access To DSS Module

| Role       | Module | API                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| ---------- | ------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| FSM\_ADMIN | FSM    | `1curl 'https://qa.digit.org/dashboard-analytics/dashboard/getDashboardConfig/fsm?_=1627404589797' \ 2 -H 'authority: qa.digit.org' \ 3 -H 'sec-ch-ua: " Not;A Brand";v="99", "Google Chrome";v="91", "Chromium";v="91"' \ 4 -H 'accept: application/json, text/plain, */*' \ 5 -H 'dnt: 1' \ 6 -H 'sec-ch-ua-mobile: ?0' \ 7 -H 'user-agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/91.0.4472.114 Safari/537.36' \ 8 -H 'auth-token: 1bc96a3e-c6c0-4af7-9b97-5cff0c035f98' \ 9 -H 'content-type: application/json;charset=utf-8' \ 10 -H 'sec-fetch-site: same-origin' \ 11 -H 'sec-fetch-mode: cors' \ 12 -H 'sec-fetch-dest: empty' \ 13 -H 'referer: https://qa.digit.org/digit-ui/employee/dss/dashboard/fsm' \ 14 -H 'accept-language: en-US,en;q=0.9,hi;q=0.8' \ 15 --compressed` |

## APIs

Data for each configuration is fetched using {env}/dashboard-analytics/dashboard/getChartV2?\_=1627404593531

API CURL -

```
curl 'https://qa.digit.org/dashboard-analytics/dashboard/getChartV2?_=1627404593531' \
  -H 'authority: qa.digit.org' \
  -H 'sec-ch-ua: " Not;A Brand";v="99", "Google Chrome";v="91", "Chromium";v="91"' \
  -H 'accept: application/json, text/plain, */*' \
  -H 'dnt: 1' \
  -H 'sec-ch-ua-mobile: ?0' \
  -H 'user-agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/91.0.4472.114 Safari/537.36' \
  -H 'content-type: application/json;charset=UTF-8' \
  -H 'origin: https://qa.digit.org' \
  -H 'sec-fetch-site: same-origin' \
  -H 'sec-fetch-mode: cors' \
  -H 'sec-fetch-dest: empty' \
  -H 'referer: https://qa.digit.org/digit-ui/employee/dss/dashboard/fsm' \
  -H 'accept-language: en-US,en;q=0.9,hi;q=0.8' \
  --data-raw '{"aggregationRequestDto":{"visualizationType":"METRIC","visualizationCode":"fsmTotalrequest","queryType":"","filters":{"tenantId":[]},"moduleLevel":"","aggregationFactors":null,"requestDate":{"startDate":1617215400000,"endDate":1627410599999,"interval":"month","title":"Apr 1, 2021 - Jul 27, 2021"}},"headers":{"tenantId":"pb.amritsar"},"RequestInfo":{"apiId":"Rainmaker","authToken":"1bc96a3e-c6c0-4af7-9b97-5cff0c035f98"}}' \
  --compressed
```

Each of the charts will have unique data params and responses in distinct API calls.

## UI Components

Fundamentally DSS has various functionalities including filtering of data, charts and drill-down charts with download PDF, Image and .XLS files. This is achieved by various components utilizing external plugins and internal services

## Filters

Filter component in DSS consists of 4 components:-

### **Date Range**

The DateRange component is a styling wrapper around DateRangePicker plugin.

![](<../../.gitbook/assets/image (251).png>)

### ULB / DDR Filter

Filter on the basis of ULB and DDR (District) is done by selecting single or multiple instances of DDR/ ULB. DDR is an encapsulation of ULBs, and getChart API filters data on the basis of ULB tenants,

Sample request header -

```
{
  "aggregationRequestDto": {
    "visualizationType": "METRIC",
    "visualizationCode": "fsmTotalrequest",
    "queryType": "",
    "filters": {
      "tenantId": [
        "pb.jalandhar",
        "pb.phagwara"
      ]
    },
    "moduleLevel": "",
    "aggregationFactors": null,
    "requestDate": {
      "startDate": 1617215400000,
      "endDate": 1627410599999,
      "duration": "month",
      "title": "Apr 1, 2021 - Jul 27, 2021"
    }
  },
...
```

The component in itself uses `MultiSelectDropdown` component

![](<../../.gitbook/assets/image (154).png>)

### Denomination

React Component named Switch which uses styled radio inputs.

![](<../../.gitbook/assets/image (142).png>)

## Generic Chart

The GenericChart is a common wrapper for all charts. It adds the basic styles to all the chart components.

### Metric Chart

The MetricChart component is a wrapper component around the MetricChartRow component. MetricChartRow component uses getChart API to fetch data for the “METRIC“ chart type. The MetricData component is a styling component used to format data.

![](<../../.gitbook/assets/image (217).png>)

### Area Chart

The CustomAreaChart component is used to render line chart type. It can format data based on denomination filter data. It uses the AreaChart component from the recharts package to draw the chart.

![](<../../.gitbook/assets/image (126).png>)

### Bar Chart

The CustomBarChart component is used to render performing-metric chart type. It uses the BarChart component from the recharts package to draw the chart.

![](<../../.gitbook/assets/image (272).png>)

### Horizontal Bar Chart

The CustomHorizontalBarChart component is used to render horizontal bar chart type. It uses the BarChart component from the recharts package to draw the chart.

![](<../../.gitbook/assets/image (174).png>)

### Pie Chart

The CustomPieChart component is used to render the donut chart type. It displays the top 4 categories and aggregates all the other categories into the “Others“ category. It uses the PieChart component from the recharts package to draw the chart.

![](<../../.gitbook/assets/image (253).png>)

### Tabular Chart

The CustomTable component is used to render table chart types. The insights are calculated by fetching the previous year's data and compared with the current data.

![](<../../.gitbook/assets/image (168).png>)

### Download Service

The download service is a common service used by all the chart components to facilitate the download/share pdf option. It is handled by using the JSPDF package.

## External plugins

#### Recharts <a href="#recharts" id="recharts"></a>

[<img src="https://static.npmjs.com/1996fcfdf7ca81ea795f67f093d7f449.png" alt="" data-size="line">npm: recharts](https://www.npmjs.com/package/recharts)

#### JSPDF <a href="#jspdf" id="jspdf"></a>

[<img src="https://static.npmjs.com/1996fcfdf7ca81ea795f67f093d7f449.png" alt="" data-size="line">npm: npm-install-peers](https://www.npmjs.com/package/jspdf)

#### HTML2Canvas <a href="#html2canvas" id="html2canvas"></a>

[<img src="https://static.npmjs.com/1996fcfdf7ca81ea795f67f093d7f449.png" alt="" data-size="line">npm: html2canvas](https://www.npmjs.com/package/html2canvas)

#### XLXS <a href="#xlxs" id="xlxs"></a>

[<img src="https://static.npmjs.com/1996fcfdf7ca81ea795f67f093d7f449.png" alt="" data-size="line">npm: xlsx](https://www.npmjs.com/package/xlsx)

#### DateRangePicker <a href="#daterangepicker" id="daterangepicker"></a>

[<img src="https://static.npmjs.com/1996fcfdf7ca81ea795f67f093d7f449.png" alt="" data-size="line">npm: daterangepicker](https://www.npmjs.com/package/daterangepicker)
