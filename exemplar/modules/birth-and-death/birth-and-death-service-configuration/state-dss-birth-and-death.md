---
description: Technical Doc
---

# State DSS - Birth and Death

## Overview

There are two dimensions to DSS. The first refers to the process where the data is pooled to ElasticSearch and the second relates to the way the data is fetched, aggregated, computed, transformed and sent across.

The DSS processes are easily configurable and this enables users to configure new analytics insights using a wide range of data sets.&#x20;

This document defines the configuration steps for the fetching analytical insights on the DSS for the Birth & Death module.



## Key Concepts

**Analytics:** Micro Service responsible for building, fetching, aggregating and computing the data on ElasticSearch to a consumable data response. This is used for visualizations and graphical representations. &#x20;

**Analytics Configurations:** Analytics contains multiple configurations. Add the changes related to FSM in the dashboard-analytics configuration file.\
File location : [<img src="https://github.com/fluidicon.png" alt="" data-size="line">configs/egov-dss-dashboards/dashboard-analytics at qa · egovernments/configs](https://github.com/egovernments/configs/tree/qa/egov-dss-dashboards/dashboard-analytics)\
List of configurations that need to be changed to run FSM successfully.

1. Chart API Configuration
2. Master Dashboard Configuration
3. Role Dashboard Mappings Configuration

**Chart API Configuration:** Each visualization has its own properties. The visualization is derived from different data sources or a combination of data sources.&#x20;

The Chart API Configuration Document is used to configure each visualization and its properties. The Visualization Code is the key and its properties are easily configurable.

Sample ChartApiConfiguration.json data for Birth and Death.

```
"dssBirthTotalApplication": {
    "chartName": "DSS_BIRTH_TOTAL_APPLICATION",
    "queries": [
    {
      "module": "BIRTH",
      "indexName": "birth-cert-v1",
      "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.tenantId.keyword\":\"pb.testing\"}},{\"terms\":{\"Data.applicationStatus.keyword\":[\"ACTIVE\"]}}]}},\"aggs\":{\"Birth total Application\":{\"value_count\":{\"field\":\"Data.birthCertificateNo.keyword\"}}}}}}",
      "requestQueryMap": "{\"wardId\" : \"Data.ward.keyword\", \"district\" : \"Data.district.keyword\", \"tenantId\" : \"Data.tenantId.keyword\"}", 
      "dateRefField": "Data.dateofissue"
    }
   ],
    "chartType": "metric", 
    "valueType": "number",
    "action": "",
    "documentType": "_doc",
    "drillChart": "none",
    "aggregationPaths": [
      "Birth total Application"
    ],
 "insight": {
      "chartResponseMap" : "totalApplication",
      "action" : "differenceOfNumbers",
      "upwardIndicator" : "positive",
      "downwardIndicator" : "negative",
      "textMessage" : "$indicator$value% than last $insightInterval",
      "colorCode" : "#228B22",
      "insightInterval" : "month"
    },
    "_comment": " totalApplication is the chartId"
  },
  "dssDeathTotalApplication": {
    "chartName": "DSS_DEATH_TOTAL_APPLICATION",
    "queries": [
    {
     "module": "DEATH",
     "indexName": "death-cert-v1",
     "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.tenantId.keyword\":\"pb.testing\"}},{\"terms\":{\"Data.applicationStatus.keyword\":[\"ACTIVE\"]}}]}},\"aggs\":{\"Death total Application\":{\"value_count\":{\"field\":\"Data.deathCertificateNo.keyword\"}}}}}}",
     "requestQueryMap": "{\"wardId\" : \"Data.ward.keyword\", \"district\" : \"Data.district.keyword\", \"tenantId\" : \"Data.tenantId.keyword\"}", 
     "dateRefField": "Data.dateofissue"
    }
   ],
    "chartType": "metric", 
    "valueType": "number",
    "action": "",
    "documentType": "_doc",
    "drillChart": "none",
    "aggregationPaths": [
      "Death total Application"
    ],
 "insight": {
      "chartResponseMap" : "totalApplication",
      "action" : "differenceOfNumbers",
      "upwardIndicator" : "positive",
      "downwardIndicator" : "negative",
      "textMessage" : "$indicator$value% than last $insightInterval",
      "colorCode" : "#228B22",
      "insightInterval" : "month"
    },
    "_comment": " totalApplication is the chartId"
  },
  "birthNetCollection": {
    "chartName": "DSS_BIRTH_NET_COLLECTION",
    "queries": [
      {
       "module": "BIRTH",
       "dateRefField": "dataObject.paymentDetails.receiptDate",
       "requestQueryMap": "{\"wardId\" : \"domainObject.ward.name.keyword\",\"module\" : \"dataObject.paymentDetails.businessService.keyword\", \"tenantId\" : \"dataObject.tenantId.keyword\"}",
       "indexName": "dss-collection_v2",
       "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"dataObject.tenantId.keyword\":\"pb.testing\"}},{\"terms\":{\"dataObject.paymentDetails.bill.status.keyword\":[\"Cancelled\"]}}],\"must\":[{\"terms\":{\"dataObject.paymentDetails.businessService.keyword\":[\"BIRTH_CERT\"]}}]}},\"aggs\":{\"Birth total Collection\":{\"sum\":{\"field\":\"dataObject.paymentDetails.bill.billDetails.amountPaid\"}}}}}}"
     }
    ],
    "chartType": "metric",
    "valueType": "amount",
    "drillChart": "none",
    "documentType": "_doc",
    "action": "",
    "aggregationPaths": [
      "Birth total Collection"
    ],
  "insight": {
      "chartResponseMap" : "netCollectionv2",
      "action" : "differenceOfNumbers",
      "upwardIndicator" : "positive",
      "downwardIndicator" : "negative",
      "textMessage" : "$indicator$value% than last $insightInterval",
      "colorCode" : "#228B22",
      "insightInterval" : "month"
    },
    "_comment": " "
  },
  "deathNetCollection": {
    "chartName": "DSS_DEATH_NET_COLLECTION",
    "queries": [
     {
       "module": "DEATH",
       "dateRefField": "dataObject.paymentDetails.receiptDate",
       "requestQueryMap": "{\"wardId\" : \"domainObject.ward.name.keyword\",\"module\" : \"dataObject.paymentDetails.businessService.keyword\", \"tenantId\" : \"dataObject.tenantId.keyword\"}",
       "indexName": "dss-collection_v2",
       "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"dataObject.tenantId.keyword\":\"pb.testing\"}},{\"terms\":{\"dataObject.paymentDetails.bill.status.keyword\":[\"Cancelled\"]}}],\"must\":[{\"terms\":{\"dataObject.paymentDetails.businessService.keyword\":[\"DEATH_CERT\"]}}]}},\"aggs\":{\"Death total Collection\":{\"sum\":{\"field\":\"dataObject.paymentDetails.bill.billDetails.amountPaid\"}}}}}}"
     }
    ],
    "chartType": "metric",
    "valueType": "amount",
    "drillChart": "none",
    "documentType": "_doc",
    "action": "",
    "aggregationPaths": [
      "Death total Collection"
    ],
  "insight": {
      "chartResponseMap" : "netCollectionv2",
      "action" : "differenceOfNumbers",
      "upwardIndicator" : "positive",
      "downwardIndicator" : "negative",
      "textMessage" : "$indicator$value% than last $insightInterval",
      "colorCode" : "#228B22",
      "insightInterval" : "month"
    },
    "_comment": " "
  },
   "deathByCategory": {
    "chartName": "DSS_DEATH_BY_CATEGORY",
    "queries": [
      {
        "module": "DEATH",
        "requestQueryMap": "{\"wardId\" : \"Data.ward.keyword\", \"district\" : \"Data.district.keyword\", \"tenantId\" : \"Data.tenantId.keyword\"}",
        "dateRefField": "Data.dateofissue",
        "indexName": "death-cert-v1",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.tenantId.keyword\":\"pb.testing\"}},{\"terms\":{\"Data.applicationStatus.keyword\":[\"ACTIVE\"]}}]}},\"aggs\":{\"category\":{\"terms\":{\"field\":\"Data.gender.keyword\"}}}}}}"
      }
    ],
      "chartType": "pie",
    "valueType": "number",
    "action": "",
    "documentType": "_doc",
    "drillChart": "deathByCategoryDrilldownAge",
    "drillFields": [
      "selectedType",
      ""
    ],    
    "aggregationPaths": [
      "category"
    ],
    "insight": {
    },
    "_comment": "Death By Age Category"
  },
  "deathByCategoryDrilldownAge": {
    "chartName": "DSS_DEATH_BY_CATEGORY_DRILLDOWN_AGE",
    "queries": [
      {
        "module": "DEATH",
        "requestQueryMap": "{\"wardId\":\"Data.ward.keyword\",\"district\":\"Data.district.keyword\",\"tenantId\":\"Data.tenantId.keyword\",\"selectedType\":\"Data.gender.keyword\"}",
        "dateRefField": "Data.dateofissue",
        "indexName": "death-cert-v1",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.tenantId.keyword\":\"pb.testing\"}},{\"terms\":{\"Data.applicationStatus.keyword\":[\"ACTIVE\"]}}]}},\"aggs\":{\"less than 2\":{\"date_range\":{\"field\":\"Data.age\",\"ranges\":[{\"to\":1}]},\"aggs\":{\"Count\":{\"value_count\":{\"field\":\"Data.age\"}}}},\"2-14\":{\"date_range\":{\"field\":\"Data.age\",\"ranges\":[{\"from\":2,\"to\":14}]},\"aggs\":{\"Count\":{\"value_count\":{\"field\":\"Data.age\"}}}},\"15-29\":{\"date_range\":{\"field\":\"Data.age\",\"ranges\":[{\"from\":15,\"to\":29}]},\"aggs\":{\"Count\":{\"value_count\":{\"field\":\"Data.age\"}}}},\"30-44\":{\"date_range\":{\"field\":\"Data.age\",\"ranges\":[{\"from\":30,\"to\":44}]},\"aggs\":{\"Count\":{\"value_count\":{\"field\":\"Data.age\"}}}},\"45-59\":{\"date_range\":{\"field\":\"Data.age\",\"ranges\":[{\"from\":45,\"to\":59}]},\"aggs\":{\"Count\":{\"value_count\":{\"field\":\"Data.age\"}}}},\"60-74\":{\"date_range\":{\"field\":\"Data.age\",\"ranges\":[{\"from\":60,\"to\":74}]},\"aggs\":{\"Count\":{\"value_count\":{\"field\":\"Data.age\"}}}},\"greater than 75\":{\"date_range\":{\"field\":\"Data.age\",\"ranges\":[{\"from\":75}]},\"aggs\":{\"Count\":{\"value_count\":{\"field\":\"Data.age\"}}}}}}}}"
      }
    ],
    "chartType": "pie",
    "valueType": "number",
    "action": "",
    "documentType": "_doc",
    "filterKeys": [
      {"key": "selectedType", "column": "gender"}
    ],
    "drillChart": "none",
    "aggregationPaths": [
      "less than 2",
      "2-14",
      "15-29",
      "30-44",
      "45-59",
      "60-74",
      "greater than 75" 
    ],
    "insight": {
    },
    "_comment": "Death By Age Category"
  },
  "birthDownloadTrend": {
    "chartName": "DSS_BIRTH_DOWNLOAD_TREND",
    "queries": [
      {
       "module": "BIRTH",
       "dateRefField": "Data.dateofissue",
       "requestQueryMap": "{\"wardId\" : \"Data.ward.keyword\", \"district\" : \"Data.district.keyword\", \"tenantId\" : \"Data.tenantId.keyword\"}", 
       "indexName": "birth-cert-v1",
       "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\": [{\"term\":{\"Data.tenantId.keyword\":\"pb.testing\"}}]}},\"aggs\":{\"downloads\":{\"date_histogram\":{\"field\": \"Data.dateofissue\",\"interval\":\"intervalvalue\"},\"aggs\":{\"Applications Total\":{\"filter\":{\"bool\":{\"must_not\":[{\"terms\":{\"Data.applicationStatus.keyword\":[\"ACTIVE\"]}}]}},\"aggs\":{\"Count\": {\"value_count\": {\"field\":\"Data.birthCertificateNo.keyword\"}}}}}}}}}}"
     }
    ],
    "chartType": "line",
    "valueType": "number",
    "action": "",
    "drillChart": "none",
    "documentType": "_doc",
    "aggregationPaths": [
      "downloads"
    ],
    "isCumulative": false,
    "interval": "month",
  "insight": {
     },
    "_comment": " "
  },
  "birthTransactionsByChannel": {
    "chartName": "DSS_DOWNLOADS_BY_CHANNEL",
    "queries": [
      {
        "module": "BIRTH",
        "requestQueryMap": "{\"wardId\" : \"Data.ward.keyword\", \"district\" : \"Data.district.keyword\", \"tenantId\" : \"Data.tenantId.keyword\"}", 
        "dateRefField": "Data.dateofissue",
        "indexName": "birth-cert-v1",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.tenantId.keyword\":\"pb.testing\"}},{\"terms\":{\"Data.applicationStatus.keyword\":[\"ACTIVE\"]}}]}},\"aggs\":{\"Transactions By Channels\":{\"terms\":{\"field\":\"Data.source.keyword\"},\"aggs\":{\"Count\":{\"value_count\":{\"field\":\"Data.id.keyword\"}}}}}}}}"
      }
    ],
    "chartType": "pie",
    "valueType": "number",
    "action": "",
    "documentType": "_doc",
    "drillChart": "none",
    "aggregationPaths": [
      "Transactions By Channels"
    ],
    "insight": {
    },
    "_comment": "Transactions By Channel"
  },
  "dssBirthByGender": {
    "chartName": "DSS_BIRTH_BY_GENDER",
    "queries": [
      {
        "module": "BIRTH",
        "requestQueryMap": "{\"wardId\" : \"Data.ward.keyword\", \"district\" : \"Data.district.keyword\", \"tenantId\" : \"Data.tenantId.keyword\"}", 
        "dateRefField": "Data.dateofissue",
        "indexName": "birth-cert-v1",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.tenantId.keyword\":\"pb.testing\"}},{\"terms\":{\"Data.applicationStatus.keyword\":[\"ACTIVE\"]}}]}},\"aggs\":{\"Birth By Gender\":{\"terms\":{\"field\":\"Data.gender.keyword\"},\"aggs\":{\"Count\":{\"value_count\":{\"field\":\"Data.id.keyword\"}}}}}}}}"
      }
    ],
    "chartType": "pie",
    "valueType": "number",
    "action": "",
    "documentType": "_doc",
    "drillChart": "none",
    "aggregationPaths": [
      "Birth By Gender"
    ],
    "insight": {
    },
    "_comment": "Birth By Gender"
  },
  "dssBirthByPlace": {
    "chartName": "DSS_BIRTH_BY_PLACE",
    "queries": [
      {
        "module": "BIRTH",
        "requestQueryMap": "{\"wardId\" : \"Data.ward.keyword\", \"district\" : \"Data.district.keyword\", \"tenantId\" : \"Data.tenantId.keyword\"}", 
        "dateRefField": "Data.dateofissue",
        "indexName": "birth-cert-v1",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.tenantId.keyword\":\"pb.testing\"}},{\"terms\":{\"Data.applicationStatus.keyword\":[\"ACTIVE\"]}}]}},\"aggs\":{\"Birth By Place\":{\"terms\":{\"field\":\"Data.birthPlace.keyword\"},\"aggs\":{\"Count\":{\"value_count\":{\"field\":\"Data.birthCertificateNo.keyword\"}}}}}}}}"
      }
    ],
    "chartType": "pie",
    "valueType": "number",
    "action": "",
    "documentType": "_doc",
    "drillChart": "none",
    "aggregationPaths": [
      "Birth By Place"
    ],
    "insight": {
    },
    "_comment": "Birth By Place"
  },
  "xBirthDownloadStatusByBoundary": {
    "chartName": "DSS_BND_CERT_DOWNLOAD_BY_BOUNDARY",
    "queries": [
      {
        "module": "BIRTH",
        "requestQueryMap": "{\"wardId\" : \"Data.ward.keyword\", \"district\" : \"Data.district.keyword\", \"tenantId\" : \"Data.tenantId.keyword\"}", 
        "dateRefField": "Data.dateofissue",
        "indexName": "birth-cert-v1",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.tenantId.keyword\":\"pb.testing\"}},{\"terms\":{\"Data.applicationStatus.keyword\":[\"ACTIVE\"]}}]}},\"aggs\":{\"Total Downloads (Mobile App)\":{\"filter\":{\"bool\":{\"must\":[{\"terms\":{\"Data.source.keyword\":[\"mobileapp\"]}}]}},\"aggs\":{\"Count\":{\"value_count\":{\"field\":\"Data.birthCertificateNo.keyword\"}}}},\"Total Downloads (Web)\":{\"filter\":{\"bool\":{\"must\":[{\"terms\":{\"Data.source.keyword\":[\"web\"]}}]}},\"aggs\":{\"Count\":{\"value_count\":{\"field\":\"Data.birthCertificateNo.keyword\"}}}},\"Total Downloads\":{\"value_count\":{\"field\":\"Data.birthCertificateNo.keyword\"}},\"Delayed Registrations\":{\"filter\":{\"bool\":{\"must\":[{\"script\":{\"script\":{\"source\":\"doc['Data.dateofreport'].value-doc['Data.dateofbirth'].value>params.threshold\",\"lang\":\"painless\",\"params\":{\"threshold\":31556952000}}}}]}},\"aggs\":{\"Count\":{\"value_count\":{\"field\":\"Data.birthCertificateNo.keyword\"}}}}}}}}"
      }
    ],
    "isMdmsEnabled": true,
    "filterKeys": [
      {"key": "tenantId", "column": "DDRs"}
    ],
    "isPostResponseHandler": true,
    "postAggregationTheory" : "repsonseToDifferenceOfDates",
    "chartType": "xtable",
    "valueType": "number",
    "drillChart": "xBirthDownloadByUlb",
    "documentType": "_doc",
    "action": "",
    "plotLabel": "DDRs",
    "excludedColumns": [],
    "removedFields":[  
       ],
    "computedFields": [
    ],
    "isRoundOff":true,
    "aggregationPaths": [
      "Total Downloads (Mobile App)",
      "Total Downloads (Web)",
      "Total Downloads",
      "Delayed Registrations"
    ],
    "pathDataTypeMapping": [
      {
        "Total Downloads (Mobile App)": "number"
      },
      {
        "Total Downloads (Web)": "number"
      },
      {
        "Total Downloads": "number"
      },
      {
        "Delayed Registrations": "number"
      }
    ],
    "insight": {
   },
    "_comment": ""
  },
  "xBirthDownloadByUlb": {
    "chartName": "DSS_BND_CERT_DOWNLOAD_BY_ULB",
    "queries": [
      {
        "module": "BIRTH",
        "requestQueryMap": "{\"wardId\" : \"Data.ward.keyword\", \"district\" : \"Data.district.keyword\", \"tenantId\" : \"Data.tenantId.keyword\"}", 
        "dateRefField": "Data.dateofissue",
        "indexName": "birth-cert-v1",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.tenantId.keyword\":\"pb.testing\"}},{\"terms\":{\"Data.applicationStatus.keyword\":[\"ACTIVE\"]}}]}},\"aggs\":{\"ULB \":{\"terms\":{\"field\":\"Data.tenantId.keyword\",\"size\":1000,\"order\":{\"_term\":\"asc\"}},\"aggs\":{\"Total Downloads (Mobile App)\":{\"filter\":{\"bool\":{\"must\":[{\"terms\":{\"Data.source.keyword\":[\"mobileapp\"]}}]}},\"aggs\":{\"Count\":{\"value_count\":{\"field\":\"Data.birthCertificateNo.keyword\"}}}},\"Total Downloads (Web)\":{\"filter\":{\"bool\":{\"must\":[{\"terms\":{\"Data.source.keyword\":[\"web\"]}}]}},\"aggs\":{\"Count\":{\"value_count\":{\"field\":\"Data.birthCertificateNo.keyword\"}}}},\"Total Downloads\":{\"value_count\":{\"field\":\"Data.birthCertificateNo.keyword\"}},\"Delayed Registrations\":{\"filter\":{\"bool\":{\"must\":[{\"script\":{\"script\":{\"source\":\"doc['Data.dateofreport'].value-doc['Data.dateofbirth'].value>params.threshold\",\"lang\":\"painless\",\"params\":{\"threshold\":31556952000}}}}]}},\"aggs\":{\"Count\":{\"value_count\":{\"field\":\"Data.birthCertificateNo.keyword\"}}}}}}}}}}"
      }
    ],
    "filterKeys": [
      {"key": "ulb", "column": "ULB"}
    ],
    "isPostResponseHandler": true,
    "postAggregationTheory" : "repsonseToDifferenceOfDates",
    "chartType": "xtable",
    "valueType": "number",
    "drillChart": "xBirthDownloadByWard",
    "documentType": "_doc",
    "action": "",
    "plotLabel": "ULB",
    "excludedColumns": [],
    "removedFields":[  
    ],
    "computedFields": [
    ],
    "isRoundOff":true,
    "aggregationPaths": [
      "Total Downloads (Mobile App)",
      "Total Downloads (Web)",
      "Total Downloads",
      "Delayed Registrations"
    ],
    "pathDataTypeMapping": [
      {
        "Total Downloads (Mobile App)": "number"
      },
      {
        "Total Downloads (Web)": "number"
      },
      {
        "Total Downloads": "number"
      },
      {
        "Delayed Registrations": "number"
      }
    ],
    "insight": {
   },
    "_comment": ""
  },
  "xBirthDownloadByWard": {
    "chartName": "DSS_BND_CERT_DOWNLOAD_BY_WARD",
    "queries": [
      {
        "module": "BIRTH",
        "requestQueryMap": "{\"wardId\" : \"Data.ward.keyword\", \"district\" : \"Data.district.keyword\", \"tenantId\" : \"Data.tenantId.keyword\"}", 
        "dateRefField": "Data.dateofissue",
        "indexName": "birth-cert-v1",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.tenantId.keyword\":\"pb.testing\"}},{\"terms\":{\"Data.applicationStatus.keyword\":[\"ACTIVE\"]}}]}},\"aggs\":{\"Ward \":{\"terms\":{\"field\":\"Data.ward.keyword\",\"size\":1000,\"order\":{\"_term\":\"asc\"}},\"aggs\":{\"Total Downloads (Mobile App)\":{\"filter\":{\"bool\":{\"must\":[{\"terms\":{\"Data.source.keyword\":[\"mobileapp\"]}}]}},\"aggs\":{\"Count\":{\"value_count\":{\"field\":\"Data.birthCertificateNo.keyword\"}}}},\"Total Downloads (Web)\":{\"filter\":{\"bool\":{\"must\":[{\"terms\":{\"Data.source.keyword\":[\"web\"]}}]}},\"aggs\":{\"Count\":{\"value_count\":{\"field\":\"Data.birthCertificateNo.keyword\"}}}},\"Total Downloads\":{\"value_count\":{\"field\":\"Data.birthCertificateNo.keyword\"}},\"Delayed Registrations\":{\"filter\":{\"bool\":{\"must\":[{\"script\":{\"script\":{\"source\":\"doc['Data.dateofreport'].value-doc['Data.dateofbirth'].value>params.threshold\",\"lang\":\"painless\",\"params\":{\"threshold\":31556952000}}}}]}},\"aggs\":{\"Count\":{\"value_count\":{\"field\":\"Data.birthCertificateNo.keyword\"}}}}}}}}}}"
      }
    ],
    "filterKeys": [
      {"key": "ward", "column": "Ward"}
    ],
    "isPostResponseHandler": true,
    "postAggregationTheory" : "repsonseToDifferenceOfDates",
    "chartType": "xtable",
    "valueType": "number",
    "drillChart": "none",
    "documentType": "_doc",
    "action": "",
    "plotLabel": "Ward",
    "excludedColumns": [],
    "removedFields":[  
    ],
    "computedFields": [
    ],
    "isRoundOff":true,
    "aggregationPaths": [
      "Total Downloads (Mobile App)",
      "Total Downloads (Web)",
      "Total Downloads",
      "Delayed Registrations"
    ],
    "pathDataTypeMapping": [
      {
        "Total Downloads (Mobile App)": "number"
      },
      {
        "Total Downloads (Web)": "number"
      },
      {
        "Total Downloads": "number"
      },
      {
        "Delayed Registrations": "number"
      }
    ],
    "insight": {
   },
    "_comment": ""
  },
  "deathDownloadTrend": {
    "chartName": "DSS_DEATH_DOWNLOAD_TREND",
    "queries": [
     {
       "module": "DEATH",
       "dateRefField": "Data.dateofissue",
       "requestQueryMap": "{\"wardId\" : \"Data.ward.keyword\", \"district\" : \"Data.district.keyword\", \"tenantId\" : \"Data.tenantId.keyword\"}", 
       "indexName": "death-cert-v1",
       "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\": [{\"term\":{\"Data.tenantId.keyword\":\"pb.testing\"}}]}},\"aggs\":{\"downloads\":{\"date_histogram\":{\"field\": \"Data.dateofissue\",\"interval\":\"intervalvalue\"},\"aggs\":{\"Applications Total\":{\"filter\":{\"bool\":{\"must_not\":[{\"terms\":{\"Data.applicationStatus.keyword\":[\"ACTIVE\"]}}]}},\"aggs\":{\"Count\": {\"value_count\": {\"field\":\"Data.deathCertificateNo.keyword\"}}}}}}}}}}"
     }
    ],
    "chartType": "line",
    "valueType": "number",
    "action": "",
    "drillChart": "none",
    "documentType": "_doc",
    "aggregationPaths": [
      "downloads"
    ],
    "isCumulative": false,
    "interval": "month",
  "insight": {
     },
    "_comment": " "
  },
  "deathTransactionsByChannel": {
    "chartName": "DSS_DOWNLOADS_BY_CHANNEL",
    "queries": [
      {
        "module": "DEATH",
        "requestQueryMap": "{\"wardId\" : \"Data.ward.keyword\", \"district\" : \"Data.district.keyword\", \"tenantId\" : \"Data.tenantId.keyword\"}", 
        "dateRefField": "Data.dateofissue",
        "indexName": "death-cert-v1",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.tenantId.keyword\":\"pb.testing\"}},{\"terms\":{\"Data.applicationStatus.keyword\":[\"ACTIVE\"]}}]}},\"aggs\":{\"Transactions By Channels\":{\"terms\":{\"field\":\"Data.source.keyword\"},\"aggs\":{\"Count\":{\"value_count\":{\"field\":\"Data.id.keyword\"}}}}}}}}"
      }
    ],
    "chartType": "pie",
    "valueType": "number",
    "action": "",
    "documentType": "_doc",
    "drillChart": "none",
    "aggregationPaths": [
      "Transactions By Channels"
    ],
    "insight": {
    },
    "_comment": "Transactions By Channel"
  },
  "xDeathDownloadsByBoundary": {
    "chartName": "DSS_CERT_DOWNLOAD_BY_BOUNDARY",
    "queries": [
      {
        "module": "DEATH",
       "dateRefField": "Data.dateofissue",
       "requestQueryMap": "{\"wardId\" : \"Data.ward.keyword\", \"district\" : \"Data.district.keyword\", \"tenantId\" : \"Data.tenantId.keyword\"}", 
       "indexName": "death-cert-v1",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.tenantId.keyword\":\"pb.testing\"}},{\"terms\":{\"Data.applicationStatus.keyword\":[\"ACTIVE\"]}}]}},\"aggs\":{\"total_downloads_mobile_app\":{\"filter\":{\"bool\":{\"must\":[{\"term\":{\"Data.source.keyword\":\"mobileapp\"}}]}},\"aggs\":{\"mobile_app\":{\"value_count\":{\"field\":\"Data.source.keyword\"}}}},\"total_downloads_web\":{\"filter\":{\"bool\":{\"must\":[{\"term\":{\"Data.source.keyword\":\"web\"}}]}},\"aggs\":{\"web\":{\"value_count\":{\"field\":\"Data.source.keyword\"}}}},\"death_total_downloads\":{\"value_count\":{\"field\":\"Data.deathCertificateNo.keyword\"}},\"death_delayed_registrations\":{\"filter\":{\"bool\":{\"must\":[{\"script\":{\"script\":{\"source\":\"doc['Data.dateofreport'].value-doc['Data.dateofdeath'].value>params.threshold\",\"lang\":\"painless\",\"params\":{\"threshold\":31536000000}}}}]}},\"aggs\":{\"registrations\":{\"value_count\":{\"field\":\"Data.deathCertificateNo.keyword\"}}}}}}}}"
      }
    ],
    "isMdmsEnabled": true,
    "filterKeys": [
      {"key": "tenantId", "column": "DDRs"}
    ],
    "isPostResponseHandler": true,
    "postAggregationTheory" : "repsonseToDifferenceOfDates",
    "chartType": "xtable",
    "valueType": "number",
    "drillChart": "xDeathDownloadsByUlb",
    "documentType": "_doc",
    "action": "",
    "plotLabel": "DDRs",
    "aggregationPaths": [
      "total_downloads_mobile_app",
      "total_downloads_web",
      "death_total_downloads",
      "death_delayed_registrations"
    ],
    "pathDataTypeMapping": [
      {
        "total_downloads_mobile_app": "number"
      },
      {
        "total_downloads_web": "number"
      },
      {
        "death_total_downloads": "number"
      },
      {
        "death_delayed_registrations": "number"
      }
    ],
    "insight": {
    },
    "_comment": ""
  },
  "xDeathDownloadsByUlb": {
    "chartName": "DSS_CERT_DOWNLOAD_BY_ULB",
    "queries": [
      {
        "module": "DEATH",
       "dateRefField": "Data.dateofissue",
       "requestQueryMap": "{\"wardId\" : \"Data.ward.keyword\", \"district\" : \"Data.district.keyword\", \"tenantId\" : \"Data.tenantId.keyword\"}", 
       "indexName": "death-cert-v1",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.tenantId.keyword\":\"pb.testing\"}},{\"terms\":{\"Data.applicationStatus.keyword\":[\"ACTIVE\"]}}]}},\"aggs\":{\"Ulb\":{\"terms\":{\"field\":\"Data.tenantId.keyword\",\"size\":1000,\"order\":{\"_term\":\"asc\"}},\"aggs\":{\"total_downloads_mobile_app\":{\"filter\":{\"bool\":{\"must\":[{\"term\":{\"Data.source.keyword\":\"mobileapp\"}}]}},\"aggs\":{\"mobile_app\":{\"value_count\":{\"field\":\"Data.source.keyword\"}}}},\"total_downloads_web\":{\"filter\":{\"bool\":{\"must\":[{\"term\":{\"Data.source.keyword\":\"web\"}}]}},\"aggs\":{\"web\":{\"value_count\":{\"field\":\"Data.source.keyword\"}}}},\"total_downloads\":{\"value_count\":{\"field\":\"Data.deathCertificateNo.keyword\"}},\"delayed_registrations\":{\"filter\":{\"bool\":{\"must\":[{\"script\":{\"script\":{\"source\":\"doc['Data.dateofreport'].value-doc['Data.dateofdeath'].value>params.threshold\",\"lang\":\"painless\",\"params\":{\"threshold\":31536000000}}}}]}},\"aggs\":{\"registrations\":{\"value_count\":{\"field\":\"Data.deathCertificateNo.keyword\"}}}}}}}}}}"
      }
    ],
    "filterKeys": [
      {"key": "ulb", "column": "Ulb"}
    ],
    "isPostResponseHandler": true,
    "postAggregationTheory" : "repsonseToDifferenceOfDates",
    "chartType": "table",
    "valueType": "number",
    "drillChart": "xDeathDownloadsByWard",
    "documentType": "_doc",
    "action": "",
    "plotLabel": "Ulb",
    "aggregationPaths": [
      "total_downloads_mobile_app",
      "total_downloads_web",
      "total_downloads",
      "delayed_registrations"
    ],
    "pathDataTypeMapping": [
      {
        "total_downloads_mobile_app": "number"
      },
      {
        "total_downloads_web": "number"
      },
      {
        "total_downloads": "number"
      },
      {
        "delayed_registrations": "number"
      }
    ],
    "insight": {
    },
    "_comment": ""
  },
  "xDeathDownloadsByWard": {
    "chartName": "DSS_CERT_DOWNLOAD_BY_WARD",
    "queries": [
      {
        "module": "DEATH",
       "dateRefField": "Data.dateofissue",
       "requestQueryMap": "{\"wardId\" : \"Data.ward.keyword\", \"district\" : \"Data.district.keyword\", \"tenantId\" : \"Data.tenantId.keyword\"}", 
       "indexName": "death-cert-v1",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.tenantId.keyword\":\"pb.testing\"}},{\"terms\":{\"Data.applicationStatus.keyword\":[\"ACTIVE\"]}}]}},\"aggs\":{\"Ward\":{\"terms\":{\"field\":\"Data.ward.keyword\",\"size\":1000,\"order\":{\"_term\":\"asc\"}},\"aggs\":{\"total_downloads_mobile_app\":{\"filter\":{\"bool\":{\"must\":[{\"term\":{\"Data.source.keyword\":\"mobileapp\"}}]}},\"aggs\":{\"mobile_app\":{\"value_count\":{\"field\":\"Data.source.keyword\"}}}},\"total_downloads_web\":{\"filter\":{\"bool\":{\"must\":[{\"term\":{\"Data.source.keyword\":\"web\"}}]}},\"aggs\":{\"web\":{\"value_count\":{\"field\":\"Data.source.keyword\"}}}},\"total_downloads\":{\"value_count\":{\"field\":\"Data.deathCertificateNo.keyword\"}},\"delayed_registrations\":{\"filter\":{\"bool\":{\"must\":[{\"script\":{\"script\":{\"source\":\"doc['Data.dateofreport'].value-doc['Data.dateofdeath'].value>params.threshold\",\"lang\":\"painless\",\"params\":{\"threshold\":31536000000}}}}]}},\"aggs\":{\"registrations\":{\"value_count\":{\"field\":\"Data.deathCertificateNo.keyword\"}}}}}}}}}}"
      }
    ],
    "filterKeys": [
      {"key": "ward", "column": "Ward"}
    ],
    "isPostResponseHandler": true,
    "postAggregationTheory" : "repsonseToDifferenceOfDates",
    "chartType": "table",
    "valueType": "number",
    "drillChart": "none",
    "documentType": "_doc",
    "action": "",
    "plotLabel": "Ward",
    "aggregationPaths": [
      "total_downloads_mobile_app",
      "total_downloads_web",
      "total_downloads",
      "delayed_registrations"
    ],
    "pathDataTypeMapping": [
      {
        "total_downloads_mobile_app": "number"
      },
      {
        "total_downloads_web": "number"
      },
      {
        "total_downloads": "number"
      },
      {
        "delayed_registrations": "number"
      }
    ],
    "insight": {
    },
    "_comment": ""
  }
```

[Click here to check the complete configuration](https://github.com/egovernments/configs/blob/qa/egov-dss-dashboards/dashboard-analytics/ChartApiConfig.json)

**Master Dashboard Configuration:** Master Dashboard Configuration is the main configuration that defines the key insights and visualizations to be painted on the screen. It includes all the visualizations, the groups, charts embedded within them and even the dimensions in terms of height and width.&#x20;

```
 {
      "name": "DSS_BIRTH_DEATH",
      "id": "birth-death",
      "isActive": "",
      "style": "linear",
      "visualizations": [
        {
          "row": 1,
          "name": "DSS_BIRTH",
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
                  "id": "dssBirthTotalApplication",
                  "name": "DSS_BIRTH_TOTAL_APPLICATION",
                  "code": "",
                  "chartType": "metric",
                  "filter": "",
                  "headers": []
                },
                {
                  "id": "birthNetCollection",
                  "name": "DSS_BIRTH_NET_COLLECTION",
                  "code": "",
                  "chartType": "metric",
                  "filter": "",
                  "headers": []
                }
              ]
            },
            {
              "id": 342,
              "name": "DSS_BIRTH_DOWNLOAD_TREND",
              "dimensions": {
                "height": 350,
                "width": 7
              },
              "vizType": "chart",
              "isCollapsible": false,
              "charts": [
                {
                  "id": "birthDownloadTrend",
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
          "name": "DSS_BIRTH",
          "vizArray": [
          {
              "id": 323,
              "name": "DSS_DOWNLOADS_BY_CHANNEL",
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
                  "id": "birthTransactionsByChannel",
                  "name": "DSS_DOWNLOADS_BY_CHANNEL",
                  "code": "",
                  "chartType": "donut",
                  "filter": "",
                  "headers": []
                }
              ]
            },
            {
              "id": 342,
              "name": "DSS_BIRTH_BY_GENDER",
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
                  "id": "dssBirthByGender",
                  "name": "DSS_BIRTH_BY_GENDER",
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
          "name": "DSS_BIRTH",
          "vizArray": [
            {
              "id": 431,
              "name": "DSS_CERT_DOWNLOAD_BY_TENANT",
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
                  "id": "xBirthDownloadStatusByBoundary",
                  "name": "DSS_CERT_DOWNLOAD_BY_BOUNDARY",
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
          "name": "DSS_DEATH",
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
                  "id": "dssDeathTotalApplication",
                  "name": "DSS_DEATH_TOTAL_APPLICATION",
                  "code": "",
                  "chartType": "metric",
                  "filter": "",
                  "headers": []
                },
                {
                  "id": "deathNetCollection",
                  "name": "DSS_DEATH_NET_COLLECTION",
                  "code": "",
                  "chartType": "metric",
                  "filter": "",
                  "headers": []
                }
              ]
            },
            {
              "id": 342,
              "name": "DSS_DEATH_DOWNLOAD_TREND",
              "dimensions": {
                "height": 350,
                "width": 7
              },
              "vizType": "chart",
              "isCollapsible": false,
              "charts": [
                {
                  "id": "deathDownloadTrend",
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
          "name": "DSS_DEATH",
          "vizArray": [
          {
              "id": 323,
              "name": "DSS_DOWNLOADS_BY_CHANNEL",
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
                  "id": "deathTransactionsByChannel",
                  "name": "DSS_DOWNLOADS_BY_CHANNEL",
                  "code": "",
                  "chartType": "donut",
                  "filter": "",
                  "headers": []
                }
              ]
            },
            {
              "id": 342,
              "name": "DSS_DEATH_BY_AGE_CATEGORY",
              "dimensions": {
                "height": 350,
                "width": 7
              },
              "vizType": "chart",
              "isCollapsible": false,
              "charts": [
                {
                  "id": "deathByCategory",
                  "name": "Monthly",
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
          "row": 7,
          "name": "DSS_DEATH",
          "vizArray": [
            {
              "id": 431,
              "name": "DSS_CERT_DOWNLOAD_BY_TENANT",
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
                  "id": "xDeathDownloadsByBoundary",
                  "name": "DSS_CERT_DOWNLOAD_BY_BOUNDARY",
                  "code": "",
                  "chartType": "table",
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

[Click here for the complete configuration](https://github.com/egovernments/configs/blob/qa/egov-dss-dashboards/dashboard-analytics/MasterDashboardConfig.json)

**Role Dashboard Mappings Configuration:** Master Dashboard configuration explained earlier contains the list of available dashboards. Map the roles to specific dashboard views based on the user role requirements. The configuration allows each role to be mapped to authorized dashboard views.

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
          "name": "Birth Death",
          "id": "birth-death"
        }
      ]
    }

  ]
}
```

[Click here to check the configuration](https://github.com/egovernments/configs/blob/qa/egov-dss-dashboards/dashboard-analytics/RoleDashboardMappingsConf.json)

**MDMS configuration to be added:** _common-masters/uiCommonConstants.json_

```
"birth-death":{
                  "routePath":"/dashboard/birth-death",
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
    },    
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
    }
```

[Click here to check the complete configuration](https://github.com/egovernments/egov-mdms-data/blob/QA/data/pb/ACCESSCONTROL-ROLEACTIONS/roleactions.json)

Action test.json:

```
{
     "id": {{PlaceHolder1}},
      "name": "DSS Dashboard Config Birth and Death",
      "url": "/dashboard-analytics/dashboard/getDashboardConfig/birth-death",
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
      "name": "Dashboard Birth and Death",
      "url": "url",
      "displayName": "Birth and Death",
      "orderNumber": 4,
      "parentModule": "dss-dashboard",
      "enabled": true,
      "serviceCode": "DSS",
      "code": "null",
      "path": "Dashboard.Birth and Death",
      "navigationURL": "/digit-ui/employee/dss/dashboard/birth-death",
      "leftIcon": "places:business-center",
      "rightIcon": ""
}
```

[Click here to check the complete configuration](https://github.com/egovernments/egov-mdms-data/blob/QA/data/pb/ACCESSCONTROL-ACTIONS-TEST/actions-test.json)

Birth and Death - State DSS contains multiple graphs which represent the data of Birth and Death. Each graph has its own configuration which will describe the chart and its type.

State DSS contains the following charts in Birth & Death module:

**Birth and Death Page**

**Birth:**

* Overview
* Certificates Download Trend
* Downloads by Channel
* Births by Gender
* Certificate Downloads by Boundary

**Overview:** The overview graph contains multiple data information as below in the selected time period.

* **Total Certificate Downloads:** This represents the total number of birth certificates downloaded.
* &#x20;**Total Collection:** Total revenue collected for downloading birth certificates for the applied date filter.

![](<../../../../.gitbook/assets/image (414).png>)

**Certificates Download Trend:** This is a line graph that shows total birth certificates downloaded for a given month, total Birth Certificates downloaded for the applied date filter.

**line** - this graph/chart is data representation on date histograms or date groupings.

![](<../../../../.gitbook/assets/image (356).png>)

**Downloads by Channel:** This is a pie chart where total birth certificate downloads are bifurcated by channel (Mobile App, Web etc.)

![](<../../../../.gitbook/assets/image (363).png>)

**Births by Gender:** A pie chart illustrating the total births registered are bifurcated by gender

![](<../../../../.gitbook/assets/image (355).png>)

**Certificate Downloads by Boundary:** This tabular chart representation graph shows multiple Birth information like Total Downloads (Mobile App), Total Downloads (Web), Total Downloads, Delayed Registrations. And this table shows the data in DDR level and also has the drill down chart for each state to ulb and from ulb to ward level data for the same.

_**xtable**_ type adds multiple computed fields with the aggregated dynamic fields.

To add multiple computed columns -&#x20;

* provide the actionName in the following format - actionNameComputedField\<T> interface
* provide the fields \[] names as it exists in the query key
* provide the newField as a name to reflect the computed details

![](<../../../../.gitbook/assets/image (354).png>)

Clicking on any DDR name offers a drill-down chart that represents the specific state data.

![](<../../../../.gitbook/assets/image (396).png>)

Clicking on the ULB navigates to show the data at the ward level.

![](<../../../../.gitbook/assets/image (416).png>)

**Death:**

* Overview
* Certificates Download Trend
* Downloads by Channel
* Deaths by Age Category
* Certificate Downloads by Boundary

**Overview:** The overview graph contains multiple data information as below in the selected time period.

* **Total Certificate Downloads:** This represents the total number of death certificates downloaded.
* &#x20;**Total Collection:** Total revenue collected for downloading death certificates for the applied date filter.

![](<../../../../.gitbook/assets/image (399).png>)

**Certificates Download Trend: A** line graph that shows total death certificates downloaded for a given month, total death Certificates downloaded for the applied date filter.

**line** - this graph/chart is data representation on date histograms or date groupings.

![](<../../../../.gitbook/assets/image (389).png>)

**Downloads by Channel:** This is a pie chart where total death certificate downloads are bifurcated by channel (Mobile App, Web etc.)

![](<../../../../.gitbook/assets/image (373).png>)

**Deaths by Gender:** This will be a split bar graph where total deaths registered will be bifurcated by age category (< 2 years, 2-15, 15-29, 30-44, 45-59, 60-74, >= 75) and each bar will show gender wise split

![](blob:https://digit-discuss.atlassian.net/affdf73f-e0d2-499b-a187-372b60f38ec7#media-blob-url=true\&id=397f47ca-dd02-4232-971a-52ba43e46c81\&collection=contentId-2131591200\&contextId=2131591200\&height=432\&width=818\&alt=)

On click of any Category name will enter into drill down charts, which will represents that specific age group data.

![](blob:https://digit-discuss.atlassian.net/c4af0872-cd31-4110-8640-762423c19127#media-blob-url=true\&id=9fbdc409-390b-4807-a024-43a6ec76cf16\&collection=contentId-2131591200\&contextId=2131591200\&height=489\&width=827\&alt=)

&#x20;

**Certificate Downloads by Boundary :** This tabular chart representation graph shows multiple Birth information like Total Downloads (Mobile App), Total Downloads (Web), Total Downloads, Delayed Registrations. And this table shows the data in DDR level and also has the drill down chart for each state to ulb and from ulb to ward level data for the same.

xtable type allows to add multiple computed fields with the aggregated fields dynamically added.

To add multiple computed columns,  computedFields \[]  where actionName (IComputedField\<T> interface), fields \[] names as in exist in query key, newField as name to appear for computation must be defined.

![](blob:https://digit-discuss.atlassian.net/a807fa5c-9bb6-4088-bd6c-d420ac7c57b2#media-blob-url=true\&id=e3ea34f1-7da3-4917-9628-d1cd3caf09ef\&collection=contentId-2131591200\&contextId=2131591200\&height=389\&width=1662\&alt=)

On click of any DDR name will enter into drill down charts, which will represents that specific state data.

![](blob:https://digit-discuss.atlassian.net/edd6d2c3-053e-4931-a5c0-8c6fdd481cf1#media-blob-url=true\&id=d379671e-3f1c-4bc5-ab59-7de260e03b99\&collection=contentId-2131591200\&contextId=2131591200\&height=340\&width=1658\&alt=)

On click of the ULB will navigate to wards under that specific ULB and each ward shows the specific data regarding that ward.

![](blob:https://digit-discuss.atlassian.net/f3c9dc03-8314-46af-aec7-abefc2182240#media-blob-url=true\&id=00076825-61a2-417d-a4b4-c7a0670506a6\&collection=contentId-2131591200\&contextId=2131591200\&height=532\&width=1706\&alt=)

#### **Newly introduced property:** <a href="#newly-introduced-property" id="newly-introduced-property"></a>

**isRoundOff**: This property is introduced to round off the decimal values. Ex: if the value is 25.43 by using isRoundOff property in configuration we will get it as 25. if value is 22.56 round of value will be 23.\
This can be used for insights configuration as well for overview graph.

#### Common Properties available: <a href="#common-properties-available" id="common-properties-available"></a>

**Key(eg: fsmTotalrequest) :** This is the Visualization Code. This key will be referred to in further visualization configurations.

This is the key which will be used by the client application to indicate which visualization is needed for display.

**chartName :** The name of the Chart which has to be used as a label on the Dashboard. The name of the Chart will be a detailed name.

In this configuration, the Name of the Chart will be the code of Localization which will be used by Client Side.

**queries :** Some visualizations are derived from a specific data source. While some others are derived from different data sources and are combined together to get a meaningful representation.

The queries of aggregation which are to be used to fetch out the right data in the right aggregated format are configured here.

**queries.module :** The module / domain level, on which the query should be applied on. Birth and Death is birth-death.

**queries.indexName :** The name of the index upon which the query has to be executed is configured here.

**queries.aggrQuery :** The aggregation query in itself is added here. Based on the Module and the Index name specified, this query is attached to the filter part of the complete search request and then executed against that index

**queries.requestQueryMap :** Client Request would carry certain fields which are to be filtered. The parameters specified in the Client Request are different from the parameters in each of these indexed documents.

In order to map the parameters of the request to the parameters of the ElasticSearch Document, this mapping is maintained.

**queries.dateRefField :** Each of these modules have separate indexes. And all of them have their own date fields.&#x20;

When there is a date filter applied against these visualizations, each of them has to apply it against their own date reference fields.

In order to maintain what is the date field in which index, we have this configured in this configuration parameter.

**chartType :** As there are different types of visualizations, this field defines what is the type of chart / visualization that this data should be used to represent.&#x20;

**Chart types available are**:

**metric** - this represents the aggregated amount/value for records filter by the aggregate es query&#x20;

**pie** - this represents the aggregated data on grouping. This is can be used to represent any line graph, bar graph, pie chart or donuts

**line** - this graph/chart is data representation on date histograms or date groupings

**perform** - this chart represents groping data as performance wise.

**table** - represents a form of plots and value with headers as grouped on and list of its key, values pairs.&#x20;

**xtable -** represents a advanced feature of table, it has addition capabilities for dynamic adding header values.

**valueType :** In any case of data, the values which are sent to plot, might be a percentage, sometimes an amount and sometimes it is just a count.

In order to represent them and differentiate the numbers from amount from percentage, this field is used to indicate the type of value that this Visualization will be sending.

**action :** Some of the visualizations are not just aggregation on data source. There might be some cases where we have to do a post aggregation computation.

For Example, in the case of Top 3 Performing ULBs, the Target and Total Collection is obtained and then the percentage is calculated. In these kinds of cases, what is the action that has to be performed on that data obtained is defined in this parameter.&#x20;

**documentType :** The type of document upon which the query has to be executed is defined here.&#x20;

**drillChart :** If there is a drill down on the visualization, then the code of the Drill Down Visualization is added here. This will be used by Client Service to manage drill downs.

**aggregationPaths :** All the queries will be having Aggregation names in it. In order to fetch the value out of each Aggregation Responses, the name of the aggregation in the query will be an easy bet. These aggregation paths will have the names of Aggregation in it.

**insights :** It is to show the data with the comparison of last year with arrow symbols, it will show the data in how much % is increased or decreased.&#x20;

**\_comment :** In order to display information on the “i” symbol of each visualization, Visualization Information is maintained in this field.&#x20;

#### **Index Properties of State Birth and Death- Dss:** <a href="#index-properties-of-state-birth-and-death-dss" id="index-properties-of-state-birth-and-death-dss"></a>

The index that contains data for State-Birth and Death are - birth-cert-v1, death-cert-v1

The mapping for this index is:

Birth :

`1"properties" : { 2 "Data" : { 3 "properties" : { 4 "additionalDetail" : { 5 "properties" : { 6 "cb" : { 7 "type" : "text", 8 "fields" : { 9 "keyword" : { 10 "type" : "keyword", 11 "ignore_above" : 256 12 } 13 } 14 }, 15 "code" : { 16 "type" : "text", 17 "fields" : { 18 "keyword" : { 19 "type" : "keyword", 20 "ignore_above" : 256 21 } 22 } 23 } 24 } 25 }, 26 "applicationStatus" : { 27 "type" : "text", 28 "fields" : { 29 "keyword" : { 30 "type" : "keyword", 31 "ignore_above" : 256 32 } 33 } 34 }, 35 "auditDetails" : { 36 "properties" : { 37 "createdBy" : { 38 "type" : "text", 39 "fields" : { 40 "keyword" : { 41 "type" : "keyword", 42 "ignore_above" : 256 43 } 44 } 45 }, 46 "createdTime" : { 47 "type" : "long" 48 }, 49 "lastModifiedBy" : { 50 "type" : "text", 51 "fields" : { 52 "keyword" : { 53 "type" : "keyword", 54 "ignore_above" : 256 55 } 56 } 57 }, 58 "lastModifiedTime" : { 59 "type" : "long" 60 } 61 } 62 }, 63 "birthCertificateNo" : { 64 "type" : "text", 65 "fields" : { 66 "keyword" : { 67 "type" : "keyword", 68 "ignore_above" : 256 69 } 70 } 71 }, 72 "birthDtlId" : { 73 "type" : "text", 74 "fields" : { 75 "keyword" : { 76 "type" : "keyword", 77 "ignore_above" : 256 78 } 79 } 80 }, 81 "birthPlace" : { 82 "type" : "text", 83 "fields" : { 84 "keyword" : { 85 "type" : "keyword", 86 "ignore_above" : 256 87 } 88 } 89 }, 90 "dateofbirth" : { 91 "type" : "long" 92 }, 93 "dateofissue" : { 94 "type" : "date", 95 "format" : "dd-MM-yyyy HH:mm:ss||dd-MM-yyyy||epoch_millis" 96 }, 97 "dateofreport" : { 98 "type" : "long" 99 }, 100 "district" : { 101 "type" : "text", 102 "fields" : { 103 "keyword" : { 104 "type" : "keyword", 105 "ignore_above" : 256 106 } 107 } 108 }, 109 "embeddedUrl" : { 110 "type" : "text", 111 "fields" : { 112 "keyword" : { 113 "type" : "keyword", 114 "ignore_above" : 256 115 } 116 } 117 }, 118 "filestoreid" : { 119 "type" : "text", 120 "fields" : { 121 "keyword" : { 122 "type" : "keyword", 123 "ignore_above" : 256 124 } 125 } 126 }, 127 "gender" : { 128 "type" : "text", 129 "fields" : { 130 "keyword" : { 131 "type" : "keyword", 132 "ignore_above" : 256 133 } 134 } 135 }, 136 "id" : { 137 "type" : "text", 138 "fields" : { 139 "keyword" : { 140 "type" : "keyword", 141 "ignore_above" : 256 142 } 143 } 144 }, 145 "source" : { 146 "type" : "text", 147 "fields" : { 148 "keyword" : { 149 "type" : "keyword", 150 "ignore_above" : 256 151 } 152 } 153 }, 154 "state" : { 155 "type" : "text", 156 "fields" : { 157 "keyword" : { 158 "type" : "keyword", 159 "ignore_above" : 256 160 } 161 } 162 }, 163 "tenantId" : { 164 "type" : "text", 165 "fields" : { 166 "keyword" : { 167 "type" : "keyword", 168 "ignore_above" : 256 169 } 170 } 171 }, 172 "ward" : { 173 "type" : "text", 174 "fields" : { 175 "keyword" : { 176 "type" : "keyword", 177 "ignore_above" : 256 178 } 179 } 180 } 181 } 182 } 183 }`

Death :

`1"properties" : { 2 "Data" : { 3 "properties" : { 4 "additionalDetail" : { 5 "properties" : { 6 "cb" : { 7 "type" : "text", 8 "fields" : { 9 "keyword" : { 10 "type" : "keyword", 11 "ignore_above" : 256 12 } 13 } 14 }, 15 "code" : { 16 "type" : "text", 17 "fields" : { 18 "keyword" : { 19 "type" : "keyword", 20 "ignore_above" : 256 21 } 22 } 23 } 24 } 25 }, 26 "age" : { 27 "type" : "long" 28 }, 29 "applicationStatus" : { 30 "type" : "text", 31 "fields" : { 32 "keyword" : { 33 "type" : "keyword", 34 "ignore_above" : 256 35 } 36 } 37 }, 38 "auditDetails" : { 39 "properties" : { 40 "createdBy" : { 41 "type" : "text", 42 "fields" : { 43 "keyword" : { 44 "type" : "keyword", 45 "ignore_above" : 256 46 } 47 } 48 }, 49 "createdTime" : { 50 "type" : "long" 51 }, 52 "lastModifiedBy" : { 53 "type" : "text", 54 "fields" : { 55 "keyword" : { 56 "type" : "keyword", 57 "ignore_above" : 256 58 } 59 } 60 }, 61 "lastModifiedTime" : { 62 "type" : "long" 63 } 64 } 65 }, 66 "dateofdeath" : { 67 "type" : "long" 68 }, 69 "dateofissue" : { 70 "type" : "long" 71 }, 72 "dateofreport" : { 73 "type" : "long" 74 }, 75 "deathCertificateNo" : { 76 "type" : "text", 77 "fields" : { 78 "keyword" : { 79 "type" : "keyword", 80 "ignore_above" : 256 81 } 82 } 83 }, 84 "deathDtlId" : { 85 "type" : "text", 86 "fields" : { 87 "keyword" : { 88 "type" : "keyword", 89 "ignore_above" : 256 90 } 91 } 92 }, 93 "district" : { 94 "type" : "text", 95 "fields" : { 96 "keyword" : { 97 "type" : "keyword", 98 "ignore_above" : 256 99 } 100 } 101 }, 102 "embeddedUrl" : { 103 "type" : "text", 104 "fields" : { 105 "keyword" : { 106 "type" : "keyword", 107 "ignore_above" : 256 108 } 109 } 110 }, 111 "filestoreid" : { 112 "type" : "text", 113 "fields" : { 114 "keyword" : { 115 "type" : "keyword", 116 "ignore_above" : 256 117 } 118 } 119 }, 120 "gender" : { 121 "type" : "text", 122 "fields" : { 123 "keyword" : { 124 "type" : "keyword", 125 "ignore_above" : 256 126 } 127 } 128 }, 129 "id" : { 130 "type" : "text", 131 "fields" : { 132 "keyword" : { 133 "type" : "keyword", 134 "ignore_above" : 256 135 } 136 } 137 }, 138 "placeofdeath" : { 139 "type" : "text", 140 "fields" : { 141 "keyword" : { 142 "type" : "keyword", 143 "ignore_above" : 256 144 } 145 } 146 }, 147 "source" : { 148 "type" : "text", 149 "fields" : { 150 "keyword" : { 151 "type" : "keyword", 152 "ignore_above" : 256 153 } 154 } 155 }, 156 "state" : { 157 "type" : "text", 158 "fields" : { 159 "keyword" : { 160 "type" : "keyword", 161 "ignore_above" : 256 162 } 163 } 164 }, 165 "tenantId" : { 166 "type" : "text", 167 "fields" : { 168 "keyword" : { 169 "type" : "keyword", 170 "ignore_above" : 256 171 } 172 } 173 }, 174 "ward" : { 175 "type" : "text", 176 "fields" : { 177 "keyword" : { 178 "type" : "keyword", 179 "ignore_above" : 256 180 } 181 } 182 } 183 } 184 } 185 }`

#### _Postman Links_ <a href="#postman-links" id="postman-links"></a>

[_https://www.getpostman.com/collections/a6622af87bd5346d11fc_](https://www.getpostman.com/collections/a6622af87bd5346d11fc)

&#x20;
