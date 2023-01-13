# Fire NOC Calculator Service

## Overview

Fire-Noc calculator service is used to calculate the fire noc charges for the building based on the billing slab defined in the system. This service allows an employee with SUPERUSER role to create the billing slab with different combination of the height of the building, built\_-\_up area, plot size, number of floors etc.

## Pre-requisites

Before you proceed with the configuration, make sure the following pre-requisites are met -

* Prior knowledge of JavaScript.
* Prior knowledge of Node.js platform.
* Kafka server is up and running
* egov-persister service is running and has firenoc-calculator-persister config path added in it
* PSQL server is running and database is created to store firenoc application data
* Following services should be up and running:
  * egov-persister
  * egov-mdms
  * firenoc-services
  * billing-service

## Key Functionalities

* An employee with SUPERUSER role can create, update billing slab(s)
* ULB Employee with NOC\_CEMP, NOC\_DOC\_VERIFIER, NOC\_FIELD\_INSPECTOR, NOC\_APPROVER, EMPLOYEE can search billing slab(s)
* firenoc-services internally call firenoc-calculator to generate demand.

## Deployment Details

1. Deploy the latest version of firenoc-services and firenoc-calculator.
2. Add firenoc-calculator-persister.yml file in config folder in git and add that path in persister . _(The file path is to be added in environment yaml file in param called_ persist-yml-path _)_

## Configuration Details

### MDMS Configuration

Firenoc Calculator makes calls to egov-mdms-service to fetch required master files. These are significant in validations of application.

|                                                                                                                                   |                                                                                                              |
| --------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------ |
| **Fire-NOC masters**                                                                                                              | **Description**                                                                                              |
| [Building Type](https://github.com/egovernments/egov-mdms-data/blob/master/data/pb/firenoc/BuildingType.json)                     | This master file contains the details about which unit of measurement is use for a particular building type. |
| [FireNocStateConstats](https://github.com/egovernments/egov-mdms-data/blob/master/data/pb/firenoc/FireNocStateConstats.json)      | This master file contains state level constants and their values.                                            |
| [UOMs](https://github.com/egovernments/egov-mdms-data/blob/master/data/pb/firenoc/UOMs.json)                                      | This master file contains list of unit of measurements for firenoc                                           |
| [FireNocULBConstats](https://github.com/egovernments/egov-mdms-data/blob/master/data/pb/amritsar/firenoc/FireNocULBConstats.json) | This master file contains the list of state level constants and their values..                               |

## Integration Details

#### Integration Scope <a href="#integration-scope" id="integration-scope"></a>

firenoc-calculator will be integrated with firenoc-services. firenoc-services internally invoke the firenoc-calculator service to calculate and generate demand for the charges.

### Integration Benefits

Firenoc calculator application is used to calculate the fire noc charges for the building based on the different billing slabs in the DB that's why the calculation and demand generation logic will be separate out from firenoc services.\
So in future, if calculation logic needs to modify then changes can be carried out for each implementation without modifying the Firenoc services.

### Steps to Integration

1. Firenoc application to call /firenoc-calculator/v1/\_calculate to calculate and generate the demand for the Firenoc application
2. /firenoc-calculator/v1/\_getbill this API updates demand with time based penalty if applicable and generates bill for the given criteria.
3. ULB Employee can create billing slab calling /firenoc-calculator/billingslab/\_create
4. ULB Employee can update billing slab calling /firenoc-calculator/billingslab/\_update
5. ULB Employee can search billing slab calling /firenoc-calculator/billingslab/\_search

## Reference Docs

#### Doc Links <a href="#doc-links" id="doc-links"></a>

|                           |                                                                                                                                                                                                           |
| ------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Title**                 | **Link**                                                                                                                                                                                                  |
| API Swagger Contract      | [Swagger Editor](https://editor.swagger.io/?url=https://raw.githubusercontent.com/egovernments/municipal-services/master/firenoc-calculator/config/docs/contract/fire\_noc\_calculation\_service.yaml#!/) |
| Fire Noc Service Document | [Fire Noc Service](./)                                                                                                                                                                                    |

#### API List <a href="#api-list" id="api-list"></a>

|                                         |                                                                                                                            |
| --------------------------------------- | -------------------------------------------------------------------------------------------------------------------------- |
| Title                                   | **Link**                                                                                                                   |
| firenoc-calculator/billingslab/\_create | [https://www.getpostman.com/collections/1906fad8a6860fbadd55](https://www.getpostman.com/collections/1906fad8a6860fbadd55) |
| firenoc-calculator/billingslab/\_search | [https://www.getpostman.com/collections/1906fad8a6860fbadd55](https://www.getpostman.com/collections/1906fad8a6860fbadd55) |
| firenoc-calculator/billingslab/\_update | [https://www.getpostman.com/collections/1906fad8a6860fbadd55](https://www.getpostman.com/collections/1906fad8a6860fbadd55) |
| firenoc-calculator/v1/\_calculate       | [https://www.getpostman.com/collections/1906fad8a6860fbadd55](https://www.getpostman.com/collections/1906fad8a6860fbadd55) |
| firenoc-calculator/v1/\_getbill         | [https://www.getpostman.com/collections/1906fad8a6860fbadd55](https://www.getpostman.com/collections/1906fad8a6860fbadd55) |

_(Note: All the API’s are in the same postman collection therefore same link is added in each row)_

\_\_

\_\_

> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)\_\_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_ ](https://egov.org.in/)_is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
