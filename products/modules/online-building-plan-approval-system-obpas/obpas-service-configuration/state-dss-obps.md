---
description: Technical Doc
---

# State DSS - OBPS

## **Overview**

DSS has two sides to it. One is the process in which the data is pooled into ElasticSearch and the other is the way it is fetched, aggregated, computed, transformed and sent across.

As this revolves around a variety of data sets, there is a need for making this configurable. So that, tomorrow, given a new scenario is introduced, it is just a configuration away from getting the newly introduced scenario involved in this flow of the process.&#x20;

This document explains the steps on how to define the configurations for the analytics side Of DSS for OBPS.

**What is analytics?**

**Analytics:** Micro Service which is responsible for building, fetching, aggregating and computing the Data on ElasticSearch to a consumable Data Response. Which shall be later used for visualizations and graphical representations. &#x20;

**Analytics Configurations:** Analytics contains multiple configurations. we need to add the changes related to OBPS in this dashboard analytics.\
Here is the location : [<img src="https://github.com/fluidicon.png" alt="" data-size="line">configs/egov-dss-dashboards/dashboard-analytics at qa · egovernments/configs](https://github.com/egovernments/configs/tree/qa/egov-dss-dashboards/dashboard-analytics)

Below is a list of configurations that need to be changed to run OBPS successfully.

1. Chart API Configuration
2. Master Dashboard Configuration
3. Role Dashboard Mappings Configuration

## **Configuration Details** <a href="#description" id="description"></a>

### **Chart API Configuration**&#x20;

Each visualization has its own properties. Each visualization comes from different data sources (Sometimes it is a combination of different data sources).

In order to configure each visualization and its properties, we have a Chart API configuration document.

In this, visualization code, which happens to be the key, will have its properties configured as a part of the configuration and easily changeable.

Below is the sample ChartApiConfiguration.json data for the OBPS.

```
  "bpaTodaysCollection": {
    "chartName": "DSS_BPA_TODAYS_COLLECTION",
    "queries": [
      {
        "module": "BPA",
        "indexName": "dss-collection_v2",
        "aggrQuery": "{ \"aggs\": { \"AGGR\": { \"filter\": { \"bool\": { \"must\": [ { \"range\": { \"dataObject.paymentDetails.receiptDate\": { \"gte\": \"now-24h\", \"lte\": \"now\" } } }, { \"terms\": { \"dataObject.paymentDetails.businessService.keyword\": [ \"BPA.LOW_RISK_PERMIT_FEE\",\"BPA.NC_APP_FEE\",\"BPA.NC_OC_APP_FEE\" ] } } ], \"must_not\": [ { \"term\": { \"dataObject.tenantId.keyword\": \"pb.testing\" } }, { \"term\": { \"dataObject.paymentStatus.keyword\": \"Cancelled\" } } ] } }, \"aggs\": { \"Today's Collection\": { \"sum\": { \"field\": \"dataObject.paymentDetails.totalAmountPaid\" } } } } } }",
        "requestQueryMap":"{\"wardId\" : \"dataObject.ward.name.keyword\",\"module\" : \"dataObject.paymentDetails.businessService.keyword\",\"tenantId\" : \"dataObject.tenantId\", \"district\" : \"dataObject.tenantData.city.districtCode\" }",
        "dateRefField": ""
      }
    ],
    "chartType": "metric",
    "valueType": "amount",
    "action": "",
    "drillChart": "none",
    "aggregationPaths": [
      "Today's Collection"
    ],
    "insight": {
     
    },
    "_comment": "BPA Today's collections "
  },
  "bpaTotalCollection": {
    "chartName": "DSS_BPA_TOTAL_COLLECTION",
    "queries": [
      {
        "module": "BPA",
        "indexName": "dss-collection_v2",
        "aggrQuery": " { \"aggs\": { \"AGGR\": { \"filter\": { \"bool\": { \"must\": [ { \"terms\": { \"dataObject.paymentDetails.businessService.keyword\": [ \"BPA.LOW_RISK_PERMIT_FEE\",\"BPA.NC_APP_FEE\",\"BPA.NC_OC_APP_FEE\" ] } } ], \"must_not\": [ { \"term\": { \"dataObject.tenantId.keyword\": \"pb.testing\" } }, { \"term\": { \"dataObject.paymentStatus.keyword\": \"Cancelled\" } } ] } }, \"aggs\": { \"Total Collection\": { \"sum\": { \"field\": \"dataObject.paymentDetails.totalAmountPaid\" } } } } } } ",
        "requestQueryMap":"{\"wardId\" : \"dataObject.ward.name.keyword\",\"module\" : \"dataObject.paymentDetails.businessService.keyword\",\"tenantId\" : \"dataObject.tenantId\", \"district\" : \"dataObject.tenantData.city.districtCode\" }",
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
      "chartResponseMap" : "bpaTotalCollection",
      "action" : "differenceOfNumbers",
      "upwardIndicator" : "positive",
      "downwardIndicator" : "negative",
      "textMessage" : "$indicator$value% than last $insightInterval",
      "colorCode" : "#228B22",
      "insightInterval" : "year",
      "isRoundOff": true
    },
    "_comment": "BPA total collections "
  },
  "bpaTotalPlansScrutinized": {
    "chartName": "DSS_BPA_TOTAL_PLANS_SCRUTINIZED",
    "queries": [
      {
        "module": "OBPS",
        "requestQueryMap": "{\"wardId\" : \"Data.ward.name.keyword\",\"tenantId\" : \"Data.tenantId\" \r\n}",
        "dateRefField": "Data.@timestamp",
        "indexName": "edcr-index",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.tenantId.keyword\":\"pb.testing\"}}],\"must\":[{\"terms\":{\"Data.applicationType.keyword\":[\"PERMIT\",\"OCCUPANCY_CERTIFICATE\"]}}]}},\"aggs\":{\"Total Plans Scrutnized\":{\"value_count\":{\"field\":\"Data.dcrNumber.keyword\"}}}}}}"
      }
    ],
    "chartType": "metric",
    "valueType": "number",
    "drillChart": "none",
    "documentType": "_doc",
    "action": "",
    "aggregationPaths": [
      "Total Plans Scrutnized"
    ],
    "insight": {
      "chartResponseMap" : "bpaTotalPlansScrutinized",
      "action" : "differenceOfNumbers",
      "upwardIndicator" : "positive",
      "downwardIndicator" : "negative",
      "textMessage" : "$indicator$value% than last $insightInterval",
      "colorCode" : "#228B22",
      "insightInterval" : "year",
      "isRoundOff": true
    },
    "_comment": " Total Number of Complaints "
  },
  "bpaTotalApplicationsSubmitted": {
    "chartName": "DSS_BPA_TOTAL_APPLICATIONS_SUBMITTED",
    "queries": [
      {
        "module": "OBPS",
        "indexName": "bpa-index",
        "aggrQuery": "{ \"aggs\": { \"AGGR\": { \"filter\": { \"bool\": { \"must_not\": [ { \"term\": { \"Data.tenantId.keyword\": \"pb.testing\" } } ], \"must\": [ { \"terms\": { \"Data.businessService.keyword\": [\"BPA\",\"BPA_LOW\"] } } ] } }, \"aggs\": { \"Total Applications\": { \"value_count\": { \"field\": \"Data.applicationNo.keyword\" } } } } }} ",
        "requestQueryMap": "{\"wardId\" : \"Data.ward.name.keyword\",\"tenantId\" : \"Data.tenantId\" \r\n}",
        "dateRefField": "Data.@timestamp"
      }
    ],
    "translateTenantCode": false,
    "chartType": "metric",
    "valueType": "number",
    "action": "",
    "drillChart": "none",
    "aggregationPaths": [
      "Total Applications"
    ],
    "insight": {
      "chartResponseMap" : "bpaTotalApplicationsSubmitted",
      "action" : "differenceOfNumbers",
      "upwardIndicator" : "positive",
      "downwardIndicator" : "negative",
      "textMessage" : "$indicator$value% than last $insightInterval",
      "colorCode" : "#228B22",
      "insightInterval" : "year",
      "isRoundOff": true
    },
    "_comment": "BPA Total Applications"
  },
  "bpaTotalPermitsIssued": {
    "chartName": "DSS_BPA_TOTAL_PERMITS_ISSUED",
    "queries": [
      {
        "module": "OBPS",
        "indexName": "bpa-index",
        "requestQueryMap": "{\"wardId\" : \"Data.ward.name.keyword\",\"tenantId\" : \"Data.tenantId\" \r\n}",
        "aggrQuery": "{ \"aggs\": { \"AGGR\": { \"filter\": { \"bool\": { \"must_not\": [ { \"term\": { \"Data.tenantId.keyword\": \"pb.testing\" } } ], \"must\": [ { \"term\": { \"Data.status.keyword\": \"APPROVED\" } }, { \"terms\": { \"Data.businessService.keyword\": [\"BPA\",\"BPA_LOW\"] } } ] } }, \"aggs\": { \"Total Permits Issued\": { \"value_count\": { \"field\": \"Data.applicationNo.keyword\" } } } } } }",
        "dateRefField": "Data.@timestamp"
      }
    ],
    "translateTenantCode": false,
    "chartType": "metric",
    "valueType": "number",
    "action": "",
    "drillChart": "none",
    "aggregationPaths": [
      "Total Permits Issued"
    ],
    "insight": {
      "chartResponseMap" : "bpaTotalPermitsIssued",
      "action" : "differenceOfNumbers",
      "upwardIndicator" : "positive",
      "downwardIndicator" : "negative",
      "textMessage" : "$indicator$value% than last $insightInterval",
      "colorCode" : "#228B22",
      "insightInterval" : "year",
      "isRoundOff": true
    },
    "_comment": "Total Permits Issued"
  },
  "bpaTotalLandApplied": {
    "chartName": "DSS_BPA_TOTAL_LAND_APPLIED",
    "queries": [
      {
        "module": "OBPS",
        "indexName": "bpa-index",
        "requestQueryMap": "{\"wardId\" : \"Data.ward.name.keyword\",\"tenantId\" : \"Data.tenantId\" \r\n}",
        "aggrQuery":"{ \"aggs\": { \"AGGR\": { \"filter\": { \"bool\": { \"must_not\": [ { \"term\": { \"Data.tenantId.keyword\": \"pb.testing\" } } ], \"must\": [ { \"terms\": { \"Data.businessService.keyword\": [\"BPA\",\"BPA_LOW\",\"BPA_OC\"] } } ] } }, \"aggs\": { \"Total Land Applied\": { \"sum\": { \"field\": \"Data.plotArea\" } } } } } }",
        "dateRefField": "Data.@timestamp"
      }
    ],
    "translateTenantCode": false,
    "chartType": "metric",
    "valueType": "number",
    "action": "",
    "drillChart": "none",
    "aggregationPaths": [
      "Total Land Applied"
    ],
    "insight": {
      "chartResponseMap" : "bpaTotalLandApplied",
      "action" : "differenceOfNumbers",
      "upwardIndicator" : "positive",
      "downwardIndicator" : "negative",
      "textMessage" : "$indicator$value% than last $insightInterval",
      "colorCode" : "#228B22",
      "insightInterval" : "year",
      "isRoundOff": true
    },
    "_comment": "Total Land Applied"
  },

  "bpaAverageDaysToIssuePermit": {
    "chartName": "DSS_BPA_AVERAGE_DAYS_ISSUE_PERMIT",
    "queries": [
      {
        "module": "OBPS",
        "indexName": "bpa-index",
        "requestQueryMap": "{\"wardId\" : \"Data.ward.name.keyword\",\"tenantId\" : \"Data.tenantId\" \r\n}",
        "aggrQuery":"{ \"aggs\": { \"BPA\": { \"filter\": { \"bool\": { \"must_not\": [ { \"term\": { \"Data.tenantId.keyword\": \"pb.testing\" } } ] } }, \"aggs\": { \"Average days to issue Permit\": { \"filter\": { \"bool\": { \"must\": [ { \"terms\": { \"Data.businessService.keyword\": [\"BPA\",\"BPA_LOW\"] } }, { \"term\": { \"Data.status.keyword\": \"APPROVED\" } } ] } }, \"aggs\": { \"average_days\": { \"avg\": { \"script\": { \"source\": \"(doc['Data.auditDetails.lastModifiedTime'].value-doc['Data.auditDetails.createdTime'].value)/(86400*1000)\" } } } } } } } } }",
        "dateRefField": "Data.@timestamp"
      }
    ],
    "translateTenantCode": false,
    "chartType": "metric",
    "valueType": "number",
    "action": "",
    "drillChart": "none",
    "aggregationPaths": [
      "Average days to issue Permit"
    ],
    "insight": {
      "chartResponseMap" : "bpaAverageDaysToIssuePermit",
      "action" : "differenceOfNumbers",
      "upwardIndicator" : "positive",
      "downwardIndicator" : "negative",
      "textMessage" : "$indicator$value% than last $insightInterval",
      "colorCode" : "#228B22",
      "insightInterval" : "year",
      "isRoundOff": true
    },
    "_comment": "Average days to issue Permit"
  },
  "bpaSLACompliance": {
    "chartName": "DSS_BPA_SLA_COMPLIANCE",
    "queries": [
      {
        "module": "OBPS",
        "indexName": "bpa-index",
        "requestQueryMap": "{\"wardId\" : \"Data.ward.name.keyword\",\"tenantId\" : \"Data.tenantId\" \r\n}",
        "aggrQuery":"{ \"aggs\": { \"BPA\": { \"filter\": { \"bool\": { \"must_not\": [ { \"term\": { \"Data.tenantId.keyword\": \"pb.testing\" } } ] } }, \"aggs\": { \"SLA Compliance Permit\": { \"filter\": { \"bool\": { \"must\": [ { \"terms\": { \"Data.businessService.keyword\": [\"BPA\",\"BPA_LOW\"] } }, { \"term\": { \"Data.status.keyword\": \"APPROVED\" } }, { \"script\": { \"script\": { \"source\": \"doc['Data.auditDetails.lastModifiedTime'].value-doc['Data.auditDetails.createdTime'].value<params.threshold\", \"lang\": \"painless\", \"params\": { \"threshold\": 172800000 } } } } ] } } } } } } }",
        "dateRefField": "Data.@timestamp"
      }
    ],
    "translateTenantCode": false,
    "chartType": "metric",
    "valueType": "number",
    "action": "",
    "drillChart": "none",
    "aggregationPaths": [
      "SLA Compliance Permit"
    ],
    "insight": {
      "chartResponseMap" : "bpaSLACompliance",
      "action" : "differenceOfNumbers",
      "upwardIndicator" : "positive",
      "downwardIndicator" : "negative",
      "textMessage" : "$indicator$value% than last $insightInterval",
      "colorCode" : "#228B22",
      "insightInterval" : "year",
      "isRoundOff": true
    },
    "_comment": "SLA Compliance (Permit)"
  },
  "bpaAverageDaysToIssueOC": {
    "chartName": "DSS_BPA_AVERAGE_DAYS_ISSUE_OC",
    "queries": [
      {
        "module": "OBPS",
        "indexName": "bpa-index",
        "requestQueryMap": "{\"wardId\" : \"Data.ward.name.keyword\",\"tenantId\" : \"Data.tenantId\" \r\n}",
        "aggrQuery":"{ \"aggs\": { \"BPA\": { \"filter\": { \"bool\": { \"must_not\": [ { \"term\": { \"Data.tenantId.keyword\": \"pb.testing\" } } ] } }, \"aggs\": { \"Average days to issue OC\": { \"filter\": { \"bool\": { \"must\": [ { \"term\": { \"Data.businessService.keyword\": \"BPA_OC\" } }, { \"term\": { \"Data.status.keyword\": \"APPROVED\" } } ] } }, \"aggs\": { \"average_days\": { \"avg\": { \"script\": { \"source\": \"(doc['Data.auditDetails.lastModifiedTime'].value-doc['Data.auditDetails.createdTime'].value)/(86400*1000)\" } } } } } } } } }",
        "dateRefField": "Data.@timestamp"
      }
    ],
    "translateTenantCode": false,
    "chartType": "metric",
    "valueType": "number",
    "action": "",
    "drillChart": "none",
    "aggregationPaths": [
      "Average days to issue OC"
    ],
    "insight": {
      "chartResponseMap" : "bpaAverageDaysToIssueOC",
      "action" : "differenceOfNumbers",
      "upwardIndicator" : "positive",
      "downwardIndicator" : "negative",
      "textMessage" : "$indicator$value% than last $insightInterval",
      "colorCode" : "#228B22",
      "insightInterval" : "year",
      "isRoundOff": true
    },
    "_comment": "Average days to issue OC"
  },
  "bpaSLAComplianceOC": {
    "chartName": "DSS_BPA_SLA_COMPLIANCE_OC",
    "queries": [
      {
        "module": "OBPS",
        "indexName": "bpa-index",
        "requestQueryMap": "{\"wardId\" : \"Data.ward.name.keyword\",\"tenantId\" : \"Data.tenantId\" \r\n}",
        "aggrQuery":"{ \"aggs\": { \"BPA\": { \"filter\": { \"bool\": { \"must_not\": [ { \"term\": { \"Data.tenantId.keyword\": \"pb.testing\" } } ] } }, \"aggs\": { \"SLA Compliance OC\": { \"filter\": { \"bool\": { \"must\": [ { \"terms\": { \"Data.businessService.keyword\": [\"BPA_OC\"] } }, { \"term\": { \"Data.status.keyword\": \"APPROVED\" } }, { \"script\": { \"script\": { \"source\": \"doc['Data.auditDetails.lastModifiedTime'].value-doc['Data.auditDetails.createdTime'].value<params.threshold\", \"lang\": \"painless\", \"params\": { \"threshold\": 172800000 } } } } ] } } } } } } }",
        "dateRefField": "Data.@timestamp"
      }
    ],
    "translateTenantCode": false,
    "chartType": "metric",
    "valueType": "number",
    "action": "",
    "drillChart": "none",
    "aggregationPaths": [
      "SLA Compliance OC"
    ],
    "insight": {
      "chartResponseMap" : "bpaSLAComplianceOC",
      "action" : "differenceOfNumbers",
      "upwardIndicator" : "positive",
      "downwardIndicator" : "negative",
      "textMessage" : "$indicator$value% than last $insightInterval",
      "colorCode" : "#228B22",
      "insightInterval" : "year",
      "isRoundOff": true
    },
    "_comment": "SLA Compliance OC"
  },
  "bpaCumulativeCollections": {
    "chartName": "DSS_BPA_TOTAL_CUMULATIVE_COLLECTION",
    "queries": [
      {
        "module": "OBPS",
        "dateRefField": "dataObject.paymentDetails.receiptDate",
        "requestQueryMap": "{\"wardId\" : \"domainObject.ward.name.keyword\",\r\n  \"module\" : \"dataObject.paymentDetails.businessService.keyword\", \n\"tenantId\" : \"dataObject.tenantId\"}",
        "indexName": "dss-collection_v2",
        "aggrQuery": "{ \"aggs\": { \"AGGR\": { \"filter\": { \"bool\": { \"must\": [ { \"terms\": { \"dataObject.paymentStatus.keyword\": [ \"DEPOSITED\", \"NEW\" ] } }, { \"terms\": { \"dataObject.paymentDetails.businessService.keyword\": [ \"BPA.LOW_RISK_PERMIT_FEE\",\"BPA.NC_APP_FEE\",\"BPA.NC_OC_APP_FEE\" ] } } ], \"must_not\": [ { \"term\": { \"dataObject.tenantId.keyword\": \"pb.testing\" } }, { \"terms\": { \"dataObject.bill.status.keyword\": [ \"Cancelled\" ] } } ] } }, \"aggs\": { \"BPA Cumulative Collections\": { \"date_histogram\": { \"field\": \"dataObject.paymentDetails.receiptDate\", \"interval\": \"month\" }, \"aggs\": { \"Sum\": { \"sum\": { \"field\": \"dataObject.paymentDetails.totalAmountPaid\" } } } } } } } }"      }
    ],
    "translateTenantCode": false,
    "chartType": "line",
    "valueType": "amount",
    "action": "",
    "drillChart": "none",
    "documentType": "_doc",
    "aggregationPaths": [
      "BPA Cumulative Collections"
    ],
    "isCumulative": true,
    "interval": "month",
    "insight": {
    },
    "_comment": "Total Cumulative Collection"
  },
  "permitIssuedByRiskType": {
    "chartName": "DSS_BPA_PERMIT_ISSUED_BY_RISK_TYPE",
    "queries": [
      {
        "module": "OBPS",
        "dateRefField": "Data.@timestamp",
        "requestQueryMap": "{\"wardId\" : \"Data.ward.name.keyword\",\"tenantId\" : \"Data.tenantId\" \r\n}",
        "indexName": "bpa-index",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.tenantId.keyword\":\"pb.testing\"}}],\"must\":[{\"term\":{\"Data.status.keyword\":\"APPROVED\"}},{\"terms\":{\"Data.businessService.keyword\":[\"BPA\",\"BPA_LOW\"]}}]}},\"aggs\":{\"PermitsIssued By RiskType\":{\"terms\":{\"field\":\"Data.riskType.keyword\"},\"aggs\":{\"Count\":{\"value_count\":{\"field\":\"Data.riskType.keyword\"}}}}}}}}"
      }
    ],
    "translateTenantCode": false,
    "chartType": "pie",
    "valueType": "number",
    "isRoundOff": true,
    "action": "",
    "documentType": "_doc",
    "drillChart": "none",
    "aggregationPaths": [
      "PermitsIssued By RiskType"
    ],
    "insight": {
    },
    "_comment": " "
  },
   "permitIssuedByOccupancyType": {
    "chartName": "DSS_BPA_PERMIT_ISSUED_BY_OCCUPANCY_TYPE",
    "queries": [
      {
        "module": "OBPS",
        "dateRefField": "Data.@timestamp",
        "requestQueryMap": "{\"wardId\" : \"Data.ward.name.keyword\",\"tenantId\" : \"Data.tenantId\" \r\n}",
        "indexName": "bpa-index",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.tenantId.keyword\":\"pb.testing\"}}],\"must\":[{\"term\":{\"Data.status.keyword\":\"APPROVED\"}},{\"terms\":{\"Data.businessService.keyword\":[\"BPA\",\"BPA_LOW\"]}}]}},\"aggs\":{\"PermitsIssued By OccupancyType\":{\"terms\":{\"field\":\"Data.landInfo.unit.occupancyType.keyword\"},\"aggs\":{\"Count\":{\"value_count\":{\"field\":\"Data.landInfo.unit.occupancyType.keyword\"}}}}}}}}"
      }
    ],
    "translateTenantCode": false,
    "chartType": "pie",
    "valueType": "number",
    "isRoundOff": true,
    "action": "",
    "documentType": "_doc",
    "drillChart": "none",
    "aggregationPaths": [
      "PermitsIssued By OccupancyType"
    ],
    "insight": {
    },
    "_comment": " "
  },
  "permitsandOCissued": {
    "chartName": "DSS_TOTAL_PERMIT_ISSUED_VS_TOTAL_OC_ISSUED_VS_TOTAL_OC_SUBMITTED",
    "queries": [
      {
        "module": "OBPS",
        "dateRefField": "Data.@timestamp",
        "requestQueryMap": "{\"wardId\" : \"Data.ward.name.keyword\",\"tenantId\" : \"Data.tenantId\" \r\n}",
        "indexName": "bpa-index",
        "aggrQuery":"{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.tenantId.keyword\":\"pb.testing\"}}]}},\"aggs\":{\"TotalPermitIssued\":{\"date_histogram\":{\"field\":\"Data.@timestamp\",\"interval\":\"intervalvalue\"},\"aggs\":{\"totalPermitIssued\":{\"filter\":{\"bool\":{\"must\":[{\"terms\":{\"Data.businessService.keyword\":[\"BPA_LOW\",\"BPA\"]}},{\"term\":{\"Data.status.keyword\":\"APPROVED\"}}]}},\"aggs\":{\"Count\":{\"value_count\":{\"field\":\"Data.businessService.keyword\"}}}}}},\"TotalOCSubmitted\":{\"date_histogram\":{\"field\":\"Data.@timestamp\",\"interval\":\"intervalvalue\"},\"aggs\":{\"totalOCSUB\":{\"filter\":{\"bool\":{\"must\":[{\"terms\":{\"Data.businessService.keyword\":[\"BPA_OC\"]}}]}},\"aggs\":{\"Count\":{\"value_count\":{\"field\":\"Data.businessService.keyword\"}}}}}},\"TotalOCissued\":{\"date_histogram\":{\"field\":\"Data.@timestamp\",\"interval\":\"intervalvalue\"},\"aggs\":{\"totalOCissued\":{\"filter\":{\"bool\":{\"must\":[{\"terms\":{\"Data.businessService.keyword\":[\"BPA_OC\"]}},{\"term\":{\"Data.status.keyword\":\"APPROVED\"}}]}},\"aggs\":{\"Count\":{\"value_count\":{\"field\":\"Data.businessService.keyword\"}}}}}}}}}}"
      }
    ],
    "chartType": "line",
    "valueType": "number",
    "action": "",
    "drillChart": "none",
    "documentType": "_doc",
    "aggregationPaths": [
      "TotalPermitIssued",
      "TotalOCSubmitted",
      "TotalOCissued"

    ],
    "isRoundOff": true,
    "isCumulative": true,
    "interval": "month",
    "insight": {
    },
    "_comment": " "
  },
"obpsServiceReport": {
    "chartName": "DSS_OBPS_SERVICE_REPORT",
    "queries": [
      {
        "module": "OBPS",
        "requestQueryMap": "{\"wardId\" : \"dataObject.ward.name.keyword\",\"module\" : \"dataObject.paymentDetails.businessService.keyword\",\"tenantId\" : \"dataObject.tenantId\", \"district\" : \"dataObject.tenantData.city.districtCode\" }",
   		"dateRefField": "dataObject.paymentDetails.receiptDate",
        "indexName": "dss-collection_v2",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"dataObject.tenantId.keyword\":\"pb.testing\"}},{\"terms\":{\"dataObject.bill.status.keyword\":[\"Cancelled\"]}}],\"must\":[{\"terms\":{\"dataObject.paymentDetails.businessService.keyword\":[\"BPA.LOW_RISK_PERMIT_FEE\",\"BPA.NC_APP_FEE\",\"BPA.NC_OC_APP_FEE\"]}}]}},\"aggs\":{\"Total Collection\":{\"sum\":{\"field\":\"dataObject.paymentDetails.totalAmountPaid\"}}}}}}"
      },
      {
        "module": "OBPS",
        "requestQueryMap": "{\"wardId\" : \"Data.ward.name.keyword\",\"tenantId\" : \"Data.tenantId\", \"district\" : \"Data.tenantData.city.districtCode\"}",
        "dateRefField": "Data.auditDetails.createdTime",
        "indexName": "bpa-index",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.tenantId.keyword\":\"pb.testing\"}}]}},\"aggs\":{\"Total Applications Submitted\":{\"filter\":{\"bool\":{\"must\":[{\"terms\":{\"Data.businessService.keyword\":[\"BPA\",\"BPA_LOW\"]}}]}},\"aggs\":{\"total\":{\"value_count\":{\"field\":\"Data.applicationNo.keyword\"}}}},\"Total Permits Issued\":{\"filter\":{\"bool\":{\"must\":[{\"term\":{\"Data.status.keyword\":\"APPROVED\"}},{\"terms\":{\"Data.businessService.keyword\":[\"BPA\",\"BPA_LOW\"]}}]}},\"aggs\":{\"total\":{\"value_count\":{\"field\":\"Data.businessService.keyword\"}}}},\"Average days to issue Permit\":{\"filter\":{\"bool\":{\"must\":[{\"terms\":{\"Data.businessService.keyword\":[\"BPA\",\"BPA_LOW\"]}},{\"term\":{\"Data.status.keyword\":\"APPROVED\"}}]}},\"aggs\":{\"average_days\":{\"avg\":{\"script\":{\"source\":\"(doc['Data.auditDetails.lastModifiedTime'].value-doc['Data.auditDetails.createdTime'].value)\/(86400*1000)\"}}}}},\"Average days to issue OC\":{\"filter\":{\"bool\":{\"must\":[{\"term\":{\"Data.businessService.keyword\":\"BPA_OC\"}},{\"term\":{\"Data.status.keyword\":\"APPROVED\"}}]}},\"aggs\":{\"average_days\":{\"avg\":{\"script\":{\"source\":\"(doc['Data.auditDetails.lastModifiedTime'].value-doc['Data.auditDetails.createdTime'].value)\/(86400*1000)\"}}}}},\"SLA Compliance Permit\":{\"filter\":{\"bool\":{\"must\":[{\"terms\":{\"Data.businessService.keyword\":[\"BPA\",\"BPA_LOW\"]}},{\"term\":{\"Data.status.keyword\":\"APPROVED\"}},{\"script\":{\"script\":{\"source\":\"doc['Data.auditDetails.lastModifiedTime'].value-doc['Data.auditDetails.createdTime'].value<params.threshold\",\"lang\":\"painless\",\"params\":{\"threshold\":172800000}}}}]}}},\"SLA Compliance OC\":{\"filter\":{\"bool\":{\"must\":[{\"term\":{\"Data.businessService.keyword\":\"BPA_OC\"}},{\"term\":{\"Data.status.keyword\":\"APPROVED\"}},{\"script\":{\"script\":{\"source\":\"doc['Data.auditDetails.lastModifiedTime'].value-doc['Data.auditDetails.createdTime'].value<params.threshold\",\"lang\":\"painless\",\"params\":{\"threshold\":172800000}}}}]}}},\"Total OC Issued\":{\"filter\":{\"bool\":{\"must\":[{\"term\":{\"Data.status.keyword\":\"APPROVED\"}},{\"terms\":{\"Data.businessService.keyword\":[\"BPA_OC\"]}}]}}},\"Total OC Submitted\":{\"filter\":{\"bool\":{\"must\":[{\"terms\":{\"Data.businessService.keyword\":[\"BPA_OC\"]}}]}}},\"Deviation\":{\"filter\":{\"bool\":{\"must\":[{\"terms\":{\"Data.businessService.keyword\":[\"BPA_OC\",\"BPA\",\"BPA_LOW\"]}},{\"term\":{\"Data.status.keyword\":\"APPROVED\"}},{\"exists\":{\"field\":\"Data.plotAreaApproved\"}}]}},\"aggs\":{\"deviation\":{\"avg\":{\"script\":{\"source\":\" Math.round(((doc['Data.plotAreaApproved'].value-doc['Data.plotArea'].value)*100)\/(doc['Data.plotArea'].value))\"}}}}}}}}}"
      },
      {
        "module": "OBPS",
        "requestQueryMap": "{\"wardId\" : \"Data.ward.name.keyword\",\"tenantId\" : \"Data.tenantId\", \"district\" : \"Data.tenantData.city.districtCode\"}",
        "dateRefField": "Data.@timestamp",
        "indexName": "edcr-index",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.tenantId.keyword\":\"pb.testing\"}}]}},\"aggs\":{\"Total Plans Scrutnized\":{\"filter\":{\"bool\":{\"must\":[{\"terms\":{\"Data.applicationType.keyword\":[\"PERMIT\",\"OCCUPANCY_CERTIFICATE\"]}}]}},\"aggs\":{\"total\":{\"value_count\":{\"field\":\"Data.dcrNumber.keyword\"}}}},\"Total OC Scrutnized\":{\"filter\":{\"bool\":{\"must\":[{\"terms\":{\"Data.applicationType.keyword\":[\"OCCUPANCY_CERTIFICATE\"]}}]}},\"aggs\":{\"total\":{\"value_count\":{\"field\":\"Data.dcrNumber.keyword\"}}}}}}}}"
      }
      
    ],
    "isMdmsEnabled": true,
    "filterKeys": [
      {"key": "tenantId", "column": "DDRs"}
    ],
    "chartType": "table",
    "valueType": "number",
    "drillChart": "obpsServiceReportDrillDown",
    "documentType": "_doc",
    "plotLabel": "DDRs",
    "aggregationPaths": [
      "Total Collection",
      "Total Plans Scrutnized",
      "Total Applications Submitted",
      "Total Permits Issued",
      "Average days to issue Permit",
      "SLA Compliance Permit",
      "Total OC Scrutnized",
      "Total OC Submitted",
      "Total OC Issued",
      "Deviation",
      "Average days to issue OC",
      "SLA Compliance OC"
    ],
    "pathDataTypeMapping": [
      {
        "Total Collection": "amount"
      },
      {
        "Total Applications Submitted": "number"
      },
      {
        "Total Permits Issued": "number"
      },
      {
        "Average days to issue Permit": "number"
      },
      {
        "SLA Compliance Permit": "number"
      },
      {
        "Total OC Submitted": "number"
      },
      {
        "Total OC Issued": "number"
      },
      {
        "Deviation": "percentage"
      },
      {
        "Average days to issue OC": "number"
      },
      {
        "SLA Compliance OC": "number"
      },
      {
        "Total Plans Scrutnized": "number"
      
      },
      {
        "Total OC Scrutnized": "number"
      }
    ],
    "insight": {
    },
    "_comment": "OBPS Service Report "
  },

  "obpsServiceReportDrillDown": {
    "chartName": "DSS_OBPS_SERVICE_REPORT_DRILL_DOWN",
    "queries": [
      {
        "module": "OBPS",
        "requestQueryMap": "{\"wardId\" : \"dataObject.ward.name.keyword\",\"module\" : \"dataObject.paymentDetails.businessService.keyword\",\"tenantId\" : \"dataObject.tenantId\", \"district\" : \"dataObject.tenantData.city.districtCode\" }",
        "dateRefField": "dataObject.paymentDetails.receiptDate",
        "indexName": "dss-collection_v2",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"dataObject.tenantId.keyword\":\"pb.testing\"}},{\"terms\":{\"dataObject.bill.status.keyword\":[\"Cancelled\"]}}],\"must\":[{\"terms\":{\"dataObject.paymentDetails.businessService.keyword\":[\"BPA.LOW_RISK_PERMIT_FEE\",\"BPA.NC_APP_FEE\",\"BPA.NC_OC_APP_FEE\"]}}]}},\"aggs\":{\"ULBs\":{\"terms\":{\"field\":\"dataObject.tenantId.keyword\",\"size\":1000},\"aggs\":{\"Total Collection\":{\"sum\":{\"field\":\"dataObject.paymentDetails.totalAmountPaid\"}}}}}}}}"
      },
      {
        "module": "OBPS",
        "requestQueryMap":  "{\"wardId\" : \"Data.ward.name.keyword\",\"tenantId\" : \"Data.tenantId\", \"ulbId\" : \"Data.tenantId\", \"district\" : \"Data.tenantData.city.districtCode\"}",
        "dateRefField": "Data.auditDetails.createdTime",
        "indexName": "bpa-index",
        "aggrQuery": "{\n  \"aggs\": {\n    \"AGGR\": {\n      \"filter\": {\n        \"bool\": {\n          \"must_not\": [\n            {\n              \"term\": {\n                \"Data.tenantId.keyword\": \"pb.testing\"\n              }\n            }\n          ]\n        }\n      },\n      \"aggs\": {\n        \"ULBs\": {\n          \"terms\": {\n            \"field\": \"Data.tenantId.keyword\",\n            \"size\": 1000\n          },\n          \"aggs\": {\n            \"Total Applications Submitted\": {\n              \"filter\": {\n                \"bool\": {\n                  \"must\": [\n                    {\n                      \"terms\": {\n                        \"Data.businessService.keyword\": [\n                          \"BPA\",\n                          \"BPA_LOW\"\n                        ]\n                      }\n                    }\n                  ]\n                }\n              }\n            },\n            \"Total Permits Issued\": {\n              \"filter\": {\n                \"bool\": {\n                  \"must\": [\n                    {\n                      \"term\": {\n                        \"Data.status.keyword\": \"APPROVED\"\n                      }\n                    },\n                    {\n                      \"terms\": {\n                        \"Data.businessService.keyword\": [\n                          \"BPA\",\n                          \"BPA_LOW\"\n                        ]\n                      }\n                    }\n                  ]\n                }\n              }\n            },\n            \"Average days to issue Permit\": {\n              \"filter\": {\n                \"bool\": {\n                  \"must\": [\n                    {\n                      \"terms\": {\n                        \"Data.businessService.keyword\": [\n                          \"BPA\",\n                          \"BPA_LOW\"\n                        ]\n                      }\n                    },\n                    {\n                      \"term\": {\n                        \"Data.status.keyword\": \"APPROVED\"\n                      }\n                    }\n                  ]\n                }\n              },\n              \"aggs\": {\n                \"average_days\": {\n                  \"avg\": {\n                    \"script\": {\n                      \"source\": \"(doc['Data.auditDetails.lastModifiedTime'].value-doc['Data.auditDetails.createdTime'].value)/(86400*1000)\"\n                    }\n                  }\n                }\n              }\n            },\n            \"Average days to issue OC\": {\n              \"filter\": {\n                \"bool\": {\n                  \"must\": [\n                    {\n                      \"term\": {\n                        \"Data.businessService.keyword\": \"BPA_OC\"\n                      }\n                    },\n                    {\n                      \"term\": {\n                        \"Data.status.keyword\": \"APPROVED\"\n                      }\n                    }\n                  ]\n                }\n              },\n              \"aggs\": {\n                \"average_days\": {\n                  \"avg\": {\n                    \"script\": {\n                      \"source\": \"(doc['Data.auditDetails.lastModifiedTime'].value-doc['Data.auditDetails.createdTime'].value)/(86400*1000)\"\n                    }\n                  }\n                }\n              }\n            },\n            \"SLA Compliance Permit\": {\n              \"filter\": {\n                \"bool\": {\n                  \"must\": [\n                    {\n                      \"terms\": {\n                        \"Data.businessService.keyword\": [\n                          \"BPA\",\n                          \"BPA_LOW\"\n                        ]\n                      }\n                    },\n                    {\n                      \"term\": {\n                        \"Data.status.keyword\": \"APPROVED\"\n                      }\n                    },\n                    {\n                      \"script\": {\n                        \"script\": {\n                          \"source\": \"doc['Data.auditDetails.lastModifiedTime'].value-doc['Data.auditDetails.createdTime'].value<params.threshold\",\n                          \"lang\": \"painless\",\n                          \"params\": {\n                            \"threshold\": 172800000\n                          }\n                        }\n                      }\n                    }\n                  ]\n                }\n              }\n            },\n            \"SLA Compliance OC\": {\n              \"filter\": {\n                \"bool\": {\n                  \"must\": [\n                    {\n                      \"term\": {\n                        \"Data.businessService.keyword\": \"BPA_OC\"\n                      }\n                    },\n                    {\n                      \"term\": {\n                        \"Data.status.keyword\": \"APPROVED\"\n                      }\n                    },\n                    {\n                      \"script\": {\n                        \"script\": {\n                          \"source\": \"doc['Data.auditDetails.lastModifiedTime'].value-doc['Data.auditDetails.createdTime'].value<params.threshold\",\n                          \"lang\": \"painless\",\n                          \"params\": {\n                            \"threshold\": 172800000\n                          }\n                        }\n                      }\n                    }\n                  ]\n                }\n              }\n            },\n            \"Total OC Issued\": {\n              \"filter\": {\n                \"bool\": {\n                  \"must\": [\n                    {\n                      \"term\": {\n                        \"Data.status.keyword\": \"APPROVED\"\n                      }\n                    },\n                    {\n                      \"terms\": {\n                        \"Data.businessService.keyword\": [\n                          \"BPA_OC\"\n                        ]\n                      }\n                    }\n                  ]\n                }\n              }\n            },\n            \"Total OC Submitted\": {\n              \"filter\": {\n                \"bool\": {\n                  \"must\": [\n                    {\n                      \"terms\": {\n                        \"Data.businessService.keyword\": [\n                          \"BPA_OC\"\n                        ]\n                      }\n                    }\n                  ]\n                }\n              }\n            },\n            \"Deviation\": {\n              \"filter\": {\n                \"bool\": {\n                  \"must\": [\n                    {\n                      \"terms\": {\n                        \"Data.businessService.keyword\": [\n                          \"BPA_OC\",\n                          \"BPA\",\n                          \"BPA_LOW\"\n                        ]\n                      }\n                    },\n                    {\n                      \"term\": {\n                        \"Data.status.keyword\": \"APPROVED\"\n                      }\n                    },\n                    {\n                      \"exists\": {\n                        \"field\": \"Data.plotAreaApproved\"\n                      }\n                    }\n                  ]\n                }\n              },\n              \"aggs\": {\n                \"deviation\": {\n                  \"avg\": {\n                    \"script\": {\n                      \"source\": \" Math.round(((doc['Data.plotAreaApproved'].value-doc['Data.plotArea'].value)*100)/(doc['Data.plotArea'].value))\"\n                    }\n                  }\n                }\n              }\n            }\n          }\n        }\n      }\n    }\n  }\n}"     
         },
         {
          "module": "OBPS",
          "requestQueryMap":  "{\"wardId\" : \"Data.ward.name.keyword\",\"tenantId\" : \"Data.tenantId\", \"ulbId\" : \"Data.tenantId\", \"district\" : \"Data.tenantData.city.districtCode\"}",
          "dateRefField": "Data.@timestamp",
          "indexName": "edcr-index",
          "aggrQuery": "{\"aggs\":{\"obps\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.tenantId.keyword\":\"pb.testing\"}}]}},\"aggs\":{\"ULBs\":{\"terms\":{\"field\":\"Data.tenantId.keyword\",\"size\":1000},\"aggs\":{\"Total Plans Scrutnized\":{\"filter\":{\"bool\":{\"must\":[{\"terms\":{\"Data.applicationType.keyword\":[\"PERMIT\",\"OCCUPANCY_CERTIFICATE\"]}}]}},\"aggs\":{\"total\":{\"value_count\":{\"field\":\"Data.dcrNumber.keyword\"}}}},\"Total OC Scrutnized\":{\"filter\":{\"bool\":{\"must\":[{\"terms\":{\"Data.applicationType.keyword\":[\"OCCUPANCY_CERTIFICATE\"]}}]}},\"aggs\":{\"total\":{\"value_count\":{\"field\":\"Data.dcrNumber.keyword\"}}}}}}}}}}"
        }

    ],
   
    "filterKeys": [
      {"key": "tenantId", "column": "ULBs"}    ],
    "chartType": "table",
    "valueType": "number",
    "drillChart": "obpsServiceReportBoundaryDrillDown",
    "documentType": "_doc",
    "plotLabel": "ULBs",
    "aggregationPaths": [
      "Total Collection",
      "Total Plans Scrutnized",
      "Total Applications Submitted",
      "Total Permits Issued",
      "Average days to issue Permit",
      "SLA Compliance Permit",
      "Total OC Scrutnized",
      "Total OC Submitted",
      "Total OC Issued",
      "Deviation",
      "Average days to issue OC",
      "SLA Compliance OC"
    
    ],
    "pathDataTypeMapping": [
      {
        "Total Collection": "amount"
      },
      {
        "Total Applications Submitted": "number"
      },
      {
        "Total Permits Issued": "number"
      },
      {
        "Average days to issue Permit": "number"
      },
      {
        "SLA Compliance Permit": "number"
      },
      {
        "Total OC Submitted": "number"
      },
      {
        "Total OC Issued": "number"
      },
      {
        "Deviation": "percentage"
      },
      {
        "Average days to issue OC": "number"
      },
      {
        "SLA Compliance OC": "number"
      },
      {
        "Total Plans Scrutnized": "number"
      
      },
      {
        "Total OC Scrutnized": "number"
      }
    ],
    "insight": {
    },
    "_comment": "OBPS Service Report ULB Drill Down"
  },
  "obpsServiceReportBoundaryDrillDown": {
    "chartName": "DSS_OBPS_SERVICE_REPORT_BOUNDARY_DRILL_DOWN",
    "queries": [
      {
        "module": "OBPS",
        "requestQueryMap": "{\"wardId\" : \"dataObject.ward.name.keyword\",\"module\" : \"dataObject.paymentDetails.businessService.keyword\",\"tenantId\" : \"dataObject.tenantId\", \"district\" : \"dataObject.tenantData.city.districtCode\" }",
        "dateRefField": "dataObject.paymentDetails.receiptDate",
        "indexName": "dss-collection_v2",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"dataObject.tenantId.keyword\":\"pb.testing\"}},{\"terms\":{\"dataObject.bill.status.keyword\":[\"Cancelled\"]}}],\"must\":[{\"terms\":{\"dataObject.paymentDetails.businessService.keyword\":[\"BPA.LOW_RISK_PERMIT_FEE\",\"BPA.NC_APP_FEE\",\"BPA.NC_OC_APP_FEE\"]}}]}},\"aggs\":{\"ULBs\":{\"terms\":{\"field\":\"dataObject.tenantId.keyword\",\"size\":1000},\"aggs\":{\"Total Collection\":{\"sum\":{\"field\":\"dataObject.paymentDetails.totalAmountPaid\"}}}}}}}}"      },
      {
        "module": "OBPS",
        "requestQueryMap":  "{\"wardId\" : \"Data.ward.name.keyword\",\"tenantId\" : \"Data.tenantId\", \"ulbId\" : \"Data.tenantId\", \"district\" : \"Data.tenantData.city.districtCode\"}",
        "dateRefField": "Data.auditDetails.createdTime",
        "indexName": "bpa-index",
        "aggrQuery":"{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.tenantId.keyword\":\"pb.testing\"}}]}},\"aggs\":{\"ward\":{\"terms\":{\"field\":\"Data.ward.name.keyword\",\"size\":1000},\"aggs\":{\"Total Applications Submitted\":{\"filter\":{\"bool\":{\"must\":[{\"terms\":{\"Data.businessService.keyword\":[\"BPA\",\"BPA_LOW\"]}}]}}},\"Total Permits Issued\":{\"filter\":{\"bool\":{\"must\":[{\"term\":{\"Data.status.keyword\":\"APPROVED\"}},{\"terms\":{\"Data.businessService.keyword\":[\"BPA\",\"BPA_LOW\"]}}]}}},\"Average days to issue Permit\":{\"filter\":{\"bool\":{\"must\":[{\"terms\":{\"Data.businessService.keyword\":[\"BPA\",\"BPA_LOW\"]}},{\"term\":{\"Data.status.keyword\":\"APPROVED\"}}]}},\"aggs\":{\"average_days\":{\"avg\":{\"script\":{\"source\":\"(doc['Data.auditDetails.lastModifiedTime'].value-doc['Data.auditDetails.createdTime'].value)\/(86400*1000)\"}}}}},\"Average days to issue OC\":{\"filter\":{\"bool\":{\"must\":[{\"term\":{\"Data.businessService.keyword\":\"BPA_OC\"}},{\"term\":{\"Data.status.keyword\":\"APPROVED\"}}]}},\"aggs\":{\"average_days\":{\"avg\":{\"script\":{\"source\":\"(doc['Data.auditDetails.lastModifiedTime'].value-doc['Data.auditDetails.createdTime'].value)\/(86400*1000)\"}}}}},\"SLA Compliance Permit\":{\"filter\":{\"bool\":{\"must\":[{\"terms\":{\"Data.businessService.keyword\":[\"BPA\",\"BPA_LOW\"]}},{\"term\":{\"Data.status.keyword\":\"APPROVED\"}},{\"script\":{\"script\":{\"source\":\"doc['Data.auditDetails.lastModifiedTime'].value-doc['Data.auditDetails.createdTime'].value<params.threshold\",\"lang\":\"painless\",\"params\":{\"threshold\":172800000}}}}]}}},\"SLA Compliance OC\":{\"filter\":{\"bool\":{\"must\":[{\"term\":{\"Data.businessService.keyword\":\"BPA_OC\"}},{\"term\":{\"Data.status.keyword\":\"APPROVED\"}},{\"script\":{\"script\":{\"source\":\"doc['Data.auditDetails.lastModifiedTime'].value-doc['Data.auditDetails.createdTime'].value<params.threshold\",\"lang\":\"painless\",\"params\":{\"threshold\":172800000}}}}]}}},\"Total OC Issued\":{\"filter\":{\"bool\":{\"must\":[{\"term\":{\"Data.status.keyword\":\"APPROVED\"}},{\"terms\":{\"Data.businessService.keyword\":[\"BPA_OC\"]}}]}}},\"Total OC Submitted\":{\"filter\":{\"bool\":{\"must\":[{\"terms\":{\"Data.businessService.keyword\":[\"BPA_OC\"]}}]}}},\"Deviation\":{\"filter\":{\"bool\":{\"must\":[{\"terms\":{\"Data.businessService.keyword\":[\"BPA_OC\",\"BPA\",\"BPA_LOW\"]}},{\"term\":{\"Data.status.keyword\":\"APPROVED\"}},{\"exists\":{\"field\":\"Data.plotAreaApproved\"}}]}},\"aggs\":{\"deviation\":{\"avg\":{\"script\":{\"source\":\" Math.round(((doc['Data.plotAreaApproved'].value-doc['Data.plotArea'].value)*100)\/(doc['Data.plotArea'].value))\"}}}}}}}}}}}"
         }
        

    ],
  
    "filterKeys": [
      {"key": "wardId", "column": "Ward"},
      {"key": "ulbId", "column": "ULB"}    ],
    "chartType": "table",
    "valueType": "number",
    "drillChart": "none",
    "documentType": "_doc",
    "plotLabel": "Ward",
    "aggregationPaths": [
      "Total Collection",
      "Total Applications Submitted",
      "Total Permits Issued",
      "Average days to issue Permit",
      "SLA Compliance Permit", 
      "Total OC Submitted",
      "Total OC Issued",
      "Deviation",
      "Average days to issue OC",
      "SLA Compliance OC"
    ],
    "pathDataTypeMapping": [
      {
        "Total Collection": "amount"
      },
      {
        "Total Applications Submitted": "number"
      },
      {
        "Total Permits Issued": "number"
      },
      {
        "Average days to issue Permit": "number"
      },
      {
        "SLA Compliance Permit": "number"
      },
      {
        "Total OC Submitted": "number"
      },
      {
        "Total OC Issued": "number"
      },
      {
        "Deviation": "percentage"
      },
      {
        "Average days to issue OC": "number"
      },
      {
        "SLA Compliance OC": "number"
      }
    ],
    "insight": {
    },
    "_comment": "OBPS Service Report Ward Drill Down"
  },
    "obpsTopUlbByPerformance": {
    "chartName": "DSS_OBPS_TOP_ULB_BY_PERFORMANCE",
    "queries": [
      {
        "module": "OBPS",
        "requestQueryMap": "{\"wardId\" : \"Data.ward.name.keyword\",\"tenantId\" : \"Data.tenantId\" \r\n}",
        "dateRefField": "Data.@timestamp",
        "indexName": "bpa-index",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.tenantId.keyword\":\"pb.testing\"}}],\"must\":[{\"terms\":{\"Data.businessService.keyword\":[\"BPA\",\"BPA_LOW\"]}}]}},\"aggs\":{\"Total Applications\":{\"terms\":{\"field\":\"Data.tenantId.keyword\",\"size\":\"200\",\"order\":{\"Permits\":\"desc\"}},\"aggs\":{\"Permits\":{\"value_count\":{\"field\":\"Data.tenantId.keyword\"}}}}}}}}"
      },
      {
        "module": "OBPS",
        "requestQueryMap": "{\"wardId\" : \"Data.ward.name.keyword\",\"tenantId\" : \"Data.tenantId\" \r\n}",
        "dateRefField": "Data.@timestamp",
        "indexName": "bpa-index",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.tenantId.keyword\":\"pb.testing\"}}],\"must\":[{\"term\":{\"Data.status.keyword\":\"APPROVED\"}},{\"terms\":{\"Data.businessService.keyword\":[\"BPA\",\"BPA_LOW\"]}}]}},\"aggs\":{\"Approved Permit applications\":{\"terms\":{\"field\":\"Data.tenantId.keyword\",\"size\":\"200\",\"order\":{\"Permits\":\"desc\"}},\"aggs\":{\"Permits\":{\"value_count\":{\"field\":\"Data.tenantId.keyword\"}}}}}}}}"
      }
    ],
    "chartType": "perform",
    "valueType": "percentage",
    "documentType": "_doc",
    "drillChart": "none",
    "action": "percentage",
    "plotLabel": "DSS_COMPLETION_RATE",
    "isRoundOff": true,
    "order": "desc",
    "limit": 3,
    "aggregationPaths": [
      "Approved Permit applications",
      "Total Applications"
      
    ],
    "isCumulative": false,
    "interval": "month",
    "insight": {
    },
    "_comment": ""
  },

  "obpsBottomUlbByPerformance": {
    "chartName": "DSS_OBPS_BOTTOM_ULB_BY_PERFORMANCE",
    "queries": [
      {
        "module": "OBPS",
        "requestQueryMap": "{\"wardId\" : \"Data.ward.name.keyword\",\"tenantId\" : \"Data.tenantId\" \r\n}",
        "dateRefField": "Data.@timestamp",
        "indexName": "bpa-index",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.tenantId.keyword\":\"pb.testing\"}}],\"must\":[{\"terms\":{\"Data.businessService.keyword\":[\"BPA\",\"BPA_LOW\"]}}]}},\"aggs\":{\"Total Applications\":{\"terms\":{\"field\":\"Data.tenantId.keyword\",\"size\":\"200\",\"order\":{\"Permits\":\"asc\"}},\"aggs\":{\"Permits\":{\"value_count\":{\"field\":\"Data.tenantId.keyword\"}}}}}}}}"
      },
      {
        "module": "OBPS",
        "requestQueryMap": "{\"wardId\" : \"Data.ward.name.keyword\",\"tenantId\" : \"Data.tenantId\" \r\n}",
        "dateRefField": "Data.@timestamp",
        "indexName": "bpa-index",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.tenantId.keyword\":\"pb.testing\"}}],\"must\":[{\"term\":{\"Data.status.keyword\":\"APPROVED\"}},{\"terms\":{\"Data.businessService.keyword\":[\"BPA\",\"BPA_LOW\"]}}]}},\"aggs\":{\"Approved Permit applications\":{\"terms\":{\"field\":\"Data.tenantId.keyword\",\"size\":\"200\",\"order\":{\"Permits\":\"asc\"}},\"aggs\":{\"Permits\":{\"value_count\":{\"field\":\"Data.tenantId.keyword\"}}}}}}}}"
      }
    ],
    "isMdmsEnabled": false,
    "isPostResponseHandler": true,
    "postAggregationTheory" : "repsonseToDifferenceOfDates",
    "chartType": "perform",
    "valueType": "percentage",
    "documentType": "_doc",
    "drillChart": "none",
    "action": "percentage",
    "isRoundOff": true,
    "plotLabel": "DSS_COMPLETION_RATE",
    "order": "asc",
    "limit":3,
    "aggregationPaths": [
      "Approved Permit applications",
      "Total Applications"
      
    ],
    "isCumulative": false,
    "interval": "month",
    "insight": {
    },
    "_comment": ""
  },
  "obpsCollectionByPaymentMode": {
    "chartName": "DSS_OBPS_COLLECTION_BY_PAYMENT_MODE",
    "queries": [
      {
        "module": "OBPS",
        "requestQueryMap": "{\"wardId\" : \"dataObject.ward.name.keyword\",\"module\" : \"dataObject.paymentDetails.businessService.keyword\",\"tenantId\" : \"dataObject.tenantId\", \"district\" : \"dataObject.tenantData.city.districtCode\" }",
        "dateRefField": "dataObject.paymentDetails.receiptDate",
        "indexName": "dss-collection_v2",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must\":[{\"terms\":{\"dataObject.paymentDetails.businessService.keyword\":[\"BPA.LOW_RISK_PERMIT_FEE\",\"BPA.NC_APP_FEE\",\"BPA.NC_OC_APP_FEE\"]}}],\"must_not\":[{\"term\":{\"dataObject.tenantId.keyword\":\"pb.testing\"}},{\"terms\":{\"dataObject.bill.status.keyword\":[\"Cancelled\"]}}]}},\"aggs\":{\"PaymentMode\":{\"terms\":{\"field\":\"dataObject.paymentMode.keyword\"},\"aggs\":{\"Total Collection\":{\"sum\":{\"field\":\"dataObject.paymentDetails.totalAmountPaid\"}}}}}}}}"
      }
    ],
    "chartType": "pie",
    "valueType": "amount",
    "action": "",
    "isRoundOff": true,
    "documentType": "_doc",
    "drillChart": "none",
    "aggregationPaths": [
      "PaymentMode"
    ],
    "insight": {
    },
    "_comment": " "
  }
```

&#x20;[Click here to check the complete configuration](https://github.com/egovernments/configs/blob/qa/egov-dss-dashboards/dashboard-analytics/ChartApiConfig.json)

### &#x20;**Master Dashboard Configuration**

Master dashboard configuration is the main configuration which defines which Dashboards are to be painted on screen.&#x20;

It includes all the visualizations, their groups, the charts which come within them and even their dimensions as what should be their height and width.

```
    {
      "name":"DSS_BUILDING_PLANNING_DASHBOARD",
      "id":"obps",
      "isActive":"",
      "style":"linear",
      "visualizations":[
        {
          "row": 1,
          "name": "DSS_BUILDING_PLANNING",
          "vizArray": [
            {
              "id": 111,
              "name": "DSS_OVERVIEW_REVENUE",
              "dimensions": {
                "height": 350,
                "width": 5
              },
              "vizType": "metric-collection",
              "noUnit": true,
              "isCollapsible": false,
              "label": "DSS_OVERVIEW_REVENUE",
              "charts": [
                {
                  "id": "bpaTodaysCollection",
                  "name": "DSS_BPA_TODAYS_COLLECTION",
                  "code": "",
                  "chartType": "metric",
                  "filter": "",
                  "headers": []
                },
                {
                  "id": "bpaTotalCollection",
                  "name": "DSS_BPA_TOTAL_COLLECTION",
                  "code": "",
                  "chartType": "metric",
                  "filter": "",
                  "headers": []
                }
              ]
            }
          ,{
              "id": 112,
              "name": "DSS_BPA_TOTAL_CUMULATIVE_COLLECTION",
              "dimensions": {
                "height": 350,
                "width": 7
              },
              "vizType": "chart",
              "noUnit": true,
              "isCollapsible": false,
              "charts": [
                {
                  "id": "bpaCumulativeCollections",
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
          "row":2,
          "name":"DSS_BUILDING_PLANNING",
          "vizArray":[
            {
              "id": 210,
              "name": "DSS_OVERVIEW_SERVICES",
              "dimensions": {
                "height": 350,
                "width": 5
              },
              "vizType": "metric-collection",
              "noUnit": true,
              "isCollapsible": false,
              "label": "DSS_OVERVIEW_SERVICES",
              "charts": [
                {
                  "id": "bpaTotalPlansScrutinized",
                  "name": "DSS_BPA_TOTAL_PLANS_SCRUTINIZED",
                  "code": "",
                  "chartType": "metric",
                  "filter": "",
                  "headers": []
                },
                {
                  "id": "bpaTotalPermitsIssued",
                  "name": "DSS_BPA_TOTAL_PERMITS_ISSUED",
                  "code": "",
                  "chartType": "metric",
                  "filter": "",
                  "headers": []
                },
                {
                  "id": "bpaTotalLandApplied",
                  "name": "DSS_BPA_TOTAL_LAND_APPLIED",
                  "code": "",
                  "chartType": "metric",
                  "filter": "",
                  "headers": []
                },
                {
                  "id": "bpaAverageDaysToIssuePermit",
                  "name": "DSS_BPA_AVERAGE_DAYS_ISSUE_PERMIT",
                  "code": "",
                  "chartType": "metric",
                  "filter": "",
                  "headers": []
                },
                {
                  "id": "bpaSLACompliance",
                  "name": "DSS_BPA_SLA_COMPLIANCE",
                  "code": "",
                  "chartType": "metric",
                  "filter": "",
                  "headers": []
                },
                {
                  "id": "bpaAverageDaysToIssueOC",
                  "name": "DSS_BPA_AVERAGE_DAYS_ISSUE_OC",
                  "code": "",
                  "chartType": "metric",
                  "filter": "",
                  "headers": []
                },
                {
                  "id": "bpaSLAComplianceOC",
                  "name": "DSS_BPA_SLA_COMPLIANCE_OC",
                  "code": "",
                  "chartType": "metric",
                  "filter": "",
                  "headers": []
                }
              ]
            },
            {
              "id": 211,
              "name": "DSS_TOTAL_PERMIT_ISSUED_VS_TOTAL_OC_ISSUED_VS_TOTAL_OC_SUBMITTED",
              "dimensions": {
                "height": 250,
                "width": 7
              },
              "vizType": "chart",
              "isCollapsible": false,
              "label": "",
              "charts": [
                {
                  "id": "permitsandOCissued",
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
          "name": "DSS_BUILDING_PLANNING",
          "vizArray": [
            {
              "id": 323,
              "name": "DSS_OBPS_COLLECTION_BY_USAGE_TYPE",
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
                  "id": "obpsCollectionByPaymentMode",
                  "name": "DSS_OBPS_COLLECTION_BY_PAYMENT_MODE",
                  "code": "",
                  "chartType": "donut",
                  "filter": "",
                  "headers": []
                }
              ]
            },
            {
              "id": 321,
              "name": "DSS_OBPS_TOP_ULB_BY_PERFORMANCE",
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
                  "id": "obpsTopUlbByPerformance",
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
              "name": "DSS_OBPS_BOTTOM_ULB_BY_PERFORMANCE",
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
                  "id": "obpsBottomUlbByPerformance",
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
          "row":4,
          "name":"DSS_BUILDING_PLANNING",
          "vizArray":[
            {
              "id":311,
              "name":"DSS_BPA_PERMIT_ISSUED_BY_RISK_TYPE",
              "dimensions":{
                "height":250,
                "width":4
              },
              "vizType":"chart",
              "noUnit": false,
              "isCollapsible":false,
              "charts":[
                {
                  "id":"permitIssuedByRiskType",
                  "name":"DSS_BPA_PERMIT_ISSUED_BY_RISK_TYPE",
                  "code":"",
                  "chartType":"donut",
                  "filter":"",
                  "headers":[

                  ]
                }
              ]
            },
            {
              "id":312,
              "name":"DSS_BPA_PERMIT_ISSUED_BY_OCCUPANCY_TYPE",
              "dimensions":{
                "height":250,
                "width":4
              },
              "vizType":"chart",
              "noUnit": false,
              "isCollapsible":false,
              "charts":[
                {
                  "id":"permitIssuedByOccupancyType",
                  "name":"DSS_BPA_PERMIT_ISSUED_BY_OCCUPANCY_TYPE",
                  "code":"",
                  "chartType":"donut",
                  "filter":"",
                  "headers":[

                  ]
                }
              ]
            }

          ]
        },
        {
          "row": 5,
          "name": "DSS_BUILDING_PLANNING",
          "vizArray": [
            {
              "id": 231,
              "name": "DSS_OBPS_SERVICE_REPORT",
              "dimensions": {
                "height": 350,
                "width": 12
              },
              "vizType": "chart",
              "noUnit": false,
              "isCollapsible": false,
              "charts": [
                {
                  "id": "obpsServiceReport",
                  "name": "DSS_OBPS_SERVICE_REPORT",
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
    },

```

[Click here for the complete configuration](https://github.com/egovernments/configs/blob/qa/egov-dss-dashboards/dashboard-analytics/MasterDashboardConfig.json)

### **Role Dashboard Mappings Configuration**

Master dashboard configuration which was explained earlier hold the list of Dashboards which are available. Given the instance where Role Action Mapping is not maintained in the application service, this configuration acts as the Role-Dashboard mapping configuration.&#x20;

In this, each role is mapped against the dashboard which they are authorized to see. This was used earlier when the role action mapping of eGov was not integrated.

Later, when the role action mapping started controlling the dashboards to be seen on the client side, this configuration was just used to enable the dashboards for viewing.&#x20;

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
          "name": "OBPS",
          "id": "obps"
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
          "id": "ulb-obps"
        }
      ]
    }
  ]
}
```

[Click here to check the configuration](https://github.com/egovernments/configs/blob/qa/egov-dss-dashboards/dashboard-analytics/RoleDashboardMappingsConf.json)&#x20;

### **MDMS Configuration**

_common-masters/uiCommonConstants.json_

```
"obps": {
                  "routePath": "/dashboard/obps",
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
     "name": "DSS Dashboard Config obps",
      "url": "/dashboard-analytics/dashboard/getDashboardConfig/obps",
      "parentModule": "",
      "displayName": "DSS",
      "orderNumber": 0,
      "enabled": false,
      "serviceCode": "DSS",
      "code": "null",
      "path": ""
    },
    {
      "id": 2233,
      "name": "Dashboard OBPS",
      "url": "url",
      "displayName": "OBPS",
      "orderNumber": 4,
      "parentModule": "dss-dashboard",
      "enabled": true,
      "serviceCode": "DSS",
      "code": "null",
      "path": "Dashboard.OBPS",
      "navigationURL": "/digit-ui/employee/dss/dashboard/obps",
      "leftIcon": "places:business-center",
      "rightIcon": ""
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
    }
