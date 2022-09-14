---
description: Technical Doc
---

# National Dashboard - Overview

## **Overview**

The Overview page is an aggregation of multiple services like property tax, trade license, water and sewerage, fire noc, obps, mcollect etc. NDSS has two sides to it. One is the process in which the data is pooled to ElasticSearch and the other is the way it is fetched, aggregated, computed, transformed and sent across.

As this revolves around various data sets, there is a need to make this configurable. This ensures that the process can be configured easily in case a new scenario is introduced.&#x20;

This document walks us through the steps on how to define the configurations for the Analytics of NDSS for the Overview page.

## **Technical Details**

**Analytics :** Microservice responsible for building, fetching, aggregating and computing the data on ElasticSearch into a consumable data response. This is essentially used for visualizations and graphical representations.&#x20;

**Analytics Configurations:** Analytics contains multiple configurations. We need to add the changes related to National-Dashboard in this dashboard-analytics.\
Configuration file path: [<img src="https://github.com/fluidicon.png" alt="" data-size="line">configs/egov-dss-dashboards/dashboard-analytics at qa · egovernments/configs](https://github.com/egovernments/configs/tree/qa/egov-dss-dashboards/dashboard-analytics)\
Below is a list of configurations that need to be changed to run National-Dashboard successfully.

1. Chart API Configuration
2. Master Dashboard Configuration
3. Role Dashboard Mappings Configuration

**Chart API Configuration -** Each Visualization has its own properties. Each Visualization comes from different data sources (Sometimes it is a combination of different data sources).&#x20;

In order to configure each visualization and their properties, we have a Chart API Configuration Document. In this, Visualization Code, which happens to be the key, will be having its properties configured as a part of configuration and are easily changeable.

Here is the sample ChartApiConfiguration.json data for the Overview Page.

```
"_comment" : "NSS-OVERVIEW",
    
	"todaysCollectionOverview": {
    "chartName": "NATIONAL_DSS_TODAYS_COLLECTION",
    "queries": [
      {
        "module": "PT",
        "dateRefField": "date",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "indexName": "pt-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"todaysDate\":{\"terms\":{\"field\":\"date\",\"order\":{\"_term\":\"desc\"},\"size\":1},\"aggs\":{\"Todays Collection\":{\"sum\":{\"field\":\"todaysCollectionForUsageCategory\"}}}},\"lastUpdatedTime\":{\"terms\":{\"field\":\"lastModifiedTime\",\"order\":{\"_term\":\"desc\"},\"size\":1}}}}}}"
      },
      {
        "module": "TL",
        "dateRefField": "date",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "indexName": "tl-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"todaysDate\":{\"terms\":{\"field\":\"date\",\"order\":{\"_term\":\"desc\"},\"size\":1},\"aggs\":{\"Todays Collection\":{\"sum\":{\"field\":\"todaysCollectionForTradeType\"}}}},\"lastUpdatedTime\":{\"terms\":{\"field\":\"lastModifiedTime\",\"order\":{\"_term\":\"desc\"},\"size\":1}}}}}}"
      },
       {
        "module": "W&S",
        "indexName": "ws-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"todaysDate\":{\"terms\":{\"field\":\"date\",\"order\":{\"_term\":\"desc\"},\"size\":1},\"aggs\":{\"Todays Collection\":{\"sum\":{\"field\":\"todaysCollectionForPaymentChannelType\"}}}},\"lastUpdatedTime\":{\"terms\":{\"field\":\"lastModifiedTime\",\"order\":{\"_term\":\"desc\"},\"size\":1}}}}}}",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "dateRefField": "date"
      },
      {
        "module": "OBPS",
        "dateRefField": "date",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "indexName": "obps-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"todaysDate\":{\"terms\":{\"field\":\"date\",\"order\":{\"_term\":\"desc\"},\"size\":1},\"aggs\":{\"Todays Collection\":{\"sum\":{\"field\":\"todaysCollectionForPaymentMode\"}}}},\"lastUpdatedTime\":{\"terms\":{\"field\":\"lastModifiedTime\",\"order\":{\"_term\":\"desc\"},\"size\":1}}}}}}"
      },
      {
        "module": "FIRENOC",
        "dateRefField": "date",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "indexName": "firenoc-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"todaysDate\":{\"terms\":{\"field\":\"date\",\"order\":{\"_term\":\"desc\"},\"size\":1},\"aggs\":{\"Todays Collection\":{\"sum\":{\"field\":\"todaysCollectionForPaymentMode\"}}}},\"lastUpdatedTime\":{\"terms\":{\"field\":\"lastModifiedTime\",\"order\":{\"_term\":\"desc\"},\"size\":1}}}}}}"
      },
      {
        "module": "MC",
        "dateRefField": "date",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "indexName": "mcollect-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"todaysDate\":{\"terms\":{\"field\":\"date\",\"order\":{\"_term\":\"desc\"},\"size\":1},\"aggs\":{\"Todays Collection\":{\"sum\":{\"field\":\"todaysCollectionForPaymentMode\"}}}},\"lastUpdatedTime\":{\"terms\":{\"field\":\"lastModifiedTime\",\"order\":{\"_term\":\"desc\"},\"size\":1}}}}}}"
      }
    ],
    "chartType": "metric",
    "valueType": "Amount",
    "drillChart": "none",
    "documentType": "_doc",
    "action": "",
    "TodaysCollection":true,
    "aggregationPaths": [
      "Todays Collection"
    ],
    "insight": {
      "chartResponseMap" : "todaysCollectionOverview",
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
  
	"totalCollectionOverview": {
    "chartName": "NATIONAL_DSS_TOTAL_COLLECTION",
    "queries": [
      {
        "module": "PT",
        "dateRefField": "date",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "indexName": "pt-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"Total Collection\":{\"sum\":{\"field\":\"todaysCollectionForUsageCategory\"}}}}}}"
      },
      {
        "module": "TL",
        "dateRefField": "date",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "indexName": "tl-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"Total Collection\":{\"sum\":{\"field\":\"todaysCollectionForTradeType\"}}}}}}"
      },
      {
        "module": "OBPS",
        "dateRefField": "date",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "indexName": "obps-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"Total Collection\":{\"sum\":{\"field\":\"todaysCollectionForPaymentMode\"}}}}}}"
      },
      {
        "module": "FIRENOC",
        "dateRefField": "date",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "indexName": "firenoc-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"Total Collection\":{\"sum\":{\"field\":\"todaysCollectionForPaymentMode\"}}}}}}"
      },
      {
        "module": "MC",
        "dateRefField": "date",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "indexName": "mcollect-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"Total Collection\":{\"sum\":{\"field\":\"todaysCollectionForPaymentMode\"}}}}}}"
      },
      {
        "module": "W&S",
        "dateRefField": "date",
        "requestQueryMap": "{\"ulb\" : \"ulb.keyword\",\"ward\" : \"ward.keyword\"}",
        "indexName": "ws-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"Total Collection\":{\"sum\":{\"field\":\"todaysCollectionForPaymentChannelType\"}}}}}}"
    }
      
    ],
    "chartType": "metric",
    "valueType": "Amount",
    "drillChart": "none",
    "documentType": "_doc",
    "action": "",
    "aggregationPaths": [
      "Total Collection"
    ],
    "insight": {
      "chartResponseMap" : "totalCollectionOverview",
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
  
  	"targetCollectionvOverview": {
    "chartName": "NATIONAL_DSS_TARGET_COLLECTION",
    "queries": [
      {
        "module": "MASTER",
        "requestQueryMap": "{\"module\" : \"module.keyword\", \"ulb\" : \"ulb.keyword\"}",
        "dateRefField": "date",
        "indexName": "master-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"Target Collection\":{\"sum\":{\"field\":\"budgetProposedForMunicipalCorporation\"}}}}}}"
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
    "isDayUnit": true,
    "postAggregationTheory" : "repsonseToDifferenceOfDates",
    "insight": {
      "chartResponseMap" : "targetCollectionvOverview",
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
  	
  	"targetAchievedOverview": {
    "chartName": "NATIONAL_DSS_TARGET_ACHIEVED",
    "queries": [
      {
        "module": "MASTER",
        "requestQueryMap": "{\"state\" : \"state.keyword\", \"module\" : \"module.keyword\", \"ulb\" : \"ulb.keyword\"}",
        "dateRefField": "date",
        "indexName": "master-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"Actual collection\":{\"sum\":{\"field\":\"budgetProposedForMunicipalCorporation\"}}}}}}"
      },
      {
        "module": "PT",
        "dateRefField": "date",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "indexName": "pt-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"Total Collection\":{\"sum\":{\"field\":\"todaysCollectionForUsageCategory\"}}}}}}"
      },
      {
        "module": "TL",
        "dateRefField": "date",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "indexName": "tl-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"Total Collection\":{\"sum\":{\"field\":\"todaysCollectionForTradeType\"}}}}}}"
      },
      {
        "module": "OBPS",
        "dateRefField": "date",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "indexName": "obps-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"Total Collection\":{\"sum\":{\"field\":\"todaysCollectionForPaymentMode\"}}}}}}"
      },
      {
        "module": "FIRENOC",
        "dateRefField": "date",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "indexName": "firenoc-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"Total Collection\":{\"sum\":{\"field\":\"todaysCollectionForPaymentMode\"}}}}}}"
      },
      {
        "module": "MC",
        "dateRefField": "date",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "indexName": "mcollect-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"Total Collection\":{\"sum\":{\"field\":\"todaysCollectionForPaymentMode\"}}}}}}"
      },
      {
        "module": "W&S",
        "dateRefField": "date",
        "requestQueryMap": "{\"ulb\" : \"ulb.keyword\",\"ward\" : \"ward.keyword\"}",
        "indexName": "ws-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"Total Collection\":{\"sum\":{\"field\":\"todaysCollectionForPaymentChannelType\"}}}}}}"
    }     

    ],
    "chartType": "metric",
    "valueType": "percentage",
    "drillChart": "none",
    "documentType": "_doc",
    "action": "percentage",
    "preActionTheory":{
      "Actual collection":"repsonseToDifferenceOfDates"
    },
    "isRoundOff": true,
    "aggregationPaths": [
      "Total Collection",
      "Actual collection"
    ],
    "insight": {
      "chartResponseMap" : "targetAchievedOverview",
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
  	
 	"cumulativeCollectionOverview": {
    "chartName": "NATIONAL_DSS_TOTAL_CUMULATIVE_COLLECTION",
    "queries": [
      {
        "module": "PT",
        "dateRefField": "date",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "indexName": "pt-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"Collections\":{\"date_histogram\":{\"field\":\"date\",\"interval\":\"intervalvalue\"},\"aggs\":{\"Sum\":{\"sum\":{\"field\":\"todaysCollectionForUsageCategory\"}}}}}}}}"
      },
      {
        "module": "TL",
        "dateRefField": "date",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "indexName": "tl-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"Collections\":{\"date_histogram\":{\"field\":\"date\",\"interval\":\"intervalvalue\"},\"aggs\":{\"Sum\":{\"sum\":{\"field\":\"todaysCollectionForTradeType\"}}}}}}}}"
      },
      {
        "module": "WS",
        "dateRefField": "date",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\",\"ward\" : \"ward.keyword\"}",
        "indexName": "ws-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"Collections\":{\"date_histogram\":{\"field\":\"date\",\"interval\":\"intervalvalue\"},\"aggs\":{\"Water\":{\"filter\":{\"bool\":{}},\"aggs\":{\"Sum\":{\"sum\":{\"field\":\"todaysCollectionForConnectionType\"}}}}}}}}}}"
      },
      {
        "module": "OBPS",
        "dateRefField": "date",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "indexName": "obps-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"Collections\":{\"date_histogram\":{\"field\":\"date\",\"interval\":\"intervalvalue\"},\"aggs\":{\"Sum\":{\"sum\":{\"field\":\"todaysCollectionForPaymentMode\"}}}}}}}}"
      },
      {
        "module": "FIRENOC",
        "dateRefField": "date",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "indexName": "firenoc-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"Collections\":{\"date_histogram\":{\"field\":\"date\",\"interval\":\"intervalvalue\"},\"aggs\":{\"Sum\":{\"sum\":{\"field\":\"todaysCollectionForPaymentMode\"}}}}}}}}"
      },
      {
        "module": "MC",
        "dateRefField": "date",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "indexName": "mcollect-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"Collections\":{\"date_histogram\":{\"field\":\"date\",\"interval\":\"intervalvalue\"},\"aggs\":{\"Sum\":{\"sum\":{\"field\":\"todaysCollectionForPaymentMode\"}}}}}}}}"
      }
    ],
    "chartType": "line",
    "valueType": "amount",
    "action": "",
    "drillChart": "none",
    "documentType": "_doc",
    "aggregationPaths": [
      "Collections"
    ],
    "isCumulative": true,
    "interval": "month",
    "insight": {
    },
    "_comment": " "
  },
 	
 	"topPerformingStatesOverview": {
    "chartName": "NATIONAL_DSS_TOP_3_PERFORMING_STATES_TARGET_ACHIEVEMENT",
    "queries": [
      {
        "module": "MASTER",
        "requestQueryMap": "{\"state\" : \"state.keyword\", \"module\" : \"module.keyword\", \"ulb\" : \"ulb.keyword\"}",
        "dateRefField": "date",
        "indexName": "master-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"Target Collection\":{\"terms\":{\"field\":\"state.keyword\",\"size\":\"200\",\"order\":{\"Sum\":\"desc\"}},\"aggs\":{\"Sum\":{\"sum\":{\"field\":\"budgetProposedForMunicipalCorporation\"}}}}}}}}"
      },
      {
        "module": "PT",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "dateRefField": "date",
        "indexName": "pt-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"Total Collection\":{\"terms\":{\"field\":\"state.keyword\",\"size\":\"200\",\"order\":{\"Sum\":\"desc\"}},\"aggs\":{\"Sum\":{\"sum\":{\"field\":\"todaysCollectionForUsageCategory\"}}}}}}}}"
      },
      {
        "module": "TL",
        "dateRefField": "date",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "indexName": "tl-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[]}},\"aggs\":{\"Total Collection\":{\"terms\":{\"field\":\"state.keyword\",\"order\":{\"Sum\":\"desc\"}},\"aggs\":{\"Sum\":{\"sum\":{\"field\":\"todaysCollectionForTradeType\"}}}}}}}}"
      },
       {
        "module": "WS",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "dateRefField": "date",
        "indexName": "ws-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"Total Collection\":{\"terms\":{\"field\":\"state.keyword\",\"size\":\"200\",\"order\":{\"Sum\":\"desc\"}},\"aggs\":{\"Sum\":{\"sum\":{\"field\":\"todaysCollectionForPaymentChannelType\"}}}}}}}}"
      }
    ],
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
    "insight": {
    },
    "_comment": " Top Performing States for target achieved"
  },
   
   	"bottomPerformingStatesOverview": {
    "chartName": "NATIONAL_DSS_BOTTOM_3_PERFORMING_STATES_TARGET_ACHIEVEMENT",
    "queries": [
       {
        "module": "MASTER",
        "requestQueryMap": "{\"state\" : \"state.keyword\", \"module\" : \"module.keyword\", \"ulb\" : \"ulb.keyword\"}",
        "dateRefField": "date",
        "indexName": "master-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"Target Collection\":{\"terms\":{\"field\":\"state.keyword\",\"size\":\"200\",\"order\":{\"Sum\":\"asc\"}},\"aggs\":{\"Sum\":{\"sum\":{\"field\":\"budgetProposedForMunicipalCorporation\"}}}}}}"
      },
      {
        "module": "PT",
       "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "dateRefField": "date",
        "indexName": "pt-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"Total Collection\":{\"terms\":{\"field\":\"state.keyword\",\"size\":\"200\",\"order\":{\"Sum\":\"asc\"}},\"aggs\":{\"Sum\":{\"sum\":{\"field\":\"todaysCollectionForUsageCategory\"}}}}}}}}"
      },
      {
        "module": "TL",
        "dateRefField": "date",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "indexName": "tl-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[]}},\"aggs\":{\"Total Collection\":{\"terms\":{\"field\":\"state.keyword\",\"order\":{\"Sum\":\"asc\"}},\"aggs\":{\"Sum\":{\"sum\":{\"field\":\"todaysCollectionForTradeType\"}}}}}}}}"
      },
      {
        "module": "WS",
       "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "dateRefField": "date",
        "indexName": "ws-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"Total Collection\":{\"terms\":{\"field\":\"state.keyword\",\"size\":\"200\",\"order\":{\"Sum\":\"asc\"}},\"aggs\":{\"Sum\":{\"sum\":{\"field\":\"todaysCollectionForPaymentChannelType\"}}}}}}}}"
      }
    ],
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
    "insight": {
    },
    "_comment": " Bottom Performing States for target achieved"
  },
  
   	"totalCollectionServiceWiseOverview": {
    "chartName": "NATIONAL_DSS_TOTAL_CUMULATIVE_COLLECTION_SERVICE_WISE",
    "queries": [
      {
        "module": "PT",
        "dateRefField": "date",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "indexName": "pt-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"PT\":{\"sum\":{\"field\":\"todaysCollectionForUsageCategory\"}}}}}}"
      },
      {
        "module": "TL",
        "dateRefField": "date",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "indexName": "tl-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"TL\":{\"sum\":{\"field\":\"todaysCollectionForTradeType\"}}}}}}"
      },
      {
        "module": "W&S",
        "dateRefField": "date",
        "requestQueryMap": "{\"ulb\" : \"ulb.keyword\",\"ward\" : \"ward.keyword\"}",
        "indexName": "ws-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"WS\":{\"sum\":{\"field\":\"todaysCollectionForPaymentChannelType\"}}}}}}"
      },
      {
        "module": "OBPS",
        "dateRefField": "date",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "indexName": "obps-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"OBPS\":{\"sum\":{\"field\":\"todaysCollectionForPaymentMode\"}}}}}}"
      },
      {
        "module": "FIRENOC",
        "dateRefField": "date",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "indexName": "firenoc-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"FNOC\":{\"sum\":{\"field\":\"todaysCollectionForPaymentMode\"}}}}}}"
      },
      {
        "module": "MC",
        "dateRefField": "date",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "indexName": "mcollect-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"MCOLLECT\":{\"sum\":{\"field\":\"todaysCollectionForPaymentMode\"}}}}}}"
      }
      
    ],
    "chartType": "pie",
    "valueType": "Amount",
    "drillChart": "none",
    "documentType": "_doc",
    "action": "",
    "aggregationPaths": [
      "PT",
      "TL",
      "WS",
      "OBPS",
      "FNOC",
      "MCOLLECT"
    ],
    "insight": {
    },
    "_comment": " "
  },
 	
 	"totalApplicationsOverview": {
    "chartName": "NATIONAL_DSS_TOTAL_APPLICATIONS",
    "queries": [
      {
        "module": "TL",
        "dateRefField": "date",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "indexName": "tl-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"state\":{\"terms\":{\"field\":\"state.keyword\"},\"aggs\":{\"intermediateAggrULB\":{\"terms\":{\"field\":\"ulb.keyword\"},\"aggs\":{\"intermediateAggrWard\":{\"terms\":{\"field\":\"ward.keyword\"},\"aggs\":{\"days\":{\"terms\":{\"field\":\"date\"},\"aggs\":{\"applications\":{\"avg\":{\"field\":\"todaysApplications\"}}}},\"wardapplications\":{\"sum_bucket\":{\"buckets_path\":\"days.applications\"}}}},\"ulbApplications\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrWard.wardapplications\"}}}},\"stateApplications\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrULB.ulbApplications\"}}}},\"Total Applications\":{\"sum_bucket\":{\"buckets_path\":\"state.stateApplications\"}}}}}}"
      },
      {
        "module": "FIRENOC",
        "dateRefField": "date",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "indexName": "firenoc-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"Total Applications\":{\"sum\":{\"field\":\"todaysApplicationsForApplicationType\"}}}}}}"
      },
      {
        "module": "PT",
        "indexName": "pt-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"state\":{\"terms\":{\"field\":\"state.keyword\"},\"aggs\":{\"intermediateAggrULB\":{\"terms\":{\"field\":\"ulb.keyword\"},\"aggs\":{\"intermediateAggrWard\":{\"terms\":{\"field\":\"ward.keyword\"},\"aggs\":{\"days\":{\"terms\":{\"field\":\"date\"},\"aggs\":{\"applications\":{\"avg\":{\"field\":\"todaysTotalApplications\"}}}},\"wardapplications\":{\"sum_bucket\":{\"buckets_path\":\"days.applications\"}}}},\"ulbApplications\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrWard.wardapplications\"}}}},\"stateApplications\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrULB.ulbApplications\"}}}},\"Total Applications\":{\"sum_bucket\":{\"buckets_path\":\"state.stateApplications\"}}}}}}",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "dateRefField": "date"
      },
      {
        "module": "OBPS",
        "indexName": "obps-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"state\":{\"terms\":{\"field\":\"state.keyword\"},\"aggs\":{\"intermediateAggrULB\":{\"terms\":{\"field\":\"ulb.keyword\"},\"aggs\":{\"intermediateAggrWard\":{\"terms\":{\"field\":\"ward.keyword\"},\"aggs\":{\"intermediateAggr\":{\"terms\":{\"field\":\"date\"},\"aggs\":{\"ocSubmitted\":{\"avg\":{\"field\":\"ocSubmitted\"}}}},\"Total OC Submitted\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggr.ocSubmitted\"}},\"intermediateAggr1\":{\"terms\":{\"field\":\"date\"},\"aggs\":{\"applicationsSubmitted\":{\"avg\":{\"field\":\"applicationsSubmitted\"}}}},\"Total Applications Submitted\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggr1.applicationsSubmitted\"}},\"ward Total Applications\":{\"bucket_script\":{\"buckets_path\":{\"att\":\"Total Applications Submitted\",\"com\":\"Total OC Submitted\"},\"script\":\"params.att + params.com\"}}}},\"ulbApplications\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrWard.ward Total Applications\"}}}},\"stateApplications\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrULB.ulbApplications\"}}}},\"Total Applications\":{\"sum_bucket\":{\"buckets_path\":\"state.stateApplications\"}}}}}}",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "dateRefField": "date"
      },
      {
        "module": "W&S",
        "indexName": "ws-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"state\":{\"terms\":{\"field\":\"state.keyword\"},\"aggs\":{\"intermediateAggrULB\":{\"terms\":{\"field\":\"ulb.keyword\"},\"aggs\":{\"intermediateAggrWard\":{\"terms\":{\"field\":\"ward.keyword\"},\"aggs\":{\"days\":{\"terms\":{\"field\":\"date\"},\"aggs\":{\"applications\":{\"avg\":{\"field\":\"todaysTotalApplications\"}}}},\"wardapplications\":{\"sum_bucket\":{\"buckets_path\":\"days.applications\"}}}},\"ulbApplications\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrWard.wardapplications\"}}}},\"stateApplications\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrULB.ulbApplications\"}}}},\"Total Applications\":{\"sum_bucket\":{\"buckets_path\":\"state.stateApplications\"}}}}}}",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "dateRefField": "date"
      }
    ],
    "chartType": "metric",
    "valueType": "number",
    "drillChart": "none",
    "documentType": "_doc",
    "action": "",
    "aggregationPaths": [
      "Total Applications"
    ],
    "insight": {
      "chartResponseMap" : "totalApplicationsOverview",
      "action" : "differenceOfNumbers",
      "upwardIndicator" : "positive",
      "downwardIndicator" : "negative",
      "textMessage" : "$indicator$value% than last $insightInterval",
      "colorCode" : "#228B22",
      "insightInterval" : "year",
      "isRoundOff": true
    }
  },
   
    "closedApplicationOverview": {
    "chartName": "NATIONAL_DSS_CLOSED_APPLICATION",
    "queries": [
      {
        "module": "PT",
        "indexName": "pt-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"state\":{\"terms\":{\"field\":\"state.keyword\"},\"aggs\":{\"intermediateAggrULB\":{\"terms\":{\"field\":\"ulb.keyword\"},\"aggs\":{\"intermediateAggrWard\":{\"terms\":{\"field\":\"ward.keyword\"},\"aggs\":{\"days\":{\"terms\":{\"field\":\"date\"},\"aggs\":{\"applications\":{\"avg\":{\"field\":\"todaysClosedApplications\"}}}},\"wardapplications\":{\"sum_bucket\":{\"buckets_path\":\"days.applications\"}}}},\"ulbApplications\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrWard.wardapplications\"}}}},\"stateApplications\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrULB.ulbApplications\"}}}},\"Applications Closed\":{\"sum_bucket\":{\"buckets_path\":\"state.stateApplications\"}}}}}}",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "dateRefField": "date"
      },
      {
        "module": "W&S",
        "indexName": "ws-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"state\":{\"terms\":{\"field\":\"state.keyword\"},\"aggs\":{\"intermediateAggrULB\":{\"terms\":{\"field\":\"ulb.keyword\"},\"aggs\":{\"intermediateAggrWard\":{\"terms\":{\"field\":\"ward.keyword\"},\"aggs\":{\"days\":{\"terms\":{\"field\":\"date\"},\"aggs\":{\"applications\":{\"avg\":{\"field\":\"todaysClosedApplications\"}}}},\"wardapplications\":{\"sum_bucket\":{\"buckets_path\":\"days.applications\"}}}},\"ulbApplications\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrWard.wardapplications\"}}}},\"stateApplications\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrULB.ulbApplications\"}}}},\"Applications Closed\":{\"sum_bucket\":{\"buckets_path\":\"state.stateApplications\"}}}}}}",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "dateRefField": "date"
      },
      {
        "module": "OBPS",
        "indexName": "obps-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"state\":{\"terms\":{\"field\":\"state.keyword\"},\"aggs\":{\"intermediateAggrULB\":{\"terms\":{\"field\":\"ulb.keyword\"},\"aggs\":{\"intermediateAggrWard\":{\"terms\":{\"field\":\"ward.keyword\"},\"aggs\":{\"intermediateAggr\":{\"terms\":{\"field\":\"date\"},\"aggs\":{\"ocSubmitted\":{\"avg\":{\"field\":\"todaysClosedApplicationsOC\"}}}},\"Total OC Closed\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggr.ocSubmitted\"}},\"intermediateAggr1\":{\"terms\":{\"field\":\"date\"},\"aggs\":{\"applicationsSubmitted\":{\"avg\":{\"field\":\"todaysClosedApplicationsPermit\"}}}},\"Total Applications Closed\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggr1.applicationsSubmitted\"}},\"Applications Closed\":{\"bucket_script\":{\"buckets_path\":{\"att\":\"Total OC Closed\",\"com\":\"Total Applications Closed\"},\"script\":\"params.att + params.com\"}}}},\"ulbApplications\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrWard.Applications Closed\"}}}},\"stateApplications\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrULB.ulbApplications\"}}}},\"Applications Closed\":{\"sum_bucket\":{\"buckets_path\":\"state.stateApplications\"}}}}}}",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "dateRefField": "date"
      },
      {
        "module": "FIRENOC",
        "dateRefField": "date",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "indexName": "firenoc-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"state\":{\"terms\":{\"field\":\"state.keyword\"},\"aggs\":{\"intermediateAggrULB\":{\"terms\":{\"field\":\"ulb.keyword\"},\"aggs\":{\"intermediateAggrWard\":{\"terms\":{\"field\":\"ward.keyword\"},\"aggs\":{\"days\":{\"terms\":{\"field\":\"date\"},\"aggs\":{\"applications\":{\"avg\":{\"field\":\"todaysClosedApplications\"}}}},\"wardapplications\":{\"sum_bucket\":{\"buckets_path\":\"days.applications\"}}}},\"ulbApplications\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrWard.wardapplications\"}}}},\"stateApplications\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrULB.ulbApplications\"}}}},\"Applications Closed\":{\"sum_bucket\":{\"buckets_path\":\"state.stateApplications\"}}}}}}"
      },
      {
        "module": "TL",
        "dateRefField": "date",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "indexName": "tl-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"state\":{\"terms\":{\"field\":\"state.keyword\"},\"aggs\":{\"intermediateAggrULB\":{\"terms\":{\"field\":\"ulb.keyword\"},\"aggs\":{\"intermediateAggrWard\":{\"terms\":{\"field\":\"ward.keyword\"},\"aggs\":{\"days\":{\"terms\":{\"field\":\"date\"},\"aggs\":{\"applications\":{\"avg\":{\"field\":\"todaysLicenseIssuedWithinSLA\"}}}},\"wardapplications\":{\"sum_bucket\":{\"buckets_path\":\"days.applications\"}}}},\"ulbApplications\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrWard.wardapplications\"}}}},\"stateApplications\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrULB.ulbApplications\"}}}},\"Applications Closed\":{\"sum_bucket\":{\"buckets_path\":\"state.stateApplications\"}}}}}}"
      }
    ],
    "chartType": "metric",
    "valueType": "number",
    "action": "",
    "documentType": "_doc",
    "drillChart": "none",
    "aggregationPaths": [
      "Applications Closed"
    ],
    "insight": {
      "chartResponseMap" : "closedApplicationOverview",
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
  
  	"slaAchievedOverview": {
    "chartName": "NATIONAL_DSS_SLA_ACHIEVED",
    "queries": [
      {
        "module": "COMMON",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "dateRefField": "date",
        "indexName": "common-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must\":[{\"term\":{\"status.keyword\":\"Live\"}}]}},\"aggs\":{\"latest\":{\"terms\":{\"field\":\"date\",\"order\":{\"_term\":\"desc\"},\"size\":1},\"aggs\":{\"slaAchieve\":{\"avg\":{\"field\":\"slaAchievement\"}}}},\"slaAchievement\":{\"avg_bucket\":{\"buckets_path\":\"latest.slaAchieve\"}}}}}}"
      }
    ],
    "chartType": "metric",
    "valueType": "percentage",
    "drillChart": "none",
    "documentType": "_doc",
    "action": "percentage",
    "isRoundOff": true,		
    "aggregationPaths": [
      "slaAchievement"
    ],
    "insight": {
      "chartResponseMap" : "slaAchievedOverview",
      "action" : "differenceOfNumbers",
      "upwardIndicator" : "positive",
      "downwardIndicator" : "negative",
      "textMessage" : "$indicator$value% than last $insightInterval",
      "colorCode" : "#228B22",
      "insightInterval" : "year",
      "isRoundOff": true
    },
    "_comment": " SLA Achieved Percentage "
  },
    
   	"citizenRegisteredOverview": {
    "chartName": "NATIONAL_DSS_CITIZEN_REGISTERED",
    "queries": [
      {
        "module": "COMMON",
        "indexName": "common-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must\":[{\"term\":{\"status.keyword\":\"Live\"}}]}},\"aggs\":{\"latest\":{\"terms\":{\"field\":\"date\",\"order\":{\"_term\":\"desc\"},\"size\":1},\"aggs\":{\"totalCitizensCount\":{\"avg\":{\"field\":\"totalCitizensCount\"}}}},\"Citizen Registered\":{\"avg_bucket\":{\"buckets_path\":\"latest.totalCitizensCount\"}}}}}}",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "dateRefField": "date"
      }
    ],
    "chartType": "metric",
    "valueType": "number",
    "action": "",
    "documentType": "_doc",
    "drillChart": "none",
    "aggregationPaths": [
      "Citizen Registered"
    ],
    "insight": {
      "chartResponseMap" : "citizenRegisteredOverview",
      "action" : "differenceOfNumbers",
      "upwardIndicator" : "positive",
      "downwardIndicator" : "negative",
      "textMessage" : "$indicator$value% than last $insightInterval",
      "colorCode" : "#228B22",
      "insightInterval" : "year",
      "isRoundOff": true
    },
    "_comment": " totalApplication is the chartId"
  },

 	"totalApplication&ClosedApplicationOverview": {
    "chartName": "NATIONAL_DSS_TOTAL_APPLICATION_&_CLOSED_APPLICATION",
    "queries": [
      {
        "module": "PT",
        "indexName": "pt-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"Total Application\":{\"date_histogram\":{\"field\":\"date\",\"interval\":\"intervalvalue\"},\"aggs\":{\"state\":{\"terms\":{\"field\":\"state.keyword\"},\"aggs\":{\"intermediateAggrULB\":{\"terms\":{\"field\":\"ulb.keyword\"},\"aggs\":{\"intermediateAggrWard\":{\"terms\":{\"field\":\"ward.keyword\"},\"aggs\":{\"days\":{\"terms\":{\"field\":\"date\"},\"aggs\":{\"applications\":{\"avg\":{\"field\":\"todaysTotalApplications\"}}}},\"wardapplications\":{\"sum_bucket\":{\"buckets_path\":\"days.applications\"}}}},\"ulbApplications\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrWard.wardapplications\"}}}},\"stateApplications\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrULB.ulbApplications\"}}}},\"allApplications\":{\"sum_bucket\":{\"buckets_path\":\"state.stateApplications\"}}}},\"Closed Application\":{\"date_histogram\":{\"field\":\"date\",\"interval\":\"intervalvalue\"},\"aggs\":{\"state\":{\"terms\":{\"field\":\"state.keyword\"},\"aggs\":{\"intermediateAggrULB\":{\"terms\":{\"field\":\"ulb.keyword\"},\"aggs\":{\"intermediateAggrWard\":{\"terms\":{\"field\":\"ward.keyword\"},\"aggs\":{\"days\":{\"terms\":{\"field\":\"date\"},\"aggs\":{\"applications\":{\"avg\":{\"field\":\"todaysClosedApplications\"}}}},\"wardapplications\":{\"sum_bucket\":{\"buckets_path\":\"days.applications\"}}}},\"ulbApplications\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrWard.wardapplications\"}}}},\"stateApplications\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrULB.ulbApplications\"}}}},\"allApplications\":{\"sum_bucket\":{\"buckets_path\":\"state.stateApplications\"}}}}}}}}",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "dateRefField": "date"
      },
      {
        "module": "TL",
        "dateRefField": "date",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "indexName": "tl-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"Total Application\":{\"date_histogram\":{\"field\":\"date\",\"interval\":\"intervalvalue\"},\"aggs\":{\"state\":{\"terms\":{\"field\":\"state.keyword\"},\"aggs\":{\"intermediateAggrULB\":{\"terms\":{\"field\":\"ulb.keyword\"},\"aggs\":{\"intermediateAggrWard\":{\"terms\":{\"field\":\"ward.keyword\"},\"aggs\":{\"days\":{\"terms\":{\"field\":\"date\"},\"aggs\":{\"applications\":{\"avg\":{\"field\":\"todaysApplications\"}}}},\"wardapplications\":{\"sum_bucket\":{\"buckets_path\":\"days.applications\"}}}},\"ulbApplications\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrWard.wardapplications\"}}}},\"stateApplications\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrULB.ulbApplications\"}}}},\"allApplications\":{\"sum_bucket\":{\"buckets_path\":\"state.stateApplications\"}}}},\"Closed Application\":{\"date_histogram\":{\"field\":\"date\",\"interval\":\"intervalvalue\"},\"aggs\":{\"state\":{\"terms\":{\"field\":\"state.keyword\"},\"aggs\":{\"intermediateAggrULB\":{\"terms\":{\"field\":\"ulb.keyword\"},\"aggs\":{\"intermediateAggrWard\":{\"terms\":{\"field\":\"ward.keyword\"},\"aggs\":{\"days\":{\"terms\":{\"field\":\"date\"},\"aggs\":{\"applications\":{\"avg\":{\"field\":\"todaysLicenseIssuedWithinSLA\"}}}},\"wardapplications\":{\"sum_bucket\":{\"buckets_path\":\"days.applications\"}}}},\"ulbApplications\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrWard.wardapplications\"}}}},\"stateApplications\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrULB.ulbApplications\"}}}},\"allApplications\":{\"sum_bucket\":{\"buckets_path\":\"state.stateApplications\"}}}}}}}}"
      },
      {
        "module": "W&S",
        "indexName": "ws-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"Total Application\":{\"date_histogram\":{\"field\":\"date\",\"interval\":\"intervalvalue\"},\"aggs\":{\"state\":{\"terms\":{\"field\":\"state.keyword\"},\"aggs\":{\"intermediateAggrULB\":{\"terms\":{\"field\":\"ulb.keyword\"},\"aggs\":{\"intermediateAggrWard\":{\"terms\":{\"field\":\"ward.keyword\"},\"aggs\":{\"days\":{\"terms\":{\"field\":\"date\"},\"aggs\":{\"applications\":{\"avg\":{\"field\":\"todaysTotalApplications\"}}}},\"wardapplications\":{\"sum_bucket\":{\"buckets_path\":\"days.applications\"}}}},\"ulbApplications\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrWard.wardapplications\"}}}},\"stateApplications\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrULB.ulbApplications\"}}}},\"allApplications\":{\"sum_bucket\":{\"buckets_path\":\"state.stateApplications\"}}}},\"Closed Application\":{\"date_histogram\":{\"field\":\"date\",\"interval\":\"intervalvalue\"},\"aggs\":{\"state\":{\"terms\":{\"field\":\"state.keyword\"},\"aggs\":{\"intermediateAggrULB\":{\"terms\":{\"field\":\"ulb.keyword\"},\"aggs\":{\"intermediateAggrWard\":{\"terms\":{\"field\":\"ward.keyword\"},\"aggs\":{\"days\":{\"terms\":{\"field\":\"date\"},\"aggs\":{\"applications\":{\"avg\":{\"field\":\"todaysClosedApplications\"}}}},\"wardapplications\":{\"sum_bucket\":{\"buckets_path\":\"days.applications\"}}}},\"ulbApplications\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrWard.wardapplications\"}}}},\"stateApplications\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrULB.ulbApplications\"}}}},\"allApplications\":{\"sum_bucket\":{\"buckets_path\":\"state.stateApplications\"}}}}}}}}",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "dateRefField": "date"
      },
      {
        "module": "OBPS",
        "indexName": "obps-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"Total Application\":{\"date_histogram\":{\"field\":\"date\",\"interval\":\"intervalvalue\"},\"aggs\":{\"state\":{\"terms\":{\"field\":\"state.keyword\"},\"aggs\":{\"intermediateAggrULB\":{\"terms\":{\"field\":\"ulb.keyword\"},\"aggs\":{\"intermediateAggrWard\":{\"terms\":{\"field\":\"ward.keyword\"},\"aggs\":{\"intermediateAggr\":{\"terms\":{\"field\":\"date\"},\"aggs\":{\"ocSubmitted\":{\"avg\":{\"field\":\"ocSubmitted\"}}}},\"Total OC Submitted\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggr.ocSubmitted\"}},\"intermediateAggr1\":{\"terms\":{\"field\":\"date\"},\"aggs\":{\"applicationsSubmitted\":{\"avg\":{\"field\":\"applicationsSubmitted\"}}}},\"Total Applications Submitted\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggr1.applicationsSubmitted\"}},\"ward Total Applications\":{\"bucket_script\":{\"buckets_path\":{\"att\":\"Total Applications Submitted\",\"com\":\"Total OC Submitted\"},\"script\":\"params.att + params.com\"}}}},\"ulbApplications\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrWard.ward Total Applications\"}}}},\"stateApplications\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrULB.ulbApplications\"}}}},\"allApplications\":{\"sum_bucket\":{\"buckets_path\":\"state.stateApplications\"}}}},\"Closed Application\":{\"date_histogram\":{\"field\":\"date\",\"interval\":\"intervalvalue\"},\"aggs\":{\"state\":{\"terms\":{\"field\":\"state.keyword\"},\"aggs\":{\"intermediateAggrULB\":{\"terms\":{\"field\":\"ulb.keyword\"},\"aggs\":{\"intermediateAggrWard\":{\"terms\":{\"field\":\"ward.keyword\"},\"aggs\":{\"intermediateAggr\":{\"terms\":{\"field\":\"date\"},\"aggs\":{\"ocSubmitted\":{\"avg\":{\"field\":\"todaysClosedApplicationsOC\"}}}},\"Total OC Closed\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggr.ocSubmitted\"}},\"intermediateAggr1\":{\"terms\":{\"field\":\"date\"},\"aggs\":{\"applicationsSubmitted\":{\"avg\":{\"field\":\"todaysClosedApplicationsPermit\"}}}},\"Total Applications Closed\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggr1.applicationsSubmitted\"}},\"Applications Closed\":{\"bucket_script\":{\"buckets_path\":{\"att\":\"Total OC Closed\",\"com\":\"Total Applications Closed\"},\"script\":\"params.att + params.com\"}}}},\"ulbApplications\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrWard.Applications Closed\"}}}},\"stateApplications\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrULB.ulbApplications\"}}}},\"allApplications\":{\"sum_bucket\":{\"buckets_path\":\"state.stateApplications\"}}}}}}}}",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "dateRefField": "date"
      },
      {
        "module": "FIRENOC",
        "dateRefField": "date",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "indexName": "firenoc-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"Total Application\":{\"date_histogram\":{\"field\":\"date\",\"interval\":\"intervalvalue\"},\"aggs\":{\"Total Applications\":{\"sum\":{\"field\":\"todaysApplicationsForApplicationType\"}}}},\"Closed Application\":{\"date_histogram\":{\"field\":\"date\",\"interval\":\"intervalvalue\"},\"aggs\":{\"state\":{\"terms\":{\"field\":\"state.keyword\"},\"aggs\":{\"intermediateAggrULB\":{\"terms\":{\"field\":\"ulb.keyword\"},\"aggs\":{\"intermediateAggrWard\":{\"terms\":{\"field\":\"ward.keyword\"},\"aggs\":{\"days\":{\"terms\":{\"field\":\"date\"},\"aggs\":{\"applications\":{\"avg\":{\"field\":\"todaysClosedApplications\"}}}},\"wardapplications\":{\"sum_bucket\":{\"buckets_path\":\"days.applications\"}}}},\"ulbApplications\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrWard.wardapplications\"}}}},\"stateApplications\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrULB.ulbApplications\"}}}},\"allApplications\":{\"sum_bucket\":{\"buckets_path\":\"state.stateApplications\"}}}}}}}}"
      }  
    ],
    "chartType": "line",
    "valueType": "number",
    "action": "",
    "drillChart": "none",
    "documentType": "_doc",
    "aggregationPaths": [
      "Total Application",
      "Closed Application"
    ],
    "isCumulative": false,
    "interval": "month",
    "insight": {
    },
    "_comment": " "
  },
    
  	"topPerformingStatesCompletionRateOverview": {
    "chartName": "NATIONAL_DSS_TOP_3_PERFORMING_STATES_COMPLETION_RATE",
    "queries": [
      {
        "module": "PT",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "dateRefField": "date",
        "indexName": "pt-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"Completed Within SLA\":{\"terms\":{\"field\":\"state.keyword\"},\"aggs\":{\"sum\":{\"sum\":{\"field\":\"assessedPropertiesForUsageCategory\"}}}},\"Total Applications\":{\"terms\":{\"field\":\"state.keyword\"},\"aggs\":{\"sum\":{\"sum\":{\"field\":\"propertiesRegisteredForFinancialYear\"}}}}}}}}"
      },
      {
         "module": "WS",
         "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
         "dateRefField": "date",
         "indexName": "ws-national-dashboard",
         "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"Completed Within SLA\":{\"terms\":{\"field\":\"state.keyword\"},\"aggs\":{\"intermediateAggrULB\":{\"terms\":{\"field\":\"ulb.keyword\"},\"aggs\":{\"intermediateAggrWard\":{\"terms\":{\"field\":\"ward.keyword\"},\"aggs\":{\"days\":{\"terms\":{\"field\":\"date\"},\"aggs\":{\"applications\":{\"avg\":{\"field\":\"todaysCompletedApplicationsWithinSLA\"}}}},\"wardapplications\":{\"sum_bucket\":{\"buckets_path\":\"days.applications\"}}}},\"ulbApplications\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrWard.wardapplications\"}}}},\"stateApplications\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrULB.ulbApplications\"}}}},\"Total Applications\":{\"terms\":{\"field\":\"state.keyword\"},\"aggs\":{\"intermediateAggrULB\":{\"terms\":{\"field\":\"ulb.keyword\"},\"aggs\":{\"intermediateAggrWard\":{\"terms\":{\"field\":\"ward.keyword\"},\"aggs\":{\"days\":{\"terms\":{\"field\":\"date\"},\"aggs\":{\"applications\":{\"avg\":{\"field\":\"todaysTotalApplications\"}}}},\"wardapplications\":{\"sum_bucket\":{\"buckets_path\":\"days.applications\"}}}},\"ulbApplications\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrWard.wardapplications\"}}}},\"stateApplications\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrULB.ulbApplications\"}}}}}}}}"
      },
      {
          "module": "TL",
          "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
          "dateRefField": "date",
          "indexName": "tl-national-dashboard",
          "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"Completed Within SLA\":{\"terms\":{\"field\":\"state.keyword\"},\"aggs\":{\"intermediateAggrULB\":{\"terms\":{\"field\":\"ulb.keyword\"},\"aggs\":{\"intermediateAggrWard\":{\"terms\":{\"field\":\"ward.keyword\"},\"aggs\":{\"days\":{\"terms\":{\"field\":\"date\"},\"aggs\":{\"applications\":{\"avg\":{\"field\":\"todaysLicenseIssuedWithinSLA\"}}}},\"wardapplications\":{\"sum_bucket\":{\"buckets_path\":\"days.applications\"}}}},\"ulbApplications\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrWard.wardapplications\"}}}},\"stateApplications\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrULB.ulbApplications\"}}}},\"Total Applications\":{\"terms\":{\"field\":\"state.keyword\"},\"aggs\":{\"Sum\":{\"sum\":{\"field\":\"todaysTradeLicensesForStatus\"}}}}}}}}"
       },
       {
         "module": "OBPS",
         "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
         "dateRefField": "date",
         "indexName": "obps-national-dashboard",
         "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[]}},\"aggs\":{\"Licenses Within SLA\":{\"terms\":{\"field\":\"state.keyword\"},\"aggs\":{\"Total Permits\":{\"sum\":{\"field\":\"permitsIssuedForRiskType\"}}}},\"Total Applications\":{\"terms\":{\"field\":\"state.keyword\"},\"aggs\":{\"intermediateAggrULB\":{\"terms\":{\"field\":\"ulb.keyword\"},\"aggs\":{\"intermediateAggrWard\":{\"terms\":{\"field\":\"ward.keyword\"},\"aggs\":{\"days\":{\"terms\":{\"field\":\"date\"},\"aggs\":{\"applications\":{\"avg\":{\"field\":\"applicationsSubmitted\"}}}},\"wardapplications\":{\"sum_bucket\":{\"buckets_path\":\"days.applications\"}}}},\"ulbApplications\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrWard.wardapplications\"}}}},\"Sum\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrULB.ulbApplications\"}}}}}}}}"
       },
       {
         "module": "FIRENOC",
         "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
         "dateRefField": "date",
         "indexName": "firenoc-national-dashboard",
         "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"Completed Within SLA\":{\"terms\":{\"field\":\"state.keyword\"},\"aggs\":{\"intermediateAggrULB\":{\"terms\":{\"field\":\"ulb.keyword\"},\"aggs\":{\"intermediateAggrWard\":{\"terms\":{\"field\":\"ward.keyword\"},\"aggs\":{\"days\":{\"terms\":{\"field\":\"date\"},\"aggs\":{\"applications\":{\"avg\":{\"field\":\"todaysCompletedApplicationsWithinSLA\"}}}},\"wardapplications\":{\"sum_bucket\":{\"buckets_path\":\"days.applications\"}}}},\"ulbApplications\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrWard.wardapplications\"}}}},\"Sum\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrULB.ulbApplications\"}}}},\"Total Applications\":{\"terms\":{\"field\":\"state.keyword\"},\"aggs\":{\"sum\":{\"sum\":{\"field\":\"todaysApplicationsForApplicationType\"}}}}}}}}"
      }
      
    ],
    "chartType": "perform",
    "valueType": "percentage",
    "drillChart": "none",
    "documentType": "_doc",
    "action": "percentage",
    "plotLabel": "DSS_COMPLETION_RATE",
    "order": "desc",
    "limit": 3,
    "isRoundOff": true,
    "aggregationPaths": [
      "Completed Within SLA",
      "Total Applications"
    ],
    "insight": {
    },
    "_comment": " Top Performing STATES for Completion rate"
  },
 
  	"bottomPerformingStatesCompletionRateOverview": {
    "chartName": "NATIONAL_DSS_BOTTOM_3_PERFORMING_STATES_COMPLETION_RATE",
    "queries": [
      {
        "module": "PT",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "dateRefField": "date",
        "indexName": "pt-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"Completed Within SLA\":{\"terms\":{\"field\":\"state.keyword\"},\"aggs\":{\"sum\":{\"sum\":{\"field\":\"assessedPropertiesForUsageCategory\"}}}},\"Total Applications\":{\"terms\":{\"field\":\"state.keyword\"},\"aggs\":{\"sum\":{\"sum\":{\"field\":\"propertiesRegisteredForFinancialYear\"}}}}}}}}"
      },
      {
         "module": "WS",
         "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
         "dateRefField": "date",
         "indexName": "ws-national-dashboard",
         "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"Completed Within SLA\":{\"terms\":{\"field\":\"state.keyword\"},\"aggs\":{\"intermediateAggrULB\":{\"terms\":{\"field\":\"ulb.keyword\"},\"aggs\":{\"intermediateAggrWard\":{\"terms\":{\"field\":\"ward.keyword\"},\"aggs\":{\"days\":{\"terms\":{\"field\":\"date\"},\"aggs\":{\"applications\":{\"avg\":{\"field\":\"todaysCompletedApplicationsWithinSLA\"}}}},\"wardapplications\":{\"sum_bucket\":{\"buckets_path\":\"days.applications\"}}}},\"ulbApplications\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrWard.wardapplications\"}}}},\"stateApplications\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrULB.ulbApplications\"}}}},\"Total Applications\":{\"terms\":{\"field\":\"state.keyword\"},\"aggs\":{\"intermediateAggrULB\":{\"terms\":{\"field\":\"ulb.keyword\"},\"aggs\":{\"intermediateAggrWard\":{\"terms\":{\"field\":\"ward.keyword\"},\"aggs\":{\"days\":{\"terms\":{\"field\":\"date\"},\"aggs\":{\"applications\":{\"avg\":{\"field\":\"todaysTotalApplications\"}}}},\"wardapplications\":{\"sum_bucket\":{\"buckets_path\":\"days.applications\"}}}},\"ulbApplications\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrWard.wardapplications\"}}}},\"stateApplications\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrULB.ulbApplications\"}}}}}}}}"
      },
      {
          "module": "TL",
          "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
          "dateRefField": "date",
          "indexName": "tl-national-dashboard",
          "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"Completed Within SLA\":{\"terms\":{\"field\":\"state.keyword\"},\"aggs\":{\"intermediateAggrULB\":{\"terms\":{\"field\":\"ulb.keyword\"},\"aggs\":{\"intermediateAggrWard\":{\"terms\":{\"field\":\"ward.keyword\"},\"aggs\":{\"days\":{\"terms\":{\"field\":\"date\"},\"aggs\":{\"applications\":{\"avg\":{\"field\":\"todaysLicenseIssuedWithinSLA\"}}}},\"wardapplications\":{\"sum_bucket\":{\"buckets_path\":\"days.applications\"}}}},\"ulbApplications\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrWard.wardapplications\"}}}},\"stateApplications\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrULB.ulbApplications\"}}}},\"Total Applications\":{\"terms\":{\"field\":\"state.keyword\"},\"aggs\":{\"Sum\":{\"sum\":{\"field\":\"todaysTradeLicensesForStatus\"}}}}}}}}"
       },
       {
         "module": "OBPS",
         "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
         "dateRefField": "date",
         "indexName": "obps-national-dashboard",
         "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[]}},\"aggs\":{\"Licenses Within SLA\":{\"terms\":{\"field\":\"state.keyword\"},\"aggs\":{\"Total Permits\":{\"sum\":{\"field\":\"permitsIssuedForRiskType\"}}}},\"Total Applications\":{\"terms\":{\"field\":\"state.keyword\"},\"aggs\":{\"intermediateAggrULB\":{\"terms\":{\"field\":\"ulb.keyword\"},\"aggs\":{\"intermediateAggrWard\":{\"terms\":{\"field\":\"ward.keyword\"},\"aggs\":{\"days\":{\"terms\":{\"field\":\"date\"},\"aggs\":{\"applications\":{\"avg\":{\"field\":\"applicationsSubmitted\"}}}},\"wardapplications\":{\"sum_bucket\":{\"buckets_path\":\"days.applications\"}}}},\"ulbApplications\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrWard.wardapplications\"}}}},\"Sum\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrULB.ulbApplications\"}}}}}}}}"
       },
       {
         "module": "FIRENOC",
         "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
         "dateRefField": "date",
         "indexName": "firenoc-national-dashboard",
         "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"Completed Within SLA\":{\"terms\":{\"field\":\"state.keyword\"},\"aggs\":{\"intermediateAggrULB\":{\"terms\":{\"field\":\"ulb.keyword\"},\"aggs\":{\"intermediateAggrWard\":{\"terms\":{\"field\":\"ward.keyword\"},\"aggs\":{\"days\":{\"terms\":{\"field\":\"date\"},\"aggs\":{\"applications\":{\"avg\":{\"field\":\"todaysCompletedApplicationsWithinSLA\"}}}},\"wardapplications\":{\"sum_bucket\":{\"buckets_path\":\"days.applications\"}}}},\"ulbApplications\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrWard.wardapplications\"}}}},\"Sum\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrULB.ulbApplications\"}}}},\"Total Applications\":{\"terms\":{\"field\":\"state.keyword\"},\"aggs\":{\"sum\":{\"sum\":{\"field\":\"todaysApplicationsForApplicationType\"}}}}}}}}"
      }
    ],
    "chartType": "perform",
    "valueType": "percentage",
    "drillChart": "none",
    "documentType": "_doc",
    "action": "percentage",
    "plotLabel": "DSS_COMPLETION_RATE",
    "order": "asc",
    "limit": 3,
    "isRoundOff": true,
    "aggregationPaths": [
     "Completed Within SLA",
      "Total Applications"
    ],
    "insight": {
    },
    "_comment": " Bottom Performing STATES for Completion rate"
  },  
  
  	"totalApplicationServiceWiseOverview": {
    "chartName": "NATIONAL_DSS_TOTAL_APPLICATIONS_SERVICE_WISE",
    "queries": [
       {
        "module": "TL",
        "dateRefField": "date",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "indexName": "tl-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"state\":{\"terms\":{\"field\":\"state.keyword\"},\"aggs\":{\"intermediateAggrULB\":{\"terms\":{\"field\":\"ulb.keyword\"},\"aggs\":{\"intermediateAggrWard\":{\"terms\":{\"field\":\"ward.keyword\"},\"aggs\":{\"days\":{\"terms\":{\"field\":\"date\"},\"aggs\":{\"applications\":{\"avg\":{\"field\":\"todaysApplications\"}}}},\"wardapplications\":{\"sum_bucket\":{\"buckets_path\":\"days.applications\"}}}},\"ulbApplications\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrWard.wardapplications\"}}}},\"stateApplications\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrULB.ulbApplications\"}}}},\"TL\":{\"sum_bucket\":{\"buckets_path\":\"state.stateApplications\"}}}}}}"
      },
      {
        "module": "FIRENOC",
        "dateRefField": "date",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "indexName": "firenoc-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"FNOC\":{\"sum\":{\"field\":\"todaysApplicationsForApplicationType\"}}}}}}"
      },
      {
        "module": "PT",
        "indexName": "pt-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"state\":{\"terms\":{\"field\":\"state.keyword\"},\"aggs\":{\"intermediateAggrULB\":{\"terms\":{\"field\":\"ulb.keyword\"},\"aggs\":{\"intermediateAggrWard\":{\"terms\":{\"field\":\"ward.keyword\"},\"aggs\":{\"days\":{\"terms\":{\"field\":\"date\"},\"aggs\":{\"applications\":{\"avg\":{\"field\":\"todaysTotalApplications\"}}}},\"wardapplications\":{\"sum_bucket\":{\"buckets_path\":\"days.applications\"}}}},\"ulbApplications\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrWard.wardapplications\"}}}},\"stateApplications\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrULB.ulbApplications\"}}}},\"PT\":{\"sum_bucket\":{\"buckets_path\":\"state.stateApplications\"}}}}}}",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "dateRefField": "date"
      },
      {
        "module": "OBPS",
        "indexName": "obps-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"state\":{\"terms\":{\"field\":\"state.keyword\"},\"aggs\":{\"intermediateAggrULB\":{\"terms\":{\"field\":\"ulb.keyword\"},\"aggs\":{\"intermediateAggrWard\":{\"terms\":{\"field\":\"ward.keyword\"},\"aggs\":{\"intermediateAggr\":{\"terms\":{\"field\":\"date\"},\"aggs\":{\"ocSubmitted\":{\"avg\":{\"field\":\"ocSubmitted\"}}}},\"Total OC Submitted\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggr.ocSubmitted\"}},\"intermediateAggr1\":{\"terms\":{\"field\":\"date\"},\"aggs\":{\"applicationsSubmitted\":{\"avg\":{\"field\":\"applicationsSubmitted\"}}}},\"Total Applications Submitted\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggr1.applicationsSubmitted\"}},\"ward Total Applications\":{\"bucket_script\":{\"buckets_path\":{\"att\":\"Total Applications Submitted\",\"com\":\"Total OC Submitted\"},\"script\":\"params.att + params.com\"}}}},\"ulbApplications\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrWard.ward Total Applications\"}}}},\"stateApplications\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrULB.ulbApplications\"}}}},\"OBPS\":{\"sum_bucket\":{\"buckets_path\":\"state.stateApplications\"}}}}}}",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "dateRefField": "date"
      },
      {
        "module": "W&S",
        "indexName": "ws-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"state\":{\"terms\":{\"field\":\"state.keyword\"},\"aggs\":{\"intermediateAggrULB\":{\"terms\":{\"field\":\"ulb.keyword\"},\"aggs\":{\"intermediateAggrWard\":{\"terms\":{\"field\":\"ward.keyword\"},\"aggs\":{\"days\":{\"terms\":{\"field\":\"date\"},\"aggs\":{\"applications\":{\"avg\":{\"field\":\"todaysTotalApplications\"}}}},\"wardapplications\":{\"sum_bucket\":{\"buckets_path\":\"days.applications\"}}}},\"ulbApplications\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrWard.wardapplications\"}}}},\"stateApplications\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrULB.ulbApplications\"}}}},\"WS\":{\"sum_bucket\":{\"buckets_path\":\"state.stateApplications\"}}}}}}",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "dateRefField": "date"
      }
    ],
    "chartType": "pie",
    "valueType": "number",
    "action": "",
    "documentType": "_doc",
    "drillChart": "none",
    "aggregationPaths": [
      "PT",
      "TL",
      "WS",
      "OBPS",
      "FNOC"
    ],
    "insight": {
    },
    "_comment": " totalApplication is the chartId"
  }

```

[Click here to check the complete configuration](https://github.com/egovernments/configs/blob/qa/egov-dss-dashboards/dashboard-analytics/ChartApiConfig.json)

**Master Dashboard Configuration -** Master Dashboard Configuration is the main configuration which defines as which are the Dashboards which are to be painted on screen.&#x20;

It includes all the Visualizations, their groups, the charts which comes within them and even their dimensions as what should be their height and width.

```
 {
      "name": "NATIONAL_OVERVIEW_DASHBOARD",
      "id": "national-overview",
      "isActive": "",
      "style": "",
      "visualizations": [
        {
          "name": "NATIONAL_DSS_REVENUE",
          "vizArray": [
            {
              "id": 111,
              "name": "NATIONAL_DSS_OVERVIEW",
              "vizType": "metric-collection",
              "noUnit": true,
              "isCollapsible": false,
              "charts": [
                {
                  "id": "todaysCollectionOverview",
                  "name": "NATIONAL_DSS_TOTAL_COLLECTION_TODAY",
                  "code": "",
                  "chartType": "",
                  "filter": {"title": "TODAY"},
                  "headers": []
                },
                {
                  "id": "totalCollectionOverview",
                  "name": "NATIONAL_DSS_TOTAL_COLLECTION",
                  "code": "",
                  "chartType": "metric",
                  "filter": "",
                  "headers": []
                },
                {
                  "id": "targetCollectionvOverview",
                  "name": "NATIONAL_DSS_TARGET_COLLECTION",
                  "code": "",
                  "chartType": "metric",
                  "filter": "",
                  "headers": []
                },
                {
                  "id": "targetAchievedOverview",
                  "name": "NATIONAL_DSS_TARGET_ACHIEVED",
                  "code": "",
                  "chartType": "metric",
                  "filter": "",
                  "headers": []
                }
              ]
            },
            {
              "id": 112,
              "name": "NATIONAL_DSS_TOTAL_CUMULATIVE_COLLECTION",
              "dimensions": {
                "height": 350,
                "width": 7
              },
              "vizType": "chart",
              "label": "",
              "noUnit": true,
              "isCollapsible": false,
              "charts": [
                {
                  "id": "cumulativeCollectionOverview",
                  "name": "Weekly",
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
          "name": "NATIONAL_DSS_REVENUE",
          "vizArray": [
               {
              "id": 121,
              "name": "NATIONAL_DSS_TOTAL_CUMULATIVE_COLLECTION_SERVICE_WISE",
              "dimensions": {
                "height": 250,
                "width": 4
              },
              "vizType": "chart",
              "noUnit": true,
              "isCollapsible": false,
              "charts": [
                {
                  "id": "totalCollectionServiceWiseOverview",
                  "name": "NATIONAL_DSS_TOTAL_CUMULATIVE_COLLECTION_SERVICE_WISE",
                  "code": "",
                  "chartType": "donut",
                  "filter": "",
                  "headers": []
                }
              ]
            },
            {
              "id": 122,
              "name": "NATIONAL_DSS_TOP_3_PERFORMING_STATES_TARGET_ACHIEVEMENT",
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
                  "id": "topPerformingStatesOverview",
                  "name": "NATIONAL_DSS_TOP_3_PERFORMING_STATES_TARGET_ACHIEVEMENT",
                  "code": "",
                  "chartType": "bar",
                  "filter": "",
                  "headers": []
                }
              ]
            },
            {
              "id": 123,
              "name": "NATIONAL_DSS_BOTTOM_3_PERFORMING_STATES_TARGET_ACHIEVEMENT",
              "dimensions": {
                "height": 250,
                "width": 4
              },
              "vizType": "performing-metric",
              "noUnit": false,
              "isCollapsible": false,
              "charts": [
                {
                  "id": "bottomPerformingStatesOverview",
                  "name": "NATIONAL_DSS_BOTTOM_3_PERFORMING_STATES_TARGET_ACHIEVEMENT",
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
          "name": "NATIONAL_DSS_SERVICE",
          "vizArray": [
            {
              "id": 131,
              "name": "NATIONAL_DSS_OVERVIEW",
              "dimensions": {
                "height": 450,
                "width": 5
              },
              "vizType": "metric-collection",
              "isCollapsible": false,
              "label": "",
              "charts": [
                {
                  "id": "totalApplicationsOverview",
                  "name": "NATIONAL_DSS_TOTAL_APPLICATION",
                  "code": "",
                  "chartType": "metric",
                  "filter": "",
                  "headers": []
                },
                {
                  "id": "closedApplicationOverview",
                  "name": "NATIONAL_DSS_CLOSED_APPLICATION",
                  "code": "",
                  "chartType": "metric",
                  "filter": "",
                  "headers": []
                },
                {
                  "id": "slaAchievedOverview",
                  "name": "NATIONAL_DSS_SLA_ACHIEVED",
                  "code": "",
                  "chartType": "metric",
                  "filter": "",
                  "headers": []
                },
                {
                  "id": "citizenRegisteredOverview",
                  "name": "NATIONAL_DSS_CITIZEN_REGISTERED",
                  "code": "",
                  "chartType": "metric",
                  "filter": "",
                  "headers": []
                }
              ]
            },
            {
              "id": 132,
              "name": "NATIONAL_DSS_TOTAL_APPLICATION_&_CLOSED_APPLICATION",
              "dimensions": {
                "height": 450,
                "width": 7
              },
              "vizType": "chart",
              "isCollapsible": false,
              "charts": [
                {
                  "id": "totalApplication&ClosedApplicationOverview",
                  "name": "NATIONAL_DSS_TOTAL_APPLICATION_&_CLOSED_APPLICATION",
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
          "row": 4,
          "name": "NATIONAL_DSS_SERVICE",
          "vizArray": [
                {
              "id": 141,
              "name": "NATIONAL_DSS_TOTAL_APPLICATIONS_SERVICE_WISE",
              "dimensions": {
                "height": 250,
                "width": 4
              },
              "vizType": "chart",
              "isCollapsible": false,
              "charts": [
                {
                  "id": "totalApplicationServiceWiseOverview",
                  "name": "NATIONAL_DSS_TOTAL_APPLICATIONS_SERVICE_WISE",
                  "code": "",
                  "chartType": "donut",
                  "filter": "",
                  "headers": []
                }
              ]
            },
            {
              "id": 142,
              "name": "NATIONAL_DSS_TOP_3_PERFORMING_STATES_COMPLETION_RATE",
              "dimensions": {
                "height": 250,
                "width": 4
              },
              "vizType": "performing-metric",
              "isCollapsible": false,
              "label": "",
              "charts": [
                {
                  "id": "topPerformingStatesCompletionRateOverview",
                  "name": "NATIONAL_DSS_TOP_3_PERFORMING_STATES_COMPLETION_RATE",
                  "code": "",
                  "chartType": "bar",
                  "filter": "",
                  "headers": []
                }
              ]
            },
            {
              "id": 143,
              "name": "NATIONAL_DSS_BOTTOM_3_PERFORMING_STATES_COMPLETION_RATE",
              "dimensions": {
                "height": 250,
                "width": 4
              },
              "vizType": "performing-metric",
              "isCollapsible": false,
              "charts": [
                {
                  "id": "bottomPerformingStatesCompletionRateOverview",
                  "name": "NATIONAL_DSS_BOTTOM_3_PERFORMING_STATES_COMPLETION_RATE",
                  "code": "",
                  "chartType": "bar",
                  "filter": "",
                  "headers": []
                }
              ]
            }
          ]
        }
      ]
    }

```

**Role Dashboard Mappings Configuration -** Master Dashboard Configuration which was explained earlier hold the list of Dashboards which are available.

Given the instance where Role Action Mapping is not maintained in the Application Service, this configuration will act as Role - Dashboard Mapping Configuration&#x20;

In this, each Role is mapped against the Dashboard which they are authorized to see

This was used earlier when the Role Action Mapping of eGov was not integrated.

Later, when the Role Action Mapping started controlling the Dashboards to be seen on the client side, this configuration was just used to enable the Dashboards for viewing.&#x20;

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
          "name": "National Overview",
          "id": "national-overview"
        }
      ]
    }

  ]
}
```

[Click here to check the configuration](https://github.com/egovernments/configs/blob/qa/egov-dss-dashboards/dashboard-analytics/RoleDashboardMappingsConf.json)

&#x20;**MDMS Configuration to be added:** _common-masters/uiCommonConstants.json_

```
"national-overview": {
                  "routePath": "/dashboard/national-overview",
                  "isOrigin": true
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
    }

