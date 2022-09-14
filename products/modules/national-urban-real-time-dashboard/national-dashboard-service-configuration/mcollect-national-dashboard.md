---
description: Technical Doc
---

# mCollect National Dashboard

## Overview

NDSS has two sides to it. One is the process in which the data is pooled to the ElasticSearch and the other is the way it is fetched, aggregated, computed, transformed and sent across.

As this revolves around a variety of data sets, there is a need for making this configurable. This ensures that the process can be configured easily in case a new scenario is introduced.&#x20;

This document walks us through the steps on how to define the configurations for DSS analytics for mCollect module.

## **Technical Details**

**Analytics:** Microservice responsible for building, fetching, aggregating and computing the data on ElasticSearch into consumable data Response. This is used for visualizations and graphical representations.&#x20;

**Analytics Configurations:** Analytics contains multiple configurations. Add the changes related to National-Dashboard in the dashboard-analytics configuration here.\
Here is the location : [<img src="https://github.com/fluidicon.png" alt="" data-size="line">configs/egov-dss-dashboards/dashboard-analytics at qa · egovernments/configs](https://github.com/egovernments/configs/tree/qa/egov-dss-dashboards/dashboard-analytics)

Below is a list of configurations that need to be changed to run the National Dashboard successfully.

1. Chart API Configuration
2. Master Dashboard Configuration
3. Role Dashboard Mappings Configuration

**Chart API Configuration:** Each Visualization has its own properties. The visualization is assembled from different data sources (Sometimes it is a combination of multiple data sources).&#x20;

The Chart API configuration document is used to configure each visualisation and its properties.&#x20;

In this, Visualisation Code, which happens to be the key, will be having its properties configured as a part of the configuration and are easily changeable.

Sample ChartApiConfiguration.json data for mCollect

```
"mCollectTodaysCollectionv2": {
      "chartName": "DSS_TODAYS_COLLECTION",
      "queries": [
        {
          "module": "COMMON",
          "dateRefField": "",
          "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
          "indexName": "mcollect-national-dashboard",
          "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must\":[{\"range\":{\"date\":{\"gt\":\"now-1d\/d\",\"lte\":\"now\"}}}]}},\"aggs\":{\"Todays Collection\":{\"sum\":{\"field\":\"todaysCollectionForPaymentMode\"}}}}}}"
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
        "chartResponseMap" : "mCollectTodaysCollectionv2",
        "action" : "differenceOfNumbers",
        "upwardIndicator" : "positive",
        "downwardIndicator" : "negative",
        "textMessage" : "$indicator$value% than last $insightInterval",
        "colorCode" : "#228B22",
        "insightInterval" : "month"
      },
      "_comment": " "
    },
  
    "mCollectTotalCollectionv2": {
      "chartName": "DSS_TOTAL_COLLECTION",
      "queries": [
        {
          "module": "COMMON",
          "dateRefField": "date",
          "requestQueryMap": "{\"state\" : \"state.keyword\",\"tenantId\" : \"ulb.keyword\"}",
          "indexName": "mcollect-national-dashboard",
          "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"Total Collection\":{\"sum\":{\"field\":\"todaysCollectionForPaymentMode\"}}}}}}"
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
        "chartResponseMap" : "mCollectTotalCollectionv2",
        "action" : "differenceOfNumbers",
        "upwardIndicator" : "positive",
        "downwardIndicator" : "negative",
        "textMessage" : "$indicator$value% than last $insightInterval",
        "colorCode" : "#228B22",
        "insightInterval" : "year"
      },
      "_comment": " "
    },
  
    "mCollectTotalChallansv2": {
      "chartName": "DSS_TOTAL_CHALLANS",
      "queries": [
        {
          "module": "COMMON",
          "dateRefField": "date",
          "requestQueryMap": "{\"state\" : \"state.keyword\",\"tenantId\" : \"ulb.keyword\"}",
          "indexName": "mcollect-national-dashboard",
          "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"Total Challans\":{\"sum\":{\"field\":\"numberOfChallansForChallanStatus\"}}}}}}"
        }
      ],
      "chartType": "metric",
      "valueType": "number",
      "drillChart": "none",
      "documentType": "_doc",
      "action": "",
      "aggregationPaths": [
        "Total Challans"
      ],
      "insight": {
        "chartResponseMap" : "mCollectTotalChallansv2",
        "action" : "differenceOfNumbers",
        "upwardIndicator" : "positive",
        "downwardIndicator" : "negative",
        "textMessage" : "$indicator$value% than last $insightInterval",
        "colorCode" : "#228B22",
        "insightInterval" : "year"
      },
      "_comment": " "
    },
  
    "mCollectTotalReceiptsv2": {
      "chartName": "DSS_TOTAL_RECEIPTS",
      "queries": [
        {
          "module": "COMMON",
          "dateRefField": "date",
          "requestQueryMap": "{\"state\" : \"state.keyword\",\"tenantId\" : \"ulb.keyword\"}",
          "indexName": "mcollect-national-dashboard",
          "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"Total Receipts\":{\"sum\":{\"field\":\"numberOfReceiptsForPaymentMode\"}}}}}}"
        }
      ],
      "chartType": "metric",
      "valueType": "number",
      "drillChart": "none",
      "documentType": "_doc",
      "action": "",
      "aggregationPaths": [
        "Total Receipts"
      ],
      "insight": {
        "chartResponseMap" : "mCollectTotalReceiptsv2",
        "action" : "differenceOfNumbers",
        "upwardIndicator" : "positive",
        "downwardIndicator" : "negative",
        "textMessage" : "$indicator$value% than last $insightInterval",
        "colorCode" : "#228B22",
        "insightInterval" : "year"
      },
      "_comment": " "
    },

    "mCollectTotalCategoriesv2": {
      "chartName": "DSS_TOTAL_CATEGORIES",
      "queries": [
        {
          "module": "COMMON",
          "dateRefField": "date",
          "requestQueryMap": "{\"state\" : \"state.keyword\",\"tenantId\" : \"ulb.keyword\"}",
          "indexName": "mcollect-national-dashboard",
          "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{}},\"aggs\":{\"Total Categories\":{\"cardinality\":{\"field\":\"category.keyword\"}}}}}}"
        }
      ],
      "chartType": "metric",
      "valueType": "number",
      "drillChart": "none",
      "documentType": "_doc",
      "action": "",
      "aggregationPaths": [
        "Total Categories"
      ],
      "insight": {
        "chartResponseMap" : "mCollectTotalCategoriesv2",
        "action" : "differenceOfNumbers",
        "upwardIndicator" : "positive",
        "downwardIndicator" : "negative",
        "textMessage" : "$indicator$value% than last $insightInterval",
        "colorCode" : "#228B22",
        "insightInterval" : "month"
      },
      "_comment": " "
    },
  
    "mcCollectionByPaymentModev2": {
      "chartName": "DSS_MC_COLLECTION_BY_PAYMENT_MODE",
      "queries": [
        {
          "module": "COMMON",
          "dateRefField": "date",
          "requestQueryMap": "{\"state\" : \"state.keyword\",\"tenantId\" : \"ulb.keyword\"}",
          "indexName": "mcollect-national-dashboard",
          "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[]}},\"aggs\":{\"Payment Mode\":{\"terms\":{\"field\":\"paymentMode.keyword\"},\"aggs\":{\"Total collection\":{\"sum\":{\"field\":\"todaysCollectionForPaymentMode\"}}}}}}}}"
        }
      ],
      "chartType": "pie",
      "valueType": "amount",
      "drillChart": "none",
      "documentType": "_doc",
      "action": "",
      "aggregationPaths": [
        "Payment Mode"
      ],
      "insight": {
        
      },
      "_comment": " "
    },
  
    "mcRceiptsByPaymentModev2": {
      "chartName": "DSS_MC_RECEIPTS_BY_PAYMENT_MODE",
      "queries": [
        {
          "module": "COMMON",
          "dateRefField": "date",
          "requestQueryMap": "{\"state\" : \"state.keyword\",\"tenantId\" : \"ulb.keyword\"}",
          "indexName": "mcollect-national-dashboard",
          "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[]}},\"aggs\":{\"Payment Mode\":{\"terms\":{\"field\":\"paymentMode.keyword\"},\"aggs\":{\"Total Receipts\":{\"sum\":{\"field\":\"numberOfReceiptsForPaymentMode\"}}}}}}}}"
        }
      ],
      "chartType": "pie",
      "valueType": "number",
      "drillChart": "none",
      "documentType": "_doc",
      "action": "",
      "aggregationPaths": [
        "Payment Mode"
      ],
      "insight": {
        
      },
      "_comment": " "
    },
    
    "mcMonthlyCumulativeCollectionv2": {
      "chartName": "DSS_MC_MONTHLY_CUMULATIVE",
      "queries": [
        {
          "module": "COMMON",
          "dateRefField": "date",
          "requestQueryMap": "{\"state\" : \"state.keyword\",\"tenantId\" : \"ulb.keyword\"}",
          "indexName": "mcollect-national-dashboard",
          "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[]}},\"aggs\":{\"Collections\":{\"date_histogram\":{\"field\":\"date\",\"interval\":\"intervalvalue\"},\"aggs\":{\"Sum\":{\"sum\":{\"field\":\"todaysCollectionForPaymentMode\"}}}}}}}}"
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
  
    "mcCollectionByStatusv2": {
      "chartName": "DSS_MC_COLLECTION_BY_STATUS",
      "queries": [
        {
          "module": "COMMON",
          "dateRefField": "date",
          "requestQueryMap": "{\"state\" : \"state.keyword\",\"tenantId\" : \"ulb.keyword\"}",
          "indexName": "mcollect-national-dashboard",
          "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[]}},\"aggs\":{\"Collection Status\":{\"terms\":{\"field\":\"status.keyword\"},\"aggs\":{\"Total collection\":{\"sum\":{\"field\":\"todaysCollectionForStatus\"}}}}}}}}"
        }
      ],
      "chartType": "pie",
      "valueType": "amount",
      "drillChart": "none",
      "documentType": "_doc",
      "action": "",
      "aggregationPaths": [
        "Collection Status"
      ],
      "insight": {
        
      },
      "_comment": " "
    },
  
    "mcChallanByStatusv2": {
      "chartName": "DSS_MC_CHALLAN_BY_STATUS",
      "queries": [
        {
          "module": "COMMON",
          "dateRefField": "date",
          "requestQueryMap": "{\"state\" : \"state.keyword\",\"tenantId\" : \"ulb.keyword\"}",
          "indexName": "mcollect-national-dashboard",
          "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[]}},\"aggs\":{\"Challan Status\":{\"terms\":{\"field\":\"challanStatus.keyword\"},\"aggs\":{\"Total collection\":{\"sum\":{\"field\":\"numberOfChallansForChallanStatus\"}}}}}}}}"
        }
      ],
      "chartType": "pie",
      "valueType": "number",
      "drillChart": "none",
      "documentType": "_doc",
      "action": "",
      "aggregationPaths": [
        "Challan Status"
      ],
      "insight": {
        
      },
      "_comment": " "
    },
  
    "mcReceiptsByStatusv2": {
      "chartName": "DSS_MC_RECEIPTS_BY_STATUS",
      "queries": [
        {
          "module": "COMMON",
          "dateRefField": "date",
          "requestQueryMap": "{\"state\" : \"state.keyword\",\"tenantId\" : \"ulb.keyword\"}",
          "indexName": "mcollect-national-dashboard",
          "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[]}},\"aggs\":{\"Receipts Status\":{\"terms\":{\"field\":\"status.keyword\"},\"aggs\":{\"Total collection\":{\"sum\":{\"field\":\"numberOfReceiptsForStatus\"}}}}}}}}"
        }
      ],
      "chartType": "pie",
      "valueType": "number",
      "drillChart": "none",
      "documentType": "_doc",
      "action": "",
      "aggregationPaths": [
        "Receipts Status"
      ],
      "insight": {
        
      },
      "_comment": " "
    },
  
    "mcCollectionCategoryWisev2": {
      "chartName": "DSS_MC_COLLECTION_CATEGORY_WISE",
      "queries": [
        {
          "module": "COMMON",
          "dateRefField": "date",
          "requestQueryMap": "{\"state\" : \"state.keyword\",\"tenantId\" : \"ulb.keyword\"}",
          "indexName": "mcollect-national-dashboard",
          "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[]}},\"aggs\":{\"Business Service\":{\"terms\":{\"field\":\"category.keyword\",\"order\":{\"total\":\"desc\"}},\"aggs\":{\"total\":{\"sum\":{\"field\":\"todaysCollectionForCategory\"}}}}}}}}"
        }
      ],
      "chartType": "pie",
      "valueType": "amount",
      "action": "",
      "documentType": "_doc",
      "drillChart": "none",
      "aggregationPaths": [
        "Business Service"
      ],
      "insight": {},
      "_comment": " "
    },

    "mcReportByStatev3": {
      "chartName": "DSS_MC_REPORT_BY_STATE",
      "queries": [
        {
          "module": "COMMON",
          "requestQueryMap": "{\"stateId\" : \"state.keyword\"}",
          "dateRefField": "date",
          "indexName": "mcollect-national-dashboard",
          "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[]}},\"aggs\":{\"State name\":{\"terms\":{\"field\":\"state.keyword\"},  \"aggs\":{\"Total_Receipts\":{\"sum\":{\"field\":\"numberOfReceiptsForPaymentMode\"}},\"Total_Collection\":{\"sum\":{\"field\":\"todaysCollectionForPaymentMode\"}},\"Total_Challans\":{\"sum\":{\"field\":\"numberOfChallansForChallanStatus\"}} }}}}}}"
        }
      ],
      "isMdmsEnabled": false,
      "filterKeys": [
        {"key": "stateId", "column": "States"}
      ],
      "chartType": "xtable",
      "drillChart": "mcReportByTenantv3",
      "plotLabel": "States",
      "aggregationPaths": [
        "Total_Collection",
        "Total_Challans",
        "Total_Receipts"
      ],
      "pathDataTypeMapping": [
        {
          "Total_Collection": "amount"
        },
        {
          "Total_Challans": "number"
        },
        {
          "Total_Receipts": "number"
        }
      ],
    
      "insight": {
      },
      "_comment": ""
    },
  
    "mcReportByDDRv3": {
      "chartName": "DSS_MC_REPORT_BY_DDR",
      "queries": [
        {
          "module": "COMMON",
          "requestQueryMap": "{\"stateId\" : \"state.keyword\", \"region\" : \"region.keyword\"}",
          "dateRefField": "date",
          "indexName": "mcollect-national-dashboard",
          "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[]}},\"aggs\":{\"Region\":{\"terms\":{\"field\":\"region.keyword\"},  \"aggs\":{\"Total_Receipts\":{\"sum\":{\"field\":\"numberOfReceiptsForPaymentMode\"}},\"Total_Collection\":{\"sum\":{\"field\":\"todaysCollectionForPaymentMode\"}},\"Total_Challans\":{\"sum\":{\"field\":\"numberOfChallansForChallanStatus\"}} }}}}}}"
        }
      ],
      "isMdmsEnabled": false,
      "filterKeys": [
        {"key": "region", "column": "DDR"}
      ],
      "chartType": "xtable",
      "drillChart": "mcReportByTenantv3",
      "plotLabel": "DDR",
      "aggregationPaths": [
        "Total_Collection",
        "Total_Challans",
        "Total_Receipts"
      ],
      "pathDataTypeMapping": [
        {
          "Total_Collection": "amount"
        },
        {
          "Total_Challans": "number"
        },
        {
          "Total_Receipts": "number"
        }
      ],
    
      "insight": {
      },
      "_comment": ""
    },
  
    "mcReportByTenantv3": {
      "chartName": "DSS_MC_REPORT_BY_TENANT",
      "queries": [
        {
          "module": "COMMON",
          "requestQueryMap": "{\"stateId\" : \"state.keyword\", \"region\" : \"region.keyword\", \"tenantId\" : \"ulb.keyword\"}",
          "dateRefField": "date",
          "indexName": "mcollect-national-dashboard",
          "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[]}},\"aggs\":{\"Tenant\":{\"terms\":{\"field\":\"ulb.keyword\"},  \"aggs\":{\"Total_Receipts\":{\"sum\":{\"field\":\"numberOfReceiptsForPaymentMode\"}},\"Total_Collection\":{\"sum\":{\"field\":\"todaysCollectionForPaymentMode\"}},\"Total_Challans\":{\"sum\":{\"field\":\"numberOfChallansForChallanStatus\"}} }}}}}}"
        }
      ],
      "isMdmsEnabled": false,
      "filterKeys": [
        {"key": "tenantId", "column": "ULB"}
      ],
      "chartType": "xtable",
      "drillChart": "mcReportByWardv3",
      "plotLabel": "ULB",
      "aggregationPaths": [
        "Total_Collection",
        "Total_Challans",
        "Total_Receipts"
      ],
      "pathDataTypeMapping": [
        {
          "Total_Collection": "amount"
        },
        {
          "Total_Challans": "number"
        },
        {
          "Total_Receipts": "number"
        }
      ],
    
      "insight": {
      },
      "_comment": ""
    },
  
    "mcReportByWardv3": {
      "chartName": "DSS_MC_REPORT_BY_WARD",
      "queries": [
        {
          "module": "COMMON",
          "requestQueryMap": "{\"stateId\" : \"state.keyword\", \"region\" : \"region.keyword\", \"tenantId\" : \"ulb.keyword\", \"ward\" : \"ward.keyword\"}",
          "dateRefField": "date",
          "indexName": "mcollect-national-dashboard",
          "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[]}},\"aggs\":{\"Ward\":{\"terms\":{\"field\":\"ward.keyword\"},  \"aggs\":{\"Total_Receipts\":{\"sum\":{\"field\":\"numberOfReceiptsForPaymentMode\"}},\"Total_Collection\":{\"sum\":{\"field\":\"todaysCollectionForPaymentMode\"}},\"Total_Challans\":{\"sum\":{\"field\":\"numberOfChallansForChallanStatus\"}} }}}}}}"
        }
      ],
      "isMdmsEnabled": false,
      "filterKeys": [
        {"key": "ward", "column": "Ward"}
      ],
      "chartType": "xtable",
      "drillChart": "none",
      "plotLabel": "Ward",
      "aggregationPaths": [
        "Total_Collection",
        "Total_Challans",
        "Total_Receipts"
      ],
      "pathDataTypeMapping": [
        {
          "Total_Collection": "amount"
        },
        {
          "Total_Challans": "number"
        },
        {
          "Total_Receipts": "number"
        }
      ],
    
      "insight": {
      },
      "_comment": ""
    },

    "mcMonthlyCollectionv2": {
      "chartName": "DSS_MC_MONTHLY_REPORT",
      "queries": [
        {
          "module": "COMMON",
          "dateRefField": "date",
          "requestQueryMap": "{\"state\" : \"state.keyword\",\"tenantId\" : \"ulb.keyword\"}",
          "indexName": "mcollect-national-dashboard",
          "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[]}},\"aggs\":{\"Collections\":{\"date_histogram\":{\"field\":\"date\",\"interval\":\"month\"},\"aggs\":{\"Sum\":{\"sum\":{\"field\":\"todaysCollectionForPaymentMode\"}}}},\"Receipts\":{\"date_histogram\":{\"field\":\"date\",\"interval\":\"month\"},\"aggs\":{\"Total Receipts\":{\"sum\":{\"field\":\"numberOfReceiptsForPaymentMode\"}}}} }}}}"
        }
      ],
  
      "valueType":"amount",
      "chartType": "line",
      "action": "",
      "drillChart": "none",
      "documentType": "_doc",
      "aggregationPaths": [
        "Collections",
        "Receipts"
      ],
      "pathDataTypeMapping": [
        {
          "Collections": "amount"
        },
        {
          "Receipts": "number"
        }
      ],
      "isCumulative": false,
      "interval": "month",
      "insight": {
      },
      "_comment": " "
    },

    "mcReportByCategoryv3": {
      "chartName": "DSS_MC_STATUS_BY_CATEGORY",
      "queries": [
        {
          "module": "COMMON",
          "requestQueryMap": "{\"departmentId\" : \"category.keyword\" , \"state\" : \"state.keyword\",\"tenantId\" : \"ulb.keyword\" , \"ward\" : \"ward.keyword\" }",
          "dateRefField": "date",
          "indexName": "mcollect-national-dashboard",
          "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[]}},\"aggs\":{\"Department\":{\"terms\":{\"field\":\"category.keyword\"},  \"aggs\":{\"Total_Receipts\":{\"sum\":{\"field\":\"numberOfReceiptsForCategory\"}},\"Total_Collection\":{\"sum\":{\"field\":\"todaysCollectionForCategory\"}}, \"Total_Challans\":{\"sum\":{\"field\":\"numberOfChallansForCategory\"}}}}}}}}"
        }
  
      ],
      "filterKeys": [
        {"key": "departmentId", "column": "Department"}
      ],
      "chartType": "xtable",
      "drillChart": "none",
  
      "documentType": "_doc",
      "action": "",
      "plotLabel": "Department",
      "aggregationPaths": [
        "Total_Collection",
        "Total_Challans",
        "Total_Receipts"
      ],
      "pathDataTypeMapping": [
        {
          "Total_Collection": "amount"
        },
        {
          "Total_Challans": "number"
        },
        {
          "Total_Receipts": "number"
        }
      ],
      "insight": {
      },
      "_comment": ""
    }
```

[Click here to check the complete configuration](https://github.com/egovernments/configs/blob/qa/egov-dss-dashboards/dashboard-analytics/ChartApiConfig.json)

**Master Dashboard Configuration -** Master Dashboard configuration is the main configuration which defines the dashboards to be painted on the screen. This includes the visualizations, the  groups, the charts which comes within them and even the dimensions in terms of height and width.

```
{
      "name": "DSS_M_COLLECT_DASHBOARD",
      "id": "national-mcollect",
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
                  "id": "mCollectTodaysCollectionv2",
                  "name": "DSS_TODAYS_COLLECTION",
                  "code": "",
                  "chartType": "metric",
                  "filter": {
                    "title": "TODAY"
                  },
                  "headers": []
                },
                {
                  "id": "mCollectTotalCollectionv2",
                  "name": "DSS_TOTAL_COLLECTION",
                  "code": "",
                  "chartType": "metric",
                  "filter": "",
                  "headers": []
                },
                {
                  "id": "mCollectTotalChallansv2",
                  "name": "DSS_TOTAL_CHALLANS",
                  "code": "",
                  "chartType": "metric",
                  "filter": "",
                  "headers": []
                },
                {
                  "id": "mCollectTotalReceiptsv2",
                  "name": "DSS_TOTAL_RECEIPTS",
                  "code": "",
                  "chartType": "metric",
                  "filter": "",
                  "headers": []
                },
                {
                  "id": "mCollectTotalCategoriesv2",
                  "name": "DSS_TOTAL_CATEGORIES",
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
                  "id": "mcMonthlyCumulativeCollectionv2",
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
              "id": 234,
              "name": "DSS_MC_RECEIPTS_BY_PAYMENTMODE",
              "dimensions": {
                "height": 250,
                "width": 4
              },
              "vizType": "chart",
              "noUnit": false,
              "isCollapsible": false,
              "charts": [
                {
                  "id": "mcRceiptsByPaymentModev2",
                  "name": "DSS_MC_RECEIPTS_BY_PAYMENT_MODE",
                  "code": "",
                  "chartType": "donut",
                  "filter": "",
                  "headers": []
                }
              ]
            },
            {
              "id": 323,
              "name": "DSS_MC_COLLECTION_BY_PAYMENT_TYPE",
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
                  "id": "mcCollectionByPaymentModev2",
                  "name": "DSS_MC_COLLECTION_BY_PAYMENT_MODE",
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
              "id": 235,
              "name": "DSS_MC_CHALLAN_COUNT_BY_STATUS",
              "dimensions": {
                "height": 250,
                "width": 4
              },
              "vizType": "chart",
              "noUnit": false,
              "isCollapsible": false,
              "charts": [
                {
                  "id": "mcChallanByStatusv2",
                  "name": "DSS_MC_CHALLAN_BY_STATUS",
                  "code": "",
                  "chartType": "donut",
                  "filter": "",
                  "headers": []
                }
              ]
            },
            {
              "id": 233,
              "name": "DSS_MC_RECEIPTS_BY_STATUS",
              "dimensions": {
                "height": 250,
                "width": 4
              },
              "vizType": "chart",
              "noUnit": false,
              "isCollapsible": false,
              "charts": [
                {
                  "id": "mcReceiptsByStatusv2",
                  "name": "DSS_MC_RECEIPTS_BY_STATUS",
                  "code": "",
                  "chartType": "donut",
                  "filter": "",
                  "headers": []
                }
              ]
            },
            {
              "id": 232,
              "name": "DSS_MC_COLLECTION_BY_STATUS",
              "dimensions": {
                "height": 250,
                "width": 4
              },
              "vizType": "chart",
              "noUnit": false,
              "isCollapsible": false,
              "charts": [
                {
                  "id": "mcCollectionByStatusv2",
                  "name": "DSS_MC_COLLECTION_BY_STATUS",
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
              "id": 123,
              "name": "DSS_MC_COLLECTION_CATEGORY_WISE",
              "dimensions": {
                "height": 250,
                "width": 4
              },
              "vizType": "chart",
              "noUnit": false,
              "isCollapsible": false,
              "charts": [
                {
                  "id": "mcCollectionCategoryWisev2",
                  "name": "DSS_MC_COLLECTION_CATEGORY_WISE",
                  "code": "",
                  "chartType": "horizontalBar",
                  "filter": "",
                  "headers": []
                }
              ]
            },
            {
              "id": 124,
              "name": "DSS_MC_MONTHLY_REPORT",
              "dimensions": {
                "height": 250,
                "width": 4
              },
              "vizType": "chart",
              "noUnit": false,
              "isCollapsible": false,
              "charts": [
                {
                  "id": "mcMonthlyCollectionv2",
                  "name": "DSS_MC_MONTHLY_REPORT",
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
          "row": 5,
          "name": "DSS_REVENUE",
          "vizArray": [
            
            {
              "id": 236,
              "name": "DSS_MC_REPORT_BY_TENANT",
              "dimensions": {
                "height": 250,
                "width": 4
              },
              "vizType": "chart",
              "noUnit": false,
              "isCollapsible": false,
              "charts": [
                {
                  "id": "mcReportByStatev3",
                  "name": "DSS_MC_REPORT_BY_TENANT",
                  "code": "",
                  "chartType": "table",
                  "filter": "",
                  "headers": [],
                  "tabName": "Boundary"
                },
                {
                  "id": "mcReportByCategoryv3",
                  "name": "DSS_MC_STATUS_BY_CATEGORY",
                  "code": "",
                  "chartType": "table",
                  "filter": "",
                  "headers": [],
                  "tabName": "Category"
                }
              ]
            }
          ]
        }
      ]
    }
```

[Click here for the complete configuration](https://github.com/egovernments/configs/blob/qa/egov-dss-dashboards/dashboard-analytics/MasterDashboardConfig.json)

**Role Dashboard Mappings Configuration -** Master Dashboard Configuration which was explained earlier hold the list of available dashboards. Given the instance where Role Action Mapping is not maintained in the application service, this configuration acts as Role - Dashboard Mapping configuration.&#x20;

Each role is mapped against the dashboards that they are authorized to see. This was used earlier when the Role Action Mapping of eGov was not integrated. Later, when the role action mapping started controlling the dashboards to be seen on the client side, this configuration was used to enable the dashboards for viewing.

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
          "name": "National mCollect",
          "id": "national-mcollect"
        }
      ]
    }

  ]
}
```

[Click here for the entire configuration](https://github.com/egovernments/configs/blob/qa/egov-dss-dashboards/dashboard-analytics/RoleDashboardMappingsConf.json)

**MDMS configuration to be added -** _common-masters/uiCommonConstants.json_

```
"national-mcollect": {
                  "routePath": "/dashboard/national-mcollect",
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

[Click here for complete configurations](https://github.com/egovernments/egov-mdms-data/blob/QA/data/pb/ACCESSCONTROL-ROLEACTIONS/roleactions.json)

Action test.json:

```
{
      "id": {{PlaceHolder1}},
      "name": "NSS Dashboard Config National mCollect",
      "url": "/dashboard-analytics/dashboard/getDashboardConfig/national-mcollect",
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
      "name": "National Dashboard mCollect",
      "url": "url",
      "displayName": "National mCollect",
      "orderNumber": 4,
      "parentModule": "ndss-dashboard",
      "enabled": true,
      "serviceCode": "NDSS",
      "code": "null",
      "path": "NatDashboard.Mcollect",
      "navigationURL": "/digit-ui/employee/dss/dashboard/national-mcollect",
      "leftIcon": "places:business-center",
      "rightIcon": ""
    }
```

[Click here for complete configuration](https://github.com/egovernments/egov-mdms-data/blob/QA/data/pb/ACCESSCONTROL-ACTIONS-TEST/actions-test.json)

mCollect - National DSS contains multiple graphs that represent mCollect data. Each graph has its own configuration that describe the chart and its type.

National DSS contains the following charts in mCollect:

* Overview
* Total Cumulative Collection
* Receipts by Payment Mode
* Collection by Payment Mode
* Challan Count by Status
* Receipts Count by Status
* Collection by Status
* Top Categories Collections
* Monthly Collections

**Overview:** Overview graph contains multiple data information as below in the selected time period.

* **Today’s Collection :** This represents the today’s collection amount
* &#x20;**Total Collection :** This represents the total collection amount
* **Total Challans :** This represents the total number of challans
* **Total Receipts :** This represents the total number of receipts
* **Number of Categories :** This represents the total number of categories

![](<../../../../.gitbook/assets/image (386).png>)

**Total Cumulative Collection -** This graph illustrates the mCollect collection amount information in the monthly base as a cumulative line graph. The graph changes as per the denomination amount filter selection.

**line** - this graph/chart is data representation on date histograms or date groupings.

![](<../../../../.gitbook/assets/image (379).png>)

**Receipts by Payment Mode -** The graph shows the number of receipts based on the payment mode.

![](<../../../../.gitbook/assets/image (395).png>)

**Collection by Payment Mode -** This graph shows the collection amount based on the payment mode.

![](<../../../../.gitbook/assets/image (398).png>)

**Challan Count by Status -** This graph shows the number of challans based on the status.

![](<../../../../.gitbook/assets/image (394).png>)

**Receipts Count by Status -**This graph shows the number of receipts based on the status.

![](<../../../../.gitbook/assets/image (381).png>)

**Collection by Status -** This graph shows the collection amount based on the status.

![](<../../../../.gitbook/assets/image (352).png>)

**Top Categories Collection -** This graph shows the collection amount based on the categories, in descending order.

![](<../../../../.gitbook/assets/image (375).png>)

**Monthly Collection -** This graph shows the total collection and number of receipts for each month.

![](<../../../../.gitbook/assets/image (360).png>)

**Collection Report**

**Boundary**

This tabular chart representation graph shows multiple mCollect information like Total Collection, Number of Receipts and Number of Challans. The table shows the data at the State level and provides a drill down chart for each State to ULB and from ULB to the Ward level data.

_**xtable**_ type allows to add multiple computed fields with the aggregated fields dynamically added.

To add multiple computed columns,  define **computedFields** \[]  where actionName (IComputedField\<T> interface), fields \[] names as in exist in query key, and newField as the name for the computation.

![](<../../../../.gitbook/assets/image (417).png>)

Clicking on any State name provides drill down charts that represent the specific ULB data.

![](<../../../../.gitbook/assets/image (404).png>)

Clicking on the ULB offers a drill-down view of the data for the Wards for the specified ULB. Clicking on any ward displays the ward level data.

![](<../../../../.gitbook/assets/image (410).png>)

**Category -** shows the category wise data for Total Collections, Number of Challans and Number of Receipts.

![](<../../../../.gitbook/assets/image (403).png>)

#### **Index Properties of National mCollect** <a href="#index-properties-of-national-mcollect" id="index-properties-of-national-mcollect"></a>

The index that contains data for National-mCollect is- _mcollect-national-dashboard_

The mapping for this index is given below:&#x20;

```
PUT mcollect-national-dashboard/_mapping/nss
{
  "properties": {
    "todaysCollectionForCategory": {
      "type": "long"
    },
    "todaysCollectionForPaymentMode": {
      "type": "long"
    },
    "todaysCollectionForStatus": {
      "type": "long"
    },
    "paymentMode": {
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
    "category": {
      "type": "text",
      "fields": {
        "keyword": {
          "type": "keyword",
          "ignore_above": 256
        }
      }
    },
    "challanStatus": {
      "type": "text",
      "fields": {
        "keyword": {
          "type": "keyword",
          "ignore_above": 256
        }
      }
    },
    "numberOfReceiptsForStatus": {
      "type": "long"
    },
    "numberOfReceiptsForPaymentMode": {
      "type": "long"
    },
    "numberOfReceiptsForCategory": {
      "type": "long"
    },
    "numberOfChallansForChallanStatus": {
      "type": "long"
    },
    "numberOfChallansForCategory": {
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

&#x20;The following is the table that describes the properties mentioned above:

| **Attributes**     | **Defintion**                                                   | **Breakup**                                                    |
| ------------------ | --------------------------------------------------------------- | -------------------------------------------------------------- |
| ulb                | The district or region for which the data is ingested.          | Nil                                                            |
| state              | The ULB name for which the data is ingested.                    | Nil                                                            |
| ward               | The ward for which the data is ingested.                        | Nil                                                            |
| numberOfCategories | Number of categories related to mCollect module on a given date | Nil                                                            |
| todaysCollection   | Total collection related to mCollect module on a given date     | Breakup by paymentMode, status and category has to be provided |
| numberOfReceipts   | Number of receipts issued on a given date                       | Breakup by paymentMode, status and category has to be provided |
| numberOfChallans   | Number of challans issued on a given date                       | Breakup by challanStatus and category has to be provided.      |

&#x20;[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_ ](https://egov.org.in/)_is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
