# National Dashboard Ingest Service

## Overview <a href="#overview" id="overview"></a>

The objective of the national-dashboard-ingest service is listed below -

1. To provide a one-stop framework for ingesting data regardless of the data source based on configuration.
2. To create provision for ingesting based on module-wise requirements which directly or indirectly requires aggregated data ingestion functionality.

## Pre-requisites <a href="#pre-requisites" id="pre-requisites"></a>

1. Prior Knowledge of Java/J2EE
2. Prior Knowledge of SpringBoot
3. Prior Knowledge of PostgresSQL
4. Prior Knowledge of REST APIs and related concepts like path parameters, headers, JSON etc.
5. Prior Knowledge of ElasticSearch

## Setup And Key Functionalities

### **Setup**

Step 1: Define the index name for the module as per your requirement in `module.index.mapping` key present in the configuration here - [<img src="https://github.com/fluidicon.png" alt="" data-size="line">DIGIT-DevOps/qa.yaml at master · egovernments/DIGIT-DevOps](https://github.com/egovernments/DIGIT-DevOps/blob/master/deploy-as-code/helm/environments/qa.yaml#L364) .

Step 2: Define the allowed metrics for the module as per your requirement in `module.fields.mapping` key present in the configuration here - [<img src="https://github.com/fluidicon.png" alt="" data-size="line">DIGIT-DevOps/qa.yaml at master · egovernments/DIGIT-DevOps](https://github.com/egovernments/DIGIT-DevOps/blob/master/deploy-as-code/helm/environments/qa.yaml#L366)

Step 3: Define the allowed group-by fields for the module as per your requirement in `module.allowed.groupby.fields.mapping` key present in the configuration here - [<img src="https://github.com/fluidicon.png" alt="" data-size="line">DIGIT-DevOps/qa.yaml at master · egovernments/DIGIT-DevOps](https://github.com/egovernments/DIGIT-DevOps/blob/master/deploy-as-code/helm/environments/qa.yaml#L368)

Step 4: Define the master data index name as per your requirement in `master.data.index` key present in the configuration here - [<img src="https://github.com/fluidicon.png" alt="" data-size="line">DIGIT-DevOps/qa.yaml at master · egovernments/DIGIT-DevOps](https://github.com/egovernments/DIGIT-DevOps/blob/master/deploy-as-code/helm/environments/qa.yaml#L365)

Step 5: Define the allowed metrics for the master data index as per your requirement in `master.module.fields.mapping` key present in the configuration here - [<img src="https://github.com/fluidicon.png" alt="" data-size="line">DIGIT-DevOps/qa.yaml at master · egovernments/DIGIT-DevOps](https://github.com/egovernments/DIGIT-DevOps/blob/master/deploy-as-code/helm/environments/qa.yaml#L367)

Step 6: Create Kafka connectors for all the modules that have been configured. A sample request for creating a trade license national dashboard Kafka connector is as follows -

```
curl --location --request POST 'http://kafka-connect.kafka-cluster:8083/connectors/' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "cms-case-es-sink9128",
    "config": {
        "connector.class": "io.confluent.connect.elasticsearch.ElasticsearchSinkConnector",
        "connection.url": "http://elasticsearch-data-v1.es-cluster:9200/",
        "type.name": "nss",
        "topics": "tl-national-dashboard",
        "key.ignore": true,
        "schemas.enable": false,
        "schema.ignore": true,
        "value.converter.schemas.enable": false,
        "key.converter": "org.apache.kafka.connect.storage.StringConverter",
        "value.converter": "org.apache.kafka.connect.json.JsonConverter",
        "batch.size": 10,
        "max.buffered.records": 500,
        "flush.timeout.ms": 600000,
        "retry.backoff.ms": 5000,
        "read.timout.ms": 10000,
        "linger.ms": 100,
        "max.in.flight.requests": 2,
        "errors.log.enable": true,
        "errors.deadletterqueue.topic.name": "nss-es-failed",
        "tasks.max": 1
    }
}'
```

Step 7: Run the national-dashboard-ingest application along with the national-dashboard-ingest-kafka-pipeline.

**Definitions**

1. Config file - A YAML (xyz.yml) file which contains configuration for running national dashboard ingest.
2. API - A REST endpoint to post data based on the configuration.

**Functionality**

1. When national dashboard ingest metrics API is hit, all the data payload lookup keys are first checked against the db to determine whether they already exist or not. The db table currently being used for storing lookup keys is `nss-ingest-data`.
2. If the record for a given date and area details is not present, the payload is then flattened and pushed to `nss-ingest-keydata` topic.
3. National dashboard ingest kafka pipeline consumer listens on `nss-ingest-keydata` topic and according to the module to which the data belongs to, pushes it to the respective topic defined in the `module.index.mapping` key.
4. Once the national dashboard ingest kafka pipeline pushes data to the respective topic, a kafka-connector then takes the flattened records from that topic and ingests to ElasticSearch.

## Deployment Details <a href="#deployment-details" id="deployment-details"></a>

1. Add configs for different modules required for National Dashboard Ingest Service and National Dashboard Kafka Pipeline service.
2. Deploy the latest version of National Dashboard Ingest and National dashboard kafka pipeline service.
3. Add Role-Action mapping for API’s.

## Integration <a href="#integration" id="integration"></a>

### Integration Scope <a href="#integration-scope" id="integration-scope"></a>

The national dashboard service is used to push aggregated data present in systems and persisting them onto elasticsearch on top of which dashboards are built for visualizing and analyzing data.

### Integration Benefits <a href="#integration-benefits" id="integration-benefits"></a>

* Can perform service-specific business logic without impacting the other module.
* In the future, if we want to expose the application to citizens then it can be done easily.

### Steps to Integration <a href="#steps-to-integration" id="steps-to-integration"></a>

1. To integrate the host of national-dashboard-ingest-service module should be overwritten in the helm chart.
2. `national-dashboard/metric/_ingest` __ should be added as the search endpoint for the config added.
3. `national-dashboard/masterdata/_ingest` __ should be added as the search endpoint for the config added.

## API Details <a href="#api-details" id="api-details"></a>

**URI**: The format of the ingest API to be used to ingest data using national-dashboard-ingest is as follows:  `national-dashboard/metric/_ingest`

**Body**: The Body consists of 2 parts: RequestInfo and Data. Data is where the aggregated data to be ingested resides. The keys given under metrics object here are metrics provided in `module.fields.mapping` present in the configuration here - [<img src="https://github.com/fluidicon.png" alt="" data-size="line">DIGIT-DevOps/qa.yaml at master · egovernments/DIGIT-DevOps](https://github.com/egovernments/DIGIT-DevOps/blob/master/deploy-as-code/helm/environments/qa.yaml#L366)

Example Ingest Request Body -

```
{
    "RequestInfo": {
        "apiId": "asset-services",
        "ver": null,
        "ts": null,
        "action": null,
        "did": null,
        "key": null,
        "msgId": "search with from and to values",
        "authToken": "82c7da0d-da73-4c35-8ea7-5b231369b4cd",
        "userInfo": {
        "id": 41737,
        "uuid": "9a81233f-e212-4035-a831-320b70e93b82",
        "userName": "NDSS1",
        "name": "National Dashboard Viewer",
        "mobileNumber": "7777888813",
        "emailId": null,
        "locale": null,
        "type": "EMPLOYEE",
        "roles": [
            {
                "name": "Employee",
                "code": "SUPERUSER",
                "tenantId": "pb.amritsar"
            },
            {
                "name": "National Dashboard Admin",
                "code": "NATADMIN",
                "tenantId": "pb.amritsar"
            },
            {
                "name": "FSM Employee Dashboard Viewer",
                "code": "FSM_DASHBOARD_VIEWER",
                "tenantId": "pb.amritsar"
            },
            {
                "name": "National Dashboard Admin",
                "code": "NATADMIN",
                "tenantId": "pb"
            }
        ],
        "active": true,
        "tenantId": "pb.amritsar",
        "permanentCity": null
    }
    },
    "Data": [
        {
        "date": "14-01-2017",
        "module": "MCOLLECT",
        "ward": "GODOWN AREA (BHABAT) - B14-SECTOR-13 - A1",
        "ulb": "pb.amritsar",
        "region": "Amritsar-MC",
        "state": "Punjab",
        "metrics": {
            "numberOfCategories": 240,
            "todaysCollection": [
                {
                    "groupBy": "paymentMode",
                    "buckets": [
                        {
                            "name": "UPI",
                            "value": 70
                        },
                        {
                            "name": "CASH",
                            "value": 45
                        },
                        {
                            "name": "DEBIT_CARD",
                            "value": 20
                        }
                    ]
                },
                {
                    "groupBy": "status",
                    "buckets": [
                        {
                            "name": "NEW",
                            "value": 70
                        },
                        {
                            "name": "DEPOSITED",
                            "value": 20
                        },
                        {
                            "name": "DISHONOURED",
                            "value": 45
                        }
                    ]
                },
                {
                    "groupBy": "category",
                    "buckets": [
                        {
                            "name": "COMMON_MASTERS_HOARDING",
                            "value": 50
                        },
                        {
                            "name": "COMMON_MASTERS_ROAD_SHOW",
                            "value": 20
                        },
                        {
                            "name": "COMMON_MASTERS_UNIPOLLS",
                            "value": 5
                        },
                        {
                            "name": "COMMON_MASTERS_AUCTION_FEE",
                            "value": 25
                        },
                        {
                            "name": "COMMON_MASTERS_USER_FEES",
                            "value": 35
                        }
                    ]
                }
            ],
            "numberOfReceipts": [
                {
                    "groupBy": "status",
                    "buckets": [
                        {
                            "name": "NEW",
                            "value": 70
                        },
                        {
                            "name": "DEPOSITED",
                            "value": 105
                        },
                        {
                            "name": "DISHONOURED",
                            "value": 50
                        }
                    ]
                },
                {
                    "groupBy": "paymentMode",
                    "buckets": [
                        {
                            "name": "CASH",
                            "value": 70
                        },
                        {
                            "name": "CHEQUE",
                            "value": 105
                        },
                        {
                            "name": "DEBIT_CARD",
                            "value": 35
                        },
                        {
                            "name": "ONLINE",
                            "value": 15
                        }
                    ]
                },
                {
                    "groupBy": "category",
                    "buckets": [
                        {
                            "name": "COMMON_MASTERS_HOARDING",
                            "value": 50
                        },
                        {
                            "name": "COMMON_MASTERS_ROAD_SHOW",
                            "value": 40
                        },
                        {
                            "name": "COMMON_MASTERS_UNIPOLLS",
                            "value": 45
                        },
                        {
                            "name": "COMMON_MASTERS_AUCTION_FEE",
                            "value": 55
                        },
                        {
                            "name": "COMMON_MASTERS_USER_FEES",
                            "value": 35
                        }
                    ]
                }
            ],
            "numberOfChallans": [
                {
                    "groupBy": "challanStatus",
                    "buckets": [
                        {
                            "name": "PAID",
                            "value": 50
                        },
                        {
                            "name": "CANCELLED",
                            "value": 105
                        },
                        {
                            "name": "ACTIVE",
                            "value": 35
                        }
                    ]
                },
                {
                    "groupBy": "category",
                    "buckets": [
                        {
                            "name": "COMMON_MASTERS_HOARDING",
                            "value": 50
                        },
                        {
                            "name": "COMMON_MASTERS_ROAD_SHOW",
                            "value": 40
                        },
                        {
                            "name": "COMMON_MASTERS_UNIPOLLS",
                            "value": 45
                        },
                        {
                            "name": "COMMON_MASTERS_AUCTION_FEE",
                            "value": 20
                        },
                        {
                            "name": "COMMON_MASTERS_USER_FEES",
                            "value": 35
                        }
                    ]
                }
            ]
        }
    }]
}
```

## Index Properties & Ingest Curls (Module-wise) <a href="#module-wise-index-properties-and-ingest-curls" id="module-wise-index-properties-and-ingest-curls"></a>

The steps for creating the index and adding the index mapping for the same are available here - [National Dashboard: Steps for index creation](https://digit-discuss.atlassian.net/wiki/spaces/EPE/pages/2093482015)

The following section contains module-wise index names, index mapping and the ingest curls for ingesting data to national dashboard indexes.

### 1. Property Tax <a href="#1.-property-tax" id="1.-property-tax"></a>

a. Index - `pt-national-dashboard`

b. Index mapping -

```
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
```

c. Ingest curl -

```
curl --location --request POST 'https://qa.digit.org/national-dashboard/metric/_ingest' \
--header 'Content-Type: application/json' \
--data-raw '{
    "RequestInfo": {
        "apiId": "asset-services",
        "ver": null,
        "ts": null,
        "action": null,
        "did": null,
        "key": null,
        "msgId": "search with from and to values",
        "authToken": "null",
        "userInfo": {
            "id": 11131,
            "uuid": "0a8ef1d4-ef5c-4061-aea5-0ac4a410b87f",
            "userName": "NDSS",
            "name": "Lata",
            "mobileNumber": "7897807878",
            "emailId": null,
            "locale": null,
            "type": "EMPLOYEE",
            "roles": [
                {
                    "name": "National Dashboard Admin",
                    "code": "NATADMIN",
                    "tenantId": "pg"
                }
            ],
            "active": true,
            "tenantId": "uk.rishikesh",
            "permanentCity": null
        }
    },
    "Data": [
        {
            "date": "23-03-2022",
            "module": "PT",
            "ward": "Block 1",
            "ulb": "uk.rishikesh",
            "region": "Rishikesh-MC",
            "state": "Uttarakhand",
            "metrics": {
                "assessments": 29,
                "todaysTotalApplications": 62,
                "todaysClosedApplications": 21,
                "propertiesRegistered": [
                    {
                        "groupBy": "financialYear",
                        "buckets": [
                            {
                                "name": "2018-19",
                                "value": 12
                            },
                            {
                                "name": "2019-20",
                                "value": 18
                            },
                            {
                                "name": "2020-21",
                                "value": 21
                            }
                        ]
                    }
                ],
                "assessedProperties": [
                    {
                        "groupBy": "usageCategory",
                        "buckets": [
                            {
                                "name": "RESIDENTIAL",
                                "value": 21
                            },
                            {
                                "name": "COMMERCIAL",
                                "value": 11
                            },
                            {
                                "name": "INDUSTRIAL",
                                "value": 13
                            }
                        ]
                    }
                ],
                "transactions": [
                    {
                        "groupBy": "usageCategory",
                        "buckets": [
                            {
                                "name": "RESIDENTIAL",
                                "value": 19
                            },
                            {
                                "name": "COMMERCIAL",
                                "value": 13
                            },
                            {
                                "name": "INDUSTRIAL",
                                "value": 13
                            }
                        ]
                    }
                ],
                "todaysCollection": [
                    {
                        "groupBy": "usageCategory",
                        "buckets": [
                            {
                                "name": "RESIDENTIAL",
                                "value": 16000
                            },
                            {
                                "name": "COMMERCIAL",
                                "value": 22500
                            },
                            {
                                "name": "INDUSTRIAL",
                                "value": 26000
                            }
                        ]
                    }
                ],
                "propertyTax": [
                    {
                        "groupBy": "usageCategory",
                        "buckets": [
                            {
                                "name": "RESIDENTIAL",
                                "value": 1200
                            },
                            {
                                "name": "COMMERCIAL",
                                "value": 2100
                            },
                            {
                                "name": "INDUSTRIAL",
                                "value": 100
                            }
                        ]
                    }
                ],
                "cess": [
                    {
                        "groupBy": "usageCategory",
                        "buckets": [
                            {
                                "name": "RESIDENTIAL",
                                "value": 1300
                            },
                            {
                                "name": "COMMERCIAL",
                                "value": 1900
                            },
                            {
                                "name": "INDUSTRIAL",
                                "value": 1000
                            }
                        ]
                    }
                ],
                "rebate": [
                    {
                        "groupBy": "usageCategory",
                        "buckets": [
                            {
                                "name": "RESIDENTIAL",
                                "value": -500
                            },
                            {
                                "name": "COMMERCIAL",
                                "value": -1200
                            },
                            {
                                "name": "INDUSTRIAL",
                                "value": -900
                            }
                        ]
                    }
                ],
                "penalty": [
                    {
                        "groupBy": "usageCategory",
                        "buckets": [
                            {
                                "name": "RESIDENTIAL",
                                "value": 1300
                            },
                            {
                                "name": "COMMERCIAL",
                                "value": 1500
                            },
                            {
                                "name": "INDUSTRIAL",
                                "value": 1500
                            }
                        ]
                    }
                ],
                "interest": [
                    {
                        "groupBy": "usageCategory",
                        "buckets": [
                            {
                                "name": "RESIDENTIAL",
                                "value": 1900
                            },
                            {
                                "name": "COMMERCIAL",
                                "value": 1800
                            },
                            {
                                "name": "INDUSTRIAL",
                                "value": 600
                            }
                        ]
                    }
                ]
            }
        }
    ]
}'
```

### &#x20;2. Water and Sewerage&#x20;

a. Index name - `ws-national-dashboard`

b. Index mapping -

```
"properties" : {
          "channelType" : {
            "type" : "text",
            "fields" : {
              "keyword" : {
                "type" : "keyword",
                "ignore_above" : 256
              }
            }
          },
          "connectionType" : {
            "type" : "text",
            "fields" : {
              "keyword" : {
                "type" : "keyword",
                "ignore_above" : 256
              }
            }
          },
          "connectionsCreatedForChannelType" : {
            "type" : "long"
          },
          "connectionsCreatedForConnectionType" : {
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
          "duration" : {
            "type" : "text",
            "fields" : {
              "keyword" : {
                "type" : "keyword",
                "ignore_above" : 256
              }
            }
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
          "meterType" : {
            "type" : "text",
            "fields" : {
              "keyword" : {
                "type" : "keyword",
                "ignore_above" : 256
              }
            }
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
          "paymentChannelType" : {
            "type" : "text",
            "fields" : {
              "keyword" : {
                "type" : "keyword",
                "ignore_above" : 256
              }
            }
          },
          "pendingConnectionsForDuration" : {
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
          "sewerageConnectionsForChannelType" : {
            "type" : "long"
          },
          "sewerageConnectionsForUsageType" : {
            "type" : "long"
          },
          "slaCompliance" : {
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
          "taxHeads" : {
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
          "todaysClosedApplications" : {
            "type" : "long"
          },
          "todaysCollectionForChannelType" : {
            "type" : "long"
          },
          "todaysCollectionForConnectionType" : {
            "type" : "long"
          },
          "todaysCollectionForPaymentChannelType" : {
            "type" : "long"
          },
          "todaysCollectionForTaxHeads" : {
            "type" : "long"
          },
          "todaysCollectionForUsageType" : {
            "type" : "long"
          },
          "todaysCompletedApplicationsWithinSLA" : {
            "type" : "long"
          },
          "todaysTotalApplications" : {
            "type" : "long"
          },
          "transactions" : {
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
          "usageType" : {
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
          },
          "waterConnectionsForChannelType" : {
            "type" : "long"
          },
          "waterConnectionsForMeterType" : {
            "type" : "long"
          },
          "waterConnectionsForUsageType" : {
            "type" : "long"
          }
        }
```

c. Ingest curl -

```
curl --location --request POST 'https://qa.digit.org/national-dashboard/metric/_ingest' \
--header 'Content-Type: application/json' \
--data-raw '{
    "RequestInfo": {
        "apiId": "asset-services",
        "ver": null,
        "ts": null,
        "action": null,
        "did": null,
        "key": null,
        "msgId": "search with from and to values",
        "authToken": "{{access_token}}",
         "userInfo": {
             "id": 11131,
        "uuid": "0a8ef1d4-ef5c-4061-aea5-0ac4a410b87f",
        "userName": "NDSS",
        "name": "Lata",
        "mobileNumber": "7897807878",
        "emailId": null,
        "locale": null,
        "type": "EMPLOYEE",
        "roles": [
            {
                "name": "National Dashboard Admin",
                "code": "NATADMIN",
                "tenantId": "pg"
            }
        ],
        "active": true,
        "tenantId": "pb.amritsar",
        "permanentCity": null
        }
    },
    "Data": [
      {
            "date": "20-02-2022",
            "module": "WS",
            "ward": "Ward 1",
            "ulb": "pb.amritsar",
            "region": "Amritsar-MC",
            "state": "Punjab",
            "metrics": {
                "transactions": 2345,
                "connectionsCreated": [
                    {
                        "groupBy": "connectionType",
                        "buckets": [
                            {
                                "name": "WATER.METERED",
                                "value": 110
                            },
                            {
                                "name": "WATER.NONMETERED",
                                "value": 50
                            },
                            {
                                "name": "SEWERAGE",
                                "value": 50
                            }
                        ]
                    },
                    {
                        "groupBy": "channelType",
                        "buckets": [
                            {
                                "name": "Counter",
                                "value": 60
                            },
                            {
                                "name": "Online",
                                "value": 70
                            },
                            {
                                "name": "System",
                                "value": 50
                            },
                            {
                                "name": "CSC",
                                "value": 30
                            }
                        ]
                    }
                ],
                "todaysCollection": [
                    {
                        "groupBy": "usageType",
                        "buckets": [
                            {
                                "name": "Domestic",
                                "value": 11000
                            },
                            {
                                "name": "Commercial",
                                "value": 5000
                            },
                            {
                                "name": "Institutional",
                                "value": 5600
                            },
                            {
                                "name": "Domestic SLC",
                                "value": 7200
                            },
                            {
                                "name": "Domestic Exempted",
                                "value": 3800
                            },
                            {
                                "name": "Commercial Motor",
                                "value": 4800
                            }
                        ]
                    },
                    {
                        "groupBy": "paymentChannelType",
                        "buckets": [
                            {
                                "name": "System",
                                "value": 8000
                            },
                            {
                                "name": "Paytm",
                                "value": 7000
                            },
                            {
                                "name": "Field",
                                "value": 3700
                            },
                            {
                                "name": "Razorpay",
                                "value": 2200
                            },
                            {
                                "name": "PayU",
                                "value": 1000
                            },
                            {
                                "name": "BBPS",
                                "value": 1400
                            },
                            {
                                "name": "POS",
                                "value": 5100
                            },
                            {
                                "name": "Sewakendra",
                                "value": 5600
                            },
                            {
                                "name": "Freecharge",
                                "value": 3400
                            }
                        ]
                    },
                    {
                        "groupBy": "taxHeads",
                        "buckets": [
                            {
                                "name": "INTEREST",
                                "value": 7000
                            },
                            {
                                "name": "LATE.CHARGES",
                                "value": 8500
                            },
                            {
                                "name": "ADVANCE",
                                "value": 3700
                            },
                            {
                                "name": "CURRENT.CHARGES",
                                "value": 12422
                            },
                            {
                                "name": "ARREAR.CHARGES",
                                "value": 5778
                            }
                        ]
                    },
                    {
                        "groupBy": "connectionType",
                        "buckets": [
                            {
                                "name": "WATER.METERED",
                                "value": 18700
                            },
                            {
                                "name": "WATER.NONMETERED",
                                "value": 8500
                            },
                            {
                                "name": "SEWERAGE",
                                "value": 10200
                            }
                        ]
                    }
                ],
                "sewerageConnections": [
                    {
                        "groupBy": "channelType",
                        "buckets": [
                            {
                                "name": "ONLINE",
                                "value": 30
                            },
                            {
                                "name": "CSC",
                                "value": 11
                            },
                            {
                                "name": "SYSTEM",
                                "value": 9
                            }
                        ]
                    },
                    {
                        "groupBy": "usageType",
                        "buckets": [
                            {
                                "name": "Domestic",
                                "value": 11
                            },
                            {
                                "name": "Commercial",
                                "value": 10
                            },
                            {
                                "name": "Residential",
                                "value": 14
                            },
                            {
                                "name": "Institutional",
                                "value": 6
                            },
                            {
                                "name": "Domestic Exempted",
                                "value": 9
                            }
                        ]
                    }
                ],
                "waterConnections": [
                    {
                        "groupBy": "channelType",
                        "buckets": [
                            {
                                "name": "Counter",
                                "value": 47
                            },
                            {
                                "name": "ONLINE",
                                "value": 53
                            },
                            {
                                "name": "CSC",
                                "value": 15
                            },
                            {
                                "name": "SYSTEM",
                                "value": 45
                            }
                        ]
                    },
                    {
                        "groupBy": "usageType",
                        "buckets": [
                            {
                                "name": "Domestic",
                                "value": 123
                            },
                            {
                                "name": "Commercial",
                                "value": 22
                            },
                            {
                                "name": "Domestic Exempted",
                                "value": 15
                            }
                        ]
                    },
                    {
                        "groupBy": "meterType",
                        "buckets": [
                            {
                                "name": "METERED",
                                "value": 110
                            },
                            {
                                "name": "NON.METERED",
                                "value": 50
                            }
                        ]
                    }
                ],
                "pendingConnections": [
                    {
                        "groupBy": "duration",
                        "buckets": [
                            {
                                "name": "0to3Days",
                                "value": 11
                            },
                            {
                                "name": "3to7Days",
                                "value": 50
                            },
                            {
                                "name": "7to15Days",
                                "value": 5
                            },
                            {
                                "name": "MoreThan15Days",
                                "value": 2
                            }
                        ]
                    }
                ],
                "slaCompliance": 24,
                "todaysTotalApplications": 35,
                "todaysClosedApplications": 33,
                "todaysCompletedApplicationsWithinSLA": 46
            }
        }
    ]
}'
```

### 3. Fire NOC  <a href="#3.-firenoc" id="3.-firenoc"></a>

a. Index name - `firenoc-national-dashboard`

b. Index mapping -

```
"properties" : {
          "actualNOCIssuedByDeptForDepartment" : {
            "type" : "long"
          },
          "actualNOCIssuedForDepartment" : {
            "type" : "long"
          },
          "actualNOCIssuedForUsageType" : {
            "type" : "long"
          },
          "applicationType" : {
            "type" : "text",
            "fields" : {
              "keyword" : {
                "type" : "keyword",
                "ignore_above" : 256
              }
            }
          },
          "avgDaysToIssueActualNOCForDepartment" : {
            "type" : "long"
          },
          "avgDaysToIssueProvisionalNOCForDepartment" : {
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
            "format" : "dd-MM-yyyy HH:mm:ss||dd-MM-yyyy||epoch_millis"
          },
          "department" : {
            "type" : "text",
            "fields" : {
              "keyword" : {
                "type" : "keyword",
                "ignore_above" : 256
              }
            }
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
          "nocIssuedTodayForType" : {
            "type" : "long"
          },
          "paymentMode" : {
            "type" : "text",
            "fields" : {
              "keyword" : {
                "type" : "keyword",
                "ignore_above" : 256
              }
            }
          },
          "provisionalNOCIssuedForDepartment" : {
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
          "slaComplianceActualForDepartment" : {
            "type" : "long"
          },
          "slaComplianceProvisionalForDepartment" : {
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
          "todaysApplicationsForApplicationType" : {
            "type" : "long"
          },
          "todaysApplicationsForDepartment" : {
            "type" : "long"
          },
          "todaysClosedApplications" : {
            "type" : "long"
          },
          "todaysCollectionForDepartment" : {
            "type" : "long"
          },
          "todaysCollectionForPaymentMode" : {
            "type" : "long"
          },
          "todaysCompletedApplicationsWithinSLA" : {
            "type" : "long"
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
          "ulb" : {
            "type" : "text",
            "fields" : {
              "keyword" : {
                "type" : "keyword",
                "ignore_above" : 256
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
```

c. Ingest curl -

```
curl --location --request POST 'https://qa.digit.org/national-dashboard/metric/_ingest' \
--header 'Content-Type: application/json' \
--data-raw '{
    "RequestInfo": {
        "apiId": "asset-services",
        "ver": null,
        "ts": null,
        "action": null,
        "did": null,
        "key": null,
        "msgId": "search with from and to values",
        "authToken": "81ee8cb1-713c-40b3-a935-d9ae66d547af",
        "userInfo": {
            "id": 11131,
            "uuid": "0a8ef1d4-ef5c-4061-aea5-0ac4a410b87f",
            "userName": "NDSS",
            "name": "Lata",
            "mobileNumber": "7897807878",
            "emailId": null,
            "locale": null,
            "type": "EMPLOYEE",
            "roles": [
                {
                    "name": "National Dashboard Admin",
                    "code": "NATADMIN",
                    "tenantId": "pg"
                }
            ],
            "active": true,
            "tenantId": "pb.amritsar",
            "permanentCity": null
        }
    },
    "Data": [
        {
            "date": "25-02-2022",
            "module": "FIRENOC",
            "ward": "Ward 1",
            "ulb": "pb.amritsar",
            "region": "Amritsar-MC",
            "state": "Punjab",
            "metrics": {
                "todaysClosedApplications": 18,
                "todaysCompletedApplicationsWithinSLA": 32,
                "todaysApplications": [
                    {
                        "groupBy": "applicationType",
                        "buckets": [
                            {
                                "name": "ACTUAL",
                                "value": 30
                            },
                            {
                                "name": "PROVISIONAL",
                                "value": 54
                            }
                        ]
                    },
                    {
                        "groupBy": "department",
                        "buckets": [
                            {
                                "name": "DEPARTMENT1",
                                "value": 35
                            },
                            {
                                "name": "DEPARTMENT2",
                                "value": 49
                            }
                        ]
                    }
                ],
                "todaysCollection": [
                    {
                        "groupBy": "paymentMode",
                        "buckets": [
                            {
                                "name": "CASH",
                                "value": 5465
                            },
                            {
                                "name": "CHEQUE",
                                "value": 1300
                            },
                            {
                                "name": "DEBIT_CARD",
                                "value": 1400
                            },
                            {
                                "name": "ONLINE",
                                "value": 7570
                            }
                        ]
                    },
                    {
                        "groupBy": "department",
                        "buckets": [
                            {
                                "name": "DEPARTMENT1",
                                "value": 11767
                            },
                            {
                                "name": "DEPARTMENT2",
                                "value": 3968
                            }
                        ]
                    }
                ],
                "nocIssuedToday": [
                    {
                        "groupBy": "type",
                        "buckets": [
                            {
                                "name": "ACTUAL",
                                "value": 13
                            },
                            {
                                "name": "PROVISIONAL",
                                "value": 65
                            }
                        ]
                    }
                ],
                "provisionalNOCIssued": [
                    {
                        "groupBy": "department",
                        "buckets": [
                            {
                                "name": "DEPARTMENT1",
                                "value": 30
                            },
                            {
                                "name": "DEPARTMENT2",
                                "value": 23
                            }
                        ]
                    }
                ],
                "actualNOCIssued": [
                    {
                        "groupBy": "department",
                        "buckets": [
                            {
                                "name": "DEPARTMENT1",
                                "value": 56
                            },
                            {
                                "name": "DEPARTMENT2",
                                "value": 43
                            }
                        ]
                    },
                    {
                        "groupBy": "usageType",
                      "buckets": [
                            {
                                "name": "GROUP_A_RESIDENTIAL.SUBDIVISIONA-1",
                                "value": 20
                            },
                            {
                                "name": "GROUP_B_EDUCATIONAL.SUBDIVISIONB-1",
                                "value": 30
                            },
                            {
                                "name": "GROUP_C_INSTITUTIONAL.SUBDIVISIONC-1",
                                "value": 50
                            },
                            {
                                "name": "GROUP_A_RESIDENTIAL.SUBDIVISIONA-2",
                                "value": 60
                            },
                            {
                                "name": "GROUP_B_EDUCATIONAL.SUBDIVISIONB-2",
                                "value": 70
                            },
                            {
                                "name": "GROUP_C_INSTITUTIONAL.SUBDIVISIONC-2",
                                "value": 80
                            }
                        ]
                    }
                ],
                "avgDaysToIssueProvisionalNOC": [
                    {
                        "groupBy": "department",
                        "buckets": [
                            {
                                "name": "DEPARTMENT1",
                                "value": 54
                            },
                            {
                                "name": "DEPARTMENT2",
                                "value": 43
                            }
                        ]
                    }
                ],
                "slaComplianceActual": [
                    {
                        "groupBy": "department",
                        "buckets": [
                            {
                                "name": "DEPARTMENT1",
                                "value": 65
                            },
                            {
                                "name": "DEPARTMENT2",
                                "value": 33
                            }
                        ]
                    }
                ],
                "slaComplianceProvisional": [
                    {
                        "groupBy": "department",
                        "buckets": [
                            {
                                "name": "DEPARTMENT1",
                                "value": 23
                            },
                            {
                                "name": "DEPARTMENT2",
                                "value": 34
                            }
                        ]
                    }
                ],
                "avgDaysToIssueActualNOC": [
                    {
                        "groupBy": "department",
                        "buckets": [
                            {
                                "name": "DEPARTMENT1",
                                "value": 43
                            },
                            {
                                "name": "DEPARTMENT2",
                                "value": 12
                            }
                        ]
                    }
                ]
            }
        }
    ]
}'
```

### 4. Public Grievance Redressal  <a href="#4.-public-grievance-redressal" id="4.-public-grievance-redressal"></a>

a. Index name - `pgr-national-dashboard`

b. Index mapping -

```
"properties" : {
          "averageSolutionTimeForDepartment" : {
            "type" : "long"
          },
          "category" : {
            "type" : "text",
            "fields" : {
              "keyword" : {
                "type" : "keyword",
                "ignore_above" : 256
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
          "closedComplaints" : {
            "type" : "long"
          },
          "completionRate" : {
            "type" : "long"
          },
          "completionRateForDepartment" : {
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
          "department" : {
            "type" : "text",
            "fields" : {
              "keyword" : {
                "type" : "keyword",
                "ignore_above" : 256
              }
            }
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
          "region" : {
            "type" : "text",
            "fields" : {
              "keyword" : {
                "type" : "keyword",
                "ignore_above" : 256
              }
            }
          },
          "resolvedComplaints" : {
            "type" : "long"
          },
          "slaAchievement" : {
            "type" : "long"
          },
          "slaAchievementForDepartment" : {
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
          "status" : {
            "type" : "text",
            "fields" : {
              "keyword" : {
                "type" : "keyword",
                "ignore_above" : 256
              }
            }
          },
          "todaysAssignedComplaintsForDepartment" : {
            "type" : "long"
          },
          "todaysClosedComplaintsForDepartment" : {
            "type" : "long"
          },
          "todaysComplaintsForCategory" : {
            "type" : "long"
          },
          "todaysComplaintsForChannel" : {
            "type" : "long"
          },
          "todaysComplaintsForDepartment" : {
            "type" : "long"
          },
          "todaysComplaintsForStatus" : {
            "type" : "long"
          },
          "todaysOpenComplaintsForDepartment" : {
            "type" : "long"
          },
          "todaysReassignRequestedComplaintsForDepartment" : {
            "type" : "long"
          },
          "todaysReassignedComplaintsForDepartment" : {
            "type" : "long"
          },
          "todaysRejectedComplaintsForDepartment" : {
            "type" : "long"
          },
          "todaysReopenedComplaintsForDepartment" : {
            "type" : "long"
          },
          "todaysResolvedComplaintsForDepartment" : {
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
          "uniqueCitizens" : {
            "type" : "long"
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
```

c. Ingest curl -

```
curl --location --request POST 'https://qa.digit.org/national-dashboard/metric/_ingest' \
--header 'Content-Type: application/json' \
--data-raw '{
    "RequestInfo": {
        "apiId": "asset-services",
        "ver": null,
        "ts": null,
        "action": null,
        "did": null,
        "key": null,
        "msgId": "search with from and to values",
        "authToken": "{{access_token}}",
         "userInfo": {
             "id": 11131,
        "uuid": "0a8ef1d4-ef5c-4061-aea5-0ac4a410b87f",
        "userName": "NDSS",
        "name": "Lata",
        "mobileNumber": "7897807878",
        "emailId": null,
        "locale": null,
        "type": "EMPLOYEE",
        "roles": [
            {
                "name": "National Dashboard Admin",
                "code": "NATADMIN",
                "tenantId": "pg"
            }
        ],
        "active": true,
        "tenantId": "pb.amritsar",
        "permanentCity": null
        }
    },
    "Data": [
        {
            "date": "01-06-2022",
            "module": "PGR",
            "ward": "Ward 1",
            "ulb": "pb.amritsar",
            "region": "Amritsar-MC",
            "state": "Punjab",
            "metrics": {
                "slaAchievement": [
                    {
                        "groupBy": "department",
                        "buckets": [
                            {
                                "name": "DEPT1",
                                "value": 2
                            },
                            {
                                "name": "DEPT2",
                                "value": 0
                            },
                            {
                                "name": "DEPT3",
                                "value": 6
                            }
                        ]
                    }
                ],
                "completionRate": [
                    {
                        "groupBy": "department",
                        "buckets": [
                            {
                                "name": "DEPT1",
                                "value": 2
                            },
                            {
                                "name": "DEPT2",
                                "value": 0
                            },
                            {
                                "name": "DEPT3",
                                "value": 6
                            }
                        ]
                    }
                ],
                "uniqueCitizens": 22,
                "todaysComplaints": [
                    {
                        "groupBy": "status",
                        "buckets": [
                            {
                                "name": "reopened",
                                "value": 15
                            },
                            {
                                "name": "open",
                                "value": 20
                            },
                            {
                                "name": "assigned",
                                "value": 16
                            },
                            {
                                "name": "rejected",
                                "value": 14
                            },
                            {
                                "name": "reassign",
                                "value": 10
                            }
                        ]
                    },
                    {
                        "groupBy": "channel",
                        "buckets": [
                            {
                                "name": "MOBILE",
                                "value": 10
                            },
                            {
                                "name": "WEB",
                                "value": 90
                            }
                        ]
                    },
                    {
                        "groupBy": "department",
                        "buckets": [
                            {
                                "name": "DEPT1",
                                "value": 20
                            },
                            {
                                "name": "DEPT2",
                                "value": 50
                            },
                            {
                                "name": "DEPT3",
                                "value": 30
                            }
                        ]
                    },
                    {
                        "groupBy": "category",
                        "buckets": [
                            {
                                "name": "Street Lights",
                                "value": 20
                            },
                            {
                                "name": "Road Repair",
                                "value": 60
                            },
                            {
                                "name": "Garbage Cleaning",
                                "value": 10
                            },
                            {
                                "name": "Drainage Issue",
                                "value": 10
                            }
                        ]
                    }
                ],
                "todaysReopenedComplaints": [
                    {
                        "groupBy": "department",
                        "buckets": [
                            {
                                "name": "DEPT1",
                                "value": 20
                            },
                            {
                                "name": "DEPT2",
                                "value": 5
                            },
                            {
                                "name": "DEPT3",
                                "value": 3
                            }
                        ]
                    }
                ],
                "todaysOpenComplaints": [
                    {
                        "groupBy": "department",
                        "buckets": [
                            {
                                "name": "DEPT1",
                                "value": 2
                            },
                            {
                                "name": "DEPT2",
                                "value": 7
                            },
                            {
                                "name": "DEPT3",
                                "value": 11
                            }
                        ]
                    }
                ],
                "todaysAssignedComplaints": [
                    {
                        "groupBy": "department",
                        "buckets": [
                            {
                                "name": "DEPT1",
                                "value": 1
                            },
                            {
                                "name": "DEPT2",
                                "value": 0
                            },
                            {
                                "name": "DEPT3",
                                "value": 2
                            }
                        ]
                    }
                ],
                "averageSolutionTime": [
                    {
                        "groupBy": "department",
                        "buckets": [
                            {
                                "name": "DEPT1",
                                "value": 2
                            },
                            {
                                "name": "DEPT2",
                                "value": 4
                            },
                            {
                                "name": "DEPT3",
                                "value": 3
                            }
                        ]
                    }
                ],
                "todaysRejectedComplaints": [
                    {
                        "groupBy": "department",
                        "buckets": [
                            {
                                "name": "DEPT1",
                                "value": 2
                            },
                            {
                                "name": "DEPT2",
                                "value": 0
                            },
                            {
                                "name": "DEPT3",
                                "value": 6
                            }
                        ]
                    }
                ],
                "todaysReassignedComplaints": [
                    {
                        "groupBy": "department",
                        "buckets": [
                            {
                                "name": "DEPT1",
                                "value": 1
                            },
                            {
                                "name": "DEPT2",
                                "value": 3
                            },
                            {
                                "name": "DEPT3",
                                "value": 1
                            }
                        ]
                    }
                ],
                "todaysReassignRequestedComplaints": [
                    {
                        "groupBy": "department",
                        "buckets": [
                            {
                                "name": "DEPT1",
                                "value": 1
                            },
                            {
                                "name": "DEPT2",
                                "value": 3
                            },
                            {
                                "name": "DEPT3",
                                "value": 1
                            }
                        ]
                    }
                ],
                "todaysClosedComplaints": [
                    {
                        "groupBy": "department",
                        "buckets": [
                            {
                                "name": "DEPT1",
                                "value": 1
                            },
                            {
                                "name": "DEPT2",
                                "value": 3
                            },
                            {
                                "name": "DEPT3",
                                "value": 1
                            }
                        ]
                    }
                ],
                "todaysResolvedComplaints": [
                    {
                        "groupBy": "department",
                        "buckets": [
                            {
                                "name": "DEPT1",
                                "value": 1
                            },
                            {
                                "name": "DEPT2",
                                "value": 3
                            },
                            {
                                "name": "DEPT3",
                                "value": 1
                            }
                        ]
                    }
                ]
            }
        }
    ]
}'
```

### 5. Trade License  <a href="#5.-trade-license" id="5.-trade-license"></a>

a. Index name - `tl-national-dashboard`

b. Index mapping -

```
"properties" : {
          "adhocPenalty" : {
            "type" : "long"
          },
          "adhocRebate" : {
            "type" : "long"
          },
          "applicationsMovedTodayForStatus" : {
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
          "status" : {
            "type" : "text",
            "fields" : {
              "keyword" : {
                "type" : "keyword",
                "ignore_above" : 256
              }
            }
          },
          "tlTax" : {
            "type" : "long"
          },
          "todaysApplications" : {
            "type" : "long"
          },
          "todaysCollectionForTradeType" : {
            "type" : "long"
          },
          "todaysLicenseIssuedWithinSLA" : {
            "type" : "long"
          },
          "todaysTradeLicensesForStatus" : {
            "type" : "long"
          },
          "tradeType" : {
            "type" : "text",
            "fields" : {
              "keyword" : {
                "type" : "keyword",
                "ignore_above" : 256
              }
            }
          },
          "transactions" : {
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
```

c. Ingest curl -

```
curl --location --request POST 'https://qa.digit.org/national-dashboard/metric/_ingest' \
--header 'Content-Type: application/json' \
--data-raw '{
    "RequestInfo": {
        "apiId": "asset-services",
        "ver": null,
        "ts": null,
        "action": null,
        "did": null,
        "key": null,
        "msgId": "search with from and to values",
        "authToken": "{{access_token_loc}}",
        "userInfo": {
            "id": 11131,
            "uuid": "0a8ef1d4-ef5c-4061-aea5-0ac4a410b87f",
            "userName": "NDSS",
            "name": "Lata",
            "mobileNumber": "7897807878",
            "emailId": null,
            "locale": null,
            "type": "EMPLOYEE",
            "roles": [
                {
                    "name": "National Dashboard Admin",
                    "code": "NATADMIN",
                    "tenantId": "pg"
                }
            ],
            "active": true,
            "tenantId": "uk.kedarnath",
            "permanentCity": null
        }
    },
    "Data": [
        {
            "date": "29-12-2021",
            "module": "TL",
            "ward": "Ward 2",
            "ulb": "uk.kedarnath",
            "region": "Kedarnath-MC",
            "state": "Uttarakhand",
            "metrics": {
                "transactions": 29,
                "todaysApplications": 179,
                "tlTax": 50000,
                "adhocPenalty": 6000,
                "adhocRebate": 2000,
                "todaysLicenseIssuedWithinSLA": 41,
                "todaysCollection": [
                    {
                        "groupBy": "tradeType",
                        "buckets": [
                            {
                                "name": "BRICKFIELD",
                                "value": 21000
                            },
                            {
                                "name": "GROCERYSTORES",
                                "value": 20000
                            },
                            {
                                "name": "CHARCOAL_KLIN",
                                "value": 13000
                            }
                        ]
                    }
                ],
                "todaysTradeLicenses": [
                    {
                        "groupBy": "status",
                        "buckets": [
                            {
                                "name": "INITIATED",
                                "value": 31
                            },
                            {
                                "name": "APPLIED",
                                "value": 56
                            },
                            {
                                "name": "FIELDINSPECTION",
                                "value": 32
                            },
                            {
                                "name": "PENDINGAPPROVAL",
                                "value": 44
                            },
                            {
                                "name": "PENDINGPAYMENT",
                                "value": 29
                            },
                            {
                                "name": "APPROVED",
                                "value": 23
                            },
                            {
                                "name": "REJECTED",
                                "value": 1
                            },
                            {
                                "name": "EXPIRED",
                                "value": 1
                            }
                        ]
                    }
                ],
                "applicationsMovedToday": [
                    {
                        "groupBy": "status",
                        "buckets": [
                            {
                                "name": "INITIATED",
                                "value": 31
                            },
                            {
                                "name": "APPLIED",
                                "value": 56
                            },
                            {
                                "name": "FIELDINSPECTION",
                                "value": 32
                            },
                            {
                                "name": "PENDINGAPPROVAL",
                                "value": 44
                            },
                            {
                                "name": "PENDINGPAYMENT",
                                "value": 29
                            },
                            {
                                "name": "APPROVED",
                                "value": 23
                            },
                            {
                                "name": "REJECTED",
                                "value": 1
                            },
                            {
                                "name": "EXPIRED",
                                "value": 1
                            }
                        ]
                    }
                ]
            }
        }
    ]
}'
```

### 6. mCollect  <a href="#6.-mcollect" id="6.-mcollect"></a>

a. Index name - `mcollect-national-dashboard`

b. Index mapping -

```
"properties" : {
          "category" : {
            "type" : "text",
            "fields" : {
              "keyword" : {
                "type" : "keyword",
                "ignore_above" : 256
              }
            }
          },
          "challanStatus" : {
            "type" : "text",
            "fields" : {
              "keyword" : {
                "type" : "keyword",
                "ignore_above" : 256
              }
            }
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
          "numberOfCategories" : {
            "type" : "long"
          },
          "numberOfChallansForCategory" : {
            "type" : "long"
          },
          "numberOfChallansForChallanStatus" : {
            "type" : "long"
          },
          "numberOfReceiptsForCategory" : {
            "type" : "long"
          },
          "numberOfReceiptsForPaymentMode" : {
            "type" : "long"
          },
          "numberOfReceiptsForStatus" : {
            "type" : "long"
          },
          "paymentMode" : {
            "type" : "text",
            "fields" : {
              "keyword" : {
                "type" : "keyword",
                "ignore_above" : 256
              }
            }
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
          "status" : {
            "type" : "text",
            "fields" : {
              "keyword" : {
                "type" : "keyword",
                "ignore_above" : 256
              }
            }
          },
          "todaysCollectionForCategory" : {
            "type" : "long"
          },
          "todaysCollectionForPaymentMode" : {
            "type" : "long"
          },
          "todaysCollectionForStatus" : {
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
```

c. Ingest curl -

```
curl --location --request POST 'https://qa.digit.org/national-dashboard/metric/_ingest' \
--header 'Content-Type: application/json' \
--data-raw '{
    "RequestInfo": {
        "apiId": "asset-services",
        "ver": null,
        "ts": null,
        "action": null,
        "did": null,
        "key": null,
        "msgId": "search with from and to values",
        "authToken": "{{access_token_loc}}",
        "userInfo": {
            "id": 11131,
            "uuid": "0a8ef1d4-ef5c-4061-aea5-0ac4a410b87f",
            "userName": "NDSS",
            "name": "Lata",
            "mobileNumber": "7897807878",
            "emailId": null,
            "locale": null,
            "type": "EMPLOYEE",
            "roles": [
                {
                    "name": "National Dashboard Admin",
                    "code": "NATADMIN",
                    "tenantId": "pg"
                }
            ],
            "active": true,
            "tenantId": "pb.amritsar",
            "permanentCity": null
        }
    },
    "Data": [
        {
            "date": "29-10-2021",
            "module": "MCOLLECT",
"ward": "Ward 1",
"ulb": "pb.amritsar",
"region": "Amritsar-MC",
"state": "Punjab",
            "metrics": {
                "numberOfCategories": 9,
                "todaysCollection": [
                    {
                        "groupBy": "paymentMode",
                        "buckets": [
                         {"name": "UPI","value":1765},{"name": "CASH","value":2415},{"name": "DEBIT_CARD","value":165}
                        ]
                    },
                    {
                        "groupBy": "status",
                        "buckets": [
                        {"name": "NEW","value":1835},{"name": "DEPOSITED","value":1425},{"name": "DISHONOURED","value":1085}
                        ]
                    },
                    {
                        "groupBy": "category",
                        "buckets": [
                           {"name": "COMMON_MASTERS_HOARDING","value":135},{"name": "COMMON_MASTERS_ROAD_SHOW","value":805},{"name": "COMMON_MASTERS_UNIPOLLS","value":795},{"name": "COMMON_MASTERS_AUCTION_FEE","value":655},{"name": "COMMON_MASTERS_USER_FEES","value":495},{"name": "COMMON_MASTERS_MUNICIPAL_SHOPS_RENT","value":305},{"name": "COMMON_MASTERS_PARKING_FEE","value":555},{"name": "COMMON_MASTERS_TOWER_ANNUAL_RENT","value":505},{"name": "COMMON_MASTERS_TOWER_INSTALLATION","value":95}
                        ]
                    }
                ],
                "numberOfReceipts": [
                    {
                        "groupBy": "status",
                        "buckets": [
                          {"name": "NEW","value":174},{"name": "DEPOSITED","value":284},{"name": "DISHONOURED","value":187}
                        ]
                    },
                    {
                        "groupBy": "paymentMode",
                        "buckets": [
                           {"name": "CASH","value":163},{"name": "CHEQUE","value":140},{"name": "DEBIT_CARD","value":156},{"name": "ONLINE","value":186}
                        ]
                    },
                    {
                        "groupBy": "category",
                        "buckets": [
                           {"name": "COMMON_MASTERS_HOARDING","value":56},{"name": "COMMON_MASTERS_ROAD_SHOW","value":51},{"name": "COMMON_MASTERS_UNIPOLLS","value":82},{"name": "COMMON_MASTERS_AUCTION_FEE","value":77},{"name": "COMMON_MASTERS_USER_FEES","value":46},{"name": "COMMON_MASTERS_MUNICIPAL_SHOPS_RENT","value":66},{"name": "COMMON_MASTERS_PARKING_FEE","value":63},{"name": "COMMON_MASTERS_TOWER_ANNUAL_RENT","value":103},{"name": "COMMON_MASTERS_TOWER_INSTALLATION","value":101}
                        ]
                    }
                ],
                "numberOfChallans": [
                    {
                        "groupBy": "challanStatus",
                        "buckets": [
                         {"name": "PAID","value":151},{"name": "CANCELLED","value":41},{"name": "ACTIVE","value":341}
                        ]
                    },
                    {
                        "groupBy": "category",
                        "buckets": [
                         {"name": "COMMON_MASTERS_HOARDING","value":45},{"name": "COMMON_MASTERS_ROAD_SHOW","value":70},{"name": "COMMON_MASTERS_UNIPOLLS","value":71},{"name": "COMMON_MASTERS_AUCTION_FEE","value":65},{"name": "COMMON_MASTERS_USER_FEES","value":75},{"name": "COMMON_MASTERS_MUNICIPAL_SHOPS_RENT","value":30},{"name": "COMMON_MASTERS_PARKING_FEE","value":61},{"name": "COMMON_MASTERS_TOWER_ANNUAL_RENT","value":56},{"name": "COMMON_MASTERS_TOWER_INSTALLATION","value":60}
                        ]
                    }
                ]
            }
        }
    ]
}'
```

### 7. Online Building Permission System <a href="#7.-online-building-permission-system" id="7.-online-building-permission-system"></a>

a. Index name - `obps-national-dashboard`

b. Index mapping -

```
"mappings" : {
      "nss" : {
        "properties" : {
          "applicationsSubmitted" : {
            "type" : "long"
          },
          "applicationsWithDeviation" : {
            "type" : "long"
          },
          "averageDaysToIssueOC" : {
            "type" : "long"
          },
          "averageDaysToIssuePermit" : {
            "type" : "long"
          },
          "averageDeviation" : {
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
          "landAreaAppliedInSystemForBPA" : {
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
          "ocIssued" : {
            "type" : "long"
          },
          "ocPlansScrutinized" : {
            "type" : "long"
          },
          "ocSubmitted" : {
            "type" : "long"
          },
          "ocWithDeviation" : {
            "type" : "long"
          },
          "occupancyType" : {
            "type" : "text",
            "fields" : {
              "keyword" : {
                "type" : "keyword",
                "ignore_above" : 256
              }
            }
          },
          "paymentMode" : {
            "type" : "text",
            "fields" : {
              "keyword" : {
                "type" : "keyword",
                "ignore_above" : 256
              }
            }
          },
          "permitsIssuedForOccupancyType" : {
            "type" : "long"
          },
          "permitsIssuedForRiskType" : {
            "type" : "long"
          },
          "permitsIssuedForSubOccupancyType" : {
            "type" : "long"
          },
          "plansScrutinized" : {
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
          "riskType" : {
            "type" : "text",
            "fields" : {
              "keyword" : {
                "type" : "keyword",
                "ignore_above" : 256
              }
            }
          },
          "slaComplianceOC" : {
            "type" : "long"
          },
          "slaCompliancePermit" : {
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
          "subOccupancyType" : {
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
          "todaysClosedApplicationsOC" : {
            "type" : "long"
          },
          "todaysClosedApplicationsPermit" : {
            "type" : "long"
          },
          "todaysCollectionForPaymentMode" : {
            "type" : "long"
          },
          "todaysCompletedApplicationsWithinSLAOC" : {
            "type" : "long"
          },
          "todaysCompletedApplicationsWithinSLAPermit" : {
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

c. Ingest curl -

```
curl --location --request POST 'https://qa.digit.org/national-dashboard/metric/_ingest' \
--header 'Content-Type: application/json' \
--data-raw '{
    "RequestInfo": {
        "apiId": "asset-services",
        "ver": null,
        "ts": null,
        "action": null,
        "did": null,
        "key": null,
        "msgId": "search with from and to values",
        "authToken": "7112c6a3-41d4-42d0-9ae9-7d2ec08d1a4f"
    },
    "Data": [ {
        "date": "05-01-2022",
        "module": "OBPS",
        "ward": "Ajit Nagar",
        "ulb": "pb.amritsar",
        "region": "amritsar-MC",
        "state": "Punjab",
        "metrics": {
            "ocPlansScrutinized": 120,
            "plansScrutinized": 540,
            "ocSubmitted": 50,
            "applicationsSubmitted": 50,
            "ocIssued": 19,
            "landAreaAppliedInSystemForBPA": 23442,
            "averageDaysToIssuePermit": 10,
            "averageDaysToIssueOC": 8,
            "todaysClosedApplicationsOC":10 ,
            "todaysCompletedApplicationsWithinSLAOC":5 ,
            "todaysClosedApplicationsPermit": 20,
            "todaysCompletedApplicationsWithinSLAPermit":10,
            "slaComplianceOC": 20,
            "slaCompliancePermit": 40,
            "applicationsWithDeviation": 20,
            "averageDeviation": 10,
            "ocWithDeviation": 30,
            "todaysCollection": [
                {
                    "groupBy": "paymentMode",
                    "buckets": [
                        {
                            "name": "UPI",
                            "value": 10000
                        },
                        {
                            "name": "DEBIT.CARD",
                            "value": 15000
                        },
                        {
                            "name": "CREDIT.CARD",
                            "value": 8500
                        }
                    ]
                }
            ],
            "permitsIssued": [
                {
                    "groupBy": "riskType",
                    "buckets": [
                        {
                            "name": "LOW",
                            "value": 150
                        },
                        {
                            "name": "MEDIUM",
                            "value": 300
                        },
                        {
                            "name": "HIGH",
                            "value": 600
                        }
                    ]
                } ,
                 {
                    "groupBy": "occupancyType",
                    "buckets": [
                        {
                            "name": "RESIDENTIAL",
                            "value": 150
                        },
                        {
                            "name": "INSTITUTIONAL",
                            "value": 180
                        }
                    ]
                },
                   {
                    "groupBy": "subOccupancyType",
                    "buckets": [
                        {
                            "name": "RESIDENTIAL.INDIVIDUAL",
                            "value": 50
                        },
                        {
                            "name": "RESIDENTIAL.SHARED",
                            "value": 20
                        },
                        {
                            "name": "INSITUTIONAL.SHARED",
                            "value": 120
                        }
                    ]
                }
            ]
        }
    }
    ]
}'
```

### 8. Common National Dashboard  <a href="#8.-common" id="8.-common"></a>

a. Index name - `common-national-dashboard`

b. Index mapping -

```
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
          "date" : {
            "type" : "date",
            "format" : "dd-MM-yyyy HH:mm:ss||dd-MM-yyyy||epoch_millis||dd-MM-yyyy'T'HH:mm:ss.SSSZ"
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
          "liveUlbsCountForServiceModuleCode" : {
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
          "onboardedUlbsCount" : {
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
          "serviceModuleCode" : {
            "type" : "text",
            "fields" : {
              "keyword" : {
                "type" : "keyword",
                "ignore_above" : 256
              }
            }
          },
          "slaAchievement" : {
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
          "status" : {
            "type" : "text",
            "fields" : {
              "keyword" : {
                "type" : "keyword",
                "ignore_above" : 256
              }
            }
          },
          "totalCitizensCount" : {
            "type" : "long"
          },
          "totalLiveUlbsCount" : {
            "type" : "long"
          },
          "totalUlbCount" : {
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
```

c. Ingest curl -

{% hint style="info" %}
Note: ulb, ward and region are not applicable as common-nation-dashboard data is ingested at state level. These three field values will be dummy and can be same across. The Dashboard queries does not use ward, ulb or region in Landing Page Metrics
{% endhint %}

```
curl --location --request POST 'https://qa.digit.org/national-dashboard/metric/_ingest' \
--header 'Content-Type: application/json' \
--data-raw '{
    "RequestInfo": {
        "apiId": "asset-services",
        "ver": null,
        "ts": null,
        "action": null,
        "did": null,
        "key": null,
        "msgId": "search with from and to values",
        "authToken": "ac024e05-2b0e-4341-b294-681c5d72fcaf",
        "userInfo": {
            "id": 11131,
            "uuid": "0a8ef1d4-ef5c-4061-aea5-0ac4a410b87f",
            "userName": "NDSS",
            "name": "Lata",
            "mobileNumber": "7897807878",
            "emailId": null,
            "locale": null,
            "type": "EMPLOYEE",
            "roles": [
                {
                    "name": "National Dashboard Admin",
                    "code": "NATADMIN",
                    "tenantId": "pg"
                }
            ],
            "active": true,
            "tenantId": "pb.amritsar",
            "permanentCity": null
        }
    },
    "Data": [
        {
            "date": "06-02-2022",
            "module": "COMMON",
            "ward": "Ward 1",
            "ulb": "pb.amritsar",
            "region": "Amritsar-MC",
            "state": "Punjab",
            "metrics": {
                "status": "Live",
                "onboardedUlbsCount": 12,
                "totalCitizensCount": 1250,
                "totalLiveUlbsCount": 15,
                "totalUlbCount": 22,
                "slaAchievement": 75,
                "liveUlbsCount": [
                    {
                        "groupBy": "serviceModuleCode",
                        "buckets": [
                            {
                                "name": "PT",
                                "value": 12
                            },
                            {
                                "name": "TL",
                                "value": 10
                            },
                            {
                                "name": "FIRENOC",
                                "value": 8
                            },
                            {
                                "name": "PGR",
                                "value": 22
                            },
                            {
                                "name": "WS",
                                "value": 12
                            }
                        ]
                    }
                ]
            }
        }
    ]
}'
```

&#x20;[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in/) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