```

[Click here to check the complete configuration](https://github.com/egovernments/egov-mdms-data/blob/QA/data/pb/ACCESSCONTROL-ROLEACTIONS/roleactions.json)

Action test.json:

```
{
      "id": {{PlaceHolder1}},
      "name": "Dashboard National Overview",
      "url": "/dashboard-analytics/dashboard/getDashboardConfig/national-overview",
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
      "name": "Dashboard National Overview",
      "url": "url",
      "displayName": "National Overview",
      "orderNumber": 2,
      "parentModule": "ndss-dashboard",
      "enabled": true,
      "serviceCode": "NDSS",
      "code": "null",
      "path": "NatDashboard.Overview",
      "navigationURL": "/digit-ui/employee/dss/dashboard/national-overview",
      "leftIcon": "places:business-center",
      "rightIcon": ""
    }
```

[Click here to check the complete configuration](https://github.com/egovernments/egov-mdms-data/blob/QA/data/pb/ACCESSCONTROL-ACTIONS-TEST/actions-test.json)

Overview Page-National DSS Consists of multiple graphs which represent the aggregated data for multiple services . Each graph has its own configuration which will describe the chart and its type.

National DSS Consists of following charts in Overview Page:

**Revenue Tab**

* Overview
* Total Cumulative Collection
* Total Cumulative Collection (Service Wise)
* Top 3 States By Performance
* Bottom 3 States by Performance

**Service Tab**

* Overview
* Total & Closed Applications
* Total Applications(Service Wise)
* Top 3 Performing States By Completion
* Bottom 3 Performing States By Completion

**Revenue Tab**&#x20;

**Overview -** Overview graph contains multiple data information as below in the selected time period.

* **Collection on :** This represents the aggregated data of today’s collection amount from the module PropertyTax, TradeLicense, Water\&Sewerage, FireNoc, OBPS, MCollect.
* &#x20;**Total Collection :** This represents the aggregated total collection amount from the module PropertyTax, TradeLicense, Water\&Sewerage, FireNoc, OBPS, MCollect.
* **Target Collection :** This represents the aggregated target collection amount from the module, PropertyTax, TradeLicense, Water\&Sewerage.
* **Target Achievement :** This represents the aggregated target achieved in percentage. This is calculated by formula- (Total Collection(PT, TL, W\&S)/Target Collection(PT, TL, W\&S))\*100%

![](<../../../../.gitbook/assets/image (123).png>)

**Total Cumulative Collection -** This Graph contains aggregated amount of the module PropertyTax, TradeLicense, Water\&Sewerage, FireNoc, OBPS, MCollect. Collection amount information in the monthly base as a cumulative line graph. This will change as per the denomination amount filter selection.

**line** - this graph/chart is data representation on date histograms or date groupings.

![](<../../../../.gitbook/assets/image (278).png>)

**Total Cumulative Collection (Service Wise) -** This Graph Represents the Module Wise Collection for the given period of time.

Modules are: PropertyTax, TradeLicense, Water\&Sewerage, FireNoc, OBPS, MCollect.

![](<../../../../.gitbook/assets/image (256).png>)

**Top 3 Performing States By Performance -** This graph represents the States based on the aggregated Target achieved from the modules PropertyTax, TradeLicense, Water\&Sewerage in bar chart representation with the % of target achieved in descending order.

![](<../../../../.gitbook/assets/image (328).png>)

**Bottom 3 Performing States By Performance -** This graph represents the States based on the aggregated Target achieved from the modules PropertyTax, TradeLicense, Water\&Sewerage in bar chart representation with the % of target achieved in ascending order.

![](<../../../../.gitbook/assets/image (150).png>)



**Service Tab**

**Overview -** Overview graph contains multiple data information as below in the selected time period.

* **Total Applications :** This represents the aggregated total number of Applications entered from the modules PropertyTax, TradeLicense, Water\&Sewerage, FireNoc, OBPS.
* **Closed Applications:** This represents the aggregated total number of Applications closed from the modules PropertyTax, TradeLicense, Water\&Sewerage, FireNoc, OBPS.
* **SLA Achievement :** This represents the total no of applications closed within time from common-index across the modules.
* **Citizen Registered:** This represents the total no of Citizen Registered from common-index across the modules.

![](<../../../../.gitbook/assets/image (200).png>)

**Total & Closed Applications -** This line chart represents Total and closed applications graph month wise (non cumulative) aggregated data lines from the modules PropertyTax, TradeLicense, Water\&Sewerage, FireNoc, OBPS.

![](<../../../../.gitbook/assets/image (222).png>)

**Total Applications(Service Wise) -** This Graph Represents the Module Wise Application Registerd.

Modules are: PropertyTax, TradeLicense, Water\&Sewerage, FireNoc, OBPS.

![](<../../../../.gitbook/assets/image (253).png>)

**Top 3 Performing States By Completion -** This graph represents the States based on the aggregated data by application closed within SLA from the modules PropertyTax, TradeLicense, Water\&Sewerage, OBPS and Firenoc in bar chart representation with the % of completion in descending order.

![](<../../../../.gitbook/assets/image (265).png>)

**Bottom 3 Performing States By Completion -** This graph represents the States based on the aggregated data by application closed within SLA from the modules PropertyTax, TradeLicense, Water\&Sewerage, OBPS and Firenoc in bar chart representation with the % of completion in ascending order.

![](<../../../../.gitbook/assets/image (299).png>)





![](blob:https://digit-discuss.atlassian.net/6dd96673-ca3d-4c5b-bd62-77518aa02e43#media-blob-url=true\&id=3041198f-560f-4a43-8964-08ab7bc0f0dc\&collection=contentId-2055503921\&contextId=2055503921\&height=487\&width=494\&alt=)\
