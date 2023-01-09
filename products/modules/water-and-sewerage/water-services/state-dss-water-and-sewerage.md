---
description: Technical Doc
---

# State DSS - Water & Sewerage

## **Overview**

DSS has two sides to it. One is the process in which the data is pooled into ElasticSearch and the other is the way it is fetched, aggregated, computed, transformed and sent across.

As this revolves around a variety of data sets, there is a need for making this configurable. So that, tomorrow, given a new scenario is introduced, then it is just a configuration away from getting the newly introduced scenario involved in this process flow.&#x20;

This document explains the steps on how to define the configurations for the analytics side of DSS for W\&S.

**What is analytics?**

**Analytics:** Micro Service which is responsible for building, fetching, aggregating and computing the data on ElasticSearch to a consumable data response. This is later used for visualizations and graphical representations.&#x20;

**Analytics Configurations:** Analytics contains multiple configurations. We need to add the changes related to Water & Sewerage(W\&S) in this dashboard analytics.\
Here is the location: [<img src="https://github.com/fluidicon.png" alt="" data-size="line">configs/egov-dss-dashboards/dashboard-analytics at qa · egovernments/configs](https://github.com/egovernments/configs/tree/qa/egov-dss-dashboards/dashboard-analytics)\
Below is a list of configurations that need to be changed to run W\&S successfully.

1. Chart API Configuration
2. Master Dashboard Configuration
3. Role Dashboard Mappings Configuration

## Configuration Details <a href="#description" id="description"></a>

### **Chart API Configuration**

Each visualization has its own properties. Each visualization comes from different data sources (Sometimes it is a combination of different data sources). In order to configure each visualization and its properties, we have a chart API configuration document.

In this, visualization code, which happens to be the key, will be having its properties configured as a part of the configuration and are easily changeable.

Here is the sample ChartApiConfiguration.json data for the W\&S.

```
"_comment": "W&S charts below-----------------------------------------------------------------------",

  "wstodaysCollection": {
    "chartName": "DSS_W&S_TODAYS_COLLECTION",
    "queries": [
      {
        "module": "W&S",
        "indexName": "dss-collection_v2",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must\":[{\"range\":{\"dataObject.paymentDetails.receiptDate\":{\"gte\":\"now-1d\/d\",\"lte\":\"now\"}}},{\"terms\":{\"dataObject.paymentDetails.businessService.keyword\":[\"WS\",\"WS.ONE_TIME_FEE\",\"SW.ONE_TIME_FEE\",\"SW\"]}}],\"must_not\":[{\"term\":{\"dataObject.tenantId.keyword\":\"pb.testing\"}},{\"term\":{\"dataObject.paymentStatus.keyword\":\"Cancelled\"}}]}},\"aggs\":{\"Total Collection\":{\"sum\":{\"field\":\"dataObject.paymentDetails.totalAmountPaid\"}}}}}}",
        "requestQueryMap": "{\"tenantId\" : \"dataObject.tenantId.keyword\", \"wardId\" : \"domainObject.ward.name.keyword\"}",
        "dateRefField": ""
      }
    ],
    "chartType": "metric",
    "valueType": "amount",
    "action": "",
    "drillChart": "none",
    "aggregationPaths": [
      "Total Collection"
    ],
    "insight": {
    },
    "_comment": "W&S todays collections "
  },
  "wstotalCollection": {
    "chartName": "DSS_W&S_TOTAL_COLLECTION",
    "queries": [
      {
        "module": "W&S",
        "indexName": "dss-collection_v2",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"dataObject.tenantId.keyword\":\"pb.testing\"}},{\"terms\":{\"dataObject.paymentDetails.bill.status.keyword\":[\"Cancelled\"]}}],\"must\":[{\"terms\":{\"dataObject.paymentDetails.businessService.keyword\":[\"WS\",\"WS.ONE_TIME_FEE\",\"SW.ONE_TIME_FEE\",\"SW\"]}}]}},\"aggs\":{\"Total Collection\":{\"sum\":{\"field\":\"dataObject.paymentDetails.totalAmountPaid\"}}}}}}",
        "requestQueryMap": "{\"tenantId\" : \"dataObject.tenantId.keyword\", \"wardId\" : \"domainObject.ward.name.keyword\"}",
        "dateRefField": "dataObject.paymentDetails.receiptDate"
      }
    ],
    "translateTenantCode": false,
    "chartType": "metric",
    "valueType": "amount",
    "action": "",
    "drillChart": "none",
    "aggregationPaths": [
      "Total Collection"
    ],
    "insight": {
      "chartResponseMap" : "wstotalCollection",
      "action" : "differenceOfNumbers",
      "upwardIndicator" : "positive",
      "downwardIndicator" : "negative",
      "textMessage" : "$indicator$value% than last $insightInterval",
      "colorCode" : "#228B22",
      "insightInterval" : "year",
      "isRoundOff": true
    },
    "_comment": "W&S total collections "
  },
  "wstargetCollection": {
    "chartName": "DSS_W&S_TARGET_COLLECTION",
    "queries": [
      {
        "module": "W&S",
        "requestQueryMap": "{\"module\" : \"businessService.keyword\", \"tenantId\" : \"tenantIdForMunicipalCorporation.keyword\"}",
        "dateRefField": "",
        "indexName": "dss-target_v1",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must\":[{\"term\":{\"businessService.keyword\":\"W&S\"}}]}},\"aggs\":{\"Target Collection\":{\"sum\":{\"field\":\"budgetProposedForMunicipalCorporation\"}}}}}}"
      }
    ],
    "chartType": "metric",
    "valueType": "amount",
    "action": "",
    "drillChart": "none",
    "documentType": "_doc",
    "aggregationPaths": [
      "Target Collection"
    ],
    "isDayUnit": false,
    "postAggregationTheory" : "repsonseToDifferenceOfDates",
    "insight": {
      "chartResponseMap" : "wstargetCollection",
      "action" : "differenceOfNumbers",
      "upwardIndicator" : "positive",
      "downwardIndicator" : "negative",
      "textMessage" : "$indicator$value% than last $insightInterval",
      "colorCode" : "#228B22",
      "insightInterval" : "year",
      "isRoundOff": true
    },
    "_comment": " "
  },
  "wstargetAchieved": {
    "chartName": "DSS_W&S_TARGET_ACHIEVED",
    "queries": [
      {
        "module": "W&S",
        "requestQueryMap": "{\r\n  \"module\" : \"businessService.keyword\", \n\"tenantId\" : \"tenantIdForMunicipalCorporation.keyword\"}",
        "dateRefField": "",
        "indexName": "dss-target_v1",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must\":[{\"term\":{\"businessService.keyword\":\"W&S\"}}]}},\"aggs\":{\"Target Collection\":{\"sum\":{\"field\":\"budgetProposedForMunicipalCorporation\"}}}}}}"
      },
      {
        "module": "W&S",
        "requestQueryMap": "{\"tenantId\" : \"dataObject.tenantId.keyword\", \"wardId\" : \"domainObject.ward.name.keyword\"}",
        "dateRefField": "dataObject.paymentDetails.receiptDate",
        "indexName": "dss-collection_v2",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"dataObject.tenantId.keyword\":\"pb.testing\"}},{\"terms\":{\"dataObject.paymentDetails.bill.status.keyword\":[\"Cancelled\"]}}],\"must\":[{\"terms\":{\"dataObject.paymentDetails.businessService.keyword\":[\"WS\",\"WS.ONE_TIME_FEE\",\"SW.ONE_TIME_FEE\",\"SW\"]}}]}},\"aggs\":{\"Total Collection\":{\"sum\":{\"field\":\"dataObject.paymentDetails.totalAmountPaid\"}}}}}}"
      }
    ],
    "translateTenantCode": false,
    "chartType": "metric",
    "valueType": "percentage",
    "drillChart": "none",
    "documentType": "_doc",
    "action": "percentage",
    "aggregationPaths": [
      "Total Collection",
      "Target Collection"
    ],
    "preActionTheory":{
      "Target Collection":"repsonseToDifferenceOfDates"
    },
    "isRoundOff": true,
    "insight": {
      "chartResponseMap" : "wstargetAchieved",
      "action" : "differenceOfNumbers",
      "upwardIndicator" : "positive",
      "downwardIndicator" : "negative",
      "textMessage" : "$indicator$value% than last $insightInterval",
      "colorCode" : "#228B22",
      "insightInterval" : "year",
      "isRoundOff": true
    },
    "_comment": " "
  },
  "wscumulativeCollections": {
    "chartName": "DSS_W&S_TOTAL_CUMULATIVE_COLLECTION",
    "queries": [
      {
        "module": "W&S",
        "dateRefField": "dataObject.paymentDetails.receiptDate",
        "requestQueryMap": "{\"tenantId\" : \"dataObject.tenantId.keyword\", \"wardId\" : \"domainObject.ward.name.keyword\"}",
        "indexName": "dss-collection_v2",
        "aggrQuery": "{\"aggs\":{\"Water Collections\":{\"date_histogram\":{\"field\":\"dataObject.paymentDetails.receiptDate\",\"interval\":\"intervalvalue\"},\"aggs\":{\"Water\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"dataObject.tenantId.keyword\":\"pb.testing\"}},{\"terms\":{\"dataObject.paymentStatus.keyword\":[\"Cancelled\"]}}],\"must\":[{\"terms\":{\"dataObject.paymentStatus.keyword\":[\"DEPOSITED\",\"NEW\"]}},{\"terms\":{\"dataObject.paymentDetails.businessService.keyword\":[\"WS\",\"WS.ONE_TIME_FEE\"]}}]}},\"aggs\":{\"Count\":{\"sum\":{\"field\":\"dataObject.paymentDetails.totalAmountPaid\"}}}}}},\"Sewerage Collections\":{\"date_histogram\":{\"field\":\"dataObject.paymentDetails.receiptDate\",\"interval\":\"intervalvalue\"},\"aggs\":{\"Sewerage\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"dataObject.tenantId.keyword\":\"pb.testing\"}},{\"terms\":{\"dataObject.paymentStatus.keyword\":[\"Cancelled\"]}}],\"must\":[{\"terms\":{\"dataObject.paymentStatus.keyword\":[\"DEPOSITED\",\"NEW\"]}},{\"terms\":{\"dataObject.paymentDetails.businessService.keyword\":[\"SW.ONE_TIME_FEE\",\"SW\"]}}]}},\"aggs\":{\"Count\":{\"sum\":{\"field\":\"dataObject.paymentDetails.totalAmountPaid\"}}}}}}}}"
      }
    ],
    "translateTenantCode": false,
    "chartType": "line",
    "valueType": "amount",
    "action": "",
    "drillChart": "none",
    "documentType": "_doc",
    "aggregationPaths": [
      "Water Collections",
      "Sewerage Collections"
    ],
    "isCumulative": true,
    "interval": "month",
    "insight": {
    },
    "_comment": " "
  },

  "wstopPerformingUlbs": {
    "chartName": "DSS_W&S_TOP_3_PERFORMING_ULBS",
    "queries": [
      {
        "module": "W&S",
        "requestQueryMap": "{\"module\" : \"businessService.keyword\", \"tenantId\" : \"tenantIdForMunicipalCorporation.keyword\"}",
        "dateRefField": "",
        "indexName": "dss-target_v1",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must\":[{\"term\":{\"businessService.keyword\":\"W&S\"}}]}},\"aggs\":{\"Target Collection\":{\"terms\":{\"field\":\"tenantIdForMunicipalCorporation.keyword\",\"size\":\"200\",\"order\":{\"Sum\":\"desc\"}},\"aggs\":{\"Sum\":{\"sum\":{\"field\":\"budgetProposedForMunicipalCorporation\"}}}}}}}}"
      },
      {
        "module": "W&S",
        "requestQueryMap": "{\"tenantId\" : \"dataObject.tenantId.keyword\", \"wardId\" : \"domainObject.ward.name.keyword\"}",
        "dateRefField": "dataObject.paymentDetails.receiptDate",
        "indexName": "dss-collection_v2",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"dataObject.tenantId.keyword\":\"pb.testing\"}},{\"terms\":{\"dataObject.paymentDetails.bill.status.keyword\":[\"Cancelled\"]}}],\"must\":[{\"terms\":{\"dataObject.paymentDetails.businessService.keyword\":[\"WS\",\"WS.ONE_TIME_FEE\",\"SW.ONE_TIME_FEE\",\"SW\"]}}]}},\"aggs\":{\"Total Collection\":{\"terms\":{\"field\":\"dataObject.tenantId.keyword\",\"size\":\"200\",\"order\":{\"Sum\":\"desc\"}},\"aggs\":{\"Sum\":{\"sum\":{\"field\":\"dataObject.paymentDetails.totalAmountPaid\"}}}}}}}}"
      }
    ],
    "translateTenantCode": false,
    "chartType": "perform",
    "valueType": "percentage",
    "drillChart": "none",
    "documentType": "_doc",
    "action": "percentage",
    "plotLabel": "DSS_TARGET_ACHIEVED",
    "order": "desc",
    "limit": 3,
    "isRoundOff": true,
    "aggregationPaths": [
      "Total Collection","Target Collection"
    ],
    "preActionTheory":{
      "Target Collection":"repsonseToDifferenceOfDates"
    },
    "insight": {
    },
    "_comment": " Top Performing Ulbs for target achieved"
  },
  "wsbottomPerformingUlbs": {
    "chartName": "DSS_W&S_BOTTOM_3_PERFORMING_ULBS",
    "queries": [
      {
        "module": "W&S",
        "requestQueryMap": "{\"module\" : \"businessService.keyword\", \"tenantId\" : \"tenantIdForMunicipalCorporation.keyword\"}",
        "dateRefField": "",
        "indexName": "dss-target_v1",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must\":[{\"term\":{\"businessService.keyword\":\"W&S\"}}]}},\"aggs\":{\"Target Collection\":{\"terms\":{\"field\":\"tenantIdForMunicipalCorporation.keyword\",\"size\":\"200\",\"order\":{\"Sum\":\"asc\"}},\"aggs\":{\"Sum\":{\"sum\":{\"field\":\"budgetProposedForMunicipalCorporation\"}}}}}}}}"
      },
      {
        "module": "W&S",
        "requestQueryMap": "{\"tenantId\" : \"dataObject.tenantId.keyword\", \"wardId\" : \"domainObject.ward.name.keyword\"}",
        "dateRefField": "dataObject.paymentDetails.receiptDate",
        "indexName": "dss-collection_v2",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"dataObject.tenantId.keyword\":\"pb.testing\"}},{\"terms\":{\"dataObject.paymentDetails.bill.status.keyword\":[\"Cancelled\"]}}],\"must\":[{\"terms\":{\"dataObject.paymentDetails.businessService.keyword\":[\"WS\",\"WS.ONE_TIME_FEE\",\"SW.ONE_TIME_FEE\",\"SW\"]}}]}},\"aggs\":{\"Total Collection\":{\"terms\":{\"field\":\"dataObject.tenantId.keyword\",\"size\":\"200\",\"order\":{\"Sum\":\"asc\"}},\"aggs\":{\"Sum\":{\"sum\":{\"field\":\"dataObject.paymentDetails.totalAmountPaid\"}}}}}}}}"
      }
    ],
    "translateTenantCode": false,
    "chartType": "perform",
    "valueType": "percentage",
    "drillChart": "none",
    "documentType": "_doc",
    "action": "percentage",
    "plotLabel": "DSS_TARGET_ACHIEVED",
    "order": "asc",
    "limit": 3,
    "isRoundOff": true,
    "aggregationPaths": [
      "Total Collection", "Target Collection"
    ],
    "preActionTheory":{
      "Target Collection":"repsonseToDifferenceOfDates"
    },
    "insight": {
    },
    "_comment": " Bottom Performing Ulbs for target achieved"
  },
  "wscollectionByUsage": {
    "chartName": "DSS_W&S_COLLECTION_BY_USAGE",
    "queries": [
      {
        "module": "W&S",
        "dateRefField": "dataObject.paymentDetails.receiptDate",
        "requestQueryMap": "{\"tenantId\" : \"dataObject.tenantId.keyword\", \"wardId\" : \"domainObject.ward.name.keyword\"}",
        "indexName": "dss-collection_v2",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"dataObject.tenantId.keyword\":\"pb.testing\"}},{\"terms\":{\"dataObject.paymentDetails.bill.status.keyword\":[\"Cancelled\"]}}],\"must\":[{\"terms\":{\"dataObject.paymentDetails.businessService.keyword\":[\"WS\",\"WS.ONE_TIME_FEE\",\"SW.ONE_TIME_FEE\",\"SW\"]}}]}},\"aggs\":{\"Collection by Usage\":{\"terms\":{\"field\":\"domainObject.propertyUsageType.keyword\"},\"aggs\":{\"total collection\":{\"sum\":{\"field\":\"dataObject.paymentDetails.totalAmountPaid\"}}}}}}}}"
      }
    ],
    "translateTenantCode": false,
    "chartType": "pie",
    "valueType": "amount",
    "action": "",
    "documentType": "_doc",
    "drillChart": "none",
    "aggregationPaths": [
      "Collection by Usage"
    ],
    "insight": {
    },
    "_comment": " "
  },

  "wscollectionByChannel": {
    "chartName": "DSS_W&S_COLLECTION_BY_CHANNEL",
    "queries": [
      {
        "module": "W&S",
        "dateRefField": "dataObject.paymentDetails.receiptDate",
        "requestQueryMap": "{\"tenantId\" : \"dataObject.tenantId.keyword\", \"wardId\" : \"domainObject.ward.name.keyword\"}",
        "indexName": "dss-collection_v2",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"dataObject.tenantId.keyword\":\"pb.testing\"}},{\"terms\":{\"dataObject.paymentDetails.bill.status.keyword\":[\"Cancelled\"]}}],\"must\":[{\"terms\":{\"dataObject.paymentDetails.businessService.keyword\":[\"WS\",\"WS.ONE_TIME_FEE\",\"SW.ONE_TIME_FEE\",\"SW\"]}}]}},\"aggs\":{\"Collection Channels\":{\"terms\":{\"field\":\"dataObject.paymentMode.keyword\"},\"aggs\":{\"totalcollection_frommode\":{\"sum\":{\"field\":\"dataObject.paymentDetails.totalAmountPaid\"}}}}}}}}"
      }
    ],
    "translateTenantCode": false,
    "chartType": "pie",
    "valueType": "amount",
    "action": "",
    "documentType": "_doc",
    "drillChart": "none",
    "aggregationPaths": [
      "Collection Channels"
    ],
    "insight": {
    },
    "_comment": " "
  },

  "wsFinancialIndicatorDDR": {
    "chartName": "DSS_WS_KEY_FY_INDICATORS",
    "queries": [
      {
        "module": "COMMON",
        "requestQueryMap": "{\"wardId\" : \"domainObject.ward.name.keyword\",\"module\" : \"dataObject.paymentDetails.businessService.keyword\", \"tenantId\" : \"dataObject.tenantId.keyword\", \"district\" : \"dataObject.tenantData.city.districtCode\" }",
        "dateRefField": "dataObject.paymentDetails.receiptDate",
        "indexName": "dss-collection_v2",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"dataObject.tenantId.keyword\":\"pb.testing\"}},{\"terms\":{\"dataObject.paymentDetails.bill.status.keyword\":[\"Cancelled\"]}}],\"must\":[{\"terms\":{\"dataObject.paymentDetails.businessService.keyword\":[\"WS\",\"WS.ONE_TIME_FEE\",\"SW.ONE_TIME_FEE\",\"SW\"]}}]}},\"aggs\":{\"Ws_Total_Collection\":{\"sum\":{\"field\":\"dataObject.paymentDetails.totalAmountPaid\"}},\"Total_Transactions\":{\"value_count\":{\"field\":\"dataObject.transactionNumber.keyword\"}}}}}}"
      },
      {
        "module": "COMMON",
        "requestQueryMap": "{\"module\" : \"businessService.keyword\", \"tenantId\" : \"tenantIdForMunicipalCorporation.keyword\"}",
        "dateRefField": "",
        "indexName": "dss-target_v1",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must\":[{\"terms\":{\"businessService.keyword\":[\"W&S\"]}}]}},\"aggs\":{\"Ws_Target_Collection\":{\"sum\":{\"field\":\"budgetProposedForMunicipalCorporation\"}}}}}}"      
      },
      {
      "module": "COMMON",
      "indexName": "water-services",
      "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.applicationStatus.keyword\":\"REJECTED\"}},{\"term\":{\"Data.tenantId.keyword\":\"pb.testing\"}}],\"must\":[{\"terms\":{\"Data.applicationStatus.keyword\":[\"CONNECTION_ACTIVATED\"]}}]}},\"aggs\":{\"Total_Connections\":{\"value_count\":{\"field\":\"Data.id.keyword\"}}}}}}",
      "requestQueryMap": "{\"tenantId\" : \"Data.tenantId.keyword\", \"wardId\" : \"Data.ward.name.keyword\"}",
      "dateRefField": "Data.connectionExecutionDate"
      },
      {
      "module": "COMMON",
      "indexName": "sewerage-services",
      "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.applicationStatus.keyword\":\"REJECTED\"}},{\"term\":{\"Data.tenantId.keyword\":\"pb.testing\"}}],\"must\":[{\"terms\":{\"Data.applicationStatus.keyword\":[\"CONNECTION_ACTIVATED\"]}}]}},\"aggs\":{\"Total_Connections\":{\"value_count\":{\"field\":\"Data.id.keyword\"}}}}}}",
      "requestQueryMap": "{\"tenantId\" : \"Data.tenantId.keyword\", \"wardId\" : \"Data.ward.name.keyword\"}",
      "dateRefField": "Data.connectionExecutionDate"
      }
    ],
    "isMdmsEnabled": true,
    "filterKeys": [
      {"key": "tenantId", "column": "DDRs"}
    ],
    "chartType": "xtable",
    "valueType": "number",
    "drillChart": "wsFinancialIndicatorUlb",
    "action": "",
    "plotLabel": "DDRs",
    "isPostResponseHandler": true,
    "postAggregationTheory" : "repsonseToDifferenceOfDates",
    "documentType": "_doc",
    "aggregationPaths": [
      "Ws_Target_Collection",
      "Total_Connections",
      "Total_Transactions", 
      "Ws_Total_Collection"        
    ],
    "computedFields": [
      {
        "postAggregationTheory" : "repsonseToDifferenceOfDates",
        "actionName": "AdditiveComputedField",
        "fields" : ["Ws_Target_Collection"],
        "newField" : "Target_Collection",
        "_comments": "fields are field names picked from its aggregation query to use post aggregation newField value with given new field name  "
      },
      {
         "postAggregationTheory" : "",
         "actionName": "PercentageComputedField",
         "fields" : ["Ws_Total_Collection","Target_Collection"],
         "newField" : "Target_Achieved",
         "_comments": "fields are field names picked from its aggregation query to use post aggregation newField value with given new field name  "
       }
     ],
     "excludedColumns":["Ws_Target_Collection"],
     "pathDataTypeMapping": [
      {
        "Ws_Target_Collection": "amount"
      },
      {
        "Total_Connections": "number"
      },
      {
        "Total_Transactions": "number"
      },
      {
        "Ws_Total_Collection": "amount"
      },
      {
        "Target_Collection": "amount"
      },
      {
        "Target_Achieved": "percentage"
      }
    ],
    "insight": {
    },
    "_comment": ""
  },
  "wsFinancialIndicatorUlb": {
    "chartName": "DSS_W&S_DEMAND_COLLECTION_BOUNDARY",
    "queries": [
      {
        "module": "COMMON",
        "requestQueryMap": "{\"wardId\" : \"domainObject.ward.name.keyword\",\"module\" : \"dataObject.paymentDetails.businessService.keyword\", \"tenantId\" : \"dataObject.tenantId.keyword\", \"district\" : \"dataObject.tenantData.city.districtCode\" }",
        "dateRefField": "dataObject.paymentDetails.receiptDate",
        "indexName": "dss-collection_v2",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"dataObject.tenantId.keyword\":\"pb.testing\"}},{\"terms\":{\"dataObject.paymentDetails.bill.status.keyword\":[\"Cancelled\"]}}],\"must\":[{\"terms\":{\"dataObject.paymentDetails.businessService.keyword\":[\"WS\",\"WS.ONE_TIME_FEE\",\"SW.ONE_TIME_FEE\",\"SW\"]}}]}},\"aggs\":{\"ULBs \":{\"terms\":{\"field\":\"dataObject.tenantId.keyword\",\"size\":200},\"aggs\":{\"Ws_Total_Collection\":{\"sum\":{\"field\":\"dataObject.paymentDetails.totalAmountPaid\"}},\"Total_Transactions\":{\"value_count\":{\"field\":\"dataObject.transactionNumber.keyword\"}}}}}}}}"
      },
      {
        "module": "COMMON",
        "requestQueryMap": "{\"module\" : \"businessService.keyword\", \"tenantId\" : \"tenantIdForMunicipalCorporation.keyword\"}",
        "dateRefField": "",
        "indexName": "dss-target_v1",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must\":[{\"terms\":{\"businessService.keyword\":[\"W&S\"]}}]}},\"aggs\":{\"ULBs \":{\"terms\":{\"field\":\"tenantIdForMunicipalCorporation.keyword\",\"size\":1000},\"aggs\":{\"Ws_Target_Collection\":{\"sum\":{\"field\":\"budgetProposedForMunicipalCorporation\"}}}}}}}}"
      },
      {
      "module": "COMMON",
      "indexName": "water-services",
      "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.applicationStatus.keyword\":\"REJECTED\"}}],\"must\":[{\"terms\":{\"Data.applicationStatus.keyword\":[\"CONNECTION_ACTIVATED\"]}}]}},\"aggs\":{\"ULB\":{\"terms\":{\"field\":\"Data.tenantId.keyword\",\"size\":2000},\"aggs\":{\"Total_Connections\":{\"value_count\":{\"field\":\"Data.id.keyword\"}}}}}}}}",
      "requestQueryMap": "{\"tenantId\" : \"Data.tenantId.keyword\", \"wardId\" : \"Data.ward.name.keyword\"}",
      "dateRefField": "Data.connectionExecutionDate"
      },
      {
      "module": "COMMON",
      "indexName": "sewerage-services",
      "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.applicationStatus.keyword\":\"REJECTED\"}}],\"must\":[{\"terms\":{\"Data.applicationStatus.keyword\":[\"CONNECTION_ACTIVATED\"]}}]}},\"aggs\":{\"ULB\":{\"terms\":{\"field\":\"Data.tenantId.keyword\",\"size\":2000},\"aggs\":{\"Total_Connections\":{\"value_count\":{\"field\":\"Data.id.keyword\"}}}}}}}}",
      "requestQueryMap": "{\"tenantId\" : \"Data.tenantId.keyword\", \"wardId\" : \"Data.ward.name.keyword\"}",
      "dateRefField": "Data.connectionExecutionDate"
      }
    ],
    "filterKeys": [
      {"key": "tenantId", "column": "ULB"}
    ],
    "chartType": "xtable",
    "valueType": "number",
    "drillChart": "wsFinancialIndicatorWard",
    "documentType": "_doc",
    "action": "",
    "plotLabel": "ULB",
    "postAggregationTheory" : "repsonseToDifferenceOfDates",
    "aggregationPaths": [
      "Ws_Target_Collection",
      "Total_Connections",
      "Total_Transactions", 
      "Ws_Total_Collection"       
    ],
    "computedFields": [
      {
        "postAggregationTheory" : "repsonseToDifferenceOfDates",
        "actionName": "AdditiveComputedField",
        "fields" : ["Ws_Target_Collection"],
        "newField" : "Target_Collection",
        "_comments": "fields are field names picked from its aggregation query to use post aggregation newField value with given new field name  "
      },
      {
         "postAggregationTheory" : "",
         "actionName": "PercentageComputedField",
         "fields" : ["Ws_Total_Collection","Target_Collection"],
         "newField" : "Target_Achieved",
         "_comments": "fields are field names picked from its aggregation query to use post aggregation newField value with given new field name  "
       }
     ],
     "excludedColumns":["Ws_Target_Collection"],
     "pathDataTypeMapping": [
      {
        "Ws_Target_Collection": "amount"
      },
      {
        "Total_Connections": "number"
      },
      {
        "Total_Transactions": "number"
      },
      {
        "Ws_Total_Collection": "amount"
      },
      {
        "Target_Collection": "amount"
      },
      {
        "Target_Achieved": "percentage"
      }
    ],
    "insight": {
    },
    "_comment": ""
  },
  "wsFinancialIndicatorWard": {
    "chartName": "",
    "queries": [
      {
        "module": "COMMON",
        "requestQueryMap": "{\"wardId\" : \"domainObject.ward.name.keyword\",\"module\" : \"dataObject.paymentDetails.businessService.keyword\", \"tenantId\" : \"dataObject.tenantId.keyword\", \"district\" : \"dataObject.tenantData.city.districtCode\" }",
        "dateRefField": "dataObject.paymentDetails.receiptDate",
        "indexName": "dss-collection_v2",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"dataObject.tenantId.keyword\":\"pb.testing\"}},{\"terms\":{\"dataObject.paymentDetails.bill.status.keyword\":[\"Cancelled\"]}}],\"must\":[{\"terms\":{\"dataObject.paymentDetails.businessService.keyword\":[\"WS\",\"WS.ONE_TIME_FEE\",\"SW.ONE_TIME_FEE\",\"SW\"]}}]}},\"aggs\":{\"Ward \":{\"terms\":{\"field\":\"domainObject.ward.name.keyword\",\"size\":200},\"aggs\":{\"Ws_Total_Collection\":{\"sum\":{\"field\":\"dataObject.paymentDetails.totalAmountPaid\"}},\"Total_Transactions\":{\"value_count\":{\"field\":\"dataObject.transactionNumber.keyword\"}}}}}}}}"
      },
      {
      "module": "COMMON",
      "indexName": "water-services",
      "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.applicationStatus.keyword\":\"REJECTED\"}}],\"must\":[{\"terms\":{\"Data.applicationStatus.keyword\":[\"CONNECTION_ACTIVATED\"]}}]}},\"aggs\":{\"Ward\":{\"terms\":{\"field\":\"Data.ward.name.keyword\",\"size\":2000},\"aggs\":{\"Total_Connections\":{\"value_count\":{\"field\":\"Data.id.keyword\"}}}}}}}}",
      "requestQueryMap": "{\"tenantId\" : \"Data.tenantId.keyword\", \"wardId\" : \"Data.ward.name.keyword\"}",
      "dateRefField": "Data.connectionExecutionDate"
      },
      {
      "module": "COMMON",
      "indexName": "sewerage-services",
      "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.applicationStatus.keyword\":\"REJECTED\"}}],\"must\":[{\"terms\":{\"Data.applicationStatus.keyword\":[\"CONNECTION_ACTIVATED\"]}}]}},\"aggs\":{\"Ward\":{\"terms\":{\"field\":\"Data.ward.name.keyword\",\"size\":2000},\"aggs\":{\"Total_Connections\":{\"value_count\":{\"field\":\"Data.id.keyword\"}}}}}}}}",
      "requestQueryMap": "{\"tenantId\" : \"Data.tenantId.keyword\", \"wardId\" : \"Data.ward.name.keyword\"}",
      "dateRefField": "Data.connectionExecutionDate"
      }
    ],
    "postAggregationTheory" : "repsonseToDifferenceOfDates",
    "chartType": "xtable",
    "valueType": "number",
    "drillChart": "none",
    "documentType": "_doc",
    "action": "",
    "plotLabel": "Ward",
    "aggregationPaths": [
      "Total_Connections",
      "Total_Transactions", 
      "Ws_Total_Collection"
    ],
    "pathDataTypeMapping": [
      {
        "Total_Connections": "number"
      },
      {
        "Total_Transactions": "number"
      },
      {
        "Ws_Total_Collection": "amount"
      }
    ],
    "insight": {
    },
    "_comment": ""
  },

  "wsTaxHeadDDR": {
    "chartName": "DSS_W&S_TAX_HEAD_BOUNDARY",
    "queries": [
      {
        "module": "W&S",
        "requestQueryMap": "{\"wardId\" : \"domainObject.ward.name.keyword\",\"module\" : \"dataObject.paymentDetails.businessService.keyword\", \"tenantId\" : \"dataObject.tenantId.keyword\", \"district\" : \"dataObject.tenantData.city.districtCode\" }",
        "dateRefField": "dataObject.paymentDetails.receiptDate",
        "indexName": "dss-collection_v2",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"dataObject.tenantId.keyword\":\"pb.testing\"}},{\"terms\":{\"dataObject.paymentDetails.bill.status.keyword\":[\"Cancelled\"]}}],\"must\":[{\"terms\":{\"dataObject.paymentDetails.businessService.keyword\":[\"WS\",\"WS.ONE_TIME_FEE\",\"SW.ONE_TIME_FEE\",\"SW\"]}}]}},\"aggs\":{\"Ws_Total_Collection\":{\"sum\":{\"field\":\"dataObject.paymentDetails.totalAmountPaid\"}},\"Penalty\":{\"nested\":{\"path\":\"dataObject.paymentDetails.bill.billDetails.billAccountDetails\"},\"aggs\":{\"aggrFilter\":{\"filter\":{\"terms\":{\"dataObject.paymentDetails.bill.billDetails.billAccountDetails.taxHeadCode.keyword\":[\"SW_TIME_PENALTY\",\"WS_TIME_PENALTY\"]}},\"aggs\":{\"amount\":{\"sum\":{\"field\":\"dataObject.paymentDetails.bill.billDetails.billAccountDetails.amount\"}}}}}},\"Interest\":{\"nested\":{\"path\":\"dataObject.paymentDetails.bill.billDetails.billAccountDetails\"},\"aggs\":{\"aggrFilter\":{\"filter\":{\"terms\":{\"dataObject.paymentDetails.bill.billDetails.billAccountDetails.taxHeadCode.keyword\":[\"SW_TIME_INTEREST\",\"WS_TIME_INTEREST\"]}},\"aggs\":{\"amount\":{\"sum\":{\"field\":\"dataObject.paymentDetails.bill.billDetails.billAccountDetails.amount\"}}}}}}}}}}"
      },
      {
        "module": "W&S",
        "requestQueryMap": "{\"module\" : \"businessService.keyword\", \"tenantId\" : \"tenantIdForMunicipalCorporation.keyword\"}",
        "dateRefField": "",
        "indexName": "dss-target_v1",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must\":[{\"terms\":{\"businessService.keyword\":[\"W&S\"]}}]}},\"aggs\":{\"Ws_Target_Collection\":{\"sum\":{\"field\":\"budgetProposedForMunicipalCorporation\"}}}}}}"      
      }
    ],
    "translateTenantCode": false,
    "isMdmsEnabled": true,
    "filterKeys": [
      {"key": "tenantId", "column": "DDRs"}
    ],
    "chartType": "xtable",
    "valueType": "amount",
    "drillChart": "wsTaxHeadUlb",
    "action": "",
    "plotLabel": "DDRs",
    "postAggregationTheory" : "",
    "aggregationPaths": [
      "Ws_Total_Collection",
      "Penalty",
      "Interest",
	    "Ws_Target_Collection"
    ], 
    "computedFields": [
      {
        "postAggregationTheory" : "repsonseToDifferenceOfDates",
        "actionName": "AdditiveComputedField",
        "fields" : ["Ws_Target_Collection"],
        "newField" : "Target_Collection",
        "_comments": "fields are field names picked from its aggregation query to use post aggregation newField value with given new field name  "
      }
     ],
    "excludedColumns":["Ws_Target_Collection"],
    "pathDataTypeMapping": [
      {
        "Ws_Total_Collection": "amount"
      },
      {
        "Penalty": "amount"
      },
      {
        "Interest": "amount"
      },
      {
        "Ws_Target_Collection": "amount"
      },
      {
        "Target_Collection": "amount"
      }
    ],
    "insight": {
    },
    "_comment": ""
  },
  "wsTaxHeadUlb": {
    "chartName": "DSS_W&S_TAX_HEAD_BOUNDARY",
    "queries": [
      {
        "module": "W&S",
        "requestQueryMap": "{\"wardId\" : \"domainObject.ward.name.keyword\",\"module\" : \"dataObject.paymentDetails.businessService.keyword\", \"tenantId\" : \"dataObject.tenantId.keyword\", \"district\" : \"dataObject.tenantData.city.districtCode\" }",
        "dateRefField": "dataObject.paymentDetails.receiptDate",
        "indexName": "dss-collection_v2",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"dataObject.tenantId.keyword\":\"pb.testing\"}},{\"terms\":{\"dataObject.paymentDetails.bill.status.keyword\":[\"Cancelled\"]}}],\"must\":[{\"terms\":{\"dataObject.paymentDetails.businessService.keyword\":[\"WS\",\"WS.ONE_TIME_FEE\",\"SW.ONE_TIME_FEE\",\"SW\"]}}]}},\"aggs\":{\"ULBs \":{\"terms\":{\"field\":\"dataObject.tenantId.keyword\",\"size\":200},\"aggs\":{\"Ws_Total_Collection\":{\"sum\":{\"field\":\"dataObject.paymentDetails.totalAmountPaid\"}},\"Penalty\":{\"nested\":{\"path\":\"dataObject.paymentDetails.bill.billDetails.billAccountDetails\"},\"aggs\":{\"aggrFilter\":{\"filter\":{\"terms\":{\"dataObject.paymentDetails.bill.billDetails.billAccountDetails.taxHeadCode.keyword\":[\"SW_TIME_PENALTY\",\"WS_TIME_PENALTY\"]}},\"aggs\":{\"amount\":{\"sum\":{\"field\":\"dataObject.paymentDetails.bill.billDetails.billAccountDetails.amount\"}}}}}},\"Interest\":{\"nested\":{\"path\":\"dataObject.paymentDetails.bill.billDetails.billAccountDetails\"},\"aggs\":{\"aggrFilter\":{\"filter\":{\"terms\":{\"dataObject.paymentDetails.bill.billDetails.billAccountDetails.taxHeadCode.keyword\":[\"SW_TIME_INTEREST\",\"WS_TIME_INTEREST\"]}},\"aggs\":{\"amount\":{\"sum\":{\"field\":\"dataObject.paymentDetails.bill.billDetails.billAccountDetails.amount\"}}}}}}}}}}}}"
      },
      {
        "module": "W&S",
        "requestQueryMap": "{\"module\" : \"businessService.keyword\", \"tenantId\" : \"tenantIdForMunicipalCorporation.keyword\"}",
        "dateRefField": "",
        "indexName": "dss-target_v1",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must\":[{\"terms\":{\"businessService.keyword\":[\"W&S\"]}}]}},\"aggs\":{\"ULBs \":{\"terms\":{\"field\":\"tenantIdForMunicipalCorporation.keyword\",\"size\":1000},\"aggs\":{\"Ws_Target_Collection\":{\"sum\":{\"field\":\"budgetProposedForMunicipalCorporation\"}}}}}}}}"      
      }
    ],
    "translateTenantCode": false,
    "isMdmsEnabled": false,
    "filterKeys": [
      {"key": "tenantId", "column": "ULB"}
    ],
    "chartType": "xtable",
    "valueType": "amount",
    "drillChart": "wsTaxHeadWard",
    "action": "",
    "plotLabel": "ULB",
    "postAggregationTheory" : "",
    "aggregationPaths": [
      "Ws_Total_Collection",
      "Penalty",
      "Interest",
	    "Ws_Target_Collection"
    ], 
    "computedFields": [
      {
        "postAggregationTheory" : "repsonseToDifferenceOfDates",
        "actionName": "AdditiveComputedField",
        "fields" : ["Ws_Target_Collection"],
        "newField" : "Target_Collection",
        "_comments": "fields are field names picked from its aggregation query to use post aggregation newField value with given new field name  "
      }
     ],
    "excludedColumns":["Ws_Target_Collection"],
    "pathDataTypeMapping": [
      {
        "Ws_Total_Collection": "amount"
      },
      {
        "Penalty": "amount"
      },
      {
        "Interest": "amount"
      },
      {
        "Ws_Target_Collection": "amount"
      },
      {
        "Target_Collection": "amount"
      }
    ],
    "insight": {
    },
    "_comment": ""
  },
  "wsTaxHeadWard": {
    "chartName": "",
    "queries": [
      {
        "module": "W&S",
        "requestQueryMap": "{\"wardId\" : \"domainObject.ward.name.keyword\",\"module\" : \"dataObject.paymentDetails.businessService.keyword\", \"tenantId\" : \"dataObject.tenantId.keyword\", \"district\" : \"dataObject.tenantData.city.districtCode\" }",
        "dateRefField": "dataObject.paymentDetails.receiptDate",
        "indexName": "dss-collection_v2",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"dataObject.tenantId.keyword\":\"pb.testing\"}},{\"terms\":{\"dataObject.paymentDetails.bill.status.keyword\":[\"Cancelled\"]}}],\"must\":[{\"terms\":{\"dataObject.paymentDetails.businessService.keyword\":[\"WS\",\"WS.ONE_TIME_FEE\",\"SW.ONE_TIME_FEE\",\"SW\"]}}]}},\"aggs\":{\"Ward \":{\"terms\":{\"field\":\"domainObject.ward.name.keyword\",\"size\":200},\"aggs\":{\"Ws_Total_Collection\":{\"sum\":{\"field\":\"dataObject.paymentDetails.totalAmountPaid\"}},\"Penalty\":{\"nested\":{\"path\":\"dataObject.paymentDetails.bill.billDetails.billAccountDetails\"},\"aggs\":{\"aggrFilter\":{\"filter\":{\"terms\":{\"dataObject.paymentDetails.bill.billDetails.billAccountDetails.taxHeadCode.keyword\":[\"SW_TIME_PENALTY\",\"WS_TIME_PENALTY\"]}},\"aggs\":{\"amount\":{\"sum\":{\"field\":\"dataObject.paymentDetails.bill.billDetails.billAccountDetails.amount\"}}}}}},\"Interest\":{\"nested\":{\"path\":\"dataObject.paymentDetails.bill.billDetails.billAccountDetails\"},\"aggs\":{\"aggrFilter\":{\"filter\":{\"terms\":{\"dataObject.paymentDetails.bill.billDetails.billAccountDetails.taxHeadCode.keyword\":[\"SW_TIME_INTEREST\",\"WS_TIME_INTEREST\"]}},\"aggs\":{\"amount\":{\"sum\":{\"field\":\"dataObject.paymentDetails.bill.billDetails.billAccountDetails.amount\"}}}}}}}}}}}}"
      }
    ],
    "isMdmsEnabled": false,
    "translateTenantCode": false,
    "filterKeys": [
    ],
    "chartType": "xtable",
    "valueType": "amount",
    "drillChart": "none",
    "action": "",
    "plotLabel": "Ward",
    "postAggregationTheory" : "",
    "aggregationPaths": [
      "Ws_Total_Collection",
      "Penalty",
      "Interest"
    ],
    "pathDataTypeMapping": [
      {
        "Ws_Total_Collection": "amount"
      },
      {
        "Penalty": "amount"
      },
      {
        "Interest": "amount"
      }
    ],
    "insight": {
    },
    "_comment": ""
  },

  "wstotalApplications": {
    "chartName": "DSS_WS_TOTAL_APPLICATIONS",
    "queries": [
      {
        "module": "W&S",
        "indexName": "water-services",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"terms\":{\"Data.applicationStatus.keyword\":[\"REJECTED\",\"CONNECTION_ACTIVATED\"]}}]}},\"aggs\":{\"Total Water Applications\":{\"value_count\":{\"field\":\"Data.id.keyword\"}}}}}}",
        "requestQueryMap": "{\"tenantId\" : \"Data.tenantId.keyword\", \"wardId\" : \"Data.ward.name.keyword\"}",
        "dateRefField": "Data.@timestamp"
      },
      {
        "module": "W&S",
        "indexName": "sewerage-services",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"terms\":{\"Data.applicationStatus.keyword\":[\"REJECTED\",\"CONNECTION_ACTIVATED\"]}}]}},\"aggs\":{\"Total Sewerage Applications\":{\"value_count\":{\"field\":\"Data.id.keyword\"}}}}}}",
        "requestQueryMap": "{\"tenantId\" : \"Data.tenantId.keyword\", \"wardId\" : \"Data.ward.name.keyword\"}",
        "dateRefField": "Data.@timestamp"
      }
    ],
    "translateTenantCode": false,
    "chartType": "metric",
    "valueType": "number",
    "action": "additive",
    "drillChart": "none",
    "aggregationPaths": [
      "Total Water Applications","Total Sewerage Applications"
    ],
    "insight": {
      "chartResponseMap" : "wstotalApplications",
      "action" : "differenceOfNumbers",
      "upwardIndicator" : "positive",
      "downwardIndicator" : "negative",
      "textMessage" : "$indicator$value% than last $insightInterval",
      "colorCode" : "#228B22",
      "insightInterval" : "year",
      "isRoundOff": true
    },
    "_comment": ""
  },
  "wstotalConnection": {
    "chartName": "DSS_WS_ACTIVE_CONNECTIONS",
    "queries": [
      {
        "module": "W&S",
        "indexName": "water-services",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.applicationStatus.keyword\":\"REJECTED\"}}],\"must\":[{\"terms\":{\"Data.applicationStatus.keyword\":[\"CONNECTION_ACTIVATED\"]}}]}},\"aggs\":{\"Total Water Connection\":{\"value_count\":{\"field\":\"Data.id.keyword\"}}}}}}",
        "requestQueryMap": "{\"tenantId\" : \"Data.tenantId.keyword\", \"wardId\" : \"Data.ward.name.keyword\"}",
        "dateRefField": "Data.connectionExecutionDate"
      },
      {
        "module": "W&S",
        "indexName": "sewerage-services",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.applicationStatus.keyword\":\"REJECTED\"}}],\"must\":[{\"terms\":{\"Data.applicationStatus.keyword\":[\"CONNECTION_ACTIVATED\"]}}]}},\"aggs\":{\"Total Sewerage Connection\":{\"value_count\":{\"field\":\"Data.id.keyword\"}}}}}}",
        "requestQueryMap": "{\"tenantId\" : \"Data.tenantId.keyword\", \"wardId\" : \"Data.ward.name.keyword\"}",
        "dateRefField": "Data.connectionExecutionDate"
      }
    ],
    "translateTenantCode": false,
    "chartType": "metric",
    "valueType": "number",
    "action": "additive",
    "drillChart": "none",
    "aggregationPaths": [
      "Total Water Connection","Total Sewerage Connection"
    ],
    "insight": {
      "chartResponseMap" : "wstotalConnection",
      "action" : "differenceOfNumbers",
      "upwardIndicator" : "positive",
      "downwardIndicator" : "negative",
      "textMessage" : "$indicator$value% than last $insightInterval",
      "colorCode" : "#228B22",
      "insightInterval" : "year",
      "isRoundOff": true
    },
    "_comment": " "
  },
  
  "wsActiveWaterConnection": {
    "chartName": "DSS_WS_ACTIVE_WATER_CONNECTIONS",
    "queries": [
      {
        "module": "WS",
        "indexName": "water-services",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.applicationStatus.keyword\":\"REJECTED\"}}],\"must\":[{\"terms\":{\"Data.applicationStatus.keyword\":[\"CONNECTION_ACTIVATED\"]}}]}},\"aggs\":{\"Active Water Connections\":{\"value_count\":{\"field\":\"Data.id.keyword\"}}}}}}",
        "requestQueryMap": "{\"tenantId\" : \"Data.tenantId.keyword\", \"wardId\" : \"Data.ward.name.keyword\"}",
        "dateRefField": "Data.connectionExecutionDate"
      }
    ],
    "translateTenantCode": false,
    "chartType": "metric",
    "valueType": "number",
    "action": "",
    "drillChart": "none",
    "aggregationPaths": [
      "Active Water Connections"
    ],
    "insight": {
      "chartResponseMap" : "wsActiveWaterConnection",
      "action" : "differenceOfNumbers",
      "upwardIndicator" : "positive",
      "downwardIndicator" : "negative",
      "textMessage" : "$indicator$value% than last $insightInterval",
      "colorCode" : "#228B22",
      "insightInterval" : "year",
      "isRoundOff": true
    },
    "_comment": "active water connections"
  },
  "wsSLACompliance": {
    "chartName": "DSS_WS_SLA_COMPLIANCE",
    "queries": [
      {
        "module": "WS",
        "indexName": "water-services",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.tenantId.keyword\":\"pb.testing\"}}]}},\"aggs\":{\"Closed With In Sla\":{\"filter\":{\"bool\":{\"must\":[{\"terms\":{\"Data.applicationStatus.keyword\":[\"CONNECTION_ACTIVATED\",\"REJECTED\"]}},{\"script\":{\"script\":{\"source\":\"doc['Data.auditDetails.lastModifiedTime'].date.millis - doc['Data.auditDetails.createdTime'].date.millis < params.threshold\",\"lang\":\"painless\",\"params\":{\"threshold\":172800000}}}}]}},\"aggs\":{\"count\":{\"terms\":{\"field\":\"Data.tenantId.keyword\"},\"aggs\":{\"tenant_count\":{\"value_count\":{\"field\":\"Data.tenantId.keyword\"}}}}}},\"Total Applications\":{\"terms\":{\"field\":\"Data.tenantId.keyword\"},\"aggs\":{\"tenant_count\":{\"value_count\":{\"field\":\"Data.tenantId.keyword\"}}}}}}}}",
        "requestQueryMap": "{\"wardId\" : \"Data.ward.name.keyword\",\"tenantId\" : \"Data.tenantId.keyword\" \r\n}",
        "dateRefField": "Data.history.auditDetails.createdTime"
      },
      {
        "module": "WS",
        "indexName": "sewerage-services",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.tenantId.keyword\":\"pb.testing\"}}]}},\"aggs\":{\"Closed With In Sla\":{\"filter\":{\"bool\":{\"must\":[{\"terms\":{\"Data.applicationStatus.keyword\":[\"CONNECTION_ACTIVATED\",\"REJECTED\"]}},{\"script\":{\"script\":{\"source\":\"doc['Data.auditDetails.lastModifiedTime'].date.millis - doc['Data.auditDetails.createdTime'].date.millis < params.threshold\",\"lang\":\"painless\",\"params\":{\"threshold\":172800000}}}}]}},\"aggs\":{\"count\":{\"terms\":{\"field\":\"Data.tenantId.keyword\"},\"aggs\":{\"tenant_count\":{\"value_count\":{\"field\":\"Data.tenantId.keyword\"}}}}}},\"Total Applications\":{\"terms\":{\"field\":\"Data.tenantId.keyword\"},\"aggs\":{\"tenant_count\":{\"value_count\":{\"field\":\"Data.tenantId.keyword\"}}}}}}}}",
        "requestQueryMap": "{\"wardId\" : \"Data.ward.name.keyword\",\"tenantId\" : \"Data.tenantId.keyword\" \r\n}",
        "dateRefField": "Data.history.auditDetails.createdTime"
      }
    ],
    "translateTenantCode": false,
    "chartType": "metric",
    "valueType": "percentage",
    "action": "percentage",
    "drillChart": "none",
    "aggregationPaths": [
      "Closed With In Sla",
      "Total Applications"
    ],
    "isRoundOff": true,
    "insight": {
      "chartResponseMap" : "wsSLACompliance",
      "action" : "differenceOfNumbers",
      "upwardIndicator" : "positive",
      "downwardIndicator" : "negative",
      "textMessage" : "$indicator$value% than last $insightInterval",
      "colorCode" : "#228B22",
      "insightInterval" : "year",
      "isRoundOff": true
      },
      "_comment": "WS SLA Compliance"
    },
    
  "wsActiveMeteredWaterConnection": {
    "chartName": "DSS_WS_ACTIVE_METERED_WATER_CONNECTIONS",
    "queries": [
      {
        "module": "WS",
        "indexName": "water-services",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.applicationStatus.keyword\":\"REJECTED\"}}],\"must\":[{\"terms\":{\"Data.applicationStatus.keyword\":[\"CONNECTION_ACTIVATED\"]}},{\"terms\":{\"Data.connectionType.keyword\":[\"Metered\"]}}]}},\"aggs\":{\"Active Metered Water Connections\":{\"value_count\":{\"field\":\"Data.id.keyword\"}}}}}}",
        "requestQueryMap": "{\"tenantId\" : \"Data.tenantId.keyword\", \"wardId\" : \"Data.ward.name.keyword\"}",
        "dateRefField": "Data.connectionExecutionDate"
      }
    ],
    "translateTenantCode": false,
    "chartType": "metric",
    "valueType": "number",
    "action": "",
    "drillChart": "none",
    "aggregationPaths": [
      "Active Metered Water Connections"
    ],
    "insight": {
      "chartResponseMap" : "wsActiveMeteredWaterConnection",
      "action" : "differenceOfNumbers",
      "upwardIndicator" : "positive",
      "downwardIndicator" : "negative",
      "textMessage" : "$indicator$value% than last $insightInterval",
      "colorCode" : "#228B22",
      "insightInterval" : "year",
      "isRoundOff": true
    },
    "_comment": "active metered water connections"
  },

  "wsActiveNonMeteredWaterConnection": {
    "chartName": "DSS_WS_ACTIVE_NON_METERED_WATER_CONNECTIONS",
    "queries": [
      {
        "module": "WS",
        "indexName": "water-services",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.applicationStatus.keyword\":\"REJECTED\"}}],\"must\":[{\"terms\":{\"Data.applicationStatus.keyword\":[\"CONNECTION_ACTIVATED\"]}},{\"terms\":{\"Data.connectionType.keyword\":[\"Non Metered\"]}}]}},\"aggs\":{\"Active Non-Metered Water Connections\":{\"value_count\":{\"field\":\"Data.id.keyword\"}}}}}}",
        "requestQueryMap": "{\"tenantId\" : \"Data.tenantId.keyword\", \"wardId\" : \"Data.ward.name.keyword\"}",
        "dateRefField": "Data.connectionExecutionDate"
      }
    ],
    "translateTenantCode": false,
    "chartType": "metric",
    "valueType": "number",
    "action": "",
    "drillChart": "none",
    "aggregationPaths": [
      "Active Non-Metered Water Connections"
    ],
    "insight": {
      "chartResponseMap" : "wsActiveNonMeteredWaterConnection",
      "action" : "differenceOfNumbers",
      "upwardIndicator" : "positive",
      "downwardIndicator" : "negative",
      "textMessage" : "$indicator$value% than last $insightInterval",
      "colorCode" : "#228B22",
      "insightInterval" : "year",
      "isRoundOff": true
    },
    "_comment": "active non-metered water connections"
  },
  "wsActiveSewerageConnection": {
    "chartName": "DSS_WS_ACTIVE_SEWERAGE_CONNECTIONS",
    "queries": [
      {
        "module": "WS",
        "indexName": "sewerage-services",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.applicationStatus.keyword\":\"REJECTED\"}}],\"must\":[{\"terms\":{\"Data.applicationStatus.keyword\":[\"CONNECTION_ACTIVATED\"]}}]}},\"aggs\":{\"Active Sewerage Connections\":{\"value_count\":{\"field\":\"Data.id.keyword\"}}}}}}",
        "requestQueryMap": "{\"tenantId\" : \"Data.tenantId.keyword\", \"wardId\" : \"Data.ward.name.keyword\"}",
        "dateRefField": "Data.connectionExecutionDate"
      }
    ],
    "translateTenantCode": false,
    "chartType": "metric",
    "valueType": "number",
    "action": "",
    "drillChart": "none",
    "aggregationPaths": [
      "Active Sewerage Connections"
    ],
    "insight": {
      "chartResponseMap" : "wsActiveSewerageConnection",
      "action" : "differenceOfNumbers",
      "upwardIndicator" : "positive",
      "downwardIndicator" : "negative",
      "textMessage" : "$indicator$value% than last $insightInterval",
      "colorCode" : "#228B22",
      "insightInterval" : "year",
      "isRoundOff": true
    },
    "_comment": "active sewerage connections "
  },

  "wscumulativeCollectionsv2": {
    "chartName": "DSS_W&S_CUMULATIVE_COLLECTION",
    "queries": [
      {
        "module": "W&S",
        "dateRefField": "dataObject.paymentDetails.receiptDate",
        "requestQueryMap": "{\"tenantId\" : \"Data.tenantId.keyword\", \"wardId\" : \"domainObject.ward.name.keyword\"}",
        "indexName": "dss-collection_v2",
        "aggrQuery": "{\"aggs\":{\"Water Collections\":{\"date_histogram\":{\"field\":\"dataObject.paymentDetails.receiptDate\",\"interval\":\"intervalvalue\"},\"aggs\":{\"Water\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"dataObject.tenantId.keyword\":\"pb.testing\"}},{\"terms\":{\"dataObject.paymentStatus.keyword\":[\"Cancelled\"]}}],\"must\":[{\"terms\":{\"dataObject.paymentStatus.keyword\":[\"DEPOSITED\",\"NEW\"]}},{\"terms\":{\"dataObject.paymentDetails.businessService.keyword\":[\"WS\",\"WS.ONE_TIME_FEE\"]}}]}},\"aggs\":{\"Count\":{\"sum\":{\"field\":\"dataObject.paymentDetails.bill.billDetails.amountPaid\"}}}}}},\"Sewerage Collections\":{\"date_histogram\":{\"field\":\"dataObject.paymentDetails.receiptDate\",\"interval\":\"intervalvalue\"},\"aggs\":{\"Sewerage\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"dataObject.tenantId.keyword\":\"pb.testing\"}},{\"terms\":{\"dataObject.paymentStatus.keyword\":[\"Cancelled\"]}}],\"must\":[{\"terms\":{\"dataObject.paymentStatus.keyword\":[\"DEPOSITED\",\"NEW\"]}},{\"terms\":{\"dataObject.paymentDetails.businessService.keyword\":[\"SW.ONE_TIME_FEE\"]}}]}},\"aggs\":{\"Count\":{\"sum\":{\"field\":\"dataObject.paymentDetails.bill.billDetails.amountPaid\"}}}}}}}}"
      }
    ],
    "translateTenantCode": false,
    "chartType": "line",
    "valueType": "amount",
    "action": "",
    "drillChart": "none",
    "documentType": "_doc",
    "aggregationPaths": [
      "Water Collections",
      "Sewerage Collections"
    ],
    "isCumulative": true,
    "interval": "month",
    "insight": {
    },
    "_comment": " "
  },
  
  "wscumulativeConnections": {
    "chartName": "DSS_W&S_CUMULATIVE_CONNECTION",
    "queries": [
      {
        "module": "W&S",
        "dateRefField": "Data.connectionExecutionDate",
        "requestQueryMap": "{\"tenantId\" : \"Data.tenantId.keyword\", \"wardId\" : \"Data.ward.name.keyword\"}",
        "indexName": "water-services",
        "aggrQuery": "{\"aggs\":{\"Water Connections\":{\"date_histogram\":{\"field\":\"Data.connectionExecutionDate\",\"interval\":\"intervalvalue\"},\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.applicationStatus.keyword\":\"REJECTED\"}}],\"must\":[{\"terms\":{\"Data.applicationStatus.keyword\":[\"CONNECTION_ACTIVATED\"]}}]}},\"aggs\":{\"Total Connections\":{\"value_count\":{\"field\":\"Data.id.keyword\"}}}}}}}}"
      },
      {
        "module": "W&S",
        "dateRefField": "Data.connectionExecutionDate",
        "requestQueryMap": "{\"tenantId\" : \"Data.tenantId.keyword\", \"wardId\" : \"Data.ward.name.keyword\"}",
        "indexName": "sewerage-services",
        "aggrQuery": "{\"aggs\":{\"Sewerage Connections\":{\"date_histogram\":{\"field\":\"Data.connectionExecutionDate\",\"interval\":\"intervalvalue\"},\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.applicationStatus.keyword\":\"REJECTED\"}}],\"must\":[{\"terms\":{\"Data.applicationStatus.keyword\":[\"CONNECTION_ACTIVATED\"]}}]}},\"aggs\":{\"Total Connections\":{\"value_count\":{\"field\":\"Data.id.keyword\"}}}}}}}}"
      }
    ],
    "translateTenantCode": false,
    "chartType": "line",
    "valueType": "number",
    "action": "",
    "drillChart": "none",
    "documentType": "_doc",
    "aggregationPaths": [
      "Water Connections",
      "Sewerage Connections"
    ],
    "isCumulative": true,
    "interval": "month",
    "insight": {
    },
    "_comment": " "
  },

  "wsWaterConsumersByUsageType": {
    "chartName": "DSS_W&S_WATER_CONNECTION_BY_USAGE",
    "queries": [
      {
        "module": "W&S",
        "indexName": "water-services",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.applicationStatus.keyword\":\"REJECTED\"}}],\"must\":[{\"terms\":{\"Data.applicationStatus.keyword\":[\"CONNECTION_ACTIVATED\"]}}]}},\"aggs\":{\"Water Consumers by Usage Type\":{\"terms\":{\"field\":\"Data.propertyUsageType.keyword\"},\"aggs\":{\"Total Connection\":{\"value_count\":{\"field\":\"Data.id.keyword\"}}}}}}}}",
        "requestQueryMap": "{\"tenantId\" : \"Data.tenantId.keyword\", \"wardId\" : \"Data.ward.name.keyword\"}",
        "dateRefField": "Data.connectionExecutionDate"
      }
    ],
    "translateTenantCode": false,
    "chartType": "pie",
    "valueType": "number",
    "action": "",
    "documentType": "_doc",
    "drillChart": "none",
    "aggregationPaths": [
      "Water Consumers by Usage Type"
    ],
    "insight": {
    },
    "_comment": " "
  },

  "wsSewerageConsumersByUsageType": {
    "chartName": "DSS_W&S_SEWERAGE_CONNECTION_BY_USAGE",
    "queries": [
      {
        "module": "W&S",
        "indexName": "sewerage-services",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.applicationStatus.keyword\":\"REJECTED\"}}],\"must\":[{\"terms\":{\"Data.applicationStatus.keyword\":[\"CONNECTION_ACTIVATED\"]}}]}},\"aggs\":{\"Sewerage Consumers by Usage Type\":{\"terms\":{\"field\":\"Data.propertyUsageType.keyword\"},\"aggs\":{\"Total Connection\":{\"value_count\":{\"field\":\"Data.id.keyword\"}}}}}}}}",
        "requestQueryMap": "{\"tenantId\" : \"Data.tenantId.keyword\", \"wardId\" : \"Data.ward.name.keyword\"}",
        "dateRefField": "Data.connectionExecutionDate"
      }
    ],
    "translateTenantCode": false,
    "chartType": "pie",
    "valueType": "number",
    "action": "",
    "documentType": "_doc",
    "drillChart": "none",
    "aggregationPaths": [
      "Sewerage Consumers by Usage Type"
    ],
    "insight": {
    },
    "_comment": " "
  },

  "wsConsumersByChannel": {
    "chartName": "DSS_W&S_CONNECTION_BY_CHANNEL",
    "queries": [
      {
        "module": "W&S",
        "indexName": "water-services",
        "requestQueryMap": "{\"tenantId\" : \"Data.tenantId.keyword\", \"wardId\" : \"Data.ward.name.keyword\"}",
        "dateRefField": "Data.connectionExecutionDate",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.applicationStatus.keyword\":\"REJECTED\"}}],\"must\":[{\"terms\":{\"Data.applicationStatus.keyword\":[\"CONNECTION_ACTIVATED\"]}}]}},\"aggs\":{\"W & S Consumers by Channel\":{\"terms\":{\"field\":\"Data.channel.keyword\"},\"aggs\":{\"Total Connection\":{\"value_count\":{\"field\":\"Data.id.keyword\"}}}}}}}}"
      },
      {
        "module": "W&S",
        "indexName": "sewerage-services",
        "requestQueryMap": "{\"tenantId\" : \"Data.tenantId.keyword\", \"wardId\" : \"Data.ward.name.keyword\"}",
        "dateRefField": "Data.connectionExecutionDate",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.applicationStatus.keyword\":\"REJECTED\"}}],\"must\":[{\"terms\":{\"Data.applicationStatus.keyword\":[\"CONNECTION_ACTIVATED\"]}}]}},\"aggs\":{\"W & S Consumers by Channel\":{\"terms\":{\"field\":\"Data.channel.keyword\"},\"aggs\":{\"Total Connection\":{\"value_count\":{\"field\":\"Data.id.keyword\"}}}}}}}}"
      }
    ],
    "translateTenantCode": false,
    "chartType": "pie",
    "valueType": "number",
    "action": "",
    "documentType": "_doc",
    "drillChart": "none",
    "aggregationPaths": [
      "W & S Consumers by Channel"
    ],
    "insight": {
    },
    "_comment": " "
  },

  "wsConnectionAgeingDDR": {
    "chartName": "DSS_W&S_CONNECTION_AGEING",
    "queries": [
      {
        "module": "W&S",
        "requestQueryMap": "{\"tenantId\" : \"Data.tenantId.keyword\", \"wardId\" : \"Data.ward.name.keyword\" }",
        "dateRefField": "Data.@timestamp",
        "indexName": "water-services",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.tenantId.keyword\":\"pb.testing\"}},{\"terms\":{\"Data.applicationStatus.keyword\":[\"REJECTED\",\"CONNECTION_ACTIVATED\"]}}]}},\"aggs\":{\"Pending_from_0_to_3_days\":{\"date_range\":{\"field\":\"Data.@timestamp\",\"ranges\":[{\"from\":\"now-3d\/d\",\"to\":\"now\"}],\"format\":\"dd-MM-yyyy\"}},\"Pending_from_3_to_7_days\":{\"date_range\":{\"field\":\"Data.@timestamp\",\"ranges\":[{\"from\":\"now-7d\/d\",\"to\":\"now-3d\"}],\"format\":\"dd-MM-yyyy\"}},\"Pending_from_7_to_15_days\":{\"date_range\":{\"field\":\"Data.@timestamp\",\"ranges\":[{\"from\":\"now-15d\",\"to\":\"now-7d\"}],\"format\":\"dd-MM-yyyy\"}},\"Pending_from_more_than_15_days\":{\"date_range\":{\"field\":\"Data.@timestamp\",\"ranges\":[{\"from\":\"now-2y\",\"to\":\"now-15d\"}],\"format\":\"dd-MM-yyyy\"}}}}}}"
      },
      {
        "module": "W&S",
        "requestQueryMap": "{\"tenantId\" : \"Data.tenantId.keyword\", \"wardId\" : \"Data.ward.name.keyword\" }",
        "dateRefField": "Data.@timestamp",
        "indexName": "sewerage-services",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.tenantId.keyword\":\"pb.testing\"}},{\"terms\":{\"Data.applicationStatus.keyword\":[\"REJECTED\",\"CONNECTION_ACTIVATED\"]}}]}},\"aggs\":{\"Pending_from_0_to_3_days\":{\"date_range\":{\"field\":\"Data.@timestamp\",\"ranges\":[{\"from\":\"now-3d\/d\",\"to\":\"now\"}],\"format\":\"dd-MM-yyyy\"}},\"Pending_from_3_to_7_days\":{\"date_range\":{\"field\":\"Data.@timestamp\",\"ranges\":[{\"from\":\"now-7d\/d\",\"to\":\"now-3d\"}],\"format\":\"dd-MM-yyyy\"}},\"Pending_from_7_to_15_days\":{\"date_range\":{\"field\":\"Data.@timestamp\",\"ranges\":[{\"from\":\"now-15d\",\"to\":\"now-7d\"}],\"format\":\"dd-MM-yyyy\"}},\"Pending_from_more_than_15_days\":{\"date_range\":{\"field\":\"Data.@timestamp\",\"ranges\":[{\"from\":\"now-2y\",\"to\":\"now-15d\"}],\"format\":\"dd-MM-yyyy\"}}}}}}"

      }
    ],
    "isMdmsEnabled": true,
    "filterKeys": [
      {"key": "tenantId", "column": "DDRs"}
    ],
    "chartType": "xtable",
    "valueType": "number",
    "drillChart": "wsConnectionAgeingUlb",
    "action": "",
    "plotLabel": "DDRs",
    "isPostResponseHandler": true,
    "aggregationPaths": [
      "Pending_from_0_to_3_days",
      "Pending_from_3_to_7_days",
      "Pending_from_7_to_15_days",
      "Pending_from_more_than_15_days"
    ],
    "computedFields": [
      {
        "postAggregationTheory" : "",
        "actionName": "AdditiveComputedField",
        "fields" : [ "Pending_from_0_to_3_days","Pending_from_3_to_7_days","Pending_from_7_to_15_days","Pending_from_more_than_15_days"],
        "newField" : "Total_Pending_Applications",
        "_comments": "fields are field names picked from its aggregation query to use post aggregation newField value with given new field name  "
      }
    ],

    "insight": {
    },
    "_comment": ""
  },
  "wsConnectionAgeingUlb": {
    "chartName": "DSS_W&S_CONNECTION_AGEING",
    "queries": [
      {
        "module": "W&S",
        "requestQueryMap": "{\"tenantId\" : \"Data.tenantId.keyword\", \"wardId\" : \"Data.ward.name.keyword\" }",
        "dateRefField": "Data.@timestamp",
        "indexName": "water-services",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.tenantId.keyword\":\"pb.testing\"}},{\"terms\":{\"Data.applicationStatus.keyword\":[\"REJECTED\",\"CONNECTION_ACTIVATED\"]}}]}},\"aggs\":{\"ULB\":{\"terms\":{\"field\":\"Data.tenantId.keyword\",\"size\":170},\"aggs\":{\"Pending_from_0_to_3_days\":{\"date_range\":{\"field\":\"Data.@timestamp\",\"ranges\":[{\"from\":\"now-3d\/d\",\"to\":\"now\"}]}},\"Pending_from_3_to_7_days\":{\"date_range\":{\"field\":\"Data.@timestamp\",\"ranges\":[{\"from\":\"now-1w\",\"to\":\"now-3d\/d\"}]}},\"Pending_from_7_to_15_days\":{\"date_range\":{\"field\":\"Data.@timestamp\",\"ranges\":[{\"from\":\"now-15d\",\"to\":\"now-1w\"}]}},\"Pending_from_more_than_15_days\":{\"date_range\":{\"field\":\"Data.@timestamp\",\"ranges\":[{\"from\":\"now-2y\",\"to\":\"now-15d\"}]}}}}}}}}"
      },
      {
        "module": "W&S",
        "requestQueryMap": "{\"tenantId\" : \"Data.tenantId.keyword\", \"wardId\" : \"Data.ward.name.keyword\" }",
        "dateRefField": "Data.@timestamp",
        "indexName": "sewerage-services",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.tenantId.keyword\":\"pb.testing\"}},{\"terms\":{\"Data.applicationStatus.keyword\":[\"REJECTED\",\"CONNECTION_ACTIVATED\"]}}]}},\"aggs\":{\"ULB\":{\"terms\":{\"field\":\"Data.tenantId.keyword\",\"size\":170},\"aggs\":{\"Pending_from_0_to_3_days\":{\"date_range\":{\"field\":\"Data.@timestamp\",\"ranges\":[{\"from\":\"now-3d\/d\",\"to\":\"now\"}]}},\"Pending_from_3_to_7_days\":{\"date_range\":{\"field\":\"Data.@timestamp\",\"ranges\":[{\"from\":\"now-1w\",\"to\":\"now-3d\/d\"}]}},\"Pending_from_7_to_15_days\":{\"date_range\":{\"field\":\"Data.@timestamp\",\"ranges\":[{\"from\":\"now-15d\",\"to\":\"now-1w\"}]}},\"Pending_from_more_than_15_days\":{\"date_range\":{\"field\":\"Data.@timestamp\",\"ranges\":[{\"from\":\"now-2y\",\"to\":\"now-15d\"}]}}}}}}}}"
      }
    ],
    "isMdmsEnabled": false,
    "filterKeys": [
      {"key": "tenantId", "column": "ULB"}
    ],
    "chartType": "xtable",
    "valueType": "number",
    "drillChart": "wsConnectionAgeingWard",
    "action": "",
    "plotLabel": "ULB",
    "isPostResponseHandler": true,
    "postAggregationTheory" : "",
    "aggregationPaths": [
      "Pending_from_0_to_3_days",
      "Pending_from_3_to_7_days",
      "Pending_from_7_to_15_days",
      "Pending_from_more_than_15_days"
    ],
    "computedFields": [
      {
        "postAggregationTheory" : "",
        "actionName": "AdditiveComputedField",
        "fields" : [ "Pending_from_0_to_3_days","Pending_from_3_to_7_days","Pending_from_7_to_15_days","Pending_from_more_than_15_days"],
        "newField" : "Total_Pending_Applications",
        "_comments": "fields are field names picked from its aggregation query to use post aggregation newField value with given new field name  "
      }
    ],

    "insight": {
    },
    "_comment": ""
  },
  "wsConnectionAgeingWard": {
    "chartName": "",
    "queries": [
      {
        "module": "W&S",
        "requestQueryMap": "{\"tenantId\" : \"Data.tenantId.keyword\", \"wardId\" : \"Data.ward.name.keyword\" }",
        "dateRefField": "Data.@timestamp",
        "indexName": "water-services",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.tenantId.keyword\":\"pb.testing\"}},{\"terms\":{\"Data.applicationStatus.keyword\":[\"REJECTED\",\"CONNECTION_ACTIVATED\"]}}]}},\"aggs\":{\"Ward\":{\"terms\":{\"field\":\"Data.ward.name.keyword\",\"size\":170},\"aggs\":{\"Pending_from_0_to_3_days\":{\"date_range\":{\"field\":\"Data.@timestamp\",\"ranges\":[{\"from\":\"now-3d\/d\",\"to\":\"now\"}]}},\"Pending_from_3_to_7_days\":{\"date_range\":{\"field\":\"Data.@timestamp\",\"ranges\":[{\"from\":\"now-1w\",\"to\":\"now-3d\/d\"}]}},\"Pending_from_7_to_15_days\":{\"date_range\":{\"field\":\"Data.@timestamp\",\"ranges\":[{\"from\":\"now-15d\",\"to\":\"now-1w\"}]}},\"Pending_from_more_than_15_days\":{\"date_range\":{\"field\":\"Data.@timestamp\",\"ranges\":[{\"from\":\"now-2y\",\"to\":\"now-15d\"}]}}}}}}}}"
      },
      {
        "module": "W&S",
        "requestQueryMap": "{\"tenantId\" : \"Data.tenantId.keyword\", \"wardId\" : \"Data.ward.name.keyword\" }",
        "dateRefField": "Data.@timestamp",
        "indexName": "sewerage-services",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.tenantId.keyword\":\"pb.testing\"}},{\"terms\":{\"Data.applicationStatus.keyword\":[\"REJECTED\",\"CONNECTION_ACTIVATED\"]}}]}},\"aggs\":{\"Ward\":{\"terms\":{\"field\":\"Data.ward.name.keyword\",\"size\":170},\"aggs\":{\"Pending_from_0_to_3_days\":{\"date_range\":{\"field\":\"Data.@timestamp\",\"ranges\":[{\"from\":\"now-3d\/d\",\"to\":\"now\"}]}},\"Pending_from_3_to_7_days\":{\"date_range\":{\"field\":\"Data.@timestamp\",\"ranges\":[{\"from\":\"now-1w\",\"to\":\"now-3d\/d\"}]}},\"Pending_from_7_to_15_days\":{\"date_range\":{\"field\":\"Data.@timestamp\",\"ranges\":[{\"from\":\"now-15d\",\"to\":\"now-1w\"}]}},\"Pending_from_more_than_15_days\":{\"date_range\":{\"field\":\"Data.@timestamp\",\"ranges\":[{\"from\":\"now-2y\",\"to\":\"now-15d\"}]}}}}}}}}"
      }
    ],
    "isMdmsEnabled": false,
    "filterKeys": [
    ],
    "chartType": "xtable",
    "valueType": "number",
    "drillChart": "none",
    "action": "",
    "plotLabel": "Ward",
    "isPostResponseHandler": true,
    "postAggregationTheory" : "",
    "aggregationPaths": [
      "Pending_from_0_to_3_days",
      "Pending_from_3_to_7_days",
      "Pending_from_7_to_15_days",
      "Pending_from_more_than_15_days"
    ],
    "computedFields": [
      {
        "postAggregationTheory" : "",
        "actionName": "AdditiveComputedField",
        "fields" : [ "Pending_from_0_to_3_days","Pending_from_3_to_7_days","Pending_from_7_to_15_days","Pending_from_more_than_15_days"],
        "newField" : "Total_Pending_Applications",
        "_comments": "fields are field names picked from its aggregation query to use post aggregation newField value with given new field name  "
      }
    ],

    "insight": {
    },
    "_comment": ""
  }
```

&#x20;[Click here to check the complete configuration](https://github.com/egovernments/configs/blob/qa/egov-dss-dashboards/dashboard-analytics/ChartApiConfig.json)

### **Master Dashboard Configuration**

Master dashboard configuration is the main configuration which defines the dashboards to be painted on the screen.&#x20;

It includes all the visualizations, their groups, the charts which come within them and even their dimensions as what should be their height and width.

```
{
      "name": "DSS_W&S_DASHBOARD",
      "id": "ws",
      "isActive": "",
      "style": "linear",
      "visualizations": [
        {
          "row": 1,
          "name": "DSS_REVENUE",
          "vizArray": [
            {
              "id": 211,
              "name": "DSS_STATE_WS_OVERVIEW",
              "dimensions": {
                "height": 350,
                "width": 5
              },
              "vizType": "metric-collection",
              "noUnit": true,
              "isCollapsible": false,
              "label": "DSS_OVERVIEW",
              "charts": [
                {
                  "id": "wstodaysCollection",
                  "name": "DSS_W&S_TODAYS_COLLECTION",
                  "code": "",
                  "chartType": "metric",
                  "filter": {"title": "TODAY"},
                  "headers": []
                },
                {
                  "id": "wstotalCollection",
                  "name": "DSS_W&S_TOTAL_COLLECTION",
                  "code": "",
                  "chartType": "metric",
                  "filter": "",
                  "headers": []
                },
                {
                  "id": "wstargetCollection",
                  "name": "DSS_W&S_TARGET_COLLECTION",
                  "code": "",
                  "chartType": "metric",
                  "filter": "",
                  "headers": []
                },
                {
                  "id": "wstargetAchieved",
                  "name": "DSS_W&S_TARGET_ACHIEVED",
                  "code": "",
                  "chartType": "metric",
                  "filter": "",
                  "headers": []
                }
              ]
            },
            {
              "id": 212,
              "name": "DSS_W&S_TOTAL_CUMULATIVE_COLLECTION",
              "dimensions": {
                "height": 350,
                "width": 7
              },
              "vizType": "chart",
              "noUnit": true,
              "isCollapsible": false,
              "charts": [
                {
                  "id": "wscumulativeCollections",
                  "name": "Monthly",
                  "code": "",
                  "chartType": "line",
                  "filter": "",
                  "headers": []
                }
              ]
            }
          ]
        },
        {
          "row": 2,
          "name": "DSS_REVENUE",
          "vizArray": [
            {
              "id": 221,
              "name": "DSS_W&S_TOP_3_PERFORMING_ULBS",
              "dimensions": {
                "height": 250,
                "width": 4
              },
              "vizType": "performing-metric",
              "noUnit": false,
              "isCollapsible": false,
              "label": "",
              "charts": [
                {
                  "id": "wstopPerformingUlbs",
                  "name": "DSS_W&S_TOP_3_PERFORMING_ULBS",
                  "code": "",
                  "chartType": "bar",
                  "filter": "",
                  "headers": []
                }
              ]
            },
            {
              "id": 222,
              "name": "DSS_W&S_BOTTOM_3_PERFORMING_ULBS",
              "dimensions": {
                "height": 250,
                "width": 4
              },
              "vizType": "performing-metric",
              "noUnit": false,
              "isCollapsible": false,
              "charts": [
                {
                  "id": "wsbottomPerformingUlbs",
                  "name": "DSS_W&S_BOTTOM_3_PERFORMING_ULBS",
                  "code": "",
                  "chartType": "bar",
                  "filter": "",
                  "headers": []
                }
              ]
            }
          ]
        },
        {
          "row": 3,
          "name": "DSS_REVENUE",
          "vizArray": [
            {
              "id": 223,
              "name": "DSS_W&S_COLLECTION_BY_USAGE",
              "dimensions": {
                "height": 250,
                "width": 4
              },
              "vizType": "chart",
              "noUnit": true,
              "isCollapsible": false,
              "charts": [
                {
                  "id": "wscollectionByUsage",
                  "name": "DSS_W&S_COLLECTION_BY_USAGE",
                  "code": "",
                  "chartType": "donut",
                  "filter": "",
                  "headers": []
                }
              ]
            },
            {
              "id": 224,
              "name": "DSS_W&S_COLLECTION_BY_CHANNEL",
              "dimensions": {
                "height": 250,
                "width": 4
              },
              "vizType": "chart",
              "noUnit": true,
              "isCollapsible": false,
              "charts": [
                {
                  "id": "wscollectionByChannel",
                  "name": "DSS_W&S_COLLECTION_BY_CHANNEL",
                  "code": "",
                  "chartType": "donut",
                  "filter": "",
                  "headers": []
                }
              ]
            }
          ]
        },
        {
          "row": 4,
          "name": "DSS_REVENUE",
          "vizArray": [
            {
              "id": 231,
              "name": "DSS_WS_KEY_FY_INDICATORS",
              "dimensions": {
                "height": 350,
                "width": 12
              },
              "vizType": "chart",
              "noUnit": false,
              "isCollapsible": false,
              "charts": [
                {
                  "id": "wsFinancialIndicatorDDR",
                  "name": "DSS_W&S_DEMAND_COLLECTION_BOUNDARY",
                  "code": "",
                  "chartType": "table",
                  "filter": "",
                  "headers": [],
                  "tabName": "Boundary"
                }
              ]
            }
          ]
        },
        {
          "row": 5,
          "name": "DSS_REVENUE",
          "vizArray": [
            {
              "id": 231,
              "name": "DSS_W&S_TAX_HEAD_BOUNDARY",
              "dimensions": {
                "height": 350,
                "width": 12
              },
              "vizType": "chart",
              "label": "",
              "noUnit": false,
              "isCollapsible": true,
              "charts": [
                {
                  "id": "wsTaxHeadDDR",
                  "name": "DSS_W&S_TAX_HEAD_BOUNDARY",
                  "code": "",
                  "chartType": "table",
                  "filter": "",
                  "headers": [],
                  "tabName": "Boundary"
                }
              ]
            }
          ]
        },
        {
          "row": 7,
          "name": "DSS_SERVICE",
          "vizArray": [
            {
              "id": 231,
              "name": "DSS_STATE_WS_OVERVIEW",
              "dimensions": {
                "height": 350,
                "width": 12
              },
              "vizType": "metric-collection",
              "label": "",
              "noUnit": false,
              "isCollapsible": true,
              "charts": [
                {
                  "id": "wstotalApplications",
                  "name": "DSS_WS_TOTAL_APPLICATIONS",
                  "code": "",
                  "chartType": "metric",
                  "filter": "",
                  "headers": []
                },
                {
                  "id": "wsSLACompliance",
                  "name": "DSS_WS_SLA_COMPLIANCE",
                  "code": "",
                  "chartType": "metric",
                  "filter": "",
                  "headers": []
                },
                {
                  "id": "wstotalConnection",
                  "name": "DSS_WS_ACTIVE_CONNECTIONS",
                  "code": "",
                  "chartType": "metric",
                  "filter": "",
                  "headers": []
                },
                {
                  "id": "wsActiveMeteredWaterConnection",
                  "name": "DSS_WS_ACTIVE_METERED_WATER_CONNECTIONS",
                  "code": "",
                  "chartType": "metric",
                  "filter": "",
                  "headers": []
                },
                {
                  "id": "wsActiveNonMeteredWaterConnection",
                  "name": "DSS_WS_ACTIVE_NON_METERED_WATER_CONNECTIONS",
                  "code": "",
                  "chartType": "metric",
                  "filter": "",
                  "headers": []
                },
                {
                  "id": "wsActiveSewerageConnection",
                  "name": "DSS_WS_ACTIVE_SEWERAGE_CONNECTIONS",
                  "code": "",
                  "chartType": "metric",
                  "filter": "",
                  "headers": []
                }
              ]
            },
            {
              "id": 232,
              "name": "DSS_W&S_CUMULATIVE_CONNECTION",
              "dimensions": {
                "height": 350,
                "width": 7
              },
              "vizType": "chart",
              "isCollapsible": false,
              "charts": [
                {
                  "id": "wscumulativeConnections",
                  "name": "Monthly",
                  "code": "",
                  "chartType": "line",
                  "filter": "",
                  "headers": []
                }
              ]
            }
          ]
        },
        {
          "row": 8,
          "name": "DSS_SERVICE",
          "vizArray": [
            {
              "id": 231,
              "name": "DSS_W&S_WATER_CONNECTION_BY_USAGE",
              "dimensions": {
                "height": 350,
                "width": 12
              },
              "vizType": "chart",
              "label": "",
              "noUnit": false,
              "isCollapsible": true,
              "charts": [
                {
                  "id": "wsWaterConsumersByUsageType",
                  "name": "",
                  "code": "",
                  "chartType": "donut",
                  "filter": "",
                  "headers": []
                }
              ]
            },
            {
              "id": 232,
              "name": "DSS_W&S_SEWERAGE_CONNECTION_BY_USAGE",
              "dimensions": {
                "height": 350,
                "width": 12
              },
              "vizType": "chart",
              "label": "",
              "noUnit": false,
              "isCollapsible": true,
              "charts": [
                {
                  "id": "wsSewerageConsumersByUsageType",
                  "name": "",
                  "code": "",
                  "chartType": "donut",
                  "filter": "",
                  "headers": []
                }
              ]
            },
            {
              "id": 233,
              "name": "DSS_W&S_CONNECTION_BY_CHANNEL",
              "dimensions": {
                "height": 350,
                "width": 12
              },
              "vizType": "chart",
              "label": "",
              "noUnit": false,
              "isCollapsible": true,
              "charts": [
                {
                  "id": "wsConsumersByChannel",
                  "name": "",
                  "code": "",
                  "chartType": "donut",
                  "filter": "",
                  "headers": []
                }
              ]
            }
          ]
        },
        {
          "row": 9,
          "name": "DSS_SERVICE",
          "vizArray": [
            {
              "id": 231,
              "name": "DSS_W&S_CONNECTION_AGEING",
              "dimensions": {
                "height": 350,
                "width": 12
              },
              "vizType": "chart",
              "label": "",
              "noUnit": false,
              "isCollapsible": true,
              "charts": [
                {
                  "id": "wsConnectionAgeingDDR",
                  "name": "DSS_W&S_CONNECTION_AGEING",
                  "code": "",
                  "chartType": "table",
                  "filter": "",
                  "headers": [],
                  "tabName": "Boundary"
                }
              ]
            }

          ]
        }
      ]
    }
```

[Click here for the complete configuration](https://github.com/egovernments/configs/blob/qa/egov-dss-dashboards/dashboard-analytics/MasterDashboardConfig.json)

### **Role Dashboard Mappings Configuration**

Master Dashboard Configuration which was explained earlier contains the list of dashboards which are available. Given the instance where Role Action Mapping is not maintained in the Application Service, this configuration will act as Role - Dashboard Mapping Configuration.

In this, each role is mapped against the Dashboard which they are authorised to see. This was used earlier when the Role Action Mapping of eGov was not integrated.

Later, when the Role Action Mapping started controlling the dashboards to be seen on the client side, this configuration was just used to enable the dashboards for viewing.&#x20;

```
{
  "_comment": "Holds mapping for each role with and its associated dashboards",
  "roles" : [
    {
      "_comment":"This role is super role which can access all the available dashboards: [other/new roles are suppose to be added]",
      "roleId": 6,
      "roleName" : "Admin",
      "isSuper" : "",
      "orgId": "",
      "dashboards": [
        {
          "name": "Water & Sewerage",
          "id": "ws"
        }
      ]
    },
    {
      "_comment":"This role is super role which can access all the available dashboards: [other/new roles are suppose to be added]",
      "roleId": 7,
      "roleName" : "Commissioner",
      "isSuper" : "",
      "orgId": "",
      "dashboards": [
        {
          "id": "ulb-ws"
        }
      ]
    }

  ]
}

```

[Click here to check the configuration](https://github.com/egovernments/configs/blob/qa/egov-dss-dashboards/dashboard-analytics/RoleDashboardMappingsConf.json)

### &#x20;**MDMS Configuration**&#x20;

_common-masters/uiCommonConstants.json_

```
"ws": {
          "routePath": "/dashboard/ws",
          "isOrigin": true
      },
"ulb-ws": {
           "routePath": "/dashboard/ulb-ws",
           "isOrigin": true
          }
```

[Click here to check the complete configuration](https://github.com/egovernments/egov-mdms-data/blob/QA/data/pb/common-masters/uiCommonConstants.json)

roleaction.json&#x20;

```
 {
      "rolecode": "STADMIN",
      "actionid": {{PlaceHolder1}},
      "actioncode": "",
      "tenantId": "pb"
    }
    
    
    {
      "rolecode": "STADMIN",
      "actionid": {{PlaceHolder2}},
      "actioncode": "",
      "tenantId": "pb"
    },
     {
      "rolecode": "EMPLOYEE",
      "actionid": {{PlaceHolder2}},
      "actioncode": "",
      "tenantId": "pb"
    },  
     {
      "rolecode": "UC_EMP",
      "actionid": {{PlaceHolder2}},
      "actioncode": "",
      "tenantId": "pb"
    },

```

[Click here to check the complete configuration](https://github.com/egovernments/egov-mdms-data/blob/QA/data/pb/ACCESSCONTROL-ROLEACTIONS/roleactions.json)

Action test.json

```
{
      "id": {{PlaceHolder1}},
      "name": "Dashboard Water Sewerage",
      "url": "/dashboard-analytics/dashboard/getDashboardConfig/ws",
      "parentModule": "",
      "displayName": "DSS",
      "orderNumber": 0,
      "enabled": false,
      "serviceCode": "DSS",
      "code": "null",
      "path": ""
},
{
      "id": {{PlaceHolder2}},
      "name": "Dashboard Water Sewerage",
      "url": "url",
      "displayName": "Water Sewerage",
      "orderNumber": 11,
      "parentModule": "dss-dashboard",
      "enabled": true,
      "serviceCode": "DSS",
      "code": "null",
      "path": "Dashboard.Ws",
      "navigationURL": "/digit-ui/employee/dss/dashboard/ws",
      "leftIcon": "places:business-center",
      "rightIcon": ""
},
{
      "id": {{PlaceHolder3}},
      "name": "DSS Dashboard Charts",
      "url": "/dashboard-analytics/dashboard/getChartV2",
      "parentModule": "",
      "displayName": "DSS",
      "orderNumber": 0,
      "enabled": false,
      "serviceCode": "DSS",
      "code": "null",
      "path": ""
} 
```

[Click here to check the complete configuration](https://github.com/egovernments/egov-mdms-data/blob/QA/data/pb/ACCESSCONTROL-ACTIONS-TEST/actions-test.json)

## Charts Overview

W\&S-DSS consists of multiple graphs which represent the data of W\&S. Each graph has its own configuration which will describe the chart and its type.

DSS consists of the following charts in W\&S:

**Revenue Tab**

* Overview
* Total Cumulative Collection
* Top ULB By Performance
* Bottom ULB by Performance
* W\&S Collection by Usage Type
* W\&S Collection by Channel Type
* W\&S Key Financial Indicators
* W\&S Tax Heads

**Service Tab**

* Overview
* Total Cumulative Connection
* Water Connection By Usage
* Sewerage Connections By Usage
* Connection By Channel
* W\&S Connection Ageing

### **Revenue Tab** <a href="#revenue-tab" id="revenue-tab"></a>

**Overview**

The overview graph contains multiple data information as below in the selected time period.

* **Today’s Collection:** This represents today’s collection amount for Water and Sewerage Application Fee + Consumption Charges.
* &#x20;**Total Collection:** This represents the total collection amount for Water and Sewerage Application Fee + Consumption Charges.
* **Target Collection:** This represents the target collection amount for the Water and Sewerage connections.
* **Target Achievement:** This represents the target achieved in percentage. This is calculated by the formula- (Total Collection/Target Collection)\*100%

![](<../../../../.gitbook/assets/image (14) (2).png>)&#x20;

#### **Total Cumulative Collection** <a href="#total-cumulative-collection" id="total-cumulative-collection"></a>

This Graph contains the Water and Sewerage collection amount information on a monthly basis as a cumulative line graph for each water and sewerage collection separately. This will change as per the denomination amount filter selection.

**line** - this graph/chart is data representation on date histograms or date groupings.

![](<../../../../.gitbook/assets/image (25).png>)

#### **Top ULB By Performance**  <a href="#top-ulb-by-performance" id="top-ulb-by-performance"></a>

This graph represents the ULBs based on the Target achieved in bar chart representation with the % of target achieved in descending order.

![](<../../../../.gitbook/assets/image (28).png>)

#### **Bottom ULB by Performance** <a href="#bottom-ulb-by-performance" id="bottom-ulb-by-performance"></a>

This graph represents the ULBs based on the target achieved in bar chart representation with the % of target achieved in ascending order.

![](<../../../../.gitbook/assets/image (18).png>)

**W\&S Collection by Usage Type**

This graph shows the collection amount based on the usage/property type and this amount will change as per the denomination filter change.

![](<../../../../.gitbook/assets/image (13).png>)

#### **W\&S Collection by Channel Type** <a href="#w-and-s-collection-by-channel-type" id="w-and-s-collection-by-channel-type"></a>

This graph shows the collection amount based on the collection channel type(eg-online, counter, etc) and this amount will change as per the denomination filter change.

![](<../../../../.gitbook/assets/image (2).png>)

#### **W\&S Key Financial Indicators** <a href="#w-and-s-key-financial-indicators" id="w-and-s-key-financial-indicators"></a>

This tabular chart representation graph shows multiple W\&S information like Target Collection, Total Collection, Total Transactions, Total Connections and Target Achievement (in %). And this table shows the data at the district level and also has the drill-down chart for each district to ulb and from ulb to ward level data for the same.

_**xtable**_ type allows to the addition of multiple computed fields with the aggregated fields dynamically added.

To add multiple computed columns,  **computedFields** \[]  where actionName (IComputedField\<T> interface), fields \[] names as in exist in query key, newField as name to appear for computation must be defined.

![](<../../../../.gitbook/assets/image (15).png>)

On click of any district name will enter into drill-down charts, which will represent that specific District data.

![](<../../../../.gitbook/assets/image (22).png>)

On click of the ULB will navigate to wards under that specific ULB and each ward shows the specific data regarding that ward.

![](<../../../../.gitbook/assets/image (24).png>)

#### **W\&S Tax Heads** <a href="#w-and-s-tax-heads" id="w-and-s-tax-heads"></a>

This tabular chart representation graph shows multiple W\&S information like Total Collection, Penalty, Interest and Target Collection. And this table shows the data at the district level and also has the drill-down chart for each district to ulb and from ulb to ward level data for the same.

_**table**_ type allows to addition of multiple aggregated fields.

&#x20;![](<../../../../.gitbook/assets/image (7).png>)

On click of any district name will enter into drill-down charts, which will represent that specific District data.

![](<../../../../.gitbook/assets/image (20).png>)

On click of the ULB will navigate to wards under that specific ULB and each ward shows the specific data regarding that ward.

![](<../../../../.gitbook/assets/image (4) (2).png>)

### **Service Tab** <a href="#service-tab" id="service-tab"></a>

**Overview**

The overview graph contains multiple data information as below in the selected time period.

* **Total Applications:** This represents the total number of applications for new, modify, and disconnection requests.
* **SLA Compliance:**  This represents the total SLA achieved in percentage.
* **Total Active Connections:** This represents the total active water and sewerage connections.
* **Water-Metered Connections:** This represents the total active metered water connections.
* **Water-Non Metered Connections:** This represents the total active non-metered water connections.
* **Sewerage Connections:** This represents the total active sewerage connections.

![](<../../../../.gitbook/assets/image (1) (1).png>)

**Total Cumulative Connections**

This Graph contains the Water and Sewerage connections information on a monthly basis as a cumulative line graph for each water and sewerage connection separately.

**line** - this graph/chart is data representation on date histograms or date groupings.

![](<../../../../.gitbook/assets/image (5) (2).png>)

#### **Water Connections by Usage Type** <a href="#water-connections-by-usage-type" id="water-connections-by-usage-type"></a>

This graph shows the active Water connections based on the usage/property type.

![](<../../../../.gitbook/assets/image (7) (2).png>)

**Sewerage Connections by Usage Type**

This graph shows the active Sewerage connections based on the usage/property type.

![](<../../../../.gitbook/assets/image (23).png>)

#### **W\&S Connections by Channel Type** <a href="#w-and-s-connections-by-channel-type" id="w-and-s-connections-by-channel-type"></a>

This graph shows the active water and sewerage connections by channel type(eg-online, counter, etc).

![](<../../../../.gitbook/assets/image (27).png>)

**W\&S Connection Ageing**

This tabular chart representation graph shows W\&S applications that have been submitted and have been pending to be worked on. Information like Pending from 0 to 3 days, Pending from 3 to 7 days, Pending from 7 to 15 days, Pending for more than 15 days, and Total Pending Applications is shown in the chart. And this table shows the data at the district level and also has the drill-down chart for each district to ulb and from ulb to ward level data for the same.

_**xtable**_ type allows the addition of multiple computed fields with the aggregated fields dynamically added.

To add multiple computed columns,  **computedFields** \[]  where actionName (IComputedField\<T> interface), fields \[] names as in exist in query key, newField as name to appear for computation must be defined.

![](<../../../../.gitbook/assets/image (19).png>)

On click of any district name will enter into drill-down charts, which will represent that specific District data.

![](<../../../../.gitbook/assets/image (16) (4).png>)

On click of the ULB will navigate to wards under that specific ULB and each ward shows the specific data regarding that ward.

![](<../../../../.gitbook/assets/image (12).png>)

### **Newly Introduced Property** <a href="#newly-introduced-property" id="newly-introduced-property"></a>

**isRoundOff**: This property is introduced to round off the decimal values. Ex: if the value is 25.43 by using isRoundOff property in the configuration we will get it as 25. if the value is 22.56 round of value will be 23.\
This can be used for insights configuration as well for overview graphs.

### Common Properties Available <a href="#common-properties-available" id="common-properties-available"></a>

**Key(eg: fsmTotalrequest):** This is the Visualization Code. This key will be referred to in further visualization configurations.

This is the key which will be used by the client application to indicate which visualization is needed for display.

**chartName:** The name of the Chart which has to be used as a label on the Dashboard. The name of the Chart will be a detailed name.

In this configuration, the Name of the Chart will be the code of Localization which will be used by the Client Side.

**queries:** Some visualizations are derived from a specific data source. While some others are derived from different data sources and are combined together to get a meaningful representation.

The queries of aggregation which are to be used to fetch the right data in the right aggregated format are configured here.

**queries.module:** The module/domain level, on which the query should be applied on. Water and sewerage are W\&S.

**queries.indexName:** The name of the index upon which the query has to be executed is configured here.

**queries.aggrQuery :** The aggregation query in itself is added here. Based on the Module and the Index name specified, this query is attached to the filter part of the complete search request and then executed against that index

**queries.requestQueryMap:** Client Request would carry certain fields which are to be filtered. The parameters specified in the Client Request are different from the parameters in each of these indexed documents.

In order to map the parameters of the request to the parameters of the ElasticSearch Document, this mapping is maintained.

**queries.dateRefField:** Each of these modules have separate indexes. And all of them have their own date fields.&#x20;

When there is a date filter applied against these visualizations, each of them has to apply it against their own date reference fields.

In order to maintain what is the date field in which index, we have this configured in this configuration parameter.

**chartType:** As there are different types of visualizations, this field defines what is the type of chart/visualization that this data should be used to represent.&#x20;

**Chart types available are**:

**metric** - this represents the aggregated amount/value for records filtered by the aggregate es query&#x20;

**pie** - this represents the aggregated data on grouping. This is can be used to represent any line graph, bar graph, pie chart or donut

**line** - this graph/chart is data representation on date histograms or date groupings

**perform** - this chart represents groping data as performance-wise.

**table** - represents a form of plots and values with headers as grouped on and a list of its key, values pairs.&#x20;

**xtable -** represents an advanced feature of the table, it has additional capabilities for dynamic adding header values.&#x20;

**valueType:** In any case of data, the values which are sent to the plot, might be a percentage, sometimes an amount and sometimes it is just a count.

In order to represent them and differentiate the numbers from the amount from the percentage, this field is used to indicate the type of value that this Visualization will be sending.

**action:** Some of the visualizations are not just aggregations of data sources. There might be some cases where we have to do a post-aggregation computation.

For Example, in the case of the top 3 Performing ULBs, the Target and Total Collection are obtained and then the percentage is calculated. In these kinds of cases, the action that has to be performed on the data obtained is defined in this parameter.&#x20;

**documentType:** The type of document upon which the query has to be executed is defined here.&#x20;

**drillChart:** If there is a drill down on the visualization, then the code of the Drill Down Visualization is added here. This will be used by Client Service to manage drill-downs.

**aggregationPaths:** All the queries will be having Aggregation names in them. In order to fetch the value out of each Aggregation Response, the name of the aggregation in the query will be an easy bet. These aggregation paths will have the names of Aggregation in it.

**insights:** It is to show the data with the comparison of last year with arrow symbols, it will show the data in how much % is increased or decreased.&#x20;

**\_comment:** In order to display information on the “i” symbol of each visualization, Visualization Information is maintained in this field.&#x20;

**Postman collection for W\&S-dss:** [https://www.getpostman.com/collections/f346eea97268ac94888b](https://www.getpostman.com/collections/f346eea97268ac94888b),

[https://www.getpostman.com/collections/bb410e74c00cea0d381c](https://www.getpostman.com/collections/bb410e74c00cea0d381c)
