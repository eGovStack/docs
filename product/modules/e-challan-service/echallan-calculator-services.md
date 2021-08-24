# eChallan Calculator Services

## Overview

eChallan Calculator service is used to calculate the echallan amount based on the details present in echallan request. This module is designed in such a way that it can be used to serve echallan for different type of service.

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

* echallan service internally call echallan-calculator to generate demand.
* Based on the tax head and tax amount defined in echallan request, echallan calculator service creates the demand.
* After Demand creation, it calls the billing service to generate the fees.

## Configuration Details

**MDMS Config**

Define the tax period in the below MDMS file for the business service which is allowed in echallan service.

[https://github.com/egovernments/egov-mdms-data/blob/DEV/data/pb/BillingService/TaxPeriod.json](https://github.com/egovernments/egov-mdms-data/blob/DEV/data/pb/BillingService/TaxPeriod.json)

Define the taxhead in the below MDMS file for the business service which is allowed in echallan service.

[https://github.com/egovernments/egov-mdms-data/blob/DEV/data/pb/BillingService/TaxHeadMaster.json](https://github.com/egovernments/egov-mdms-data/blob/DEV/data/pb/BillingService/TaxHeadMaster.json)

Define the action and role action mapping for the API’s in the below MDMS files.

[https://github.com/egovernments/egov-mdms-data/blob/DEV/data/pb/ACCESSCONTROL-ACTIONS-TEST/actions-test.json](https://github.com/egovernments/egov-mdms-data/blob/DEV/data/pb/ACCESSCONTROL-ACTIONS-TEST/actions-test.json)

[https://github.com/egovernments/egov-mdms-data/blob/DEV/data/pb/ACCESSCONTROL-ROLEACTIONS/roleactions.json](https://github.com/egovernments/egov-mdms-data/blob/DEV/data/pb/ACCESSCONTROL-ROLEACTIONS/roleactions.json)

## Deployment Details

1. Add MDMS configs required for eChallan Service and calculator and restart MDMS service.
2. Deploy the latest version of eChallan Service and calculator.
3. Add eChallan Service persister yaml path in persister configuration and restart persister service
4. Add Role-Action mapping for API’s.

## Integration

### Integration Scope

echallan-calculator will be integrated with echallan-services. echallan-services internally invoke the echallan-calculator service to calculate and generate demand for the echallan request.

### Integration Benefits

eChallan calculator application is used to calculate the eChallan Fees based on the data mentioned in echallan creation. Based on the tax amount mentioned in the echallan, demand is created. So because of eChallan calculator, the calculation and demand generation logic will be separated out from eChallan services.  
So in future, if calculation logic needs to modify then changes can be carried out for each implementation without modifying the eChallan services.

### Steps to Integration

eChallan service application needs to call echallan-calculator/v1/\_calculate API to calculate and generate the demand for the eChallan application.

### Interaction Diagram

TBD

## Reference Docs

#### Doc Links <a id="Doc-Links"></a>

| **Title** | **Link** |
| :--- | :--- |
| API Swagger Contract | [![](https://editor.swagger.io/dist/favicon-32x32.png)Swagger Editor](https://editor.swagger.io/?url=https://raw.githubusercontent.com/egovernments/municipal-services/develop/docs/e-Challan-v1.0.0.yaml#!/) |
| eChallan Service Document | [eChallans Service](https://digit-discuss.atlassian.net/l/c/CHpaLj9c) |

#### API List <a id="API-List"></a>

| Title | **Link** |
| :--- | :--- |
| echallan-calculator/v1/\_calculate | [https://www.getpostman.com/collections/349413e52bf743d50b0a](https://www.getpostman.com/collections/349413e52bf743d50b0a) |

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)_​_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in/) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._

