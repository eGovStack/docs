# FSM-DSS Technical Documentation

## Overview

DSS has two sides to it. One being the process in which the Data is pooled to ElasticSearch and the other being the way it is fetched, aggregated, computed, transformed and sent across.

As this revolves around a variety of Data Set, there is a need for making this configurable. So that, tomorrow, given a new scenario is introduced, then it is just a configuration away from getting the newly introduced scenario involved in this flow of process.

This document explains the steps on how to define the configurations for Analytics Side Of DSS for FSM.

## **What is analytics?**

**Analytics :** Micro Service which is responsible for building, fetching, aggregating and computing the Data on ElasticSearch to a consumable Data Response. Which shall be later used for visualizations and graphical representations.

### **Analytics Configurations**

Analytics contains multiple configurations. we need to add the changes related to fsm in this dashboard-analytics.\
Here is the location :[ ![](https://github.com/fluidicon.png)configs/egov-dss-dashboards/dashboard-analytics at qa · egovernments/configs](https://github.com/egovernments/configs/tree/qa/egov-dss-dashboards/dashboard-analytics)\
Below is a list of configurations that need to be changed to run fsm successfully.

1. Chart API Configuration
2. Master Dashboard Configuration
3. Role Dashboard Mappings Configuration

### **Description**

**Chart API Configuration**

Each Visualization has its own properties. Each Visualization comes from different data sources (Sometimes it is a combination of different data sources)

In order to configure each visualization and their properties, we have a Chart API Configuration Document.

In this, Visualization Code, which happens to be the key, will be having its properties configured as a part of configuration and are easily changeable.

Here is the sample ChartApiConfiguration.json data for the fsm.

```
  "fsmTotalrequest": {
    "chartName": "DSS_FSM_TOTAL_REQUESTS",
    "queries": [
      {
        "module": "FSM",
        "indexName": "fsm",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.fsm.tenantId.keyword\":\"pb.testing\"}}]}},\"aggs\":{\"Total Application\":{\"value_count\":{\"field\":\"Data.fsm.@timestamp\"}}}}}}",
        "requestQueryMap": "{\"wardId\" : \"Data.ward.name.keyword\", \"tenantId\" : \"Data.tenantData.code\" ,  \"district\" : \"Data.tenantData.city.districtCode\"}",
        "dateRefField": "Data.fsm.@timestamp"
      }
    ],
    "chartType": "metric",
    "valueType": "number",
    "action": "",
    "drillChart": "none",
    "aggregationPaths": [
      "Total Application"
    ],
    "insight": {
      "chartResponseMap" : "totalApplication",
      "action" : "differenceOfNumbers",
      "upwardIndicator" : "positive",
      "downwardIndicator" : "negative",
      "textMessage" : "$indicator$value% than last $insightInterval",
      "colorCode" : "#228B22",
      "insightInterval" : "year",
      "isRoundOff": true
    },
    "_comment": " FSM Total Applications"
  },
  "totalSludgeTreated": {
    "chartName": "DSS_FSM_TOTAL_SLUDGE_TREATED",
    "queries": [
      {
        "module": "FSM",
        "indexName": "vehicletrip",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.vehicleTrip.tenantId.keyword\":\"pb.testing\"}}]}},\"aggs\":{\"Total Sludge Collection\":{\"sum\":{\"script\":{\"source\":\"(doc['Data.vehicleTrip.volumeCarried'].value)/1000.0\"}}}}}}}",
        "requestQueryMap": "{\"wardId\" : \"Data.ward.name.keyword\", \"tenantId\" : \"Data.tenantData.code\" ,  \"district\" : \"Data.tenantData.city.districtCode\"}",
        "dateRefField": "Data.vehicleTrip.@timestamp"
      }
    ],
    "chartType": "metric",
    "valueType": "number",
    "action": "",
    "drillChart": "none",
    "aggregationPaths": [
      "Total Sludge Collection"
    ],
    "insight": {
      "chartResponseMap" : "totalSludgeTreated",
      "action" : "differenceOfNumbers",
      "upwardIndicator" : "positive",
      "downwardIndicator" : "negative",
      "textMessage" : "$indicator$value% than last $insightInterval",
      "colorCode" : "#228B22",
      "insightInterval" : "year",
      "isRoundOff": true
    },
    "_comment": " FSM Total Sludge Treated"
  },
  "avgFSMCostRequest": {
    "chartName": "DSS_FSM_AVG_FSM_COST_OR_REQ",
    "queries": [
      {
        "module": "FSM",
        "indexName": "fsm",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.tenantId.keyword\":\"pb.testing\"}}],\"must\":[{\"term\":{\"Data.payments.paymentDetails.businessService.keyword\":\"FSM.TRIP_CHARGES\"}}]}},\"aggs\":{\"Average Collection\":{\"avg\":{\"field\":\"Data.payments.paymentDetails.bill.billDetails.amountPaid\"}}}}}}",
        "requestQueryMap": "{\"wardId\" : \"Data.ward.name.keyword\", \"tenantId\" : \"Data.tenantData.code\" ,  \"district\" : \"Data.tenantData.city.districtCode\"}",
        "dateRefField": "Data.fsm.@timestamp"
      }
    ],
    "chartType": "metric",
    "valueType": "amount",
    "action": "",
    "drillChart": "none",
    "isRoundOff": true,
    "aggregationPaths": [
      "Average Collection"
    ],
    "insight": {
      "chartResponseMap" : "averageCollection",
      "action" : "differenceOfNumbers",
      "upwardIndicator" : "positive",
      "downwardIndicator" : "negative",
      "textMessage" : "$indicator$value% than last $insightInterval",
      "colorCode" : "#228B22",
      "insightInterval" : "year",
      "isRoundOff": true
    },
    "_comment": " FSM Average Collection"
  },
  "totalCollectioninLacs": {
    "chartName": "DSS_FSM_TOTAL_COLLECTION",
    "queries": [
      {
        "module": "FSM",
        "indexName": "fsm",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.tenantId.keyword\":\"pb.testing\"}}],\"must\":[{\"term\":{\"Data.payments.paymentDetails.businessService.keyword\":\"FSM.TRIP_CHARGES\"}}]}},\"aggs\":{\"Total Collection\":{\"sum\":{\"field\":\"Data.payments.paymentDetails.bill.billDetails.amountPaid\"}}}}}}",
        "requestQueryMap": "{\"wardId\" : \"Data.ward.name.keyword\", \"tenantId\" : \"Data.tenantData.code\" ,  \"district\" : \"Data.tenantData.city.districtCode\"}",
        "dateRefField": "Data.fsm.@timestamp"
      }
    ],
    "chartType": "metric",
    "valueType": "amount",
    "action": "",
    "drillChart": "none",
    "documentType": "_doc",
    "aggregationPaths": [
      "Total Collection"
    ],
    "insight": {
      "chartResponseMap" : "totalCollection",
      "action" : "differenceOfNumbers",
      "upwardIndicator" : "positive",
      "downwardIndicator" : "negative",
      "textMessage" : "$indicator$value% than last $insightInterval",
      "colorCode" : "#228B22",
      "insightInterval" : "year",
      "isRoundOff": true
    },
    "_comment": " FSM Total Collection"
  },
  "slaCompliance": {
    "chartName": "DSS_FSM_SLA_COMPLIANCE",
    "queries": [
      {
        "module": "FSM",
        "indexName": "fsm",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.service.tenantId.keyword\":\"pb.testing\"}}]}},\"aggs\":{\"Closed With In Sla\":{\"filter\":{\"bool\":{\"must\":[{\"terms\":{\"Data.fsm.applicationStatus.keyword\":[\"COMPLETED\",\"CITIZEN_FEEDBACK_PENDING\"]}},{\"script\":{\"script\":{\"source\":\"doc['Data.fsm.auditDetails.lastModifiedTime'].value - doc['Data.fsm.auditDetails.createdTime'].value < params.threshold\",\"lang\":\"painless\",\"params\":{\"threshold\":172800000}}}}]}},\"aggs\":{\"count\":{\"terms\":{\"field\":\"Data.fsm.tenantId.keyword\"},\"aggs\":{\"tenant_count\":{\"value_count\":{\"field\":\"Data.fsm.tenantId.keyword\"}}}}}},\"Total Applications\":{\"terms\":{\"field\":\"Data.fsm.tenantId.keyword\"},\"aggs\":{\"tenant_count\":{\"value_count\":{\"field\":\"Data.fsm.tenantId.keyword\"}}}}}}}}",
        "requestQueryMap": "{\"wardId\" : \"Data.ward.name.keyword\", \"tenantId\" : \"Data.tenantData.code\" ,  \"district\" : \"Data.tenantData.city.districtCode\"}",
        "dateRefField": "Data.fsm.@timestamp"
      }
    ],
    "chartType": "metric",
    "valueType": "percentage",
    "drillChart": "none",
    "documentType": "_doc",
    "action": "percentage",
    "isRoundOff": true,
    "aggregationPaths": [
      "Closed With In Sla",
      "Total Applications"
    ],
    "insight": {
      "chartResponseMap" : "slaCompliance",
      "action" : "differenceOfNumbers",
      "upwardIndicator" : "positive",
      "downwardIndicator" : "negative",
      "textMessage" : "$indicator$value% than last $insightInterval",
      "colorCode" : "#228B22",
      "insightInterval" : "year",
      "isRoundOff": true
    },
    "_comment": " SLA Compliance"
  },
  "citizenAvgRating": {
    "chartName": "DSS_FSM_CITIZEN_AVG_RATING",
    "queries": [
      {
        "module": "FSM",
        "indexName": "fsm",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.fsm.tenantId.keyword\":\"pb.testing\"}}],\"must\":[{\"terms\":{\"Data.fsm.applicationStatus.keyword\":[\"COMPLETED\"]}},{\"term\":{\"Data.history.action.keyword\":\"RATE\"}},{\"exists\":{\"field\":\"Data.history\"}},{\"range\":{\"Data.history.rating\":{\"gte\":1}}}]}},\"aggs\":{\"Citizen Average Rating\":{\"avg\":{\"script\":\"int sum = 0;int count =0;if(params['_source']['Data']['history']!=null){ for (item in params['_source']['Data']['history']) {if(item.rating!=null){ sum += item.rating;} }} return sum;\"}}}}}}",
        "requestQueryMap": "{\"wardId\" : \"Data.ward.name.keyword\", \"tenantId\" : \"Data.tenantData.code\" ,  \"district\" : \"Data.tenantData.city.districtCode\"}",
        "dateRefField": "Data.fsm.@timestamp"
      }
    ],
    "chartType": "metric",
    "valueType": "number",
    "action": "",
    "drillChart": "none",
    "documentType": "_doc",
    "aggregationPaths": [
      "Citizen Average Rating"
    ],
    "postAggregationTheory": "",
    "insight": {},
    "_comment": " Citizen Average rating"
  },
  "fsmCollectionByUsageType": {
    "chartName": "DSS_FSM_COLLECTION_BY_USAGE_TYPE",
    "queries": [
      {
        "module": "FSM",
        "dateRefField": "Data.fsm.@timestamp",
        "requestQueryMap": "{\"wardId\" : \"Data.ward.name.keyword\", \"tenantId\" : \"Data.tenantData.code\" ,  \"district\" : \"Data.tenantData.city.districtCode\"}",
        "indexName": "fsm",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.fsm.tenantId.keyword\":\"pb.testing\"}}]}},\"aggs\":{\"Usage Type\":{\"terms\":{\"field\":\"Data.fsm.propertyUsage.keyword\"},\"aggs\":{\"Assessed Properties\":{\"sum\":{\"field\":\"Data.payments.paymentDetails.bill.billDetails.amountPaid\"}}}}}}}}"
      }
    ],
    "chartType": "pie",
    "valueType": "amount",
    "action": "",
    "documentType": "_doc",
    "drillChart": "none",
    "aggregationPaths": [
      "Usage Type"
    ],
    "insight": {
    },
    "_comment": " "
  },
  "fsmTotalCumulativeCollection": {
    "chartName": "DSS_FSM_TOTAL_CUMULATIVE_COLLECTION",
    "queries": [
      {
        "module": "FSM",
        "dateRefField": "Data.fsm.@timestamp",
        "requestQueryMap": "{\"wardId\" : \"Data.ward.name.keyword\", \"tenantId\" : \"Data.tenantData.code\" ,  \"district\" : \"Data.tenantData.city.districtCode\"}",
        "indexName": "fsm",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.fsm.tenantId.keyword\":\"pb.testing\"}}]}},\"aggs\":{\"Total Collection\":{\"date_histogram\":{\"field\":\"Data.fsm.@timestamp\",\"interval\":\"intervalvalue\"},\"aggs\":{\"Count\":{\"sum\":{\"field\":\"Data.payments.paymentDetails.bill.billDetails.amountPaid\"}}}}}}}}"
      }
    ],
    "chartType": "line",
    "valueType": "amount",
    "action": "",
    "drillChart": "none",
    "documentType": "_doc",
    "aggregationPaths": [
      "Total Collection"
    ],
    "isCumulative": true,
    "interval": "month",
    "insight": {
    },
    "_comment": " "
  },
  "fsmTopUlbByPerformance": {
    "chartName": "DSS_FSM_TOP_ULB_BY_PERFORMANCE",
    "queries": [
      {
        "module": "FSM",
        "dateRefField": "Data.fsm.@timestamp",
        "requestQueryMap": "{\"wardId\" : \"Data.ward.name.keyword\", \"tenantId\" : \"Data.tenantData.code\" ,  \"district\" : \"Data.tenantData.city.districtCode\"}",
        "indexName": "fsm",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.fsm.tenantId.keyword\":\"pb.testing\"}}]}},\"aggs\":{\"Closed With In Sla\":{\"filter\":{\"bool\":{\"must\":[{\"terms\":{\"Data.fsm.applicationStatus.keyword\":[\"COMPLETED\",\"CITIZEN_FEEDBACK_PENDING\"]}},{\"script\":{\"script\":{\"source\":\"doc['Data.fsm.auditDetails.lastModifiedTime'].value - doc['Data.fsm.auditDetails.createdTime'].value < params.threshold\",\"lang\":\"painless\",\"params\":{\"threshold\":172800000}}}}]}},\"aggs\":{\"count\":{\"terms\":{\"field\":\"Data.fsm.tenantId.keyword\"},\"aggs\":{\"tenant_count\":{\"value_count\":{\"field\":\"Data.fsm.tenantId.keyword\"}}}}}},\"Total Applications\":{\"terms\":{\"field\":\"Data.fsm.tenantId.keyword\"},\"aggs\":{\"tenant_count\":{\"value_count\":{\"field\":\"Data.fsm.tenantId.keyword\"}}}}}}}}"
      }
    ],
    "chartType": "perform",
    "valueType": "percentage",
    "drillChart": "none",
    "documentType": "_doc",
    "drillChart": "ulbTopDrillChart",
    "action": "percentage",
    "plotLabel": "DSS_COMPLETION_RATE",
    "isRoundOff": true,
    "order": "desc",
    "limit": 3,
    "aggregationPaths": [
      "Closed With In Sla",
      "Total Applications"
    ],
    "isCumulative": false,
    "interval": "month",
    "insight": {
    },
    "_comment": ""
  },
  "ulbTopDrillChart": {
    "chartName": "DSS_FSM_ULB_PERFORMANCE",
    "queries": [
      {
        "module": "FSM",
        "dateRefField": "Data.fsm.@timestamp",
        "requestQueryMap": "{\"wardId\" : \"Data.ward.name.keyword\", \"tenantId\" : \"Data.tenantData.code\" ,  \"district\" : \"Data.tenantData.city.districtCode\"}",
        "indexName": "fsm",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"data.fsm.tenantId.keyword\":\"pb.testing\"}}]}},\"aggs\":{\"ULB\":{\"terms\":{\"field\":\"Data.fsm.tenantId.keyword\",\"size\":1000,\"order\":{\"_count\":\"desc\"}},\"aggs\":{\"TotalRequests\":{\"value_count\":{\"field\":\"Data.fsm.tenantId.keyword\"}},\"ClosedWithInSLA\":{\"filter\":{\"bool\":{\"must\":[{\"terms\":{\"Data.fsm.applicationStatus.keyword\":[\"COMPLETED\",\"CITIZEN_FEEDBACK_PENDING\"]}},{\"script\":{\"script\":{\"source\":\"doc['Data.fsm.auditDetails.lastModifiedTime'].value - doc['Data.fsm.auditDetails.createdTime'].value < params.threshold\",\"lang\":\"painless\",\"params\":{\"threshold\":172800000}}}}]}},\"aggs\":{\"valueCount\":{\"value_count\":{\"field\":\"Data.fsm.tenantId.keyword\"}}}},\"ClosedOutsideSLA\":{\"filter\":{\"bool\":{\"must\":[{\"terms\":{\"Data.fsm.applicationStatus.keyword\":[\"COMPLETED\",\"CITIZEN_FEEDBACK_PENDING\"]}},{\"script\":{\"script\":{\"source\":\"doc['Data.fsm.auditDetails.lastModifiedTime'].value - doc['Data.fsm.auditDetails.createdTime'].value > params.threshold\",\"lang\":\"painless\",\"params\":{\"threshold\":172800000}}}}]}},\"aggs\":{\"valueCount\":{\"value_count\":{\"field\":\"Data.fsm.tenantId.keyword\"}}}},\"CitizenAverageRating\":{\"filter\":{\"bool\":{\"must\":[{\"terms\":{\"Data.fsm.applicationStatus.keyword\":[\"COMPLETED\"]}},{\"term\":{\"Data.history.action.keyword\":\"RATE\"}},{\"exists\":{\"field\":\"Data.history\"}},{\"range\":{\"Data.history.rating\":{\"gte\":1}}}]}},\"aggs\":{\"CitizenAvgRating\":{\"avg\":{\"script\":\"int sum = 0;int count =0;if(params['_source']['Data']['history']!=null){ for (item in params['_source']['Data']['history']) {if(item.rating!=null){ sum += item.rating;} }} return sum;\"}}}}}}}}}}"
      }
    ],
   "filterKeys": [
      {"key": "tenantId", "column": "ULB"}
    ],
    "isPostResponseHandler": true,
    "chartType": "table",
    "valueType": "number",
    "action": "",
    "documentType": "_doc",
    "drillChart": "none",
    "plotLabel":"ULB",
    "aggregationPaths": [
      "TotalRequests",
      "ClosedWithInSLA",
      "ClosedOutsideSLA",
      "CitizenAverageRating"
    ],
    "pathDataTypeMapping": [
      {
        "TotalRequests" : "number"
      },
      {
        "ClosedWithInSLA" : "number"
      },
      {
        "ClosedOutsideSLA" : "number"
      },
      {
        "CitizenAverageRating" : "number"
      }
    ],
    "isCumulative": true,
    "interval": "month",
    "insight": {
    },
    "_comment": " "
  },
  "fsmBottomUlbByPerformance": {
    "chartName": "DSS_FSM_BOTTOM_ULB_BY_PERFORMANCE",
    "queries": [
      {
        "module": "FSM",
        "dateRefField": "Data.fsm.@timestamp",
        "requestQueryMap": "{\"wardId\" : \"Data.ward.name.keyword\", \"tenantId\" : \"Data.tenantData.code\" ,  \"district\" : \"Data.tenantData.city.districtCode\"}",
        "indexName": "fsm",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.fsm.tenantId.keyword\":\"pb.testing\"}}]}},\"aggs\":{\"Closed With In Sla\":{\"filter\":{\"bool\":{\"must\":[{\"terms\":{\"Data.fsm.applicationStatus.keyword\":[\"COMPLETED\",\"CITIZEN_FEEDBACK_PENDING\"]}},{\"script\":{\"script\":{\"source\":\"doc['Data.fsm.auditDetails.lastModifiedTime'].value - doc['Data.fsm.auditDetails.createdTime'].value < params.threshold\",\"lang\":\"painless\",\"params\":{\"threshold\":172800000}}}}]}},\"aggs\":{\"count\":{\"terms\":{\"field\":\"Data.fsm.tenantId.keyword\"},\"aggs\":{\"tenant_count\":{\"value_count\":{\"field\":\"Data.fsm.tenantId.keyword\"}}}}}},\"Total Applications\":{\"terms\":{\"field\":\"Data.fsm.tenantId.keyword\"},\"aggs\":{\"tenant_count\":{\"value_count\":{\"field\":\"Data.fsm.tenantId.keyword\"}}}}}}}}"
      }
    ],
    "chartType": "perform",
    "valueType": "percentage",
    "drillChart": "none",
    "documentType": "_doc",
    "drillChart": "ulbBottomDrillChart",
    "action": "percentage",
    "isRoundOff": true,
    "plotLabel": "DSS_COMPLETION_RATE",
    "order": "asc",
    "limit": 3,
    "aggregationPaths": [
      "Closed With In Sla",
      "Total Applications"
    ],
    "isCumulative": false,
    "interval": "month",
    "insight": {
    },
    "_comment": ""
  },
  "ulbBottomDrillChart": {
    "chartName": "DSS_FSM_ULB_PERFORMANCE",
    "queries": [
      {
        "module": "FSM",
        "dateRefField": "Data.fsm.@timestamp",
        "requestQueryMap": "{\"wardId\" : \"Data.ward.name.keyword\", \"tenantId\" : \"Data.tenantData.code\" ,  \"district\" : \"Data.tenantData.city.districtCode\"}",
        "indexName": "fsm",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"data.fsm.tenantId.keyword\":\"pb.testing\"}}]}},\"aggs\":{\"ULB\":{\"terms\":{\"field\":\"Data.fsm.tenantId.keyword\",\"size\":1000,\"order\":{\"_count\":\"asc\"}},\"aggs\":{\"TotalRequests\":{\"value_count\":{\"field\":\"Data.fsm.tenantId.keyword\"}},\"ClosedWithInSLA\":{\"filter\":{\"bool\":{\"must\":[{\"terms\":{\"Data.fsm.applicationStatus.keyword\":[\"COMPLETED\",\"CITIZEN_FEEDBACK_PENDING\"]}},{\"script\":{\"script\":{\"source\":\"doc['Data.fsm.auditDetails.lastModifiedTime'].value - doc['Data.fsm.auditDetails.createdTime'].value < params.threshold\",\"lang\":\"painless\",\"params\":{\"threshold\":172800000}}}}]}},\"aggs\":{\"valueCount\":{\"value_count\":{\"field\":\"Data.fsm.tenantId.keyword\"}}}},\"ClosedOutsideSLA\":{\"filter\":{\"bool\":{\"must\":[{\"terms\":{\"Data.fsm.applicationStatus.keyword\":[\"COMPLETED\",\"CITIZEN_FEEDBACK_PENDING\"]}},{\"script\":{\"script\":{\"source\":\"doc['Data.fsm.auditDetails.lastModifiedTime'].value - doc['Data.fsm.auditDetails.createdTime'].value > params.threshold\",\"lang\":\"painless\",\"params\":{\"threshold\":172800000}}}}]}},\"aggs\":{\"valueCount\":{\"value_count\":{\"field\":\"Data.fsm.tenantId.keyword\"}}}},\"CitizenAverageRating\":{\"filter\":{\"bool\":{\"must\":[{\"terms\":{\"Data.fsm.applicationStatus.keyword\":[\"COMPLETED\"]}},{\"term\":{\"Data.history.action.keyword\":\"RATE\"}},{\"exists\":{\"field\":\"Data.history\"}},{\"range\":{\"Data.history.rating\":{\"gte\":1}}}]}},\"aggs\":{\"CitizenAvgRating\":{\"avg\":{\"script\":\"int sum = 0;int count =0;if(params['_source']['Data']['history']!=null){ for (item in params['_source']['Data']['history']) {if(item.rating!=null){ sum += item.rating;} }} return sum;\"}}}}}}}}}}"
      }
    ],
   "filterKeys": [
      {"key": "tenantId", "column": "ULB"}
    ],
    "isPostResponseHandler": true,
    "chartType": "table",
    "valueType": "number",
    "action": "",
    "documentType": "_doc",
    "drillChart": "none",
    "plotLabel":"ULB",
    "aggregationPaths": [
      "TotalRequests",
      "ClosedWithInSLA",
      "ClosedOutsideSLA",
      "CitizenAverageRating"
    ],
    "pathDataTypeMapping": [
      {
        "TotalRequests" : "number"
      },
      {
        "ClosedWithInSLA" : "number"
      },
      {
        "ClosedOutsideSLA" : "number"
      },
      {
        "CitizenAverageRating" : "number"
      }
    ],
    "isCumulative": true,
    "interval": "month",
    "insight": {
    },
    "_comment": " "
  },
  "fsmCapacityUtilization": {
    "chartName": "DSS_FSTP_CAPACITY_UTILIZATION",
    "queries": [
      {
        "module": "FSM",
        "dateRefField": "Data.vehicleTrip.@timestamp",
        "requestQueryMap": "{\"wardId\" : \"Data.ward.name.keyword\", \"tenantId\" : \"Data.tenantData.code\" ,  \"district\" : \"Data.tenantData.city.districtCode\"}",
        "indexName": "vehicletrip",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.vehicleTrip.tenantId.keyword\":\"pb.testing\"}}]}},\"aggs\":{\"Capacity Utilization\":{\"date_histogram\":{\"field\":\"Data.vehicleTrip.@timestamp\",\"interval\":\"month\"},\"aggs\":{\"Count\":{\"sum\":{\"script\":{\"source\":\"(doc['Data.vehicleTrip.volumeCarried'].value)/1000.0\"}}}}}}}}}"
      }
    ],
    "chartType": "line",
    "valueType": "amount",
    "action": "",
    "isRoundOff": true,
    "documentType": "_doc",
    "drillChart": "none",
    "aggregationPaths": [
      "Capacity Utilization"
    ],
    "isCumulative": true,
    "interval": "month",
    "insight": {
    },
    "_comment": " "
  },
  "fsmMonthlyWasteCal": {
    "chartName": "DSS_FSM_MONTHLY_WASTE_CAL",
    "queries": [
      {
        "module": "FSM",
        "dateRefField": "Data.vehicleTrip.@timestamp",
        "requestQueryMap": "{\"wardId\" : \"Data.ward.name.keyword\", \"tenantId\" : \"Data.tenantData.code\" ,  \"district\" : \"Data.tenantData.city.districtCode\"}",
        "indexName": "vehicletrip",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.vehicleTrip.tenantId.keyword\":\"pb.testing\"}}]}},\"aggs\":{\"Septage Dumped At Plant\":{\"date_histogram\":{\"field\":\"Data.vehicleTrip.@timestamp\",\"interval\":\"month\"},\"aggs\":{\"Count\":{\"sum\":{\"script\":{\"source\":\"(doc['Data.vehicleTrip.volumeCarried'].value)/1000.0\"}}}}},\"Septage Collected\":{\"date_histogram\":{\"field\":\"Data.vehicleTrip.@timestamp\",\"interval\":\"month\"},\"aggs\":{\"Count\":{\"sum\":{\"script\":{\"source\":\"(doc['Data.vehicleTrip.tripDetails.volume'].value)/1000.0\"}}}}}}}}}"
      }
    ],
    "chartType": "line",
    "valueType": "number",
    "action": "",
    "isRoundOff": true,
    "documentType": "_doc",
    "drillChart": "none",
    "aggregationPaths": [
      "Septage Collected",
      "Septage Dumped At Plant"
    ],
    "isCumulative": false,
    "interval": "month",
    "insight": {
    },
    "_comment": " "
  },
  "fsmTopDsoByPerformance": {
    "chartName": "DSS_FSM_TOP_DSO_BY_PERFORMANCE",
    "queries": [
      {
        "module": "FSM",
        "dateRefField": "Data.fsm.@timestamp",
        "requestQueryMap": "{\"wardId\" : \"Data.ward.name.keyword\", \"tenantId\" : \"Data.tenantData.code\" ,  \"district\" : \"Data.tenantData.city.districtCode\"}",
        "indexName": "fsm",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.fsm.tenantId.keyword\":\"pb.testing\"}}]}},\"aggs\":{\"Raised\":{\"terms\":{\"field\":\"Data.vendor.name.keyword\",\"size\":3,\"order\":{\"_count\":\"desc\"}},\"aggs\":{\"Count\":{\"value_count\":{\"field\":\"Data.vendor.name.keyword\"}}}},\"Closed Within SLA\":{\"terms\":{\"field\":\"Data.vendor.name.keyword\",\"size\":3,\"order\":{\"_count\":\"desc\"}},\"aggs\":{\"Count\":{\"filter\":{\"bool\":{\"must\":[{\"terms\":{\"Data.fsm.applicationStatus.keyword\":[\"COMPLETED\",\"CITIZEN_FEEDBACK_PENDING\"]}},{\"script\":{\"script\":{\"source\":\"doc['Data.fsm.auditDetails.lastModifiedTime'].value - doc['Data.fsm.auditDetails.createdTime'].value < params.threshold\",\"lang\":\"painless\",\"params\":{\"threshold\":172800000}}}}]}},\"aggs\":{\"valueCount\":{\"value_count\":{\"field\":\"Data.vendor.name.keyword\"}}}}}},\"Closed Outside SLA\":{\"terms\":{\"field\":\"Data.vendor.name.keyword\",\"size\":3,\"order\":{\"_count\":\"desc\"}},\"aggs\":{\"Count\":{\"filter\":{\"bool\":{\"must\":[{\"terms\":{\"Data.fsm.applicationStatus.keyword\":[\"COMPLETED\",\"CITIZEN_FEEDBACK_PENDING\"]}},{\"script\":{\"script\":{\"source\":\"doc['Data.fsm.auditDetails.lastModifiedTime'].value - doc['Data.fsm.auditDetails.createdTime'].value > params.threshold\",\"lang\":\"painless\",\"params\":{\"threshold\":172800000}}}}]}},\"aggs\":{\"valueCount\":{\"value_count\":{\"field\":\"Data.vendor.name.keyword\"}}}}}}}}}}"
      }
    ],
    "chartType": "line",
    "valueType": "number",
    "action": "",
    "drillChart": "dsoTopDrillChart",
    "documentType": "_doc",
    "aggregationPaths": [
      "Raised",
      "Closed Within SLA",
      "Closed Outside SLA"
    ],
    "isCumulative": false,
    "interval": "month",
    "insight": {
    },
    "_comment": ""
  },
  "dsoTopDrillChart": {
    "chartName": "DSS_FSM_DSO_PERFORMANCE",
    "queries": [
      {
        "module": "FSM",
        "dateRefField": "Data.fsm.@timestamp",
        "requestQueryMap": "{\"wardId\" : \"Data.ward.name.keyword\", \"tenantId\" : \"Data.tenantData.code\" ,  \"district\" : \"Data.tenantData.city.districtCode\"}",
        "indexName": "fsm",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"data.fsm.tenantId.keyword\":\"pb.testing\"}}]}},\"aggs\":{\"DSOName\":{\"terms\":{\"field\":\"Data.vendor.name.keyword\",\"size\":1000,\"order\":{\"_count\":\"desc\"}},\"aggs\":{\"TotalRequest\":{\"value_count\":{\"field\":\"Data.vendor.name.keyword\"}},\"ClosedWithinSLA\":{\"filter\":{\"bool\":{\"must\":[{\"terms\":{\"Data.fsm.applicationStatus.keyword\":[\"COMPLETED\",\"CITIZEN_FEEDBACK_PENDING\"]}},{\"script\":{\"script\":{\"source\":\"doc['Data.fsm.auditDetails.lastModifiedTime'].value - doc['Data.fsm.auditDetails.createdTime'].value < params.threshold\",\"lang\":\"painless\",\"params\":{\"threshold\":172800000}}}}]}},\"aggs\":{\"valueCount\":{\"value_count\":{\"field\":\"Data.vendor.name.keyword\"}}}},\"ClosedOutsideSLA\":{\"filter\":{\"bool\":{\"must\":[{\"terms\":{\"Data.fsm.applicationStatus.keyword\":[\"COMPLETED\",\"CITIZEN_FEEDBACK_PENDING\"]}},{\"script\":{\"script\":{\"source\":\"doc['Data.fsm.auditDetails.lastModifiedTime'].value - doc['Data.fsm.auditDetails.createdTime'].value > params.threshold\",\"lang\":\"painless\",\"params\":{\"threshold\":172800000}}}}]}},\"aggs\":{\"valueCount\":{\"value_count\":{\"field\":\"Data.vendor.name.keyword\"}}}},\"CitizenAverageRating\":{\"filter\":{\"bool\":{\"must\":[{\"terms\":{\"Data.fsm.applicationStatus.keyword\":[\"COMPLETED\"]}},{\"term\":{\"Data.history.action.keyword\":\"RATE\"}},{\"exists\":{\"field\":\"Data.history\"}},{\"range\":{\"Data.history.rating\":{\"gte\":1}}}]}},\"aggs\":{\"CitizenAvgRating\":{\"avg\":{\"script\":\"int sum = 0;int count =0;if(params['_source']['Data']['history']!=null){ for (item in params['_source']['Data']['history']) {if(item.rating!=null){ sum += item.rating;} }} return sum;\"}}}}}}}}}}"
      }
    ],
    "filterKeys": [
      {"key": "dsoName", "column": "DSOName"}
    ],
    "isPostResponseHandler": true,
    "chartType": "table",
    "valueType": "number",
    "action": "",
    "documentType": "_doc",
    "drillChart": "none",
    "plotLabel":"DSOName",
    "aggregationPaths": [
      "TotalRequest",
      "ClosedWithinSLA",
      "ClosedOutsideSLA",
      "CitizenAverageRating"
    ],
    "pathDataTypeMapping": [
      {
        "TotalRequest" : "number"
      },
      {
        "ClosedWithinSLA" : "number"
      },
        {
        "ClosedOutsideSLA" : "number"
      },
      {
        "CitizenAverageRating" : "number"
      }
    ],
    "isCumulative": true,
    "interval": "month",
    "insight": {
    },
    "_comment": " "
  },
  "fsmBottomDsoByPerformance": {
    "chartName": "DSS_FSM_BOTTOM_DSO_BY_PERFORMANCE",
    "queries": [
      {
        "module": "FSM",
        "dateRefField": "Data.fsm.@timestamp",
        "requestQueryMap": "{\"wardId\" : \"Data.ward.name.keyword\", \"tenantId\" : \"Data.tenantData.code\" ,  \"district\" : \"Data.tenantData.city.districtCode\"}",
        "indexName": "fsm",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.fsm.tenantId.keyword\":\"pb.testing\"}}]}},\"aggs\":{\"Raised\":{\"terms\":{\"field\":\"Data.vendor.name.keyword\",\"size\":3,\"order\":{\"_count\":\"asc\"}},\"aggs\":{\"Count\":{\"value_count\":{\"field\":\"Data.vendor.name.keyword\"}}}},\"Closed Within SLA\":{\"terms\":{\"field\":\"Data.vendor.name.keyword\",\"size\":3,\"order\":{\"_count\":\"asc\"}},\"aggs\":{\"Count\":{\"filter\":{\"bool\":{\"must\":[{\"terms\":{\"Data.fsm.applicationStatus.keyword\":[\"COMPLETED\",\"CITIZEN_FEEDBACK_PENDING\"]}},{\"script\":{\"script\":{\"source\":\"doc['Data.fsm.auditDetails.lastModifiedTime'].value - doc['Data.fsm.auditDetails.createdTime'].value < params.threshold\",\"lang\":\"painless\",\"params\":{\"threshold\":172800000}}}}]}},\"aggs\":{\"valueCount\":{\"value_count\":{\"field\":\"Data.vendor.name.keyword\"}}}}}},\"Closed Outside SLA\":{\"terms\":{\"field\":\"Data.vendor.name.keyword\",\"size\":3,\"order\":{\"_count\":\"asc\"}},\"aggs\":{\"Count\":{\"filter\":{\"bool\":{\"must\":[{\"terms\":{\"Data.fsm.applicationStatus.keyword\":[\"COMPLETED\",\"CITIZEN_FEEDBACK_PENDING\"]}},{\"script\":{\"script\":{\"source\":\"doc['Data.fsm.auditDetails.lastModifiedTime'].value - doc['Data.fsm.auditDetails.createdTime'].value > params.threshold\",\"lang\":\"painless\",\"params\":{\"threshold\":172800000}}}}]}},\"aggs\":{\"valueCount\":{\"value_count\":{\"field\":\"Data.vendor.name.keyword\"}}}}}}}}}}"
      }
    ],
    "chartType": "line",
    "valueType": "number",
    "action": "",
    "drillChart": "dsoBottomDrillChart",
    "documentType": "_doc",
    "aggregationPaths": [
      "Raised",
      "Closed Within SLA",
      "Closed Outside SLA"
    ],
    "isCumulative": false,
    "interval": "month",
    "insight": {
    },
    "_comment": ""
  },
  "dsoBottomDrillChart": {
    "chartName": "DSS_FSM_DSO_PERFORMANCE",
    "queries": [
      {
        "module": "FSM",
        "dateRefField": "Data.fsm.@timestamp",
        "requestQueryMap": "{\"wardId\" : \"Data.ward.name.keyword\", \"tenantId\" : \"Data.tenantData.code\" ,  \"district\" : \"Data.tenantData.city.districtCode\"}",
        "indexName": "fsm",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"data.fsm.tenantId.keyword\":\"pb.testing\"}}]}},\"aggs\":{\"DSOName\":{\"terms\":{\"field\":\"Data.vendor.name.keyword\",\"size\":1000,\"order\":{\"_count\":\"asc\"}},\"aggs\":{\"TotalRequest\":{\"value_count\":{\"field\":\"Data.vendor.name.keyword\"}},\"ClosedWithinSLA\":{\"filter\":{\"bool\":{\"must\":[{\"terms\":{\"Data.fsm.applicationStatus.keyword\":[\"COMPLETED\",\"CITIZEN_FEEDBACK_PENDING\"]}},{\"script\":{\"script\":{\"source\":\"doc['Data.fsm.auditDetails.lastModifiedTime'].value - doc['Data.fsm.auditDetails.createdTime'].value < params.threshold\",\"lang\":\"painless\",\"params\":{\"threshold\":172800000}}}}]}},\"aggs\":{\"valueCount\":{\"value_count\":{\"field\":\"Data.vendor.name.keyword\"}}}},\"ClosedOutsideSLA\":{\"filter\":{\"bool\":{\"must\":[{\"terms\":{\"Data.fsm.applicationStatus.keyword\":[\"COMPLETED\",\"CITIZEN_FEEDBACK_PENDING\"]}},{\"script\":{\"script\":{\"source\":\"doc['Data.fsm.auditDetails.lastModifiedTime'].value - doc['Data.fsm.auditDetails.createdTime'].value > params.threshold\",\"lang\":\"painless\",\"params\":{\"threshold\":172800000}}}}]}},\"aggs\":{\"valueCount\":{\"value_count\":{\"field\":\"Data.vendor.name.keyword\"}}}},\"CitizenAverageRating\":{\"filter\":{\"bool\":{\"must\":[{\"terms\":{\"Data.fsm.applicationStatus.keyword\":[\"COMPLETED\"]}},{\"term\":{\"Data.history.action.keyword\":\"RATE\"}},{\"exists\":{\"field\":\"Data.history\"}},{\"range\":{\"Data.history.rating\":{\"gte\":1}}}]}},\"aggs\":{\"CitizenAvgRating\":{\"avg\":{\"script\":\"int sum = 0;int count =0;if(params['_source']['Data']['history']!=null){ for (item in params['_source']['Data']['history']) {if(item.rating!=null){ sum += item.rating;} }} return sum;\"}}}}}}}}}}"
      }
    ],
    "filterKeys": [
      {"key": "dsoName", "column": "DSOName"}
    ],
    "isPostResponseHandler": true,
    "chartType": "table",
    "valueType": "number",
    "action": "",
    "documentType": "_doc",
    "drillChart": "none",
    "plotLabel":"DSOName",
    "aggregationPaths": [
      "TotalRequest",
      "ClosedWithinSLA",
      "ClosedOutsideSLA",
      "CitizenAverageRating"
    ],
    "pathDataTypeMapping": [
      {
        "TotalRequest" : "number"
      },
      {
        "ClosedWithinSLA" : "number"
      },
      {
        "ClosedOutsideSLA" : "number"
      },
      {
        "CitizenAverageRating" : "number"
      }
    ],
    "isCumulative": true,
    "interval": "month",
    "insight": {
    },
    "_comment": " "
  },
  "fsmTotalReqByDistrict": {
    "chartName": "DSS_FSM_TOTAL_REQ_BY_DISTRICT",
    "queries": [
      {
        "module": "FSM",
        "dateRefField": "Data.fsm.@timestamp",
        "requestQueryMap": "{\"wardId\" : \"Data.ward.name.keyword\", \"tenantId\" : \"Data.tenantData.code\" ,  \"district\" : \"Data.tenantData.city.districtName\"}",
        "indexName": "fsm",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.fsm.tenantId.keyword\":\"pb.testing\"}}]}},\"aggs\":{\"Open_Req\":{\"filter\":{\"bool\":{\"must_not\":[{\"terms\":{\"Data.fsm.applicationStatus.keyword\":[\"COMPLETED\",\"CITIZEN_FEEDBACK_PENDING\"]}}]}},\"aggs\":{\"OpenReq\":{\"value_count\":{\"field\":\"Data.fsm.tenantId.keyword\"}}}},\"Closed_Req\":{\"filter\":{\"bool\":{\"must\":[{\"terms\":{\"Data.fsm.applicationStatus.keyword\":[\"COMPLETED\",\"CITIZEN_FEEDBACK_PENDING\"]}}]}},\"aggs\":{\"ClosedReq\":{\"value_count\":{\"field\":\"Data.fsm.tenantId.keyword\"}}}},\"TotalReq\":{\"value_count\":{\"field\":\"Data.fsm.tenantId.keyword\"}},\"Closed_With_In_Sla\":{\"filter\":{\"bool\":{\"must\":[{\"terms\":{\"Data.fsm.applicationStatus.keyword\":[\"COMPLETED\",\"CITIZEN_FEEDBACK_PENDING\"]}},{\"script\":{\"script\":{\"source\":\"doc['Data.fsm.auditDetails.lastModifiedTime'].value - doc['Data.fsm.auditDetails.createdTime'].value < params.threshold\",\"lang\":\"painless\",\"params\":{\"threshold\":172800000}}}}]}},\"aggs\":{\"ClosedWithInSla\":{\"value_count\":{\"field\":\"Data.fsm.tenantId.keyword\"}}}},\"TotalCollection\":{\"sum\":{\"field\":\"Data.payments.paymentDetails.bill.billDetails.amountPaid\"}}}}}}"
      }
    ],
    "isMdmsEnabled": true,
    "filterKeys": [
      {"key": "tenantId", "column": "District"}
    ],
    "chartType": "xtable",
    "valueType": "number",
    "isRoundOff": true,
    "drillChart": "fsmTotalReqByTenant",
    "plotLabel": "District",
    "excludedColumns": ["ClosedWithInSla"],
    "computedFields": [
      {
        "postAggregationTheory" : "",
        "actionName": "PercentageComputedField",
        "fields" : ["ClosedReq", "TotalReq"],
        "newField" : "CompletionRateIn%",
        "_comments": "fields are field names picked from its aggregation query to use post aggregation newField value with given new field name  "
      },
      {
        "postAggregationTheory" : "",
        "actionName": "PercentageComputedField",
        "fields" : ["ClosedWithInSla","TotalReq"],
        "newField" : "SLAAchievedIn%",
        "_comments": "fields are field names picked from its aggregation query to use post aggregation newField value with given new field name  "
      }
    ],
     "chartSpecificProperty": {
     "XtableColumnOrder":[
     "S.N.",
     "District",
     "OpenReq",
     "ClosedReq",
     "TotalReq",
     "CompletionRateIn%",
     "SLAAchievedIn%",
     "TotalCollection"
     ]
     },
    "insight": {
    },
    "_comment": " "
  },
  "fsmTotalReqByTenant": {
    "chartName": "DSS_FSM_TOTAL_REQ_BY_ULB",
    "queries": [
      {
        "module": "FSM",
        "dateRefField": "Data.fsm.@timestamp",
        "requestQueryMap": "{\"wardId\" : \"Data.ward.name.keyword\", \"tenantId\" : \"Data.tenantData.code\" ,  \"district\" : \"Data.tenantData.city.districtName\"}",
        "indexName": "fsm",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.fsm.tenantId.keyword\":\"pb.testing\"}}]}},\"aggs\":{\"ULBs\":{\"terms\":{\"field\":\"Data.fsm.tenantId.keyword\",\"size\":1000},\"aggs\":{\"Open_Req\":{\"filter\":{\"bool\":{\"must_not\":[{\"terms\":{\"Data.fsm.applicationStatus.keyword\":[\"COMPLETED\",\"CITIZEN_FEEDBACK_PENDING\"]}}]}},\"aggs\":{\"OpenReq\":{\"value_count\":{\"field\":\"Data.fsm.tenantId.keyword\"}}}},\"Closed_Req\":{\"filter\":{\"bool\":{\"must\":[{\"terms\":{\"Data.fsm.applicationStatus.keyword\":[\"COMPLETED\",\"CITIZEN_FEEDBACK_PENDING\"]}}]}},\"aggs\":{\"ClosedReq\":{\"value_count\":{\"field\":\"Data.fsm.tenantId.keyword\"}}}},\"TotalReq\":{\"value_count\":{\"field\":\"Data.fsm.tenantId.keyword\"}},\"Closed_With_In_Sla\":{\"filter\":{\"bool\":{\"must\":[{\"terms\":{\"Data.fsm.applicationStatus.keyword\":[\"COMPLETED\",\"CITIZEN_FEEDBACK_PENDING\"]}},{\"script\":{\"script\":{\"source\":\"doc['Data.fsm.auditDetails.lastModifiedTime'].value - doc['Data.fsm.auditDetails.createdTime'].value < params.threshold\",\"lang\":\"painless\",\"params\":{\"threshold\":172800000}}}}]}},\"aggs\":{\"ClosedWithInSla\":{\"value_count\":{\"field\":\"Data.fsm.tenantId.keyword\"}}}},\"TotalCollection\":{\"sum\":{\"field\":\"Data.payments.paymentDetails.bill.billDetails.amountPaid\"}}}}}}}}"
      }
    ],
    "filterKeys": [
      {"key": "tenantId", "column": "ULB"}
    ],
    "chartType": "xtable",
    "valueType": "number",
    "isRoundOff": true,
    "drillChart": "fsmTotalReqByWard",
    "plotLabel": "ULB",
    "excludedColumns": ["ClosedWithInSla"],
    "computedFields": [
      {
        "postAggregationTheory" : "",
        "actionName": "PercentageComputedField",
        "fields" : ["ClosedReq", "TotalReq"],
        "newField" : "CompletionRateIn%",
        "_comments": "fields are field names picked from its aggregation query to use post aggregation newField value with given new field name  "
      },
      {
        "postAggregationTheory" : "",
        "actionName": "PercentageComputedField",
        "fields" : ["ClosedWithInSla","TotalReq"],
        "newField" : "SLAAchievedIn%",
        "_comments": "fields are field names picked from its aggregation query to use post aggregation newField value with given new field name  "
      }
    ],
    "chartSpecificProperty": {
     "XtableColumnOrder":[
     "S.N.",
     "ULB",
     "OpenReq",
     "ClosedReq",
     "TotalReq",
     "CompletionRateIn%",
     "SLAAchievedIn%",
     "TotalCollection"
     ]
     },
    "insight": {
    },
    "_comment": " "
  },
  "fsmTotalReqByWard": {
    "chartName": "DSS_FSM_TOTAL_REQ_BY_WARD",
    "queries": [
      {
        "module": "FSM",
        "dateRefField": "Data.fsm.@timestamp",
        "requestQueryMap": "{\"wardId\" : \"Data.ward.name.keyword\", \"tenantId\" : \"Data.tenantData.code\" ,  \"district\" : \"Data.tenantData.city.districtCode\"}",
        "indexName": "fsm",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.fsm.tenantId.keyword\":\"pb.testing\"}}]}},\"aggs\":{\"Ward\":{\"terms\":{\"field\":\"Data.ward.name.keyword\",\"size\":1000},\"aggs\":{\"Open_Req\":{\"filter\":{\"bool\":{\"must_not\":[{\"terms\":{\"Data.fsm.applicationStatus.keyword\":[\"COMPLETED\",\"CITIZEN_FEEDBACK_PENDING\"]}}]}},\"aggs\":{\"OpenReq\":{\"value_count\":{\"field\":\"Data.fsm.tenantId.keyword\"}}}},\"Closed_Req\":{\"filter\":{\"bool\":{\"must\":[{\"terms\":{\"Data.fsm.applicationStatus.keyword\":[\"COMPLETED\",\"CITIZEN_FEEDBACK_PENDING\"]}}]}},\"aggs\":{\"ClosedReq\":{\"value_count\":{\"field\":\"Data.fsm.tenantId.keyword\"}}}},\"TotalReq\":{\"value_count\":{\"field\":\"Data.fsm.tenantId.keyword\"}},\"Closed_With_In_Sla\":{\"filter\":{\"bool\":{\"must\":[{\"terms\":{\"Data.fsm.applicationStatus.keyword\":[\"COMPLETED\",\"CITIZEN_FEEDBACK_PENDING\"]}},{\"script\":{\"script\":{\"source\":\"doc['Data.fsm.auditDetails.lastModifiedTime'].value - doc['Data.fsm.auditDetails.createdTime'].value < params.threshold\",\"lang\":\"painless\",\"params\":{\"threshold\":172800000}}}}]}},\"aggs\":{\"ClosedWithInSla\":{\"value_count\":{\"field\":\"Data.fsm.tenantId.keyword\"}}}},\"TotalCollection\":{\"sum\":{\"field\":\"Data.payments.paymentDetails.bill.billDetails.amountPaid\"}}}}}}}}"
      }
    ],
    "filterKeys": [
      {"key": "wardId", "column": "Ward"},
      {"key": "ulbId", "column": "ULB"}
    ],
    "chartType": "xtable",
    "valueType": "number",
    "isRoundOff": true,
    "drillChart": "none",
    "action": "",
    "documentType": "_doc",
    "plotLabel": "Ward",
    "excludedColumns": ["ClosedWithInSla"],
    "computedFields": [
      {
        "postAggregationTheory" : "",
        "actionName": "PercentageComputedField",
        "fields" : ["ClosedReq", "TotalReq"],
        "newField" : "CompletionRateIn%",
        "_comments": "fields are field names picked from its aggregation query to use post aggregation newField value with given new field name  "
      },
      {
        "postAggregationTheory" : "",
        "actionName": "PercentageComputedField",
        "fields" : ["ClosedWithInSla","TotalReq"],
        "newField" : "SLAAchievedIn%",
        "_comments": "fields are field names picked from its aggregation query to use post aggregation newField value with given new field name  "
      }
    ],
     "chartSpecificProperty": {
     "XtableColumnOrder":[
     "S.N.",
     "Ward",
     "OpenReq",
     "ClosedReq",
     "TotalReq",
     "CompletionRateIn%",
     "SLAAchievedIn%",
     "TotalCollection"
     ]
     },
    "insight": {
    },
    "_comment": " "
  },
  "fsmVehicleLogReportByDDR": {
    "chartName": "DSS_FSM_VECHILE_LOG_REPORT",
    "queries": [
      {
        "module": "FSM",
        "dateRefField": "Data.vehicleTrip.@timestamp",
        "requestQueryMap": "{\"wardId\" : \"Data.ward.name.keyword\", \"tenantId\" : \"Data.tenantData.code\" ,  \"district\" : \"Data.tenantData.city.districtName\"}",
        "indexName": "vehicletrip",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"data.vehicleTrip.tenantId.keyword\":\"pb.testing\"}}]}},\"aggs\":{\"NoOfTrips\":{\"value_count\":{\"field\":\"Data.vehicleTrip.@timestamp\"}},\"TotalSeptageCollected\":{\"sum\":{\"script\":{\"source\":\"(doc['Data.vehicleTrip.tripDetails.volume'].value)/1000.0\"}}},\"TotalSeptageDumped\":{\"sum\":{\"script\":{\"source\":\"(doc['Data.vehicleTrip.volumeCarried'].value)/1000.0\"}}},\"CapacityUtilization\":{\"sum\":{\"script\":{\"source\":\"(doc['Data.vehicleTrip.volumeCarried'].value)/1000.0\"}}}}}}}"
      }
    ],
    "isMdmsEnabled": true,
    "filterKeys": [
      {"key": "tenantId", "column": "District"}
    ],
    "isPostResponseHandler": true,
    "chartType": "xtable",
    "valueType": "number",
    "action": "",
    "isRoundOff": true,
    "documentType": "_doc",
    "drillChart": "fsmVehicleLogReportByTenant",
    "plotLabel":"District",
    "aggregationPaths": [
      "NoOfTrips",
      "TotalSeptageCollected",
      "TotalSeptageDumped",
      "CapacityUtilization"
    ],
    "pathDataTypeMapping": [
      {
        "NoOfTrips" : "number"
      },
      {
        "TotalSeptageCollected" : "number"
      },
      {
        "TotalSeptageDumped" : "number"
      },
      {
        "CapacityUtilization" : "number"
      }
    ],
    "isCumulative": true,
    "interval": "month",
    "insight": {
    },
    "_comment": " "
  },
  "fsmVehicleLogReportByTenant": {
    "chartName": "DSS_FSM_VECHILE_LOG_REPORT",
    "queries": [
      {
        "module": "FSM",
        "dateRefField": "Data.vehicleTrip.@timestamp",
        "requestQueryMap": "{\"wardId\" : \"Data.ward.name.keyword\", \"tenantId\" : \"Data.tenantData.code\" ,  \"district\" : \"Data.tenantData.city.districtName\"}",
        "indexName": "vehicletrip",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"data.vehicleTrip.tenantId.keyword\":\"pb.testing\"}}]}},\"aggs\":{\"ULBs \":{\"terms\":{\"field\":\"Data.vehicleTrip.tenantId.keyword\",\"size\":1000},\"aggs\":{\"NoOfTrips\":{\"value_count\":{\"field\":\"Data.vehicleTrip.@timestamp\"}},\"TotalSeptageCollected\":{\"sum\":{\"script\":{\"source\":\"(doc['Data.vehicleTrip.tripDetails.volume'].value)/1000.0\"}}},\"TotalSeptageDumped\":{\"sum\":{\"script\":{\"source\":\"(doc['Data.vehicleTrip.volumeCarried'].value)/1000.0\"}}},\"CapacityUtilization\":{\"sum\":{\"script\":{\"source\":\"(doc['Data.vehicleTrip.volumeCarried'].value)/1000.0\"}}}}}}}}}"
      }
    ],
    "filterKeys": [
      {"key": "tenantId", "column": "Boundary"}
    ],
    "isPostResponseHandler": true,
    "chartType": "xtable",
    "valueType": "number",
    "action": "",
    "isRoundOff": true,
    "documentType": "_doc",
    "drillChart": "fsmVehicleLogReportByVehicleNo",
    "plotLabel":"Boundary",
    "aggregationPaths": [
      "NoOfTrips",
      "TotalSeptageCollected",
      "TotalSeptageDumped",
      "CapacityUtilization"
    ],
    "pathDataTypeMapping": [
      {
        "NoOfTrips" : "number"
      },
      {
        "TotalSeptageCollected" : "number"
      },
      {
        "TotalSeptageDumped" : "number"
      },
      {
        "CapacityUtilization" : "number"
      }
    ],
    "isCumulative": true,
    "interval": "month",
    "insight": {
    },
    "_comment": " "
  },
  "fsmVehicleLogReportByVehicleNo": {
    "chartName": "DSS_FSM_VECHILE_LOG_REPORT",
    "queries": [
      {
        "module": "FSM",
        "dateRefField": "Data.vehicleTrip.@timestamp",
        "requestQueryMap": "{\"wardId\" : \"Data.ward.name.keyword\", \"tenantId\" : \"Data.tenantData.code\" ,  \"district\" : \"Data.tenantData.city.districtCode\"}",
        "indexName": "vehicletrip",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"data.vehicleTrip.tenantId.keyword\":\"pb.testing\"}}]}},\"aggs\":{\"Vehicle Reg No\":{\"terms\":{\"field\":\"Data.vehicleTrip.vehicle.registrationNumber.keyword\",\"size\":1000},\"aggs\":{\"NoOfTrips\":{\"value_count\":{\"field\":\"Data.vehicleTrip.@timestamp\"}},\"TotalSeptageCollected\":{\"sum\":{\"script\":{\"source\":\"(doc['Data.vehicleTrip.tripDetails.volume'].value)/1000.0\"}}},\"TotalSeptageDumped\":{\"sum\":{\"script\":{\"source\":\"(doc['Data.vehicleTrip.volumeCarried'].value)/1000.0\"}}},\"CapacityUtilization\":{\"sum\":{\"script\":{\"source\":\"(doc['Data.vehicleTrip.volumeCarried'].value)/1000.0\"}}},\"TankCapacity\":{\"sum\":{\"script\":{\"source\":\"(doc['Data.vehicleTrip.vehicle.tankCapacity'].value)/1000.0\"}}}}}}}}}"
      }
    ],
    "filterKeys": [
      {"key": "registrationNumber", "column": "Vehicle_No"},
      {"key": "wardId", "column": "Ward"},
      {"key": "ulbId", "column": "ULB"}
    ],
    "isPostResponseHandler": true,
    "chartType": "xtable",
    "valueType": "number",
    "action": "",
    "isRoundOff": true,
    "documentType": "_doc",
    "drillChart": "none",
    "plotLabel":"Vehicle_No",
    "aggregationPaths": [
      "NoOfTrips",
      "TotalSeptageCollected",
      "TotalSeptageDumped",
      "CapacityUtilization",
      "TankCapacity"
    ],
    "pathDataTypeMapping": [
      {
        "NoOfTrips" : "number"
      },
      {
        "TotalSeptageCollected" : "number"
      },
      {
        "TotalSeptageDumped" : "number"
      },
      {
        "CapacityUtilization" : "number"
      },
      {
        "TankCapacity" : "number"
      }
    ],
    "isCumulative": true,
    "interval": "month",
    "insight": {
    },
    "_comment": " "
  }
```

[Click here to check the complete configuration](https://github.com/egovernments/configs/blob/qa/egov-dss-dashboards/dashboard-analytics/ChartApiConfig.json)

### **Master Dashboard Configuration**

Master Dashboard Configuration is the main configuration which defines as which are the Dashboards which are to be painted on screen.

It includes all the Visualizations, their groups, the charts which comes within them and even their dimensions as what should be their height and width.

```
{
      "name": "DSS_FSM_DASHBOARD",
      "id": "fsm",
      "isActive": "",
      "style": "linear",
      "visualizations": [
        {
          "row": 1,
          "name": "DSS_REVENUE",
          "vizArray": [
            {
              "id": 311,
              "name": "DSS_OVERVIEW",
              "dimensions": {
                "height": 450,
                "width": 4
              },
              "vizType": "metric-collection",
              "label": "DSS_OVERVIEW",
              "noUnit": true,
              "isCollapsible": false,
              "charts": [
                {
                  "id": "fsmTotalrequest",
                  "name": "DSS_FSM_TOTAL_REQUESTS",
                  "code": "",
                  "chartType": "metric",
                  "filter": "",
                  "headers": []
                },
                {
                  "id": "totalSludgeTreated",
                  "name": "DSS_FSM_TOTAL_SLUDGE_TREATED",
                  "code": "",
                  "chartType": "metric",
                  "filter": "",
                  "headers": []
                },
                {
                  "id": "avgFSMCostRequest",
                  "name": "DSS_FSM_AVG_FSM_COST_OR_REQ",
                  "code": "",
                  "chartType": "metric",
                  "filter": "",
                  "headers": []
                },
                {
                  "id": "totalCollectioninLacs",
                  "name": "DSS_FSM_TOTAL_COLLECTION",
                  "code": "",
                  "chartType": "metric",
                  "filter": "",
                  "headers": []
                },
                {
                  "id": "slaCompliance",
                  "name": "DSS_FSM_SLA_COMPLIANCE",
                  "code": "",
                  "chartType": "metric",
                  "filter": "",
                  "headers": []
                },
                {
                  "id": "citizenAvgRating",
                  "name": "DSS_FSM_CITIZEN_AVG_RATING",
                  "code": "",
                  "chartType": "metric",
                  "filter": "",
                  "headers": []
                }
              ]
            },
            {
              "id": 322,
              "name": "DSS_FSM_TOTAL_CUMULATIVE_COLLECTION",
              "dimensions": {
                "height": 450,
                "width": 6
              },
              "vizType": "chart",
              "label": "",
              "noUnit": true,
              "isCollapsible": false,
              "charts": [
                {
                  "id": "fsmTotalCumulativeCollection",
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
              "id": 321,
              "name": "DSS_FSM_TOP_ULB_BY_PERFORMANCE",
              "dimensions": {
                "height": 250,
                "width": 3
              },
              "vizType": "performing-metric",
              "label": "",
              "noUnit": false,
              "isCollapsible": false,
              "charts": [
                {
                  "id": "fsmTopUlbByPerformance",
                  "name": "Monthly",
                  "code": "",
                  "chartType": "bar",
                  "filter": "",
                  "headers": []
                }
              ]
            },
            {
              "id": 322,
              "name": "DSS_FSM_BOTTOM_ULB_BY_PERFORMANCE",
              "dimensions": {
                "height": 250,
                "width": 3
              },
              "vizType": "performing-metric",
              "label": "",
              "noUnit": false,
              "isCollapsible": false,
              "charts": [
                {
                  "id": "fsmBottomUlbByPerformance",
                  "name": "Monthly",
                  "code": "",
                  "chartType": "bar",
                  "filter": "",
                  "headers": []
                }
              ]
            },
            {
              "id": 323,
              "name": "DSS_FSM_COLLECTION_BY_USAGE_TYPE",
              "dimensions": {
                "height": 250,
                "width": 4
              },
              "vizType": "chart",
              "label": "",
              "noUnit": false,
              "isCollapsible": false,
              "charts": [
                {
                  "id": "fsmCollectionByUsageType",
                  "name": "DSS_FSM_COLLECTION_BY_USAGE_TYPE",
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
          "row": 3,
          "name": "DSS_REVENUE",
          "vizArray": [
            {
              "id": 325,
              "name": "DSS_FSTP_CAPACITY_UTILIZATION",
              "dimensions": {
                "height": 450,
                "width": 5
              },
              "vizType": "chart",
              "label": "",
              "noUnit": true,
              "isCollapsible": false,
              "charts": [
                {
                  "id": "fsmCapacityUtilization",
                  "name": "Monthly",
                  "code": "",
                  "chartType": "line",
                  "filter": "",
                  "headers": []
                }
              ]
            },
            {
              "id": 326,
              "name": "DSS_FSM_MONTHLY_WASTE_CAL",
              "dimensions": {
                "height": 450,
                "width": 5
              },
              "vizType": "chart",
              "label": "",
              "noUnit": true,
              "isCollapsible": false,
              "charts": [
                {
                  "id": "fsmMonthlyWasteCal",
                  "name": "Monthly",
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
          "row": 4,
          "name": "DSS_REVENUE",
          "vizArray": [
            {
              "id": 327,
              "name": "DSS_FSM_TOP_DSO_BY_PERFORMANCE",
              "dimensions": {
                "height": 450,
                "width": 5
              },
              "vizType": "chart",
              "label": "",
              "noUnit": true,
              "isCollapsible": false,
              "charts": [
                {
                  "id": "fsmTopDsoByPerformance",
                  "name": "Monthly",
                  "code": "",
                  "chartType": "horizontalBar",
                  "filter": "",
                  "headers": []
                }
              ]
            },
            {
              "id": 329,
              "name": "DSS_FSM_BOTTOM_DSO_BY_PERFORMANCE",
              "dimensions": {
                "height": 450,
                "width": 5
              },
              "vizType": "chart",
              "label": "",
              "noUnit": true,
              "isCollapsible": false,
              "charts": [
                {
                  "id": "fsmBottomDsoByPerformance",
                  "name": "Monthly",
                  "code": "",
                  "chartType": "horizontalBar",
                  "filter": "",
                  "headers": []
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
              "id": 339,
              "name": "DSS_FSM_TOTAL_REQ_BY_DISTRICT",
              "dimensions": {
                "height": 350,
                "width": 10
              },
              "vizType": "chart",
              "label": "",
              "noUnit": false,
              "isCollapsible": true,
              "charts": [
                {
                  "id": "fsmTotalReqByDistrict",
                  "name": "DSS_FSM_TOTAL_REQ_BY_DISTRICT",
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
          "row": 6,
          "name": "DSS_REVENUE",
          "vizArray": [
            {
              "id": 331,
              "name": "DSS_FSM_VECHILE_LOG_REPORT",
              "dimensions": {
                "height": 350,
                "width": 10
              },
              "vizType": "chart",
              "label": "",
              "noUnit": false,
              "isCollapsible": true,
              "charts": [
                {
                  "id": "fsmVehicleLogReportByDDR",
                  "name": "DSS_FSM_VECHILE_LOG_REPORT",
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
    },
```

[Click here for the complete configuration](https://github.com/egovernments/configs/blob/qa/egov-dss-dashboards/dashboard-analytics/MasterDashboardConfig.json)

### **Role Dashboard Mappings Configuration**

Master Dashboard Configuration which was explained earlier hold the list of Dashboards which are available.

Given the instance where Role Action Mapping is not maintained in the Application Service, this configuration will act as Role - Dashboard Mapping Configuration

In this, each Role is mapped against the Dashboard which they are authorized to see

This was used earlier when the Role Action Mapping of eGov was not integrated.

Later, when the Role Action Mapping started controlling the Dashboards to be seen on the client side, this configuration was just used to enable the Dashboards for viewing.

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
          "name": "Facial Sludge Management",
          "id": "fsm"
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
          "id": "ulb-fsm"
        }
      ]
    }

  ]
}
```

[Click here to check the configuration](https://github.com/egovernments/configs/blob/qa/egov-dss-dashboards/dashboard-analytics/RoleDashboardMappingsConf.json)

### **MDMS Configuration to be added**

_common-masters/uiCommonConstants.json_

```
"fsm":{
                 "routePath":"/dashboard/fsm",
                 "isOrigin":true
              },
              "ulb-fsm":{
                 "routePath":"/dashboard/ulb-fsm",
                 "isOrigin":true
              }
