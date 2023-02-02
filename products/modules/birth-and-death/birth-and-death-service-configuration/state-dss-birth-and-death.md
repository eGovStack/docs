---
description: Technical Doc
---

# State DSS - Birth and Death

## Overview

There are two dimensions to DSS. The first refers to the process where the data is pooled into ElasticSearch and the second relates to the way the data is fetched, aggregated, computed, transformed and sent across.

The DSS processes are easily configurable and this enables users to configure new analytics insights using a wide range of data sets.&#x20;

This document defines the configuration steps for fetching analytical insights on the DSS for the Birth & Death module.

## Key Concepts

**Analytics:** Micro Service responsible for building, fetching, aggregating and computing the data on ElasticSearch to a consumable data response. This is used for visualizations and graphical representations. &#x20;

**Analytics Configurations:** Analytics contains multiple configurations. Add the changes related to Birth& Death in the dashboard analytics configuration file.\
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

**Master Dashboard Configuration:** Master Dashboard Configuration is the main configuration that defines the key insights and visualizations to be painted on the screen. It includes all the visualizations, the groups, the charts embedded within them and even the dimensions in terms of height and width.&#x20;

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

State DSS contains the following charts in the Birth & Death module:

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

**Certificates Download Trend: A** line graph that shows the total death certificates downloaded for a given month, and total death Certificates downloaded for the applied date filter.

**line** - this graph/chart is data representation on date histograms or date groupings.

![](<../../../../.gitbook/assets/image (389).png>)

**Downloads by Channel:** This is a pie chart where total death certificate downloads are bifurcated by channel (Mobile App, Web etc.)

![](<../../../../.gitbook/assets/image (373).png>)

**Deaths by Gender:** This will be a split bar graph where total deaths registered will be bifurcated by age category (< 2 years, 2-15, 15-29, 30-44, 45-59, 60-74, >= 75) and each bar will show gender wise split

![](<../../../../.gitbook/assets/image (5) (4).png>)

Clicking on any Category name drills down to charts that provide specific age group data.

![](<../../../../.gitbook/assets/image (2) (6).png>)

**Certificate Downloads by Boundary:** This tabular chart representation graph shows multiple Birth information like Total Downloads (Mobile App), Total Downloads (Web), Total Downloads, and Delayed Registrations. And this table shows the data at the DDR level and also has the drill-down chart for each state to ULB and from ULB to ward level data for the same.

xtable type allows to add multiple computed fields with the aggregated fields dynamically added.

To add multiple computed columns,  computedFields \[]  where actionName (IComputedField\<T> interface), fields \[] names as in exist in query key, newField as name to appear for computation must be defined.

<figure><img src="../../../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

Clicking on any DDR name provides the drill-down charts that represent state-specific data.

<figure><img src="../../../../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

Clicking on the ULB navigates to wards under that specific ULB and each ward shows the specific data regarding that ward.

<figure><img src="../../../../.gitbook/assets/image (21).png" alt=""><figcaption></figcaption></figure>

## **Newly Introduced Property** <a href="#newly-introduced-property" id="newly-introduced-property"></a>

**isRoundOff**: This property is introduced to round off the decimal values. Ex: if the value is 25.43 by using the isRoundOff property in the configuration we will get it as 25. if the value is 22.56 round of value will be 23.\
This can be used for insights configuration as well for overview graphs.

## Common Properties Available <a href="#common-properties-available" id="common-properties-available"></a>

**Key(eg: fsmTotalrequest):** This is the Visualization Code. This key will be referred to in further visualization configurations.

This is the key which will be used by the client application to indicate which visualization is needed for display.

**chartName:** The name of the Chart which has to be used as a label on the Dashboard. The name of the Chart will be a detailed name.

In this configuration, the Name of the Chart will be the code of Localization which will be used by the Client Side.

**queries:** Some visualizations are derived from a specific data source. While some others are derived from different data sources and are combined together to get a meaningful representation.

The queries of aggregation which are to be used to fetch out the right data in the right aggregated format are configured here.

**queries.module:** The module/domain level, on which the query should be applied on. Birth and Death is birth-death.

**queries.indexName:** The name of the index upon which the query has to be executed is configured here.

**queries.aggrQuery:** The aggregation query in itself is added here. Based on the Module and the Index name specified, this query is attached to the filter part of the complete search request and then executed against that index

**queries.requestQueryMap:** Client Request would carry certain fields which are to be filtered. The parameters specified in the Client Request are different from the parameters in each of these indexed documents.

In order to map the parameters of the request to the parameters of the ElasticSearch Document, this mapping is maintained.

**queries.dateRefField:** Each of these modules have separate indexes. And all of them have their own date fields.&#x20;

When there is a date filter applied against these visualizations, each of them has to apply it against their own date reference fields.

In order to maintain what is the date field in which index, we have this configured in this configuration parameter.

**chartType:** As there are different types of visualizations, this field defines what is the type of chart/visualization that this data should be used to represent.&#x20;

