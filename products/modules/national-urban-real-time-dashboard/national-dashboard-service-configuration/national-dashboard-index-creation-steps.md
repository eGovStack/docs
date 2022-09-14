# National Dashboard: Index Creation Steps

## Overview <a href="#overview" id="overview"></a>

This document lists the steps to be followed to create national dashboard indexes.

## Pre-requisites <a href="#pre-requisites" id="pre-requisites"></a>

* Prior Knowledge of ElasticSearch

## Index Creation Steps <a href="#steps-for-index-creation" id="steps-for-index-creation"></a>

The steps to be followed to create a **property tax** index for the national dashboard are exemplified here.

1. Open Kibana
2.  Create an index using the following query -

    `1PUT pt-national-dashboard 2{}`
3. Add corresponding field mappings for the created index -

```
 PUT pt-national-dashboard/_mapping/nss
 {
        "properties" : {
          "assessedPropertiesForUsageCategory" : {
            "type" : "long"
          },
          "assessments" : {
            "type" : "long"
          },
          "cessForUsageCategory" : {
            "type" : "long"
          },
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
          "date" : {
            "type" : "date",
            "format" : "dd-MM-yyyy HH:mm:ss||dd-MM-yyyy||epoch_millis||dd-MM-yyyy'T'HH:mm:ss.SSSZ"
          },
          "financialYear" : {
            "type" : "text",
            "fields" : {
              "keyword" : {
                "type" : "keyword",
                "ignore_above" : 256
              }
            }
          },
          "interestForUsageCategory" : {
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
          },
          "module" : {
            "type" : "text",
            "fields" : {
              "keyword" : {
                "type" : "keyword",
                "ignore_above" : 256
              }
            }
          },
          "penaltyForUsageCategory" : {
            "type" : "long"
          },
          "propertiesRegisteredForFinancialYear" : {
            "type" : "long"
          },
          "propertyTaxForUsageCategory" : {
            "type" : "long"
          },
          "rebateForUsageCategory" : {
            "type" : "long"
          },
          "region" : {
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
          "todaysClosedApplications" : {
            "type" : "long"
          },
          "todaysCollectionForUsageCategory" : {
            "type" : "long"
          },
          "todaysTotalApplications" : {
            "type" : "long"
          },
          "transactionsForUsageCategory" : {
            "type" : "long"
          },
          "ulb" : {
            "type" : "text",
            "fields" : {
              "keyword" : {
                "type" : "keyword",
                "ignore_above" : 256
              }
            }
          },
          "usageCategory" : {
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
```

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in/) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
