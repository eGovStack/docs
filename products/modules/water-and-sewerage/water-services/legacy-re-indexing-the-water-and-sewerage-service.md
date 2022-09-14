# Legacy/Re-Indexing the Water & Sewerage Service

#### Overview <a href="#overview" id="overview"></a>

We are using re-indexing to get all the data to respective indexer. We have 2 steps for this. First as to run the connector from playground, which is followed by legacyindexer service call from indexer service, which internally call the respective plain search service to get the data and to send to respective indexer.

\
**Prerequisites**:

* Access to kubectl of the environment targetted
* Postman scripts
* Plain search apis in the respective services

**We have two services for water and sewerage**

* water-services
* sewerage-services

**water-services reindexing steps**

* Connect to playground pod.
* Delete the kafka connector if already exists with the kafka connection, using below command through playground pod.

```
curl --location --request DELETE 'http://kafka-connect.kafka-cluster:8083/connectors/water-services-enriched-es-sink'
```

* Run below kafka connector curl from playground pod:

```
curl --location --request POST 'http://kafka-connect.kafka-cluster:8083/connectors/' \
--header 'Cache-Control: no-cache' \
--header 'Content-Type: application/json' \
--header 'Postman-Token: 419e68ba-ffb9-4da9-86e1-7ad5a4c8d0b9' \
--data '{
    "name": "water-services-enriched-es-sink",
    "config": {
        "connector.class": "io.confluent.connect.elasticsearch.ElasticsearchSinkConnector",
        "type.name": "general",
        "tasks.max": "1",
        "max.retries": "15",
        "key.ignore": "false",
        "retry.backoff.ms": "5000",
        "max.buffered.records": "25",
        "value.converter": "org.apache.kafka.connect.json.JsonConverter",
        "errors.log.enable": "true",
        "key.converter": "org.apache.kafka.connect.storage.StringConverter",
        "read.timeout.ms": "100000",
        "topics": "water-services-enriched",
        "batch.size": "25",
        "max.in.flight.requests": "2",
        "schema.ignore": "true",
        "behavior.on.malformed.documents": "warn",
        "flush.timeout.ms": "3600000",
        "errors.deadletterqueue.topic.name": "water-services-enriched-failed",
        "errors.tolerance": "all",
        "value.converter.schemas.enable": "false",
        "name": "water-services-enriched-es-sink",
        "connection.url": "http://elasticsearch-data-v1.es-cluster:9200",
        "linger.ms": "1000",
        "transforms": "TopicNameRouter",
        "transforms.TopicNameRouter.type": "org.apache.kafka.connect.transforms.RegexRouter",
        "transforms.TopicNameRouter.regex": "water-services-enriched*",
        "transforms.TopicNameRouter.replacement": "water-services-enriched"
    }
}'
```

* port forward to egov-indexer pod and run below curl throw postman.

```
curl --location --request POST 'http://localhost:8088/egov-indexer/index-operations/_legacyindex' \
--header 'Content-Type: application/json' \
--data-raw '{
    "RequestInfo": {
        "apiId": "string",
        "ver": "string",
        "ts": null,
        "action": "string",
        "did": "string",
        "key": "string",
        "msgId": "string",
        "authToken": "ca3256e3-5318-47b1-8a68-ffcf2228fe35",
        "correlationId": "e721639b-c095-40b3-86e2-acecb2cb6efb",
        "userInfo": {
            "id": 23299,
            "uuid": "e721639b-c095-40b3-86e2-acecb2cb6efb",
            "userName": "9337682030",
            "name": "Abhilash Seth",
            "type": "CITIZEN",
            "mobileNumber": "9337682030",
            "emailId": "abhilash.seth@gmail.com",
            "roles": [
                {
                    "id": 281,
                    "name": "Citizen"
                }
            ]
        }
    },
    "apiDetails": {
        "uri": "http://ws-services.egov:8080/ws-services/wc/_plainsearch",
        "tenantIdForOpenSearch": "pb",
        "paginationDetails": {
            "offsetKey": "offset",
            "sizeKey": "limit",
            "maxPageSize": 25,
            "limit": 25
        },
        "responseJsonPath": "$.WaterConnection"
    },
    "legacyIndexTopic": "ws-connection-legacyIndex",
    "tenantId": "pb"
}'
```

* Delete the kafka connection after all the data has been re-indexed by follwing below command through playground pod.

