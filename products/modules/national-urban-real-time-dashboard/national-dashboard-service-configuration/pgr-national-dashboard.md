---
description: Technical Doc
---

# PGR - National Dashboard

## **Overview**

NDSS has two sides to it. One is the process in which the data is pooled to the ElasticSearch and the other is the way it is fetched, aggregated, computed, transformed and sent across.

As this revolves around a variety of data sets, there is a need for making this configurable. This ensures that the process can be configured easily in case a new scenario is introduced. This document walks us through the steps on how to define the configurations for DSS analytics for the PGR module.

## **Technical Details**

**Analytics:** Microservice responsible for building, fetching, aggregating and computing the data on ElasticSearch into a consumable data response. This is used for visualizations and graphical representations.&#x20;

**Analytics Configurations:** Analytics contains multiple configurations. Add the changes related to PGR in the dashboard-analytics. Configuration file link: [<img src="https://github.com/fluidicon.png" alt="" data-size="line">configs/egov-dss-dashboards/dashboard-analytics at qa · egovernments/configs](https://github.com/egovernments/configs/tree/qa/egov-dss-dashboards/dashboard-analytics)

Below is a list of configurations that need to be changed to run PGR successfully.

1. Chart API Configuration
2. Master Dashboard Configuration
3. Role Dashboard Mappings Configuration

**Chart API Configuration:** Each visualization has its own properties. The visualization comes from different data sources (sometimes it is a combination of different data sources).

The Chart API configuration document enables users to configure each visualisation and its properties. The visualization code is the key that has its properties configured as a part of the configuration and are easily changeable.

Sample ChartApiConfiguration.json data for National PGR:

```
"_comment": "National PGR charts below-----------------------------------------------------------------------",

  "nationalPgrTotalComplaints": {
    "chartName": "NATIONAL_DSS_TOTAL_COMPLAINTS",
    "queries": [
      {
        "module": "PGR",
        "dateRefField": "date",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "indexName": "pgr-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.service.tenantId.keyword\":\"pb.testing\"}}]}},\"aggs\":{\"Todays Complaints\":{\"sum\":{\"field\":\"todaysComplaintsForCategory\"}}}}}}"
      }
    ],
    "chartType": "metric",
    "valueType": "number",
    "drillChart": "none",
    "documentType": "_doc",
    "action": "",
    "aggregationPaths": [
      "Todays Complaints"
    ],
    "insight": {
      "chartResponseMap" : "nationalPgrTotalComplaints",
      "action" : "differenceOfNumbers",
      "upwardIndicator" : "positive",
      "downwardIndicator" : "negative",
      "isRoundOff":true,
      "textMessage" : "$indicator$value% than last $insightInterval",
      "colorCode" : "#228B22",
      "insightInterval" : "year"
    },
    "_comment": " "
  },

  "pgrClosedComplaints": {
    "chartName": "NATIONAL_DSS_CLOSED_COMPLAINTS",
    "queries": [
      {
        "module": "PGR",
        "dateRefField": "date",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "indexName": "pgr-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"ulb.keyword\":\"pb.testing\"}}]}},\"aggs\":{\"Closed_Complaints\":{\"sum\":{\"field\":\"todaysClosedComplaintsForDepartment\"}}}}}}"
      }
    ],
    "chartType": "metric",
    "valueType": "number",
    "drillChart": "none",
    "documentType": "_doc",
    "action": "",
    "aggregationPaths": [
      "Closed_Complaints"
    ],
    "insight": {
      "chartResponseMap" : "pgrClosedComplaints",
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
 
  "nationalPgrSlaAchieved": {
    "chartName": "NATIONAL_DSS_SLA_ACHIEVED",
    "queries": [
      {
        "module": "PGR",
        "dateRefField": "date",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "indexName": "pgr-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"ulb.keyword\":\"pb.testing\"}}]}},\"aggs\":{\"State\":{\"terms\":{\"field\":\"module.keyword\"},\"aggs\":{\"Test\":{\"terms\":{\"field\":\"module.keyword\"},\"aggs\":{\"Resolved_Complaints\":{\"sum\":{\"field\":\"todaysResolvedComplaintsForDepartment\"}},\"Total_Complaints\":{\"sum\":{\"field\":\"todaysComplaintsForCategory\"}}}},\"Resolved Complaints\":{\"sum_bucket\":{\"buckets_path\":\"Test.Resolved_Complaints\"}},\"Total Complaints\":{\"sum_bucket\":{\"buckets_path\":\"Test.Total_Complaints\"}},\"slaAchived\":{\"bucket_script\":{\"buckets_path\":{\"att\":\"Total Complaints\",\"com\":\"Resolved Complaints\"},\"script\":\"params.com \/ params.att * 100\"}}}}}}}}"
      }
    ],
    "chartType": "metric",
    "valueType": "percentage",
    "drillChart": "none",
    "documentType": "_doc",
    "action": "percentage",
    "isRoundOff":true,
    "aggregationPaths": [
      "slaAchived"
    ],
    "insight": {
      "chartResponseMap" : "nationalPgrSlaAchieved",
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

  "pgrCompletionRate": {
    "chartName": "NATIONAL_DSS_PGR_COMPLETION_RATE",
    "queries": [
      {
        "module":"PGR",
        "dateRefField": "date",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "indexName": "pgr-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"ulb.keyword\":\"pb.testing\"}}]}},\"aggs\":{\"State\":{\"terms\":{\"field\":\"module.keyword\"},\"aggs\":{\"Test\":{\"terms\":{\"field\":\"module.keyword\"},\"aggs\":{\"Closed_Complaints\":{\"sum\":{\"field\":\"todaysClosedComplaintsForDepartment\"}},\"Total_Complaints\":{\"sum\":{\"field\":\"todaysComplaintsForCategory\"}}}},\"Closed Complaints\":{\"sum_bucket\":{\"buckets_path\":\"Test.Closed_Complaints\"}},\"Total Complaints\":{\"sum_bucket\":{\"buckets_path\":\"Test.Total_Complaints\"}},\"Completion Rate\":{\"bucket_script\":{\"buckets_path\":{\"att\":\"Total Complaints\",\"com\":\"Closed Complaints\"},\"script\":\"params.com \/ params.att * 100\"}}}}}}}}"
      }
    ],
    "chartType": "metric",
    "valueType": "percentage",
    "drillChart": "none",
    "documentType": "_doc",
    "action": "percentage",
    "isRoundOff":true,
    "aggregationPaths": [
      "Completion Rate"
    ],
    "insight": {
      "chartResponseMap" : "pgrCompletionRate",
      "action" : "differenceOfNumbers",
      "upwardIndicator" : "positive",
      "downwardIndicator" : "negative",
      "textMessage" : "$indicator$value% than last $insightInterval",
      "colorCode" : "#228B22",
      "insightInterval" : "year",
      "isRoundOff": true
    },
    "_comment": "Completion rate"
  },

  "pgrCumulativeClosedComplaints": {
    "chartName": "NATIONAL_DSS_TOTAL_CUMULATIVE_CLOSED_COMPLAINTS",
    "queries": [
      {
        "module": "PGR",
        "dateRefField": "date",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "indexName": "pgr-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.service.tenantId.keyword\":\"pb.testing\"}}]}},\"aggs\":{\"Closed Complaints\":{\"date_histogram\":{\"field\":\"date\",\"interval\":\"month\"},\"aggs\":{\"Closed_Complaints\":{\"sum\":{\"field\":\"todaysClosedComplaintsForDepartment\"}}}},\"Reopened Complaints\":{\"date_histogram\":{\"field\":\"date\",\"interval\":\"month\"},\"aggs\":{\"Reopened\":{\"sum\":{\"field\":\"todaysReopenedComplaintsForDepartment\"}}}},\"Total Complaints\":{\"date_histogram\":{\"field\":\"date\",\"interval\":\"month\"},\"aggs\":{\"total\":{\"sum\":{\"field\":\"todaysComplaintsForCategory\"}}}}}}}}"
      }
    ],
    "chartType": "line",
    "valueType": "number",
    "action": "",
    "drillChart": "none",
    "documentType": "_doc",
    "aggregationPaths": [
      "Closed Complaints",
      "Reopened Complaints",
      "Total Complaints"
    ],
    "isCumulative": true,
    "interval": "month",
    "insight": {
    },
    "_comment": "National PGR Cumulatiove closed complaints by month area chart"
  },

  "pgrTotalComplaintsbyStatus": {
    "chartName": "NATIONAL_DSS_PGR_TOTAL_COMPLAINTS_BY_STATUS",
    "queries": [
      {
        "module": "PGR",
        "dateRefField": "date",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "indexName": "pgr-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.service.tenantId.keyword\":\"pb.testing\"}}]}},\"aggs\":{\"Resolved\":{\"date_histogram\":{\"field\":\"date\",\"interval\":\"intervalvalue\"},\"aggs\":{\"resolve\":{\"filter\":{\"terms\":{\"status.keyword\":[\"resolved\"]}},\"aggs\":{\"Count\":{\"sum\":{\"field\":\"todaysComplaintsForStatus\"}}}}}},\"Closed\":{\"date_histogram\":{\"field\":\"date\",\"interval\":\"intervalvalue\"},\"aggs\":{\"close\":{\"filter\":{\"terms\":{\"status.keyword\":[\"closed\"]}},\"aggs\":{\"Count\":{\"sum\":{\"field\":\"todaysComplaintsForStatus\"}}}}}},\"Open\":{\"date_histogram\":{\"field\":\"date\",\"interval\":\"intervalvalue\"},\"aggs\":{\"opened\":{\"filter\":{\"terms\":{\"status.keyword\":[\"open\"]}},\"aggs\":{\"Count\":{\"sum\":{\"field\":\"todaysComplaintsForStatus\"}}}}}},\"Assigned\":{\"date_histogram\":{\"field\":\"date\",\"interval\":\"intervalvalue\"},\"aggs\":{\"assign\":{\"filter\":{\"terms\":{\"status.keyword\":[\"assigned\"]}},\"aggs\":{\"Count\":{\"sum\":{\"field\":\"todaysComplaintsForStatus\"}}}}}},\"Rejected\":{\"date_histogram\":{\"field\":\"date\",\"interval\":\"intervalvalue\"},\"aggs\":{\"reject\":{\"filter\":{\"terms\":{\"status.keyword\":[\"rejected\"]}},\"aggs\":{\"Count\":{\"sum\":{\"field\":\"todaysComplaintsForStatus\"}}}}}},\"Reassign_Requested\":{\"date_histogram\":{\"field\":\"date\",\"interval\":\"intervalvalue\"},\"aggs\":{\"reassign_request\":{\"filter\":{\"terms\":{\"status.keyword\":[\"reassignrequested\"]}},\"aggs\":{\"Count\":{\"sum\":{\"field\":\"todaysComplaintsForStatus\"}}}}}}}}}}"
      }
    ],
    "chartType": "line",
    "valueType": "number",
    "action": "",
    "drillChart": "none",
    "documentType": "_doc",
    "aggregationPaths": [
      "Resolved",
      "Closed",
      "Open",
      "Assigned",
      "Rejected",
      "Reassign_Requested"
    ],
    "isCumulative": false,
    "interval": "month",
    "insight": {
    },
    "_comment": " "
  },

  "pgrComplaintsByStatusPieChart": {
    "chartName": "NATIONAL_DSS_PGR_COMPLAINTS_BY_STATUS_PIE_CHART",
    "queries": [
      {
        "module":"PGR",
        "dateRefField": "date",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "indexName": "pgr-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.service.tenantId.keyword\":\"pb.testing\"}}]}},\"aggs\":{\"Complaints By Status\":{\"terms\":{\"field\":\"status.keyword\"},\"aggs\":{\"Count\":{\"sum\":{\"field\":\"todaysComplaintsForStatus\"}}}}}}}}"
      }
    ],
    "chartType": "pie",
    "valueType": "number",
    "action": "",
    "documentType": "_doc",
    "drillChart": "none",
    "aggregationPaths": [
      "Complaints By Status"
    ],
    "insight": {
    },
    "_comment": "PGR Complaints by status"
  },

  "pgrComplaintsByDepartment": {
    "chartName": "NATIONAL_DSS_PGR_COMPLAINTS_BY_DEPARTMENT",
    "queries": [
      {
        "module":"PGR",
        "dateRefField": "date",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "indexName": "pgr-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.service.tenantId.keyword\":\"pb.testing\"}}]}},\"aggs\":{\"Complaints By Department\":{\"terms\":{\"field\":\"department.keyword\"},\"aggs\":{\"Count\":{\"sum\":{\"field\":\"todaysComplaintsForDepartment\"}}}}}}}}"
      }
    ],
    "chartType": "pie",
    "valueType": "number",
    "action": "",
    "documentType": "_doc",
    "drillChart": "none",
    "aggregationPaths": [
      "Complaints By Department"
    ],
    "insight": {
    },
    "_comment": "PGR Complaints by Department"
  },

  "pgrComplaintsByChannel": {
    "chartName": "DSS_PGR_COMPLAINTS_BY_CHANNELS",
    "queries": [
      {
        "module":"PGR",
        "dateRefField": "date",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "indexName": "pgr-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.service.tenantId.keyword\":\"pb.testing\"}}]}},\"aggs\":{\"Complaints By Channels\":{\"terms\":{\"field\":\"channel.keyword\"},\"aggs\":{\"Count\":{\"sum\":{\"field\":\"todaysComplaintsForChannel\"}}}}}}}}"
      }
    ],
    "chartType": "pie",
    "valueType": "number",
    "action": "",
    "documentType": "_doc",
    "drillChart": "none",
    "aggregationPaths": [
      "Complaints By Channels"
    ],
    "insight": {
    },
    "_comment": "PGR Channels For Complaints"
  },

  "pgrAverageSolutionTime": {
    "chartName": "NATIONAL_DSS_PGR_EVENT_DASHBOARD",
    "queries": [
      {
        "module":"PGR",
        "dateRefField": "date",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "indexName": "pgr-national-dashboard",
        "aggrQuery":"{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.service.tenantId.keyword\":\"pb.testing\"}}]}},\"aggs\":{\"Event Average Turn Around Time\":{\"date_histogram\":{\"field\":\"date\",\"interval\":\"intervalvalue\"},\"aggs\":{\"average_time\":{\"sum\":{\"field\":\"averageSolutionTimeForDepartment\"}}}}}}}}"
      }
    ],
    "chartType": "line",
    "valueType": "number",
    "action": "",
    "drillChart": "none",
    "documentType": "_doc",
    "aggregationPaths": [
      "Event Average Turn Around Time"
    ],
    "isCumulative": true,
    "interval": "month",
    "insight": {
    },
    "_comment": " "
  },

  "pgrUniqueCitizens": {
    "chartName": "NATIONAL_DSS_PGR_UNIQUE_CITIZENS",
    "queries": [
      {
        "module": "PGR",
        "dateRefField": "date",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "indexName": "pgr-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.fsm.tenantid.keyword\":\"pb.testing\"}}]}},\"aggs\":{\"Total Citizens\":{\"date_histogram\":{\"field\":\"date\",\"interval\":\"intervalvalue\"},\"aggs\":{\"state\":{\"terms\":{\"field\":\"state.keyword\"},\"aggs\":{\"intermediateAggrULB\":{\"terms\":{\"field\":\"ulb.keyword\"},\"aggs\":{\"intermediateAggrWard\":{\"terms\":{\"field\":\"ward.keyword\"},\"aggs\":{\"days\":{\"terms\":{\"field\":\"date\"},\"aggs\":{\"citizen\":{\"avg\":{\"field\":\"uniqueCitizens\"}}}},\"wardUniqueCitizens\":{\"sum_bucket\":{\"buckets_path\":\"days.citizen\"}}}},\"ulbUniqueCitizens\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrWard.wardUniqueCitizens\"}}}},\"stateUniqueCitizens\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrULB.ulbUniqueCitizens\"}}}},\"Unique Citizens\":{\"sum_bucket\":{\"buckets_path\":\"state.stateUniqueCitizens\"}}}}}}}}"
      }
    ],
    "chartType": "line",
    "valueType": "number",
    "action": "",
    "drillChart": "none",
    "documentType": "_doc",
    "aggregationPaths": [
      "Total Citizens"
    ],
    "isCumulative": false,
    "interval": "month",
    "insight": {
    },
    "_comment": " "
  },

  "pgrTopComplaints": {
    "chartName": "NATIONAL_DSS_PGR_TOP_COMPLAINTS",
  "queries": [
    {
      "module":"PGR",
      "dateRefField": "date",
      "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
      "indexName": "pgr-national-dashboard",
      "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.tenantId.keyword\":\"pb.testing\"}}]}},\"aggs\":{\"Complain Category\":{\"terms\":{\"field\":\"category.keyword\",\"order\":{\"Count\":\"desc\"}},\"aggs\":{\"Count\":{\"sum\":{\"field\":\"todaysComplaintsForCategory\"}}}}}}}}"
    }
  ],
  "chartType": "pie",
  "valueType": "number",
  "action": "",
  "documentType": "_doc",
  "drillChart": "none",
  "aggregationPaths": [
    "Complain Category"
  ],
  "insight": {
  },
  "_comment": "Top Complaints By Their Statuses"
  },

  "nationalPgrStatusByState": {
    "chartName": "NATIONAL_DSS_PGR_STATUS_BY_STATE",
    "queries": [
      {
        "module": "PGR",
        "requestQueryMap": "{\"ward\" : \"ward.keyword\",\"state\":\"state.keyword\"}",
        "dateRefField": "date",
        "indexName": "pgr-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"ulb.keyword\":\"pb.testing\"}}]}},\"aggs\":{\"State\":{\"terms\":{\"field\":\"state.keyword\"},\"aggs\":{\"Test\":{\"terms\":{\"field\":\"module.keyword\"},\"aggs\":{\"Closed_Complaints\":{\"sum\":{\"field\":\"todaysClosedComplaintsForDepartment\"}},\"Total_Complaints\":{\"sum\":{\"field\":\"todaysComplaintsForCategory\"}},\"Resolved_Complaints\":{\"sum\":{\"field\":\"todaysResolvedComplaintsForDepartment\"}}}},\"Total_Closed_Complaints\":{\"sum_bucket\":{\"buckets_path\":\"Test.Closed_Complaints\"}},\"Total Complaints\":{\"sum_bucket\":{\"buckets_path\":\"Test.Total_Complaints\"}},\"Total_Resolved_Complaints\":{\"sum_bucket\":{\"buckets_path\":\"Test.Resolved_Complaints\"}},\"Completion_Rate\":{\"bucket_script\":{\"buckets_path\":{\"att\":\"Total Complaints\",\"com\":\"Total_Closed_Complaints\"},\"script\":\"params.com \/ params.att * 100\"}},\"SLA_Achieved\":{\"bucket_script\":{\"buckets_path\":{\"att\":\"Total Complaints\",\"com\":\"Total_Resolved_Complaints\"},\"script\":\"params.com \/ params.att * 100\"}},\"Open_Complaints\":{\"sum\":{\"field\":\"todaysOpenComplaintsForDepartment\"}},\"Total_Complaints\":{\"sum\":{\"field\":\"todaysComplaintsForCategory\"}},\"Assigned_Complaints\":{\"sum\":{\"field\":\"todaysAssignedComplaintsForDepartment\"}},\"Rejected_Complaints\":{\"sum\":{\"field\":\"todaysRejectedComplaintsForDepartment\"}},\"Reassigned_Complaints\":{\"sum\":{\"field\":\"todaysReassignRequestedComplaintsForDepartment\"}},\"Reopened_Complaints\":{\"sum\":{\"field\":\"todaysReopenedComplaintsForDepartment\"}},\"Reassign_Requested\":{\"sum\":{\"field\":\"todaysReassignRequestedComplaintsForDepartment\"}}}}}}}}"
      }
    ],
    "isMdmsEnabled": false,
    "filterKeys": [
      {"key": "state", "column": "State"}
    ],
    "chartType": "xtable",
    "valueType": "number",
    "action": "",
    "plotLabel": "State",
    "isPostResponseHandler": true,
    "postAggregationTheory" : "repsonseToDifferenceOfDates",
    "documentType": "_doc",
    "drillChart": "nationalPgrStatusDrillDownUlb",
    "isRoundOff":true,
    "aggregationPaths": [
      "Total_Closed_Complaints",
      "Reopened_Complaints",
      "Open_Complaints",
      "Total_Complaints",
      "Completion_Rate",
      "SLA_Achieved",
      "Total_Resolved_Complaints",
      "Rejected_Complaints",
      "Reassigned_Complaints",
      "Assigned_Complaints",
      "Reassign_Requested"
    ],
    "pathDataTypeMapping": [
      {
        "Total_Closed_Complaints": "number"
      },
      {
        "Reopened_Complaints": "number"
      },
      {
        "Open_Complaints": "number"
      },
      {
        "Total_Complaints": "number"
      },
      {
        "Completion_Rate": "percentage"
      },
      {
        "SLA_Achieved": "percentage"
      },
      {
        "Total_Resolved_Complaints": "number"
      },
      {
        "Rejected_Complaints": "number"
      },
      {
        "Reassigned_Complaints": "number"
      },
      {
        "Assigned_Complaints": "number"
      },
      {
        "Reassign_Requested": "number"
      }
    ],
    "insight": {
    },
    "_comment": " "
  },
  
  "nationalPgrStatusDrillDownUlb": {
    "chartName": "NATIONAL_DSS_STATUS_ULB",
    "queries": [
      {
        "module": "PGR",
        "requestQueryMap": "{\"ward\" : \"ward.keyword\", \"ulb\":\"ulb.keyword\", \"state\":\"state.keyword\"}",
        "dateRefField": "date",
        "indexName": "pgr-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"ulb.keyword\":\"pb.testing\"}}]}},\"aggs\":{\"ULBs\":{\"terms\":{\"field\":\"ulb.keyword\"},\"aggs\":{\"Test\":{\"terms\":{\"field\":\"module.keyword\"},\"aggs\":{\"Closed_Complaints\":{\"sum\":{\"field\":\"todaysClosedComplaintsForDepartment\"}},\"Total_Complaints\":{\"sum\":{\"field\":\"todaysComplaintsForCategory\"}},\"Resolved_Complaints\":{\"sum\":{\"field\":\"todaysResolvedComplaintsForDepartment\"}}}},\"Total_Closed_Complaints\":{\"sum_bucket\":{\"buckets_path\":\"Test.Closed_Complaints\"}},\"Total Complaints\":{\"sum_bucket\":{\"buckets_path\":\"Test.Total_Complaints\"}},\"Total_Resolved_Complaints\":{\"sum_bucket\":{\"buckets_path\":\"Test.Resolved_Complaints\"}},\"Completion_Rate\":{\"bucket_script\":{\"buckets_path\":{\"att\":\"Total Complaints\",\"com\":\"Total_Closed_Complaints\"},\"script\":\"params.com \/ params.att * 100\"}},\"SLA_Achieved\":{\"bucket_script\":{\"buckets_path\":{\"att\":\"Total Complaints\",\"com\":\"Total_Resolved_Complaints\"},\"script\":\"params.com \/ params.att * 100\"}},\"Open_Complaints\":{\"sum\":{\"field\":\"todaysOpenComplaintsForDepartment\"}},\"Total_Complaints\":{\"sum\":{\"field\":\"todaysComplaintsForCategory\"}},\"Assigned_Complaints\":{\"sum\":{\"field\":\"todaysAssignedComplaintsForDepartment\"}},\"Rejected_Complaints\":{\"sum\":{\"field\":\"todaysRejectedComplaintsForDepartment\"}},\"Reassigned_Complaints\":{\"sum\":{\"field\":\"todaysReassignRequestedComplaintsForDepartment\"}},\"Reopened_Complaints\":{\"sum\":{\"field\":\"todaysReopenedComplaintsForDepartment\"}},\"Reassign_Requested\":{\"sum\":{\"field\":\"todaysReassignRequestedComplaintsForDepartment\"}}}}}}}}"
      }
    ],
    "isMdmsEnabled": false,
    "filterKeys": [
      {"key": "ulb", "column": "ULBs"}
    ],
    "chartType": "xtable",
    "valueType": "number",
    "action": "",
    "plotLabel": "ULBs",
    "isPostResponseHandler": true,
    "postAggregationTheory" : "repsonseToDifferenceOfDates",
    "documentType": "_doc",
    "drillChart": "nationalPgrStatusDrillDownWard",
    "isRoundOff":true,
    "aggregationPaths": [
      "Total_Closed_Complaints",
      "Reopened_Complaints",
      "Open_Complaints",
      "Total_Complaints",
      "Completion_Rate",
      "SLA_Achieved",
      "Total_Resolved_Complaints",
      "Rejected_Complaints",
      "Reassigned_Complaints",
      "Assigned_Complaints",
      "Reassign_Requested"
    ],
    "pathDataTypeMapping": [
      {
        "Total_Closed_Complaints": "number"
      },
      {
        "Reopened_Complaints": "number"
      },
      {
        "Open_Complaints": "number"
      },
      {
        "Total_Complaints": "number"
      },
      {
        "Completion_Rate": "percentage"
      },
      {
        "SLA_Achieved": "percentage"
      },
      {
        "Total_Resolved_Complaints": "number"
      },
      {
        "Rejected_Complaints": "number"
      },
      {
        "Reassigned_Complaints": "number"
      },
      {
        "Assigned_Complaints": "number"
      },
      {
        "Reassign_Requested": "number"
      }
    ],
    "insight": {
    },
    "_comment": " "
  },
   "nationalPgrStatusDrillDownWard": {
    "kind": "drillDown",
    "chartName": "Boundary",
    "queries": [
      {
        "module": "PGR",
        "requestQueryMap": "{\"ward\":\"ward.keyword\", \"state\":\"state.keyword\", \"ulb\":\"ulb.keyword\"}",
        "dateRefField": "date",
        "indexName": "pgr-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"ulb.keyword\":\"pb.testing\"}}]}},\"aggs\":{\"Ward\":{\"terms\":{\"field\":\"ward.keyword\"},\"aggs\":{\"Total_Closed_Complaints\":{\"sum\":{\"field\":\"todaysClosedComplaintsForDepartment\"}},\"Total_Resolved_Complaints\":{\"sum\":{\"field\":\"todaysResolvedComplaintsForDepartment\"}},\"SLA\":{\"terms\":{\"field\":\"date\",\"order\":{\"_term\":\"desc\"},\"size\":1},\"aggs\":{\"slaAchievement\":{\"avg\":{\"field\":\"slaAchievementForDepartment\"}}}},\"SLA_Achieved\":{\"avg_bucket\":{\"buckets_path\":\"SLA.slaAchievement\"}},\"CompletionRate\":{\"terms\":{\"field\":\"date\",\"order\":{\"_term\":\"desc\"},\"size\":1},\"aggs\":{\"rate\":{\"avg\":{\"field\":\"completionRateForDepartment\"}}}},\"Completion_Rate\":{\"avg_bucket\":{\"buckets_path\":\"CompletionRate.rate\"}},\"Open_Complaints\":{\"sum\":{\"field\":\"todaysOpenComplaintsForDepartment\"}},\"Total_Complaints\":{\"sum\":{\"field\":\"todaysComplaintsForCategory\"}},\"Assigned_Complaints\":{\"sum\":{\"field\":\"todaysAssignedComplaintsForDepartment\"}},\"Rejected_Complaints\":{\"sum\":{\"field\":\"todaysRejectedComplaintsForDepartment\"}},\"Reassigned_Complaints\":{\"sum\":{\"field\":\"todaysReassignRequestedComplaintsForDepartment\"}},\"Reopened_Complaints\":{\"sum\":{\"field\":\"todaysReopenedComplaintsForDepartment\"}},\"Reassign_Requested\":{\"sum\":{\"field\":\"todaysReassignRequestedComplaintsForDepartment\"}}}}}}}}"
      }
    ],
    "isMdmsEnabled": false,
    "chartType": "table",
    "valueType": "number",
    "action": "",
    "plotLabel": "Ward",
    "isPostResponseHandler": true,
    "postAggregationTheory" : "repsonseToDifferenceOfDates",
    "documentType": "_doc",
    "drillChart": "none",
    "isRoundOff":true,
    "aggregationPaths": [
      "Total_Closed_Complaints",
      "Reopened_Complaints",
      "Open_Complaints",
      "Total_Complaints",
      "Completion_Rate",
      "SLA_Achieved",
      "Total_Resolved_Complaints",
      "Rejected_Complaints",
      "Reassigned_Complaints",
      "Assigned_Complaints",
      "Reassign_Requested"
    ],
    "pathDataTypeMapping": [
      {
        "Total_Closed_Complaints": "number"
      },
      {
        "Reopened_Complaints": "number"
      },
      {
        "Open_Complaints": "number"
      },
      {
        "Total_Complaints": "number"
      },
      {
        "Completion_Rate": "percentage"
      },
      {
        "SLA_Achieved": "percentage"
      },
      {
        "Total_Resolved_Complaints": "number"
      },
      {
        "Rejected_Complaints": "number"
      },
      {
        "Reassigned_Complaints": "number"
      },
      {
        "Assigned_Complaints": "number"
      },
      {
        "Reassign_Requested": "number"
      }
    ],
    "insight": {
    },
    "_comment": ""
  },

  "nationalPgrStatusByDepartment": {
    "chartName": "NATIONAL_DSS_PGR_STATUS_BY_DEPARTMENT",
    "queries": [
      {
        "module": "PGR",
        "requestQueryMap": "{\"ward\" : \"ward.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "dateRefField": "date",
        "indexName": "pgr-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"ulb.keyword\":\"pb.testing\"}}]}},\"aggs\":{\"Department\":{\"terms\":{\"field\":\"department.keyword\"},\"aggs\":{\"Total_Closed_Complaints\":{\"sum\":{\"field\":\"todaysClosedComplaintsForDepartment\"}},\"Total_Resolved_Complaints\":{\"sum\":{\"field\":\"todaysResolvedComplaintsForDepartment\"}},\"Open_Complaints\":{\"sum\":{\"field\":\"todaysOpenComplaintsForDepartment\"}},\"Total_Complaints\":{\"sum\":{\"field\":\"todaysComplaintsForDepartment\"}},\"CompletionRate\":{\"terms\":{\"field\":\"date\",\"order\":{\"_term\":\"desc\"},\"size\":1},\"aggs\":{\"rate\":{\"avg\":{\"field\":\"completionRateForDepartment\"}}}},\"Completion_Rate\":{\"avg_bucket\":{\"buckets_path\":\"CompletionRate.rate\"}},\"SLA\":{\"terms\":{\"field\":\"date\",\"order\":{\"_term\":\"desc\"},\"size\":1},\"aggs\":{\"slaAchievement\":{\"avg\":{\"field\":\"slaAchievementForDepartment\"}}}},\"SLA_Achieved\":{\"avg_bucket\":{\"buckets_path\":\"SLA.slaAchievement\"}},\"Assigned_Complaints\":{\"sum\":{\"field\":\"todaysAssignedComplaintsForDepartment\"}},\"Rejected_Complaints\":{\"sum\":{\"field\":\"todaysRejectedComplaintsForDepartment\"}},\"Reassigned_Complaints\":{\"sum\":{\"field\":\"todaysReassignedComplaintsForDepartment\"}},\"Reopened_Complaints\":{\"sum\":{\"field\":\"todaysReopenedComplaintsForDepartment\"}},\"Reassign_Requested\":{\"sum\":{\"field\":\"todaysReassignRequestedComplaintsForDepartment\"}}}}}}}}"
      }
    ],
    "isMdmsEnabled": false,
    "chartType": "table",
    "valueType": "number",
    "action": "",
    "plotLabel": "Department",
    "isPostResponseHandler": true,
    "postAggregationTheory" : "repsonseToDifferenceOfDates",
    "documentType": "_doc",
    "drillChart": "none",
    "isRoundOff":true,
    "aggregationPaths": [
      "Total_Closed_Complaints",
      "Reopened_Complaints",
      "Open_Complaints",
      "Total_Complaints",
      "Completion_Rate",
      "SLA_Achieved",
      "Total_Resolved_Complaints",
      "Rejected_Complaints",
      "Reassigned_Complaints",
      "Assigned_Complaints",
      "Reassign_Requested"
    ],
    "pathDataTypeMapping": [
      {
        "Total_Closed_Complaints": "number"
      },
      {
        "Reopened_Complaints": "number"
      },
      {
        "Open_Complaints": "number"
      },
      {
        "Total_Complaints": "number"
      },
      {
        "Completion_Rate": "percentage"
      },
      {
        "SLA_Achieved": "percentage"
      },
      {
        "Total_Resolved_Complaints": "number"
      },
      {
        "Rejected_Complaints": "number"
      },
      {
        "Reassigned_Complaints": "number"
      },
      {
        "Assigned_Complaints": "number"
      },
      {
        "Reassign_Requested": "number"
      }
    ],
    "insight": {
    },
    "_comment": ""
  }
```

[Click here to check the complete configuration](https://github.com/egovernments/configs/blob/qa/egov-dss-dashboards/dashboard-analytics/ChartApiConfig.json)

**Master Dashboard Configuration:** __ Master dashboard configuration is the main configuration that defines the dashboards to be painted on the screen. This includes the visualizations, their groups, the charts and even the dimensions in terms of height and width.

```
"_comment": "National PGR charts below-----------------------------------------------------------------------",

  "nationalPgrTotalComplaints": {
    "chartName": "NATIONAL_DSS_TOTAL_COMPLAINTS",
    "queries": [
      {
        "module": "PGR",
        "dateRefField": "date",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "indexName": "pgr-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.service.tenantId.keyword\":\"pb.testing\"}}]}},\"aggs\":{\"Todays Complaints\":{\"sum\":{\"field\":\"todaysComplaintsForCategory\"}}}}}}"
      }
    ],
    "chartType": "metric",
    "valueType": "number",
    "drillChart": "none",
    "documentType": "_doc",
    "action": "",
    "aggregationPaths": [
      "Todays Complaints"
    ],
    "insight": {
      "chartResponseMap" : "nationalPgrTotalComplaints",
      "action" : "differenceOfNumbers",
      "upwardIndicator" : "positive",
      "downwardIndicator" : "negative",
      "isRoundOff":true,
      "textMessage" : "$indicator$value% than last $insightInterval",
      "colorCode" : "#228B22",
      "insightInterval" : "year",
      "isRoundOff": true
    },
    "_comment": " "
  },

  "pgrClosedComplaints": {
    "chartName": "NATIONAL_DSS_CLOSED_COMPLAINTS",
    "queries": [
      {
        "module": "PGR",
        "dateRefField": "date",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "indexName": "pgr-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"ulb.keyword\":\"pb.testing\"}}]}},\"aggs\":{\"Closed_Complaints\":{\"sum\":{\"field\":\"todaysClosedComplaintsForDepartment\"}}}}}}"
      }
    ],
    "chartType": "metric",
    "valueType": "number",
    "drillChart": "none",
    "documentType": "_doc",
    "action": "",
    "aggregationPaths": [
      "Closed_Complaints"
    ],
    "insight": {
      "chartResponseMap" : "pgrClosedComplaints",
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
 
  "nationalPgrSlaAchieved": {
    "chartName": "NATIONAL_DSS_SLA_ACHIEVED",
    "queries": [
      {
        "module": "PGR",
        "dateRefField": "date",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "indexName": "pgr-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"ulb.keyword\":\"pb.testing\"}}]}},\"aggs\":{\"State\":{\"terms\":{\"field\":\"module.keyword\"},\"aggs\":{\"Test\":{\"terms\":{\"field\":\"module.keyword\"},\"aggs\":{\"Resolved_Complaints\":{\"sum\":{\"field\":\"todaysResolvedComplaintsForDepartment\"}},\"Total_Complaints\":{\"sum\":{\"field\":\"todaysComplaintsForCategory\"}}}},\"Resolved Complaints\":{\"sum_bucket\":{\"buckets_path\":\"Test.Resolved_Complaints\"}},\"Total Complaints\":{\"sum_bucket\":{\"buckets_path\":\"Test.Total_Complaints\"}},\"slaAchived\":{\"bucket_script\":{\"buckets_path\":{\"att\":\"Total Complaints\",\"com\":\"Resolved Complaints\"},\"script\":\"params.com \/ params.att * 100\"}}}}}}}}"
      }
    ],
    "chartType": "metric",
    "valueType": "percentage",
    "drillChart": "none",
    "documentType": "_doc",
    "action": "percentage",
    "aggregationPaths": [
      "slaAchived"
    ],
    "insight": {
      "chartResponseMap" : "nationalPgrSlaAchieved",
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

  "pgrCompletionRate": {
    "chartName": "NATIONAL_DSS_PGR_COMPLETION_RATE",
    "queries": [
      {
        "module":"PGR",
        "dateRefField": "date",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "indexName": "pgr-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"ulb.keyword\":\"pb.testing\"}}]}},\"aggs\":{\"State\":{\"terms\":{\"field\":\"module.keyword\"},\"aggs\":{\"Test\":{\"terms\":{\"field\":\"module.keyword\"},\"aggs\":{\"Closed_Complaints\":{\"sum\":{\"field\":\"todaysClosedComplaintsForDepartment\"}},\"Total_Complaints\":{\"sum\":{\"field\":\"todaysComplaintsForCategory\"}}}},\"Closed Complaints\":{\"sum_bucket\":{\"buckets_path\":\"Test.Closed_Complaints\"}},\"Total Complaints\":{\"sum_bucket\":{\"buckets_path\":\"Test.Total_Complaints\"}},\"Completion Rate\":{\"bucket_script\":{\"buckets_path\":{\"att\":\"Total Complaints\",\"com\":\"Closed Complaints\"},\"script\":\"params.com \/ params.att * 100\"}}}}}}}}"
      }
    ],
    "chartType": "metric",
    "valueType": "percentage",
    "drillChart": "none",
    "documentType": "_doc",
    "action": "percentage",
    "aggregationPaths": [
      "Completion Rate"
    ],
    "insight": {
      "chartResponseMap" : "pgrCompletionRate",
      "action" : "differenceOfNumbers",
      "upwardIndicator" : "positive",
      "downwardIndicator" : "negative",
      "textMessage" : "$indicator$value% than last $insightInterval",
      "colorCode" : "#228B22",
      "insightInterval" : "year",
      "isRoundOff": true
    },
    "_comment": "Completion rate"
  },

  "pgrCumulativeClosedComplaints": {
    "chartName": "NATIONAL_DSS_TOTAL_CUMULATIVE_CLOSED_COMPLAINTS",
    "queries": [
      {
        "module": "PGR",
        "dateRefField": "date",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "indexName": "pgr-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.service.tenantId.keyword\":\"pb.testing\"}}]}},\"aggs\":{\"Closed Complaints\":{\"date_histogram\":{\"field\":\"date\",\"interval\":\"month\"},\"aggs\":{\"Closed_Complaints\":{\"sum\":{\"field\":\"todaysClosedComplaintsForDepartment\"}}}},\"Reopened Complaints\":{\"date_histogram\":{\"field\":\"date\",\"interval\":\"month\"},\"aggs\":{\"Reopened\":{\"sum\":{\"field\":\"todaysReopenedComplaintsForDepartment\"}}}},\"Total Complaints\":{\"date_histogram\":{\"field\":\"date\",\"interval\":\"month\"},\"aggs\":{\"total\":{\"sum\":{\"field\":\"todaysComplaintsForCategory\"}}}}}}}}"
      }
    ],
    "chartType": "line",
    "valueType": "number",
    "action": "",
    "drillChart": "none",
    "documentType": "_doc",
    "aggregationPaths": [
      "Closed Complaints",
      "Reopened Complaints",
      "Total Complaints"
    ],
    "isCumulative": true,
    "interval": "month",
    "insight": {
    },
    "_comment": "National PGR Cumulatiove closed complaints by month area chart"
  },

  "pgrTotalComplaintsbyStatus": {
    "chartName": "NATIONAL_DSS_PGR_TOTAL_COMPLAINTS_BY_STATUS",
    "queries": [
      {
        "module": "PGR",
        "dateRefField": "date",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "indexName": "pgr-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.service.tenantId.keyword\":\"pb.testing\"}}]}},\"aggs\":{\"Resolved\":{\"date_histogram\":{\"field\":\"date\",\"interval\":\"intervalvalue\"},\"aggs\":{\"resolve\":{\"filter\":{\"terms\":{\"status.keyword\":[\"resolved\"]}},\"aggs\":{\"Count\":{\"sum\":{\"field\":\"todaysComplaintsForStatus\"}}}}}},\"Closed\":{\"date_histogram\":{\"field\":\"date\",\"interval\":\"intervalvalue\"},\"aggs\":{\"close\":{\"filter\":{\"terms\":{\"status.keyword\":[\"closed\"]}},\"aggs\":{\"Count\":{\"sum\":{\"field\":\"todaysComplaintsForStatus\"}}}}}},\"Open\":{\"date_histogram\":{\"field\":\"date\",\"interval\":\"intervalvalue\"},\"aggs\":{\"opened\":{\"filter\":{\"terms\":{\"status.keyword\":[\"open\"]}},\"aggs\":{\"Count\":{\"sum\":{\"field\":\"todaysComplaintsForStatus\"}}}}}},\"Assigned\":{\"date_histogram\":{\"field\":\"date\",\"interval\":\"intervalvalue\"},\"aggs\":{\"assign\":{\"filter\":{\"terms\":{\"status.keyword\":[\"assigned\"]}},\"aggs\":{\"Count\":{\"sum\":{\"field\":\"todaysComplaintsForStatus\"}}}}}},\"Rejected\":{\"date_histogram\":{\"field\":\"date\",\"interval\":\"intervalvalue\"},\"aggs\":{\"reject\":{\"filter\":{\"terms\":{\"status.keyword\":[\"rejected\"]}},\"aggs\":{\"Count\":{\"sum\":{\"field\":\"todaysComplaintsForStatus\"}}}}}},\"Reassign_Requested\":{\"date_histogram\":{\"field\":\"date\",\"interval\":\"intervalvalue\"},\"aggs\":{\"reassign_request\":{\"filter\":{\"terms\":{\"status.keyword\":[\"reassignrequested\"]}},\"aggs\":{\"Count\":{\"sum\":{\"field\":\"todaysComplaintsForStatus\"}}}}}}}}}}"
      }
    ],
    "chartType": "line",
    "valueType": "number",
    "action": "",
    "drillChart": "none",
    "documentType": "_doc",
    "aggregationPaths": [
      "Resolved",
      "Closed",
      "Open",
      "Assigned",
      "Rejected",
      "Reassign_Requested"
    ],
    "isCumulative": false,
    "interval": "month",
    "insight": {
    },
    "_comment": " "
  },

  "pgrComplaintsByStatusPieChart": {
    "chartName": "NATIONAL_DSS_PGR_COMPLAINTS_BY_STATUS_PIE_CHART",
    "queries": [
      {
        "module":"PGR",
        "dateRefField": "date",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "indexName": "pgr-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.service.tenantId.keyword\":\"pb.testing\"}}]}},\"aggs\":{\"Complaints By Status\":{\"terms\":{\"field\":\"status.keyword\"},\"aggs\":{\"Count\":{\"sum\":{\"field\":\"todaysComplaintsForStatus\"}}}}}}}}"
      }
    ],
    "chartType": "pie",
    "valueType": "number",
    "action": "",
    "documentType": "_doc",
    "drillChart": "none",
    "aggregationPaths": [
      "Complaints By Status"
    ],
    "insight": {
    },
    "_comment": "PGR Complaints by status"
  },

  "pgrComplaintsByDepartment": {
    "chartName": "NATIONAL_DSS_PGR_COMPLAINTS_BY_DEPARTMENT",
    "queries": [
      {
        "module":"PGR",
        "dateRefField": "date",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "indexName": "pgr-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.service.tenantId.keyword\":\"pb.testing\"}}]}},\"aggs\":{\"Complaints By Department\":{\"terms\":{\"field\":\"department.keyword\"},\"aggs\":{\"Count\":{\"sum\":{\"field\":\"todaysComplaintsForDepartment\"}}}}}}}}"
      }
    ],
    "chartType": "pie",
    "valueType": "number",
    "action": "",
    "documentType": "_doc",
    "drillChart": "none",
    "aggregationPaths": [
      "Complaints By Department"
    ],
    "insight": {
    },
    "_comment": "PGR Complaints by Department"
  },

  "pgrComplaintsByChannel": {
    "chartName": "DSS_PGR_COMPLAINTS_BY_CHANNELS",
    "queries": [
      {
        "module":"PGR",
        "dateRefField": "date",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "indexName": "pgr-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.service.tenantId.keyword\":\"pb.testing\"}}]}},\"aggs\":{\"Complaints By Channels\":{\"terms\":{\"field\":\"channel.keyword\"},\"aggs\":{\"Count\":{\"sum\":{\"field\":\"todaysComplaintsForChannel\"}}}}}}}}"
      }
    ],
    "chartType": "pie",
    "valueType": "number",
    "action": "",
    "documentType": "_doc",
    "drillChart": "none",
    "aggregationPaths": [
      "Complaints By Channels"
    ],
    "insight": {
    },
    "_comment": "PGR Channels For Complaints"
  },

  "pgrAverageSolutionTime": {
    "chartName": "NATIONAL_DSS_PGR_EVENT_DASHBOARD",
    "queries": [
      {
        "module":"PGR",
        "dateRefField": "date",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "indexName": "pgr-national-dashboard",
        "aggrQuery":"{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.service.tenantId.keyword\":\"pb.testing\"}}]}},\"aggs\":{\"Event Average Turn Around Time\":{\"date_histogram\":{\"field\":\"date\",\"interval\":\"intervalvalue\"},\"aggs\":{\"average_time\":{\"sum\":{\"field\":\"averageSolutionTimeForDepartment\"}}}}}}}}"
      }
    ],
    "chartType": "line",
    "valueType": "number",
    "action": "",
    "drillChart": "none",
    "documentType": "_doc",
    "aggregationPaths": [
      "Event Average Turn Around Time"
    ],
    "isCumulative": true,
    "interval": "month",
    "insight": {
    },
    "_comment": " "
  },

  "pgrUniqueCitizens": {
    "chartName": "NATIONAL_DSS_PGR_UNIQUE_CITIZENS",
    "queries": [
      {
        "module": "PGR",
        "dateRefField": "date",
        "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "indexName": "pgr-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.fsm.tenantid.keyword\":\"pb.testing\"}}]}},\"aggs\":{\"Total Citizens\":{\"date_histogram\":{\"field\":\"date\",\"interval\":\"intervalvalue\"},\"aggs\":{\"state\":{\"terms\":{\"field\":\"state.keyword\"},\"aggs\":{\"intermediateAggrULB\":{\"terms\":{\"field\":\"ulb.keyword\"},\"aggs\":{\"intermediateAggrWard\":{\"terms\":{\"field\":\"ward.keyword\"},\"aggs\":{\"days\":{\"terms\":{\"field\":\"date\"},\"aggs\":{\"citizen\":{\"avg\":{\"field\":\"uniqueCitizens\"}}}},\"wardUniqueCitizens\":{\"sum_bucket\":{\"buckets_path\":\"days.citizen\"}}}},\"ulbUniqueCitizens\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrWard.wardUniqueCitizens\"}}}},\"stateUniqueCitizens\":{\"sum_bucket\":{\"buckets_path\":\"intermediateAggrULB.ulbUniqueCitizens\"}}}},\"Unique Citizens\":{\"sum_bucket\":{\"buckets_path\":\"state.stateUniqueCitizens\"}}}}}}}}"
      }
    ],
    "chartType": "line",
    "valueType": "number",
    "action": "",
    "drillChart": "none",
    "documentType": "_doc",
    "aggregationPaths": [
      "Total Citizens"
    ],
    "isCumulative": false,
    "interval": "month",
    "insight": {
    },
    "_comment": " "
  },

  "pgrTopComplaints": {
    "chartName": "NATIONAL_DSS_PGR_TOP_COMPLAINTS",
  "queries": [
    {
      "module":"PGR",
      "dateRefField": "date",
      "requestQueryMap": "{\"state\" : \"state.keyword\",\"ulb\" : \"ulb.keyword\"}",
      "indexName": "pgr-national-dashboard",
      "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"Data.tenantId.keyword\":\"pb.testing\"}}]}},\"aggs\":{\"Complain Category\":{\"terms\":{\"field\":\"category.keyword\",\"order\":{\"Count\":\"desc\"}},\"aggs\":{\"Count\":{\"sum\":{\"field\":\"todaysComplaintsForCategory\"}}}}}}}}"
    }
  ],
  "chartType": "pie",
  "valueType": "number",
  "action": "",
  "documentType": "_doc",
  "drillChart": "none",
  "aggregationPaths": [
    "Complain Category"
  ],
  "insight": {
  },
  "_comment": "Top Complaints By Their Statuses"
  },

  "nationalPgrStatusByState": {
    "chartName": "NATIONAL_DSS_PGR_STATUS_BY_STATE",
    "queries": [
      {
        "module": "PGR",
        "requestQueryMap": "{\"ward\" : \"ward.keyword\",\"state\":\"state.keyword\"}",
        "dateRefField": "date",
        "indexName": "pgr-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"ulb.keyword\":\"pb.testing\"}}]}},\"aggs\":{\"State\":{\"terms\":{\"field\":\"state.keyword\"},\"aggs\":{\"Test\":{\"terms\":{\"field\":\"module.keyword\"},\"aggs\":{\"Closed_Complaints\":{\"sum\":{\"field\":\"todaysClosedComplaintsForDepartment\"}},\"Total_Complaints\":{\"sum\":{\"field\":\"todaysComplaintsForCategory\"}},\"Resolved_Complaints\":{\"sum\":{\"field\":\"todaysResolvedComplaintsForDepartment\"}}}},\"Total_Closed_Complaints\":{\"sum_bucket\":{\"buckets_path\":\"Test.Closed_Complaints\"}},\"Total Complaints\":{\"sum_bucket\":{\"buckets_path\":\"Test.Total_Complaints\"}},\"Total_Resolved_Complaints\":{\"sum_bucket\":{\"buckets_path\":\"Test.Resolved_Complaints\"}},\"Completion_Rate\":{\"bucket_script\":{\"buckets_path\":{\"att\":\"Total Complaints\",\"com\":\"Total_Closed_Complaints\"},\"script\":\"params.com \/ params.att * 100\"}},\"SLA_Achieved\":{\"bucket_script\":{\"buckets_path\":{\"att\":\"Total Complaints\",\"com\":\"Total_Resolved_Complaints\"},\"script\":\"params.com \/ params.att * 100\"}},\"Open_Complaints\":{\"sum\":{\"field\":\"todaysOpenComplaintsForDepartment\"}},\"Total_Complaints\":{\"sum\":{\"field\":\"todaysComplaintsForCategory\"}},\"Assigned_Complaints\":{\"sum\":{\"field\":\"todaysAssignedComplaintsForDepartment\"}},\"Rejected_Complaints\":{\"sum\":{\"field\":\"todaysRejectedComplaintsForDepartment\"}},\"Reassigned_Complaints\":{\"sum\":{\"field\":\"todaysReassignRequestedComplaintsForDepartment\"}},\"Reopened_Complaints\":{\"sum\":{\"field\":\"todaysReopenedComplaintsForDepartment\"}},\"Reassign_Requested\":{\"sum\":{\"field\":\"todaysReassignRequestedComplaintsForDepartment\"}}}}}}}}"
      }
    ],
    "isMdmsEnabled": false,
    "filterKeys": [
      {"key": "state", "column": "State"}
    ],
    "chartType": "xtable",
    "valueType": "number",
    "action": "",
    "plotLabel": "State",
    "isPostResponseHandler": true,
    "postAggregationTheory" : "repsonseToDifferenceOfDates",
    "documentType": "_doc",
    "drillChart": "nationalPgrStatusDrillDownUlb",
    "aggregationPaths": [
      "Total_Closed_Complaints",
      "Reopened_Complaints",
      "Open_Complaints",
      "Total_Complaints",
      "Completion_Rate",
      "SLA_Achieved",
      "Total_Resolved_Complaints",
      "Rejected_Complaints",
      "Reassigned_Complaints",
      "Assigned_Complaints",
      "Reassign_Requested"
    ],
    "pathDataTypeMapping": [
      {
        "Total_Closed_Complaints": "number"
      },
      {
        "Reopened_Complaints": "number"
      },
      {
        "Open_Complaints": "number"
      },
      {
        "Total_Complaints": "number"
      },
      {
        "Completion_Rate": "percentage"
      },
      {
        "SLA_Achieved": "percentage"
      },
      {
        "Total_Resolved_Complaints": "number"
      },
      {
        "Rejected_Complaints": "number"
      },
      {
        "Reassigned_Complaints": "number"
      },
      {
        "Assigned_Complaints": "number"
      },
      {
        "Reassign_Requested": "number"
      }
    ],
    "insight": {
    },
    "_comment": " "
  },
  
  "nationalPgrStatusDrillDownUlb": {
    "chartName": "NATIONAL_DSS_STATUS_ULB",
    "queries": [
      {
        "module": "PGR",
        "requestQueryMap": "{\"ward\" : \"ward.keyword\", \"ulb\":\"ulb.keyword\", \"state\":\"state.keyword\"}",
        "dateRefField": "date",
        "indexName": "pgr-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"ulb.keyword\":\"pb.testing\"}}]}},\"aggs\":{\"ULBs\":{\"terms\":{\"field\":\"ulb.keyword\"},\"aggs\":{\"Test\":{\"terms\":{\"field\":\"module.keyword\"},\"aggs\":{\"Closed_Complaints\":{\"sum\":{\"field\":\"todaysClosedComplaintsForDepartment\"}},\"Total_Complaints\":{\"sum\":{\"field\":\"todaysComplaintsForCategory\"}},\"Resolved_Complaints\":{\"sum\":{\"field\":\"todaysResolvedComplaintsForDepartment\"}}}},\"Total_Closed_Complaints\":{\"sum_bucket\":{\"buckets_path\":\"Test.Closed_Complaints\"}},\"Total Complaints\":{\"sum_bucket\":{\"buckets_path\":\"Test.Total_Complaints\"}},\"Total_Resolved_Complaints\":{\"sum_bucket\":{\"buckets_path\":\"Test.Resolved_Complaints\"}},\"Completion_Rate\":{\"bucket_script\":{\"buckets_path\":{\"att\":\"Total Complaints\",\"com\":\"Total_Closed_Complaints\"},\"script\":\"params.com \/ params.att * 100\"}},\"SLA_Achieved\":{\"bucket_script\":{\"buckets_path\":{\"att\":\"Total Complaints\",\"com\":\"Total_Resolved_Complaints\"},\"script\":\"params.com \/ params.att * 100\"}},\"Open_Complaints\":{\"sum\":{\"field\":\"todaysOpenComplaintsForDepartment\"}},\"Total_Complaints\":{\"sum\":{\"field\":\"todaysComplaintsForCategory\"}},\"Assigned_Complaints\":{\"sum\":{\"field\":\"todaysAssignedComplaintsForDepartment\"}},\"Rejected_Complaints\":{\"sum\":{\"field\":\"todaysRejectedComplaintsForDepartment\"}},\"Reassigned_Complaints\":{\"sum\":{\"field\":\"todaysReassignRequestedComplaintsForDepartment\"}},\"Reopened_Complaints\":{\"sum\":{\"field\":\"todaysReopenedComplaintsForDepartment\"}},\"Reassign_Requested\":{\"sum\":{\"field\":\"todaysReassignRequestedComplaintsForDepartment\"}}}}}}}}"
      }
    ],
    "isMdmsEnabled": false,
    "filterKeys": [
      {"key": "ulb", "column": "ULBs"}
    ],
    "chartType": "xtable",
    "valueType": "number",
    "action": "",
    "plotLabel": "ULBs",
    "isPostResponseHandler": true,
    "postAggregationTheory" : "repsonseToDifferenceOfDates",
    "documentType": "_doc",
    "drillChart": "nationalPgrStatusDrillDownWard",
    "aggregationPaths": [
      "Total_Closed_Complaints",
      "Reopened_Complaints",
      "Open_Complaints",
      "Total_Complaints",
      "Completion_Rate",
      "SLA_Achieved",
      "Total_Resolved_Complaints",
      "Rejected_Complaints",
      "Reassigned_Complaints",
      "Assigned_Complaints",
      "Reassign_Requested"
    ],
    "pathDataTypeMapping": [
      {
        "Total_Closed_Complaints": "number"
      },
      {
        "Reopened_Complaints": "number"
      },
      {
        "Open_Complaints": "number"
      },
      {
        "Total_Complaints": "number"
      },
      {
        "Completion_Rate": "percentage"
      },
      {
        "SLA_Achieved": "percentage"
      },
      {
        "Total_Resolved_Complaints": "number"
      },
      {
        "Rejected_Complaints": "number"
      },
      {
        "Reassigned_Complaints": "number"
      },
      {
        "Assigned_Complaints": "number"
      },
      {
        "Reassign_Requested": "number"
      }
    ],
    "insight": {
    },
    "_comment": " "
  },
   "nationalPgrStatusDrillDownWard": {
    "kind": "drillDown",
    "chartName": "Boundary",
    "queries": [
      {
        "module": "PGR",
        "requestQueryMap": "{\"ward\":\"ward.keyword\", \"state\":\"state.keyword\", \"ulb\":\"ulb.keyword\"}",
        "dateRefField": "date",
        "indexName": "pgr-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"ulb.keyword\":\"pb.testing\"}}]}},\"aggs\":{\"Ward\":{\"terms\":{\"field\":\"ward.keyword\"},\"aggs\":{\"Total_Closed_Complaints\":{\"sum\":{\"field\":\"todaysClosedComplaintsForDepartment\"}},\"Total_Resolved_Complaints\":{\"sum\":{\"field\":\"todaysResolvedComplaintsForDepartment\"}},\"SLA\":{\"terms\":{\"field\":\"date\",\"order\":{\"_term\":\"desc\"},\"size\":1},\"aggs\":{\"slaAchievement\":{\"avg\":{\"field\":\"slaAchievementForDepartment\"}}}},\"SLA_Achieved\":{\"avg_bucket\":{\"buckets_path\":\"SLA.slaAchievement\"}},\"CompletionRate\":{\"terms\":{\"field\":\"date\",\"order\":{\"_term\":\"desc\"},\"size\":1},\"aggs\":{\"rate\":{\"avg\":{\"field\":\"completionRateForDepartment\"}}}},\"Completion_Rate\":{\"avg_bucket\":{\"buckets_path\":\"CompletionRate.rate\"}},\"Open_Complaints\":{\"sum\":{\"field\":\"todaysOpenComplaintsForDepartment\"}},\"Total_Complaints\":{\"sum\":{\"field\":\"todaysComplaintsForCategory\"}},\"Assigned_Complaints\":{\"sum\":{\"field\":\"todaysAssignedComplaintsForDepartment\"}},\"Rejected_Complaints\":{\"sum\":{\"field\":\"todaysRejectedComplaintsForDepartment\"}},\"Reassigned_Complaints\":{\"sum\":{\"field\":\"todaysReassignRequestedComplaintsForDepartment\"}},\"Reopened_Complaints\":{\"sum\":{\"field\":\"todaysReopenedComplaintsForDepartment\"}},\"Reassign_Requested\":{\"sum\":{\"field\":\"todaysReassignRequestedComplaintsForDepartment\"}}}}}}}}"
      }
    ],
    "isMdmsEnabled": false,
    "chartType": "table",
    "valueType": "number",
    "action": "",
    "plotLabel": "Ward",
    "isPostResponseHandler": true,
    "postAggregationTheory" : "repsonseToDifferenceOfDates",
    "documentType": "_doc",
    "drillChart": "none",
    "aggregationPaths": [
      "Total_Closed_Complaints",
      "Reopened_Complaints",
      "Open_Complaints",
      "Total_Complaints",
      "Completion_Rate",
      "SLA_Achieved",
      "Total_Resolved_Complaints",
      "Rejected_Complaints",
      "Reassigned_Complaints",
      "Assigned_Complaints",
      "Reassign_Requested"
    ],
    "pathDataTypeMapping": [
      {
        "Total_Closed_Complaints": "number"
      },
      {
        "Reopened_Complaints": "number"
      },
      {
        "Open_Complaints": "number"
      },
      {
        "Total_Complaints": "number"
      },
      {
        "Completion_Rate": "percentage"
      },
      {
        "SLA_Achieved": "percentage"
      },
      {
        "Total_Resolved_Complaints": "number"
      },
      {
        "Rejected_Complaints": "number"
      },
      {
        "Reassigned_Complaints": "number"
      },
      {
        "Assigned_Complaints": "number"
      },
      {
        "Reassign_Requested": "number"
      }
    ],
    "insight": {
    },
    "_comment": ""
  },

  "nationalPgrStatusByDepartment": {
    "chartName": "NATIONAL_DSS_PGR_STATUS_BY_DEPARTMENT",
    "queries": [
      {
        "module": "PGR",
        "requestQueryMap": "{\"ward\" : \"ward.keyword\",\"ulb\" : \"ulb.keyword\"}",
        "dateRefField": "date",
        "indexName": "pgr-national-dashboard",
        "aggrQuery": "{\"aggs\":{\"AGGR\":{\"filter\":{\"bool\":{\"must_not\":[{\"term\":{\"ulb.keyword\":\"pb.testing\"}}]}},\"aggs\":{\"Department\":{\"terms\":{\"field\":\"department.keyword\"},\"aggs\":{\"Total_Closed_Complaints\":{\"sum\":{\"field\":\"todaysClosedComplaintsForDepartment\"}},\"Total_Resolved_Complaints\":{\"sum\":{\"field\":\"todaysResolvedComplaintsForDepartment\"}},\"Open_Complaints\":{\"sum\":{\"field\":\"todaysOpenComplaintsForDepartment\"}},\"Total_Complaints\":{\"sum\":{\"field\":\"todaysComplaintsForDepartment\"}},\"CompletionRate\":{\"terms\":{\"field\":\"date\",\"order\":{\"_term\":\"desc\"},\"size\":1},\"aggs\":{\"rate\":{\"avg\":{\"field\":\"completionRateForDepartment\"}}}},\"Completion_Rate\":{\"avg_bucket\":{\"buckets_path\":\"CompletionRate.rate\"}},\"SLA\":{\"terms\":{\"field\":\"date\",\"order\":{\"_term\":\"desc\"},\"size\":1},\"aggs\":{\"slaAchievement\":{\"avg\":{\"field\":\"slaAchievementForDepartment\"}}}},\"SLA_Achieved\":{\"avg_bucket\":{\"buckets_path\":\"SLA.slaAchievement\"}},\"Assigned_Complaints\":{\"sum\":{\"field\":\"todaysAssignedComplaintsForDepartment\"}},\"Rejected_Complaints\":{\"sum\":{\"field\":\"todaysRejectedComplaintsForDepartment\"}},\"Reassigned_Complaints\":{\"sum\":{\"field\":\"todaysReassignedComplaintsForDepartment\"}},\"Reopened_Complaints\":{\"sum\":{\"field\":\"todaysReopenedComplaintsForDepartment\"}},\"Reassign_Requested\":{\"sum\":{\"field\":\"todaysReassignRequestedComplaintsForDepartment\"}}}}}}}}"
      }
    ],
    "isMdmsEnabled": false,
    "chartType": "table",
    "valueType": "number",
    "action": "",
    "plotLabel": "Department",
    "isPostResponseHandler": true,
    "postAggregationTheory" : "repsonseToDifferenceOfDates",
    "documentType": "_doc",
    "drillChart": "none",
    "aggregationPaths": [
      "Total_Closed_Complaints",
      "Reopened_Complaints",
      "Open_Complaints",
      "Total_Complaints",
      "Completion_Rate",
      "SLA_Achieved",
      "Total_Resolved_Complaints",
      "Rejected_Complaints",
      "Reassigned_Complaints",
      "Assigned_Complaints",
      "Reassign_Requested"
    ],
    "pathDataTypeMapping": [
      {
        "Total_Closed_Complaints": "number"
      },
      {
        "Reopened_Complaints": "number"
      },
      {
        "Open_Complaints": "number"
      },
      {
        "Total_Complaints": "number"
      },
      {
        "Completion_Rate": "percentage"
      },
      {
        "SLA_Achieved": "percentage"
      },
      {
        "Total_Resolved_Complaints": "number"
      },
      {
        "Rejected_Complaints": "number"
      },
      {
        "Reassigned_Complaints": "number"
      },
      {
        "Assigned_Complaints": "number"
      },
      {
        "Reassign_Requested": "number"
      }
    ],
    "insight": {
    },
    "_comment": ""
  }
```

[Click here for the complete configuration](https://github.com/egovernments/configs/blob/qa/egov-dss-dashboards/dashboard-analytics/MasterDashboardConfig.json)

**Role Dashboard Mappings Configuration:** Master Dashboard configuration explained earlier holds the list of available dashboards.

Given the instance where role action mapping is not maintained in the Application Service, this configuration provides the facility to map the roles to specific dashboard views. This option was used earlier when the role action mapping of eGov was not integrated. Once the role action mapping feature was integrated, this configuration was just used to enable the dashboards for viewing.&#x20;

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
          "name": "National PGR",
          "id": "national-pgr"
        }
      ]
    }
  ]
}
```

&#x20;[Click here to check the configuration](https://github.com/egovernments/configs/blob/qa/egov-dss-dashboards/dashboard-analytics/RoleDashboardMappingsConf.json)

&#x20;**MDMS Configuration to be added:** _common-masters/uiCommonConstants.json_

```
"national-pgr":{
  "routePath":"/dashboard/national-pgr",
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

Action test.json:

```
{
      "id": {{PlaceHolder1}},
      "name": "NSS Dashboard Config obps",
      "url": "/dashboard-analytics/dashboard/getDashboardConfig/national-pgr",
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
  "name": "National Dashboard pgr",
  "url": "/dashboard-analytics/dashboard/getDashboardConfig/national-pgr",
  "displayName": "National pgr",
  "orderNumber": 4,
  "parentModule": "ndss-dashboard",
  "enabled": true,
  "serviceCode": "NDSS",
  "code": "null",
  "path": "NatDashboard.PGR",
  "navigationURL": "/digit-ui/employee/dss/dashboard/national-pgr",
  "leftIcon": "places:business-center",
  "rightIcon": ""
}
```

[Click here to check the complete configuration](https://github.com/egovernments/egov-mdms-data/blob/QA/data/pb/ACCESSCONTROL-ACTIONS-TEST/actions-test.json)

The national dashboard contains multiple graphs that represent the data of the national PGR. Each graph has its own configuration that describe the chart and its type.

&#x20;**National PGR consists of the following chart:**

* Overview
* Cumulative Closed Complaints
* Total Complaints by Source
* Total Complaints by Status
* Complaint By Status
* Complaint By Department
* Complaint By Channel
* Event Duration Graph
* Unique Citizens
* Top Complaints
* Service Report

**Overview:** The overview card contains metrics data information within a selected date range.

* **Total Complaints:** Number of complaints raised by citizens or employees. This is calculated by the formula (Open Complaints + Closed Complaints).
* **Closed Complaints:** Number of complaints successfully resolved by the concerned authorities. This is calculated by the formula (Resolved Complaints + Rejected Complaints).
* **SLA Achievements:** Percentage of complaints resolved within SLA. This is calculated by the formula (Resolved complaints within SLA/Total Complaints) \* 100%
*   **Completion Rate:** This represents the completion rate of raised complaints. This is calculated by the formula (Closed Complaints / Total Complaints) \* 100%

    ![](<../../../../.gitbook/assets/image (380).png>)

**Cumulative Closed Complaints:** This graph contains the Total Complaints, Closed Complaints, and Reopened Complaints information on a monthly base in the form of cumulative line graphs. The graph changes as per the denomination amount filter selection.

**line** - this graph/chart is data representation on date histograms or date groupings.

![](<../../../../.gitbook/assets/image (348).png>)

**Complaint By Channel:** This graph shows the total number of complaints categorized by channel (eg Mobile, Web, etc) and it changes as per the denomination filter change.

![](<../../../../.gitbook/assets/image (401).png>)

**Complaint By Department:** This graph shows the total number of complaints categorized by department and it changes as per the denomination filter change.

![](<../../../../.gitbook/assets/image (413).png>)

**Complaint By Status:** This graph shows the total number of complaints categorized by status and it changes as per the denomination filter change. It shows the % of the top 4 properties, the remaining properties are reflected in the 'other' category.

![](<../../../../.gitbook/assets/image (382).png>)

**Total Complaints by Status:** This graph shows the data in horizontal bar representation and bars contain complaints categorized by status (eg Mobile App, Web, etc) in monthly wide and non-cumulative data.

![](<../../../../.gitbook/assets/image (370).png>)

**Average Solution Time:** This graph shows the average of (start to end) in a workflow, irrespective of status on a monthly basis as a line graph.

![](<../../../../.gitbook/assets/image (351).png>)

**Unique Citizens:** This graph shows the number of Unique Citizens who have filed complaints on a monthly basis as a line graph.

![](<../../../../.gitbook/assets/image (362).png>)

**Top Complaints:** This graph shows the total complaints based on category with the category having most of the registered complaints on top.

![](<../../../../.gitbook/assets/image (358).png>)

**Service Report:** This tabular chart representation graph in the form of a xtable shows multiple National PGR information like Total Complaints, Closed Complaints, Opened Complaints, Reopened Complaints, Resolved Complaints, Assigned Complaints, Reassigned Complaints, Rejected Complaints, Completion Rate (in %) and SLA Achievement (in %). The table has two tabs. The first tab shows the State level data and provides the option to drill down the chart to the ULB level and from the ULB to the ward level data. The second is the Department level view which shows the data for the department categories.

The service report contains metrics data information within a selected date range.

* **Total Complaints:** Number of complaints raised by citizens or employees. This is calculated by the formula (Open Complaints + Closed Complaints).
* **Closed Complaints:** Number of complaints successfully resolved by the concerned authorities. This is calculated by the formula (Resolved Complaints + Rejected Complaints).
* **Resolved Complaints:** Number of complaints that are marked as done by last-mile employees and await citizen feedback.
* **Open Complaints:** Number of complaints that have been filed by the citizen and await further action (assignment). This is calculated by the formula (Reopened Complaints + Assigned Complaints + Reassigned Complaints).
* **Reopened Complaints:** Number of complaints reopened by the citizen (directly/ via counter employee) due to the unsuccessful resolution of complaint earlier.
* **Assigned Complaints:** Number of complaints that have been assigned to an individual of the respective department.
* **Reassigned Complaints:** Number of complaints for which a reassignment has been requested by the last mile employee.
* **Rejected Complaints:** Number of complaints that have been terminated by the redressal officer. In such cases, citizens will have to file a new complaint.
* **SLA Achievements:** Percentage of complaints resolved within SLA. This is calculated by the formula (Resolved complaints within SLA/Total Complaints) \* 100%
* **Completion Rate:** This represents the completion rate of raised complaints. This is calculated by the formula (Closed Complaints / Total Complaints) \* 100%

_**xtable**_ type allows adding multiple computed fields with the aggregated fields dynamically added.

To add multiple computed columns, define the **computedFields** \[]  where actionName (IComputedField\<T> interface), fields \[] names as existing in query key, newField as the name that appears on the computed field column.

![](<../../../../.gitbook/assets/image (364).png>)

Clicking on any state name provides drill-down charts that represent the district-specific data:

![](<../../../../.gitbook/assets/image (376).png>)

Clicking on the ULB navigates to the ward level data for the specific ULB and each ward shows the specific data for that ward.

![](<../../../../.gitbook/assets/image (387).png>)

Clicking on the department tab navigates to the Departments and each department shows the specific data for that department.

![](<../../../../.gitbook/assets/image (408).png>)

#### **Newly introduced property:** <a href="#newly-introduced-property" id="newly-introduced-property"></a>

**isRoundOff**: This property is introduced to round off the decimal values. For instance, the value 25.43 using isRoundOff property in the configuration displays it as 25. The value 22.56 is rounded off to 23. This is used for insights configuration as well as for the overview graph.

#### Common properties available: <a href="#common-properties-available" id="common-properties-available"></a>

**Key(eg: fsmTotalrequest):** This is the visualization code. The key is referred to in further visualization configurations. This key is used by the client application to indicate which visualization is needed for display.

**chartName:** The name of the chart to be used as a label on the dashboard. The name of the chart is the detailed name. In this configuration, the name of the chart is the localization code used by the client.

**queries:** Some visualizations are derived from a specific data source. While some others are derived from different data sources and are combined together to get a meaningful representation. The queries of aggregation which are to be used to fetch out the right data in the right aggregated format are configured here.

**queries.module:** The module / domain level, on which the query should be applied on. Faecal Sludge Management is FSM.

**queries.indexName:** The name of the index upon which the query has to be executed is configured here.

**queries.aggrQuery:** The aggregation query in itself is added here. Based on the Module and the Index name specified, this query is attached to the filter part of the complete search request and then executed against that index

**queries.requestQueryMap:** Client requests carry certain fields that need to be filtered. The parameters specified in the client request are different from the parameters in each indexed document. In order to map the parameters of the request to the parameters of the ElasticSearch Document, this mapping is maintained.

**queries.dateRefField:** Each of these modules have separate indexes. And all of them have their own date fields. When there is a date filter applied against these visualizations, each of them has to apply it against their own date reference fields.

This configuration parameter maintains the date field index.

**chartType:** As there are different types of visualizations, this field defines what is the type of chart / visualization that this data should be used to represent.&#x20;

**Available chart types**

**metric** - this represents the aggregated amount/value for records filtered by the aggregate es query&#x20;

**pie** - this represents the aggregated data on grouping. This is can be used to represent any line graph, bar graph, pie chart or donuts

**line** - this graph/chart is data representation on date histograms or date groupings

**perform** - this chart represents groping data as performance-wise.

**table** - represents a form of plots and values with headers as grouped on and list of its key, values pairs.&#x20;

**xtable -** represents an advanced feature of the table - it has addition capabilities for adding header values dynamically.

**valueType:** the data values which are sent to the plot, might be a percentage, sometimes an amount and sometimes it is just a count. In order to represent them and differentiate the numbers in the form of numbers or percentages - this field allows the configuration of the type of value that the visualization illustrates.

**action:** some visualizations are not just aggregation of data sources. There might be some cases where a post aggregation computation is required.

For instance, in the case of the top 3 performing ULBs, the Target and Total Collection are obtained and then the percentage is calculated. In these kinds of cases, the parameter defines what is the action that has to be performed on that data obtained.&#x20;

**documentType:** the type of document upon which the query has to be executed is defined here.&#x20;

**drillChart:** if there is a drill down on the visualization, the code for the drill-down is added here. This is used by Client Service to manage drill downs.

**aggregationPaths:** All queries have Aggregation names in them. In order to fetch the value out of each Aggregation Responses, the name of the aggregation in the query is an easy bet. These aggregation paths have the names of Aggregation in it.

**insights:** It shows the data in comparison to last year with arrow symbols. It shows the data in terms of how much % is increased or decreased.&#x20;

**\_comment:** the display information on the “i” symbol of each visualization is maintained in this field.&#x20;

**Index Properties of National PGR:** The index contains data for National-PGR is- _pgr-national-dashboard_

The mapping for this index is given below:

```
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
    "tenantId": {
      "type": "text",
      "fields": {
        "keyword": {
          "type": "keyword",
          "ignore_above": 256
        }
      }
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
    "date": {
      "type": "date",
      "format": "dd-MM-yyyy HH:mm:ss||dd-MM-yyyy||epoch_millis||dd-MM-yyyy'T'HH:mm:ss.SSSZ"
    },
    "uniqueCitizens": {
      "type": "long"
    },
    "statusType": {
      "type": "text",
      "fields": {
        "keyword": {
          "type": "keyword",
          "ignore_above": 256
        }
      }
    },
    "todaysComplaintsGroupByStatus": {
      "type": "long"
    },
    "channelType": {
      "type": "text",
      "fields": {
        "keyword": {
          "type": "keyword",
          "ignore_above": 256
        }
      }
    },
    "todaysComplaintsGroupByChannel": {
      "type": "long"
    },
    "departmentType": {
      "type": "text",
      "fields": {
        "keyword": {
          "type": "keyword",
          "ignore_above": 256
        }
      }
    },
    "todaysComplaintsGroupByDepartment": {
      "type": "long"
    },
    "todaysReopenedComplaintsByDepartment": {
      "type": "long"
    },
    "todaysOpenComplaintsByDepartment": {
      "type": "long"
    },
    "todaysAssignedComplaintsByDepartment": {
      "type": "long"
    },
    "todaysRejectedComplaintsByDepartment": {
      "type": "long"
    },
    "todaysReassignedComplaintsByDepartment": {
      "type": "long"
    },
    "todaysReassignRequestedComplaintsByDepartment": {
      "type": "long"
    },
    "todaysClosedComplaintsByDepartment": {
      "type": "long"
    },
    "todaysResolvedComplaintsByDepartment": {
      "type": "long"
    },
    "slaAchievementByDepartment": {
      "type": "long"
    },
    "averageSolutionTimeByDepartment": {
      "type": "long"
    },
    "completionRateByDepartment": {
      "type": "long"
    },
    "categoryType": {
      "type": "text",
      "fields": {
        "keyword": {
          "type": "keyword",
          "ignore_above": 256
        }
      }
    },
    "todaysComplaintsGroupByCategory": {
      "type": "long"
    }
  }
}
```

The following table describes the properties mentioned above:

| **Attribute**                     | **Definition**                                                                                                                          | **Breakup**                                                                                                                                                                                                                                                                                      |
| --------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| ulb                               | The district or region for which the data is ingested                                                                                   | Nil                                                                                                                                                                                                                                                                                              |
| state                             | The ULB name for which the data is ingested                                                                                             | Nil                                                                                                                                                                                                                                                                                              |
| ward                              | The ward for which the data is ingested                                                                                                 | Nil                                                                                                                                                                                                                                                                                              |
| uniqueCitizens                    | Unique number of citizens who have filed a complaint on given date                                                                      | Nil                                                                                                                                                                                                                                                                                              |
| todaysComplaints                  | Number of complaints filed on given date                                                                                                | Breakup by status type(`closed`, `reassignrequested`, `open`, `assigned`, `rejected`, `resolved`), channel type(`MOBILE`, `WEB` etc), department type(`DEPT1`, `DEPT2, DEPT3` etc) and category type(`Street Light`, `Road Repair`, `Garbage Cleaning`, `Drainage Issue` etc) has to be provided |
| todaysReopenedComplaints          | Number of complaints reopened by citizen due to unsuccessful resolution till given date                                                 | Breakup by department type(`DEPT1`, `DEPT2, DEPT3` etc) has to be provided                                                                                                                                                                                                                       |
| todaysOpenComplaints              | Number of complaints that have been filed by the citizen and are yet to be assigned to the respective department till given date        | Breakup by department type(`DEPT1`, `DEPT2, DEPT3` etc) has to be provided                                                                                                                                                                                                                       |
| todaysAssignedComplaints          | Number of complaints that have been assigned to the respective department till given date                                               | Breakup by department type(`DEPT1`, `DEPT2, DEPT3` etc) has to be provided                                                                                                                                                                                                                       |
| todaysReassignRequestedComplaints | Number of complaints for which a reassignment has been requested by the last mile employee to the respective department till given date | Breakup by department type(`DEPT1`, `DEPT2, DEPT3` etc) has to be provided                                                                                                                                                                                                                       |
| todaysRejectedComplaints          | Number of complaints that have been terminated by the redressal officer to the respective department till given date                    | Breakup by department type(`DEPT1`, `DEPT2, DEPT3` etc) has to be provided                                                                                                                                                                                                                       |
| todaysReassignedComplaints        | Number of complaints that have been reassigned to the redressal officer to the respective department till given date                    | Breakup by department type(`DEPT1`, `DEPT2, DEPT3` etc) has to be provided                                                                                                                                                                                                                       |
| todaysClosedComplaints            | Number of complaints that moved to closed status on the given date                                                                      | Breakup by department type(`DEPT1`, `DEPT2, DEPT3` etc) has to be provided                                                                                                                                                                                                                       |
| todaysResolvedComplaints          | Number of complaints that moved to resolved status on the given date                                                                    | Breakup by department type(`DEPT1`, `DEPT2, DEPT3` etc) has to be provided                                                                                                                                                                                                                       |
| slaAchievement                    | Percentage of complaints that are resolved with SLA till the given date                                                                 | Breakup by department type(`DEPT1`, `DEPT2, DEPT3` etc) has to be provided                                                                                                                                                                                                                       |
| completionRate                    | Percentage of complaints that are closed till given date                                                                                | Breakup by department type(`DEPT1`, `DEPT2, DEPT3` etc) has to be provided                                                                                                                                                                                                                       |
| averageSolutionTime               | Average of (start to end) in a workflow, irrespective of status to the respective department on given date                              | Breakup by department type(`DEPT1`, `DEPT2, DEPT3` etc) has to be provided                                                                                                                                                                                                                       |

**Postman collection for pgr-national:** [https://www.getpostman.com/collections/11732dbcf9237ed73b8b](https://www.getpostman.com/collections/11732dbcf9237ed73b8b)



&#x20;

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)\_\_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_ ](https://egov.org.in/)_is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._

&#x20;
