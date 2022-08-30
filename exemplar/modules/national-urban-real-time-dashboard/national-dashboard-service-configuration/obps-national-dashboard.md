# OBPS - National Dashboard

## **Overview**

NDSS has two sides to it. One is the process in which the data is pooled to the ElasticSearch and the other is the way it is fetched, aggregated, computed, transformed and sent across.

As this revolves around a variety of data sets, there is a need for making this configurable. This ensures that the process can be configured easily in case a new scenario is introduced.&#x20;

This document walks us through the steps on how to define the configurations for DSS analytics for the OBPS module.

## **Technical Details**

**Analytics:** Microservice responsible for building, fetching, aggregating and computing the data on ElasticSearch into a consumable data response. This is used for visualizations and graphical representations.&#x20;

**Analytics Configurations:** Analytics contains multiple configurations. Add the changes related to OBPS in this dashboard-analytics.\
Configuration file path: [<img src="https://github.com/fluidicon.png" alt="" data-size="line">configs/egov-dss-dashboards/dashboard-analytics at qa · egovernments/configs](https://github.com/egovernments/configs/tree/qa/egov-dss-dashboards/dashboard-analytics)\
Below is a list of configurations that need to be changed to run OBPS successfully.

1. Chart API Configuration
2. Master Dashboard Configuration
3. Role Dashboard Mappings Configuration

**Chart API Configuration:** Each visualization has its own properties. The visualization data is fetched from different sources. In some cases, it is a combination of different data sources.&#x20;

The Chart API configuration document is used to configure each visualization and its properties.

The visualization code is the key whose properties are configured here. These properties are easily changeable.

Below is the sample ChartApiConfiguration.json data for the OBPS.

```
  "nssOBPSTodaysCollection": {
    "chartName": "NSS_OBPS_TODAYS_COLLECTION",
    "queries": [
      {
        "module": "OBPS",
        "dateRefField": "date",
        "requestQueryMap":  "{\"ward\" : \"ward.keyword\",\"ulb\" : \"ulb.keyword\", \"state\" : \"state.keyword\"}",
        "indexName": "obps-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must\":[{\"range\":{\"date\":{\"gt\":\"now-1d\/d\",\"lte\":\"now\"}}}]}},\"aggs\":{\"todaysDate\":{\"terms\":{\"field\":\"date\",\"order\":{\"_term\":\"desc\"},\"size\":1},\"aggs\":{\"Todays Collection\":{\"sum\":{\"field\":\"todaysCollectionForPaymentMode\"}}}},\"lastUpdatedTime\":{\"terms\":{\"field\":\"lastModifiedTime\",\"order\":{\"_term\":\"desc\"},\"size\":1}}}}}}"
      }
    ],
    "chartType": "metric",
    "valueType": "amount",
    "action": "",
    "drillChart": "none",
    "TodaysCollection":true,
    "aggregationPaths": [
      "Todays Collection"
    ],
    "insight": {
    },
    "_comment": "DSS OBPS todays collections "
  },
  "nssOBPSTotalCollection": {
    "chartName": "NSS_OBPS_TOTAL_COLLECTION",
    "queries": [
      {
        "module": "OBPS",
        "dateRefField": "date",
        "requestQueryMap":  "{\"ward\" : \"ward.keyword\",\"ulb\" : \"ulb.keyword\", \"state\" : \"state.keyword\"}",
        "indexName": "obps-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"Total Collection\":{\"sum\":{\"field\":\"todaysCollectionForPaymentMode\"}}}}"
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
      "chartResponseMap" : "nssOBPSTotalCollection",
      "action" : "differenceOfNumbers",
      "upwardIndicator" : "positive",
      "downwardIndicator" : "negative",
      "textMessage" : "$indicator$value% than last $insightInterval",
      "colorCode" : "#228B22",
      "insightInterval" : "year",
      "isRoundOff": true
    },
    "_comment": "DSS OBPS Total Collection"
  },
  "nssOBPSTotalApplicationsSubmmited": {
    "chartName": "NSS_OBPS_TOTAL_APPLICATIONS_SUBMITTED",
    "queries": [
      {
        "module": "OBPS",
        "dateRefField": "date",
        "requestQueryMap":  "{\"ward\" : \"ward.keyword\",\"ulb\" : \"ulb.keyword\", \"state\" : \"state.keyword\"}",
        "indexName": "obps-national-dashboard",
        "aggrQuery": "{ \"aggs\": { \"intermediateAggr\": { \"terms\": { \"field\": \"date\" }, \"aggs\":{ \"applicationsSubmitted\":{ \"avg\":{ \"field\":\"applicationsSubmitted\" } } } }, \"Total Applications Submitted\": { \"sum_bucket\": { \"buckets_path\": \"intermediateAggr.applicationsSubmitted\" } } } }"      }
    ],
    "chartType": "metric",
    "valueType": "number",
    "action": "",
    "drillChart": "none",
    "aggregationPaths": [
      "Total Applications Submitted"
    ],
    "insight":  {
      "chartResponseMap" : "nssOBPSTotalApplicationsSubmmited",
      "action" : "differenceOfNumbers",
      "upwardIndicator" : "positive",
      "downwardIndicator" : "negative",
      "textMessage" : "$indicator$value% than last $insightInterval",
      "colorCode" : "#228B22",
      "insightInterval" : "year",
      "isRoundOff": true
    },
    "_comment": "DSS OBPS Total Applications Submitted"
  },
  "nssOBPSTotalPermitsIssued": {
    "chartName": "NSS_OBPS_TOTAL_PERMITS_ISSUED",
    "queries": [
      {
        "module": "OBPS",
        "dateRefField": "date",
        "requestQueryMap":   "{\"ward\" : \"ward.keyword\",\"ulb\" : \"ulb.keyword\", \"state\" : \"state.keyword\"}",
        "indexName": "obps-national-dashboard",
        "aggrQuery": "{ \"aggs\": { \"AGGR\": { \"filter\": { \"bool\": { \"must\": [ { \"terms\": { \"riskType.keyword\": [ \"LOW\", \"MEDIUM\",\"HIGH\" ] } } ] } }, \"aggs\": { \"Total Permits Issued\": { \"sum\": { \"field\": \"permitsIssuedForRiskType\" } } } } } }"
      }
    ],
    "chartType": "metric",
    "valueType": "number",
    "action": "",
    "drillChart": "none",
    "aggregationPaths": [
      "Total Permits Issued"
    ],
    "insight":  {
      "chartResponseMap" : "nssOBPSTotalPermitsIssued",
      "action" : "differenceOfNumbers",
      "upwardIndicator" : "positive",
      "downwardIndicator" : "negative",
      "textMessage" : "$indicator$value% than last $insightInterval",
      "colorCode" : "#228B22",
      "insightInterval" : "year",
      "isRoundOff": true
    },
    "_comment": "DSS OBPS Total Permits Issued"
  },
  "nssOBPSTotalPlansScrutinized": {
    "chartName": "NSS_OBPS_TOTAL_PLANS_SCRUTINIZED",
    "queries": [
      {
        "module": "OBPS",
        "dateRefField": "date",
        "requestQueryMap":  "{\"ward\" : \"ward.keyword\",\"ulb\" : \"ulb.keyword\", \"state\" : \"state.keyword\"}",
        "indexName": "obps-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"intermediateAggr\":{\"terms\":{\"field\":\"date\"},\"aggs\":{\"plansScrutinized\":{\"avg\":{\"field\":\"plansScrutinized\"}}}},\"Total Plans Scrutinized\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggr.plansScrutinized\"}}}}"
      }
    ],
    "chartType": "metric",
    "valueType": "number",
    "action": "",
    "drillChart": "none",
    "aggregationPaths": [
      "Total Plans Scrutinized"
    ],
    "insight": {
      "chartResponseMap" : "nssOBPSTotalPlansScrutinized",
      "action" : "differenceOfNumbers",
      "upwardIndicator" : "positive",
      "downwardIndicator" : "negative",
      "textMessage" : "$indicator$value% than last $insightInterval",
      "colorCode" : "#228B22",
      "insightInterval" : "year",
      "isRoundOff": true
    },
    "_comment": "DSS OBPS Total Plans Scrutinized "
  },
  "nssOBPSTotalOCIssued": {
    "chartName": "NSS_OBPS_TOTAL_OC_ISSUED",
    "queries": [
      {
        "module": "OBPS",
        "dateRefField": "date",
        "requestQueryMap":  "{\"ward\" : \"ward.keyword\",\"ulb\" : \"ulb.keyword\", \"state\" : \"state.keyword\"}",
        "indexName": "obps-national-dashboard",
        "aggrQuery": "{ \"aggs\": { \"intermediateAggr\": { \"terms\": { \"field\": \"date\" }, \"aggs\":{ \"ocIssued\":{ \"avg\":{ \"field\":\"ocIssued\" } } } }, \"Total OC Issued\": { \"sum_bucket\": { \"buckets_path\": \"intermediateAggr.ocIssued\" } } } }"      }
    ],
    "chartType": "metric",
    "valueType": "number",
    "action": "",
    "drillChart": "none",
    "aggregationPaths": [
      "Total OC Issued"
    ],
    "insight":  {
      "chartResponseMap" : "nssOBPSTotalOCIssued",
      "action" : "differenceOfNumbers",
      "upwardIndicator" : "positive",
      "downwardIndicator" : "negative",
      "textMessage" : "$indicator$value% than last $insightInterval",
      "colorCode" : "#228B22",
      "insightInterval" : "year",
      "isRoundOff": true
    },
    "_comment": "DSS OBPS Total OC Issued"
  },
  "nssOBPSTotalOCPlansScrutinized": {
    "chartName": "NSS_OBPS_TOTAL_OC_PLANS_SCRUTINIZED",
    "queries": [
      {
        "module": "OBPS",
        "dateRefField": "date",
        "requestQueryMap":  "{\"ward\" : \"ward.keyword\",\"ulb\" : \"ulb.keyword\", \"state\" : \"state.keyword\"}",
        "indexName": "obps-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"intermediateAggr\":{\"terms\":{\"field\":\"date\"},\"aggs\":{\"ocPlansScrutinized\":{\"avg\":{\"field\":\"ocPlansScrutinized\"}}}},\"Total OC plans scrutinized\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggr.ocPlansScrutinized\"}}}}"
      }
    ],
    "chartType": "metric",
    "valueType": "number",
    "action": "",
    "drillChart": "none",
    "aggregationPaths": [
      "Total OC plans scrutinized"
    ],
    "insight": {
      "chartResponseMap" : "nssOBPSTotalOCPlansScrutinized",
      "action" : "differenceOfNumbers",
      "upwardIndicator" : "positive",
      "downwardIndicator" : "negative",
      "textMessage" : "$indicator$value% than last $insightInterval",
      "colorCode" : "#228B22",
      "insightInterval" : "year",
      "isRoundOff": true
    },
    "_comment": "DSS OBPS Total OC plans scrutinized"
  },
  "nssOBPSAverageDaysIssuePermit": {
    "chartName": "NSS_OBPS_AVERAGE_DAYS_TO_ISSUE_PERMIT",
    "queries": [
      {
        "module": "OBPS",
        "dateRefField": "date",
        "requestQueryMap": "{\"ward\" : \"ward.keyword\",\"ulb\" : \"ulb.keyword\", \"state\" : \"state.keyword\"}",
        "indexName": "obps-national-dashboard",
        "aggrQuery":  "{\"aggs\":{\"intermediateAggr\":{\"terms\":{\"field\":\"date\"},\"aggs\":{\"averageDaysToIssuePermit\":{\"avg\":{\"field\":\"averageDaysToIssuePermit\"}}}},\"Average Days to issue permit\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggr.averageDaysToIssuePermit\"}}}}"
      }
    ],
    "chartType": "metric",
    "valueType": "number",
    "action": "",
    "drillChart": "none",
    "aggregationPaths": [
      "Average Days to issue permit"
    ],
    "insight": {
      "chartResponseMap" : "nssOBPSAverageDaysIssuePermit",
      "action" : "differenceOfNumbers",
      "upwardIndicator" : "positive",
      "downwardIndicator" : "negative",
      "textMessage" : "$indicator$value% than last $insightInterval",
      "colorCode" : "#228B22",
      "insightInterval" : "year",
      "isRoundOff": true
    },
    "_comment": "DSS OBPS Average Days to issue permit"
  },
  "nssOBPSAverageDaysIssueOC": {
    "chartName": "NSS_OBPS_AVERAGE_DAYS_TO_ISSUE_PERMIT",
    "queries": [
      {
        "module": "OBPS",
        "dateRefField": "date",
        "requestQueryMap":  "{\"ward\" : \"ward.keyword\",\"ulb\" : \"ulb.keyword\", \"state\" : \"state.keyword\"}",
        "indexName": "obps-national-dashboard",
        "aggrQuery":  "{\"aggs\":{\"intermediateAggr\":{\"terms\":{\"field\":\"date\"},\"aggs\":{\"averageDaysToIssueOC\":{\"avg\":{\"field\":\"averageDaysToIssueOC\"}}}},\"Average Days to issue OC\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggr.averageDaysToIssueOC\"}}}}"
      }
    ],
    "chartType": "metric",
    "valueType": "number",
    "action": "",
    "drillChart": "none",
    "aggregationPaths": [
      "Average Days to issue OC"
    ],
    "insight": {
      "chartResponseMap" : "nssOBPSAverageDaysIssueOC",
      "action" : "differenceOfNumbers",
      "upwardIndicator" : "positive",
      "downwardIndicator" : "negative",
      "textMessage" : "$indicator$value% than last $insightInterval",
      "colorCode" : "#228B22",
      "insightInterval" : "year",
      "isRoundOff": true
    },
    "_comment": "DSS OBPS Average Days to issue OC"
  },
  "nssOBPSTotalOCSubmitted": {
    "chartName": "NSS_OBPS_TOTAL_OC_SUBMITTED",
    "queries": [
      {
        "module": "OBPS",
        "dateRefField": "date",
        "requestQueryMap":   "{\"ward\" : \"ward.keyword\",\"ulb\" : \"ulb.keyword\", \"state\" : \"state.keyword\"}",
        "indexName": "obps-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"intermediateAggr\":{\"terms\":{\"field\":\"date\"},\"aggs\":{\"ocSubmitted\":{\"avg\":{\"field\":\"ocSubmitted\"}}}},\"Total OC Submitted\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggr.ocSubmitted\"}}}}"
      }
    ],
    "chartType": "metric",
    "valueType": "number",
    "action": "",
    "drillChart": "none",
    "aggregationPaths": [
      "Total OC Submitted"
    ],
    "insight": {
      "chartResponseMap" : "nssOBPSTotalOCSubmitted",
      "action" : "differenceOfNumbers",
      "upwardIndicator" : "positive",
      "downwardIndicator" : "negative",
      "textMessage" : "$indicator$value% than last $insightInterval",
      "colorCode" : "#228B22",
      "insightInterval" : "year",
      "isRoundOff": true
    },
    "_comment": "DSS OBPS Total OC submitted"
  },
  "nssOBPSTotalLandAreaAppliedInSystem": {
    "chartName": "TOTAL_Sq_m_LAND_AREA_APPLIED_IN_SYSTEM",
    "queries": [
      {
        "module": "OBPS",
        "dateRefField": "date",
        "requestQueryMap":   "{\"ward\" : \"ward.keyword\",\"ulb\" : \"ulb.keyword\", \"state\" : \"state.keyword\"}",
        "indexName": "obps-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"intermediateAggr\":{\"terms\":{\"field\":\"date\"},\"aggs\":{\"landAreaAppliedInSystemForBPA\":{\"avg\":{\"field\":\"landAreaAppliedInSystemForBPA\"}}}},\"Land Area Applied In System For BPA\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggr.landAreaAppliedInSystemForBPA\"}}}}"
      }
    ],
    "chartType": "metric",
    "valueType": "number",
    "action": "",
    "drillChart": "none",
    "aggregationPaths": [
      "Land Area Applied In System For BPA"
    ],
    "insight": {
      "chartResponseMap" : "nssOBPSTotalLandAreaAppliedInSystem",
      "action" : "differenceOfNumbers",
      "upwardIndicator" : "positive",
      "downwardIndicator" : "negative",
      "textMessage" : "$indicator$value% than last $insightInterval",
      "colorCode" : "#228B22",
      "insightInterval" : "year",
      "isRoundOff": true
    },
    "_comment": "DSS OBPS Total sq m of land applied in BPA system "
  },
  "nssOBPSCumulativeCollection": {
    "chartName": "NSS_OBPS_TOTAL_CUMULATIVE_COLLECTION",
    "queries": [
      {
        "module": "OBPS",
        "dateRefField": "date",
        "requestQueryMap":  "{\"ward\" : \"ward.keyword\",\"ulb\" : \"ulb.keyword\", \"state\" : \"state.keyword\"}",
        "indexName": "obps-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"Collections\":{\"date_histogram\":{\"field\":\"date\",\"interval\":\"month\"},\"aggs\":{\"Sum\":{\"sum\":{\"field\":\"todaysCollectionForPaymentMode\"}}}}}}"
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
    "_comment": "DSS OBPS Total cumulative collections "
  },
  "nssOBPSPermitIssuedByOccupancyType": {
    "chartName": "NSS_OBPS_PERMIT_ISSUED_BY_OCCUPANCY_TYPE",
    "queries": [
      {
        "module": "OBPS",
        "dateRefField": "date",
        "requestQueryMap":  "{\"ward\" : \"ward.keyword\",\"ulb\" : \"ulb.keyword\", \"state\" : \"state.keyword\"}",
        "indexName": "obps-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"Permit Issued By OccupancyType\":{\"terms\":{\"field\":\"occupancyType.keyword\"},\"aggs\":{\"PemritIssued\":{\"sum\":{\"field\":\"permitsIssuedForOccupancyType\"}}}}}}"
      }
    ],
    "chartType": "pie",
    "valueType": "number",
    "action": "",
    "isRoundOff": true,
    "documentType": "_doc",
    "drillChart": "none",
    "aggregationPaths": [
      "Permit Issued By OccupancyType"
    ],
    "insight": {
    },
    "_comment": "NSS OBPS Permit Issued By OccupancyType"
  },
  "nssOBPSPermitIssuedByRiskType": {
    "chartName": "NSS_OBPS_PERMIT_ISSUED_BY_RISK_TYPE",
    "queries": [
      {
        "module": "OBPS",
        "dateRefField": "date",
        "requestQueryMap":  "{\"ward\" : \"ward.keyword\",\"ulb\" : \"ulb.keyword\", \"state\" : \"state.keyword\"}",
        "indexName": "obps-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"Permit Issued By RiskType\":{\"terms\":{\"field\":\"riskType.keyword\"},\"aggs\":{\"Pemrit Issued\":{\"sum\":{\"field\":\"permitsIssuedForRiskType\"}}}}}}"
      }
    ],
    "chartType": "pie",
    "valueType": "number",
    "action": "",
    "isRoundOff": true,
    "documentType": "_doc",
    "drillChart": "none",
    "aggregationPaths": [
      "Permit Issued By RiskType"
    ],
    "insight": {
    },
    "_comment": "NSS OBPS Permit Issued By RiskType"
  },
  "nssOBPSTotalPermitsVsTotalOCSubmittedVsTotalOCIssued": {
    "chartName": "NSS_TOTAL_PERMITS_VS_TOTAL_OC_SUBMITTED_VS_OC_ISSUED",
    "queries": [
      {
        "module": "OBPS",
        "dateRefField": "date",
        "requestQueryMap":  "{\"ward\" : \"ward.keyword\",\"ulb\" : \"ulb.keyword\", \"state\" : \"state.keyword\"}",
        "indexName": "obps-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"Permits Issued\":{\"date_histogram\":{\"field\":\"date\",\"interval\":\"intervalvalue\"},\"aggs\":{\"Permits\":{\"filter\":{\"bool\":{\"must\":[{\"terms\":{\"riskType.keyword\":[\"HIGH\",\"MEDIUM\",\"LOW\"]}}]}},\"aggs\":{\"Total Permits Issued\":{\"sum\":{\"field\":\"permitsIssuedForRiskType\"}}}}}},\"OC Issued\":{\"date_histogram\":{\"field\":\"date\",\"interval\":\"intervalvalue\"},\"aggs\":{\"intermediateAggr\":{\"terms\":{\"field\":\"date\"},\"aggs\":{\"ocIssued\":{\"avg\":{\"field\":\"ocIssued\"}}}},\"Total OC Issued\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggr.ocIssued\"}}}},\"OC Submitted\":{\"date_histogram\":{\"field\":\"date\",\"interval\":\"intervalvalue\"},\"aggs\":{\"intermediateAggr\":{\"terms\":{\"field\":\"date\"},\"aggs\":{\"ocSubmitted\":{\"avg\":{\"field\":\"ocSubmitted\"}}}},\"Total OC submitted\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggr.ocSubmitted\"}}}}}}"
      }
    ],
    "chartType": "line",
    "valueType": "number",
    "action": "",
    "drillChart": "none",
    "documentType": "_doc",
    "aggregationPaths": [
      "Permits Issued",
      "OC Issued",
      "OC Submitted"
    ],
    "isCumulative": true,
    "interval": "month",
    "insight": {
    },
    "_comment": "NSS OBPS TotalPermits Vs TotalOCSubmitted Vs TotalOCIssued"
  },
  "nssOBPSCollectionByPaymentMode": {
    "chartName": "NSS_OBPS_COLLECTION_BY_PAYMENT_MODE",
    "queries": [
      {
        "module": "OBPS",
        "dateRefField": "date",
        "requestQueryMap":  "{\"ward\" : \"ward.keyword\",\"ulb\" : \"ulb.keyword\", \"state\" : \"state.keyword\"}",
        "indexName": "obps-national-dashboard",
        "aggrQuery": "{ \"aggs\": { \"Collection By Payment Mode\": { \"terms\": { \"field\": \"paymentMode.keyword\" }, \"aggs\": { \"Collection\": { \"sum\": { \"field\": \"todaysCollectionForPaymentMode\" } } } } } }"
      }
    ],
    "chartType": "pie",
    "valueType": "amount",
    "action": "",
    "isRoundOff": true,
    "documentType": "_doc",
    "drillChart": "none",
    "aggregationPaths": [
      "Collection By Payment Mode"
    ],
    "insight": {
    },
    "_comment": "NSS OBPS Collection By Payment Mode"
  },
  "nssOBPSSlaCompliancePermit": {
    "chartName": "NSS_OBPS__SLA_COMPLIANCE_PERMIT",
    "queries": [
      {
        "module": "OBPS",
        "dateRefField": "date",
        "requestQueryMap": "{\"ward\" : \"ward.keyword\",\"ulb\" : \"ulb.keyword\", \"state\" : \"state.keyword\"}",
        "indexName": "obps-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"intermediateAggr\":{\"terms\":{\"field\":\"date\"},\"aggs\":{\"slaCompliancePermit\":{\"avg\":{\"field\":\"SLACompliancePermit\"}}}},\"SLA Compliance Permit\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggr.slaCompliancePermit\"}}}}"
      }
    ],
    "chartType": "metric",
    "valueType": "number",
    "action": "",
    "drillChart": "none",
    "aggregationPaths": [
      "SLA Compliance Permit"
    ],
    "insight": {
      "chartResponseMap" : "nssOBPSSlaCompliancePermit",
      "action" : "differenceOfNumbers",
      "upwardIndicator" : "positive",
      "downwardIndicator" : "negative",
      "textMessage" : "$indicator$value% than last $insightInterval",
      "colorCode" : "#228B22",
      "insightInterval" : "year",
      "isRoundOff": true
    },
    "_comment": "DSS OBPS SLA Compliance Permit"
  },
  "nssOBPSSlaComplianceOC": {
    "chartName": "NSS_OBPS_SLA_COMPLIANCE_OC",
    "queries": [
      {
        "module": "OBPS",
        "dateRefField": "date",
        "requestQueryMap":   "{\"ward\" : \"ward.keyword\",\"ulb\" : \"ulb.keyword\", \"state\" : \"state.keyword\"}",
        "indexName": "obps-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"intermediateAggr\":{\"terms\":{\"field\":\"date\"},\"aggs\":{\"slaComplianceOC\":{\"avg\":{\"field\":\"SLAComplianceOC\"}}}},\"SLA Compliance OC\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggr.slaComplianceOC\"}}}}"
      }
    ],
    "chartType": "metric",
    "valueType": "number",
    "action": "",
    "drillChart": "none",
    "aggregationPaths": [
      "SLA Compliance OC"
    ],
    "insight": {
      "chartResponseMap" : "nssOBPSSlaComplianceOC",
      "action" : "differenceOfNumbers",
      "upwardIndicator" : "positive",
      "downwardIndicator" : "negative",
      "textMessage" : "$indicator$value% than last $insightInterval",
      "colorCode" : "#228B22",
      "insightInterval" : "year",
      "isRoundOff": true
    },
    "_comment": "DSS OBPS SLA Compliance OC"
  },
  "nssOBPSBottomPerformingUlbs": {
    "chartName": "NSS_OBPS_BOTTOM_3_PERFORMING_ULBS",
    "queries": [
      {
        "module": "OBPS",
        "dateRefField": "date",
        "requestQueryMap":  "{\"ward\" : \"ward.keyword\",\"ulb\" : \"ulb.keyword\", \"state\" : \"state.keyword\"}",
        "indexName": "obps-national-dashboard",
        "aggrQuery": "{ \"aggs\": { \"StateWiseApplications\": { \"terms\": { \"field\": \"state.keyword\" }, \"aggs\": { \"intermediateAggr\": { \"terms\": { \"field\": \"date\" }, \"aggs\": { \"applicationsSubmitted\": { \"avg\": { \"field\": \"applicationsSubmitted\" } } } }, \"TAS1\": { \"sum_bucket\": { \"buckets_path\": \"intermediateAggr.applicationsSubmitted\" } } } }, \"Total Applications Submitted\": { \"sum_bucket\": { \"buckets_path\": \"StateWiseApplications.TAS1\" } } } }"      },
      {
        "module": "OBPS",
        "requestQueryMap":"{\"ward\" : \"ward.keyword\",\"ulb\" : \"ulb.keyword\", \"state\" : \"state.keyword\"}",
        "dateRefField": "date",
        "indexName": "obps-national-dashboard",
        "aggrQuery": "{ \"aggs\": { \"Total Permits Issued\": { \"terms\": { \"field\": \"state.keyword\", \"size\": 200, \"order\": { \"Total Permits\": \"desc\" } }, \"aggs\": { \"Total Permits\": { \"sum\": { \"field\": \"permitsIssuedForRiskType\" } } } } } } "
      }
    ],
    "isMdmsEnabled": false,
    "isPostResponseHandler": true,
    "chartType": "perform",
    "valueType": "percentage",
    "isRoundOff": true,
    "drillChart": "none",
    "documentType": "_doc",
    "action": "percentage",
    "plotLabel": "NSS_OBPS_BOTTOM_3_PERFORMING_ULBS",
    "order": "asc",
    "limit": 3,
    "aggregationPaths": [
      "Total Permits Issued",
      "StateWiseApplications"
    ],
    "insight": {
    },
    "_comment": "NSS OBPS Bottom Performing Ulbs by permits issued"
  },
  "nssOBPSTopPerformingUlbs": {
    "chartName": "NSS_OBPS_TOP_3_PERFORMING_ULBS",
    "queries": [
      {
        "module": "OBPS",
        "dateRefField": "date",
        "requestQueryMap":  "{\"ward\" : \"ward.keyword\",\"ulb\" : \"ulb.keyword\", \"state\" : \"state.keyword\"}",
        "indexName": "obps-national-dashboard",
        "aggrQuery": "{ \"aggs\": { \"StateWiseApplications\": { \"terms\": { \"field\": \"state.keyword\" }, \"aggs\": { \"intermediateAggr\": { \"terms\": { \"field\": \"date\" }, \"aggs\": { \"applicationsSubmitted\": { \"avg\": { \"field\": \"applicationsSubmitted\" } } } }, \"TAS1\": { \"sum_bucket\": { \"buckets_path\": \"intermediateAggr.applicationsSubmitted\" } } } }, \"Total Applications Submitted\": { \"sum_bucket\": { \"buckets_path\": \"StateWiseApplications.TAS1\" } } } }"      },
      {
        "module": "OBPS",
        "requestQueryMap":  "{\"ward\" : \"ward.keyword\",\"ulb\" : \"ulb.keyword\", \"state\" : \"state.keyword\"}",
        "dateRefField": "date",
        "indexName": "obps-national-dashboard",
        "aggrQuery": "{ \"aggs\": { \"Total Permits Issued\": { \"terms\": { \"field\": \"state.keyword\", \"size\": 200, \"order\": { \"Total Permits\": \"desc\" } }, \"aggs\": { \"Total Permits\": { \"sum\": { \"field\": \"permitsIssuedForRiskType\" } } } } } } "
      }
    ],
    "isMdmsEnabled": false,
    "isPostResponseHandler": true,
    "chartType": "perform",
    "valueType": "percentage",
    "isRoundOff": true,
    "drillChart": "none",
    "documentType": "_doc",
    "action": "percentage",
    "plotLabel": "NSS_OBPS_TOP_3_PERFORMING_ULBS",
    "order": "desc",
    "limit": 3,
    "aggregationPaths": [
      "Total Permits Issued",
      "StateWiseApplications"
    ],
    "insight": {
    },
    "_comment": "NSS OBPS Top Performing Ulbs by permits issued"
  },
  "nssOBPSServiceReport": {
    "chartName": "NSS_OBPS_SERVICE_REPORT",
    "queries": [
      {
        "module": "OBPS",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ward\" : \"ward.keyword\"}",
        "dateRefField": "date",
        "indexName": "obps-national-dashboard",
        "aggrQuery": "{ \"aggs\": { \"AGGR\": { \"filter\": { \"bool\": {} }, \"aggs\": { \"State\": { \"terms\": { \"field\": \"state.keyword\", \"size\": 1000 }, \"aggs\": { \"Total_Collection\": { \"sum\": { \"field\": \"todaysCollectionForPaymentMode\" } }, \"Total_Plans_Scrutinized\": { \"filter\": { \"bool\": { \"must_not\": [] } }, \"aggs\": { \"intermediateAggr\": { \"terms\": { \"field\": \"date\" }, \"aggs\": { \"plansScrutinized\": { \"avg\": { \"field\": \"plansScrutinized\" } } } }, \"Total_Plans_Scrutinized\": { \"sum_bucket\": { \"buckets_path\": \"intermediateAggr.plansScrutinized\" } } } }, \"Total_Applications\": { \"filter\": { \"bool\": { \"must_not\": [] } }, \"aggs\": { \"intermediateAggr\": { \"terms\": { \"field\": \"date\" }, \"aggs\": { \"applicationsSubmitted\": { \"avg\": { \"field\": \"applicationsSubmitted\" } } } }, \"Total_Applications\": { \"sum_bucket\": { \"buckets_path\": \"intermediateAggr.applicationsSubmitted\" } } } }, \"Total_Permits_Issued\": { \"sum\": { \"field\": \"permitsIssuedForRiskType\" } }, \"Average_Days_To_Issue_Permit\": { \"filter\": { \"bool\": { \"must_not\": [] } }, \"aggs\": { \"intermediateAggr\": { \"terms\": { \"field\": \"date\" }, \"aggs\": { \"averageDaysToIssuePermit\": { \"avg\": { \"field\": \"averageDaysToIssuePermit\" } } } }, \"Average_Days_To_Issue_Permit\": { \"sum_bucket\": { \"buckets_path\": \"intermediateAggr.averageDaysToIssuePermit\" } } } }, \"SLA_Compliance_Permit\": { \"filter\": { \"bool\": { \"must_not\": [] } }, \"aggs\": { \"intermediateAggr\": { \"terms\": { \"field\": \"date\" }, \"aggs\": { \"slaCompliancePermit\": { \"avg\": { \"field\": \"slaCompliancePermit\" } } } }, \"Average_Days_To_Issue_Permit\": { \"sum_bucket\": { \"buckets_path\": \"intermediateAggr.slaCompliancePermit\" } } } }, \"Total_OC_Scrutinized\": { \"filter\": { \"bool\": { \"must_not\": [] } }, \"aggs\": { \"intermediateAggr\": { \"terms\": { \"field\": \"date\" }, \"aggs\": { \"ocPlansScrutinized\": { \"avg\": { \"field\": \"ocPlansScrutinized\" } } } }, \"Total_OC_Scrutinized\": { \"sum_bucket\": { \"buckets_path\": \"intermediateAggr.ocPlansScrutinized\" } } } }, \"Total_OC_Submitted\": { \"filter\": { \"bool\": { \"must_not\": [] } }, \"aggs\": { \"intermediateAggr\": { \"terms\": { \"field\": \"date\" }, \"aggs\": { \"ocSubmitted\": { \"avg\": { \"field\": \"ocSubmitted\" } } } }, \"Total_OC_Submitted\": { \"sum_bucket\": { \"buckets_path\": \"intermediateAggr.ocSubmitted\" } } } }, \"Total_OC_Issued\": { \"filter\": { \"bool\": { \"must_not\": [] } }, \"aggs\": { \"intermediateAggr\": { \"terms\": { \"field\": \"date\" }, \"aggs\": { \"ocIssued\": { \"avg\": { \"field\": \"ocIssued\" } } } }, \"Total_OC_Issued\": { \"sum_bucket\": { \"buckets_path\": \"intermediateAggr.ocIssued\" } } } }, \"Average_Days_To_Issue_OC\": { \"filter\": { \"bool\": { \"must_not\": [] } }, \"aggs\": { \"intermediateAggr\": { \"terms\": { \"field\": \"date\" }, \"aggs\": { \"averageDaysToIssueOC\": { \"avg\": { \"field\": \"averageDaysToIssueOC\" } } } }, \"Average_Days_To_Issue_OC\": { \"sum_bucket\": { \"buckets_path\": \"intermediateAggr.averageDaysToIssueOC\" } } } }, \"intermediateAggr1\": { \"terms\": { \"field\": \"date\" }, \"aggs\": { \"applicationsWithDeviation\": { \"avg\": { \"field\": \"applicationsWithDeviation\" } }, \"averageDeviation\": { \"avg\": { \"field\": \"averageDeviation\" } }, \"TotalDeviation\": { \"avg\": { \"script\": { \"params\": { \"attr\": 2 }, \"source\": \"doc['applicationsWithDeviation'].value * doc['averageDeviation'].value\" } } } } }, \"Applications With Deviation\": { \"sum_bucket\": { \"buckets_path\": \"intermediateAggr1.applicationsWithDeviation\" } }, \"Total Deviation\": { \"sum_bucket\": { \"buckets_path\": \"intermediateAggr1.TotalDeviation\" } }, \"Average_Deviation\": { \"bucket_script\": { \"buckets_path\": { \"att\": \"Applications With Deviation\", \"com\": \"Total Deviation\" }, \"script\": \"params.com / params.att\" } }, \"SLA_Compliance_OC\": { \"filter\": { \"bool\": { \"must_not\": [] } }, \"aggs\": { \"intermediateAggr\": { \"terms\": { \"field\": \"date\" }, \"aggs\": { \"slaComplianceOC\": { \"avg\": { \"field\": \"slaComplianceOC\" } } } }, \"SLA_Compliance_OC\": { \"sum_bucket\": { \"buckets_path\": \"intermediateAggr.slaComplianceOC\" } } } }, \"Total_OC_With_Deviation\": { \"filter\": { \"bool\": { \"must_not\": [] } }, \"aggs\": { \"intermediateAggr\": { \"terms\": { \"field\": \"date\" }, \"aggs\": { \"ocWithDeviation\": { \"avg\": { \"field\": \"ocWithDeviation\" } } } }, \"Total_OC_With_Deviation\": { \"sum_bucket\": { \"buckets_path\": \"intermediateAggr.ocWithDeviation\" } } } } } } } } } } "
      }
    ],
    "isMdmsEnabled": false,
    "filterKeys": [
      {"key": "state", "column": "State"}
    ],
    "chartType": "table",
    "valueType": "number",
    "action": "",
    "plotLabel": "State",
    "drillChart": "nssOBPSServiceReportDrillDownUlb",
    "aggregationPaths": [
      "Total_Collection",
      "Total_Plans_Scrutinized",
      "Total_Applications",
      "Total_Permits_Issued",
      "Average_Days_To_Issue_Permit",
      "SLA_Compliance_Permit",
      "Total_OC_Scrutinized",
      "Total_OC_Submitted",
      "Total_OC_Issued",
      "Average_Days_To_Issue_OC",
      "Average_Deviation",
      "SLA_Compliance_OC",
      "Total_OC_With_Deviation"
    ],
    "pathDataTypeMapping": [
      {
        "Total_Collection": "amount"
      },
      {
        "Total_Plans_Scrutinized": "number"
      },
      {
        "Total_Applications": "number"
      },
      {
        "Total_Permits_Issued": "number"
      },
      {
        "Average_Days_To_Issue_Permit": "number"
      },
      {
        "SLA_Compliance_Permit": "number"
      },
      {
        "Total_OC_Scrutinized": "number"
      },
      {
        "Total_OC_Submitted": "number"
      },
      {
        "Total_OC_Issued": "number"
      },
      {
        "Average_Days_To_Issue_OC": "number"
      },
      {
        "Average_Deviation": "number"
      },
      {
        "SLA_Compliance_OC": "number"
      },
      {
        "Total_OC_With_Deviation": "number"
      }
    ],
    "insight": {
    },
    "_comment": ""
  },
  "nssOBPSServiceReportDrillDownUlb": {
    "chartName": "NSS_OBPS_SERVICE_REPORT_ULB",
    "queries": [
      {
        "module": "OBPS",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\",\"ward\" : \"ward.keyword\"}",
        "dateRefField": "date",
        "indexName": "obps-national-dashboard",
        "aggrQuery": "{ \"aggs\": { \"AGGR\": { \"filter\": { \"bool\": {} }, \"aggs\": { \"ULBs\": { \"terms\": { \"field\": \"ulb.keyword\", \"size\": 1000 }, \"aggs\": { \"Total_Collection\": { \"sum\": { \"field\": \"todaysCollectionForPaymentMode\" } }, \"Total_Plans_Scrutinized\": { \"filter\": { \"bool\": { \"must_not\": [] } }, \"aggs\": { \"intermediateAggr\": { \"terms\": { \"field\": \"date\" }, \"aggs\": { \"plansScrutinized\": { \"avg\": { \"field\": \"plansScrutinized\" } } } }, \"Total_Plans_Scrutinized\": { \"sum_bucket\": { \"buckets_path\": \"intermediateAggr.plansScrutinized\" } } } }, \"Total_Applications\": { \"filter\": { \"bool\": { \"must_not\": [] } }, \"aggs\": { \"intermediateAggr\": { \"terms\": { \"field\": \"date\" }, \"aggs\": { \"applicationsSubmitted\": { \"avg\": { \"field\": \"applicationsSubmitted\" } } } }, \"Total_Applications\": { \"sum_bucket\": { \"buckets_path\": \"intermediateAggr.applicationsSubmitted\" } } } }, \"Total_Permits_Issued\": { \"sum\": { \"field\": \"permitsIssuedForRiskType\" } }, \"Average_Days_To_Issue_Permit\": { \"filter\": { \"bool\": { \"must_not\": [] } }, \"aggs\": { \"intermediateAggr\": { \"terms\": { \"field\": \"date\" }, \"aggs\": { \"averageDaysToIssuePermit\": { \"avg\": { \"field\": \"averageDaysToIssuePermit\" } } } }, \"Average_Days_To_Issue_Permit\": { \"sum_bucket\": { \"buckets_path\": \"intermediateAggr.averageDaysToIssuePermit\" } } } }, \"SLA_Compliance_Permit\": { \"filter\": { \"bool\": { \"must_not\": [] } }, \"aggs\": { \"intermediateAggr\": { \"terms\": { \"field\": \"date\" }, \"aggs\": { \"slaCompliancePermit\": { \"avg\": { \"field\": \"slaCompliancePermit\" } } } }, \"Average_Days_To_Issue_Permit\": { \"sum_bucket\": { \"buckets_path\": \"intermediateAggr.slaCompliancePermit\" } } } }, \"Total_OC_Scrutinized\": { \"filter\": { \"bool\": { \"must_not\": [] } }, \"aggs\": { \"intermediateAggr\": { \"terms\": { \"field\": \"date\" }, \"aggs\": { \"ocPlansScrutinized\": { \"avg\": { \"field\": \"ocPlansScrutinized\" } } } }, \"Total_OC_Scrutinized\": { \"sum_bucket\": { \"buckets_path\": \"intermediateAggr.ocPlansScrutinized\" } } } }, \"Total_OC_Submitted\": { \"filter\": { \"bool\": { \"must_not\": [] } }, \"aggs\": { \"intermediateAggr\": { \"terms\": { \"field\": \"date\" }, \"aggs\": { \"ocSubmitted\": { \"avg\": { \"field\": \"ocSubmitted\" } } } }, \"Total_OC_Submitted\": { \"sum_bucket\": { \"buckets_path\": \"intermediateAggr.ocSubmitted\" } } } }, \"Total_OC_Issued\": { \"filter\": { \"bool\": { \"must_not\": [] } }, \"aggs\": { \"intermediateAggr\": { \"terms\": { \"field\": \"date\" }, \"aggs\": { \"ocIssued\": { \"avg\": { \"field\": \"ocIssued\" } } } }, \"Total_OC_Issued\": { \"sum_bucket\": { \"buckets_path\": \"intermediateAggr.ocIssued\" } } } }, \"Average_Days_To_Issue_OC\": { \"filter\": { \"bool\": { \"must_not\": [] } }, \"aggs\": { \"intermediateAggr\": { \"terms\": { \"field\": \"date\" }, \"aggs\": { \"averageDaysToIssueOC\": { \"avg\": { \"field\": \"averageDaysToIssueOC\" } } } }, \"Average_Days_To_Issue_OC\": { \"sum_bucket\": { \"buckets_path\": \"intermediateAggr.averageDaysToIssueOC\" } } } }, \"intermediateAggr1\": { \"terms\": { \"field\": \"date\" }, \"aggs\": { \"applicationsWithDeviation\": { \"avg\": { \"field\": \"applicationsWithDeviation\" } }, \"averageDeviation\": { \"avg\": { \"field\": \"averageDeviation\" } }, \"TotalDeviation\": { \"avg\": { \"script\": { \"params\": { \"attr\": 2 }, \"source\": \"doc['applicationsWithDeviation'].value * doc['averageDeviation'].value\" } } } } }, \"Applications With Deviation\": { \"sum_bucket\": { \"buckets_path\": \"intermediateAggr1.applicationsWithDeviation\" } }, \"Total Deviation\": { \"sum_bucket\": { \"buckets_path\": \"intermediateAggr1.TotalDeviation\" } }, \"Average_Deviation\": { \"bucket_script\": { \"buckets_path\": { \"att\": \"Applications With Deviation\", \"com\": \"Total Deviation\" }, \"script\": \"params.com / params.att\" } }, \"SLA_Compliance_OC\": { \"filter\": { \"bool\": { \"must_not\": [] } }, \"aggs\": { \"intermediateAggr\": { \"terms\": { \"field\": \"date\" }, \"aggs\": { \"slaComplianceOC\": { \"avg\": { \"field\": \"slaComplianceOC\" } } } }, \"SLA_Compliance_OC\": { \"sum_bucket\": { \"buckets_path\": \"intermediateAggr.slaComplianceOC\" } } } }, \"Total_OC_With_Deviation\": { \"filter\": { \"bool\": { \"must_not\": [] } }, \"aggs\": { \"intermediateAggr\": { \"terms\": { \"field\": \"date\" }, \"aggs\": { \"ocWithDeviation\": { \"avg\": { \"field\": \"ocWithDeviation\" } } } }, \"Total_OC_With_Deviation\": { \"sum_bucket\": { \"buckets_path\": \"intermediateAggr.ocWithDeviation\" } } } } } } } } } } "
      }
    ],
    "isMdmsEnabled": false,
    "filterKeys": [
      {"key": "ulb", "column": "ULBs"}
    ],
    "chartType": "table",
    "valueType": "number",
    "action": "",
    "plotLabel": "ULBs",
    "drillChart": "nssOBPSServiceReportDrillDownWard",
    "aggregationPaths": [
      "Total_Collection",
      "Total_Plans_Scrutinized",
      "Total_Applications",
      "Total_Permits_Issued",
      "Average_Days_To_Issue_Permit",
      "SLA_Compliance_Permit",
      "Total_OC_Scrutinized",
      "Total_OC_Submitted",
      "Total_OC_Issued",
      "Average_Days_To_Issue_OC",
      "Average_Deviation",
      "SLA_Compliance_OC",
      "Total_OC_With_Deviation"
    ],
    "pathDataTypeMapping": [
      {
        "Total_Collection": "amount"
      },
      {
        "Total_Plans_Scrutinized": "number"
      },
      {
        "Total_Applications": "number"
      },
      {
        "Total_Permits_Issued": "number"
      },
      {
        "Average_Days_To_Issue_Permit": "number"
      },
      {
        "SLA_Compliance_Permit": "number"
      },
      {
        "Total_OC_Scrutinized": "number"
      },
      {
        "Total_OC_Submitted": "number"
      },
      {
        "Total_OC_Issued": "number"
      },
      {
        "Average_Days_To_Issue_OC": "number"
      },
      {
        "Average_Deviation": "number"
      },
      {
        "SLA_Compliance_OC": "number"
      },
      {
        "Total_OC_With_Deviation": "number"
      }
    ],
    "insight": {
    },
    "_comment": " "
  },
  "nssOBPSServiceReportDrillDownWard": {
    "chartName": "",
    "queries": [
      {
        "module": "OBPS",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\",\"ward\" : \"ward.keyword\"}",
        "dateRefField": "date",
        "indexName": "obps-national-dashboard",
        "aggrQuery": "{ \"aggs\": { \"AGGR\": { \"filter\": { \"bool\": {} }, \"aggs\": { \"Ward\": { \"terms\": { \"field\": \"ward.keyword\", \"size\": 1000 }, \"aggs\": { \"Total_Collection\": { \"sum\": { \"field\": \"todaysCollectionForPaymentMode\" } }, \"Total_Plans_Scrutinized\": { \"filter\": { \"bool\": { \"must_not\": [] } }, \"aggs\": { \"intermediateAggr\": { \"terms\": { \"field\": \"date\" }, \"aggs\": { \"plansScrutinized\": { \"avg\": { \"field\": \"plansScrutinized\" } } } }, \"Total_Plans_Scrutinized\": { \"sum_bucket\": { \"buckets_path\": \"intermediateAggr.plansScrutinized\" } } } }, \"Total_Applications\": { \"filter\": { \"bool\": { \"must_not\": [] } }, \"aggs\": { \"intermediateAggr\": { \"terms\": { \"field\": \"date\" }, \"aggs\": { \"applicationsSubmitted\": { \"avg\": { \"field\": \"applicationsSubmitted\" } } } }, \"Total_Applications\": { \"sum_bucket\": { \"buckets_path\": \"intermediateAggr.applicationsSubmitted\" } } } }, \"Total_Permits_Issued\": { \"sum\": { \"field\": \"permitsIssuedForRiskType\" } }, \"Average_Days_To_Issue_Permit\": { \"filter\": { \"bool\": { \"must_not\": [] } }, \"aggs\": { \"intermediateAggr\": { \"terms\": { \"field\": \"date\" }, \"aggs\": { \"averageDaysToIssuePermit\": { \"avg\": { \"field\": \"averageDaysToIssuePermit\" } } } }, \"Average_Days_To_Issue_Permit\": { \"sum_bucket\": { \"buckets_path\": \"intermediateAggr.averageDaysToIssuePermit\" } } } }, \"SLA_Compliance_Permit\": { \"filter\": { \"bool\": { \"must_not\": [] } }, \"aggs\": { \"intermediateAggr\": { \"terms\": { \"field\": \"date\" }, \"aggs\": { \"slaCompliancePermit\": { \"avg\": { \"field\": \"slaCompliancePermit\" } } } }, \"Average_Days_To_Issue_Permit\": { \"sum_bucket\": { \"buckets_path\": \"intermediateAggr.slaCompliancePermit\" } } } }, \"Total_OC_Scrutinized\": { \"filter\": { \"bool\": { \"must_not\": [] } }, \"aggs\": { \"intermediateAggr\": { \"terms\": { \"field\": \"date\" }, \"aggs\": { \"ocPlansScrutinized\": { \"avg\": { \"field\": \"ocPlansScrutinized\" } } } }, \"Total_OC_Scrutinized\": { \"sum_bucket\": { \"buckets_path\": \"intermediateAggr.ocPlansScrutinized\" } } } }, \"Total_OC_Submitted\": { \"filter\": { \"bool\": { \"must_not\": [] } }, \"aggs\": { \"intermediateAggr\": { \"terms\": { \"field\": \"date\" }, \"aggs\": { \"ocSubmitted\": { \"avg\": { \"field\": \"ocSubmitted\" } } } }, \"Total_OC_Submitted\": { \"sum_bucket\": { \"buckets_path\": \"intermediateAggr.ocSubmitted\" } } } }, \"Total_OC_Issued\": { \"filter\": { \"bool\": { \"must_not\": [] } }, \"aggs\": { \"intermediateAggr\": { \"terms\": { \"field\": \"date\" }, \"aggs\": { \"ocIssued\": { \"avg\": { \"field\": \"ocIssued\" } } } }, \"Total_OC_Issued\": { \"sum_bucket\": { \"buckets_path\": \"intermediateAggr.ocIssued\" } } } }, \"Average_Days_To_Issue_OC\": { \"filter\": { \"bool\": { \"must_not\": [] } }, \"aggs\": { \"intermediateAggr\": { \"terms\": { \"field\": \"date\" }, \"aggs\": { \"averageDaysToIssueOC\": { \"avg\": { \"field\": \"averageDaysToIssueOC\" } } } }, \"Average_Days_To_Issue_OC\": { \"sum_bucket\": { \"buckets_path\": \"intermediateAggr.averageDaysToIssueOC\" } } } }, \"intermediateAggr1\": { \"terms\": { \"field\": \"date\" }, \"aggs\": { \"applicationsWithDeviation\": { \"avg\": { \"field\": \"applicationsWithDeviation\" } }, \"averageDeviation\": { \"avg\": { \"field\": \"averageDeviation\" } }, \"TotalDeviation\": { \"avg\": { \"script\": { \"params\": { \"attr\": 2 }, \"source\": \"doc['applicationsWithDeviation'].value * doc['averageDeviation'].value\" } } } } }, \"Applications With Deviation\": { \"sum_bucket\": { \"buckets_path\": \"intermediateAggr1.applicationsWithDeviation\" } }, \"Total Deviation\": { \"sum_bucket\": { \"buckets_path\": \"intermediateAggr1.TotalDeviation\" } }, \"Average_Deviation\": { \"bucket_script\": { \"buckets_path\": { \"att\": \"Applications With Deviation\", \"com\": \"Total Deviation\" }, \"script\": \"params.com / params.att\" } }, \"SLA_Compliance_OC\": { \"filter\": { \"bool\": { \"must_not\": [] } }, \"aggs\": { \"intermediateAggr\": { \"terms\": { \"field\": \"date\" }, \"aggs\": { \"slaComplianceOC\": { \"avg\": { \"field\": \"slaComplianceOC\" } } } }, \"SLA_Compliance_OC\": { \"sum_bucket\": { \"buckets_path\": \"intermediateAggr.slaComplianceOC\" } } } }, \"Total_OC_With_Deviation\": { \"filter\": { \"bool\": { \"must_not\": [] } }, \"aggs\": { \"intermediateAggr\": { \"terms\": { \"field\": \"date\" }, \"aggs\": { \"ocWithDeviation\": { \"avg\": { \"field\": \"ocWithDeviation\" } } } }, \"Total_OC_With_Deviation\": { \"sum_bucket\": { \"buckets_path\": \"intermediateAggr.ocWithDeviation\" } } } } } } } } } }"
      }
    ],
    "isMdmsEnabled": false,
    "chartType": "table",
    "valueType": "number",
    "action": "",
    "filterKeys": [
    ],
    "plotLabel": "Ward",
    "drillChart": "none",
    "aggregationPaths": [
      "Total_Collection",
      "Total_Plans_Scrutinized",
      "Total_Applications",
      "Total_Permits_Issued",
      "Average_Days_To_Issue_Permit",
      "SLA_Compliance_Permit",
      "Total_OC_Scrutinized",
      "Total_OC_Submitted",
      "Total_OC_Issued",
      "Average_Days_To_Issue_OC",
      "Average_Deviation",
      "SLA_Compliance_OC",
      "Total_OC_With_Deviation"
    ],
    "pathDataTypeMapping": [
      {
        "Total_Collection": "amount"
      },
      {
        "Total_Plans_Scrutinized": "number"
      },
      {
        "Total_Applications": "number"
      },
      {
        "Total_Permits_Issued": "number"
      },
      {
        "Average_Days_To_Issue_Permit": "number"
      },
      {
        "SLA_Compliance_Permit": "number"
      },
      {
        "Total_OC_Scrutinized": "number"
      },
      {
        "Total_OC_Submitted": "number"
      },
      {
        "Total_OC_Issued": "number"
      },
      {
        "Average_Days_To_Issue_OC": "number"
      },
      {
        "Average_Deviation": "number"
      },
      {
        "SLA_Compliance_OC": "number"
      },
      {
        "Total_OC_With_Deviation": "number"
      }
    ],
    "insight": {
    },
    "_comment": ""
  }
```

[Click here to check the complete configuration](https://github.com/egovernments/configs/blob/qa/egov-dss-dashboards/dashboard-analytics/ChartApiConfig.json)

**Master Dashboard Configuration:** Master dashboard configuration is the main configuration that defines the dashboards to be painted on the screen. This includes the visualizations, their groups, the charts and the chart dimensions in terms of height and width.

```
    {
      "name": "NSS_OBPS_DASHBOARD",
      "id": "nss-obps",
      "isActive": "",
      "style": "linear",
      "visualizations": [
        {
          "row": 1,
          "name": "NSS_OBPS_DASHBOARD",
          "vizArray": [
            {
              "id": 110,
              "name": "NSS_OVERVIEW_REVENUE",
              "dimensions": {
                "height": 350,
                "width": 2
              },
              "vizType": "metric-collection",
              "noUnit": true,
              "isCollapsible": false,
              "charts": [
                {
                  "id": "nssOBPSTodaysCollection",
                  "name": "NSS_OBPS_TODAYS_COLLECTION",
                  "code": "",
                  "chartType": "metric",
                  "filter": {
                    "title": "TODAY"
                  },
                  "headers": []
                },
                {
                  "id": "nssOBPSTotalCollection",
                  "name": "NSS_OBPS_TOTAL_COLLECTION",
                  "code": "",
                  "chartType": "metric",
                  "filter": {},
                  "headers": []
                }
              ]
            },
            {
              "id": 111,
              "name": "NSS_OBPS_TOTAL_CUMULATIVE_COLLECTION",
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
                  "id": "nssOBPSCumulativeCollection",
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
          "name": "NSS_OBPS_DASHBOARD",
          "vizArray": [
            {
              "id": 210,
              "name": "NSS_OVERVIEW_SERVICES",
              "dimensions": {
                "height": 350,
                "width": 2
              },
              "vizType": "metric-collection",
              "noUnit": true,
              "isCollapsible": false,
              "charts": [
                {
                  "id": "nssOBPSTotalPlansScrutinized",
                  "name": "NSS_OBPS_TOTAL_PLANS_SCRUTINIZED",
                  "code": "",
                  "chartType": "metric",
                  "filter": "",
                  "headers": []
                },
                {
                  "id": "nssOBPSTotalPermitsIssued",
                  "name": "NSS_OBPS_TOTAL_PERMITS_ISSUED",
                  "code": "",
                  "chartType": "metric",
                  "filter": "",
                  "headers": []
                },
                {
                  "id": "nssOBPSTotalOCIssued",
                  "name": "NSS_OBPS_TOTAL_OC_ISSUED",
                  "code": "",
                  "chartType": "metric",
                  "filter": "",
                  "headers": []
                },
                {
                  "id": "nssOBPSTotalOCPlansScrutinized",
                  "name": "NSS_OBPS_TOTAL_OC_PLANS_SCRUTINIZED",
                  "code": "",
                  "chartType": "metric",
                  "filter": "",
                  "headers": []
                },
                {
                  "id": "nssOBPSAverageDaysIssuePermit",
                  "name": "NSS_OBPS_AVERAGE_DAYS_TO_ISSUE_PERMIT",
                  "code": "",
                  "chartType": "metric",
                  "filter": "",
                  "headers": []
                },
                {
                  "id": "nssOBPSAverageDaysIssueOC",
                  "name": "NSS_OBPS_AVERAGE_DAYS_TO_ISSUE_PERMIT",
                  "code": "",
                  "chartType": "metric",
                  "filter": "",
                  "headers": []
                },
                {
                  "id": "nssOBPSTotalOCSubmitted",
                  "name": "NSS_OBPS_TOTAL_OC_SUBMITTED",
                  "code": "",
                  "chartType": "metric",
                  "filter": "",
                  "headers": []
                },
                {
                  "id": "nssOBPSSlaCompliancePermit",
                  "name": "NSS_OBPS__SLA_COMPLIANCE_PERMIT",
                  "code": "",
                  "chartType": "metric",
                  "filter": "",
                  "headers": []
                },    {
                  "id": "nssOBPSSlaComplianceOC",
                  "name": "NSS_OBPS_SLA_COMPLIANCE_OC",
                  "code": "",
                  "chartType": "metric",
                  "filter": "",
                  "headers": []
                },
                {
                  "id": "nssOBPSTotalLandAreaAppliedInSystem",
                  "name": "TOTAL_Sq_m_LAND_AREA_APPLIED_IN_SYSTEM",
                  "code": "",
                  "chartType": "metric",
                  "filter": "",
                  "headers": []
                }



              ]
            },
            {
              "id": 211,
              "name": "NSS_TOTAL_PERMITS_VS_TOTAL_OC_SUBMITTED_VS_OC_ISSUED",
              "dimensions": {
                "height": 250,
                "width": 4
              },
              "vizType": "chart",
              "isCollapsible": false,
              "label": "",
              "charts": [
                {
                  "id": "nssOBPSTotalPermitsVsTotalOCSubmittedVsTotalOCIssued",
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
          "name": "NSS_OBPS_DASHBOARD",
          "vizArray": [
            {
              "id": 310,
              "name": "NSS_OBPS_COLLECTION_BY_PAYMENT_MODE",
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
                  "id": "nssOBPSCollectionByPaymentMode",
                  "name": "NSS_OBPS_COLLECTION_BY_PAYMENT_MODE",
                  "code": "",
                  "chartType": "donut",
                  "filter": "",
                  "headers": []
                }
              ]
            },
            {
              "id": 311,
              "name": "NSS_OBPS_TOP_3_PERFORMING_ULBS",
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
                  "id": "nssOBPSTopPerformingUlbs",
                  "name": "NSS_OBPS_TOP_3_PERFORMING_ULBS",
                  "code": "",
                  "chartType": "bar",
                  "filter": "",
                  "headers": []
                }
              ]
            },
            {
              "id": 312,
              "name": "NSS_OBPS_BOTTOM_3_PERFORMING_ULBS",
              "dimensions": {
                "height": 250,
                "width": 4
              },
              "vizType": "performing-metric",
              "noUnit": false,
              "isCollapsible": false,
              "charts": [
                {
                  "id": "nssOBPSBottomPerformingUlbs",
                  "name": "NSS_OBPS_BOTTOM_3_PERFORMING_ULBS",
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
          "name": "NSS_OBPS_DASHBOARD",
          "vizArray": [
            {
              "id": 410,
              "name": "NSS_OBPS_PERMIT_ISSUED_BY_RISK_TYPE",
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
                  "id": "nssOBPSPermitIssuedByRiskType",
                  "name": "NSS_OBPS_PERMIT_ISSUED_BY_RISK_TYPE",
                  "code": "",
                  "chartType": "donut",
                  "filter": "",
                  "headers": []
                }
              ]
            },
            {
              "id": 411,
              "name": "NSS_OBPS_PERMIT_ISSUED_BY_OCCUPANCY_TYPE",
              "dimensions": {
                "height": 250,
                "width": 4
              },
              "vizType": "chart",
              "noUnit": false,
              "isCollapsible": false,
              "charts": [
                {
                  "id": "nssOBPSPermitIssuedByOccupancyType",
                  "name": "NSS_OBPS_PERMIT_ISSUED_BY_OCCUPANCY_TYPE",
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
          "row": 5,
          "name": "NSS_OBPS_DASHBOARD",
          "vizArray": [
            {
              "id": 510,
              "name": "NSS_OBPS_SERVICE_REPORT",
              "dimensions": {
                "height": 350,
                "width": 12
              },
              "vizType": "chart",
              "noUnit": false,
              "isCollapsible": false,
              "charts": [
                {
                  "id": "nssOBPSServiceReport",
                  "name": "NSS_OBPS_SERVICE_REPORT_ULB",
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

**Role Dashboard Mappings Configuration:**

Master Dashboard Configuration which was explained earlier hold the list of Dashboards which are available.

Given the instance where Role Action Mapping is not maintained in the Application Service, this configuration will act as Role - Dashboard Mapping Configuration&#x20;

In this, each Role is mapped against the Dashboard which they are authorized to see

This was used earlier when the Role Action Mapping of eGov was not integrated.

Later, when the Role Action Mapping started controlling the Dashboards to be seen on the client side, this configuration was just used to enable the Dashboards for viewing.&#x20;

```
uration was just used to enable the Dashboards for viewing. 


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
          "name": "NSS OBPS",
          "id": "nss-obps"
        }
      ]
    }

  ]
}

