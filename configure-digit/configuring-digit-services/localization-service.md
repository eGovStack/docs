# Localization Service

## Overview <a href="#overview" id="overview"></a>

An eGov core application that provides locale-specific components and translation of text for the eGov group of applications.

## Pre-requisites <a href="#pre-requisites" id="pre-requisites"></a>

1. Prior Knowledge of Java/J2EE.
2. Prior Knowledge of Spring Boot.
3. Prior Knowledge of REST APIs and related concepts like path parameters, headers, JSON etc.
4. Prior knowledge of Redis and postgres.

## Key Functionalities <a href="#key-functionalities" id="key-functionalities"></a>

The localization application stores the locale data in the format of key and value along with the module, tenantid and locale. Module defines which application of eGov owns the locale data and tenantId do the same for the tenant. Locale refers to the specific location where data is being added. &#x20;

The request can be posted through the post API with the above-mentioned variables in the request body.

Once posted the same data can be searched based on the module, locale and tenantId as keys.

The Data posted to the localization service is permanently stored in the database and is loaded into the Redis cache for easy access. Each time the new data is added to the application the Redis cache is refreshed.

## Deployment Details <a href="#deployment-details" id="deployment-details"></a>

1. Deploy the latest version of Localization Service.
2. Add Role-Action mapping for APIs.

## Integration <a href="#integration" id="integration"></a>

### Integration Scope <a href="#integration-scope" id="integration-scope"></a>

The Localization service is used to store **key-value pairs** of metadata in different languages for all miscellaneous / adhoc services which citizens avail from ULBs.

### Integration Benefits <a href="#integration-benefits" id="integration-benefits"></a>

* Can perform service-specific business logic without impacting the other module.
* Provides the capability of having multiple languages in modules.

### Steps to Integration <a href="#steps-to-integration" id="steps-to-integration"></a>

1. To integrate, a host of localization-services modules should be overwritten in the helm chart.
2. `/localization/messages/v1/_upsert` __ should be added as the create endpoint for creating localization key-value pairs in the system
3. `/localization/messages/v1/_search` should be added as the search endpoint. This method handles all requests to search existing records depending on different search criteria

## Resources

### Postman Collection

{% embed url="https://www.getpostman.com/collections/a140e7426ab4419ed5b5" %}

### Swagger Contract <a href="#swagger-contract" id="swagger-contract"></a>

{% embed url="https://editor.swagger.io/?url=https%3A%2F%2Fraw.githubusercontent.com%2Fegovernments%2FDIGIT-OSS%2Fmaster%2Fcore-services%2Fdocs%2Flocalisation-contract.yml" %}

>

&#x20;