```
curl --location --request DELETE 'http://kafka-connect.kafka-cluster:8083/connectors/water-services-enriched-es-sink'
```

* Alias water-services-enriched as water-services through kibana server.

```
POST /_aliases 
{
  "actions": [
    {
      "add": {
        "index": "water-services-enriched",
        "alias": "water-services"
      }
    }
  ]
}
```



**sewerage-services re-indexing steps**

* Connect to playground pod.
* Delete the kafka connector if already exists with the kafka connection, using below command through playground pod.

```
curl --location --request DELETE 'http://kafka-connect.kafka-cluster:8083/sewerage-services-enriched-es-sink'
```

* Run below kafka connector curl from playground pod:

```
curl --location --request POST 'http://kafka-connect.kafka-cluster:8083/connectors/' \
--header 'Cache-Control: no-cache' \
--header 'Content-Type: application/json' \
--header 'Postman-Token: 419e68ba-ffb9-4da9-86e1-7ad5a4c8d0b9' \
--data-raw '{
    "name": "sewerage-services-enriched-es-sink",
    "config": {
        "connector.class": "io.confluent.connect.elasticsearch.ElasticsearchSinkConnector",
        "type.name": "general",
        "tasks.max": "1",
        "max.retries": "15",
        "key.ignore": "false",
        "retry.backoff.ms": "5000",
        "max.buffered.records": "25",
        "value.converter": "org.apache.kafka.connect.json.JsonConverter",
        "errors.log.enable": "true",
        "key.converter": "org.apache.kafka.connect.storage.StringConverter",
        "read.timeout.ms": "100000",
        "topics": "sewerage-services-enriched",
        "batch.size": "25",
        "max.in.flight.requests": "2",
        "schema.ignore": "true",
        "behavior.on.malformed.documents": "warn",
        "flush.timeout.ms": "3600000",
        "errors.deadletterqueue.topic.name": "sewerage-services-enriched-failed",
        "errors.tolerance": "all",
        "value.converter.schemas.enable": "false",
        "name": "sewerage-services-enriched-es-sink",
        "connection.url": "http://elasticsearch-data-v1.es-cluster:9200",
        "linger.ms": "1000",
        "transforms": "TopicNameRouter",
        "transforms.TopicNameRouter.type": "org.apache.kafka.connect.transforms.RegexRouter",
        "transforms.TopicNameRouter.regex": "sewerage-services-enriched*",
        "transforms.TopicNameRouter.replacement": "sewerage-services-enriched"
    }
}'
```

* port forward to egov-indexer pod and run below curl throw postman.

```
curl --location --request POST 'http://localhost:8088/egov-indexer/index-operations/_legacyindex' \
--header 'Content-Type: application/json' \
--data-raw '{
    "RequestInfo": {
        "apiId": "string",
        "ver": "string",
        "ts": null,
        "action": "string",
        "did": "string",
        "key": "string",
        "msgId": "string",
        "authToken": "ca3256e3-5318-47b1-8a68-ffcf2228fe35",
        "correlationId": "e721639b-c095-40b3-86e2-acecb2cb6efb",
        "userInfo": {
            "id": 23299,
            "uuid": "e721639b-c095-40b3-86e2-acecb2cb6efb",
            "userName": "9337682030",
            "name": "Abhilash Seth",
            "type": "CITIZEN",
            "mobileNumber": "9337682030",
            "emailId": "abhilash.seth@gmail.com",
            "roles": [
                {
                    "id": 281,
                    "name": "Citizen"
                }
            ]
        }
    },
    "apiDetails": {
        "uri": "http://sw-services.egov:8080/sw-services/swc/_plainsearch",
        "tenantIdForOpenSearch": "pb",
        "paginationDetails": {
            "offsetKey": "offset",
            "sizeKey": "limit",
            "maxPageSize": 25,
            "limit":25
        },
        "responseJsonPath": "$.SewerageConnections"
    },
    "legacyIndexTopic": "sw-connection-legacyIndex",
    "tenantId": "pb"
}'
```

* Delete the kafka connection after all the data has been re-indexed by follwing below command through playground pod.

```
curl --location --request DELETE 'http://kafka-connect.kafka-cluster:8083/sewerage-services-enriched-es-sink'
```

* Alias water-services-enriched as water-services through kibana server.

```
POST /_aliases 
{
  "actions": [
    {
      "add": {
        "index": "sewerage-services-enriched",
        "alias": "sewerage-services"
      }
    }
  ]
}
```

