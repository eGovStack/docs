# Indexer Service

## Overview <a href="#overview" id="overview"></a>

Indexer service runs as a separate service. This service is designed to perform all the indexing tasks of the digit platform. The service reads records posted on specific Kafka topics and picks the corresponding index configuration from the yaml file provided by the respective module. The objective of the Indexer Service is listed below.

* To provide a one-stop framework for indexing the data to elasticsearch.
* To create a provision for indexing live data, reindexing from one index to the other and indexing legacy data from the data store.

## Pre-requisites <a href="#pre-requisites" id="pre-requisites"></a>

Before you proceed with the configuration, make sure the following pre-requisites are met -

1. Prior Knowledge of Java/J2EE
2. Prior Knowledge of SpringBoot
3. Prior Knowledge of Elasticsearch
4. Prior Knowledge of REST APIs and related concepts like path parameters, headers, JSON etc.
5. Prior Knowledge of Kafka and related concepts like Producer, Consumer, Topic etc.

## Key Functionalities <a href="#key-functionalities" id="key-functionalities"></a>

* Performs three major tasks namely: LiveIndex, Reindex and LegacyIndex.
* LiveIndex: Task of indexing the live transaction data on the platform. This keeps the es data in sync with the database.
* Reindex: Task of indexing data from one index to the other. ES already provides this feature, indexer does the same but with data transformation.
* LegacyIndex: Task of indexing legacy data from the tables to ES.
* Provides flexibility to index the entire object, a part of the object or an entirely different custom object all using one input json from modules.
* Provides features for customizing index json by field mapping, field masking, data enrichment through external APIs and data denormalization using MDMS.
* One-stop shop for all the es index requirements with easy-to-write and easy-to-maintain configuration files.
* Designed as a consumer to save API overhead. The consumer configs are written from scratch to have complete control over consumer behaviour.

## Deployment Details <a href="#deployment-details" id="deployment-details"></a>

* Step 1: Write the configuration as per your requirement. The structure of the config file is explained later in the same doc.
* Step 2: Check in the config file to a remote location, preferably Github. Currently, the files are checked into the folder here - [https://github.com/egovernments/configs/tree/DEV/egov-indexer](https://github.com/egovernments/configs/tree/DEV/egov-indexer) -for dev
* Step 3: Provide the absolute path of the checked-in file to DevOps. This file path is added to the file-read path of the egov-indexer. The file is added to the egov-indexer's environment manifest file for it to be read at the start-up of the application.
* Step 4: Run the egov-indexer app, Since it is a consumer, it starts listening to the configured topics and indexes the data.

## Interaction Diagram <a href="#interaction-diagram" id="interaction-diagram"></a>

![](../../../.gitbook/assets/indexer.png)

## Configuration Details <a href="#configuration-details" id="configuration-details"></a>

For Indexer Configuration, please refer to the document in the reference docs table given below.

## API Details <a href="#api-details" id="api-details"></a>

a) POST /{key}/\_index

Receive data and index. There should be a mapping with the topic as {key} in index config files.

b) POST /\_reindex

This is used to migrate data from one index to another index

c) POST /\_legacyindex

This is to run the LegacyIndex job to index data from the database. In the request body, the URL of the service that will be called by the indexer service to pick the data must be mentioned.

{% hint style="info" %}
In legacy indexing and for collection-service records LiveIndex kafka-connect is used to do part of pushing records to elastic search. For more details please refer to the document mentioned in the document list.
{% endhint %}

## Reference Docs <a href="#reference-docs" id="reference-docs"></a>

### Doc Links <a href="#doc-links" id="doc-links"></a>

{% file src="../../../.gitbook/assets/using-kafka-connect.pdf" %}
Using kafka-connect in egov-indexer reindexing jobs to push records to elastic search
{% endfile %}

{% file src="../../../.gitbook/assets/indexer-configuration.pdf" %}
Indexer Configuration
{% endfile %}

[Swagger Documentation](https://editor.swagger.io/?url=https://raw.githubusercontent.com/egovernments/core-services/master/docs/indexer-contract.yml#!/)

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation ](https://egov.org.in/)is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).