## **Available Chart Types**&#x20;

**metric** - this represents the aggregated amount/value for records filtered by the aggregate es query&#x20;

**pie** - this represents the aggregated data on grouping. This is can be used to represent any line graph, bar graph, pie chart or donuts

**line** - this graph/chart is data representation on date histograms or date groupings

**perform** - this chart represents groping data performance-wise.

**table** - represents a form of plots and values with headers as grouped on and a list of its key, values pairs.&#x20;

**xtable -** represents an advanced feature of the table, it has the addition capabilities for adding dynamic header values.

**valueType:** In any case of data, the values which are sent to the plot, might be a percentage, sometimes an amount and sometimes it is just a count.

In order to represent them and differentiate the numbers from the amount from the percentage, this field is used to indicate the type of value that this Visualization will be sending.

**action:** Some of the visualizations are not just aggregations of data sources. There might be some cases where we have to do a post-aggregation computation.

For Example, in the case of the Top 3 Performing ULBs, the Target and Total Collection are obtained and then the percentage is calculated. In these kinds of cases, the action that has to be performed on the data obtained is defined in this parameter.&#x20;

**documentType:** The type of document upon which the query has to be executed is defined here.&#x20;

**drillChart:** If there is a drill down on the visualization, then the code of the Drill Down Visualization is added here. This will be used by Client Service to manage drill-downs.

**aggregationPaths:** All the queries will be having Aggregation names in them. In order to fetch the value out of each Aggregation Responses, the name of the aggregation in the query will be an easy bet. These aggregation paths will have the names of Aggregation in them.

**insights:** It is to show the data with the comparison of last year with arrow symbols, it will show the data in how much % is increased or decreased.&#x20;

**\_comment:** In order to display information on the “i” symbol of each visualization, Visualization Information is maintained in this field.&#x20;

#### **Index Properties of State Birth and Death- Dss:** <a href="#index-properties-of-state-birth-and-death-dss" id="index-properties-of-state-birth-and-death-dss"></a>

The index that contains data for State-Birth and Death are - birth-cert-v1, death-cert-v1

The mapping for this index is:

**Birth**

```
"properties" : {
          "Data" : {
            "properties" : {
              "additionalDetail" : {
                "properties" : {
                  "cb" : {
                    "type" : "text",
                    "fields" : {
                      "keyword" : {
                        "type" : "keyword",
                        "ignore_above" : 256
                      }
                    }
                  },
                  "code" : {
                    "type" : "text",
                    "fields" : {
                      "keyword" : {
                        "type" : "keyword",
                        "ignore_above" : 256
                      }
                    }
                  }
                }
              },
              "applicationStatus" : {
                "type" : "text",
                "fields" : {
                  "keyword" : {
                    "type" : "keyword",
                    "ignore_above" : 256
                  }
                }
              },
              "auditDetails" : {
                "properties" : {
                  "createdBy" : {
                    "type" : "text",
                    "fields" : {
                      "keyword" : {
                        "type" : "keyword",
                        "ignore_above" : 256
                      }
                    }
                  },
                  "createdTime" : {
                    "type" : "long"
                  },
                  "lastModifiedBy" : {
                    "type" : "text",
                    "fields" : {
                      "keyword" : {
                        "type" : "keyword",
                        "ignore_above" : 256
                      }
                    }
                  },
                  "lastModifiedTime" : {
                    "type" : "long"
                  }
                }
              },
              "birthCertificateNo" : {
                "type" : "text",
                "fields" : {
                  "keyword" : {
                    "type" : "keyword",
                    "ignore_above" : 256
                  }
                }
              },
              "birthDtlId" : {
                "type" : "text",
                "fields" : {
                  "keyword" : {
                    "type" : "keyword",
                    "ignore_above" : 256
                  }
                }
              },
              "birthPlace" : {
                "type" : "text",
                "fields" : {
                  "keyword" : {
                    "type" : "keyword",
                    "ignore_above" : 256
                  }
                }
              },
              "dateofbirth" : {
                "type" : "long"
              },
              "dateofissue" : {
                "type" : "date",
                "format" : "dd-MM-yyyy HH:mm:ss||dd-MM-yyyy||epoch_millis"
              },
              "dateofreport" : {
                "type" : "long"
              },
              "district" : {
                "type" : "text",
                "fields" : {
                  "keyword" : {
                    "type" : "keyword",
                    "ignore_above" : 256
                  }
                }
              },
              "embeddedUrl" : {
                "type" : "text",
                "fields" : {
                  "keyword" : {
                    "type" : "keyword",
                    "ignore_above" : 256
                  }
                }
              },
              "filestoreid" : {
                "type" : "text",
                "fields" : {
                  "keyword" : {
                    "type" : "keyword",
                    "ignore_above" : 256
                  }
                }
              },
              "gender" : {
                "type" : "text",
                "fields" : {
                  "keyword" : {
                    "type" : "keyword",
                    "ignore_above" : 256
                  }
                }
              },
              "id" : {
                "type" : "text",
                "fields" : {
                  "keyword" : {
                    "type" : "keyword",
                    "ignore_above" : 256
                  }
                }
              },
              "source" : {
                "type" : "text",
                "fields" : {
                  "keyword" : {
                    "type" : "keyword",
                    "ignore_above" : 256
                  }
                }
              },
              "state" : {
                "type" : "text",
                "fields" : {
                  "keyword" : {
                    "type" : "keyword",
                    "ignore_above" : 256
                  }
                }
              },
              "tenantId" : {
                "type" : "text",
                "fields" : {
                  "keyword" : {
                    "type" : "keyword",
                    "ignore_above" : 256
                  }
                }
              },
              "ward" : {
                "type" : "text",
                "fields" : {
                  "keyword" : {
                    "type" : "keyword",
                    "ignore_above" : 256
                  }
                }
              }
            }
          }
        }
```

