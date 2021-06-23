# URL Shortening Service

## Overview <a id="Overview"></a>

The URL shortening service is used to shorten long URLs. There may be requirement when we want to avoid sending very long urls to the user via SMS, Whatsapp etc, this service compresses the URL.

## Pre-requisites <a id="Pre-requisites"></a>

Before you proceed with the configuration, make sure the following pre-requisites are met -

1. Prior Knowledge of Java/J2EE
2. Prior Knowledge of SpringBoot
3. Prior Knowledge of REST APIs and related concepts like path parameters, headers, JSON etc.

## Key Functionalities <a id="Key-Functionalities"></a>

1. Compress long URLs.
2. Converted short URLs contains id, which is used by this service to identify and get longer URLs.

| **Environment Variable** | **Description** |
| :--- | :--- |
| host.name | Host name to append in short URL |
| db.persistance.enabled | The boolean flag to store the short URL in database when flag is set as TRUE. |

## Deployment Details <a id="Deployment-Details"></a>

* Deploy latest version of URL Shortening service

## API Details <a id="API-Details"></a>

### a\) POST /egov-url-shortening/shortener <a id="a)-POST-/egov-url-shortening/shortener"></a>

Receive long urls and converts them to shorter urls. Shortened urls contains urls to endpoint mentioned next. When user clicks on shortened URL, user is redirected to long URL.

### b\) GET /{id} <a id="b)-GET-/{id}"></a>

This shortened urls contains path to this endpoint. The service uses id used in last endpoint to get long URL. As response the user is redirected to long URL.

## Reference Docs <a id="Reference-Docs"></a>

### Doc Links <a id="Doc-Links"></a>

| **Title** | **Link** |
| :--- | :--- |
| Swagger API Contract | [API Contract](https://editor.swagger.io/?url=https://raw.githubusercontent.com/egovernments/core-services/master/docs/url-shortening_contract.yml#!/) |
| Local Setup | [URL Shortening Local Setup](https://github.com/egovernments/core-services/blob/master/egov-url-shortening/LOCALSETUP.md) |

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation ](https://egov.org.in/)is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).