```

[Click here to check the configuration](https://github.com/egovernments/configs/blob/qa/egov-dss-dashboards/dashboard-analytics/RoleDashboardMappingsConf.json)

**MDMS configuration to be added:** _common-masters/uiCommonConstants.json_

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
    }

```

[Click here to check the complete configuration](https://github.com/egovernments/egov-mdms-data/blob/QA/data/pb/ACCESSCONTROL-ROLEACTIONS/roleactions.json)

Action test.json:

```
 {
      "id": {{PlaceHolder1}},
      "name": "NSS Dashboard Config obps",
      "url": "/dashboard-analytics/dashboard/getDashboardConfig/nss-obps",
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
      "name": "National Dashboard OBPS",
      "url": "url",
      "displayName": "National Dashboard OBPS",
      "orderNumber": 4,
      "parentModule": "ndss-dashboard",
      "enabled": true,
      "serviceCode": "NDSS",
      "code": "null",
      "path": "NatDashboard.OBPS",
      "navigationURL": "/digit-ui/employee/dss/dashboard/nss-obps",
      "leftIcon": "places:business-center",
      "rightIcon": ""
}

```

[Click here to check the complete configuration](https://github.com/egovernments/egov-mdms-data/blob/QA/data/pb/ACCESSCONTROL-ACTIONS-TEST/actions-test.json)

OBPS-National DSS contains multiple graphs that represent OBPS data. Each graph has its own configuration that describes the chart and its type.

National DSS contains the following charts in OBPS:

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

More details about the respective charts are discussed below.

**Overview-Revenue:** this chart contains multiple data information as below in the selected time period.

* **Today's Collection -** This represents the day’s collection amount for OBPS Application Fee + Permit Fee.
* **Total Collection** - This represents the total collection amount for OBPS Application Fee + Permit Fee.

![](<../../../../.gitbook/assets/image (412).png>)

**Overview-Service:** This chart illustrates multiple data information as below for the selected time period.

* **Total Plans Scrutinized** - This represents the total number of plans submitted by an architect for scrutiny for new construction to the concerned authority.
* **Total permits issued** - This represents the total number of new permits issued by the concerned authority.
* **Total OC issued** - This represents the total number of occupancy certificates issued by the concerned authority for new construction.
* **Total sq m of land applied in the BPA system** - This represents the total area in square meters approved for construction.
* **Avg. days to issue permits** - This represents the average number of days taken to issue a permit application.
* **SLA Compliance (Permits)** - This represents the total percentage of permits issued within SLA.
* **Avg. days to issue OC** - This represents the average number of days taken to issue an OC.
* **SLA Compliance (OC)** - This represents the percentage of OCs issued within SLA

![](<../../../../.gitbook/assets/image (406).png>)

&#x20;

**Total Cumulative Collection:** This graph displays the OBPS collection amount information on a monthly base as a cumulative line graph. The graph changes as per the selected denomination amount filter.

**line** - this graph/chart is data representation on date histograms or date groupings.

![](<../../../../.gitbook/assets/image (371).png>)

**Total permits issued vs Total OC submitted vs Total OC issued:** This graph shows total permits issued vs total OC submitted vs total OC issued for a given time period in the form of a line chart.

**line** - this graph/chart is data representation on date histograms or date groupings.

![](<../../../../.gitbook/assets/image (388).png>)

**Collection by Payment Mode:** This pie chart shows the bifurcation of total collections by payment mode (online, cash, card, cheque) which is the sum of revenue collected from the OBPS module for the applied date filter.

![](<../../../../.gitbook/assets/image (393).png>)

&#x20;

**Top 3 Performing States:** This card shows the top 3 performing states/ULBs/wards based on the percentage of permits issued. Number of Permits issued / Number of applications

&#x20;![](<../../../../.gitbook/assets/image (402).png>)

Clicking on the Show More option displays the data for all states.

![](<../../../../.gitbook/assets/image (384).png>)

**Bottom 3 Performing States:** This card shows the bottom 3 performing states/ULBs/wards based on the percentage of permits issued. Number of Permits issued / Number of applications

![](<../../../../.gitbook/assets/image (372).png>)

Clicking on the Show More option displays the data for all states.

![](<../../../../.gitbook/assets/image (405).png>)

**Permits Issued by Risk Type:** This pie chart illustrates the bifurcation of total permits issued by risk type (low risk, medium risk, high risk) for the applied date filter.

![](<../../../../.gitbook/assets/image (407).png>)

**Permits Issued by Occupancy Type:** This pie chart illustrates the bifurcation of total permits issued by occupancy type (Residential, Institutional etc) for the applied date filter.

![](<../../../../.gitbook/assets/image (369).png>)

**Service Report:** This tabular chart representation graph shows information about multiple OBPS metrics like Total Collection or Total Cumulative Collection, Total Plans Scrutinized, Total applications submitted, Total permits issued, Avg. days to issue a permit, SLA Compliance (Permits), Total OC Plans scrutinized, Total OC submitted, Total OC issued, Deviation Percentage, Avg. days to issue OC, SLA Compliance (OC), and Total OCs with deviation. The table displays the data at the state level and also provides a drill down chart from state to ULB and from ULB to ward level.

![](<../../../../.gitbook/assets/image (383).png>)

Clicking on the state name provides drill-down charts representing the state-specific data.

![](<../../../../.gitbook/assets/image (419).png>)

Clicking on the ULB navigates to the display of ward-level data for the specified ULB.

![](<../../../../.gitbook/assets/image (409).png>)

#### **Newly introduced property:** <a href="#newly-introduced-property" id="newly-introduced-property"></a>

**isRoundOff**: This property is introduced to round off the decimal values. For instance, the value 25.43 uses isRoundOff property in configuration to display it as 25. The value 22.56 is rounded off to 23. This can be used for insights configuration as well for overview graph.

#### Common properties available: <a href="#common-properties-available" id="common-properties-available"></a>

**Key(eg: bpaTotalCollection):** This is the Visualization Code. This key is referred to in further visualization configurations. It is used by the client application to indicate which visualization is needed for display.

**chartName:** The name of the chart used as a label on the dashboard. The name of the chart is a detailed name. In this configuration, the chart name is added to the localization code used by the client-side.

**queries:** Some visualizations are derived from a specific data source. While some others are derived from different data sources and are combined together to get a meaningful representation. The queries of aggregation to fetch the right data in the right aggregated format are configured here.

**queries.module:** The module/domain level, on which the query is applied i.e., OBPS

**queries.indexName:** The name of the index upon which the query is executed is configured here.

**queries.aggrQuery:** The aggregation query in itself is added here. Based on the module and the index name specified, this query is attached to the filter part of the complete search request and then executed against that index.

**queries.requestQueryMap:** Client requests carry certain fields that need to be filtered. The parameters specified in the client request are different from the parameters in each of these indexed documents. In order to map the parameters of the request to the parameters of the ElasticSearch Document, this mapping is maintained.

**queries.dateRefField:** Each of these modules have separate indexes. And all of them have their own date fields. When there is a date filter applied against these visualizations, each of them has to apply it against their own date reference fields. This parameter is configured to maintain the date field and index mapping.

**chartType:** As there are different types of visualizations, this field defines what is the type of chart/visualization that should be used to represent the data.&#x20;

**Available chart types**:

**metric** - this represents the aggregated amount/value for records filtered by the aggregate as query&#x20;

**pie** - this represents the aggregated data on grouping. This is can be used to represent any line graph, bar graph, pie chart or donuts

**line** - this graph/chart is data representation on date histograms or date groupings

**perform** - this chart represents performance-wise grouping of data.

**table** - represents a form of plots and values grouped under distinct headers.&#x20;

**xtable -** represents an advanced feature of a table that has the capability to add header values.

**valueType:** In any case of data, the values which are sent for plotting, might be a percentage, sometimes an amount or sometimes just a count. This field is used to indicate the type of value that the visualization displays.

**action:** Some of the visualizations are not just aggregation on data source. There might be some cases where a post aggregation computation is required. For instance, in the case of the top 3 performing ULBs, the Target and Total Collection is obtained and then the percentage is calculated. This parameter defines the action that has to be performed on the obtained data.&#x20;

**documentType:** The type of document upon which the query has to be executed is defined here.&#x20;

**drillChart:** If there is a drill down on the visualization the code for the drill-down is added here. This is used by client services to manage drill downs.

**aggregationPaths:** all the queries have aggregation names in it. In order to fetch the value out of each aggregation response, the name of the aggregation in the query is used. These aggregation paths have the names of aggregation in it.

**insights:** shows the data in comparison to last year with arrow symbols - displays the data on how much % is increased or decreased.&#x20;

**\_comment:** display information for the “i” symbol of each visualization is maintained in this field.&#x20;

**Index Properties of National OBPS:** The index that contains data for National-OBPS is- _obps-national-dashboard_

The mapping for this index is given below:

```
PUT obps-national-dashboard/_mapping/nss
{
  "properties": {
    "applicationsSubmitted": {
      "type": "long"
    },
    "applicationsWithDeviation": {
      "type": "long"
    },
    "averageDaysToIssueOC": {
      "type": "long"
    },
    "averageDaysToIssuePermit": {
      "type": "long"
    },
    "averageDeviation": {
      "type": "long"
    },
    "date": {
      "type": "date",
      "format": "dd-MM-yyyy HH:mm:ss||dd-MM-yyyy||epoch_millis||dd-MM-yyyy'T'HH:mm:ss.SSSZ"
    },
    "landAreaAppliedInSystemForBPA": {
      "type": "long"
    },
    "module": {
      "type": "text",
      "fields": {
        "keyword": {
          "type": "keyword",
          "ignore_above": 256
        }
      }
    },
    "ocIssued": {
      "type": "long"
    },
    "ocPlansScrutinized": {
      "type": "long"
    },
    "ocSubmitted": {
      "type": "long"
    },
    "ocWithDeviation": {
      "type": "long"
    },
    "occupancyType": {
      "type": "text",
      "fields": {
        "keyword": {
          "type": "keyword",
          "ignore_above": 256
        }
      }
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
    "permitsIssuedForOccupancyType": {
      "type": "long"
    },
    "permitsIssuedForRiskType": {
      "type": "long"
    },
    "permitsIssuedForSubOccupancyType": {
      "type": "long"
    },
    "plansScrutinized": {
      "type": "long"
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
    "riskType": {
      "type": "text",
      "fields": {
        "keyword": {
          "type": "keyword",
          "ignore_above": 256
        }
      }
    },
    "slaComplianceOC": {
      "type": "long"
    },
    "slaCompliancePermit": {
      "type": "long"
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
    "subOccupancyType": {
      "type": "text",
      "fields": {
        "keyword": {
          "type": "keyword",
          "ignore_above": 256
        }
      }
    },
    "tenantId": {
      "type": "text",
      "fields": {
        "keyword": {
          "type": "keyword",
          "ignore_above": 256
        }
      }
    },
    "todaysClosedApplicationsOC": {
      "type": "long"
    },
    "todaysClosedApplicationsPermit": {
      "type": "long"
    },
    "todaysCollectionForPaymentMode": {
      "type": "long"
    },
    "todaysCompletedApplicationsWithinSLAOC": {
      "type": "long"
    },
    "todaysCompletedApplicationsWithinSLAPermit": {
      "type": "long"
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
    "ward": {
      "type": "text",
      "fields": {
        "keyword": {
          "type": "keyword",
          "ignore_above": 256
        }
      }
    }
  }
}
```

The table below describes the properties mentioned above:

| **Attributes**                                 | **Definition**                                                                                                                 | **Breakup**                                                             |
| ---------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------ | ----------------------------------------------------------------------- |
| **ulb**                                        | The district for which the data is ingested                                                                                    | Nil                                                                     |
| **region**                                     | The region for which the data is ingested                                                                                      | Nil                                                                     |
| **state**                                      | The ULB name for which the data is ingested                                                                                    | Nil                                                                     |
| **ward**                                       | The ward for which the data is ingested                                                                                        | Nil                                                                     |
| **date**                                       | The date for which the data is ingested                                                                                        | Nil                                                                     |
| **module**                                     | The name of the module for which data is ingested i.e, OBPS                                                                    | Nil                                                                     |
| **ocPlansScrutinized**                         | # of plans submitted by an architect for scrutiny for new construction to concerned authority for issuing OC on the given date | Nil                                                                     |
| **plansScrutinized**                           | # of plans submitted by an architect for scrutiny for new construction to concerned authority on the given date                | Nil                                                                     |
| **ocSubmitted**                                | # of applications submitted for OC for new construction on the given date                                                      | Nil                                                                     |
| **applicationsSubmitted**                      | # of applications submitted for building permit for new construction on the given date                                         | Nil                                                                     |
| **ocIssued**                                   | # of OC applications issued by the concerned authority on the given date                                                       | Nil                                                                     |
| **landAreaAppliedInSystemForBPA**              | total area in sq. mtr. approved for construction on the given date                                                             | Nil                                                                     |
| **averageDaysToIssuePermit**                   | # of days taken to issue a permit / Total permits issued - latest date                                                         | Nil                                                                     |
| **averageDaysToIssueOC**                       | # of days taken to issue an OC / Total OCs issued - latest date                                                                | Nil                                                                     |
| **slaCompliancePermit**                        | # of permits issued within SLA / Total permits issued - till the given date                                                    | Nil                                                                     |
| **slaComplianceOC**                            | # of OCs issued within SLA / Total OCs issued - till the given date                                                            | Nil                                                                     |
| **applicationsWithDeviation**                  | # of Permit Applications with Deviation on the given date                                                                      | Nil                                                                     |
| **averageDeviation**                           | Average deviation % for all applications with deviations on the given date                                                     | Nil                                                                     |
| **ocWithDeviation**                            | # of OC Applications with Deviation on the given date                                                                          | Nil                                                                     |
| **todaysClosedApplicationsOC**                 | # of OC Applications closed on the given date                                                                                  | Nil                                                                     |
| **todaysClosedApplicationsOC**                 | # of Permit Applications closed on the given date                                                                              | Nil                                                                     |
| **todaysCompletedApplicationsWithinSLAOC**     | # of OC Applications closed on the given date within SLA                                                                       | Nil                                                                     |
| **todaysCompletedApplicationsWithinSLAPermit** | # of Permit Applications closed on the given date within SLA                                                                   | Nil                                                                     |
| **todaysCollection**                           | Total collection related to OBPS module on a given date                                                                        | Breakup by payment mode has to be provided                              |
| **permitsIssued**                              | # of new permits issued by the concerned authority on the given date                                                           | Breakup by riskType, occupancyType, subOccupancyType has to be provided |

**Postman collection for National OBPS:**

{% embed url="https://www.getpostman.com/collections/e5f3441fb0ddc3b9bd5e" %}

&#x20;

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)\_\_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_ ](https://egov.org.in/)_is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
