# Appropriation Service

## Overview

Apportion service is used to apportion the amount paid against a bill among the different tax heads based on the implemented algorithm. The default algorithm uses the order of the tax head to apportion the tax head with the lowest order apportioned off first and the highest order tax head apportioned last.

## Pre-requisites

Before you proceed with the documentation, make sure the following pre-requisites are met -

* _Java 8_
* Kafka server is up and running
* egov-persister service is running and has apportioned persister config path added to it
* PSQL server is running and a database is created to store apportion audit data

## Key Functionalities

* Apportion payment in tax heads of bill
* Apportion advance amount in tax heads of demand during demand creation

|                                      |                                                                                           |
| ------------------------------------ | ----------------------------------------------------------------------------------------- |
| **Environment Variables**            | **Description**                                                                           |
| `egov.apportion.default.value.order` | If set to true will apportion of the negative amount first irrespective of tax head order |

## ![](blob:https://digit-discuss.atlassian.net/018f514c-9da6-4242-ac5b-bd91de04413d#media-blob-url=true\&id=64163d40-059e-418c-955d-97bd506369af\&collection=contentId-1656717351\&contextId=1656717351\&mimeType=image%2Fpng\&name=Bill%20Apportion%20Flow%20.png\&size=29437\&width=1102\&height=381)Deployment Details

1. Deploy the latest version of egov-apportion-service&#x20;
2. Add apportion persister yaml path in persister configuration

## Configuration Details

There is no separate configuration required. The TaxHead master that is configured in the billing service is only used

## Integration Details

### Integration Scope

Any payment service which wants to divide the paid amount into different tax head buckets can integrate with apportion service.

### Integration Benefits

* Apportions amount in tax heads

### Steps to Integration

1. To integrate, the host of egov-apportion-service should be overwritten in the helm chart
2. /apportion-service/v2/bill/\_apportion should be called to apportion the bill
3. /apportion-service/v2/demand/\_apportion should be called to apportion the advance amount in demands

## Interaction Diagram

![](../../../.gitbook/assets/demand-apportion-flow-.png)

## Reference Docs

### Doc Links <a href="#doc-links" id="doc-links"></a>

|                           |                                                                                                                    |
| ------------------------- | ------------------------------------------------------------------------------------------------------------------ |
| **Title**                 | **Link**                                                                                                           |
| Collection Service        | [Collection Service V2](https://digit-discuss.atlassian.net/wiki/spaces/DD/pages/1620574288/Collection+Service+V2) |
| Billing Service           | [Billing Service](https://digit-discuss.atlassian.net/wiki/spaces/DD/pages/1620672528/Billing+Service)             |
| API Swagger Documentation |                                                                                                                    |

### API List <a href="#api-list" id="api-list"></a>

|                                            |                                                                                                                            |
| ------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------- |
| Title                                      | **Link**                                                                                                                   |
| _/apportion-service/v2/bill/\_apportion_   | [https://www.getpostman.com/collections/142983a40e95da157b45](https://www.getpostman.com/collections/142983a40e95da157b45) |
| _/apportion-service/v2/demand/\_apportion_ | [https://www.getpostman.com/collections/142983a40e95da157b45](https://www.getpostman.com/collections/142983a40e95da157b45) |

_(Note: All the APIs are in the same postman collection therefore the same link is added in each row)_



[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)_​_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in/) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
