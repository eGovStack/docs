---
description: Technical Document
---

# Property Tax - National Dashboard

## Overview

NDSS has two sides to it. One is the process in which the data is pooled to the ElasticSearch and the other is the way it is fetched, aggregated, computed, transformed and sent across.

As this revolves around a variety of data sets, there is a need for making this configurable. This ensures that the process can be configured easily in case a new scenario is introduced.&#x20;

This document walks us through the steps on how to define the configurations for DSS analytics for Property Tax module.

## Key Concepts

**Analytics:** A microservice responsible for building, fetching, aggregating and computing the Data on ElasticSearch to a consumable data response. This is later used for visualizations and graphical representations.&#x20;

**Analytics Configurations:** Analytics contains multiple configurations. We need to add the changes related to National Dashboard in this dashboard analytics.\
Dashboard analytics configuration file path: [<img src="https://github.com/fluidicon.png" alt="" data-size="line">configs/egov-dss-dashboards/dashboard-analytics at qa · egovernments/configs](https://github.com/egovernments/configs/tree/qa/egov-dss-dashboards/dashboard-analytics)\
Below is a list of configurations that need to be changed to run the National Dashboard successfully.

1. Chart API Configuration
2. Master Dashboard Configuration
3. Role Dashboard Mappings Configuration

**Chart API Configuration:** Each visualization has its own properties. Each visualization comes from different data sources (sometimes it is a combination of different data sources). In order to configure each visualization and its properties, we have a Chart API Configuration Document.

In this, Visualization Code, which happens to be the key, has its properties configured as a part of the configuration and is easily changeable.&#x20;

Sample ChartApiConfiguration.json data for the Property Tax below.

```
"_comment": "NSS-PROPERTYTAX",
   
 	"todaysCollectionv3": {
    "chartName": "NATIONAL_DSS_TODAYS_COLLECTION",
    "queries": [
      {
        "module": "PT",
        "dateRefField": "",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "indexName": "pt-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"todaysDate\":{\"terms\":{\"field\":\"date\",\"order\":{\"_term\":\"desc\"},\"size\":1},\"aggs\":{\"Todays Collection\":{\"sum\":{\"field\":\"todaysCollectionForUsageCategory\"}}}},\"lastUpdatedTime\":{\"terms\":{\"field\":\"lastModifiedTime\",\"order\":{\"_term\":\"desc\"},\"size\":1}}}}}}"
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
      
    },
    "_comment": " "
  },
 	
 	"totalCollectionv3": {
    "chartName": "NATIONAL_DSS_TOTAL_COLLECTION",
    "queries": [
      {
        "module": "PT",
        "dateRefField": "date",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "indexName": "pt-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"Total Collection\":{\"sum\":{\"field\":\"todaysCollectionForUsageCategory\"}}}}}}"
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
      "chartResponseMap" : "totalCollectionv3",
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
 	
 	"targetCollectionv3": {
    "chartName": "NATIONAL_DSS_TARGET_COLLECTION",
    "queries": [
      {
        "module": "MASTER",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "dateRefField": "date",
        "indexName": "master-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must\":[{\"term\":{\"module.keyword\":\"PT\"}}]}},\"aggs\":{\"Target Collection\":{\"sum\":{\"field\":\"budgetProposedForMunicipalCorporation\"}}}}}}"
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
      "chartResponseMap" : "targetCollectionv3",
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
  	
  	"targetAchievedv3": {
    "chartName": "NATIONAL_DSS_TARGET_ACHIEVED",
    "queries": [
      {
        "module": "MASTER",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "dateRefField": "date",
        "indexName": "master-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must\":[{\"term\":{\"module.keyword\":\"PT\"}}]}},\"aggs\":{\"Actual collection\":{\"sum\":{\"field\":\"budgetProposedForMunicipalCorporation\"}}}}}}"
      },
      {
        "module": "PT",
        "dateRefField": "date",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "indexName": "pt-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"Total Collection\":{\"sum\":{\"field\":\"todaysCollectionForUsageCategory\"}}}}}}"
      }

    ],
    "chartType": "metric",
    "valueType": "percentage",
    "drillChart": "none",
    "documentType": "_doc",
    "action": "percentage",
    "isRoundOff": true,
    "preActionTheory":{
      "Actual collection":"repsonseToDifferenceOfDates"
    },
    "aggregationPaths": [
      "Total Collection",
      "Actual collection"
    ],
    "insight": {
      "chartResponseMap" : "targetAchievedv3",
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
  
  	"cumulativeCollectionv3": {
    "chartName": "NATIONAL_DSS_TOTAL_CUMULATIVE_COLLECTION",
    "queries": [
      {
        "module": "PT",
        "dateRefField": "date",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "indexName": "pt-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"Collections\":{\"date_histogram\":{\"field\":\"date\",\"interval\":\"intervalvalue\"},\"aggs\":{\"Sum\":{\"sum\":{\"field\":\"todaysCollectionForUsageCategory\"}}}}}}}}"
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
	
	"topPerformingStatesv3": {
    "chartName": "NATIONAL_DSS_PT_TOP_3_PERFORMING_STATES_TARGET_ACHIEVEMENT",
    "queries": [
      {
        "module": "MASTER",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "dateRefField": "date",
        "indexName": "master-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must\":[{\"term\":{\"module.keyword\":\"PT\"}}]}},\"aggs\":{\"Target Collection\":{\"terms\":{\"field\":\"state.keyword\",\"size\":\"200\",\"order\":{\"Sum\":\"desc\"}},\"aggs\":{\"Sum\":{\"sum\":{\"field\":\"budgetProposedForMunicipalCorporation\"}}}}}}}}"
      },
      {
        "module": "PT",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "dateRefField": "date",
        "indexName": "pt-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"Total Collection\":{\"terms\":{\"field\":\"state.keyword\",\"size\":\"200\",\"order\":{\"Sum\":\"desc\"}},\"aggs\":{\"Sum\":{\"sum\":{\"field\":\"todaysCollectionForUsageCategory\"}}}}}}}}"
      }
    ],
    "chartType": "perform",
    "valueType": "percentage",
    "drillChart": "none",
    "documentType": "_doc",
    "action": "percentage",
    "plotLabel": "NATIONAL_DSS_TARGET_ACHIEVED",
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
	
	"bottomPerformingStatesv3": {
    "chartName": "NATIONAL_DSS_PT_BOTTOM_3_PERFORMING_STATES_TARGET_ACHIEVEMENT",
    "queries": [
      {
        "module": "MASTER",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "dateRefField": "date",
        "indexName": "master-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must\":[{\"term\":{\"module.keyword\":\"PT\"}}]}},\"aggs\":{\"Target Collection\":{\"terms\":{\"field\":\"state.keyword\",\"size\":\"200\",\"order\":{\"Sum\":\"asc\"}},\"aggs\":{\"Sum\":{\"sum\":{\"field\":\"budgetProposedForMunicipalCorporation\"}}}}}}}}"
      },
      {
        "module": "PT",
       "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "dateRefField": "date",
        "indexName": "pt-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"Total Collection\":{\"terms\":{\"field\":\"state.keyword\",\"size\":\"200\",\"order\":{\"Sum\":\"asc\"}},\"aggs\":{\"Sum\":{\"sum\":{\"field\":\"todaysCollectionForUsageCategory\"}}}}}}}}"
      }
    ],
    "chartType": "perform",
    "valueType": "percentage",
    "drillChart": "none",
    "documentType": "_doc",
    "action": "percentage",
    "plotLabel": "NATIONAL_DSS_TARGET_ACHIEVED",
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
	
	"collectionByUsageTypev3": {
    "chartName": "NATIONAL_DSS_PT_COLLECTION_BY_USAGE_TYPE",
    "queries": [
      {
        "module": "PT",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "dateRefField": "date",
        "indexName": "pt-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"Usage Type\":{\"terms\":{\"field\":\"usageCategory.keyword\",\"size\":200},\"aggs\":{\"Amount Paid\":{\"sum\":{\"field\":\"todaysCollectionForUsageCategory\"}}}}}}}}"
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
    "_comment": " collection/amount per usage type"
  },

	"demandCollectionIndexStatesRevenuev3": {
    "chartName": "NATIONAL_DSS_PT_KEY_FY_INDICATORS",
    "queries": [
      {
        "module": "PT",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "dateRefField": "date",
        "indexName": "pt-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"state \":{\"terms\":{\"field\":\"state.keyword\",\"size\":200},\"aggs\":{\"PT_Total_Collection\":{\"sum\":{\"field\":\"todaysCollectionForUsageCategory\"}},\"PT_Transactions\":{\"sum\":{\"field\":\"transactionsForUsageCategory\"}},\"PT_Assessed_Properties\":{\"sum\":{\"field\":\"assessedPropertiesForUsageCategory\"}}}}}}}}"
      },
      {
        "module": "MASTER",
       "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "dateRefField": "date",
        "indexName": "master-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"state \":{\"terms\":{\"field\":\"state.keyword\",\"size\":200},\"aggs\":{\"PT_Target_Collection\":{\"filter\":{\"term\":{\"module.keyword\":\"PT\"}},\"aggs\":{\"sum\":{\"sum\":{\"field\":\"budgetProposedForMunicipalCorporation\"}}}}}}}}}}"
      }
    ],
    "isMdmsEnabled": false,
    "filterKeys": [
      {"key": "state", "column": "State"}
    ],
    "chartType": "xtable",
    "valueType": "number",
    "drillChart": "demandCollectionIndexUlbRevenuev3",
    "action": "",
    "plotLabel": "State",
    "isPostResponseHandler": true,
    "postAggregationTheory" : "repsonseToDifferenceOfDates",
    "aggregationPaths": [
      "PT_Total_Collection",
      "PT_Transactions",
      "PT_Assessed_Properties",
      "PT_Target_Collection"
    ],
     "computedFields": [
      {
        "postAggregationTheory" : "repsonseToDifferenceOfDates",
        "actionName": "AdditiveComputedField",
        "fields" : ["PT_Target_Collection"],
        "newField" : "Target_Collection_PT",
        "_comments": "fields are field names picked from its aggregation query to use post aggregation newField value with given new field name  "
      },
      {
        "postAggregationTheory" : "",
        "actionName": "PercentageComputedField",
        "fields" : ["PT_Total_Collection","Target_Collection_PT"],
        "newField" : "Target Achieved",
        "_comments": "fields are field names picked from its aggregation query to use post aggregation newField value with given new field name  "
      }
    ],
    "excludedColumns":["PT_Target_Collection"],
    "pathDataTypeMapping": [
      {
        "PT_Total_Collection": "amount"
      },
      {
        "PT_Transactions": "number"
      },
      {
        "PT_Assessed_Properties": "number"
      },
      {
        "PT_Target_Collection": "amount"
      },
      {
      	"Target Achieved" : "percentage"
      },
      {
         "Target_Collection_PT": "amount"
      }
    ],
    "insight": {
    },
    "_comment": ""
  },
	
	"demandCollectionIndexUlbRevenuev3": {
    "chartName": "NATIONAL_DSS_PT_DEMAND_COLLECTION_ULB",
    "queries": [
       {
        "module": "PT",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "dateRefField": "date",
        "indexName": "pt-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"ulb \":{\"terms\":{\"field\":\"ulb.keyword\",\"size\":200},\"aggs\":{\"PT_Total_Collection\":{\"sum\":{\"field\":\"todaysCollectionForUsageCategory\"}},\"PT_Transactions\":{\"sum\":{\"field\":\"transactionsForUsageCategory\"}},\"PT_Assessed_Properties\":{\"sum\":{\"field\":\"assessedPropertiesForUsageCategory\"}}}}}}}}"
      },
      {
        "module": "MASTER",
       "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "dateRefField": "date",
        "indexName": "master-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"ulb \":{\"terms\":{\"field\":\"ulb.keyword\",\"size\":200},\"aggs\":{\"PT_Target_Collection\":{\"filter\":{\"term\":{\"module.keyword\":\"PT\"}},\"aggs\":{\"sum\":{\"sum\":{\"field\":\"budgetProposedForMunicipalCorporation\"}}}}}}}}}}"
      }
    ],
    "filterKeys": [
      {"key": "ulb", "column": "Ulb"}
    ],
    "postAggregationTheory" : "repsonseToDifferenceOfDates",    
    "chartType": "xtable",
    "valueType": "number",
    "drillChart": "demandCollectionIndexWardRevenuev3",
    "drillFields": [
      "ward",
      ""
    ],
    "documentType": "_doc",
    "action": "",
    "plotLabel": "Ulb",
    "aggregationPaths": [ 
      "PT_Total_Collection",
      "PT_Transactions",
      "PT_Assessed_Properties",
      "PT_Target_Collection"
    ],
     "computedFields": [
      {
        "postAggregationTheory" : "repsonseToDifferenceOfDates",
        "actionName": "AdditiveComputedField",
        "fields" : ["PT_Target_Collection"],
        "newField" : "Target_Collection_PT",
        "_comments": "fields are field names picked from its aggregation query to use post aggregation newField value with given new field name  "
      },
      {
        "postAggregationTheory" : "",
        "actionName": "PercentageComputedField",
        "fields" : ["PT_Total_Collection","Target_Collection_PT"],
        "newField" : "Target Achieved",
        "_comments": "fields are field names picked from its aggregation query to use post aggregation newField value with given new field name  "
      }
    ],
    "excludedColumns":["PT_Target_Collection"],
    "pathDataTypeMapping": [
      {
        "PT_Total_Collection": "amount"
      },
      {
        "PT_Transactions": "number"
      },
      {
        "PT_Assessed_Properties": "number"
      },
      {
        "PT_Target_Collection": "amount"
      },
      {
      	"Target Achieved" : "percentage"
      },
      {
      	"Target_Collection_PT" : "amount"
      }
    ],
    "insight": {
    },
    "_comment": ""
  },
  	
  	"demandCollectionIndexWardRevenuev3": {
    "chartName": "NATIONAL_DSS_PT_DEMAND_COLLECTION_WARD",
    "queries": [
       {
        "module": "PT",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\", \"ward\" : \"ward.keyword\"}",
        "dateRefField": "date",
        "indexName": "pt-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"ward \":{\"terms\":{\"field\":\"ward.keyword\",\"size\":200},\"aggs\":{\"PT_Total_Collection\":{\"sum\":{\"field\":\"todaysCollectionForUsageCategory\"}},\"PT_Transactions\":{\"sum\":{\"field\":\"transactionsForUsageCategory\"}},\"PT_Assessed_Properties\":{\"sum\":{\"field\":\"assessedPropertiesForUsageCategory\"}}}}}}}}"
      },
      {
        "module": "MASTER",
       "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\", \"ward\" : \"ward.keyword\"}",
        "dateRefField": "date",
        "indexName": "master-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"ward \":{\"terms\":{\"field\":\"ward.keyword\",\"size\":200},\"aggs\":{\"PT_Target_Collection\":{\"filter\":{\"term\":{\"module.keyword\":\"PT\"}},\"aggs\":{\"sum\":{\"sum\":{\"field\":\"budgetProposedForMunicipalCorporation\"}}}}}}}}}}"
      }
    ],
    "filterKeys": [
    ],
    "postAggregationTheory" : "repsonseToDifferenceOfDates",    
    "chartType": "xtable",
    "valueType": "number",
    "drillChart": "",
    "documentType": "_doc",
    "action": "",
    "plotLabel": "Ward",
    "aggregationPaths": [
      "PT_Total_Collection",
      "PT_Transactions",
      "PT_Assessed_Properties",
      "PT_Target_Collection"
    ],
     "computedFields": [
      {
        "postAggregationTheory" : "repsonseToDifferenceOfDates",
        "actionName": "AdditiveComputedField",
        "fields" : ["PT_Target_Collection"],
        "newField" : "Target_Collection_PT",
        "_comments": "fields are field names picked from its aggregation query to use post aggregation newField value with given new field name  "
      },
      {
        "postAggregationTheory" : "",
        "actionName": "PercentageComputedField",
        "fields" : ["PT_Total_Collection","Target_Collection_PT"],
        "newField" : "Target Achieved",
        "_comments": "fields are field names picked from its aggregation query to use post aggregation newField value with given new field name  "
      }
    ],
    "excludedColumns":["PT_Target_Collection"],
    "pathDataTypeMapping": [
      {
        "PT_Total_Collection": "amount"
      },
      {
        "PT_Transactions": "number"
      },
      {
        "PT_Assessed_Properties": "number"
      },
      {
        "PT_Target_Collection": "amount"
      },
      {
      	"Target Achieved" : "percentage"
      },
      {
        "Target_Collection_PT": "amount"
      }
    ],
    "insight": {
    },
    "_comment": ""
  },
  
	"demandCollectionIndexUsageRevenuev3": {
    "chartName": "NATIONAL_DSS_PT_DEMAND_COLLECTION_USAGETYPE",
    "queries": [
      {
        "module": "PT",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "dateRefField": "date",
        "indexName": "pt-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"UsageType \":{\"terms\":{\"field\":\"usageCategory.keyword\",\"size\":200},\"aggs\":{\"PT_Total_Collection\":{\"filter\":{\"term\":{\"module.keyword\":\"PT\"}},\"aggs\":{\"top_tags_per_comment\":{\"sum\":{\"field\":\"todaysCollectionForUsageCategory\"}}}},\"PT_Transactions\":{\"filter\":{\"term\":{\"module.keyword\":\"PT\"}},\"aggs\":{\"txn\":{\"sum\":{\"field\":\"transactionsForUsageCategory\"}}}},\"PT_Assessed_Properties\":{\"filter\":{\"term\":{\"module.keyword\":\"PT\"}},\"aggs\":{\"assessedProperties\":{\"sum\":{\"field\":\"assessedPropertiesForUsageCategory\"}}}}}}}}}}"
      }
    ],
    "filterKeys": [

    ],
    "chartType": "table",
    "valueType": "number",
    "drillChart": "",
    "drillFields": [
      "ward",
      ""
    ],
    "documentType": "_doc",
    "action": "",
    "plotLabel": "Usage Type",
    "aggregationPaths": [
      "PT_Total_Collection",
      "PT_Transactions",
      "PT_Assessed_Properties"

    ],
    "pathDataTypeMapping": [
      {
        "PT_Total_Collection": "amount"
      },
      {
        "PT_Transactions": "number"
      },
      {
        "PT_Assessed_Properties": "number"
      }
    ],
    "insight": {
    },
    "_comment": ""
  },
  	
  	"taxHeadsBreakupStatesRevenuev3": {
    "chartName": "NATIONAL_DSS_PT_TAX_HEAD_BREAKUP_REVENUE_STATES",
    "queries": [
      {
        "module": "PT",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "dateRefField": "date",
      	"indexName": "pt-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"State \":{\"terms\":{\"field\":\"state.keyword\",\"size\":200},\"aggs\":{\"PT_Total_Amount\":{\"sum\":{\"field\":\"todaysCollectionForUsageCategory\"}},\"PT_Tax\":{\"filter\":{\"term\":{\"module.keyword\":\"PT\"}},\"aggs\":{\"amount\":{\"sum\":{\"field\":\"propertyTaxForUsageCategory\"}}}},\"PT_Cess\":{\"filter\":{\"term\":{\"module.keyword\":\"PT\"}},\"aggs\":{\"amount\":{\"sum\":{\"field\":\"cessForUsageCategory\"}}}},\"PT_Rebate\":{\"filter\":{\"term\":{\"module.keyword\":\"PT\"}},\"aggs\":{\"amount\":{\"sum\":{\"field\":\"rebateForUsageCategory\"}}}},\"PT_Penalty\":{\"filter\":{\"term\":{\"module.keyword\":\"PT\"}},\"aggs\":{\"amount\":{\"sum\":{\"field\":\"penaltyForUsageCategory\"}}}},\"PT_Interest\":{\"filter\":{\"term\":{\"module.keyword\":\"PT\"}},\"aggs\":{\"amount\":{\"sum\":{\"field\":\"interestForUsageCategory\"}}}}}}}}}}"

      }
    ],
    "isMdmsEnabled": false,
    "filterKeys": [
      {"key": "state", "column": "State"}

    ],
    "chartType": "xtable",
    "valueType": "number",
    "drillChart": "taxHeadsBreakupUlbRevenuev3",
    "isPostResponseHandler": true,
    "documentType": "_doc",
    "action": "",
    "plotLabel": "State",
    "aggregationPaths": [
      "PT_Tax",
      "PT_Cess",
      "PT_Rebate",
      "PT_Penalty",
      "PT_Interest"
    ],
    "computedFields": [
      {
        "postAggregationTheory" : "",
        "actionName": "AdditiveComputedField",
        "fields" : [ "PT_Tax", "PT_Cess", "PT_Rebate", "PT_Penalty", "PT_Interest"],
        "newField" : "PT_Total_Amount",
        "_comments": "fields are field names picked from its aggregation query to use post aggregation newField value with given new field name  "
      }
    ],
    "pathDataTypeMapping": [
      {
        "PT_Total_Amount": "amount"
      },
      {
        "PT_Tax": "amount"
      },
      {
        "PT_Cess": "amount"
      },
      {
        "PT_Rebate": "amount"
      },
      {
        "PT_Penalty": "amount"
      },
      {
        "PT_Interest": "amount"
      }
    ],
    "insight": {
    },
    "_comment": ""
  },

	"taxHeadsBreakupUlbRevenuev3": {
    "chartName": "NATIONAL_DSS_PT_TAX_HEAD_BREAKUP_REVENUE_ULB",
    "queries": [
      {
        "module": "PT",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "dateRefField": "date",
        "indexName": "pt-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"State \":{\"terms\":{\"field\":\"ulb.keyword\",\"size\":200},\"aggs\":{\"PT_Total_Amount\":{\"sum\":{\"field\":\"todaysCollectionForUsageCategory\"}},\"PT_Tax\":{\"filter\":{\"term\":{\"module.keyword\":\"PT\"}},\"aggs\":{\"amount\":{\"sum\":{\"field\":\"propertyTaxForUsageCategory\"}}}},\"PT_Cess\":{\"filter\":{\"term\":{\"module.keyword\":\"PT\"}},\"aggs\":{\"amount\":{\"sum\":{\"field\":\"cessForUsageCategory\"}}}},\"PT_Rebate\":{\"filter\":{\"term\":{\"module.keyword\":\"PT\"}},\"aggs\":{\"amount\":{\"sum\":{\"field\":\"rebateForUsageCategory\"}}}},\"PT_Penalty\":{\"filter\":{\"term\":{\"module.keyword\":\"PT\"}},\"aggs\":{\"amount\":{\"sum\":{\"field\":\"penaltyForUsageCategory\"}}}},\"PT_Interest\":{\"filter\":{\"term\":{\"module.keyword\":\"PT\"}},\"aggs\":{\"amount\":{\"sum\":{\"field\":\"interestForUsageCategory\"}}}}}}}}}}"
      }
    ],
    "filterKeys": [
      {"key": "ulb", "column": "Ulb"}

    ],
    "chartType": "xtable",
    "valueType": "number",
    "drillChart": "taxHeadsBreakupWardRevenuev3",
    "drillFields": [
      "ward",
      ""
    ],
    "documentType": "_doc",
    "action": "",
    "plotLabel": "Ulb",
    "aggregationPaths": [
      "PT_Tax",
      "PT_Cess",
      "PT_Rebate",
      "PT_Penalty",
      "PT_Interest"
    ],
	 "computedFields": [
      {
        "postAggregationTheory" : "",
        "actionName": "AdditiveComputedField",
        "fields" : ["PT_Tax", "PT_Cess", "PT_Rebate", "PT_Penalty", "PT_Interest"],
        "newField" : "PT_Total_Amount",
        "_comments": "fields are field names picked from its aggregation query to use post aggregation newField value with given new field name  "
      }
    ],
    "pathDataTypeMapping": [
      {
        "PT_Total_Amount": "amount"
      },
      {
        "PT_Tax": "amount"
      },
      {
        "PT_Cess": "amount"
      },
      {
        "PT_Rebate": "amount"
      },
      {
        "PT_Penalty": "amount"
      },
      {
        "PT_Interest": "amount"
      }
    ],
    "insight": {
    },
    "_comment": ""
  },
	
	"taxHeadsBreakupWardRevenuev3": {
    "chartName": "National Tax head Breakup Ward",
    "queries": [
      {
      	"module": "PT",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "dateRefField": "date",
        "indexName": "pt-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"State \":{\"terms\":{\"field\":\"ward.keyword\",\"size\":200},\"aggs\":{\"PT_Total_Amount\":{\"sum\":{\"field\":\"todaysCollectionForUsageCategory\"}},\"PT_Tax\":{\"filter\":{\"term\":{\"module.keyword\":\"PT\"}},\"aggs\":{\"amount\":{\"sum\":{\"field\":\"propertyTaxForUsageCategory\"}}}},\"PT_Cess\":{\"filter\":{\"term\":{\"module.keyword\":\"PT\"}},\"aggs\":{\"amount\":{\"sum\":{\"field\":\"cessForUsageCategory\"}}}},\"PT_Rebate\":{\"filter\":{\"term\":{\"module.keyword\":\"PT\"}},\"aggs\":{\"amount\":{\"sum\":{\"field\":\"rebateForUsageCategory\"}}}},\"PT_Penalty\":{\"filter\":{\"term\":{\"module.keyword\":\"PT\"}},\"aggs\":{\"amount\":{\"sum\":{\"field\":\"penaltyForUsageCategory\"}}}},\"PT_Interest\":{\"filter\":{\"term\":{\"module.keyword\":\"PT\"}},\"aggs\":{\"amount\":{\"sum\":{\"field\":\"interestForUsageCategory\"}}}}}}}}}}"
      }
    ],
    "filterKeys": [

    ],
    "chartType": "xtable",
    "valueType": "number",
    "drillChart": "",
    "drillFields": [
      "ward",
      ""
    ],
    "documentType": "_doc",
    "action": "",
    "plotLabel": "Ward",
    "aggregationPaths": [
      "PT_Tax",
      "PT_Cess",
      "PT_Rebate",
      "PT_Penalty",
      "PT_Interest"
    ],
	 "computedFields": [
      {
        "postAggregationTheory" : "",
        "actionName": "AdditiveComputedField",
        "fields" : [ "PT_Tax", "PT_Cess", "PT_Rebate", "PT_Penalty", "PT_Interest"],
        "newField" : "PT_Total_Amount",
        "_comments": "fields are field names picked from its aggregation query to use post aggregation newField value with given new field name  "
      }
    ],
    "pathDataTypeMapping": [
      {
        "PT_Total_Amount": "amount"
      },
      {
        "PT_Tax": "amount"
      },
      {
        "PT_Cess": "amount"
      },
      {
        "PT_Rebate": "amount"
      },
      {
        "PT_Penalty": "amount"
      },
      {
        "PT_Interest": "amount"
      }
    ],
    "insight": {
    },
    "_comment": ""
  },

 	"taxHeadsBreakupUsagev3": {
    "chartName": "NATIONAL_DSS_PT_TAX_HEAD_BREAKUP_USAGE",
    "queries": [
      {
        "module": "PT",
       	"requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "dateRefField": "date",
        "indexName": "pt-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"usage \":{\"terms\":{\"field\":\"usageCategory.keyword\",\"size\":200},\"aggs\":{\"PT_Total_Amount\":{\"sum\":{\"field\":\"todaysCollectionForUsageCategory\"}},\"PT_Tax\":{\"filter\":{\"term\":{\"module.keyword\":\"PT\"}},\"aggs\":{\"amount\":{\"sum\":{\"field\":\"propertyTaxForUsageCategory\"}}}},\"PT_Cess\":{\"filter\":{\"term\":{\"module.keyword\":\"PT\"}},\"aggs\":{\"amount\":{\"sum\":{\"field\":\"cessForUsageCategory\"}}}},\"PT_Rebate\":{\"filter\":{\"term\":{\"module.keyword\":\"PT\"}},\"aggs\":{\"amount\":{\"sum\":{\"field\":\"rebateForUsageCategory\"}}}},\"PT_Penalty\":{\"filter\":{\"term\":{\"module.keyword\":\"PT\"}},\"aggs\":{\"amount\":{\"sum\":{\"field\":\"penaltyForUsageCategory\"}}}},\"PT_Interest\":{\"filter\":{\"term\":{\"module.keyword\":\"PT\"}},\"aggs\":{\"amount\":{\"sum\":{\"field\":\"interestForUsageCategory\"}}}}}}}}}}"
      }
    ],
    "filterKeys": [

    ],
    "chartType": "table",
    "valueType": "number",
    "drillChart": "",
    "documentType": "_doc",
    "action": "",
    "plotLabel": "Usage Type",
    "aggregationPaths": [
      "PT_Total_Amount",
      "PT_Tax",
      "PT_Cess",
      "PT_Rebate",
      "PT_Penalty",
      "PT_Interest"
    ],
    "pathDataTypeMapping": [
      {
        "PT_Total_Amount": "amount"
      },
      {
        "PT_Tax": "amount"
      },
      {
        "PT_Cess": "amount"
      },
      {
        "PT_Rebate": "amount"
      },
      {
        "PT_Penalty": "amount"
      },
      {
        "PT_Interest": "amount"
      }
    ],
    "insight": {
    },
    "_comment": ""
  },
	     
    "totalApplicationsv3": {
    "chartName": "NATIONAL_DSS_PT_TOTAL_APPLICATIONS",
    "queries": [
      {
        "module": "PT",
        "indexName": "pt-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"state\":{\"terms\":{\"field\":\"state.keyword\"},\"aggs\":{\"intermediateAggrULB\":{\"terms\":{\"field\":\"ulb.keyword\"},\"aggs\":{\"intermediateAggrWard\":{\"terms\":{\"field\":\"ward.keyword\"},\"aggs\":{\"days\":{\"terms\":{\"field\":\"date\"},\"aggs\":{\"applications\":{\"avg\":{\"field\":\"todaysTotalApplications\"}}}},\"wardapplications\":{\"sum_bucket\":{\"buckets_path\":\"days.applications\"}}}},\"ulbApplications\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrWard.wardapplications\"}}}},\"stateApplications\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrULB.ulbApplications\"}}}},\"Total Applications\":{\"sum_bucket\":{\"buckets_path\":\"state.stateApplications\"}}}}}}",
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
      "Total Applications"
    ],
    "insight": {
      "chartResponseMap" : "totalApplicationsv3",
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
    
    
    "totalPropertiesv3": {
    "chartName": "NATIONAL_DSS_PT_TOTAL_PROPERTIES",
    "queries": [
      {
        "module": "PT",
        "indexName": "pt-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"Total Application\":{\"sum\":{\"field\":\"propertiesRegisteredForFinancialYear\"}}}}}}",
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
      "Total Application"
    ],
    "insight": {
      "chartResponseMap" : "totalPropertiesv3",
      "action" : "differenceOfNumbers",
      "upwardIndicator" : "positive",
      "downwardIndicator" : "negative",
      "textMessage" : "$indicator$value% than last $insightInterval",
      "colorCode" : "#228B22",
      "insightInterval" : "year",
      "isRoundOff": true
    },
    "_comment": " totol properties count"
  },

	"propertiesAssessedv3": {
    "chartName": "NATIONAL_PT_TOTAL_PROPERTIES_ASSESSED",
    "queries": [
      {
        "module": "PT",
        "indexName": "pt-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"Assessed Properties\":{\"sum\":{\"field\":\"assessedPropertiesForUsageCategory\"}}}}}}",
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
      "Assessed Properties"
    ],
    "insight": {
      "chartResponseMap" : "propertiesAssessedv3",
      "action" : "differenceOfNumbers",
      "upwardIndicator" : "positive",
      "downwardIndicator" : "negative",
      "textMessage" : "$indicator$value% than last $insightInterval",
      "colorCode" : "#228B22",
      "insightInterval" : "year",
      "isRoundOff": true
    },
    "_comment": " totol properties having assessmentNumber "
  },
	
	"totalAssessmentv3": {
    "chartName": "NATIONAL_DSS_PT_TOTAL_ASSESSMENTS",
    "queries": [
      {
        "module": "PT",
        "indexName": "pt-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"state\":{\"terms\":{\"field\":\"state.keyword\"},\"aggs\":{\"intermediateAggrULB\":{\"terms\":{\"field\":\"ulb.keyword\"},\"aggs\":{\"intermediateAggrWard\":{\"terms\":{\"field\":\"ward.keyword\"},\"aggs\":{\"days\":{\"terms\":{\"field\":\"date\"},\"aggs\":{\"applications\":{\"avg\":{\"field\":\"assessments\"}}}},\"wardapplications\":{\"sum_bucket\":{\"buckets_path\":\"days.applications\"}}}},\"ulbApplications\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrWard.wardapplications\"}}}},\"stateApplications\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrULB.ulbApplications\"}}}},\"Total Assessments\":{\"sum_bucket\":{\"buckets_path\":\"state.stateApplications\"}}}}}}",
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
      "Total Assessments"
    ],
    "insight": {
      "chartResponseMap" : "totalAssessmentv3",
      "action" : "differenceOfNumbers",
      "upwardIndicator" : "positive",
      "downwardIndicator" : "negative",
      "textMessage" : "$indicator$value% than last $insightInterval",
      "colorCode" : "#228B22",
      "insightInterval" : "year",
      "isRoundOff": true
    },
    "_comment": " totol properties having assessmentNumber "
  },
  
	"completionRateV3": {
    "chartName": "NATIONAL_DSS_PT_COMPLETION_RATE",
    "queries": [
       {
        "module": "PT",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "dateRefField": "date",
        "indexName": "pt-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"Closed Application\":{\"terms\":{\"field\":\"state.keyword\"},\"aggs\":{\"sum\":{\"sum\":{\"field\":\"assessedPropertiesForUsageCategory\"}}}},\"Total Application\":{\"terms\":{\"field\":\"state.keyword\"},\"aggs\":{\"sum\":{\"sum\":{\"field\":\"propertiesRegisteredForFinancialYear\"}}}}}}}}"
      }
    ],
    "chartType": "metric",
    "valueType": "percentage",
    "drillChart": "none",
    "documentType": "_doc",
    "action": "percentage",
    "isRoundOff": true,
    "aggregationPaths": [
      "Closed Application",
      "Total Application"
    ],
    "insight": {
      "chartResponseMap" : "completionRateV3",
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
	
	
	"cumulativePropertiesAssessedv3": {
    "chartName": "NATIONAL_DSS_PT_CUMULATIVE_PROPERTIES_ASSESSED",
    "queries": [
      {
        "module": "PT",
        "indexName": "pt-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"Assesments\":{\"date_histogram\":{\"field\":\"date\",\"interval\":\"intervalvalue\"},\"aggs\":{\"SUM\":{\"sum\":{\"field\":\"assessedPropertiesForUsageCategory\"}}}}}}}}",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "dateRefField": "date"
      }
    ],
    "chartType": "line",
    "valueType": "number",
    "action": "",
    "documentType": "_doc",
    "drillChart": "none",
    "aggregationPaths": [
      "Assesments"
    ],
    "isCumulative": true,
    "interval": "month",	
    "insight": {
    },
    "_comment": " totol properties having assessmentNumber "
  },
  
 	"topPerformingStatesCompletionRatev3": {
    "chartName": "NATIONAL_DSS_PT_TOP_3_PERFORMING_STATES_COMPLETION_RATE",
    "queries": [
      {
        "module": "PT",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "dateRefField": "date",
        "indexName": "pt-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"Closed Application\":{\"terms\":{\"field\":\"state.keyword\"},\"aggs\":{\"sum\":{\"sum\":{\"field\":\"assessedPropertiesForUsageCategory\"}}}},\"Total Application\":{\"terms\":{\"field\":\"state.keyword\"},\"aggs\":{\"sum\":{\"sum\":{\"field\":\"propertiesRegisteredForFinancialYear\"}}}}}}}}"
      }
    ],
    "chartType": "perform",
    "valueType": "percentage",
    "drillChart": "none",
    "documentType": "_doc",
    "action": "percentage",
    "plotLabel": "NATIONAL_DSS_COMPLETION_RATE",
    "order": "desc",
    "limit": 3,
    "isRoundOff": true,
    "aggregationPaths": [
      "Closed Application",
      "Total Application"
    ],
    "insight": {
    },
    "_comment": " Top Performing states for Completion rate"
  },
  
  	"bottomPerformingStatesCompletionRatev3": {
    "chartName": "NATIONAL_DSS_PT_BOTTOM_3_PERFORMING_STATES_COMPLETION_RATE",
    "queries": [
      {
        "module": "PT",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "dateRefField": "date",
        "indexName": "pt-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"Closed Application\":{\"terms\":{\"field\":\"state.keyword\"},\"aggs\":{\"sum\":{\"sum\":{\"field\":\"assessedPropertiesForUsageCategory\"}}}},\"Total Application\":{\"terms\":{\"field\":\"state.keyword\"},\"aggs\":{\"sum\":{\"sum\":{\"field\":\"propertiesRegisteredForFinancialYear\"}}}}}}}}"
      }
    ],
    "chartType": "perform",
    "valueType": "percentage",
    "drillChart": "none",
    "documentType": "_doc",
    "action": "percentage",
    "plotLabel": "NATIONAL_DSS_COMPLETION_RATE",
    "order": "asc",
    "limit": 3,
    "isRoundOff": true,
    "aggregationPaths": [
      "Closed Application",
      "Total Application"
    ],
    "insight": {
    },
    "_comment": " Bottom Performing states for Completion rate"
  },
 	
 	"propertiesByUsageTypev3": {
    "chartName": "NATIONAL_DSS_PT_PROPERTIES_BY_USAGE_TYPE",
    "queries": [
      {
        "module": "PT",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "dateRefField": "date",
        "indexName": "pt-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"Usage Type\":{\"terms\":{\"field\":\"usageCategory.keyword\"},\"aggs\":{\"Assessed Properties\":{\"sum\":{\"field\":\"assessedPropertiesForUsageCategory\"}}}}}}}}"

      }
    ],
    "chartType": "pie",
    "valueType": "number",
    "action": "",
    "documentType": "_doc",
    "drillChart": "none",
    "aggregationPaths": [
      "Usage Type"
    ],
    "insight": {
    },
    "_comment": " properties having assessmentNumber per usage type"
  },
	
	"xptFyByStatesv3": {
    "chartName": "NATIONAL_DSS_PT_PROPERTIES_BY_FINANCIAL_YEAR",
    "queries": [
       {
      
        "module": "PT",
		"requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "dateRefField": "date",
        "indexName": "pt-national-dashboard",	
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"state \":{\"terms\":{\"field\":\"state.keyword\",\"size\":200},\"aggs\":{\"Fys\":{\"terms\":{\"field\":\"financialYear.keyword\",\"min_doc_count\":0,\"order\":{\"_term\":\"asc\"}},\"aggs\":{\"sum\":{\"sum\":{\"field\":\"propertiesRegisteredForFinancialYear\"}}}}}}}}}}"
      },
      {
        "module": "PT",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "dateRefField": "date",
        "indexName": "pt-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"state \":{\"terms\":{\"field\":\"state.keyword\",\"size\":200},\"aggs\":{\"Total\":{\"sum\":{\"field\":\"propertiesRegisteredForFinancialYear\"}}}}}}}}"
      }
    ],
    "isMdmsEnabled": false,
    "filterKeys": [
      {"key": "state", "column": "State"}
    ],
    "chartType": "xtable",
    "valueType": "number",
    "drillChart": "xptFyByUlbv3",
    "plotLabel": "State",
    "insight": {
    },
    "_comment": " fy data"
  },
  
  	"xptFyByUlbv3": {
    "chartName": "NATIONAL_DSS_PT_PROPERTIES_BY_FINANCIAL_YEAR_ULB",
    "queries": [
       {
      
        "module": "PT",
		"requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "dateRefField": "date",
        "indexName": "pt-national-dashboard",	
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"ulb \":{\"terms\":{\"field\":\"ulb.keyword\",\"size\":200},\"aggs\":{\"Fys\":{\"terms\":{\"field\":\"financialYear.keyword\",\"min_doc_count\":0,\"order\":{\"_term\":\"asc\"}},\"aggs\":{\"sum\":{\"sum\":{\"field\":\"propertiesRegisteredForFinancialYear\"}}}}}}}}}}"
      },
      {
        "module": "PT",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "dateRefField": "date",
        "indexName": "pt-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"ulb \":{\"terms\":{\"field\":\"ulb.keyword\",\"size\":200},\"aggs\":{\"Total\":{\"sum\":{\"field\":\"propertiesRegisteredForFinancialYear\"}}}}}}}}"
      }
    ],
    "isMdmsEnabled": false,
    "filterKeys": [
      {"key": "ulb", "column": "Ulb"}
    ],
    "chartType": "xtable",
    "valueType": "number",
    "drillChart": "xptFyByWardv3",
    "drillFields": [
      "ward",
      ""
    ],
    "plotLabel": "Ulb",
    "insight": {
    },
    "_comment": " fy data"
  },
  
  	"xptFyByWardv3": {
    "chartName": "NATIONAL_DSS_PT_PROPERTIES_BY_FINANCIAL_YEAR_Ward",
    "queries": [
       {
      
        "module": "PT",
		"requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "dateRefField": "date",
        "indexName": "pt-national-dashboard",	
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"ward \":{\"terms\":{\"field\":\"ward.keyword\",\"size\":200},\"aggs\":{\"Fys\":{\"terms\":{\"field\":\"financialYear.keyword\",\"min_doc_count\":0,\"order\":{\"_term\":\"asc\"}},\"aggs\":{\"sum\":{\"sum\":{\"field\":\"propertiesRegisteredForFinancialYear\"}}}}}}}}}}"
      },
      {
        "module": "PT",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "dateRefField": "date",
        "indexName": "pt-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"ward \":{\"terms\":{\"field\":\"ward.keyword\",\"size\":200},\"aggs\":{\"Total\":{\"sum\":{\"field\":\"propertiesRegisteredForFinancialYear\"}}}}}}}}"
      }
    ],
    "isMdmsEnabled": false,
    "filterKeys": [
    ],
    "chartType": "xtable",
    "valueType": "number",
    "drillChart": "",
    "plotLabel": "Ward",
    "insight": {
    },
    "_comment": " fy data"
  },

```

[Click here to check the complete configuration](https://github.com/egovernments/configs/blob/qa/egov-dss-dashboards/dashboard-analytics/ChartApiConfig.json)

**Master Dashboard Configuration:** Master Dashboard Configuration is the main configuration which defines the Dashboards to be painted on the screen. It includes all visualizations, their groups, the charts which comes within them and even their dimensions in terms of height and width.

```
{
      "name": "NATIONAL_DSS_PROPERTY_TAX_DASHBOARD",
      "id": "national-propertyTax",
      "isActive": "",
      "style": "linear",
      "visualizations": [
        {
          "row": 1,
          "name": "NATIONAL_DSS_REVENUE",
          "vizArray": [
            {
              "id": 211,
              "name": "NATIONAL_DSS_OVERVIEW",
              "dimensions": {
                "height": 350,
                "width": 5
              },
              "vizType": "metric-collection",
              "noUnit": true,
              "isCollapsible": false,
              "label": "NATIONAL_DSS_OVERVIEW",
              "charts": [
                {
                  "id": "todaysCollectionv3",
                  "name": "NATIONAL_DSS_TOTAL_COLLECTION_TODAY",
                  "code": "",
                  "chartType": "metric",
                  "filter": {"title": "TODAY"},
                  "headers": []
                },
                {
                  "id": "totalCollectionv3",
                  "name": "NATIONAL_PT_DSS_TOTAL_COLLECTION",
                  "code": "",
                  "chartType": "metric",
                  "filter": "",
                  "headers": []
                },
                {
                  "id": "targetCollectionv3",
                  "name": "NATIONAL_PT_DSS_TARGET_COLLECTION",
                  "code": "",
                  "chartType": "metric",
                  "filter": "",
                  "headers": []
                },
                {
                  "id": "targetAchievedv3",
                  "name": "NATIONAL_DSS_TARGET_ACHIEVED",
                  "code": "",
                  "chartType": "metric",
                  "filter": "",
                  "headers": []
                }
              ]
            },
            {
              "id": 212,
              "name": "NATIONAL_DSS_TOTAL_CUMULATIVE_COLLECTION",
              "dimensions": {
                "height": 350,
                "width": 7
              },
              "vizType": "chart",
              "noUnit": true,
              "isCollapsible": false,
              "charts": [
                {
                  "id": "cumulativeCollectionv3",
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
          "name": "NATIONAL_DSS_REVENUE",
          "vizArray": [
               {
              "id": 221,
              "name": "NATIONAL_DSS_PT_COLLECTION_BY_USAGE_TYPE",
              "dimensions": {
                "height": 250,
                "width": 4
              },
              "vizType": "chart",
              "noUnit": true,
              "isCollapsible": false,
              "charts": [
                {
                  "id": "collectionByUsageTypev3",
                  "name": "NATIONAL_DSS_PT_COLLECTION_BY_USAGE_TYPE",
                  "code": "",
                  "chartType": "donut",
                  "filter": "",
                  "headers": []
                }
              ]
            },
            {
              "id": 222,
              "name": "NATIONAL_DSS_PT_TOP_3_PERFORMING_STATES_TARGET_ACHIEVEMENT",
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
                  "id": "topPerformingStatesv3",
                  "name": "NATIONAL_DSS_PT_TOP_3_PERFORMING_STATES_TARGET_ACHIEVEMENT",
                  "code": "",
                  "chartType": "bar",
                  "filter": "",
                  "headers": []
                }
              ]
            },
            {
              "id": 223,
              "name": "NATIONAL_DSS_PT_BOTTOM_3_PERFORMING_STATES_TARGET_ACHIEVEMENT",
              "dimensions": {
                "height": 250,
                "width": 4
              },
              "vizType": "performing-metric",
              "noUnit": false,
              "isCollapsible": false,
              "charts": [
                {
                  "id": "bottomPerformingStatesv3",
                  "name": "NATIONAL_DSS_PT_BOTTOM_3_PERFORMING_STATES_TARGET_ACHIEVEMENT",
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
          "name": "NATIONAL_DSS_REVENUE",
          "vizArray": [
            {
              "id": 231,
              "name": "NATIONAL_DSS_PT_KEY_FY_INDICATORS",
              "dimensions": {
                "height": 350,
                "width": 12
              },
              "vizType": "chart",
              "noUnit": false,
              "isCollapsible": false,
              "charts": [
                {
                  "id": "demandCollectionIndexStatesRevenuev3",
                  "name": "NATIONAL_DSS_PT_DEMAND_COLLECTION_STATES",
                  "code": "",
                  "chartType": "table",
                  "filter": "",
                  "headers": [],
                  "tabName": "Boundary"
                },
                {
                  "id": "demandCollectionIndexUsageRevenuev3",
                  "name": "NATIONAL_DSS_PT_DEMAND_COLLECTION_USAGETYPE",
                  "code": "",
                  "chartType": "table",
                  "filter": "",
                  "headers": [],
                  "tabName": "Usage"
                }
              ]
            }
          ]
        },
        {
          "row": 4,
          "name": "NATIONAL_DSS_REVENUE",
          "vizArray": [
            {
              "id": 231,
              "name": "NATIONAL_DSS_PT_TAX_HEAD",
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
                  "id": "taxHeadsBreakupStatesRevenuev3",
                  "name": "NATIONAL_DSS_PT_TAX_HEAD_BREAKUP_REVENUE",
                  "code": "",
                  "chartType": "table",
                  "filter": "",
                  "headers": [],
                  "tabName": "Boundary"
                },
                {
                  "id": "taxHeadsBreakupUsagev3",
                  "name": "NATIONAL_DSS_PT_TAX_HEAD_BREAKUP_USAGE",
                  "code": "",
                  "chartType": "table",
                  "filter": "",
                  "headers": [],
                  "tabName": "Usage"
                }
              ]
            }
          ]
        },
        {
          "row": 5,
          "name": "NATIONAL_DSS_SERVICE",
          "vizArray": [
            {
              "id": 241,
              "name": "NATIONAL_DSS_OVERVIEW",
              "dimensions": {
                "height": 350,
                "width": 5
              },
              "vizType": "metric-collection",
              "isCollapsible": false,
              "label": "NATIONAL_DSS_OVERVIEW",
              "charts": [
                {
                  "id": "totalApplicationsv3",
                  "name": "NATIONAL_DSS_PT_TOTAL_APPLICATIONS",
                  "code": "",
                  "chartType": "metric",
                  "filter": "",
                  "headers": []
                },
                {
                  "id": "totalPropertiesv3",
                  "name": "NATIONAL_DSS_PT_TOTAL_PROPERTIES",
                  "code": "",
                  "chartType": "metric",
                  "filter": "",
                  "headers": []
                },
                {
                  "id": "propertiesAssessedv3",
                  "name": "NATIONAL_DSS_PT_TOTAL_PROPERTIES_ASSESSED",
                  "code": "",
                  "chartType": "metric",
                  "filter": "",
                  "headers": []
                },
                {
                  "id": "totalAssessmentv3",
                  "name": "NATIONAL_DSS_PT_TOTAL_ASSESSMENTS",
                  "code": "",
                  "chartType": "metric",
                  "filter": "",
                  "headers": []
                },
                {
                  "id": "completionRateV3",
                  "name": "NATIONAL_DSS_PT_COMPLETION_RATE",
                  "code": "",
                  "chartType": "metric",
                  "filter": "",
                  "headers": []
                }
              ]
            },
            {
              "id": 242,
              "name": "NATIONAL_DSS_PT_CUMULATIVE_PROPERTIES_ASSESSED",
              "dimensions": {
                "height": 350,
                "width": 7
              },
              "vizType": "chart",
              "isCollapsible": false,
              "charts": [
                {
                  "id": "cumulativePropertiesAssessedv3",
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
          "row": 6,
          "name": "NATIONAL_DSS_SERVICE",
          "vizArray": [
            {
              "id": 251,
              "name": "NATIONAL_DSS_PT_PROPERTIES_BY_USAGE_TYPE",
              "dimensions": {
                "height": 250,
                "width": 4
              },
              "vizType": "chart",
              "isCollapsible": false,
              "charts": [
                {
                  "id": "propertiesByUsageTypev3",
                  "name": "NATIONAL_DSS_PT_PROPERTIES_BY_USAGE_TYPE",
                  "code": "",
                  "chartType": "donut",
                  "filter": "",
                  "headers": []
                }
              ]
            },
            {
              "id": 252,
              "name": "NATIONAL_DSS_PT_TOP_3_PERFORMING_STATES_COMPLETION_RATE",
              "dimensions": {
                "height": 250,
                "width": 4
              },
              "vizType": "performing-metric",
              "isCollapsible": false,
              "label": "",
              "charts": [
                {
                  "id": "topPerformingStatesCompletionRatev3",
                  "name": "NATIONAL_DSS_PT_TOP_3_PERFORMING_STATES_COMPLETION_RATE",
                  "code": "",
                  "chartType": "bar",
                  "filter": "",
                  "headers": []
                }
              ]
            },
            {
              "id": 253,
              "name": "NATIONAL_DSS_PT_BOTTOM_3_PERFORMING_STATES_COMPLETION_RATE",
              "dimensions": {
                "height": 250,
                "width": 4
              },
              "vizType": "performing-metric",
              "isCollapsible": false,
              "charts": [
                {
                  "id": "bottomPerformingStatesCompletionRatev3",
                  "name": "NATIONAL_DSS_PT_BOTTOM_3_PERFORMING_STATES_COMPLETION_RATE",
                  "code": "",
                  "chartType": "bar",
                  "filter": "",
                  "headers": []
                }
              ]
            }          ]
        },
        {
          "row": 7,
          "name": "NATIONAL_DSS_SERVICE",
          "vizArray": [
            {
              "id": 231,
              "name": "NATIONAL_DSS_PT_PROPERTIES_BY_FINANCIAL_YEAR",
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
                  
                  "id": "xptFyByStatesv3",
                  "name": "NATIONAL_DSS_PT_PROPERTIES_BY_FINANCIAL_YEAR",
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

**Role Dashboard Mappings Configuration:** Master Dashboard Configuration which was explained earlier hold the list of available dashboards.

Given the instance where Role Action Mapping is not maintained in the Application Service, this configuration acts as the Role - Dashboard Mapping Configuration. Each Role is mapped against the Dashboard which they are authorized to see. This was used earlier when the Role Action Mapping of eGov was not integrated. Later, when the Role Action Mapping started controlling the Dashboards to be seen on the client side, this configuration was just used to enable the Dashboards for viewing.&#x20;

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
          "name": "National Property Tax",
          "id": "national-propertyTax"
        }
      ]
    }

  ]
}

```

[Click here to check the configuration](https://github.com/egovernments/configs/blob/qa/egov-dss-dashboards/dashboard-analytics/RoleDashboardMappingsConf.json)

**MDMS configuration file path:** _common-masters/uiCommonConstants.json_

```
"national-propertytax": {
                  "routePath": "/dashboard/national-propertytax",
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
    },

```

[Click here to check the complete configuration](https://github.com/egovernments/egov-mdms-data/blob/QA/data/pb/ACCESSCONTROL-ROLEACTIONS/roleactions.json)

Action test.json:

```
{
      "id": {{PlaceHolder1}},
      "name": "NSS Dashboard Config National Property Tax",
      "url": "/dashboard-analytics/dashboard/getDashboardConfig/national-propertytax",
      "parentModule": "",
      "displayName": "NSS",
      "orderNumber": 0,
      "enabled": false,
      "serviceCode": "NSS",
      "code": "null",
      "path": ""
    },
    {
      "id": {{PlaceHolder2}},
      "name": "National Dashboard Property Tax",
      "url": "url",
      "displayName": "National Property Tax",
      "orderNumber": 4,
      "parentModule": "ndss-dashboard",
      "enabled": true,
      "serviceCode": "NDSS",
      "code": "null",
      "path": "NatDashboard.PropertyTax",
      "navigationURL": "/digit-ui/employee/dss/dashboard/national-propertytax",
      "leftIcon": "places:business-center",
      "rightIcon": ""
    }
```

[Click here to check the complete configuration](https://github.com/egovernments/egov-mdms-data/blob/QA/data/pb/ACCESSCONTROL-ACTIONS-TEST/actions-test.json)

Property Tax-National DSS _c_ontains multiple graphs that represent the PT data. Each graph has its own configuration that describes the chart and its type.

National DSS contains the following charts in Property Tax:

**Revenue Tab:**

* Overview
* Total Cumulative Collection
* Top 3 States By Performance
* Bottom 3 States by Performance
* Collection by Usage Type
* Key Financial Indicators
  * Boundary
  * Usage
* Tax Heads
  * Boundary
  * Usage

**Service Tab:**

* Overview
* Total Cumulative Properties Assessed
* Top 3 Performing States By Completion
* Bottom 3 Performing States By Completion
* Properties By Usage Type
* Properties By Financial Year

**Revenue Tab:**

* **Overview:** Overview graph contains multiple data information as below in the selected time period.
* **Collection on:** This represents the today’s collection amount.
* &#x20;**Total Collection:** This represents the total collection amount.
* **Target Collection:** This represents the target collection amount.
* **Target Achievement:** This represents the target achieved in percentage. This is calculated by formula- (Total Collection/Target Collection)\*100%

![](<../../../../.gitbook/assets/image (316).png>)

**Total Cumulative Collection:** This graph contains the Property Tax collection amount information in the monthly base as a cumulative line graph. This will change as per the denomination amount filter selection.

**line** - this graph/chart is data representation on date histograms or date groupings.

![](<../../../../.gitbook/assets/image (149).png>)

**Top 3 Performing States By Completion -**This graph represents the States based on the target achieved in bar chart representation with the % of target achieved in descending order.

&#x20;

![](<../../../../.gitbook/assets/image (331).png>)

**Bottom 3 States by Performance -** This graph represents the States based on the target achieved in bar chart representation with the % of target achieved in ascending order.

![](<../../../../.gitbook/assets/image (52).png>)

**Collection by Usage Type -** This graph shows the collection amount based on the usage/property type.

![](<../../../../.gitbook/assets/image (118).png>)

**Key Financial Indicators**

**Boundary -** This tabular chart representation graph shows multiple W\&S information like Target Collection, Total Collection, Total Transactions, Total Assessed Properties and Target Achievement (in %). And this table shows the data at the State level and also has the drill-down chart for each State to ULB and from ULB to ward level data for the same.

_**xtable**_ type allows adding multiple computed fields with the aggregated fields dynamically added.

To add multiple computed columns,  **computedFields** \[]  where actionName (IComputedField\<T> interface), fields \[] names as in existing query key, newField as name to appear for computation must be defined.

![](<../../../../.gitbook/assets/image (147).png>)

Clicking on any State name provides a drill-down view of charts for the specific ULB level data.

![](<../../../../.gitbook/assets/image (186).png>)

Clicking on the ULB navigates users to the wards specific data.

**Usage -** shows the data in the form of connection type for the given time period. Usage Type, Total Collection, Transactions, Assessed Properties.

![](<../../../../.gitbook/assets/image (243).png>)

**Tax Heads**

**Boundary -** This tabular chart representation graph shows multiple PT information like Total Collection, Penalty, Interest etc. And this table shows the data at the State level and also has the drill-down chart for each State to ULB and from ULB to ward level data for the same.

_**table**_ type allows adding multiple aggregated fields.

![](<../../../../.gitbook/assets/image (308).png>)

Clicking on the State name provides a drill down view of the specific ULB data in the form of charts.

![](<../../../../.gitbook/assets/image (87).png>)

Clicking on the ULB navigates to the specific ward and displays the ward-level data insights.

**Usage -** shows the data in form of Connection type for the given time period. Usage Type, Total Amount,Tax, Cess, Rebate, Penalty, Interest.

![](<../../../../.gitbook/assets/image (225).png>)

**Service Tab**

**Overview:** The overview graph contains multiple data information as below in the selected time period.

* **Total Applications:** This represents the total number of applications.
* **Total Properties:** This represents the total number of properties registered.
* **Total Properties Assessed:**  This represents the total Properties Assessed.
* **Total Assessments:** This represents the total Assessment of Properties.
* **Completion Rate:** This represents Total Properties Assessed / Total Properties.

![](<../../../../.gitbook/assets/image (189).png>)

**Total Cumulative Properties Assessed:** This Graph contains the Assessed Properties information in the monthly base as a cumulative line graph.

**line** - this graph/chart is data representation on date histograms or date groupings.

![](<../../../../.gitbook/assets/image (162).png>)

**Top 3 Performing States By Completion:** This graph represents the States based on the Assessed Properties of Total Properties Register in bar chart representation with the % in descending order.

![](<../../../../.gitbook/assets/image (332).png>)

**Bottom 3 Performing States By Completion:** This graph represents the States based on the Assessed Properties of Total Properties Register in bar chart representation with the % in descending order.

**Properties By Usage Type:** This circular chart represents the assessed properties as part of connection type like commercial, industrial, residential etc for the given time period.

![](<../../../../.gitbook/assets/image (309).png>)

**Properties By Financial Year:** This table shows total number of properties which has been registered on the system for the financial years.

![](<../../../../.gitbook/assets/image (312).png>)

**Index Properties of National Property Tax -** The index that contains data for National-PT is- _pt-national-dashboard._ The mapping details for this index is given below:

```
PUT pt-national-dashboard/_mapping/nss
{
  "properties": {
    "ulb": {
      "type": "text",
      "fields": {
        "keyword": {
          "type": "keyword",
          "ignore_above": 256
        }
      }
    },
    "state": {
      "type": "text",
      "fields": {
        "keyword": {
          "type": "keyword",
          "ignore_above": 256
        }
      }
    },
    "ward": {
      "type": "text",
      "fields": {
        "keyword": {
          "type": "keyword",
          "ignore_above": 256
        }
      }
    },
    "region": {
      "type": "text",
      "fields": {
        "keyword": {
          "type": "keyword",
          "ignore_above": 256
        }
      }
    },
    "transactionsForUsageCategory": {
      "type": "long"
    },
    "todaysTotalApplications": {
      "type": "long"
    },
    "todaysClosedApplications": {
      "type": "long"
    },
    "assessedPropertiesForUsageCategory": {
      "type": "long"
    },
    "date": {
      "type": "date",
      "format": "dd-MM-yyyy HH:mm:ss||dd-MM-yyyy||epoch_millis||dd-MM-yyyy'T'HH:mm:ss.SSSZ"
    },
    "propertiesRegisteredForFinancialYear": {
      "type": "long"
    },
    "financialYear": {
      "type": "text",
      "fields": {
        "keyword": {
          "type": "keyword",
          "ignore_above": 256
        }
      }
    },
    "usageCategory": {
      "type": "text",
      "fields": {
        "keyword": {
          "type": "keyword",
          "ignore_above": 256
        }
      }
    },
    "todaysCollectionForUsageCategory": {
      "type": "long"
    },
    "propertyTaxForUsageCategory": {
      "type": "long"
    },
    "cessForUsageCategory": {
      "type": "long"
    },
    "rebateForUsageCategory": {
      "type": "long"
    },
    "penaltyForUsageCategory": {
      "type": "long"
    },
    "interestForUsageCategory": {
      "type": "long"
    },
	 "assessments": {
      "type": "long"
    }
  }
}

```

The following table that describes the properties mentioned above:

| **Attributes**                         | **Definition**                                                                                                                                                                                                 | **Breakup**                                                        |
| -------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------ |
| `state`                                | <p>It represents the state name.</p><p>for ex. <strong>Punjab</strong></p>                                                                                                                                     | Nil                                                                |
| `ulb`                                  | <p>It represents the ulb name of state .</p><p>for ex. for state <strong>Punjab, ulb</strong> can be <code>"pb.amritsar"</code>, <code>"pb.longowal" etc.</code></p>                                           | Nil                                                                |
| `ward`                                 | <p>It represents the ward name of particular ulb of particular state.</p><p>for ex. for ulb <code>"pb.amritsar"</code>, ward name can we “<strong>Ram Nagar</strong>”, “<strong>Ajith Nagar</strong>” etc.</p> | Nil                                                                |
| `usageCategory`                        | It represents the category like “RESIDENCIAL”, INDUSTRIAL”, “COMMERCIAL” etc.                                                                                                                                  | Nil                                                                |
| `transactionsForUsageCategory`         | It represents total transactions based on the **usageCategory** on given date.                                                                                                                                 | Breakup by usageCategory(RESIDENCIAL, INDUSTRIAL,COMMERCIAL etc. ) |
| `assessedPropertiesForUsageCategory`   | It represents total properties assessed based on the **usageCategory** on given date.                                                                                                                          | Breakup by usageCategory(RESIDENCIAL, INDUSTRIAL,COMMERCIAL etc. ) |
| `todaysCollectionForUsageCategory`     | It represents the aggregation of fields property tax, cess, penalty, interest, rebate(should be nagative number) for the given date based on the **usageCategory.**                                            | Breakup by usageCategory(RESIDENCIAL, INDUSTRIAL,COMMERCIAL etc. ) |
| `propertyTaxForUsageCategory`          | It represents the collection done as part of property tax for given date based on the **usageCategory.**                                                                                                       | Breakup by usageCategory(RESIDENCIAL, INDUSTRIAL,COMMERCIAL etc. ) |
| `cessForUsageCategory`                 | It represents the collection done as part of cess for given date based on the **usageCategory.**                                                                                                               | Breakup by usageCategory(RESIDENCIAL, INDUSTRIAL,COMMERCIAL etc. ) |
| `rebateForUsageCategory`               | It represents the rebate given based on the **usageCategory.**                                                                                                                                                 | Breakup by usageCategory(RESIDENCIAL, INDUSTRIAL,COMMERCIAL etc. ) |
| `penaltyForUsageCategory`              | It represents the collection done as part of panalty for given date based on the **usageCategory.**                                                                                                            | Breakup by usageCategory(RESIDENCIAL, INDUSTRIAL,COMMERCIAL etc. ) |
| `interestForUsageCategory`             | It represents the collection done as part of interest for given date based on the **usageCategory.**                                                                                                           | Breakup by usageCategory(RESIDENCIAL, INDUSTRIAL,COMMERCIAL etc. ) |
| `assessments`                          | It represents number of assessments done.                                                                                                                                                                      | Nil                                                                |
| `todaysTotalApplications`              | It represents number of applications created as part of property tax on given date                                                                                                                             | Nil                                                                |
| `todaysClosedApplications`             | It represents number of closed applications as part of property tax on given date.                                                                                                                             | Nil                                                                |
| `date`                                 | It represents date for which data is ingesting                                                                                                                                                                 | Nil                                                                |
| `financialYear`                        | it represents financial year which which data is inserting.                                                                                                                                                    | Nil                                                                |
| `propertiesRegisteredForFinancialYear` | It represents number of properties registered in the system for the given financial year.                                                                                                                      | Breakup by financialYear(“2021-22”, “2022-23” etc.)                |

**Postman collection for National Property Tax**

{% embed url="https://www.getpostman.com/collections/4fe5a883ea653bfe07a2" %}

