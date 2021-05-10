# MDMS \(Master Data Management Service\)

## Overview

One of the applications in the Digit core group of services aims to reduce the time spent by developers on writing codes to store and fetch master data \( primary data needed for module functionality \) which doesn’t have any business logic associated with them. Instead of writing APIs, creating tables in every different service to store and retrieve data that is seldom changed MDMS service keeps them at a single location for all modules and provides data on will with the help of no more than three lines of configuration.

## **Pre-requisites**

1. Prior Knowledge of Java/J2EE.
2. Prior Knowledge of Spring Boot.
3. Prior Knowledge of REST APIs and related concepts like path parameters, headers, JSON etc.
4. Prior knowledge of Git.
5. Advanced knowledge on how to operate JSON data would be an added advantage to understand the service.

## **Key Functionalities**

* Adds master data for usage without the need to create master data APIs in every module.
* Reads data from GIT directly with no dependency on any database services.

| **Environment Variables** | **Description** |
| :--- | :--- |
| egov.mdms.conf.path | The default value of folder where master data files are stored |
| masters.config.url | The default value of the file URL which contains master-config values |

## Deployment Details <a id="Deployment-Details"></a>

1. Deploy the latest version of Mdms-service
2. Add conf path for the file location
3. Add master config JSON path

## **Integration Details**

### Integration Scope <a id="Integration-Scope"></a>

The MDMS service provides ease of access to master data for any service.

### Integration Benefits <a id="Integration-Benefits"></a>

* No time spent writing repetitive codes with no business logic.

### Steps to Integration <a id="Steps-to-Integration"></a>

1. To integrate, host of egov-mdms-service should be overwritten in helm chart
2. _egov-mdms-service/v1/\_search_ should be added as the search endpoint for searching master data.
3. Mdms client from eGov snapshots should be added as mvn entity in pom.xml for ease of access since it provides mdms request pojos.

## Reference Docs

| Title | Link |
| :--- | :--- |
| egov-mdms sample data | [![](https://github.githubassets.com/favicon.ico)https://github.com/egovernments/egov-mdms-data/tree/DEV/data - Connect to preview](https://github.com/egovernments/egov-mdms-data/tree/DEV/data) |
| master-config.json | [![](https://github.githubassets.com/favicon.ico)https://github.com/egovernments/egov-mdms-data/blob/DEV/master-config.json - Connect to preview](https://github.com/egovernments/egov-mdms-data/blob/DEV/master-config.json) |

### API List <a id="API-List"></a>

| egov-mdms-service/v1/\_search | [https://www.getpostman.com/collections/fcc9a71375b674de1308](https://www.getpostman.com/collections/fcc9a71375b674de1308) |
| :--- | :--- |


[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation ](https://egov.org.in/)is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).

