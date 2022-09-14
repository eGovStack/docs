---
description: Technical Doc
---

# Trade License - National Dashboard

## **Overview**

NDSS has two sides to it. One is the process in which the data is pooled to the ElasticSearch and the other is the way it is fetched, aggregated, computed, transformed and sent across.&#x20;

As this revolves around a variety of data sets, there is a need for making this configurable. This ensures that the process can be configured easily in case a new scenario is introduced.&#x20;

This document walks us through the steps on how to define the configurations for DSS analytics for the Trade License module.

## **Technical Details**

**Analytics:** Microservice responsible for building, fetching, aggregating and computing the data on ElasticSearch into a consumable data response. This is used for visualizations and graphical representations.&#x20;

**Analytics Configurations:** Analytics contains multiple configurations. Add the changes related to OBPS in this dashboard analytics.&#x20;

Configuration file path: [<img src="https://github.com/fluidicon.png" alt="" data-size="line">configs/egov-dss-dashboards/dashboard-analytics at qa · egovernments/configs](https://github.com/egovernments/configs/tree/qa/egov-dss-dashboards/dashboard-analytics)

Below is a list of configurations that need to be changed to run the National Dashboard successfully.

1. Chart API Configuration
2. Master Dashboard Configuration
3. Role Dashboard Mappings Configuration

**Chart API Configuration:** Each visualization has its own properties. The visualization data is fetched from different sources. In some cases, it is a combination of different data sources. The Chart API configuration document is used to configure each visualization and its properties.&#x20;

The visualization code is the key whose properties are configured here. These properties are easily changeable.

Below is the sample ChartApiConfiguration.json data for the Trade License.

```
"tradeLicenseTodaysCollectionv2": {
      "chartName": "DSS_TODAYS_COLLECTION",
      "queries": [
        {
          "module": "COMMON",
          "dateRefField": "date",
          "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
          "indexName": "tl-national-dashboard",
          "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must\":[{\"range\":{\"date\":{\"gt\":\"now-1d\/d\",\"lte\":\"now\"}}}]}},\"aggs\":{\"Todays Collection\":{\"sum\":{\"field\":\"todaysCollectionForTradeType\"}}}}}}"
        }
      ],
      "chartType": "metric",
      "valueType": "Amount",
      "drillChart": "none",
      "documentType": "_doc",
      "action": "",
      "aggregationPaths": [
        "Todays Collection"
      ],
      "insight": {
        "chartResponseMap" : "tradeLicenseTodaysCollectionv2",
        "action" : "differenceOfNumbers",
        "upwardIndicator" : "positive",
        "downwardIndicator" : "negative",
        "textMessage" : "$indicator$value% than last $insightInterval",
        "colorCode" : "#228B22",
        "insightInterval" : "month"
      },
      "_comment": " "
    },
  
    "tradeLicenseTotalCollectionv2": {
      "chartName": "DSS_TOTAL_COLLECTION",
      "queries": [
        {
          "module": "COMMON",
          "dateRefField": "date",
          "requestQueryMap": "{\"state\" : \"state.keyword\",\"tenantId\" : \"ulb.keyword\"}",
          "indexName": "tl-national-dashboard",
          "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"Total Collection\":{\"sum\":{\"field\":\"todaysCollectionForTradeType\"}}}}}}"
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
        "chartResponseMap" : "tradeLicenseTotalCollectionv2",
        "action" : "differenceOfNumbers",
        "upwardIndicator" : "positive",
        "downwardIndicator" : "negative",
        "textMessage" : "$indicator$value% than last $insightInterval",
        "colorCode" : "#228B22",
        "insightInterval" : "year"
      },
      "_comment": " "
    },
  
    "totalLicensesIssuedv2": {
      "chartName": "DSS_TOTAL_LICENSES",
      "queries": [
        {
          "module": "COMMON",
          "dateRefField": "date",
          "requestQueryMap": "{\"state\" : \"state.keyword\",\"tenantId\" : \"ulb.keyword\"}",
          "indexName": "tl-national-dashboard",
          "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"Total Licenses\":{\"sum\":{\"field\":\"todaysTradeLicensesForStatus\"}}}}}}"
        }
      ],
      "chartType": "metric",
      "valueType": "number",
      "drillChart": "none",
      "documentType": "_doc",
      "action": "",
      "aggregationPaths": [
        "Total Licenses"
      ],
      "insight": {
        "chartResponseMap" : "totalLicensesIssuedv2",
        "action" : "differenceOfNumbers",
        "upwardIndicator" : "positive",
        "downwardIndicator" : "negative",
        "textMessage" : "$indicator$value% than last $insightInterval",
        "colorCode" : "#228B22",
        "insightInterval" : "year"
      }
    },

    "tlMonthlyCumulativeCollectionv2": {
      "chartName": "DSS_TL_MONTHLY_CUMULATIVE",
      "queries": [
        {
          "module": "COMMON",
          "dateRefField": "date",
          "requestQueryMap": "{\"state\" : \"state.keyword\",\"tenantId\" : \"ulb.keyword\"}",
          "indexName": "tl-national-dashboard",
          "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[]}},\"aggs\":{\"Collections\":{\"date_histogram\":{\"field\":\"date\",\"interval\":\"month\"},\"aggs\":{\"Sum\":{\"sum\":{\"field\":\"todaysCollectionForTradeType\"}}}}}}}}"
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
      "insight": {},
      "_comment": " "
    },
  
    "totalTransactionsv2": {
      "chartName": "DSS_TOTAL_TRANSACTIONS",
      "queries": [
        {
          "module": "COMMON",
          "dateRefField": "date",
          "requestQueryMap": "{\"state\" : \"state.keyword\",\"tenantId\" : \"ulb.keyword\"}",
          "indexName": "tl-national-dashboard",
          "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"state\":{\"terms\":{\"field\":\"state.keyword\"},\"aggs\":{\"intermediateAggrULB\":{\"terms\":{\"field\":\"ulb.keyword\"},\"aggs\":{\"intermediateAggrWard\":{\"terms\":{\"field\":\"ward.keyword\"},\"aggs\":{\"days\":{\"terms\":{\"field\":\"date\"},\"aggs\":{\"applications\":{\"avg\":{\"field\":\"transactions\"}}}},\"wardapplications\":{\"sum_bucket\":{\"buckets_path\":\"days.applications\"}}}},\"ulbApplications\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrWard.wardapplications\"}}}},\"stateApplications\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrULB.ulbApplications\"}}}},\"Total Transactions\":{\"sum_bucket\":{\"buckets_path\":\"state.stateApplications\"}}}}}}"
        }
      ],
      "chartType": "metric",
      "valueType": "number",
      "drillChart": "none",
      "documentType": "_doc",
      "action": "",
      "aggregationPaths": [
        "Total Transactions"
      ],
      "insight": {
        "chartResponseMap" : "totalTransactionsv2",
        "action" : "differenceOfNumbers",
        "upwardIndicator" : "positive",
        "downwardIndicator" : "negative",
        "textMessage" : "$indicator$value% than last $insightInterval",
        "colorCode" : "#228B22",
        "insightInterval" : "year"
      }
    },
  
    "totalApplicationsv2": {
      "chartName": "DSS_TOTAL_APPLICATIONS",
      "queries": [
        {
          "module": "COMMON",
          "dateRefField": "date",
          "requestQueryMap": "{\"state\" : \"state.keyword\",\"tenantId\" : \"ulb.keyword\"}",
          "indexName": "tl-national-dashboard",
          "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"state\":{\"terms\":{\"field\":\"state.keyword\"},\"aggs\":{\"intermediateAggrULB\":{\"terms\":{\"field\":\"ulb.keyword\"},\"aggs\":{\"intermediateAggrWard\":{\"terms\":{\"field\":\"ward.keyword\"},\"aggs\":{\"days\":{\"terms\":{\"field\":\"date\"},\"aggs\":{\"applications\":{\"avg\":{\"field\":\"todaysApplications\"}}}},\"wardapplications\":{\"sum_bucket\":{\"buckets_path\":\"days.applications\"}}}},\"ulbApplications\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrWard.wardapplications\"}}}},\"stateApplications\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrULB.ulbApplications\"}}}},\"Total Applications\":{\"sum_bucket\":{\"buckets_path\":\"state.stateApplications\"}}}}}}"
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
        "chartResponseMap" : "totalApplicationsv2",
        "action" : "differenceOfNumbers",
        "upwardIndicator" : "positive",
        "downwardIndicator" : "negative",
        "textMessage" : "$indicator$value% than last $insightInterval",
        "colorCode" : "#228B22",
        "insightInterval" : "year"
      }
    },
  
    "tlCollectionByTradeTypev2": {
      "chartName": "DSS_TL_COLLECTION_BY_TRADE_TYPE",
      "queries": [
        {
          "module": "COMMON",
          "dateRefField": "date",
          "requestQueryMap": "{\"state\" : \"state.keyword\",\"tenantId\" : \"ulb.keyword\"}",
          "indexName": "tl-national-dashboard",
          "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[]}},\"aggs\":{\"Trade Type\":{\"terms\":{\"field\":\"tradeType.keyword\"},\"aggs\":{\"Total collection\":{\"sum\":{\"field\":\"todaysCollectionForTradeType\"}}}}}}}}"
        }
      ],
      "chartType": "pie",
      "valueType": "amount",
      "drillChart": "none",
      "documentType": "_doc",
      "action": "",
      "aggregationPaths": [
        "Trade Type"
      ],
      "insight": {
        
      },
      "_comment": " "
    },
  
    "tlTradeLicenseByStatusv2": {
      "chartName": "DSS_TL_COLLECTION_BY_TRADE_TYPE",
      "queries": [
        {
          "module": "COMMON",
          "dateRefField": "date",
          "requestQueryMap": "{\"state\" : \"state.keyword\",\"tenantId\" : \"ulb.keyword\"}",
          "indexName": "tl-national-dashboard",
          "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[]}},\"aggs\":{\"Status\":{\"terms\":{\"field\":\"status.keyword\"},\"aggs\":{\"Total Licenses\":{\"sum\":{\"field\":\"todaysTradeLicensesForStatus\"}}}}}}}}"
        }
      ],
      "chartType": "pie",
      "valueType": "number",
      "drillChart": "none",
      "documentType": "_doc",
      "action": "",
      "aggregationPaths": [
        "Status"
      ],
      "insight": {
        
      },
      "_comment": " "
    },

    "tlTargetAchieved": {
      "chartName": "DSS_TARGET_ACHIEVED",
      "queries": [
        {
          "module": "COMMON",
          "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
          "dateRefField": "date",
          "indexName": "master-national-dashboard",
          
          "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"term\":{\"module.keyword\":\"TL\"}},\"aggs\":{\"Target Collection\":{\"sum\":{\"field\":\"budgetProposedForMunicipalCorporation\"}}}}}}"
        },
        {
          "module": "COMMON",
          "dateRefField": "date",
          "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
          "indexName": "tl-national-dashboard",
          "aggrQuery": "{\"aggs\":{\"Total Collection\":{\"sum\":{\"field\":\"todaysCollectionForTradeType\"}}}}"
        }
  
      ],
      "chartType": "metric",
      "valueType": "percentage",
      "drillChart": "none",
      "documentType": "_doc",
      "action": "percentage",
      "isRoundOff": true,
      "preActionTheory":{
        "Target Collection":"repsonseToDifferenceOfDates"
      },
      "aggregationPaths": [
        "Total Collection",
        "Target Collection"
      ],
      "insight": {
        "chartResponseMap" : "tlTargetAchieved",
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
  
    "tlTargetCollection": {
      "chartName": "DSS_TARGET_COLLECTION",
      "queries": [
        {
          "module": "COMMON",
          "requestQueryMap": "{\"state\" : \"state.keyword\", \"ulb\" : \"ulb.keyword\"}",
          "dateRefField": "date",
          "indexName": "master-national-dashboard",
          "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"term\":{\"module.keyword\":\"TL\"}},\"aggs\":{\"Target Collection\":{\"sum\":{\"field\":\"budgetProposedForMunicipalCorporation\"}}}}}}"
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
      },
      "_comment": " "
    },
  
    "tlTopPerformingUlbs": {
      "chartName": "NATIONAL_DSS_TOP_PERFORMING_STATES",
      "queries": [
        {
          "module": "COMMON",
          "requestQueryMap": "{\r\n  \"module\" : \"module.keyword\", \n\"ulb\" : \"ulb.keyword\"}",
          "dateRefField": "",
          "indexName": "master-national-dashboard",
          "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"term\":{\"module.keyword\":\"TL\"}},\"aggs\":{\"Target Collection\":{\"terms\":{\"field\":\"state.keyword\",\"order\":{\"Sum\":\"desc\"}},\"aggs\":{\"Sum\":{\"sum\":{\"field\":\"budgetProposedForMunicipalCorporation\"}}}}}}}}"
        },
        {
          "module": "COMMON",
          "dateRefField": "date",
          "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
          "indexName": "tl-national-dashboard",
          "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[]}},\"aggs\":{\"Total Collection\":{\"terms\":{\"field\":\"state.keyword\",\"order\":{\"Sum\":\"desc\"}},\"aggs\":{\"Sum\":{\"sum\":{\"field\":\"todaysCollectionForTradeType\"}}}}}}}}"
        }
      ],
      "chartType": "perform",
      "valueType": "percentage",
      "drillChart": "none",
      "documentType": "_doc",
      "action": "percentage",
      "isRoundOff": true,
      "plotLabel": "DSS_TARGET_ACHIEVED",
      "order": "desc",
      "limit": 3,
      "aggregationPaths": [
        "Total Collection","Target Collection"
      ],
      "insight": {
      },
      "_comment": " Top Performing Ulbs for target achieved"
    },
  
    "tlBottomPerformingUlbs": {
      "chartName": "NATIONAL_DSS_BOTTOM_PERFORMING_STATES",
      "queries": [
        {
          "module": "COMMON",
          "requestQueryMap": "{\r\n  \"module\" : \"module.keyword\", \n\"ulb\" : \"ulb.keyword\"}",
          "dateRefField": "",
          "indexName": "master-national-dashboard",
          "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"term\":{\"module.keyword\":\"TL\"}},\"aggs\":{\"Target Collection\":{\"terms\":{\"field\":\"state.keyword\",\"order\":{\"Sum\":\"asc\"}},\"aggs\":{\"Sum\":{\"sum\":{\"field\":\"budgetProposedForMunicipalCorporation\"}}}}}}}}"
        },
        {
          "module": "COMMON",
          "dateRefField": "date",
          "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
          "indexName": "tl-national-dashboard",
          "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[]}},\"aggs\":{\"Total Collection\":{\"terms\":{\"field\":\"state.keyword\",\"order\":{\"Sum\":\"asc\"}},\"aggs\":{\"Sum\":{\"sum\":{\"field\":\"todaysCollectionForTradeType\"}}}}}}}}"
        }
      ],
      "chartType": "perform",
      "valueType": "percentage",
      "drillChart": "none",
      "documentType": "_doc",
      "action": "percentage",
      "isRoundOff": true,
      "plotLabel": "DSS_TARGET_ACHIEVED",
      "order": "asc",
      "limit": 3,
      "aggregationPaths": [
        "Total Collection","Target Collection"
      ],
      "insight": {
      },
      "_comment": " Bottom Performing Ulbs for target achieved"
    },
  
    "tlactiveUlbs": {
      "chartName": "DSS_TL_TOTAL_ACTIVE_ULBS",
      "queries": [
        
        {
          "module": "COMMON",
          "dateRefField": "date",
          "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
          "indexName": "tl-national-dashboard",
          "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[]}},\"aggs\":{\"Active ULBs\":{\"cardinality\":{\"field\":\"ulb.keyword\"}}}}}}"
        }
      ],
      "chartType": "metric",
      "valueType": "number",
      "action": "",
      "documentType": "_doc",
      "drillChart": "none",
      "aggregationPaths": [
        "Active ULBs"
      ],
      "insight": {
        "chartResponseMap" : "tlactiveUlbs",
        "action" : "differenceOfNumbers",
        "upwardIndicator" : "positive",
        "downwardIndicator" : "negative",
        "textMessage" : "$indicator$value% than last $insightInterval",
        "colorCode" : "#228B22",
        "insightInterval" : "month",
        "isRoundOff": true
      },
      "_comment": " total ULBs count"
    },
    
    "licenseIssuedBoundaryRevenuev3": {
      "chartName": "DSS_TL_DEMAND_COLLECTION_BOUNDARY",
      "queries": [
        {
          "module": "COMMON",
          "requestQueryMap": "{\"state\" : \"state.keyword\"}",
          "dateRefField": "date",
          "indexName": "tl-national-dashboard",
          "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[]}},\"aggs\":{\"States\":{\"terms\":{\"field\":\"state.keyword\"},\"aggs\":{\"TL_Total_Collection\":{\"sum\":{\"field\":\"todaysCollectionForTradeType\"}},\"Total_Licence_Issued\":{\"sum\":{\"field\":\"todaysTradeLicensesForStatus\"}},\"intermediateAggrULB\":{\"terms\":{\"field\":\"ulb.keyword\"},\"aggs\":{\"intermediateAggrWard\":{\"terms\":{\"field\":\"ward.keyword\"},\"aggs\":{\"days\":{\"terms\":{\"field\":\"date\"},\"aggs\":{\"applications\":{\"avg\":{\"field\":\"transactions\"}}}},\"wardapplications\":{\"sum_bucket\":{\"buckets_path\":\"days.applications\"}}}},\"ulbApplications\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrWard.wardapplications\"}}}},\"Transactions\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrULB.ulbApplications\"}}}}}}}}"
        },
        {
          "module": "COMMON",
          "requestQueryMap": "{\"state\" : \"state.keyword\"}",
          "dateRefField": "date",
          "indexName": "master-national-dashboard",
          "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[],\"must\":[{\"term\":{\"module.keyword\":\"TL\"}}]}},\"aggs\":{\"States\":{\"terms\":{\"field\":\"state.keyword\"},\"aggs\":{\"Target_Collection\":{\"sum\":{\"field\":\"budgetProposedForMunicipalCorporation\"}}}}}}}}"
        }
        
      ],
      "filterKeys": [
        {"key": "state", "column": "States"}
      ],
      "postAggregationTheory" : "repsonseToDifferenceOfDates",
      "chartType": "xtable",
      "valueType": "number",
      "drillChart": "licenseIssuedTenantRevenuev3",
      "documentType": "_doc",
      "action": "",
      "plotLabel": "States",
      "aggregationPaths": [
        "TL_Total_Collection",
        "Transactions",
        "Total_Licence_Issued",
        "Target_Collection"
      ],
      "pathDataTypeMapping": [
        {
          "TL_Total_Collection": "amount"
        },
        {
          "Target_Collection": "amount"
        },
        {
          "Transactions": "number"
        },
        {
          "Total_Licence_Issued": "number"
        },
        {
          "TL_Target_Collection": "amount"
        }
      ],
      "computedFields": [
       {
          "postAggregationTheory" : "repsonseToDifferenceOfDates",
          "actionName": "AdditiveComputedField",
          "fields" : ["Target_Collection"],
          "newField" : "TL_Target_Collection",
          "_comments": "fields are field names picked from its aggregation query to use post aggregation newField value with given new field name  "
        },
        {
          "postAggregationTheory" : "",
          "actionName": "PercentageComputedField",
          "fields" : ["TL_Total_Collection", "TL_Target_Collection"],
          "newField" : "TL_Target_Achieved",
          "isRoundOff": true,
          "_comments": "fields are field names picked from its aggregation query to use post aggregation newField value with given new field name  "
        }
        
      ],
      "excludedColumns":["Target_Collection"],
      "insight": {
      },
      "_comment": ""
    },
  
    "licenseIssuedDDDRRevenuev3": {
      "chartName": "DSS_TL_DEMAND_COLLECTION_BOUNDARY",
      "queries": [
        {
          "module": "COMMON",
          "requestQueryMap": "{\"state\" : \"state.keyword\", \"regionId\" : \"region.keyword\"}",
          "dateRefField": "date",
          "indexName": "tl-national-dashboard",
          "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[]}},\"aggs\":{\"Regions\":{\"terms\":{\"field\":\"region.keyword\"},\"aggs\":{\"Total Collection\":{\"sum\":{\"field\":\"todaysCollectionForTradeType\"}},\"Transactions\":{\"sum\":{\"field\":\"transactions\"}},\"Total Licence Issued\":{\"sum\":{\"field\":\"todaysTradeLicensesForStatus\"}}}}}}}}"
        },
        {
          "module": "COMMON",
          "requestQueryMap": "{\"state\" : \"state.keyword\", \"regionId\" : \"region.keyword\"}",
          "dateRefField": "",
          "indexName": "master-national-dashboard",
          "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[]}},\"aggs\":{\"Regions\":{\"terms\":{\"field\":\"region.keyword\"},\"aggs\":{\"Target Collection\":{\"sum\":{\"field\":\"budgetProposedForMunicipalCorporation\"}}}}}}}}"
        }
      ],
      "filterKeys": [
        {"key": "regionId", "column": "Regions"}
      ],
      "postAggregationTheory" : "repsonseToDifferenceOfDates",
      "chartType": "xtable",
      "valueType": "number",
      "drillChart": "licenseIssuedTenantRevenuev3",
      "documentType": "_doc",
      "action": "",
      "plotLabel": "Regions",
      "aggregationPaths": [
        "Total Collection",
        "Transactions",
        "Total Licence Issued",
        "Target Collection"
      ],
      "pathDataTypeMapping": [
        {
          "Total Collection": "amount"
        },
        {
          "Transactions": "number"
        },
        {
          "Total Licence Issued": "number"
        },
        {
          "Target Collection": "amount"
        }
      ],
      "computedFields": [
        {
          "postAggregationTheory" : "repsonseToDifferenceOfDates",
          "actionName": "PercentageComputedField",
          "fields" : ["Total Collection", "Target Collection"],
          "newField" : "Target Achieved",
          "_comments": "fields are field names picked from its aggregation query to use post aggregation newField value with given new field name  "
        }
        
      ],
      "insight": {
      },
      "_comment": ""
    },
  
    "licenseIssuedTenantRevenuev3": {
      "chartName": "DSS_TL_DEMAND_COLLECTION_BOUNDARY",
      "queries": [
        {
          "module": "COMMON",
          "requestQueryMap": "{\"state\" : \"state.keyword\", \"regionId\" : \"region.keyword\", \"ulb\" : \"ulb.keyword\"}",
          "dateRefField": "date",
          "indexName": "tl-national-dashboard",
          "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[]}},\"aggs\":{\"Tenants\":{\"terms\":{\"field\":\"ulb.keyword\"},\"aggs\":{\"TL_Total_Collection\":{\"sum\":{\"field\":\"todaysCollectionForTradeType\"}},\"Total_Licence_Issued\":{\"sum\":{\"field\":\"todaysTradeLicensesForStatus\"}},\"intermediateAggrWard\":{\"terms\":{\"field\":\"ward.keyword\"},\"aggs\":{\"days\":{\"terms\":{\"field\":\"date\"},\"aggs\":{\"applications\":{\"avg\":{\"field\":\"transactions\"}}}},\"wardapplications\":{\"sum_bucket\":{\"buckets_path\":\"days.applications\"}}}},\"Transactions\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrWard.wardapplications\"}}}}}}}}"
        },
        {
          "module": "COMMON",
          "requestQueryMap": "{\"state\" : \"state.keyword\", \"regionId\" : \"region.keyword\", \"ulb\" : \"ulb.keyword\"}",
          "dateRefField": "date",
          "indexName": "master-national-dashboard",
          "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[],\"must\":[{\"term\":{\"module.keyword\":\"TL\"}}]}},\"aggs\":{\"Tenants\":{\"terms\":{\"field\":\"ulb.keyword\"},\"aggs\":{\"Target_Collection\":{\"sum\":{\"field\":\"budgetProposedForMunicipalCorporation\"}}}}}}}}"
        }
      ],
      "filterKeys": [
        {"key": "ulb", "column": "ULB"}
      ],
      "postAggregationTheory" : "repsonseToDifferenceOfDates",
      "chartType": "xtable",
      "valueType": "number",
      "drillChart": "licenseIssuedWardRevenuev3",
      "documentType": "_doc",
      "action": "",
      "plotLabel": "ULB",
      "aggregationPaths": [
        "TL_Total_Collection",
        "Transactions",
        "Total_Licence_Issued",
        "Target_Collection"
      ],
      "pathDataTypeMapping": [
        {
          "TL_Total_Collection": "amount"
        },
        {
          "Target_Collection": "amount"
        },
        {
          "Transactions": "number"
        },
        {
          "Total_Licence_Issued": "number"
        },
        {
          "TL_Target_Collection": "amount"
        }
      ],
      "computedFields": [
       {
          "postAggregationTheory" : "repsonseToDifferenceOfDates",
          "actionName": "AdditiveComputedField",
          "fields" : ["Target_Collection"],
          "newField" : "TL_Target_Collection",
          "_comments": "fields are field names picked from its aggregation query to use post aggregation newField value with given new field name  "
        },
        {
          "postAggregationTheory" : "",
          "actionName": "PercentageComputedField",
          "fields" : ["TL_Total_Collection", "TL_Target_Collection"],
          "newField" : "TL_Target_Achieved",
          "isRoundOff": true,
          "_comments": "fields are field names picked from its aggregation query to use post aggregation newField value with given new field name  "
        }
        
      ],
      "excludedColumns":["Target_Collection"],
      "insight": {
      },
      "_comment": ""
    },
  
    "licenseIssuedWardRevenuev3": {
      "chartName": "DSS_TL_DEMAND_COLLECTION_BOUNDARY",
      "queries": [
        {
          "module": "COMMON",
          "requestQueryMap": "{\"state\" : \"state.keyword\", \"regionId\" : \"region.keyword\", \"ulb\" : \"ulb.keyword\",\"ward\" : \"ward.keyword\" }",
          "dateRefField": "date",
          "indexName": "tl-national-dashboard",
          "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[]}},\"aggs\":{\"Wards\":{\"terms\":{\"field\":\"ward.keyword\"},\"aggs\":{\"TL_Total_Collection\":{\"sum\":{\"field\":\"todaysCollectionForTradeType\"}},\"Total_Licence_Issued\":{\"sum\":{\"field\":\"todaysTradeLicensesForStatus\"}},\"days\":{\"terms\":{\"field\":\"date\"},\"aggs\":{\"applications\":{\"avg\":{\"field\":\"transactions\"}}}},\"Transactions\":{\"sum_bucket\":{\"buckets_path\":\"days.applications\"}}}}}}}}"
        },
        {
          "module": "COMMON",
          "requestQueryMap": "{\"state\" : \"state.keyword\", \"regionId\" : \"region.keyword\", \"ulb\" : \"ulb.keyword\",\"ward\" : \"ward.keyword\"}",
          "dateRefField": "date",
          "indexName": "master-national-dashboard",
          "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[],\"must\":[{\"term\":{\"module.keyword\":\"TL\"}}]}},\"aggs\":{\"Wards\":{\"terms\":{\"field\":\"ward.keyword\"},\"aggs\":{\"Target_Collection\":{\"sum\":{\"field\":\"budgetProposedForMunicipalCorporation\"}}}}}}}}"
        }
      ],
      "filterKeys": [
        {"key": "ward", "column": "Wards"}
      ],
      "postAggregationTheory" : "repsonseToDifferenceOfDates",
      "chartType": "xtable",
      "valueType": "number",
      "drillChart": "none",
      "documentType": "_doc",
      "action": "",
      "plotLabel": "Wards",
      "aggregationPaths": [
        "TL_Total_Collection",
        "Transactions",
        "Total_Licence_Issued",
        "Target_Collection"
      ],
      "pathDataTypeMapping": [
        {
          "TL_Total_Collection": "amount"
        },
        {
          "Target_Collection": "amount"
        },
        {
          "Transactions": "number"
        },
        {
          "Total_Licence_Issued": "number"
        },
        {
          "TL_Target_Collection": "amount"
        }
      ],
      "computedFields": [
       {
          "postAggregationTheory" : "repsonseToDifferenceOfDates",
          "actionName": "AdditiveComputedField",
          "fields" : ["Target_Collection"],
          "newField" : "TL_Target_Collection",
          "_comments": "fields are field names picked from its aggregation query to use post aggregation newField value with given new field name  "
        },
        {
          "postAggregationTheory" : "",
          "actionName": "PercentageComputedField",
          "fields" : ["TL_Total_Collection", "TL_Target_Collection"],
          "newField" : "TL_Target_Achieved",
          "isRoundOff": true,
          "_comments": "fields are field names picked from its aggregation query to use post aggregation newField value with given new field name  "
        }
        
      ],
      "excludedColumns":["Target_Collection"],
      "insight": {
      },
      "_comment": ""
    },
  
    "licenceTaxHeadsBreakupState": {
      "chartName": "DSS_TL_TAX_HEAD_BREAKUP_BOUNDARY",
      "queries": [
        {
          "module": "COMMON",
          "requestQueryMap": "{\"state\" : \"state.keyword\"}",
          "dateRefField": "date",
          "indexName": "tl-national-dashboard",
          "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[]}},\"aggs\":{\"States\":{\"terms\":{\"field\":\"state.keyword\"},\"aggs\":{\"intermediateAggrULB\":{\"terms\":{\"field\":\"ulb.keyword\"},\"aggs\":{\"intermediateAggrWard\":{\"terms\":{\"field\":\"ward.keyword\"},\"aggs\":{\"days\":{\"terms\":{\"field\":\"date\"},\"aggs\":{\"applicationsTax\":{\"avg\":{\"field\":\"tlTax\"}},\"applicationsPenalty\":{\"avg\":{\"field\":\"adhocPenalty\"}},\"applicationsRebate\":{\"avg\":{\"field\":\"adhocRebate\"}}}},\"wardapplicationsTax\":{\"sum_bucket\":{\"buckets_path\":\"days.applicationsTax\"}},\"wardapplicationsPenalty\":{\"sum_bucket\":{\"buckets_path\":\"days.applicationsPenalty\"}},\"wardapplicationsRebate\":{\"sum_bucket\":{\"buckets_path\":\"days.applicationsRebate\"}}}},\"ulbApplicationsTax\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrWard.wardapplicationsTax\"}},\"ulbApplicationsPenalty\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrWard.wardapplicationsPenalty\"}},\"ulbApplicationsRebate\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrWard.wardapplicationsRebate\"}}}},\"TL_Tax\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrULB.ulbApplicationsTax\"}},\"Adhoc_Penalty\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrULB.ulbApplicationsPenalty\"}},\"Adhoc_Rebate\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrULB.ulbApplicationsRebate\"}},\"Total_Amount\":{\"bucket_script\":{\"buckets_path\":{\"Adhoc_Rebate\":\"Adhoc_Rebate\",\"TL_Tax\":\"TL_Tax\",\"Adhoc_Penalty\":\"Adhoc_Penalty\"},\"script\":{\"source\":\" params.TL_Tax + params.Adhoc_Penalty - params.Adhoc_Rebate\"}}}}}}}}}"
        }
      ],
      "filterKeys": [
        {"key": "state", "column": "States"}
      ],
      "chartType": "xtable",
      "valueType": "amount",
      "drillChart": "licenceTaxHeadsBreakupTenant",
      "documentType": "_doc",
      "action": "",
      "plotLabel": "States",
      "aggregationPaths": [
        "TL_Tax",
        "Adhoc_Penalty",
        "Adhoc_Rebate",
        "Total_Amount"
      ],
      "pathDataTypeMapping": [
        {
          "TL_Tax": "amount"
        },
        {
          "Adhoc_Penalty": "amount"
        },
        {
          "Adhoc_Rebate": "amount"
        },
        {
          "Total_Amount":"amount"
        }
      ],
  
      
  
      "insight": {
      },
      "_comment": ""
    },
  
    "licenceTaxHeadsBreakupDDRv3": {
      "chartName": "DSS_TL_TAX_HEAD_BREAKUP_BOUNDARY",
      "queries": [
        {
          "module": "COMMON",
          "requestQueryMap": "{\"state\" : \"state.keyword\", \"regionId\" : \"region.keyword\"}",
          "dateRefField": "date",
          "indexName": "tl-national-dashboard",
          "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[]}},\"aggs\":{\"Regions\":{\"terms\":{\"field\":\"region.keyword\"},\"aggs\":{\"TL Tax\":{\"sum\":{\"field\":\"tlTax\"}},\"Adhoc Penalty\":{\"sum\":{\"field\":\"adhocPenalty\"}},\"Adhoc Rebate\":{\"sum\":{\"field\":\"adhocRebate\"}}}}}}}}"
        }
      ],
      "filterKeys": [
        {"key": "regionId", "column": "Regions"}
      ],
      "chartType": "xtable",
      "valueType": "amount",
      "drillChart": "licenceTaxHeadsBreakupTenant",
      "documentType": "_doc",
      "action": "",
      "plotLabel": "Regions",
      "aggregationPaths": [
        "TL Tax",
        "Adhoc Penalty",
        "Adhoc Rebate"
      ],
      "pathDataTypeMapping": [
        {
          "TL Tax": "amount"
        },
        {
          "Adhoc Penalty": "amount"
        },
        {
          "Adhoc Rebate": "amount"
        }
      ],
      "computedFields": [
        {
          "postAggregationTheory" : "",
          "actionName": "AdditiveComputedField",
          "fields" : ["TL Tax", "Adhoc Penalty", "Adhoc Rebate"],
          "newField" : "Total Amount",
          "_comments": "fields are field names picked from its aggregation query to use post aggregation newField value with given new field name  "
        }
      ],
  
      "insight": {
      },
      "_comment": ""
    },
  
    "licenceTaxHeadsBreakupTenant": {
      "chartName": "DSS_TL_TAX_HEAD_BREAKUP_BOUNDARY",
      "queries": [
        {
          "module": "COMMON",
          "requestQueryMap": "{\"state\" : \"state.keyword\", \"regionId\" : \"region.keyword\", \"ulb\" : \"ulb.keyword\"}",
          "dateRefField": "date",
          "indexName": "tl-national-dashboard",
          "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[]}},\"aggs\":{\"ULBs\":{\"terms\":{\"field\":\"ulb.keyword\"},\"aggs\":{\"intermediateAggrWard\":{\"terms\":{\"field\":\"ward.keyword\"},\"aggs\":{\"days\":{\"terms\":{\"field\":\"date\"},\"aggs\":{\"applicationsTax\":{\"avg\":{\"field\":\"tlTax\"}},\"applicationsPenalty\":{\"avg\":{\"field\":\"adhocPenalty\"}},\"applicationsRebate\":{\"avg\":{\"field\":\"adhocRebate\"}}}},\"wardapplicationsTax\":{\"sum_bucket\":{\"buckets_path\":\"days.applicationsTax\"}},\"wardapplicationsPenalty\":{\"sum_bucket\":{\"buckets_path\":\"days.applicationsPenalty\"}},\"wardapplicationsRebate\":{\"sum_bucket\":{\"buckets_path\":\"days.applicationsRebate\"}}}},\"TL_Tax\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrWard.wardapplicationsTax\"}},\"Adhoc_Penalty\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrWard.wardapplicationsPenalty\"}},\"Adhoc_Rebate\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrWard.wardapplicationsRebate\"}},\"Total_Amount\":{\"bucket_script\":{\"buckets_path\":{\"Adhoc_Rebate\":\"Adhoc_Rebate\",\"TL_Tax\":\"TL_Tax\",\"Adhoc_Penalty\":\"Adhoc_Penalty\"},\"script\":{\"source\":\" params.TL_Tax + params.Adhoc_Penalty - params.Adhoc_Rebate\"}}}}}}}}}"
        }
      ],
      "filterKeys": [
        {"key": "ulb", "column": "ULB"}
      ],
      "chartType": "xtable",
      "valueType": "amount",
      "drillChart": "licenceTaxHeadsBreakupWardv3",
      "documentType": "_doc",
      "action": "",
      "plotLabel": "ULB",
      "aggregationPaths": [
        "TL_Tax",
        "Adhoc_Penalty",
        "Adhoc_Rebate",
        "Total_Amount"
      ],
      "pathDataTypeMapping": [
        {
          "TL_Tax": "amount"
        },
        {
          "Adhoc_Penalty": "amount"
        },
        {
          "Adhoc_Rebate": "amount"
        },
        {
          "Total_Amount": "amount"
        }
      ],
      
  
      "insight": {
      },
      "_comment": ""
    },
  
    "licenceTaxHeadsBreakupWardv3": {
      "chartName": "DSS_TL_TAX_HEAD_BREAKUP_BOUNDARY",
      "queries": [
        {
          "module": "COMMON",
          "requestQueryMap": "{\"state\" : \"state.keyword\", \"regionId\" : \"region.keyword\", \"ulb\" : \"ulb.keyword\",\"ward\" : \"ward.keyword\" }",
          "dateRefField": "date",
          "indexName": "tl-national-dashboard",
          "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[]}},\"aggs\":{\"Wards\":{\"terms\":{\"field\":\"ward.keyword\"},\"aggs\":{\"days\":{\"terms\":{\"field\":\"date\"},\"aggs\":{\"applicationsTax\":{\"avg\":{\"field\":\"tlTax\"}},\"applicationsPenalty\":{\"avg\":{\"field\":\"adhocPenalty\"}},\"applicationsRebate\":{\"avg\":{\"field\":\"adhocRebate\"}}}},\"TL_Tax\":{\"sum_bucket\":{\"buckets_path\":\"days.applicationsTax\"}},\"Adhoc_Penalty\":{\"sum_bucket\":{\"buckets_path\":\"days.applicationsPenalty\"}},\"Adhoc_Rebate\":{\"sum_bucket\":{\"buckets_path\":\"days.applicationsRebate\"}},\"Total_Amount\":{\"bucket_script\":{\"buckets_path\":{\"Adhoc_Rebate\":\"Adhoc_Rebate\",\"TL_Tax\":\"TL_Tax\",\"Adhoc_Penalty\":\"Adhoc_Penalty\"},\"script\":{\"source\":\" params.TL_Tax + params.Adhoc_Penalty - params.Adhoc_Rebate\"}}}}}}}}}"
        }
      ],
      "filterKeys": [
        {"key": "ward", "column": "Wards"}
      ],
      "chartType": "xtable",
      "valueType": "amount",
      "drillChart": "none",
      "documentType": "_doc",
      "action": "",
      "plotLabel": "Wards",
      "aggregationPaths": [
        "TL_Tax",
        "Adhoc_Penalty",
        "Adhoc_Rebate",
        "Total_Amount"
      ],
      "pathDataTypeMapping": [
        {
          "TL_Tax": "amount"
        },
        {
          "Adhoc_Penalty": "amount"
        },
        {
          "Adhoc_Rebate": "amount"
        },
        {
          "Total_Amount" : "amount"
        }
      ],
      
  
      "insight": {
      },
      "_comment": ""
    },

    "tlTopPerformingUlbsCompletionRate": {
      "chartName": "NATIONAL_DSS_TOP_3_PERFORMING_STATES_COMPLETION_RATE",
      "queries": [
        
        {
          "module": "COMMON",
          "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
          "dateRefField": "date",
          "indexName": "tl-national-dashboard",
          "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[]}},\"aggs\":{\"Licenses Within SLA\":{\"terms\":{\"field\":\"state.keyword\"},\"aggs\":{\"intermediateAggrULB\":{\"terms\":{\"field\":\"ulb.keyword\"},\"aggs\":{\"intermediateAggrWard\":{\"terms\":{\"field\":\"ward.keyword\"},\"aggs\":{\"days\":{\"terms\":{\"field\":\"date\"},\"aggs\":{\"applications\":{\"avg\":{\"field\":\"todaysLicenseIssuedWithinSLA\"}}}},\"wardapplications\":{\"sum_bucket\":{\"buckets_path\":\"days.applications\"}}}},\"ulbApplications\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrWard.wardapplications\"}}}},\"Licenses Within SLA\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrULB.ulbApplications\"}}}},\"Total Licenses\":{\"terms\":{\"field\":\"state.keyword\"},\"aggs\":{\"intermediateAggrULB\":{\"terms\":{\"field\":\"ulb.keyword\"},\"aggs\":{\"intermediateAggrWard\":{\"terms\":{\"field\":\"ward.keyword\"},\"aggs\":{\"days\":{\"terms\":{\"field\":\"date\"},\"aggs\":{\"licenses\":{\"sum\":{\"field\":\"todaysTradeLicensesForStatus\"}}}},\"wardlicenses\":{\"sum_bucket\":{\"buckets_path\":\"days.licenses\"}}}},\"ulblicenses\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrWard.wardlicenses\"}}}},\"totalLicenses\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrULB.ulblicenses\"}}}}}}}}"
        }
      ],
      "chartType": "perform",
      "valueType": "percentage",
      "drillChart": "none",
      "documentType": "_doc",
      "action": "percentage",
      "isRoundOff": true,
      "plotLabel": "DSS_COMPLETION_RATE",
      "order": "desc",
      "limit": 3,
      "aggregationPaths": [
        "Licenses Within SLA",
        "Total Licenses"
      ],
      "insight": {
      },
      "_comment": " Top Performing Ulbs for Completion rate"
    },

    "tlBottomPerformingUlbsCompletionRate": {
      "chartName": "NATIONAL_DSS_BOTTOM_3_PERFORMING_STATES_COMPLETION_RATE",
      "queries": [
        
        {
          "module": "COMMON",
          "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
          "dateRefField": "date",
          "indexName": "tl-national-dashboard",
          "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[]}},\"aggs\":{\"Licenses Within SLA\":{\"terms\":{\"field\":\"state.keyword\"},\"aggs\":{\"intermediateAggrULB\":{\"terms\":{\"field\":\"ulb.keyword\"},\"aggs\":{\"intermediateAggrWard\":{\"terms\":{\"field\":\"ward.keyword\"},\"aggs\":{\"days\":{\"terms\":{\"field\":\"date\"},\"aggs\":{\"applications\":{\"avg\":{\"field\":\"todaysLicenseIssuedWithinSLA\"}}}},\"wardapplications\":{\"sum_bucket\":{\"buckets_path\":\"days.applications\"}}}},\"ulbApplications\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrWard.wardapplications\"}}}},\"Licenses Within SLA\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrULB.ulbApplications\"}}}},\"Total Licenses\":{\"terms\":{\"field\":\"state.keyword\"},\"aggs\":{\"intermediateAggrULB\":{\"terms\":{\"field\":\"ulb.keyword\"},\"aggs\":{\"intermediateAggrWard\":{\"terms\":{\"field\":\"ward.keyword\"},\"aggs\":{\"days\":{\"terms\":{\"field\":\"date\"},\"aggs\":{\"licenses\":{\"sum\":{\"field\":\"todaysTradeLicensesForStatus\"}}}},\"wardlicenses\":{\"sum_bucket\":{\"buckets_path\":\"days.licenses\"}}}},\"ulblicenses\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrWard.wardlicenses\"}}}},\"totalLicenses\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrULB.ulblicenses\"}}}}}}}}"
        }
      ],
      "chartType": "perform",
      "valueType": "percentage",
      "drillChart": "none",
      "documentType": "_doc",
      "action": "percentage",
      "isRoundOff": true,
      "plotLabel": "DSS_COMPLETION_RATE",
      "order": "asc",
      "limit": 3,
      "aggregationPaths": [
        "Licenses Within SLA",
        "Total Licenses"
      ],
      "insight": {
      },
      "_comment": " Top Performing Ulbs for Completion rate"
    },

    "cumulativeLicenseIssuedv2": {
      "chartName": "DSS_TL_CUMULATIVE_LICENSE_ISSUED",
      "queries": [
        {
          "module": "COMMON",
          "indexName": "tl-national-dashboard",
          "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[]}},\"aggs\":{\"Trade Licence Issued\":{\"date_histogram\":{\"field\":\"date\",\"interval\":\"month\"},\"aggs\":{\"Count\":{\"sum\":{\"field\":\"todaysTradeLicensesForStatus\"}}}}}}}}",
          "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
          "dateRefField": "date"
        },
        {
          "module": "COMMON",
          "indexName": "tl-national-dashboard",
          "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"Total Application\":{\"date_histogram\":{\"field\":\"date\",\"interval\":\"month\"},\"aggs\":{\"state\":{\"terms\":{\"field\":\"state.keyword\"},\"aggs\":{\"intermediateAggrULB\":{\"terms\":{\"field\":\"ulb.keyword\"},\"aggs\":{\"intermediateAggrWard\":{\"terms\":{\"field\":\"ward.keyword\"},\"aggs\":{\"days\":{\"terms\":{\"field\":\"date\"},\"aggs\":{\"applications\":{\"avg\":{\"field\":\"todaysApplications\"}}}},\"wardapplications\":{\"sum_bucket\":{\"buckets_path\":\"days.applications\"}}}},\"ulbApplications\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrWard.wardapplications\"}}}},\"stateApplications\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrULB.ulbApplications\"}}}},\"allApplications\":{\"sum_bucket\":{\"buckets_path\":\"state.stateApplications\"}}}}}}}}",
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
        "Trade Licence Issued",
        "Total Application"
      ],
      "isCumulative": true,
      "interval": "month",
      "insight": {
      },
      "_comment": " Total Number of License having issued"
    },
    
    "tlStatusByState": {
    "chartName": "DSS_TL_STATUS_BY_STATE",
    "queries": [
      {
        "module": "COMMON",
        "requestQueryMap": "{\"state\" : \"state.keyword\"} ",
        "dateRefField": "date",
        "indexName": "tl-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"ulb.keyword\":\"pb.testing\"}}]}},\"aggs\":{\"State\":{\"terms\":{\"field\":\"state.keyword\",\"size\":1000},\"aggs\":{\"Status\":{\"terms\":{\"field\":\"status.keyword\",\"size\":1000,\"min_doc_count\":0},\"aggs\":{\"License Issued\":{\"sum\":{\"field\":\"todaysTradeLicensesForStatus\"}}}}}}}}}}"
        
      }
    ],
    "filterKeys": [
      {"key": "state", "column": "State"}
    ],
    "chartType": "xtable",
    "valueType": "number",
    "drillChart": "tlStatusByUlb",
    "drillFields": [
      ""
    ],
    "pathDataTypeMapping": [
      
      {
        "INITIATED": "number"
      },
      {
        "FIELDINSPECTION": "number"
      },
      {
        "REJECTED": "number"
      },
      {
        "APPROVED": "number"
      },
      {
        "APPLIED": "number"
      },
      {
        "PENDINGAPPROVAL": "number"
      },
      {
        "CANCELLED": "number"
      },
      {
        "PENDINGPAYMENT": "number"
      },
      {
        "PAID": "number"
      }
    ],

    "documentType": "_doc",
    "action": "",
    "plotLabel": "State",
    
    


    "insight": {
    },
    "_comment": ""
  },

  "tlStatusByUlb": {
    "chartName": "DSS_TL_STATUS_BY_WARD",
    "queries": [
      {
        "module": "COMMON",
        "requestQueryMap": "{\"state\" : \"state.keyword\" , \"ulb\" : \"ulb.keyword\" } ",
        "dateRefField": "date",
        "indexName": "tl-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"ulb.keyword\":\"pb.testing\"}}]}},\"aggs\":{\"ULB\":{\"terms\":{\"field\":\"ulb.keyword\",\"size\":1000},\"aggs\":{\"Status\":{\"terms\":{\"field\":\"status.keyword\",\"size\":1000,\"min_doc_count\":0},\"aggs\":{\"License Issued\":{\"sum\":{\"field\":\"todaysTradeLicensesForStatus\"}}}}}}}}}}"
        
      }
    ],
    "filterKeys": [
      {"key": "ulb", "column": "ULB"}
    ],
    "chartType": "xtable",
    "valueType": "number",
    "drillChart": "tlStatusByWard",
    "drillFields": [
      ""
    ],
    "pathDataTypeMapping": [
      
      {
        "INITIATED": "number"
      },
      {
        "FIELDINSPECTION": "number"
      },
      {
        "REJECTED": "number"
      },
      {
        "APPROVED": "number"
      },
      {
        "APPLIED": "number"
      },
      {
        "PENDINGAPPROVAL": "number"
      },
      {
        "CANCELLED": "number"
      },
      {
        "PENDINGPAYMENT": "number"
      },
      {
        "PAID": "number"
      }
    ],

    "documentType": "_doc",
    "action": "",
    "plotLabel": "ULB",
    
    


    "insight": {
    },
    "_comment": ""
  },

  "tlStatusByWard": {
    "chartName": "DSS_TL_STATUS_BY_WARD",
    "queries": [
      {
        "module": "COMMON",
        "requestQueryMap": "{\"state\" : \"state.keyword\" , \"ulb\" : \"ulb.keyword\" , \"ward\" : \"ward.keyword\" } ",
        "dateRefField": "date",
        "indexName": "tl-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"ulb.keyword\":\"pb.testing\"}}]}},\"aggs\":{\"Ward\":{\"terms\":{\"field\":\"ward.keyword\",\"size\":1000},\"aggs\":{\"Status\":{\"terms\":{\"field\":\"status.keyword\",\"size\":1000,\"min_doc_count\":0},\"aggs\":{\"License Issued\":{\"sum\":{\"field\":\"todaysTradeLicensesForStatus\"}}}}}}}}}}"
        
      }
    ],
    "filterKeys": [
      {"key": "ward", "column": "Ward"}
    ],
    "chartType": "table",
    "valueType": "number",
    "drillChart": "none",
    "drillFields": [
      ""
    ],
    "pathDataTypeMapping": [
      
      {
        "INITIATED": "number"
      },
      {
        "FIELDINSPECTION": "number"
      },
      {
        "REJECTED": "number"
      },
      {
        "APPROVED": "number"
      },
      {
        "APPLIED": "number"
      },
      {
        "PENDINGAPPROVAL": "number"
      },
      {
        "CANCELLED": "number"
      },
      {
        "PENDINGPAYMENT": "number"
      },
      {
        "PAID": "number"
      }
    ],

    "documentType": "_doc",
    "action": "",
    "plotLabel": "Ward",
    
    


    "insight": {
    },
    "_comment": ""
  }
```

[Click here for the complete configuration](https://github.com/egovernments/configs/blob/qa/egov-dss-dashboards/dashboard-analytics/ChartApiConfig.json)

**Master Dashboard Configuration:** Master dashboard configuration is the main configuration that defines the dashboards to be painted on the screen. This includes the visualizations, their groups, the charts and the chart dimensions in terms of height and width.

```
{
      "name": "DSS_TRADE_LICENSE_DASHBOARD",
      "id": "national-tradelicense",
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
                "height": 350,
                "width": 5
              },
              "vizType": "metric-collection",
              "label": "DSS_OVERVIEW",
              "noUnit": true,
              "isCollapsible": false,
              "charts": [
                {
                  "id": "tradeLicenseTodaysCollectionv2",
                  "name": "DSS_TODAYS_COLLECTION",
                  "code": "",
                  "chartType": "metric",
                  "filter": {"title": "TODAY"},
                  "headers": []
                },
                {
                  "id": "tradeLicenseTotalCollectionv2",
                  "name": "DSS_TOTAL_COLLECTION",
                  "code": "",
                  "chartType": "metric",
                  "filter": "",
                  "headers": []
                },
                {
                  "id": "tlTargetCollection",
                  "name": "DSS_TARGET_COLLECTION",
                  "code": "",
                  "chartType": "metric",
                  "filter": "",
                  "headers": []
                },
                {
                  "id": "tlTargetAchieved",
                  "name": "DSS_TARGET_ACHIEVED",
                  "code": "",
                  "chartType": "metric",
                  "filter": "",
                  "headers": []
                }
              ]
            },
            {
              "id": 312,
              "name": "Total Cumulative Collection",
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
                  "id": "tlMonthlyCumulativeCollectionv2",
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
              "name": "NATIONAL_DSS_TOP_PERFORMING_STATES",
              "dimensions": {
                "height": 250,
                "width": 4
              },
              "vizType": "performing-metric",
              "label": "",
              "noUnit": false,
              "isCollapsible": false,
              "charts": [
                {
                  "id": "tlTopPerformingUlbs",
                  "name": "NATIONAL_DSS_TOP_PERFORMING_STATES",
                  "code": "",
                  "chartType": "bar",
                  "filter": "",
                  "headers": []
                }
              ]
            },
            {
              "id": 322,
              "name": "NATIONAL_DSS_BOTTOM_PERFORMING_STATES",
              "dimensions": {
                "height": 250,
                "width": 4
              },
              "vizType": "performing-metric",
              "label": "",
              "noUnit": false,
              "isCollapsible": false,
              "charts": [
                {
                  "id": "tlBottomPerformingUlbs",
                  "name": "NATIONAL_DSS_BOTTOM_PERFORMING_STATES",
                  "code": "",
                  "chartType": "bar",
                  "filter": "",
                  "headers": []
                }
              ]
            },
            {
              "id": 323,
              "name": "DSS_TL_LICENSE_BY_TYPE",
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
                  "id": "tlCollectionByTradeTypev2",
                  "name": "DSS_TL_COLLECTION_BY_TRADE_TYPE",
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
              "name": "DSS_TL_KEY_FY_INDICATORS",
              "dimensions": {
                "height": 350,
                "width": 12
              },
              "vizType": "chart",
              "label": "",
              "noUnit": false,
              "isCollapsible": false,
              "charts": [
                {
                  "id": "licenseIssuedBoundaryRevenuev3",
                  "name": "DSS_TL_DEMAND_COLLECTION_BOUNDARY",
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
              "name": "DSS_TL_TAX_HEAD_BREAKUP",
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
                  "id": "licenceTaxHeadsBreakupState",
                  "name": "DSS_TL_TAX_HEAD_BREAKUP_BOUNDARY",
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
          "name": "DSS_SERVICE",
          "vizArray": [
            {
              "id": 341,
              "name": "DSS_OVERVIEW",
              "dimensions": {
                "height": 350,
                "width": 5
              },
              "vizType": "metric-collection",
              "isCollapsible": false,
              "label": "DSS_OVERVIEW",
              "charts": [
                {
                  "id": "totalApplicationsv2",
                  "name": "DSS_TOTAL_APPLICATION",
                  "code": "",
                  "chartType": "metric",
                  "filter": "",
                  "headers": []
                },
                {
                  "id": "totalLicensesIssuedv2",
                  "name": "DSS_TOTAL_LICENSES",
                  "code": "",
                  "chartType": "metric",
                  "filter": "",
                  "headers": []
                }
              ]
            },
            {
              "id": 342,
              "name": "DSS_TL_CUMULATIVE_LICENSE_ISSUED",
              "dimensions": {
                "height": 350,
                "width": 7
              },
              "vizType": "chart",
              "isCollapsible": false,
              "charts": [
                {
                  "id": "cumulativeLicenseIssuedv2",
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
          "row": 7,
          "name": "DSS_SERVICE",
          "vizArray": [
            {
              "id": 351,
              "name": "NATIONAL_DSS_TOP_3_PERFORMING_STATES_COMPLETION_RATE",
              "dimensions": {
                "height": 250,
                "width": 4
              },
              "vizType": "performing-metric",
              "label": "",
              "noUnit": false,
              "isCollapsible": false,
              "charts": [
                {
                  "id": "tlTopPerformingUlbsCompletionRate",
                  "name": "NATIONAL_DSS_TOP_3_PERFORMING_STATES_COMPLETION_RATE",
                  "code": "",
                  "chartType": "bar",
                  "filter": "",
                  "headers": []
                }
              ]
            },
            {
              "id": 352,
              "name": "NATIONAL_DSS_BOTTOM_3_PERFORMING_STATES_COMPLETION_RATE",
              "dimensions": {
                "height": 250,
                "width": 4
              },
              "vizType": "performing-metric",
              "noUnit": false,
              "isCollapsible": false,
              "charts": [
                {
                  "id": "tlBottomPerformingUlbsCompletionRate",
                  "name": "NATIONAL_DSS_BOTTOM_3_PERFORMING_STATES_COMPLETION_RATE",
                  "code": "",
                  "chartType": "bar",
                  "filter": "",
                  "headers": []
                }
              ]
            },
            {
              "id": 353,
              "name": "DSS_TL_LICENSE_BY_STATUS",
              "dimensions": {
                "height": 250,
                "width": 4
              },
              "vizType": "chart",
              "isCollapsible": false,
              "charts": [
                {
                  "id": "tlTradeLicenseByStatusv2",
                  "name": "DSS_TL_COLLECTION_BY_TRADE_TYPE",
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
          "row": 8,
          "name": "DSS_SERVICE",
          "vizArray": [
            {
              "id": 351,
              "name": "DSS_TL_STATUS_BOUNDARY",
              "dimensions": {
                "height": 250,
                "width": 4
              },
              "vizType": "chart",
              "label": "",
              "noUnit": false,
              "isCollapsible": true,
              "charts": [
                {
                  "id": "tlStatusByState",
                  "name": "",
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

[Click here for complete configuration](https://github.com/egovernments/configs/blob/qa/egov-dss-dashboards/dashboard-analytics/MasterDashboardConfig.json)

**Role Dashboard Mappings Configuration:** Master Dashboard Configuration which was explained earlier hold the list of Dashboards which are available.

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
          "name": "National Trade License",
          "id": "national-tradelicense"
        }
      ]
    }

  ]
}
```

[Click here for complete configuration](https://github.com/egovernments/configs/blob/qa/egov-dss-dashboards/dashboard-analytics/RoleDashboardMappingsConf.json)

**MDMS Configuration to be added:** _common-masters/uiCommonConstants.json_

```
"national-tradelicense": {
                  "routePath": "/dashboard/national-tradelicense",
                  "isOrigin": true
               }
```

[Click here for complete configuration](https://github.com/egovernments/egov-mdms-data/blob/QA/data/pb/common-masters/uiCommonConstants.json)

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

[Click here for complete configuration](https://github.com/egovernments/egov-mdms-data/blob/QA/data/pb/ACCESSCONTROL-ROLEACTIONS/roleactions.json)

Action test.json:

```
{
      "id": {{PlaceHolder1}},
      "name": "NSS Dashboard Config National Trade License",
      "url": "/dashboard-analytics/dashboard/getDashboardConfig/national-tradelicense",
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
      "name": "National Dashboard Trade License",
      "url": "url",
      "displayName": "National Trade License",
      "orderNumber": 4,
      "parentModule": "ndss-dashboard",
      "enabled": true,
      "serviceCode": "NDSS",
      "code": "null",
      "path": "NatDashboard.TradeLicense",
      "navigationURL": "/digit-ui/employee/dss/dashboard/national-tradelicense",
      "leftIcon": "places:business-center",
      "rightIcon": ""
    }
```

[Click here for complete configuration](https://github.com/egovernments/egov-mdms-data/blob/QA/data/pb/ACCESSCONTROL-ACTIONS-TEST/actions-test.json)

Trade License-National DSS contains multiple graphs that represent trade license data. Each graph has its own configuration that describes the chart and its type.&#x20;

National DSS contains the following charts in Trade License:

**Revenue Tab:**

* Overview
* Total Cumulative Collection
* Top 3 States By Performance
* Bottom 3 States by Performance
* Collection by Trade Type
* Key Financial Indicators
* Tax Heads

**Service Tab:**

* Overview
* Total Cumulative Licenses Issued
* Top 3 Performing States By Completion
* Bottom 3 Performing States By Completion
* Trade Licenses by Status
* Status Report

**Revenue Tab:**

**Overview:** The **** Overview graph contains multiple data information as below in the selected time period.

* **Today’s Collection:** This represents the day’s collection amount.
* &#x20;**Total Collection:** This represents the total collection amount.
* **Target Collection:** This represents the target collection amount.
* **Target Achievement:** This represents the target achieved in percentage. This is calculated by the formula - (Total Collection/Target Collection)\*100

**Total Cumulative Collection:** This graph displays the Trade License collection amount information on a monthly base as a cumulative line graph. The graph changes as per the selected denomination amount filter.

**line** - this graph/chart is data representation on date histograms or date groupings.

![](<../../../../.gitbook/assets/image (350).png>)

**Top 3 Performing States By Completion:** This graph represents the States based on the Target achieved in bar chart representation with the % of target achieved in descending order.

![](<../../../../.gitbook/assets/image (353).png>)

**Bottom 3 States by Performance:** This graph represents the States based on the Target achieved in bar chart representation with the % of target achieved in ascending order.

![](<../../../../.gitbook/assets/image (397).png>)

**Collection by Trade Type:** This graph shows the collection amount based on the trade type.

![](<../../../../.gitbook/assets/image (420).png>)

**Key Financial Indicators:** This tabular chart representation displays multiple Trade License information like Target Collection, Total Collection, Total Transactions, Total Licenses Issued and Target Achievement (in %). The table shows the data at the State level and also provides the drill-down chart for each State to ULB and from ULB to the ward level data.

_**xtable**_ type allows adding multiple computed fields with the aggregated fields dynamically added.

To add multiple computed columns, define **computedFields** \[]  where actionName (IComputedField\<T> interface), fields \[] names as existing in query key, newField as name to appear for computation must be defined.

![](<../../../../.gitbook/assets/image (357).png>)

Clicking on any State name provides the drill-down charts and data for that specific ULB.

![](<../../../../.gitbook/assets/image (366).png>)

Clicking on the ULB navigates to the ward-level data for that specific ULB.

![](<../../../../.gitbook/assets/image (361).png>)

**Tax Heads:** This tabular chart representation graph shows multiple Trade License information like TL Tax, Adhoc Penalty, Adhoc Rebate, Total Amount etc. The table displays the data at the State level and also provides a drill-down chart for each State to ULB and from ULB to ward level data for the same.

_**table**_ type allows adding multiple aggregated fields.

![](<../../../../.gitbook/assets/image (377).png>)

Clicking on the State name provides the drill-down charts that represent the specific ULB data.

![](<../../../../.gitbook/assets/image (400).png>)

Clicking on the ULB navigates to the ward level data illustration.

![](<../../../../.gitbook/assets/image (378).png>)

**Service Tab:**

**Overview:** The **** Overview graph illustrates multiple data information as below in the selected time period.

* **Total Applications:** This represents the total number of trade license applications.
* **Total Licenses:**  This represents the total licenses issued.

![](<../../../../.gitbook/assets/image (390).png>)

**Total Cumulative Licenses Issued:** This graph displays the licenses issued and total application information on a monthly base as a cumulative line graph.

**line** - this graph/chart is data representation on date histograms or date groupings.

![](<../../../../.gitbook/assets/image (367).png>)

**Top 3 Performing States By Completion:** This graph represents the States based on the number of licenses issued within SLA and the number of licenses issued, in bar chart representation with the % in descending order.

![](<../../../../.gitbook/assets/image (368).png>)

&#x20;

**Bottom 3 Performing States By Completion:** This graph represents the states based on the number of licenses issued within SLA and the number of licenses issued, in bar chart representation with the % in ascending order.

![](<../../../../.gitbook/assets/image (392).png>)

&#x20;

**Trade Licenses by Status:** This circular chart represents the number of trade licenses according to status.

![](<../../../../.gitbook/assets/image (365).png>)

**Status report:** This table shows the status-wise breakup of trade licenses by states for the selected year.

![](<../../../../.gitbook/assets/image (391).png>)

If we select a state, the drill down chart for ULBs in that state appears.

![](<../../../../.gitbook/assets/image (418).png>)

**Index Properties of National Trade License:** The index that contains the data for National-Trade License is- _tl-national-dashboard_

The mapping for this index is given below:

```
PUT tl-national-dashboard/_mapping/nss
{
  "properties": {
    "transactions": {
      "type": "long"
    },
    "todaysApplications": {
      "type": "long"
    },
    "tlTax": {
      "type": "long"
    },
    "adhocPenalty": {
      "type": "long"
    },
    "adhocRebate": {
      "type": "long"
    },
    "todaysLicenseIssuedWithinSLA": {
      "type": "long"
    },
    "tradeType": {
      "type": "text",
      "fields": {
        "keyword": {
          "type": "keyword",
          "ignore_above": 256
        }
      }
    },
    "status": {
      "type": "text",
      "fields": {
        "keyword": {
          "type": "keyword",
          "ignore_above": 256
        }
      }
    },
    "todaysCollectionForTradeType": {
      "type": "long"
    },
    "todaysTradeLicensesForStatus": {
      "type": "long"
    },
    "applicationsMovedTodayForStatus": {
      "type": "long"
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
    "ulb": {
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
    "state": {
      "type": "text",
      "fields": {
        "keyword": {
          "type": "keyword",
          "ignore_above": 256
        }
      }
    },
    "date": {
      "type": "date",
      "format": "dd-MM-yyyy HH:mm:ss||dd-MM-yyyy||epoch_millis||dd-MM-yyyy'T'HH:mm:ss.SSSZ"
    }
  }
}
```

The table below describes the properties mentioned above:

| **Attributes**        | **Definition**                                              | **Breakup**                                                    |
| --------------------- | ----------------------------------------------------------- | -------------------------------------------------------------- |
| ulb                   | The district or region for which the data is ingested       | Nil                                                            |
| state                 | The ULB name for which the data is ingested                 | Nil                                                            |
| ward                  | The ward for which the data is ingested                     | Nil                                                            |
| transactions          | Number of transactions related to TL module on a given date | Nil                                                            |
| todaysApplications    | Number of applications related to TL module on a given date | Breakup by channel type and connection type has to be provided |
| todaysCollection      | Total collection related to TL module on a given date       | Breakup by trade type                                          |
| todaysTradeLicenses   | # of tradelicenses issued today                             | Breakup by status                                              |
| applicatonsMovedToday | # of Applications moved today                               | Breakup by status                                              |
| tlTax                 | Total tax applied on the trade license                      | Nil                                                            |
| adhocPenalty          | Total ad-hoc penalty on the trade license                   | Nil                                                            |
| adhocRebate           | Total ad-hoc rebate received on the trade license           | Nil                                                            |

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_ ](https://egov.org.in/)_is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
