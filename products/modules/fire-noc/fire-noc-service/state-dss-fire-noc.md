---
description: Technical Doc
---

# State DSS - Fire NOC

## Overview

DSS has two sides to it. One is the process in which the data is pooled into ElasticSearch and the other is the way it is fetched, aggregated, computed, transformed and sent across.

As this revolves around a variety of data sets, there is a need for making this configurable. So that, tomorrow, given a new scenario is introduced, then it is just a configuration away from getting the newly introduced scenario involved in this flow of the process.&#x20;

This document explains the steps on how to define the configurations for the analytics side Of DSS for FireNoc.

**What is analytics?**

**Analytics:** Micro Service which is responsible for building, fetching, aggregating and computing the Data on ElasticSearch to a consumable Data Response. Which shall be later used for visualizations and graphical representations.&#x20;

**Analytics Configurations:** Analytics contains multiple configurations. we need to add the changes related to firenoc in this dashboard-analytics.\
File location : [<img src="https://github.com/fluidicon.png" alt="" data-size="line">configs/egov-dss-dashboards/dashboard-analytics at qa · egovernments/configs](https://github.com/egovernments/configs/tree/qa/egov-dss-dashboards/dashboard-analytics)\
Below is a list of configurations that need to be changed to run firenoc successfully.

1. Chart API Configuration
2. Master Dashboard Configuration
3. Role Dashboard Mappings Configuration

## **Configuration Details**

### **Chart API Configuration**

Each visualization has its own properties. Each visualization comes from different data sources (Sometimes it is a combination of different data sources)&#x20;

In order to configure each visualization and its properties, we have a Chart API Configuration document.

In this, visualization code, which happens to be the key, has its properties configured as a part of the configuration and are easily changeable.

Here is the sample ChartApiConfiguration.json data for the FireNoc.

```
"nocTodaysCollection": {
    "chartName": "DSS_NOC_TODAYS_COLLECTION",
    "queries": [
      {
        "module": "FIRENOC",
        "indexName": "dss-collection_v2",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must\":[{\"terms\":{\"dataObject.paymentDetails.businessService.keyword\":[\"FIRENOC\"]}},{\"range\":{\"dataObject.paymentDetails.receiptDate\":{\"gte\":\"now-24h\",\"lte\":\"now\"}}}],\"must_not\":[{\"term\":{\"dataObject.tenantId.keyword\":\"pb.testing\"}},{\"term\":{\"dataObject.paymentStatus.keyword\":\"Cancelled\"}}]}},\"aggs\":{\"Todays Collection\":{\"sum\":{\"field\":\"dataObject.paymentDetails.totalAmountPaid\"}}}}}}",
        "requestQueryMap": "{\"wardId\" : \"dataObject.ward.name.keyword\",\"module\" : \"dataObject.paymentDetails.businessService.keyword\",\"tenantId\" : \"dataObject.tenantId\", \"district\" : \"dataObject.tenantData.city.districtCode\" }",
        "dateRefField": ""
      }
    ],
    "chartType": "metric",
    "valueType": "amount",
    "action": "",
    "drillChart": "none",
    "aggregationPaths": [
      "Todays Collection"
    ],
    "insight": {
    },
    "_comment": "FIRE NOC todays collections "
  },

  "nocTotalCollection": {
    "chartName": "DSS_NOC_TOTAL_COLLECTION",
    "queries": [
      {
        "module": "FIRENOC",
        "indexName": "dss-collection_v2",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must\":[{\"terms\":{\"dataObject.paymentDetails.businessService.keyword\":[\"FIRENOC\"]}}],\"must_not\":[{\"term\":{\"dataObject.tenantId.keyword\":\"pb.testing\"}},{\"term\":{\"dataObject.paymentStatus.keyword\":\"Cancelled\"}}]}},\"aggs\":{\"Total Collection\":{\"sum\":{\"field\":\"dataObject.paymentDetails.totalAmountPaid\"}}}}}}",
        "requestQueryMap": "{\"wardId\" : \"dataObject.ward.name.keyword\",\"module\" : \"dataObject.paymentDetails.businessService.keyword\",\"tenantId\" : \"dataObject.tenantId\", \"district\" : \"dataObject.tenantData.city.districtCode\" }",
        "dateRefField": "dataObject.paymentDetails.receiptDate"
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
      "chartResponseMap" : "nocTotalCollection",
      "action" : "differenceOfNumbers",
      "upwardIndicator" : "positive",
      "downwardIndicator" : "negative",
      "textMessage" : "$indicator$value% than last $insightInterval",
      "colorCode" : "#228B22",
      "insightInterval" : "year",
      "isRoundOff": true
    },
    "_comment": "FIRE NOC total collections "
  },

  "nocTotalApplications": {
    "chartName": "DSS_NOC_TOTAL_APPLICATIONS",
    "queries": [
      {
        "module": "FIRENOC",
        "indexName": "firenoc-services",
        "aggrQuery": "{\"aggs\":{\"FireNOC\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.tenantId.keyword\":\"pb.testing\"}}]}},\"aggs\":{\"Total Applications\":{\"value_count\":{\"field\":\"Data.tenantId.keyword\"}}}}}}",
        "requestQueryMap": "{\"wardId\" : \"Data.ward.name.keyword\",\"tenantId\" : \"Data.tenantId\", \"district\" : \"Data.tenantData.city.districtCode\"}",
        "dateRefField": "Data.auditDetails.createdTime"
      }
    ],
    "chartType": "metric",
    "valueType": "number",
    "action": "",
    "drillChart": "none",
    "aggregationPaths": [
      "Total Applications"
    ],
    "insight": {
      "chartResponseMap" : "nocTotalApplications",
      "action" : "differenceOfNumbers",
      "upwardIndicator" : "positive",
      "downwardIndicator" : "negative",
      "textMessage" : "$indicator$value% than last $insightInterval",
      "colorCode" : "#228B22",
      "insightInterval" : "year"
    },
    "_comment": "FIRE NOC total applications "
  },

  "nocProvisionalIssued": {
    "chartName": "DSS_NOC_PROVISIONAL_ISSUED",
    "queries": [
      {
        "module": "FIRENOC",
        "indexName": "firenoc-services",
        "aggrQuery": "{\"aggs\":{\"FireNOC\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.tenantId.keyword\":\"pb.testing\"}}]}},\"aggs\":{\"Provisional Fire Nocs issued\":{\"filter\":{\"bool\":{\"must\":[{\"term\":{\"Data.fireNOCDetails.fireNOCType.keyword\":\"PROVISIONAL\"}}]}}}}}}}",
        "requestQueryMap": "{\"wardId\" : \"Data.ward.name.keyword\",\"tenantId\" : \"Data.tenantId\", \"district\" : \"Data.tenantData.city.districtCode\"}",
        "dateRefField": "Data.auditDetails.createdTime"
      }
    ],
    "chartType": "metric",
    "valueType": "number",
    "action": "",
    "drillChart": "none",
    "aggregationPaths": [
      "Provisional Fire Nocs issued"
    ],
    "insight": {
      "chartResponseMap" : "nocProvisionalIssued",
      "action" : "differenceOfNumbers",
      "upwardIndicator" : "positive",
      "downwardIndicator" : "negative",
      "textMessage" : "$indicator$value% than last $insightInterval",
      "colorCode" : "#228B22",
      "insightInterval" : "year"
    },
    "_comment": "FIRE NOC Provisional Issued"
  },

  "nocActualIssued": {
    "chartName": "DSS_NOC_ACTUAL_ISSUED",
    "queries": [
      {
        "module": "FIRENOC",
        "indexName": "firenoc-services",
        "aggrQuery": "{\"aggs\":{\"FireNOC\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.tenantId.keyword\":\"pb.testing\"}}]}},\"aggs\":{\"Actual Fire Nocs issued\":{\"filter\":{\"bool\":{\"must\":[{\"term\":{\"Data.fireNOCDetails.fireNOCType.keyword\":\"NEW\"}}]}}}}}}}",
        "requestQueryMap": "{\"wardId\" : \"Data.ward.name.keyword\",\"tenantId\" : \"Data.tenantId\", \"district\" : \"Data.tenantData.city.districtCode\"}",
        "dateRefField": "Data.auditDetails.createdTime"
      }
    ],
    "chartType": "metric",
    "valueType": "number",
    "action": "",
    "drillChart": "none",
    "aggregationPaths": [
      "Actual Fire Nocs issued"
    ],
    "insight": {
      "chartResponseMap" : "nocActualIssued",
      "action" : "differenceOfNumbers",
      "upwardIndicator" : "positive",
      "downwardIndicator" : "negative",
      "textMessage" : "$indicator$value% than last $insightInterval",
      "colorCode" : "#228B22",
      "insightInterval" : "year"
    },
    "_comment": "Actual fire nocs Issued"
  },

  "nocAverageDaysToIssueProvisional": {
    "chartName": "DSS_NOC_AVERAGE_DAYS_TO_ISSUE_PROVISIONAL",
    "queries": [
      {
        "module": "FIRENOC",
        "indexName": "firenoc-services",
        "aggrQuery": "{\"aggs\":{\"FireNOC\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.tenantId.keyword\":\"pb.testing\"}}]}},\"aggs\":{\"Average days to issue Provisional NOC\":{\"filter\":{\"bool\":{\"must\":[{\"term\":{\"Data.fireNOCDetails.fireNOCType.keyword\":\"PROVISIONAL\"}},{\"term\":{\"Data.fireNOCDetails.status.keyword\":\"APPROVED\"}}]}},\"aggs\":{\"average_days\":{\"avg\":{\"script\":{\"source\":\"(doc['Data.auditDetails.lastModifiedTime'].value-doc['Data.auditDetails.createdTime'].value)\/(86400*1000)\"}}}}}}}}}",
        "requestQueryMap": "{\"wardId\" : \"Data.ward.name.keyword\",\"tenantId\" : \"Data.tenantId\", \"district\" : \"Data.tenantData.city.districtCode\"}",
        "dateRefField": "Data.auditDetails.createdTime"
      }
    ],
    "chartType": "metric",
    "valueType": "number",
    "action": "",
    "drillChart": "none",
    "aggregationPaths": [
      "Average days to issue Provisional NOC"
    ],
    "insight": {
      "chartResponseMap" : "nocAvgDayToIssueProvisional",
      "action" : "differenceOfNumbers",
      "upwardIndicator" : "positive",
      "downwardIndicator" : "negative",
      "textMessage" : "$indicator$value% than last $insightInterval",
      "colorCode" : "#228B22",
      "insightInterval" : "year"
    },
    "_comment": "FIRE Avg. days to issue Provisional"
  },

  "nocSLAComplianceProvisional": {
    "chartName": "DSS_NOC_SLA_COMPLIANCE_PROVISIONAL",
    "queries": [
      {
        "module": "FIRENOC",
        "indexName": "firenoc-services",
        "aggrQuery": "{\"aggs\":{\"FireNOC\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.tenantId.keyword\":\"pb.testing\"}}]}},\"aggs\":{\"SLA Compliance (Provisional NOC)\":{\"filter\":{\"bool\":{\"must\":[{\"term\":{\"Data.fireNOCDetails.fireNOCType.keyword\":\"PROVISIONAL\"}},{\"term\":{\"Data.fireNOCDetails.status.keyword\":\"APPROVED\"}},{\"script\":{\"script\":{\"source\":\"doc['Data.auditDetails.lastModifiedTime'].value-doc['Data.auditDetails.createdTime'].value<params.threshold\",\"lang\":\"painless\",\"params\":{\"threshold\":172800000}}}}]}}}}}}}",
        "requestQueryMap": "{\"wardId\" : \"Data.ward.name.keyword\",\"tenantId\" : \"Data.tenantId\", \"district\" : \"Data.tenantData.city.districtCode\"}",
        "dateRefField": "Data.auditDetails.createdTime"
      }
    ],
    "chartType": "metric",
    "valueType": "percentage",
    "action": "percentage",
    "drillChart": "none",
    "aggregationPaths": [
      "SLA Compliance (Provisional NOC)"
    ],
    "insight": {
      "chartResponseMap" : "slaCompliance",
      "action" : "differenceOfNumbers",
      "upwardIndicator" : "positive",
      "downwardIndicator" : "negative",
      "textMessage" : "$indicator$value% than last $insightInterval",
      "colorCode" : "#228B22",
      "insightInterval" : "year"
    },
    "_comment": "FIRE NOC SLA Compliance Provisional"
  },

  "nocAverageDaysToIssueActual": {
    "chartName": "DSS_NOC_AVERAGE_DAYS_TO_ISSUE_ACTUAL",
    "queries": [
      {
        "module": "FIRENOC",
        "indexName": "firenoc-services",
        "aggrQuery": "{\"aggs\":{\"FireNOC\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.tenantId.keyword\":\"pb.testing\"}}]}},\"aggs\":{\"Average days to issue Actual NOC\":{\"filter\":{\"bool\":{\"must\":[{\"term\":{\"Data.fireNOCDetails.fireNOCType.keyword\":\"NEW\"}},{\"term\":{\"Data.fireNOCDetails.status.keyword\":\"APPROVED\"}}]}},\"aggs\":{\"average_days\":{\"avg\":{\"script\":{\"source\":\"(doc['Data.auditDetails.lastModifiedTime'].value-doc['Data.auditDetails.createdTime'].value)\/(86400*1000)\"}}}}}}}}}",
        "requestQueryMap": "{\"wardId\" : \"Data.ward.name.keyword\",\"tenantId\" : \"Data.tenantId\", \"district\" : \"Data.tenantData.city.districtCode\"}",
        "dateRefField": "Data.auditDetails.createdTime"
      }
    ],
    "chartType": "metric",
    "valueType": "number",
    "action": "",
    "drillChart": "none",
    "aggregationPaths": [
      "Average days to issue Actual NOC"
    ],
    "insight": {
      "chartResponseMap" : "nocAvgDayToIssueActual",
      "action" : "differenceOfNumbers",
      "upwardIndicator" : "positive",
      "downwardIndicator" : "negative",
      "textMessage" : "$indicator$value% than last $insightInterval",
      "colorCode" : "#228B22",
      "insightInterval" : "year"
    },
    "_comment": "FIRE Avg. days to issue Actual"
  },

  "nocSLAComplianceActual": {
    "chartName": "DSS_NOC_SLA_COMPLIANCE_ACTUAL",
    "queries": [
      {
        "module": "FIRENOC",
        "indexName": "firenoc-services",
        "aggrQuery": "{\"aggs\":{\"FireNOC\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.tenantId.keyword\":\"pb.testing\"}}]}},\"aggs\":{\"SLA Compliance (Actual NOC)\":{\"filter\":{\"bool\":{\"must\":[{\"term\":{\"Data.fireNOCDetails.fireNOCType.keyword\":\"NEW\"}},{\"term\":{\"Data.fireNOCDetails.status.keyword\":\"APPROVED\"}},{\"script\":{\"script\":{\"source\":\"doc['Data.auditDetails.lastModifiedTime'].value-doc['Data.auditDetails.createdTime'].value<params.threshold\",\"lang\":\"painless\",\"params\":{\"threshold\":172800000}}}}]}}}}}}}",
        "requestQueryMap": "{\"wardId\" : \"Data.ward.name.keyword\",\"tenantId\" : \"Data.tenantId\", \"district\" : \"Data.tenantData.city.districtCode\"}",
        "dateRefField": "Data.auditDetails.createdTime"
      }
    ],
    "chartType": "metric",
    "valueType": "percentage",
    "action": "percentage",
    "drillChart": "none",
    "aggregationPaths": [
      "SLA Compliance (Actual NOC)"
    ],
    "insight": {
      "chartResponseMap" : "slaCompliance",
      "action" : "differenceOfNumbers",
      "upwardIndicator" : "positive",
      "downwardIndicator" : "negative",
      "textMessage" : "$indicator$value% than last $insightInterval",
      "colorCode" : "#228B22",
      "insightInterval" : "year"
    },
    "_comment": "FIRE NOC SLA Compliance Actual"
  },
  "nocCumulativeCollection": {
    "chartName": "DSS_NOC_TOTAL_CUMULATIVE_COLLECTION",
    "queries": [
      {
        "module": "FIRENOC",
        "dateRefField": "dataObject.paymentDetails.receiptDate",
        "requestQueryMap": "{\"wardId\" : \"domainObject.ward.name.keyword\",\r\n  \"module\" : \"dataObject.paymentDetails.businessService.keyword\", \n\"tenantId\" : \"dataObject.tenantId\"}",
        "indexName": "dss-collection_v2",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must\":[{\"terms\":{\"dataObject.paymentDetails.businessService.keyword\":[\"FIRENOC\"]}}],\"must_not\":[{\"term\":{\"dataObject.tenantId.keyword\":\"pb.testing\"}},{\"terms\":{\"dataObject.bill.status.keyword\":[\"Cancelled\"]}}]}},\"aggs\":{\"NOC Cumulative Collections\":{\"date_histogram\":{\"field\":\"dataObject.paymentDetails.receiptDate\",\"interval\":\"intervalvalue\"},\"aggs\":{\"Sum\":{\"sum\":{\"field\":\"dataObject.paymentDetails.totalAmountPaid\"}}}}}}}}"
      }
    ],
    "chartType": "line",
    "valueType": "amount",
    "action": "",
    "drillChart": "none",
    "documentType": "_doc",
    "aggregationPaths": [
      "NOC Cumulative Collections"
    ],
    "isCumulative": true,
    "interval": "month",
    "insight": {},
    "_comment": ""
  },

  "nocCollectionByPaymentMode": {
    "chartName": "DSS_NOC_COLLECTION_BY_PAYMENT_MODE",
    "queries": [
      {
        "module": "FIRENOC",
        "requestQueryMap": "{\"module\" : \"dataObject.paymentDetails.businessService.keyword\", \"tenantId\" : \"dataObject.tenantId\"}",
        "dateRefField": "dataObject.paymentDetails.receiptDate",
        "indexName": "dss-collection_v2",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must\":[{\"terms\":{\"dataObject.paymentDetails.businessService.keyword\":[\"FIRENOC\"]}}],\"must_not\":[{\"term\":{\"dataObject.tenantId.keyword\":\"pb.testing\"}},{\"terms\":{\"dataObject.bill.status.keyword\":[\"Cancelled\"]}}]}},\"aggs\":{\"NOC Payment Mode\":{\"terms\":{\"field\":\"dataObject.paymentMode.keyword\"},\"aggs\":{\"Total Collection\":{\"sum\":{\"field\":\"dataObject.paymentDetails.totalAmountPaid\"}}}}}}}}"
      }
    ],
    "chartType": "pie",
    "valueType": "amount",
    "action": "",
    "documentType": "_doc",
    "drillChart": "none",
    "aggregationPaths": [
      "NOC Payment Mode"
    ],
    "insight": {},
    "_comment": ""
  },
  "nocActualTopPerformingUlbs": {
    "chartName": "DSS_NOC_ACTUAL_TOP_3_PERFORMING_ULBS",
    "queries": [
      {
        "module": "FIRENOC",
        "requestQueryMap": "{\"wardId\" : \"Data.ward.name.keyword\",\"tenantId\" : \"Data.tenantId\" \r\n}",
        "dateRefField": "Data.auditDetails.createdTime",
        "indexName": "firenoc-services",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.tenantId.keyword\":\"pb.testing\"}}]}},\"aggs\":{\"Total NOCs issued\":{\"terms\":{\"field\":\"Data.tenantId.keyword\",\"size\":\"200\",\"order\":{\"NOCs\":\"desc\"}},\"aggs\":{\"NOCs\":{\"value_count\":{\"field\":\"Data.tenantId.keyword\"}}}}}}}}"
      },
      {
        "module": "FIRENOC",
        "requestQueryMap": "{\"wardId\" : \"Data.ward.name.keyword\",\"tenantId\" : \"Data.tenantId\" \r\n}",
        "dateRefField": "Data.auditDetails.createdTime",
        "indexName": "firenoc-services",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.tenantId.keyword\":\"pb.testing\"}}],\"must\":[{\"term\":{\"Data.fireNOCDetails.fireNOCType.keyword\":\"NEW\"}}]}},\"aggs\":{\"Actual NOCs issued\":{\"terms\":{\"field\":\"Data.tenantId.keyword\",\"size\":\"200\",\"order\":{\"NOCs\":\"desc\"}},\"aggs\":{\"NOCs\":{\"value_count\":{\"field\":\"Data.tenantId.keyword\"}}}}}}}}"
      }
    ],
    "chartType": "perform",
    "valueType": "percentage",
    "drillChart": "none",
    "documentType": "_doc",
    "action": "percentage",
    "plotLabel": "Actual",
    "order": "desc",
    "limit": 3,
    "aggregationPaths": [
      "Actual NOCs issued",
      "Total NOCs issued"
    ],
    "insight": {
    },
    "_comment": "Top Performing Ulbs for actual nocs issued"
  },

  "nocProvisionalTopPerformingUlbs": {
    "chartName": "DSS_NOC_PROVISIONAL_TOP_3_PERFORMING_ULBS",
    "queries": [
      {
        "module": "FIRENOC",
        "requestQueryMap": "{\"wardId\" : \"Data.ward.name.keyword\",\"tenantId\" : \"Data.tenantId\" \r\n}",
        "dateRefField": "Data.auditDetails.createdTime",
        "indexName": "firenoc-services",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.tenantId.keyword\":\"pb.testing\"}}]}},\"aggs\":{\"Total NOCs issued\":{\"terms\":{\"field\":\"Data.tenantId.keyword\",\"size\":\"200\",\"order\":{\"NOCs\":\"desc\"}},\"aggs\":{\"NOCs\":{\"value_count\":{\"field\":\"Data.tenantId.keyword\"}}}}}}}}"
      },
      {
        "module": "FIRENOC",
        "requestQueryMap": "{\"wardId\" : \"Data.ward.name.keyword\",\"tenantId\" : \"Data.tenantId\" \r\n}",
        "dateRefField": "Data.auditDetails.createdTime",
        "indexName": "firenoc-services",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.tenantId.keyword\":\"pb.testing\"}}],\"must\":[{\"term\":{\"Data.fireNOCDetails.fireNOCType.keyword\":\"PROVISIONAL\"}}]}},\"aggs\":{\"Provisional NOCs issued\":{\"terms\":{\"field\":\"Data.tenantId.keyword\",\"size\":\"200\",\"order\":{\"NOCs\":\"desc\"}},\"aggs\":{\"NOCs\":{\"value_count\":{\"field\":\"Data.tenantId.keyword\"}}}}}}}}"
      }
    ],
    "chartType": "perform",
    "valueType": "percentage",
    "drillChart": "none",
    "documentType": "_doc",
    "action": "percentage",
    "plotLabel": "Provisional",
    "order": "desc",
    "limit": 3,
    "aggregationPaths": [
      "Provisional NOCs issued",
      "Total NOCs issued"
    ],
    "insight": {
    },
    "_comment": "Top Performing Ulbs for provisional nocs issued"
  },

  "nocActualBottomPerformingUlbs": {
    "chartName": "DSS_NOC_ACTUAL_BOTTOM_3_PERFORMING_ULBS",
    "queries": [
      {
        "module": "FIRENOC",
        "requestQueryMap": "{\"wardId\" : \"Data.ward.name.keyword\",\"tenantId\" : \"Data.tenantId\" \r\n}",
        "dateRefField": "Data.auditDetails.createdTime",
        "indexName": "firenoc-services",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.tenantId.keyword\":\"pb.testing\"}}]}},\"aggs\":{\"Total NOCs issued\":{\"terms\":{\"field\":\"Data.tenantId.keyword\",\"size\":\"200\",\"order\":{\"NOCs\":\"asc\"}},\"aggs\":{\"NOCs\":{\"value_count\":{\"field\":\"Data.tenantId.keyword\"}}}}}}}}"
      },
      {
        "module": "FIRENOC",
        "requestQueryMap": "{\"wardId\" : \"Data.ward.name.keyword\",\"tenantId\" : \"Data.tenantId\" \r\n}",
        "dateRefField": "Data.auditDetails.createdTime",
        "indexName": "firenoc-services",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.tenantId.keyword\":\"pb.testing\"}}],\"must\":[{\"term\":{\"Data.fireNOCDetails.fireNOCType.keyword\":\"NEW\"}}]}},\"aggs\":{\"Actual NOCs issued\":{\"terms\":{\"field\":\"Data.tenantId.keyword\",\"size\":\"200\",\"order\":{\"NOCs\":\"asc\"}},\"aggs\":{\"NOCs\":{\"value_count\":{\"field\":\"Data.tenantId.keyword\"}}}}}}}}"
      }
    ],
    "chartType": "perform",
    "valueType": "percentage",
    "drillChart": "none",
    "documentType": "_doc",
    "action": "percentage",
    "plotLabel": "Actual",
    "order": "asc",
    "limit": 3,
    "aggregationPaths": [
      "Actual NOCs issued",
      "Total NOCs issued"
    ],
    "insight": {
    },
    "_comment": "Bottom Performing Ulbs for actual nocs issued"
  },

  "nocProvisionalBottomPerformingUlbs": {
    "chartName": "DSS_NOC_PROVISIONAL_BOTTOM_3_PERFORMING_ULBS",
    "queries": [
      {
        "module": "FIRENOC",
        "requestQueryMap": "{\"wardId\" : \"Data.ward.name.keyword\",\"tenantId\" : \"Data.tenantId\" \r\n}",
        "dateRefField": "Data.auditDetails.createdTime",
        "indexName": "firenoc-services",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.tenantId.keyword\":\"pb.testing\"}}]}},\"aggs\":{\"Total NOCs issued\":{\"terms\":{\"field\":\"Data.tenantId.keyword\",\"size\":\"200\",\"order\":{\"NOCs\":\"asc\"}},\"aggs\":{\"NOCs\":{\"value_count\":{\"field\":\"Data.tenantId.keyword\"}}}}}}}}"
      },
      {
        "module": "FIRENOC",
        "requestQueryMap": "{\"wardId\" : \"Data.ward.name.keyword\",\"tenantId\" : \"Data.tenantId\" \r\n}",
        "dateRefField": "Data.auditDetails.createdTime",
        "indexName": "firenoc-services",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.tenantId.keyword\":\"pb.testing\"}}],\"must\":[{\"term\":{\"Data.fireNOCDetails.fireNOCType.keyword\":\"PROVISIONAL\"}}]}},\"aggs\":{\"Provisional NOCs issued\":{\"terms\":{\"field\":\"Data.tenantId.keyword\",\"size\":\"200\",\"order\":{\"NOCs\":\"asc\"}},\"aggs\":{\"NOCs\":{\"value_count\":{\"field\":\"Data.tenantId.keyword\"}}}}}}}}"
      }
    ],
    "chartType": "perform",
    "valueType": "percentage",
    "drillChart": "none",
    "documentType": "_doc",
    "action": "percentage",
    "plotLabel": "Provisional",
    "order": "asc",
    "limit": 3,
    "aggregationPaths": [
      "Provisional NOCs issued",
      "Total NOCs issued"
    ],
    "insight": {
    },
    "_comment": "Bottom Performing Ulbs for provisional nocs issued"
  },
   "totalNocIssuedByType": {
    "chartName": "DSS_TOTAL_NOC_ISSUED_TYPE",
    "queries": [
      {
        "module": "FIRENOC",
        "indexName": "firenoc-services",
       "aggrQuery": "{\"aggs\":{\"FireNOC\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.tenantId.keyword\":\"pb.testing\"}}]}},\"aggs\": {\"fireNOC Issued\": {\"terms\": {\"field\": \"Data.fireNOCDetails.fireNOCType.keyword\"},\"aggs\": {\"total_nocs_by_type\": {\"cardinality\": {\"field\": \"_id\"}}}}}}}}",
        "requestQueryMap": "{\"wardId\" : \"Data.ward.name.keyword\",\"tenantId\" : \"Data.tenantId\" \r\n}",
        "dateRefField": "Data.auditDetails.createdTime"
      }
    ],
    "chartType": "pie",
    "valueType": "number",
    "action": "",
    "documentType": "_doc",
    "drillChart": "none",
    "aggregationPaths": [
      "fireNOC Issued"
    ],
    "insight": {
    },
    "_comment": "Total NOCs issued by Type"
  },
  "actualNocIssuedByUsageType": {
    "chartName": "DSS_ACTUAL_NOC_ISSUED_USAGETYPE",
    "queries": [
      {
        "module": "FIRENOC",
        "indexName": "firenoc-services",
        "aggrQuery": "{\"aggs\":{\"FireNOC\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.tenantId.keyword\":\"pb.testing\"}}],\"must\":[{\"term\":{\"Data.fireNOCDetails.fireNOCType.keyword\":\"NEW\"}}]}},\"aggs\":{\"actualNOC Issued\":{\"terms\":{\"field\":\"Data.fireNOCDetails.buildings.usageType.keyword\"},\"aggs\":{\"actual_nocs_by_usagetype\":{\"cardinality\":{\"field\":\"_id\"}}}}}}}}",
        "requestQueryMap": "{\"wardId\" : \"Data.ward.name.keyword\",\"tenantId\" : \"Data.tenantId\" \r\n}",
        "dateRefField": "Data.auditDetails.createdTime"
      }
    ],
    "chartType": "pie",
    "valueType": "number",
    "action": "",
    "documentType": "_doc",
    "drillChart": "none",
    "aggregationPaths": [
      "actualNOC Issued"
    ],
    "insight": {
    },
    "_comment": "Actual NOCs Issued by usageType."
  },
  
  
  "nocServiceReportByRegion": {
    "chartName": "DSS_NOC_SERVICE_REPORT_REGION",
    "queries": [
      {
        "module": "COMMON",
        "requestQueryMap": "{\"wardId\" : \"dataObject.ward.name.keyword\",\"module\" : \"dataObject.paymentDetails.businessService.keyword\",\"tenantId\" : \"dataObject.tenantId\", \"district\" : \"dataObject.tenantData.city.districtCode\" }",
		"dateRefField": "dataObject.paymentDetails.receiptDate",
        "indexName": "dss-collection_v2",
        "aggrQuery": "{\"aggs\":{\"FireNOC\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"dataObject.tenantId.keyword\":\"pb.testing\"}},{\"terms\":{\"dataObject.bill.status.keyword\":[\"Cancelled\"]}}],\"must\":[{\"terms\":{\"dataObject.paymentDetails.businessService.keyword\":[\"FIRENOC\"]}}]}},\"aggs\":{\"firenoc_Total_Collection\":{\"sum\":{\"field\":\"dataObject.paymentDetails.totalAmountPaid\"}}}}}}"
      },
      {
        "module": "COMMON",
        "requestQueryMap": "{\"wardId\" : \"Data.ward.name.keyword\",\"tenantId\" : \"Data.tenantId\", \"district\" : \"Data.tenantData.city.districtCode\"}",
        "dateRefField": "Data.auditDetails.createdTime",
        "indexName": "firenoc-services",
        "aggrQuery": "{\"aggs\":{\"FireNOC\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.tenantId.keyword\":\"pb.testing\"}}]}},\"aggs\":{\"Total_Applications\":{\"value_count\":{\"field\":\"Data.tenantId.keyword\"}},\"Provisional_Fire_Nocs_issued\":{\"filter\":{\"bool\":{\"must\":[{\"term\":{\"Data.fireNOCDetails.fireNOCType.keyword\":\"PROVISIONAL\"}}]}}},\"Actual_Fire_Nocs_issued\":{\"filter\":{\"bool\":{\"must\":[{\"term\":{\"Data.fireNOCDetails.fireNOCType.keyword\":\"NEW\"}}]}}},\"Average_days_to_issue_Provisional_NOC\":{\"filter\":{\"bool\":{\"must\":[{\"term\":{\"Data.fireNOCDetails.fireNOCType.keyword\":\"PROVISIONAL\"}},{\"term\":{\"Data.fireNOCDetails.status.keyword\":\"APPROVED\"}}]}},\"aggs\":{\"average_days\":{\"avg\":{\"script\":{\"source\":\"(doc['Data.auditDetails.lastModifiedTime'].value-doc['Data.auditDetails.createdTime'].value)\/(86400*1000)\"}}}}},\"Average_days_to_issue_Actual_NOC\":{\"filter\":{\"bool\":{\"must\":[{\"term\":{\"Data.fireNOCDetails.fireNOCType.keyword\":\"NEW\"}},{\"term\":{\"Data.fireNOCDetails.status.keyword\":\"APPROVED\"}}]}},\"aggs\":{\"average_days\":{\"avg\":{\"script\":{\"source\":\"(doc['Data.auditDetails.lastModifiedTime'].value-doc['Data.auditDetails.createdTime'].value)\/(86400*1000)\"}}}}},\"SLA_Compliance(Actual_NOC)\":{\"filter\":{\"bool\":{\"must\":[{\"term\":{\"Data.fireNOCDetails.fireNOCType.keyword\":\"NEW\"}},{\"term\":{\"Data.fireNOCDetails.status.keyword\":\"APPROVED\"}},{\"script\":{\"script\":{\"source\":\"doc['Data.auditDetails.lastModifiedTime'].value-doc['Data.auditDetails.createdTime'].value<params.threshold\",\"lang\":\"painless\",\"params\":{\"threshold\":172800000}}}}]}}},\"SLA_Compliance(Provisional_NOC)\":{\"filter\":{\"bool\":{\"must\":[{\"term\":{\"Data.fireNOCDetails.fireNOCType.keyword\":\"PROVISIONAL\"}},{\"term\":{\"Data.fireNOCDetails.status.keyword\":\"APPROVED\"}},{\"script\":{\"script\":{\"source\":\"doc['Data.auditDetails.lastModifiedTime'].value-doc['Data.auditDetails.createdTime'].value<params.threshold\",\"lang\":\"painless\",\"params\":{\"threshold\":172800000}}}}]}}}}}}}"
      }
    ],
    "isMdmsEnabled": true,
    "filterKeys": [
      {"key": "tenantId", "column": "Region"}
    ],
    "chartType": "xtable",
    "valueType": "number",
    "action": "",
    "plotLabel": "Region",
    "isPostResponseHandler": true,
    "postAggregationTheory" : "repsonseToDifferenceOfDates",
    "documentType": "_doc",
    "drillChart": "nocServiceReportDrillDown",
    "aggregationPaths": [
      "firenoc_Total_Collection",
      "Total_Applications",
      "Provisional_Fire_Nocs_issued",
      "Actual_Fire_Nocs_issued",
      "Average_days_to_issue_Provisional_NOC",
      "SLA_Compliance(Provisional_NOC)",
      "Average_days_to_issue_Actual_NOC",
      "SLA_Compliance(Actual_NOC)"
    ],
    "pathDataTypeMapping": [
      {
        "firenoc_Total_Collection": "amount"
      },
      {
        "Total_Applications": "number"
      },
      {
        "Provisional_Fire_Nocs_issued": "number"
      },
      {
        "Actual_Fire_Nocs_issued": "number"
      },
      {
        "Average_days_to_issue_Provisional_NOC": "number"
      },
      {
        "SLA_Compliance(Provisional_NOC)": "number"
      },
      {
        "Average_days_to_issue_Actual_NOC": "number"
      },
      {
        "SLA_Compliance(Actual_NOC)": "number"
      }
    ],
    "insight": {
    },
    "_comment": ""
  },
  
  "nocServiceReportDrillDown": {
    "chartName": "DSS_NOC_SERVICE_REPORT_BOUNDRY",
    "queries": [
      {
        "module": "COMMON",
        "requestQueryMap": "{\"wardId\" : \"dataObject.ward.name.keyword\",\"module\" : \"dataObject.paymentDetails.businessService.keyword\",\"tenantId\" : \"dataObject.tenantId\", \"ulbId\" : \"dataObject.tenantId\", \"district\" : \"dataObject.tenantData.city.districtCode\" }",
		    "dateRefField": "dataObject.paymentDetails.receiptDate",
        "indexName": "dss-collection_v2",
        "aggrQuery": "{\"aggs\":{\"FireNOC\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"dataObject.tenantId.keyword\":\"pb.testing\"}},{\"terms\":{\"dataObject.bill.status.keyword\":[\"Cancelled\"]}}],\"must\":[{\"terms\":{\"dataObject.paymentDetails.businessService.keyword\":[\"FIRENOC\"]}}]}},\"aggs\":{\"ULBs\":{\"terms\":{\"field\":\"dataObject.tenantId.keyword\",\"size\":1000},\"aggs\":{\"firenoc_Total_Collection\":{\"sum\":{\"field\":\"dataObject.paymentDetails.totalAmountPaid\"}}}}}}}}"
      },
      {
        "module": "COMMON",
        "requestQueryMap": "{\"wardId\" : \"Data.ward.name.keyword\",\"tenantId\" : \"Data.tenantId\", \"ulbId\" : \"Data.tenantId\", \"district\" : \"Data.tenantData.city.districtCode\"}",
        "dateRefField": "Data.auditDetails.createdTime",
        "indexName": "firenoc-services",
        "aggrQuery": "{\"aggs\":{\"FireNOC\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.tenantId.keyword\":\"pb.testing\"}}]}},\"aggs\":{\"ULBs\":{\"terms\":{\"field\":\"Data.tenantId.keyword\",\"size\":1000},\"aggs\":{\"Total_Applications\":{\"value_count\":{\"field\":\"Data.tenantId.keyword\"}},\"Provisional_Fire_Nocs_issued\":{\"filter\":{\"bool\":{\"must\":[{\"term\":{\"Data.fireNOCDetails.fireNOCType.keyword\":\"PROVISIONAL\"}}]}}},\"Actual_Fire_Nocs_issued\":{\"filter\":{\"bool\":{\"must\":[{\"term\":{\"Data.fireNOCDetails.fireNOCType.keyword\":\"NEW\"}}]}}},\"Average_days_to_issue_Provisional_NOC\":{\"filter\":{\"bool\":{\"must\":[{\"term\":{\"Data.fireNOCDetails.fireNOCType.keyword\":\"PROVISIONAL\"}},{\"term\":{\"Data.fireNOCDetails.status.keyword\":\"APPROVED\"}}]}},\"aggs\":{\"average_days\":{\"avg\":{\"script\":{\"source\":\"(doc['Data.auditDetails.lastModifiedTime'].value-doc['Data.auditDetails.createdTime'].value)\/(86400*1000)\"}}}}},\"Average_days_to_issue_Actual_NOC\":{\"filter\":{\"bool\":{\"must\":[{\"term\":{\"Data.fireNOCDetails.fireNOCType.keyword\":\"NEW\"}},{\"term\":{\"Data.fireNOCDetails.status.keyword\":\"APPROVED\"}}]}},\"aggs\":{\"average_days\":{\"avg\":{\"script\":{\"source\":\"(doc['Data.auditDetails.lastModifiedTime'].value-doc['Data.auditDetails.createdTime'].value)\/(86400*1000)\"}}}}},\"SLA_Compliance(Actual_NOC)\":{\"filter\":{\"bool\":{\"must\":[{\"term\":{\"Data.fireNOCDetails.fireNOCType.keyword\":\"NEW\"}},{\"term\":{\"Data.fireNOCDetails.status.keyword\":\"APPROVED\"}},{\"script\":{\"script\":{\"source\":\"doc['Data.auditDetails.lastModifiedTime'].value-doc['Data.auditDetails.createdTime'].value<params.threshold\",\"lang\":\"painless\",\"params\":{\"threshold\":172800000}}}}]}}},\"SLA_Compliance(Provisional_NOC)\":{\"filter\":{\"bool\":{\"must\":[{\"term\":{\"Data.fireNOCDetails.fireNOCType.keyword\":\"PROVISIONAL\"}},{\"term\":{\"Data.fireNOCDetails.status.keyword\":\"APPROVED\"}},{\"script\":{\"script\":{\"source\":\"doc['Data.auditDetails.lastModifiedTime'].value-doc['Data.auditDetails.createdTime'].value<params.threshold\",\"lang\":\"painless\",\"params\":{\"threshold\":172800000}}}}]}}}}}}}}}"
      }
    ],
    "filterKeys": [
      {"key": "tenantId", "column": "ULBs"}
    ],
    "chartType": "xtable",
    "valueType": "number",
    "drillChart": "nocServiceReportBoundaryDrillDown",
    "documentType": "_doc",
    "action": "",
    "plotLabel": "ULBs",
    "postAggregationTheory" : "repsonseToDifferenceOfDates",
    "aggregationPaths": [
      "firenoc_Total_Collection",
      "Total_Applications",
      "Provisional_Fire_Nocs_issued",
      "Actual_Fire_Nocs_issued",
      "Average_days_to_issue_Provisional_NOC",
      "SLA_Compliance(Provisional_NOC)",
      "Average_days_to_issue_Actual_NOC",
      "SLA_Compliance(Actual_NOC)"
    ],
    "pathDataTypeMapping": [
      {
        "firenoc_Total_Collection": "amount"
      },
      {
        "Total_Applications": "number"
      },
      {
        "Provisional_Fire_Nocs_issued": "number"
      },
      {
        "Actual_Fire_Nocs_issued": "number"
      },
      {
        "Average_days_to_issue_Provisional_NOC": "number"
      },
      {
        "SLA_Compliance(Provisional_NOC)": "number"
      },
      {
        "Average_days_to_issue_Actual_NOC": "number"
      },
      {
        "SLA_Compliance(Actual_NOC)": "number"
      }
    ],
    "insight": {
    },
    "_comment": " "
  },
  
   "nocServiceReportBoundaryDrillDown": {
    "kind": "drillDown",
    "chartName": "Boundary",
    "queries": [
    {
        "module": "COMMON",
        "requestQueryMap": "{\"wardId\" : \"domainObject.ward.name.keyword\",\"module\" : \"dataObject.paymentDetails.businessService.keyword\",\"tenantId\" : \"dataObject.tenantId\", \"ulbId\" : \"dataObject.tenantId\", \"district\" : \"dataObject.tenantData.city.districtCode\" }",
		"dateRefField": "dataObject.paymentDetails.receiptDate",
        "indexName": "dss-collection_v2",
        "aggrQuery": "{\"aggs\":{\"FireNOC\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"dataObject.tenantId.keyword\":\"pb.testing\"}},{\"terms\":{\"dataObject.bill.status.keyword\":[\"Cancelled\"]}}],\"must\":[{\"terms\":{\"dataObject.paymentDetails.businessService.keyword\":[\"FIRENOC\"]}}]}},\"aggs\":{\"Ward \":{\"terms\":{\"field\":\"domainObject.ward.name.keyword\",\"size\":200},\"aggs\":{\"firenoc_Total_Collection\":{\"sum\":{\"field\":\"dataObject.paymentDetails.totalAmountPaid\"}}}}}}}}"
      },
      {
        "module": "COMMON",
        "requestQueryMap": "{\"wardId\" : \"Data.ward.name.keyword\",\"tenantId\" : \"Data.tenantId\", \"ulbId\" : \"Data.tenantId\", \"district\" : \"Data.tenantData.city.districtCode\"}",
        "dateRefField": "Data.auditDetails.createdTime",
        "indexName": "firenoc-services",
        "aggrQuery": "{\"aggs\":{\"FireNOC\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.tenantId.keyword\":\"pb.testing\"}}]}},\"aggs\":{\"Ward \":{\"terms\":{\"field\":\"Data.ward.name.keyword\",\"size\":200},\"aggs\":{\"Total_Applications\":{\"value_count\":{\"field\":\"Data.tenantId.keyword\"}},\"Provisional_Fire_Nocs_issued\":{\"filter\":{\"bool\":{\"must\":[{\"term\":{\"Data.fireNOCDetails.fireNOCType.keyword\":\"PROVISIONAL\"}}]}}},\"Actual_Fire_Nocs_issued\":{\"filter\":{\"bool\":{\"must\":[{\"term\":{\"Data.fireNOCDetails.fireNOCType.keyword\":\"NEW\"}}]}}},\"Average_days_to_issue_Provisional_NOC\":{\"filter\":{\"bool\":{\"must\":[{\"term\":{\"Data.fireNOCDetails.fireNOCType.keyword\":\"PROVISIONAL\"}},{\"term\":{\"Data.fireNOCDetails.status.keyword\":\"APPROVED\"}}]}},\"aggs\":{\"average_days\":{\"avg\":{\"script\":{\"source\":\"(doc['Data.auditDetails.lastModifiedTime'].value-doc['Data.auditDetails.createdTime'].value)\/(86400*1000)\"}}}}},\"Average_days_to_issue_Actual_NOC\":{\"filter\":{\"bool\":{\"must\":[{\"term\":{\"Data.fireNOCDetails.fireNOCType.keyword\":\"NEW\"}},{\"term\":{\"Data.fireNOCDetails.status.keyword\":\"APPROVED\"}}]}},\"aggs\":{\"average_days\":{\"avg\":{\"script\":{\"source\":\"(doc['Data.auditDetails.lastModifiedTime'].value-doc['Data.auditDetails.createdTime'].value)\/(86400*1000)\"}}}}},\"SLA_Compliance(Actual_NOC)\":{\"filter\":{\"bool\":{\"must\":[{\"term\":{\"Data.fireNOCDetails.fireNOCType.keyword\":\"NEW\"}},{\"term\":{\"Data.fireNOCDetails.status.keyword\":\"APPROVED\"}},{\"script\":{\"script\":{\"source\":\"doc['Data.auditDetails.lastModifiedTime'].value-doc['Data.auditDetails.createdTime'].value<params.threshold\",\"lang\":\"painless\",\"params\":{\"threshold\":172800000}}}}]}}},\"SLA_Compliance(Provisional_NOC)\":{\"filter\":{\"bool\":{\"must\":[{\"term\":{\"Data.fireNOCDetails.fireNOCType.keyword\":\"PROVISIONAL\"}},{\"term\":{\"Data.fireNOCDetails.status.keyword\":\"APPROVED\"}},{\"script\":{\"script\":{\"source\":\"doc['Data.auditDetails.lastModifiedTime'].value-doc['Data.auditDetails.createdTime'].value<params.threshold\",\"lang\":\"painless\",\"params\":{\"threshold\":172800000}}}}]}}}}}}}}}"
      }
    ],
    "filterKeys": [
      {"key": "wardId", "column": "Ward"},
      {"key": "ulbId", "column": "ULB"}
    ],
    "chartType": "table",
    "valueType": "number",
    "drillChart": "none",
    "documentType": "_doc",
    "action": "",
    "plotLabel": "Ward",
    "aggregationPaths": [
      "firenoc_Total_Collection",
      "Total_Applications",
      "Provisional_Fire_Nocs_issued",
      "Actual_Fire_Nocs_issued",
      "Average_days_to_issue_Provisional_NOC",
      "SLA_Compliance(Provisional_NOC)",
      "Average_days_to_issue_Actual_NOC",
      "SLA_Compliance(Actual_NOC)"
    ],
    "pathDataTypeMapping": [
      {
        "firenoc_Total_Collection": "amount"
      },
      {
        "Total_Applications": "number"
      },
      {
        "Provisional_Fire_Nocs_issued": "number"
      },
      {
        "Actual_Fire_Nocs_issued": "number"
      },
      {
        "Average_days_to_issue_Provisional_NOC": "number"
      },
      {
        "SLA_Compliance(Provisional_NOC)": "number"
      },
      {
        "Average_days_to_issue_Actual_NOC": "number"
      },
      {
        "SLA_Compliance(Actual_NOC)": "number"
      }
    ],
    "insight": {
    },
    "_comment": " "
  },
  
  "nocServiceReportByDepartment": {
    "chartName": "DSS_NOC_SERVICE_REPORT_DEPARTMENT",
    "queries": [
      {
        "module": "COMMON",
        "requestQueryMap": "{\"wardId\" : \"dataObject.ward.name.keyword\", \"tenantId\" : \"dataObject.tenantId.keyword\"}",
        "dateRefField": "dataObject.paymentDetails.receiptDate",
        "indexName": "dss-collection_v2",
        "aggrQuery": "{\"aggs\":{\"FireNOC\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"dataObject.tenantId.keyword\":\"pb.testing\"}},{\"terms\":{\"dataObject.bill.status.keyword\":[\"Cancelled\"]}}],\"must\":[{\"terms\":{\"dataObject.paymentDetails.businessService.keyword\":[\"FIRENOC\"]}}]}},\"aggs\":{\"Department\":{\"terms\":{\"field\":\"domainObject.Department.keyword\",\"size\":1000},\"aggs\":{\"firenoc_Total_Collection\":{\"sum\":{\"field\":\"dataObject.paymentDetails.totalAmountPaid\"}}}}}}}}"
      },
      {
        "module": "COMMON",
        "requestQueryMap": "{\"wardId\" : \"Data.ward.name.keyword\",\"tenantId\" : \"Data.tenantId.keyword\"}",
        "indexName": "firenoc-services",
        "dateRefField": "Data.auditDetails.createdTime",
        "aggrQuery": "{\"aggs\":{\"FireNOC\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.tenantId.keyword\":\"pb.testing\"}}]}},\"aggs\":{\"Department\":{\"terms\":{\"field\":\"Data.Department.keyword\",\"size\":1000},\"aggs\":{\"Total_Applications\":{\"value_count\":{\"field\":\"Data.tenantId.keyword\"}},\"Provisional_Fire_Nocs_issued\":{\"filter\":{\"bool\":{\"must\":[{\"term\":{\"Data.fireNOCDetails.fireNOCType.keyword\":\"PROVISIONAL\"}}]}}},\"Actual_Fire_Nocs_issued\":{\"filter\":{\"bool\":{\"must\":[{\"term\":{\"Data.fireNOCDetails.fireNOCType.keyword\":\"NEW\"}}]}}},\"Average_days_to_issue_Provisional_NOC\":{\"filter\":{\"bool\":{\"must\":[{\"term\":{\"Data.fireNOCDetails.fireNOCType.keyword\":\"PROVISIONAL\"}},{\"term\":{\"Data.fireNOCDetails.status.keyword\":\"APPROVED\"}}]}},\"aggs\":{\"average_days\":{\"avg\":{\"script\":{\"source\":\"(doc['Data.auditDetails.lastModifiedTime'].value-doc['Data.auditDetails.createdTime'].value)\/(86400*1000)\"}}}}},\"Average_days_to_issue_Actual_NOC\":{\"filter\":{\"bool\":{\"must\":[{\"term\":{\"Data.fireNOCDetails.fireNOCType.keyword\":\"NEW\"}},{\"term\":{\"Data.fireNOCDetails.status.keyword\":\"APPROVED\"}}]}},\"aggs\":{\"average_days\":{\"avg\":{\"script\":{\"source\":\"(doc['Data.auditDetails.lastModifiedTime'].value-doc['Data.auditDetails.createdTime'].value)\/(86400*1000)\"}}}}},\"SLA_Compliance(Actual_NOC)\":{\"filter\":{\"bool\":{\"must\":[{\"term\":{\"Data.fireNOCDetails.fireNOCType.keyword\":\"NEW\"}},{\"term\":{\"Data.fireNOCDetails.status.keyword\":\"APPROVED\"}},{\"script\":{\"script\":{\"source\":\"doc['Data.auditDetails.lastModifiedTime'].value-doc['Data.auditDetails.createdTime'].value<params.threshold\",\"lang\":\"painless\",\"params\":{\"threshold\":172800000}}}}]}}},\"SLA_Compliance(Provisional_NOC)\":{\"filter\":{\"bool\":{\"must\":[{\"term\":{\"Data.fireNOCDetails.fireNOCType.keyword\":\"PROVISIONAL\"}},{\"term\":{\"Data.fireNOCDetails.status.keyword\":\"APPROVED\"}},{\"script\":{\"script\":{\"source\":\"doc['Data.auditDetails.lastModifiedTime'].value-doc['Data.auditDetails.createdTime'].value<params.threshold\",\"lang\":\"painless\",\"params\":{\"threshold\":172800000}}}}]}}}}}}}}}"
      }
    ],
    "filterKeys": [
      {"key": "tenantId", "column": "Department"}
    ],
    "chartType": "table",
    "valueType": "number",
    "drillChart": "none",
    "documentType": "_doc",
    "plotLabel": "firenoc_Department",
    "aggregationPaths": [
      "firenoc_Total_Collection",
      "Total_Applications",
      "Provisional_Fire_Nocs_issued",
      "Actual_Fire_Nocs_issued",
      "Average_days_to_issue_Provisional_NOC",
      "SLA_Compliance(Provisional_NOC)",
      "Average_days_to_issue_Actual_NOC",
      "SLA_Compliance(Actual_NOC)"
    ],
    "pathDataTypeMapping": [
      {
        "firenoc_Total_Collection": "amount"
      },
      {
        "Total_Applications": "number"
      },
      {
        "Provisional_Fire_Nocs_issued": "number"
      },
      {
        "Actual_Fire_Nocs_issued": "number"
      },
      {
        "Average_days_to_issue_Provisional_NOC": "number"
      },
      {
        "SLA_Compliance(Provisional_NOC)": "number"
      },
      {
        "Average_days_to_issue_Actual_NOC": "number"
      },
      {
        "SLA_Compliance(Actual_NOC)": "number"
      }
    ],
    "insight": {
    },
    "_comment": ""
  },
```

[Click here to check the complete configuration](https://github.com/egovernments/configs/blob/qa/egov-dss-dashboards/dashboard-analytics/ChartApiConfig.json)

### **Master Dashboard Configuration**

Master Dashboard Configuration is the main configuration which defines the dashboards to be painted on the screen.&#x20;

It includes all the visualizations, their groups, the charts which come within them and even their dimensions as what should be their height and width.

```
 {
      "name": "DSS_FIRE_NOC_DASHBOARD",
      "id": "noc",
      "isActive": "",
      "style": "linear",
      "visualizations": [
        {
          "row": 1,
          "name": "DSS_OVERVIEW",
          "vizArray": [
            {
              "id": 341,
              "name": "DSS_NOC_REVENUE",
              "dimensions": {
                "height": 400,
                "width": 5
              },
              "vizType": "metric-collection",
              "label": "DSS_NOC_REVENUE",
              "noUnit": true,
              "isCollapsible": false,
              "charts": [
                {
                  "id": "nocTodaysCollection",
                  "name": "DSS_NOC_TODAYS_COLLECTION",
                  "code": "",
                  "chartType": "metric",
                  "filter": {
                    "title": "TODAY"
                  },
                  "headers": []
                },
                {
                  "id": "nocTotalCollection",
                  "name": "DSS_NOC_TOTAL_COLLECTION",
                  "code": "",
                  "chartType": "metric",
                  "filter": "",
                  "headers": []
                }
              ]
            },
            {
              "id": 342,
              "name": "DSS_NOC_TOTAL_CUMULATIVE_COLLECTION",
              "dimensions": {
                "height": 190,
                "width": 7
              },
              "vizType": "chart",
              "label": "",
              "noUnit": true,
              "isCollapsible": false,
              "charts": [
                {
                  "id": "nocCumulativeCollection",
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
          "name": "DSS_OVERVIEW",
          "vizArray": [
            {
              "id": 341,
              "name": "DSS_NOC_OVERVIEW",
              "dimensions": {
                "height": 400,
                "width": 5
              },
              "vizType": "metric-collection",
              "label": "DSS_NOC_OVERVIEW",
              "noUnit": true,
              "isCollapsible": false,
              "charts": [
                {
                  "id": "nocTotalApplications",
                  "name": "DSS_NOC_TOTAL_APPLICATIONS",
                  "code": "",
                  "chartType": "metric",
                  "filter": "",
                  "headers": []
                },
                {
                  "id": "nocProvisionalIssued",
                  "name": "DSS_NOC_PROVISIONAL_ISSUED",
                  "code": "",
                  "chartType": "metric",
                  "filter": "",
                  "headers": []
                },
                {
                  "id": "nocActualIssued",
                  "name": "DSS_NOC_ACTUAL_ISSUED",
                  "code": "",
                  "chartType": "metric",
                  "filter": "",
                  "headers": []
                },
                {
                  "id": "nocSLAComplianceProvisional",
                  "name": "DSS_NOC_SLA_COMPLIANCE_PROVISIONAL",
                  "code": "",
                  "chartType": "metric",
                  "filter": "",
                  "headers": []
                },
                {
                  "id": "nocSLAComplianceActual",
                  "name": "DSS_NOC_SLA_COMPLIANCE_ACTUAL",
                  "code": "",
                  "chartType": "metric",
                  "filter": "",
                  "headers": []
                }
              ]
            },
            {
              "id": 343,
              "name": "DSS_APPLICATION_VS_PROVISIONAL_VS_ACTUAL",
              "dimensions": {
                "height": 190,
                "width": 7
              },
              "vizType": "chart",
              "isCollapsible": false,
              "label": "",
              "charts": [
                {
                  "id": "nocApplicationVsProvisionalVsActual",
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
          "row": 3,
          "name": "DSS_OVERVIEW",
          "vizArray": [
           {
              "id": 210,
              "name": "DSS_NOC_COLLECTION_BY_PAYMENT_MODE",
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
                  "id": "nocCollectionByPaymentMode",
                  "name": "DSS_NOC_COLLECTION_BY_PAYMENT_MODE",
                  "code": "",
                  "chartType": "donut",
                  "filter": "",
                  "headers": []
                }
              ]
            },
            {
              "id": 211,
              "name": "DSS_TOTAL_NOC_ISSUED_TYPE",
              "dimensions": {
                "height": 250,
                "width": 4
              },
              "vizType": "chart",
              "noUnit": false,
              "isCollapsible": false,
              "charts": [
                {
                  "id": "totalNocIssuedByType",
                  "name": "DSS_TOTAL_NOC_ISSUED_TYPE",
                  "code": "",
                  "chartType": "donut",
                  "filter": "",
                  "headers": []
                }
              ]
           },
           {
              "id": 212,
              "name": "DSS_ACTUAL_NOC_ISSUED_USAGETYPE",
              "dimensions": {
                "height": 250,
                "width": 4
              },
              "vizType": "chart",
              "noUnit": false,
              "isCollapsible": false,
              "charts": [
                {
                  "id": "actualNocIssuedByUsageType",
                  "name": "DSS_ACTUAL_NOC_ISSUED_USAGETYPE",
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
          "name": "DSS_OVERVIEW",
          "vizArray": [
            {
              "id": 321,
              "name": "DSS_NOC_TOP_3_PERFORMING_ULBS",
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
                  "id": "nocActualTopPerformingUlbs",
                  "name": "DSS_NOC_ACTUAL_TOP_3_PERFORMING_ULBS",
                  "code": "",
                  "chartType": "bar",
                  "filter": "",
                  "headers": [],
                  "tabName":"Actual"
                },
                {
                  "id": "nocProvisionalTopPerformingUlbs",
                  "name": "DSS_NOC_PROVISIONAL_TOP_3_PERFORMING_ULBS",
                  "code": "",
                  "chartType": "bar",
                  "filter": "",
                  "headers": [],
                  "tabName":"Provisional"
                }
              ]
            },
            {
              "id": 322,
              "name": "DSS_NOC_BOTTOM_3_PERFORMING_ULBS",
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
                  "id": "nocActualBottomPerformingUlbs",
                  "name": "DSS_NOC_ACTUAL_BOTTOM_3_PERFORMING_ULBS",
                  "code": "",
                  "chartType": "bar",
                  "filter": "",
                  "headers": [],
                  "tabName":"Actual"
                },
                {
                  "id": "nocProvisionalBottomPerformingUlbs",
                  "name": "DSS_NOC_PROVISIONAL_BOTTOM_3_PERFORMING_ULBS",
                  "code": "",
                  "chartType": "bar",
                  "filter": "",
                  "headers": [],
                  "tabName":"Provisional"
                }                
              ]
            }
          ]
        },
        {
          "row": 5,
          "name": "DSS_OVERVIEW",
          "vizArray": [
            {
              "id": 231,
              "name": "Service Report",
              "dimensions": {
                "height": 350,
                "width": 12
              },
              "vizType": "chart",
              "noUnit": false,
              "isCollapsible": false,
              "charts": [
                {
                  "id": "nocServiceReportByRegion",
                  "name": "DSS_NOC_SERVICE_REPORT_REGION",
                  "code": "",
                  "chartType": "table",
                  "filter": "",
                  "headers": [],
                  "tabName": "Region"
                },
                {
                  "id": "nocServiceReportByDepartment",
                  "name": "DSS_NOC_SERVICE_REPORT_DEPARTMENT",
                  "code": "",
                  "chartType": "table",
                  "filter": "",
                  "headers": [],
                  "tabName": "Department"
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

Master Dashboard Configuration which was explained earlier holds the list of dashboards which are available.

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
          "name": "Fire Noc",
          "id": "noc"
        }
      ]
    }

  ]
}
```

[Click here to check the configuration](https://github.com/egovernments/configs/blob/qa/egov-dss-dashboards/dashboard-analytics/RoleDashboardMappingsConf.json)

&#x20;**MDMS Configuration to be added:**_common-masters/uiCommonConstants.json_

```
"State-firenoc":{
                  "routePath":"/dashboard/noc",
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
    },  
     {
      "rolecode": "UC_EMP",
      "actionid": {{PlaceHolder2}},
      "actioncode": "",
      "tenantId": "pb"
    },
```

[Click here to check the complete configuration](https://github.com/egovernments/egov-mdms-data/blob/QA/data/pb/ACCESSCONTROL-ROLEACTIONS/roleactions.json)

Action test.json:&#x20;

```
{
      "id": {{PlaceHolder1}},
      "name": "DSS Dashboard Config noc",
      "url": "/dashboard-analytics/dashboard/getDashboardConfig/noc",
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
      "url": "url",
      "displayName": "Firenoc",
      "orderNumber": 4,
      "parentModule": "dss-dashboard",
      "enabled": true,
      "serviceCode": "DSS",
      "code": "null",
      "path": "Dashboard.Firenoc",
      "navigationURL": "/digit-ui/employee/dss/dashboard/noc",
      "leftIcon": "places:business-center",
      "rightIcon": ""
}
```

[Click here to check the complete configuration](https://github.com/egovernments/egov-mdms-data/blob/QA/data/pb/ACCESSCONTROL-ACTIONS-TEST/actions-test.json)

FireNoc-State DSS Consists of multiple graphs which represent the data of FireNoc. Each graph has its own configuration which will describe the chart and its type.

State DSS consists of following charts in FireNoc:

**FireNoc Page**

* Overview
* Total Cumulative Collection
* Total applications vs Provisional NOCs issued vs Actual NOCs issued
* Collection by Payment Mode
* Total NOCs issued by type
* Actual Fire NOCs by usage type
* Top 3 Performing States
* Bottom 3 Performing States
* Service Report

**Overview**

The overview graph contains multiple data information as below in the selected time period.

* **Today’s Collection:** This represents the sum of revenue collected from the issuance of a Provisional and Actual Fire NOC which is Application fee + NOC Issuance fee.
* &#x20;**Total Collection:** Sum of revenue collected from Fire NOC for the applied date filter.
* **Total Applications:** Total number of applications submitted for a new FireNOC.
* **Provisional NOCs Issued:** The Provisional NOC is to be obtained to ensure that the proposed constructions meet the fire safety-compliant norms.
* **Actual NOCs Issued:** The Actual NOC is to be obtained to ensure that the proposed constructions meet the fire safety compliant norms.
* **Avg. days to issue Provisional Fire NOC:** Average number of days taken to issue a Provisional NOC.
* **Avg. days to issue Actual Fire NOC:** Average number of days taken to issue an Actual NOC.
* **SLA Compliance (Actual FIre NOC):** % of Actual NOCs issued within SLA.
* **SLA Compliance (Provisional FIre NOC):** % of Provisional NOCs issued within SLA.

![](<../../../../.gitbook/assets/image (10).png>)

**Total Cumulative Collection**

This Graph contains the Fire NOC collection amount information on a monthly basis as a cumulative line graph for each Fire NOC collection separately. This will change as per the denomination amount filter selection.

**line** - this graph/chart is data representation on date histograms or date groupings.

![](<../../../../.gitbook/assets/image (15).png>)

**Total applications vs Provisional NOCs issued vs Actual NOCs issued**

This Graph contains the Fire NOC showing total applications submitted vs provisional NOCs issued vs actual NOCs issued for a given month collection separately. This will change as per the denomination amount filter selection.

**line** - this graph/chart is data representation on date histograms or date groupings.

![](<../../../../.gitbook/assets/image (5) (3).png>)

**Collection by Payment Mode:** This will be a pie chart showing the bifurcation of total collections by payment mode (online, cash, card, cheque) which is the sum of revenue collected from Fire NOC for the applied date filter.

![](<../../../../.gitbook/assets/image (6).png>)

**Total NOCs issued by type:** This will be a pie chart showing the bifurcation of Total NOCs issued into Provisional and Actual Fire NOCs. Sum of Provisional and Actual Fire NOCs issued.

![](<../../../../.gitbook/assets/image (12).png>)

**Actual Fire NOCs by usage type:** This will be a pie chart showing a bifurcation of Actual Fire NOCs by usage type. The total number of Fire NOCs issued by the concerned authority.

![](<../../../../.gitbook/assets/image (14).png>)

**Top 3 Performing States:** This card will show the Top 3 Performing States/ULBs/Wards based on % NOCs issued. The number of Fire NOCs issued / Number of applications depends on whether a user selects 'Provisional' or 'Actual'.

On click of Actual it shows the % of NOCs issued for Actual FireNocs.

![](<../../../../.gitbook/assets/image (7).png>)

On click of Provisional it shows the % of NOCs issued for Actual FireNocs.

![](<../../../../.gitbook/assets/image (1) (5).png>)

On click of Show More, it shows the information of all the states.

<figure><img src="../../../../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

**Bottom 3 Performing States:** This card will show the Bottom 3 Performing States/ULBs/Wards based on % NOCs issued. The number of Fire NOCs issued / Number of applications depends on whether a user selects 'Provisional' or 'Actual'.

On click of Actual it shows the % of NOCs issued for Actual FireNocs.

![](<../../../../.gitbook/assets/image (3) (3).png>)

On click of Provisional it shows the % of NOCs issued for Actual FireNocs.

![](<../../../../.gitbook/assets/image (9).png>)

On click of Show More, it shows the information of all the states.

<figure><img src="../../../../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

**Service Report:** This tabular chart representation graph shows multiple Fire NOC information like Total Collection, Applications Submitted, Provisional FireNoc issued, New FireNOC Issued, Average days to issue Provisional NOC, SLA Compliance (Provisional NOC), Average days to issue New NOC, SLA Compliance (New NOC). And this table shows the data at the state level and also has the drill-down chart for each state to ULB and from ULB to ward level data for the same.

xtable type allows the addition of multiple computed fields with the aggregated fields dynamically added.

To add multiple computed columns,  computedFields \[]  where actionName (IComputedField\<T> interface), fields \[] names as in exist in query key, newField as name to appear for computation must be defined.

<figure><img src="../../../../.gitbook/assets/image (13) (3).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/image (1) (5) (1).png" alt=""><figcaption></figcaption></figure>

Clicking on any region name provides a drill down to the specific state data.

<figure><img src="../../../../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

Clicking on the ULB navigates to the wards under that specific ULB and each ward shows the specific data for that ward.

<figure><img src="../../../../.gitbook/assets/image (2) (5).png" alt=""><figcaption></figcaption></figure>

## **Newly Introduced Property** <a href="#newly-introduced-property" id="newly-introduced-property"></a>

**isRoundOff**: This property is introduced to round off the decimal values. Ex: if the value is 25.43 by using isRoundOff property in the configuration we will get it as 25. if the value is 22.56 round of value will be 23.\
This can be used for insights configuration as well for overview graphs.

## Common Properties Available <a href="#common-properties-available" id="common-properties-available"></a>

**Key(eg: fsmTotalrequest):** This is the Visualization Code. This key will be referred to in further visualization configurations.

This is the key which will be used by the client application to indicate which visualization is needed for display.

**chartName:** The name of the Chart which has to be used as a label on the Dashboard. The name of the Chart will be a detailed name.

In this configuration, the Name of the Chart will be the code of Localization which will be used by the Client Side.

**queries:** Some visualizations are derived from a specific data source. While some others are derived from different data sources and are combined together to get a meaningful representation.

The queries of aggregation which are to be used to fetch the right data in the right aggregated format are configured here.

**queries.module:** The module/domain level, on which the query should be applied on. Fire NOC is FIRENOC.

**queries.indexName:** The name of the index upon which the query has to be executed is configured here.

**queries.aggrQuery:** The aggregation query in itself is added here. Based on the Module and the Index name specified, this query is attached to the filter part of the complete search request and then executed against that index

**queries.requestQueryMap:** Client Request would carry certain fields which are to be filtered. The parameters specified in the Client Request are different from the parameters in each of these indexed documents.

In order to map the parameters of the request to the parameters of the ElasticSearch Document, this mapping is maintained.

**queries.dateRefField:** Each of these modules have separate indexes. And all of them have their own date fields.&#x20;

When there is a date filter applied against these visualizations, each of them has to apply it against their own date reference fields.

In order to maintain what is the date field in which index, we have this configured in this configuration parameter.

**chartType:** As there are different types of visualizations, this field defines what is the type of chart/visualization that this data should be used to represent.&#x20;

## **Available Chart Types**&#x20;

**metric** - this represents the aggregated amount/value for records filtered by the aggregate query&#x20;

**pie** - this represents the aggregated data on grouping. This is can be used to represent any line graph, bar graph, pie chart or donuts

**line** - this graph/chart is data representation on date histograms or date groupings

**perform** - this chart represents groping data performance-wise.

**table** - represents a form of plots and values with headers as grouped on and a list of its key, values pairs.&#x20;

**xtable -** represents an advanced feature of the table, it has addition capabilities for dynamic adding header values.

**valueType :** Instance of data, the values which are sent for plotting, might be a percentage, sometimes an amount and sometimes it is just a count.

In order to represent them and differentiate the numbers from the amount from the percentage, this field is used to indicate the type of value that this Visualization will be sending.

**action:** Some of the visualizations are not just aggregations of data sources. There might be some cases where we have to do a post-aggregation computation.

For Example, in the case of the Top 3 Performing ULBs, the Target and Total Collection are obtained and then the percentage is calculated. In these kinds of cases, the action that has to be performed on the data obtained is defined in this parameter.&#x20;

**documentType:** The type of document upon which the query has to be executed is defined here.&#x20;

**drillChart:** If there is a drill down on the visualization, then the code of the Drill Down Visualization is added here. This will be used by Client Service to manage drill-downs.

**aggregationPaths:** All the queries will be having Aggregation names in them. In order to fetch the value out of each Aggregation Response, the name of the aggregation in the query will be an easy bet. These aggregation paths will have the names of Aggregation in them.

**insights:** It is to show the data with the comparison of last year with arrow symbols, it will show the data in how much % is increased or decreased.&#x20;

**\_comment:** In order to display information on the “i” symbol of each visualization, Visualization Information is maintained in this field.&#x20;

## **Index Properties**  <a href="#index-properties-of-state-firenoc-dss" id="index-properties-of-state-firenoc-dss"></a>

The index that contains data for State-FireNoc is- _firenoc-services_

The mapping for this index is:

```
"properties" : {
          "Data" : {
            "properties" : {
              "@timestamp" : {
                "type" : "date"
              },
              "Department" : {
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
              "channel" : {
                "type" : "text",
                "fields" : {
                  "keyword" : {
                    "type" : "keyword",
                    "ignore_above" : 256
                  }
                }
              },
              "fireNOCDetails" : {
                "properties" : {
                  "action" : {
                    "type" : "text",
                    "fields" : {
                      "keyword" : {
                        "type" : "keyword",
                        "ignore_above" : 256
                      }
                    }
                  },
                  "additionalDetail" : {
                    "properties" : {
                      "assignee" : {
                        "type" : "text",
                        "fields" : {
                          "keyword" : {
                            "type" : "keyword",
                            "ignore_above" : 256
                          }
                        }
                      },
                      "comment" : {
                        "type" : "text",
                        "fields" : {
                          "keyword" : {
                            "type" : "keyword",
                            "ignore_above" : 256
                          }
                        }
                      },
                      "documents" : {
                        "properties" : {
                          "documentType" : {
                            "type" : "text",
                            "fields" : {
                              "keyword" : {
                                "type" : "keyword",
                                "ignore_above" : 256
                              }
                            }
                          },
                          "fileStoreId" : {
                            "type" : "text",
                            "fields" : {
                              "keyword" : {
                                "type" : "keyword",
                                "ignore_above" : 256
                              }
                            }
                          },
                          "link" : {
                            "type" : "text",
                            "fields" : {
                              "keyword" : {
                                "type" : "keyword",
                                "ignore_above" : 256
                              }
                            }
                          },
                          "linkText" : {
                            "type" : "text",
                            "fields" : {
                              "keyword" : {
                                "type" : "keyword",
                                "ignore_above" : 256
                              }
                            }
                          },
                          "name" : {
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
                          "title" : {
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
                      "ownerAuditionalDetail" : {
                        "properties" : {
                          "documents" : {
                            "properties" : {
                              "documentType" : {
                                "type" : "text",
                                "fields" : {
                                  "keyword" : {
                                    "type" : "keyword",
                                    "ignore_above" : 256
                                  }
                                }
                              },
                              "fileStoreId" : {
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
                          "institutionDesignation" : {
                            "type" : "text",
                            "fields" : {
                              "keyword" : {
                                "type" : "keyword",
                                "ignore_above" : 256
                              }
                            }
                          },
                          "institutionName" : {
                            "type" : "text",
                            "fields" : {
                              "keyword" : {
                                "type" : "keyword",
                                "ignore_above" : 256
                              }
                            }
                          },
                          "telephoneNumber" : {
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
                      "wfDocuments" : {
                        "properties" : {
                          "documentType" : {
                            "type" : "text",
                            "fields" : {
                              "keyword" : {
                                "type" : "keyword",
                                "ignore_above" : 256
                              }
                            }
                          },
                          "fileName" : {
                            "type" : "text",
                            "fields" : {
                              "keyword" : {
                                "type" : "keyword",
                                "ignore_above" : 256
                              }
                            }
                          },
                          "fileStoreId" : {
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
                  },
                  "applicantDetails" : {
                    "properties" : {
                      "additionalDetail" : {
                        "properties" : {
                          "documents" : {
                            "properties" : {
                              "documentType" : {
                                "type" : "text",
                                "fields" : {
                                  "keyword" : {
                                    "type" : "keyword",
                                    "ignore_above" : 256
                                  }
                                }
                              },
                              "fileStoreId" : {
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
                          "institutionDesignation" : {
                            "type" : "text",
                            "fields" : {
                              "keyword" : {
                                "type" : "keyword",
                                "ignore_above" : 256
                              }
                            }
                          },
                          "institutionName" : {
                            "type" : "text",
                            "fields" : {
                              "keyword" : {
                                "type" : "keyword",
                                "ignore_above" : 256
                              }
                            }
                          },
                          "telephoneNumber" : {
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
                      "ownerShipMajorType" : {
                        "type" : "text",
                        "fields" : {
                          "keyword" : {
                            "type" : "keyword",
                            "ignore_above" : 256
                          }
                        }
                      },
                      "ownerShipType" : {
                        "type" : "text",
                        "fields" : {
                          "keyword" : {
                            "type" : "keyword",
                            "ignore_above" : 256
                          }
                        }
                      },
                      "owners" : {
                        "properties" : {
                          "accountLocked" : {
                            "type" : "boolean"
                          },
                          "accountLockedDate" : {
                            "type" : "long"
                          },
                          "active" : {
                            "type" : "boolean"
                          },
                          "altContactNumber" : {
                            "type" : "text",
                            "fields" : {
                              "keyword" : {
                                "type" : "keyword",
                                "ignore_above" : 256
                              }
                            }
                          },
                          "correspondenceAddress" : {
                            "type" : "text",
                            "fields" : {
                              "keyword" : {
                                "type" : "keyword",
                                "ignore_above" : 256
                              }
                            }
                          },
                          "createdBy" : {
                            "type" : "long"
                          },
                          "createdDate" : {
                            "type" : "long"
                          },
                          "dob" : {
                            "type" : "long"
                          },
                          "emailId" : {
                            "type" : "text",
                            "fields" : {
                              "keyword" : {
                                "type" : "keyword",
                                "ignore_above" : 256
                              }
                            }
                          },
                          "fatherOrHusbandName" : {
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
                            "type" : "long"
                          },
                          "lastModifiedBy" : {
                            "type" : "long"
                          },
                          "lastModifiedDate" : {
                            "type" : "long"
                          },
                          "locale" : {
                            "type" : "text",
                            "fields" : {
                              "keyword" : {
                                "type" : "keyword",
                                "ignore_above" : 256
                              }
                            }
                          },
                          "mobileNumber" : {
                            "type" : "text",
                            "fields" : {
                              "keyword" : {
                                "type" : "keyword",
                                "ignore_above" : 256
                              }
                            }
                          },
                          "name" : {
                            "type" : "text",
                            "fields" : {
                              "keyword" : {
                                "type" : "keyword",
                                "ignore_above" : 256
                              }
                            }
                          },
                          "ownerType" : {
                            "type" : "text",
                            "fields" : {
                              "keyword" : {
                                "type" : "keyword",
                                "ignore_above" : 256
                              }
                            }
                          },
                          "ownerUUID" : {
                            "type" : "text",
                            "fields" : {
                              "keyword" : {
                                "type" : "keyword",
                                "ignore_above" : 256
                              }
                            }
                          },
                          "permanentAddress" : {
                            "type" : "text",
                            "fields" : {
                              "keyword" : {
                                "type" : "keyword",
                                "ignore_above" : 256
                              }
                            }
                          },
                          "permanentCity" : {
                            "type" : "text",
                            "fields" : {
                              "keyword" : {
                                "type" : "keyword",
                                "ignore_above" : 256
                              }
                            }
                          },
                          "permanentPinCode" : {
                            "type" : "text",
                            "fields" : {
                              "keyword" : {
                                "type" : "keyword",
                                "ignore_above" : 256
                              }
                            }
                          },
                          "pwdExpiryDate" : {
                            "type" : "long"
                          },
                          "relationship" : {
                            "type" : "text",
                            "fields" : {
                              "keyword" : {
                                "type" : "keyword",
                                "ignore_above" : 256
                              }
                            }
                          },
                          "roles" : {
                            "properties" : {
                              "code" : {
                                "type" : "text",
                                "fields" : {
                                  "keyword" : {
                                    "type" : "keyword",
                                    "ignore_above" : 256
                                  }
                                }
                              },
                              "name" : {
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
                          "type" : {
                            "type" : "text",
                            "fields" : {
                              "keyword" : {
                                "type" : "keyword",
                                "ignore_above" : 256
                              }
                            }
                          },
                          "userName" : {
                            "type" : "text",
                            "fields" : {
                              "keyword" : {
                                "type" : "keyword",
                                "ignore_above" : 256
                              }
                            }
                          },
                          "useruuid" : {
                            "type" : "text",
                            "fields" : {
                              "keyword" : {
                                "type" : "keyword",
                                "ignore_above" : 256
                              }
                            }
                          },
                          "uuid" : {
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
                  },
                  "applicationNumber" : {
                    "type" : "text",
                    "fields" : {
                      "keyword" : {
                        "type" : "keyword",
                        "ignore_above" : 256
                      }
                    }
                  },
                  "buildings" : {
                    "properties" : {
                      "applicationDocuments" : {
                        "properties" : {
                          "documentType" : {
                            "type" : "text",
                            "fields" : {
                              "keyword" : {
                                "type" : "keyword",
                                "ignore_above" : 256
                              }
                            }
                          },
                          "fileStoreId" : {
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
                          "tenantId" : {
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
                      "id" : {
                        "type" : "text",
                        "fields" : {
                          "keyword" : {
                            "type" : "keyword",
                            "ignore_above" : 256
                          }
                        }
                      },
                      "name" : {
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
                      "uoms" : {
                        "properties" : {
                          "active" : {
                            "type" : "boolean"
                          },
                          "code" : {
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
                          "isActiveUom" : {
                            "type" : "boolean"
                          },
                          "value" : {
                            "type" : "long"
                          }
                        }
                      },
                      "uomsMap" : {
                        "properties" : {
                          "BUILTUP_AREA" : {
                            "type" : "text",
                            "fields" : {
                              "keyword" : {
                                "type" : "keyword",
                                "ignore_above" : 256
                              }
                            }
                          },
                          "HEIGHT_OF_BUILDING" : {
                            "type" : "text",
                            "fields" : {
                              "keyword" : {
                                "type" : "keyword",
                                "ignore_above" : 256
                              }
                            }
                          },
                          "NO_OF_BASEMENTS" : {
                            "type" : "text",
                            "fields" : {
                              "keyword" : {
                                "type" : "keyword",
                                "ignore_above" : 256
                              }
                            }
                          },
                          "NO_OF_FLOORS" : {
                            "type" : "text",
                            "fields" : {
                              "keyword" : {
                                "type" : "keyword",
                                "ignore_above" : 256
                              }
                            }
                          },
                          "PLOT_SIZE" : {
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
                      "usageType" : {
                        "type" : "text",
                        "fields" : {
                          "keyword" : {
                            "type" : "keyword",
                            "ignore_above" : 256
                          }
                        }
                      },
                      "usageTypeMajor" : {
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
                  "fireNOCType" : {
                    "type" : "text",
                    "fields" : {
                      "keyword" : {
                        "type" : "keyword",
                        "ignore_above" : 256
                      }
                    }
                  },
                  "firestationId" : {
                    "type" : "text",
                    "fields" : {
                      "keyword" : {
                        "type" : "keyword",
                        "ignore_above" : 256
                      }
                    }
                  },
                  "propertyDetails" : {
                    "properties" : {
                      "address" : {
                        "properties" : {
                          "buildingName" : {
                            "type" : "text",
                            "fields" : {
                              "keyword" : {
                                "type" : "keyword",
                                "ignore_above" : 256
                              }
                            }
                          },
                          "city" : {
                            "type" : "text",
                            "fields" : {
                              "keyword" : {
                                "type" : "keyword",
                                "ignore_above" : 256
                              }
                            }
                          },
                          "doorNo" : {
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
                          "locality" : {
                            "properties" : {
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
                          "pincode" : {
                            "type" : "text",
                            "fields" : {
                              "keyword" : {
                                "type" : "keyword",
                                "ignore_above" : 256
                              }
                            }
                          },
                          "street" : {
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
                      "propertyId" : {
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
                  "status" : {
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
              "history" : {
                "properties" : {
                  "action" : {
                    "type" : "text",
                    "fields" : {
                      "keyword" : {
                        "type" : "keyword",
                        "ignore_above" : 256
                      }
                    }
                  },
                  "assigner" : {
                    "properties" : {
                      "emailId" : {
                        "type" : "text",
                        "fields" : {
                          "keyword" : {
                            "type" : "keyword",
                            "ignore_above" : 256
                          }
                        }
                      },
                      "id" : {
                        "type" : "long"
                      },
                      "mobileNumber" : {
                        "type" : "text",
                        "fields" : {
                          "keyword" : {
                            "type" : "keyword",
                            "ignore_above" : 256
                          }
                        }
                      },
                      "name" : {
                        "type" : "text",
                        "fields" : {
                          "keyword" : {
                            "type" : "keyword",
                            "ignore_above" : 256
                          }
                        }
                      },
                      "roles" : {
                        "properties" : {
                          "code" : {
                            "type" : "text",
                            "fields" : {
                              "keyword" : {
                                "type" : "keyword",
                                "ignore_above" : 256
                              }
                            }
                          },
                          "name" : {
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
                      "type" : {
                        "type" : "text",
                        "fields" : {
                          "keyword" : {
                            "type" : "keyword",
                            "ignore_above" : 256
                          }
                        }
                      },
                      "userName" : {
                        "type" : "text",
                        "fields" : {
                          "keyword" : {
                            "type" : "keyword",
                            "ignore_above" : 256
                          }
                        }
                      },
                      "uuid" : {
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
                  "assignes" : {
                    "properties" : {
                      "emailId" : {
                        "type" : "text",
                        "fields" : {
                          "keyword" : {
                            "type" : "keyword",
                            "ignore_above" : 256
                          }
                        }
                      },
                      "id" : {
                        "type" : "long"
                      },
                      "mobileNumber" : {
                        "type" : "text",
                        "fields" : {
                          "keyword" : {
                            "type" : "keyword",
                            "ignore_above" : 256
                          }
                        }
                      },
                      "name" : {
                        "type" : "text",
                        "fields" : {
                          "keyword" : {
                            "type" : "keyword",
                            "ignore_above" : 256
                          }
                        }
                      },
                      "roles" : {
                        "properties" : {
                          "code" : {
                            "type" : "text",
                            "fields" : {
                              "keyword" : {
                                "type" : "keyword",
                                "ignore_above" : 256
                              }
                            }
                          },
                          "name" : {
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
                      "type" : {
                        "type" : "text",
                        "fields" : {
                          "keyword" : {
                            "type" : "keyword",
                            "ignore_above" : 256
                          }
                        }
                      },
                      "userName" : {
                        "type" : "text",
                        "fields" : {
                          "keyword" : {
                            "type" : "keyword",
                            "ignore_above" : 256
                          }
                        }
                      },
                      "uuid" : {
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
                  "businessId" : {
                    "type" : "text",
                    "fields" : {
                      "keyword" : {
                        "type" : "keyword",
                        "ignore_above" : 256
                      }
                    }
                  },
                  "businessService" : {
                    "type" : "text",
                    "fields" : {
                      "keyword" : {
                        "type" : "keyword",
                        "ignore_above" : 256
                      }
                    }
                  },
                  "businesssServiceSla" : {
                    "type" : "long"
                  },
                  "comment" : {
                    "type" : "text",
                    "fields" : {
                      "keyword" : {
                        "type" : "keyword",
                        "ignore_above" : 256
                      }
                    }
                  },
                  "documents" : {
                    "properties" : {
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
                      "documentType" : {
                        "type" : "text",
                        "fields" : {
                          "keyword" : {
                            "type" : "keyword",
                            "ignore_above" : 256
                          }
                        }
                      },
                      "fileStoreId" : {
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
                      "tenantId" : {
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
                  "escalated" : {
                    "type" : "boolean"
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
                  "moduleName" : {
                    "type" : "text",
                    "fields" : {
                      "keyword" : {
                        "type" : "keyword",
                        "ignore_above" : 256
                      }
                    }
                  },
                  "rating" : {
                    "type" : "long"
                  },
                  "state" : {
                    "properties" : {
                      "actions" : {
                        "properties" : {
                          "action" : {
                            "type" : "text",
                            "fields" : {
                              "keyword" : {
                                "type" : "keyword",
                                "ignore_above" : 256
                              }
                            }
                          },
                          "currentState" : {
                            "type" : "text",
                            "fields" : {
                              "keyword" : {
                                "type" : "keyword",
                                "ignore_above" : 256
                              }
                            }
                          },
                          "nextState" : {
                            "type" : "text",
                            "fields" : {
                              "keyword" : {
                                "type" : "keyword",
                                "ignore_above" : 256
                              }
                            }
                          },
                          "roles" : {
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
                          "uuid" : {
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
                      "businessServiceId" : {
                        "type" : "text",
                        "fields" : {
                          "keyword" : {
                            "type" : "keyword",
                            "ignore_above" : 256
                          }
                        }
                      },
                      "docUploadRequired" : {
                        "type" : "boolean"
                      },
                      "isStartState" : {
                        "type" : "boolean"
                      },
                      "isTerminateState" : {
                        "type" : "boolean"
                      },
                      "sla" : {
                        "type" : "long"
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
                      "uuid" : {
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
                  "stateSla" : {
                    "type" : "long"
                  },
                  "tenantId" : {
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
              "id" : {
                "type" : "text",
                "fields" : {
                  "keyword" : {
                    "type" : "keyword",
                    "ignore_above" : 256
                  }
                }
              },
              "tenantData" : {
                "properties" : {
                  "OfficeTimings" : {
                    "properties" : {
                      "Mon - Fri" : {
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
                  "address" : {
                    "type" : "text",
                    "fields" : {
                      "keyword" : {
                        "type" : "keyword",
                        "ignore_above" : 256
                      }
                    }
                  },
                  "city" : {
                    "properties" : {
                      "code" : {
                        "type" : "text",
                        "fields" : {
                          "keyword" : {
                            "type" : "keyword",
                            "ignore_above" : 256
                          }
                        }
                      },
                      "ddrName" : {
                        "type" : "text",
                        "fields" : {
                          "keyword" : {
                            "type" : "keyword",
                            "ignore_above" : 256
                          }
                        }
                      },
                      "districtCode" : {
                        "type" : "text",
                        "fields" : {
                          "keyword" : {
                            "type" : "keyword",
                            "ignore_above" : 256
                          }
                        }
                      },
                      "districtName" : {
                        "type" : "text",
                        "fields" : {
                          "keyword" : {
                            "type" : "keyword",
                            "ignore_above" : 256
                          }
                        }
                      },
                      "districtTenantCode" : {
                        "type" : "text",
                        "fields" : {
                          "keyword" : {
                            "type" : "keyword",
                            "ignore_above" : 256
                          }
                        }
                      },
                      "latitude" : {
                        "type" : "float"
                      },
                      "localName" : {
                        "type" : "text",
                        "fields" : {
                          "keyword" : {
                            "type" : "keyword",
                            "ignore_above" : 256
                          }
                        }
                      },
                      "longitude" : {
                        "type" : "float"
                      },
                      "municipalityName" : {
                        "type" : "text",
                        "fields" : {
                          "keyword" : {
                            "type" : "keyword",
                            "ignore_above" : 256
                          }
                        }
                      },
                      "name" : {
                        "type" : "text",
                        "fields" : {
                          "keyword" : {
                            "type" : "keyword",
                            "ignore_above" : 256
                          }
                        }
                      },
                      "regionCode" : {
                        "type" : "text",
                        "fields" : {
                          "keyword" : {
                            "type" : "keyword",
                            "ignore_above" : 256
                          }
                        }
                      },
                      "regionName" : {
                        "type" : "text",
                        "fields" : {
                          "keyword" : {
                            "type" : "keyword",
                            "ignore_above" : 256
                          }
                        }
                      },
                      "ulbGrade" : {
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
                  "code" : {
                    "type" : "text",
                    "fields" : {
                      "keyword" : {
                        "type" : "keyword",
                        "ignore_above" : 256
                      }
                    }
                  },
                  "contactNumber" : {
                    "type" : "text",
                    "fields" : {
                      "keyword" : {
                        "type" : "keyword",
                        "ignore_above" : 256
                      }
                    }
                  },
                  "description" : {
                    "type" : "text",
                    "fields" : {
                      "keyword" : {
                        "type" : "keyword",
                        "ignore_above" : 256
                      }
                    }
                  },
                  "domainUrl" : {
                    "type" : "text",
                    "fields" : {
                      "keyword" : {
                        "type" : "keyword",
                        "ignore_above" : 256
                      }
                    }
                  },
                  "emailId" : {
                    "type" : "text",
                    "fields" : {
                      "keyword" : {
                        "type" : "keyword",
                        "ignore_above" : 256
                      }
                    }
                  },
                  "facebookUrl" : {
                    "type" : "text",
                    "fields" : {
                      "keyword" : {
                        "type" : "keyword",
                        "ignore_above" : 256
                      }
                    }
                  },
                  "imageId" : {
                    "type" : "text",
                    "fields" : {
                      "keyword" : {
                        "type" : "keyword",
                        "ignore_above" : 256
                      }
                    }
                  },
                  "logoId" : {
                    "type" : "text",
                    "fields" : {
                      "keyword" : {
                        "type" : "keyword",
                        "ignore_above" : 256
                      }
                    }
                  },
                  "name" : {
                    "type" : "text",
                    "fields" : {
                      "keyword" : {
                        "type" : "keyword",
                        "ignore_above" : 256
                      }
                    }
                  },
                  "pincode" : {
                    "type" : "long"
                  },
                  "twitterUrl" : {
                    "type" : "text",
                    "fields" : {
                      "keyword" : {
                        "type" : "keyword",
                        "ignore_above" : 256
                      }
                    }
                  },
                  "type" : {
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
                "properties" : {
                  "boundaryNum" : {
                    "type" : "long"
                  },
                  "children" : {
                    "properties" : {
                      "area" : {
                        "type" : "text",
                        "fields" : {
                          "keyword" : {
                            "type" : "keyword",
                            "ignore_above" : 256
                          }
                        }
                      },
                      "boundaryNum" : {
                        "type" : "long"
                      },
                      "code" : {
                        "type" : "text",
                        "fields" : {
                          "keyword" : {
                            "type" : "keyword",
                            "ignore_above" : 256
                          }
                        }
                      },
                      "label" : {
                        "type" : "text",
                        "fields" : {
                          "keyword" : {
                            "type" : "keyword",
                            "ignore_above" : 256
                          }
                        }
                      },
                      "name" : {
                        "type" : "text",
                        "fields" : {
                          "keyword" : {
                            "type" : "keyword",
                            "ignore_above" : 256
                          }
                        }
                      },
                      "pincode" : {
                        "type" : "long"
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
                  },
                  "label" : {
                    "type" : "text",
                    "fields" : {
                      "keyword" : {
                        "type" : "keyword",
                        "ignore_above" : 256
                      }
                    }
                  },
                  "name" : {
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
          }
        } 
```

## API List <a href="#api-list" id="api-list"></a>

| <h4 id="title"><strong>Title</strong> </h4> | **Link**                                                                                                                    |
| ------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------- |
| _firenoc-services/v1/\_create_              |  [https://www.getpostman.com/collections/093e28bb4e341770b6c7](https://www.getpostman.com/collections/093e28bb4e341770b6c7) |
| _firenoc-services/v1/\_search_              |  [https://www.getpostman.com/collections/093e28bb4e341770b6c7](https://www.getpostman.com/collections/093e28bb4e341770b6c7) |
| _firenoc-services/v1/\_update_              |  [https://www.getpostman.com/collections/093e28bb4e341770b6c7](https://www.getpostman.com/collections/093e28bb4e341770b6c7) |

_(Note: All the APIs are in the same postman collection therefore the same link is added in each row)_

&#x20;