**Death**

```
"properties" : {
          "Data" : {
            "properties" : {
              "additionalDetail" : {
                "properties" : {
                  "cb" : {
                    "type" : "text",
                    "fields" : {
                      "keyword" : {
                        "type" : "keyword",
                        "ignore_above" : 256
                      }
                    }
                  },
                  "code" : {
                    "type" : "text",
                    "fields" : {
                      "keyword" : {
                        "type" : "keyword",
                        "ignore_above" : 256
                      }
                    }
                  }
                }
              },
              "age" : {
                "type" : "long"
              },
              "applicationStatus" : {
                "type" : "text",
                "fields" : {
                  "keyword" : {
                    "type" : "keyword",
                    "ignore_above" : 256
                  }
                }
              },
              "auditDetails" : {
                "properties" : {
                  "createdBy" : {
                    "type" : "text",
                    "fields" : {
                      "keyword" : {
                        "type" : "keyword",
                        "ignore_above" : 256
                      }
                    }
                  },
                  "createdTime" : {
                    "type" : "long"
                  },
                  "lastModifiedBy" : {
                    "type" : "text",
                    "fields" : {
                      "keyword" : {
                        "type" : "keyword",
                        "ignore_above" : 256
                      }
                    }
                  },
                  "lastModifiedTime" : {
                    "type" : "long"
                  }
                }
              },
              "dateofdeath" : {
                "type" : "long"
              },
              "dateofissue" : {
                "type" : "long"
              },
              "dateofreport" : {
                "type" : "long"
              },
              "deathCertificateNo" : {
                "type" : "text",
                "fields" : {
                  "keyword" : {
                    "type" : "keyword",
                    "ignore_above" : 256
                  }
                }
              },
              "deathDtlId" : {
                "type" : "text",
                "fields" : {
                  "keyword" : {
                    "type" : "keyword",
                    "ignore_above" : 256
                  }
                }
              },
              "district" : {
                "type" : "text",
                "fields" : {
                  "keyword" : {
                    "type" : "keyword",
                    "ignore_above" : 256
                  }
                }
              },
              "embeddedUrl" : {
                "type" : "text",
                "fields" : {
                  "keyword" : {
                    "type" : "keyword",
                    "ignore_above" : 256
                  }
                }
              },
              "filestoreid" : {
                "type" : "text",
                "fields" : {
                  "keyword" : {
                    "type" : "keyword",
                    "ignore_above" : 256
                  }
                }
              },
              "gender" : {
                "type" : "text",
                "fields" : {
                  "keyword" : {
                    "type" : "keyword",
                    "ignore_above" : 256
                  }
                }
              },
              "id" : {
                "type" : "text",
                "fields" : {
                  "keyword" : {
                    "type" : "keyword",
                    "ignore_above" : 256
                  }
                }
              },
              "placeofdeath" : {
                "type" : "text",
                "fields" : {
                  "keyword" : {
                    "type" : "keyword",
                    "ignore_above" : 256
                  }
                }
              },
              "source" : {
                "type" : "text",
                "fields" : {
                  "keyword" : {
                    "type" : "keyword",
                    "ignore_above" : 256
                  }
                }
              },
              "state" : {
                "type" : "text",
                "fields" : {
                  "keyword" : {
                    "type" : "keyword",
                    "ignore_above" : 256
                  }
                }
              },
              "tenantId" : {
                "type" : "text",
                "fields" : {
                  "keyword" : {
                    "type" : "keyword",
                    "ignore_above" : 256
                  }
                }
              },
              "ward" : {
                "type" : "text",
                "fields" : {
                  "keyword" : {
                    "type" : "keyword",
                    "ignore_above" : 256
                  }
                }
              }
            }
          }
        }
```

#### _Postman Links_ <a href="#postman-links" id="postman-links"></a>

[_https://www.getpostman.com/collections/a6622af87bd5346d11fc_](https://www.getpostman.com/collections/a6622af87bd5346d11fc)

&#x20;
