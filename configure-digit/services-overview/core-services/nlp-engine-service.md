# NLP Engine Service

## Overview

In the existing version of the chatbot, for the PGR complaint creation feature, the user has to select the city from a drop-down menu by visiting the mSeva website. This significantly reduces user convenience as the user is required to constantly switch pages.\
To overcome the above inconvenience, the nlp-engine service is used. The service has an algorithm that uses _**fuzzy matching**_ and _**pattern recognition**_ to recognise the city provided by the user as input. Based on the user input, the cities having the highest match ratio with the input are being returned as the output list. A list comprising all the city names in English, Punjabi and Hindi was used as a reference tool for this service.

## Pre-requisites

Before you proceed with the documentation, make sure the following pre-requisites are met -

* _Python._
* egov-mdms service is running and all the data related to the service are added to the MDMS repository.
* egov-running service is running.

## Key Functionalities

* Provides city fuzzy search feature which returns the list of cities having the highest match ratio with the input.
* City fuzzy search can support input data in _English, Hindi and Punjabi_ language.
* Provides locality fuzzy search feature which returns the list of localities having the highest match ratio with the input.

| Environment Variables  | Description                                                                                                                |
| ---------------------- | -------------------------------------------------------------------------------------------------------------------------- |
| `MDMS_MODULE_NAME`     | Contains the module name of mdms required for nlp-engine.                                                                  |
| `CITY_MASTER`          | Contains the file name of mdms master file which contains the city names in various locale.                                |
| `CITY_LOCALE_MASTER`   | Contains the file name of mdms master file which contains the tenantid of the cities present in `CityNames.json` mdms file |
| `STATE_LEVEL_TENANTID` | Contains the state level tenantid                                                                                          |

## Interaction Diagram

![](<../../../.gitbook/assets/image (302) (1).png>)

![](<../../../.gitbook/assets/image (284).png>)

<figure><img src="../../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (40).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (2) (3).png" alt=""><figcaption></figcaption></figure>

## Deployment Details

1. Add mdms configs required for nlp-engine service ([mdms folder](https://github.com/egovernments/egov-mdms-data/tree/QA/data/pb/Chatbot)) and restart mdms service.
2. Deploy the latest version of nlp-engine service.
3. Whitelist the city and locality fuzzy search APIs.

## Integration

### Integration Scope

The nlp-engine service is used to locate user city and locality by using fuzzy string matching and pattern recognition.

### Integration Benefits

* Currently integrated into the chatbots for locating user city and locality for complaint creation use case.
* This feature functionality can be extended for the other entities and can be used for a fuzzy search of those different entities.

### Steps to Integration

1. To integrate, the host of nlp-engine service module should be overwritten in the helm chart.
2. `/nlp-engine/fuzzy/city` should be added as the fuzzy search endpoint for a city search.
3. `/nlp-engine/fuzzy/locality` should be added as the fuzzy search endpoint for locality search.

## Reference Docs

#### Doc Links <a href="#doc-links" id="doc-links"></a>

| Description | Link                                                                                                                                                                                                                                |
| ----------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| NLP Chatbot | [<img src="https://ssl.gstatic.com/docs/documents/images/kix-favicon7.ico" alt="" data-size="line">Documentation on NLP Chatbot](https://docs.google.com/document/d/1Z3IgyjlZzAchlMPfURmUrgVfcSqU316R\_0Z6KNrRbLo/edit?usp=sharing) |

## API List

| Description                  | Link                                                                                                                       |
| ---------------------------- | -------------------------------------------------------------------------------------------------------------------------- |
| _/nlp-engine/fuzzy/city_     | [https://www.getpostman.com/collections/9cd7600909d4ed16c173](https://www.getpostman.com/collections/9cd7600909d4ed16c173) |
| _/nlp-engine/fuzzy/locality_ | [https://www.getpostman.com/collections/9cd7600909d4ed16c173](https://www.getpostman.com/collections/9cd7600909d4ed16c173) |

_(Note: All the APIs are in the same postman collection therefore the same link is added in each row)_

__

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_ ](https://egov.org.in/)_is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