```

[Click here to check the complete configuration](https://github.com/egovernments/egov-mdms-data/blob/QA/data/pb/common-masters/uiCommonConstants.json)

roleaction.json

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

Action test.json:

```
{
      "id": {{PlaceHolder1}},
      "name": "DSS Dashboard Config Facial Sludge Management",
      "url": "/dashboard-analytics/dashboard/getDashboardConfig/fsm",
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
      "name": "DSS Dashboard Charts",
      "url": "/dashboard-analytics/dashboard/getChartV2",
      "parentModule": "",
      "displayName": "DSS",
      "orderNumber": 0,
      "enabled": false,
      "serviceCode": "DSS",
      "code": "null",
      "path": ""
    },
    
```

[Click here to check the complete configuration](https://github.com/egovernments/egov-mdms-data/blob/QA/data/pb/ACCESSCONTROL-ACTIONS-TEST/actions-test.json)

FSM-DSS Consists of multiple graphs which represent the data of FSM. Each graph has its own configuration which will describe the chart and its type.

DSS Consists of following charts in FSM:

* Overview
* Total Cumulative Collection
* Top ULB By Performance
* Bottom ULB by Performance
* FSM Collection by Usage Type
* FSTP - Capacity Utilization
* Monthly Septage Collected
* Top DSO By Performance
* Bottom DSO By Performance
* Desludging Request Report
* Vehicle Log Report

## **Overview**

Overview graph contains multiple data information as below in the selected time period.

* **Total Requests :** Which represents the no of FSM applications count.
* **Total Sludge Treated :** This represents the total sludge dumped at the yard in KL.
* **Average FSM Cost :** This represents the average collection amount for the FSM applications.
* **Total Collection :** This represents the total collection amount for the FSM applications.
* **SLA Compliance :** This represents the total SLA achieved in percentage.
* **Average Citizen Rating :** This represents the Citizen Average Rating value.

![](<../../../../.gitbook/assets/image (274).png>)

![](blob:https://digit-discuss.atlassian.net/3d62049a-19f1-462c-b6b5-4a2eaadfa344#media-blob-url=true\&id=89036142-2f32-4b35-8e01-0ca866821419\&collection=contentId-1821016076\&contextId=1821016076\&mimeType=image%2Fpng\&name=image-20210730-103733.png\&size=30411\&width=457\&height=546)

## **Total Cumulative Collection**

This Graph contains the collection amount information in the monthly base as a cumulative line graph. This will change as per the denomination amount filter selection.

**line** - this graph/chart is data representation on date histograms or date groupings.![](blob:https://digit-discuss.atlassian.net/a94232b7-556f-44ac-8ab9-a81ba1207dd5#media-blob-url=true\&id=1ea67496-c39f-4bb0-a93f-8ff914975afe\&collection=contentId-1821016076\&contextId=1821016076\&mimeType=image%2Fpng\&name=image-20210730-105012.png\&size=39544\&width=932\&height=450)

![](<../../../../.gitbook/assets/image (292).png>)

## **Top ULB By Performance**

This graph represents the ULB’s based on the sla achieved in bar chart representation with the % of sla achieved in ascending order. Also this chart contains the drill down to give the complete information regarding each ULB.

**drillChart :** If there is a drill down on the visualization, then the code of the Drill Down Visualization is added here. This will be used by Client Service to manage drill downs.

![](<../../../../.gitbook/assets/image (304).png>)

This chart consists of drill down so we gave the drill down chart key as reference in this chart as in the above picture.

Here is the drill down chart config params.

**Table chart Sample:** This chart comes with 2 kinds, table and xtable.

table type allows aggregated fields added as available in the query keys, hence to extract the values based on the key, **aggegationPaths** needs to add along with their data type as in **pathDataTypeMapping**.

![](<../../../../.gitbook/assets/image (295).png>)

### **Bottom ULB by Performance** <a href="#bottom-ulb-by-performance" id="bottom-ulb-by-performance"></a>

This graph represents the ULB’s based on the sla achieved in bar chart representation with the % of sla achieved in descending order. Also this chart contains the drill down to give the complete information regarding each ULB.![](blob:https://digit-discuss.atlassian.net/dd364c4c-2d03-4f43-aedf-cf4f29996ae9#media-blob-url=true\&id=8e1ca71b-593e-4a91-8553-fd2dcb125bc3\&collection=contentId-1821016076\&contextId=1821016076\&mimeType=image%2Fpng\&name=image-20210730-105307.png\&size=22133\&width=472\&height=454)

![](<../../../../.gitbook/assets/image (286).png>)

On click of show more You will navigate to tabular chart of bottom ULB by performance.

![](<../../../../.gitbook/assets/image (289).png>)

### **FSM Collection by Usage Type** <a href="#fsm-collection-by-usage-type" id="fsm-collection-by-usage-type"></a>

This graph shows the collection amount based on the usage/property type and this amount will change as per the denomination filter change and this also shows the % of the top 4 properties, remaining properties will go under others category.

![](<../../../../.gitbook/assets/image (294).png>)

### **FSTP - Capacity Utilization** <a href="#fstp-capacity-utilization" id="fstp-capacity-utilization"></a>

This graph is in the line chart representation and shows the data in cumulative format, and it contains the information about the waste collecting plant capacity utilization in % and also shows the total waste dumped at plant in KL at the top of the graph.

![](blob:https://digit-discuss.atlassian.net/04cde148-bed4-4019-be7b-24dad4370a9e#media-blob-url=true\&id=5f0dcd41-c868-4248-96d8-2cb818bb771e\&collection=contentId-1821016076\&contextId=1821016076\&mimeType=image%2Fpng\&name=image-20210730-110151.png\&size=32932\&width=690\&height=423)

![](<../../../../.gitbook/assets/image (297).png>)

### **Monthly Septage Collected** <a href="#monthly-septage-collected" id="monthly-septage-collected"></a>

This graph shows the data in horizontal bar representation and bars contain data in monthly wide and non cumulative data. This graph contains the monthly information of septage collected and dumped at the plant in KL.\
![](blob:https://digit-discuss.atlassian.net/110a5513-a7c4-43ed-9a4b-321ff97536c3#media-blob-url=true\&id=e3468cb8-aa5e-40f4-b825-d66f9cc1e5bc\&collection=contentId-1821016076\&contextId=1821016076\&mimeType=image%2Fpng\&name=image-20210730-110226.png\&size=24501\&width=715\&height=427)

![](<../../../../.gitbook/assets/image (276).png>)

### **Top DSO By Performance** <a href="#top-dso-by-performance" id="top-dso-by-performance"></a>

This graph represents the DSO’s based on the no of dso requests and based on sla achievement in bar chart representation in ascending order. Also, this chart contains the drill down to give the complete information regarding each DSO.\
![](blob:https://digit-discuss.atlassian.net/95ba92f9-c85a-4a87-966e-296e2012d863#media-blob-url=true\&id=b9e5c08c-2f3c-4471-9498-598106f1e728\&collection=contentId-1821016076\&contextId=1821016076\&mimeType=image%2Fpng\&name=image-20210730-111554.png\&size=24951\&width=702\&height=431)

![](<../../../../.gitbook/assets/image (301).png>)

On click of show more we can see the details of the available DSO’s under the selected ULB.![](blob:https://digit-discuss.atlassian.net/830242f7-689b-48ae-b39a-bb9c45196ef1#media-blob-url=true\&id=107112c5-9b71-46cb-8c36-20b97f05f209\&collection=contentId-1821016076\&contextId=1821016076\&mimeType=image%2Fpng\&name=image-20210730-111852.png\&size=52942\&width=1424\&height=570)

![](<../../../../.gitbook/assets/image (287).png>)

### **Bottom DSO By Performance** <a href="#bottom-dso-by-performance" id="bottom-dso-by-performance"></a>

This graph represents the DSO’s based on the no of dso requests and based on sla achievement in bar chart representation in descending order. Also this chart contains the drill down to give the complete information regarding each DSO.

This is the bottom DSO drill down chart which represents the table chart type.

![](<../../../../.gitbook/assets/image (296).png>)

On click of show more we can see the details of the available DSO’s under the selected ULB.

![](<../../../../.gitbook/assets/image (282).png>)

### **Desludging Request Report** <a href="#desludging-request-report" id="desludging-request-report"></a>

This tabular chart representation graph shows multiple FSM information like no of open application requests, closed requests, total requests, completion rate in %, sla achieved in % and total collection amount. And this table shows the data in district level and also has the drill down chart for each district to ulb and from ulb to ward level data for the same.

_**xtable**_ type allows to add multiple computed fields with the aggregated fields dynamically added.

To add multiple computed columns, **computedFields** \[] where actionName (IComputedField\<T> interface), fields \[] names as in exist in query key, newField as name to appear for computation must be defined.

**chartSpecificProperty** : This is specific to FSM-DSS, and it is used to achieve the xtable column order along with the computed fields. This property is not used in any other modules till now.

![](<../../../../.gitbook/assets/image (275).png>)

On click of any district name will enter into drill down charts, which will represents that specific District data.

![](<../../../../.gitbook/assets/image (288).png>)

On click of the ULB will navigate to wards under that specific ULB and each ward shows the specific data regarding that ward.

![](<../../../../.gitbook/assets/image (290).png>)

### **Vehicle Log Report** <a href="#vehicle-log-report" id="vehicle-log-report"></a>

This table shows data data of vehicle trips which have no of trips, Total septage collected, total septage dumped and capacity utilization in %. This graph also contains the drills downs from district to ULB and from ULB to vehicle level, which shows the vehicle no.

![](<../../../../.gitbook/assets/image (303).png>)

On click of any district name will enter into drill down charts, which will represents that specific District data.

![](<../../../../.gitbook/assets/image (281).png>)

On click of any boundary/ ULB we will navigate to specific vehicle details which will be as below.

![](<../../../../.gitbook/assets/image (278).png>)

#### **Newly Introduced Property** <a href="#newly-introduced-property" id="newly-introduced-property"></a>

**isRoundOff**: This property is introduced to round off the decimal values. Ex: if the value is 25.43 by using isRoundOff property in configuration we will get it as 25. if value is 22.56 round of value will be 23.\
This can be used for insights configuration as well for overview graph.

#### Common Properties available <a href="#common-properties-available" id="common-properties-available"></a>

**Key(eg: fsmTotalrequest) :** This is the Visualization Code. This key will be referred to in further visualization configurations.

This is the key which will be used by the client application to indicate which visualization is needed for display.

**chartName :** The name of the Chart which has to be used as a label on the Dashboard. The name of the Chart will be a detailed name.

In this configuration, the Name of the Chart will be the code of Localization which will be used by Client Side.

**queries :** Some visualizations are derived from a specific data source. While some others are derived from different data sources and are combined together to get a meaningful representation.

The queries of aggregation which are to be used to fetch out the right data in the right aggregated format are configured here.

**queries.module :** The module / domain level, on which the query should be applied on. Facial Sludge Management is fsm.

**queries.indexName :** The name of the index upon which the query has to be executed is configured here.

**queries.aggrQuery :** The aggregation query in itself is added here. Based on the Module and the Index name specified, this query is attached to the filter part of the complete search request and then executed against that index

**queries.requestQueryMap :** Client Request would carry certain fields which are to be filtered. The parameters specified in the Client Request are different from the parameters in each of these indexed documents.

In order to map the parameters of the request to the parameters of the ElasticSearch Document, this mapping is maintained.

**queries.dateRefField :** Each of these modules have separate indexes. And all of them have their own date fields.

When there is a date filter applied against these visualizations, each of them has to apply it against their own date reference fields.

In order to maintain what is the date field in which index, we have this configured in this configuration parameter.

**chartType :** As there are different types of visualizations, this field defines what is the type of chart / visualization that this data should be used to represent.

**Chart types available are**:

**metric** - this represents the aggregated amount/value for records filter by the aggregate es query

**pie** - this represents the aggregated data on grouping. This is can be used to represent any line graph, bar graph, pie chart or donuts

**line** - this graph/chart is data representation on date histograms or date groupings

**perform** - this chart represents groping data as performance wise.

**table** - represents a form of plots and value with headers as grouped on and list of its key, values pairs.

**xtable -** represents a advanced feature of table, it has addition capabilities for dynamic adding header values.

**valueType :** In any case of data, the values which are sent to plot, might be a percentage, sometimes an amount and sometimes it is just a count.

In order to represent them and differentiate the numbers from amount from percentage, this field is used to indicate the type of value that this Visualization will be sending.

**action :** Some of the visualizations are not just aggregation on data source. There might be some cases where we have to do a post aggregation computation.

For Example, in the case of Top 3 Performing ULBs, the Target and Total Collection is obtained and then the percentage is calculated. In these kinds of cases, what is the action that has to be performed on that data obtained is defined in this parameter.

**documentType :** The type of document upon which the query has to be executed is defined here.

**drillChart :** If there is a drill down on the visualization, then the code of the Drill Down Visualization is added here. This will be used by Client Service to manage drill downs.

**aggregationPaths :** All the queries will be having Aggregation names in it. In order to fetch the value out of each Aggregation Responses, the name of the aggregation in the query will be an easy bet. These aggregation paths will have the names of Aggregation in it.

**insights :** It is to show the data with the comparison of last year with arrow symbols, it will show the data in how much % is increased or decreased.

**\_comment :** In order to display information on the “i” symbol of each visualization, Visualization Information is maintained in this field.

**Postman collection for fsm-dss:** [https://www.getpostman.com/collections/119ee90dd54c04617c3a](https://www.getpostman.com/collections/119ee90dd54c04617c3a)
