# NLP Engine Service

## Overview

In the existing version of the chatbot, for PGR complaint creation feature, the user has to select his/her city from a drop-down menu by visiting the mseva website. This significantly reduces user convenience as the user is required to constantly switch pages.\
To overcome the above inconvenience, nlp-engine service is used. The service has an algorithm that uses _**fuzzy matching**_ and _**pattern recognition**_ to recognise the city provided by the user as input. Based on the user input, the cities having the highest match ratio with the input are being returned as the output list. A list comprising all the city names in English, Punjabi and Hindi was used as a reference tool for this service.

## Pre-requisites

Before you proceed with the documentation, make sure the following pre-requisites are met -

* _Python._
* egov-mdms service is running and all the data related to the service are added in the mdms repository.
* egov-running service is running.

## Key Functionalities

* Provides city fuzzy search feature which returns the list of cities having the highest match ratio with the input.
* City fuzzy search can support input data in _English, Hindi and Punjabi_ language.
* Provides locality fuzzy search feature which returns the list of localities having the highest match ratio with the input.

|                           |                                                                                                                            |
| ------------------------- | -------------------------------------------------------------------------------------------------------------------------- |
| **Environment Variables** | **Description**                                                                                                            |
| `MDMS_MODULE_NAME`        | Contains the module name of mdms required for nlp-engine.                                                                  |
| `CITY_MASTER`             | Contains the file name of mdms master file which contains the city names in various locale.                                |
| `CITY_LOCALE_MASTER`      | Contains the file name of mdms master file which contains the tenantid of the cities present in `CityNames.json` mdms file |
| `STATE_LEVEL_TENANTID`    | Contains the state level tenantid                                                                                          |

## Interaction Diagram

![](<../../../../.gitbook/assets/image (302).png>)

![](<../../../../.gitbook/assets/image (284).png>)

![](<../../../../.gitbook/assets/image (298).png>)

![](<../../../../.gitbook/assets/image (293).png>)

![](<../../../../.gitbook/assets/image (299).png>)

## Deployment Details

1. Add mdms configs required for nlp-engine service ([mdms folder](https://github.com/egovernments/egov-mdms-data/tree/QA/data/pb/Chatbot)) and restart mdms service.
2. Deploy the latest version of nlp-engine service.
3. Whitelist the city and locality fuzzy search API’s.

## Integration

### Integration Scope

The nlp-engine service is used to locate the user city and locality by using fuzzy string matching and pattern recognition.

### Integration Benefits

* Currently integrated into the chatbots for locating user city and locality for complaint creation use case.
* This feature functionality can be extended for the other entities and can be used for a fuzzy search of those different entities.

### Steps to Integration

1. To integrate, the host of nlp-engine service module should be overwritten in the helm chart.
2. `/nlp-engine/fuzzy/city` should be added as the fuzzy search endpoint for a city search.
3. `/nlp-engine/fuzzy/locality` should be added as the fuzzy search endpoint for locality search.

## Reference Docs

#### Doc Links <a href="#doc-links" id="doc-links"></a>

|             |                                                                                                                                                                                                      |
| ----------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Title**   | **Link**                                                                                                                                                                                             |
| NLP Chatbot | [![](https://ssl.gstatic.com/docs/documents/images/kix-favicon7.ico)Documentation on NLP Chatbot](https://docs.google.com/document/d/1Z3IgyjlZzAchlMPfURmUrgVfcSqU316R\_0Z6KNrRbLo/edit?usp=sharing) |

## API List

|                              |                                                                                                                            |
| ---------------------------- | -------------------------------------------------------------------------------------------------------------------------- |
|                              | **Link**                                                                                                                   |
| _/nlp-engine/fuzzy/city_     | [https://www.getpostman.com/collections/9cd7600909d4ed16c173](https://www.getpostman.com/collections/9cd7600909d4ed16c173) |
| _/nlp-engine/fuzzy/locality_ | [https://www.getpostman.com/collections/9cd7600909d4ed16c173](https://www.getpostman.com/collections/9cd7600909d4ed16c173) |

_(Note: All the API’s are in the same postman collection therefore same link is added in each row)_