```

[Click here to check the complete configuration](https://github.com/egovernments/egov-mdms-data/blob/QA/data/pb/ACCESSCONTROL-ACTIONS-TEST/actions-test.json)

## Charts Configuration Details

&#x20;OBPS-State DSS consists of multiple graphs which represent the data of OBPS. Each graph has its own configuration which describes the chart and its type.

State DSS consists of the following charts in OBPS:

* Overview-Revenue
* Overview-Service
* Total Cumulative Collection
* Total permits issued vs Total OC submitted vs Total OC issued
* Collection by Payment Mode
* Top 3 Performing States/ULBs/Ward
* Bottom 3 Performing States/ULBs/Ward
* Permits Issued by Risk Type
* Permits Issued by Occupancy Type
* Service Report

More details about the respective charts are below:

**Overview-Revenue:** The Overview-Revenue chart contains multiple data information as below in the selected time period.

* **Today's Collection -** This represents today’s collection amount for OBPS Application Fee + Permit Fee.
* **Total Collection** - This represents the total collection amount for OBPS Application Fee + Permit Fee.

![](<../../../../.gitbook/assets/image (9) (3).png>)

**Overview-Service:** The Overview-Service chart contains multiple data information as below in the selected time period.

* **Total Plans Scrutinized** - This represents the total number of plans submitted by an architect for scrutiny for new construction to the concerned authority.
* **Total permits issued** - This represents the total number of new permits issued by the concerned authority.
* **Total sq m of land applied in the BPA system** - This represents the total area in square meters approved for construction.
* **Avg. days to issue permits** - This represents the average number of days taken to issue a permit application.
* **SLA Compliance (Permits)** - This represents the total percentage of permits issued within SLA.
* **Avg. days to issue OC** - This represents the average number of days taken to issue an OC.
* **SLA Compliance (OC)** - This represents the percentage of OCs issued within SLA

![](<../../../../.gitbook/assets/image (1) (4).png>)

**Total Cumulative Collection:** This graph contains the OBPS collection amount information on a monthly basis as a cumulative line graph for each OBPS collection separately. This changes as per the denomination amount filter selection.

**line** - this graph/chart is data representation on date histograms or date groupings.

![](<../../../../.gitbook/assets/image (38).png>)

**Total permits issued vs Total OC submitted vs Total OC issued:** This graph shows the total permits issued vs total OC submitted vs total OC issued for a given time period in the form of a line chart.

**line** - this graph/chart is data representation on date histograms or date groupings.

![](<../../../../.gitbook/assets/image (32).png>)

&#x20;**Collection by Payment Mode:** This chart is a pie chart showing the bifurcation of total collections by payment mode (online, cash, card, cheque) which is the sum of revenue collected from the OBPS module for the applied date filter.

![](<../../../../.gitbook/assets/image (39).png>)

&#x20;**Top 3 Performing ULBs:** This card will show the Top 3 Performing ULBs based on the percentage of permits issued. The number of permits issued / Number of applications.

![](<../../../../.gitbook/assets/image (6) (3).png>)

&#x20;**Bottom 3 Performing States:** This card shows the bottom 3 Performing States/ULBs/Wards based on the percentage of permits issued. Number of Permits issued / Number of applications

![](<../../../../.gitbook/assets/image (14).png>)

**Permits Issued by Risk Type:** This chart is a pie chart showing the bifurcation of total permits issued by risk type (low risk, medium risk, high risk) for the applied date filter.

![](<../../../../.gitbook/assets/image (4).png>)

&#x20;**Permits Issued by Occupancy Type:** This chart is a pie chart showing the bifurcation of total permits issued by occupancy type (Residential, Institutional etc) for the applied date filter.

![](<../../../../.gitbook/assets/image (5) (3).png>)

**Service Report:** This tabular chart representation graph shows information about multiple OBPS-related categories like Total Collection or Total Cumulative Collection, Total Plans Scrutinized, Total applications submitted, Total permits issued, Avg. days to issue a permit, SLA Compliance (Permits), Total OC Plans scrutinized, Total OC submitted, Total OC issued, Deviation Percentage, Avg. days to issue OC, SLA Compliance (OC), Total OCs with deviation. This table also shows the data at the state level and also has the drill-down chart for each state to ULB and from ULB to ward level data for the same.

<figure><img src="../../../../.gitbook/assets/image (24).png" alt=""><figcaption></figcaption></figure>

Clicking on any DDR name drills down the charts to show the specified state data.

<figure><img src="../../../../.gitbook/assets/image (37).png" alt=""><figcaption></figcaption></figure>

&#x20;Clicking on the ULB navigates to the ward-level data for the specified ULB.

<figure><img src="../../../../.gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure>

## **Newly Introduced Property Details** <a href="#newly-introduced-property" id="newly-introduced-property"></a>

**isRoundOff**: This property is introduced to round off the decimal values. For instance, if the value is 25.43 by using isRoundOff property in the configuration, the value is displayed as 25. Similarly, if the value is 22.56 round of value is displayed as 23. This can be used for insights configuration as well for overview graphs.

## Common Properties Available <a href="#common-properties-available" id="common-properties-available"></a>

**Key(eg: bpaTotalCollection):** This is the visualization code. This key is referred to in further visualization configurations. This is the key which will be used by the client application to indicate which visualization is needed for display.

**chartName:** The name of the chart which has to be used as a label on the dashboard. The name of the chart will be a detailed name. In this configuration, the Name of the Chart will be the code of Localization which will be used by the Client Side.

**queries:** Some visualizations are derived from a specific data source. While some others are derived from different data sources and are combined together to get a meaningful representation.

The queries of aggregation which are to be used to fetch out the right data in the right aggregated format are configured here.

**queries.module:** The module/domain level, on which the query should be applied i.e., OBPS

**queries.indexName:** The name of the index upon which the query has to be executed is configured here.

**queries.aggrQuery:** The aggregation query in itself is added here. Based on the Module and the Index name specified, this query is attached to the filter part of the complete search request and then executed against that index

**queries.requestQueryMap:** Client Request would carry certain fields which are to be filtered. The parameters specified in the Client Request are different from the parameters in each of these indexed documents.

In order to map the parameters of the request to the parameters of the ElasticSearch Document, this mapping is maintained.

**queries.dateRefField:** Each of these modules have separate indexes. And all of them have their own date fields.&#x20;

When there is a date filter applied against these visualizations, each of them has to apply it against their own date reference fields.

In order to maintain what is the date field in which index, we have this configured in this configuration parameter.

**chartType:** As there are different types of visualizations, this field defines what is the type of chart/visualization that this data should be used to represent.&#x20;

## **Chart Types Available**

**metric** - this represents the aggregated amount/value for records filtered by the aggregate es query&#x20;

**pie** - this represents the aggregated data on grouping. This is can be used to represent any line graph, bar graph, pie chart or donuts

**line** - this graph/chart is data representation on date histograms or date groupings

**perform** - this chart represents groping data performance-wise.

**table** - represents a form of plots and values with headers as grouped on and a list of its key, values pairs.&#x20;

**xtable -** represents an advanced feature of the table, it has the addition capabilities for adding dynamic header values.

**valueType -** In any instance of data, the values which are sent for plotting, might be a percentage, sometimes an amount or sometimes just a count.

In order to represent them and differentiate the numbers from the amount from the percentage, this field is used to indicate the type of value that this visualization will be sending.

**action:** Some of the visualizations are not just aggregations of data sources. There might be some cases where we have to do a post-aggregation computation.

For example, in the case of the Top 3 performing ULBs, the target and total collection are obtained and then the percentage is calculated. In these kinds of cases, the action that has to be performed on the data obtained is defined in this parameter.&#x20;

**documentType:** The type of document upon which the query has to be executed is defined here.&#x20;

**drillChart:** If there is a drill down on the visualization, then the code of the Drill Down Visualization is added here. This will be used by Client Service to manage drill-downs.

**aggregationPaths :** All the queries will be having Aggregation names in it. In order to fetch the value out of each Aggregation Responses, the name of the aggregation in the query will be an easy bet. These aggregation paths will have the names of Aggregation in them.

**insights:** It is to show the data with the comparison of last year with arrow symbols, it will show the data in how much % is increased or decreased.&#x20;

**\_comment:** In order to display information on the “i” symbol of each visualization, Visualization Information is maintained in this field.&#x20;

## **Postman Collection For OBPS-DSS**

[https://www.getpostman.com/collections/667f52a25918f7f5ba25](https://www.getpostman.com/collections/667f52a25918f7f5ba25)
