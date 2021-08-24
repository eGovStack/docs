# Legacy/Re-Indexing the FSM Data

## Overview 

In this document, we will learn how to legacy index/re-index the fsm index.

## Pre-Requisites

* Kubectl access to the required environment in which you want to run the re-indexing
* playground pod access
* Legacy index mapping/configuration done in the respective indexer-config \( in this case for FSM, legacy index configuration for fsm is done [here](https://github.com/egovernments/configs/blob/8149b5a799aa0413b26f02c56c1bea58da6210bb/egov-indexer/egov-fsm.yml#L172), Similarly for VehicleTrip also exists \)

#### Postman Collection  <a id="Postman-Collection"></a>

Postman collection to re-index the data for FSM, VehicleTrip, Vehicle, Vendor Services can be downloaded [here](https://www.getpostman.com/collections/c94923b02c20ab6d7db1)

## Steps to legacy-index FSM

1. After importing the postman collection downloaded from above section, you can find two request
   1. fsm-legacy : This request helps to get the data from fsm/plainsearch api and push data to fsm-enriched topic by indexer service
   2. fsm-legacy-kafkaconnector : This is the request to create a connector which can listen to the fsm-enriched topic and push data to the elastic search with the new index fsm-enriched
2. Run the fsm-legacy-kafkaconnector request in the playground pod, which would create a connector which would intern start listening to the topic fsm-enriched-sink
3. Run the fsm-legacy request in the playground pod, which would call indexer service to intiate the process of fetching the data from plainsearch and push the data prepared according to the legacy-index mapping and push the data to the fsm-enriched-sink topic
4. Whole process would take some time, mean while you can searc for the data in fsm-enriched index in the elastic search
5. we can go through the logs of the indexer pod, which would help to understand the job is done
6. Once the job is done, delete the kafka connector running the below curl in the playground `curl --location --request DELETE 'http://kafka-connect.kafka-cluster:8083/connectors/fsm-enriched-es-sink'`

7. Once reindexing is completed, please verfiy the count in fsm index and fsm-enriched index, then delete the fsm index and create alias for fsm-enriched index as fsm.Please use below command for alias creating.

```text
POST /_aliases
{  "actions":
[  
  {      "add":
 {        "index": "fsm-enriched",    
   "alias": "fsm"    
  }    
}
 ]
}
```

## Steps to legacy index VehicleTrip

1. After importing the postman collection downloaded from above section, you can find two request
   1. vehicleTrip-legacy : This request helps to get the data from vehicletrip/plainsearch api and push data to vehicletrip-enriched topic by indexer service
   2. vehicle-trip-legacy-kafkaconnector : This is the request to create a connector which can listen to the vehicletrip-enriched topic and push data to the elastic search with the new index vehicletrip-enriched
2. Run the vehicletrip-legacy-kafkaconnector request in the playground pod, which would create a connector which would intern start listening to the topic vehicletrip-enriched-sink
3. Run the vehicletrip-legacy request in the playground pod, which would call indexer service to intiate the process of fetching the data from plainsearch and push the data prepared according to the legacy-index mapping and push the data to the vehicletrip-enriched-sink topic
4. Whole process would take some time, mean while you can searc for the data in vehicletrip-enriched index in the elastic search
5. we can go through the logs of the indexer pod, which would help to understand the job is done
6. Once the job is done, delete the kafka connector running the below curl in the playground `curl --location --request DELETE 'http://kafka-connect.kafka-cluster:8083/connectors/vehicletrip-enriched-es-sink'`
7. Once reindexing is completed, please verfiy the count in vehicletrip index and vehicletrip-enriched index, then delete the vehicletrip index and create alias for vehicletrip-enriched index as vehicletrip.Please use below command for alias creating.

```text
POST /_aliases
{  "actions":
[  
  {      "add":
 {        "index": "vehicletrip-enriched",    
   "alias": "vehicletrip"    
  }    
}
 ]
}
```







