# National Dashboard Service Configuration

### Recently Added Properties in ChartApiConfig  <a href="#newly-introduced-properties-in-chartapiconfig" id="newly-introduced-properties-in-chartapiconfig"></a>

#### Todays Collection <a href="#todayscollection" id="todayscollection"></a>

**Possible Values:** true/false

**Supported Chart Types:** METRIC

**How it Works:** This property is added to support the new requirement to show the Date and the last updated time in the Todays Collection Metric Chart

&#x20;![](<../../../../.gitbook/assets/image (168).png>)

Populating true for **isTodaysCollection** for a any chart config in chartApiConfig.json of type metric chart, MetricChartResponseHandler looks for **todaysDate** and **lastUpdatedTime** aggregations with the bucket(s) having epoch in key. This is used as values for todaysDate and lastUpdatedTime respectively and added to plots in the response. The UI framework is used to show the Collection on Date and lastupdate time tooltip.

**Sample Response**

```
  "aggregations" : {
    "AGGR" : {
      "meta" : { },
      "doc_count" : 256,
      "todaysDate" : {
        "doc_count_error_upper_bound" : 0,
        "sum_other_doc_count" : 240,
        "buckets" : [
          {
            "key" : 1645747200000,
            "key_as_string" : "25-02-2022 00:00:00",
            "doc_count" : 16,
            "Todays Collection" : {
              "value" : 135.0
            }
          }
        ]
      },
      "lastUpdatedTime" : {
        "doc_count_error_upper_bound" : 0,
        "sum_other_doc_count" : 16,
        "buckets" : [
          {
            "key" : 1646316682170,
            "doc_count" : 16
          }
        ]
      }
    }
  }
```

&#x20;**Sample Query**

```
{
  "aggs": {
    "AGGR": {
      "filter": {
        "bool": {}
      },
      "aggs": {
        "todaysDate": {
          "terms": {
            "field": "date",
            "order": {
              "_term": "desc"
            },
            "size": 1
          },
          "aggs": {
            "Todays Collection": {
              "sum": {
                "field": "todaysCollectionForPaymentMode"
              }
            }
          }
        },
        "lastUpdatedTime": {
          "terms": {
            "field": "lastModifiedTime",
            "order": {
              "_term": "desc"
            },
            "size": 1
          }
        }
      }
    }
  }
}
```

#### preActionTheory <a href="#preactiontheory" id="preactiontheory"></a>

**Posssible Vaues:** Map he key as one of the aggregationPaths and value as compute Helper

For instance -

```
"preActionTheory":{
      "Actual collection":"repsonseToDifferenceOfDates"
    }
```

**Supported Chart Types:** METRIC

**How it Works:** Metric Chart Type has the **action** property. Possible values include **percentage** or **undefined.** On Collecting the aggregationPath values -

* percentage is calculated if the action is percentage
* all aggregation values are summed up if the action is undefined

For TargetAchievement there is a requirement to apply `repsonseToDifferenceOfDates` compute helper on one of the aggregation path values before applying action.

The preaction theory helps to apply to compute helper before actually applying the action.

According to the above example, **responseToDifferenceOfDate** Compute helper is applied to the value of the **Actual Collection** aggregation before applying percentage calculation on all aggregation values.\
\
**National Dashboard UI Tech Documentation:**&#x20;

****[National Dashboard - UI Technical Documentation](national-dashboard-ui-technical-doc.md)

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_ ](https://egov.org.in/)_is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
