# e-Challan Calculator Service

## Overview

e-Challan Calculator service is used to calculate the e-challan amount based on the details present in the e-challan request. This module is designed in such a way that it can be used to serve e-challan for different types of services.

## Pre-requisites

Before you proceed with the configuration, make sure the following pre-requisites are met -

* _Java 8_
* Kafka server is up and running.
* PSQL server is running and a database is created to store eChallan Calculator Application data.
* Following services should be up and running:
  * egov-mdms
  * echallan-services
  * billing-service

## Key Functionalities

* e-challan service internally call e-challan-calculator to generate demand.
* Based on the tax head and tax amount defined in e-challan request, e-challan calculator service creates the demand.
* After Demand creation, it calls the billing service to generate the fees.

## Configuration Details

**MDMS Config**

Define the tax period in the below MDMS file for the business service defined in the e-challan service.

[https://github.com/egovernments/egov-mdms-data/blob/DEV/data/pb/BillingService/TaxPeriod.json](https://github.com/egovernments/egov-mdms-data/blob/DEV/data/pb/BillingService/TaxPeriod.json)

Define the tax head in the below MDMS file for the business service defined in the e-challan service.

[https://github.com/egovernments/egov-mdms-data/blob/DEV/data/pb/BillingService/TaxHeadMaster.json](https://github.com/egovernments/egov-mdms-data/blob/DEV/data/pb/BillingService/TaxHeadMaster.json)

Define the action and role action mapping for the APIs in the below MDMS files.

[https://github.com/egovernments/egov-mdms-data/blob/DEV/data/pb/ACCESSCONTROL-ACTIONS-TEST/actions-test.json](https://github.com/egovernments/egov-mdms-data/blob/DEV/data/pb/ACCESSCONTROL-ACTIONS-TEST/actions-test.json)

[https://github.com/egovernments/egov-mdms-data/blob/DEV/data/pb/ACCESSCONTROL-ROLEACTIONS/roleactions.json](https://github.com/egovernments/egov-mdms-data/blob/DEV/data/pb/ACCESSCONTROL-ROLEACTIONS/roleactions.json)

## Deployment Details

1. Add MDMS configs required for e-Challan Service and calculator and restart MDMS service.
2. Deploy the latest version of e-Challan Service and calculator.
3. Add e-Challan Service persister yaml path in persister configuration and restart persister service
4. Add role-action mapping for APIs.

## Integration

### Integration Scope

e-Challan-calculator is integrated with e-Challan-services. The e-Challan-services internally invoke the e-Challan-calculator service to calculate and generate demand for the e-Challan request.

### Integration Benefits

The e-Challan calculator application is used to calculate the e-Challan Fees based on the data mentioned in e-Challan creation. Based on the tax amount mentioned in the e-Challan, demand is created. So because of the e-Challan calculator, the calculation and demand generation logic is separated out from eChallan services.\
So in future, if calculation logic requires changes, the modifications can be carried out for each implementation without making any changes to the e-Challan services.

### Steps to Integration

e-Challan service application needs to call the eChallan-calculator/v1/\_calculate API to calculate and generate the demand for the e-Challan application.

### Interaction Diagram

TBD

## Reference Docs

#### Doc Links <a href="#doc-links" id="doc-links"></a>

| Title                     | Link                                                                                                                                                                                                          |
| ------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| API Swagger Contract      | [![](https://editor.swagger.io/dist/favicon-32x32.png)Swagger Editor](https://editor.swagger.io/?url=https://raw.githubusercontent.com/egovernments/municipal-services/develop/docs/e-Challan-v1.0.0.yaml#!/) |
| eChallan Service Document | [eChallans Service](https://digit-discuss.atlassian.net/l/c/CHpaLj9c)                                                                                                                                         |

#### API List <a href="#api-list" id="api-list"></a>

| Title                              | Link                                                                                                                       |
| ---------------------------------- | -------------------------------------------------------------------------------------------------------------------------- |
| echallan-calculator/v1/\_calculate | [https://www.getpostman.com/collections/349413e52bf743d50b0a](https://www.getpostman.com/collections/349413e52bf743d50b0a) |

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)_​_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in/) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
