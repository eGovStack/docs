# Trade License Calculator

## Overview

Trade License Calculator service is used to calculate the Trade license fees / renewal fees based on the defined billing slabs. This service enables the TL admins to create billing slab with different combination of license type, trade type, structure type and accessory type.  
The service is designed in such a way that it can be used to serve different type of licenses.

## Pre-requisites

Before you proceed with the configuration, make sure the following pre-requisites are met -

* _Java 8_
* Kafka server is up and running
* egov-persister service is running and has tl-calculation-persister & tl-billing-slab-persister config path added in it
* PSQL server is running and a database is created to store TL Application data
* Following services should be up and running:
  * egov-perister
  * egov-mdms
  * tl-services
  * billing-service

## Key Functionalities

* TL Admin an Employee of ULB with TL\_Admin role can create, update billing slab\(s\)
* ULB Employee with TL\_CREATOR and TL\_ADMIN can search billing slab\(s\)
* TL service internally calls tl-calculator to generate demand.

## Deployment Details

1. Deploy the latest version of tl-service and tl-calculator
2. Add tl-calculation-persister.yml & tl-billing-slab-persister.yml file in config folder in git and add that path in persister . _\(The file path is to be added in environment yaml file in param called_ persist-yml-path _\)_

## Configuration Details

### MDMS Configuration

#### **MDMS for Penalty Calculation**

```text
{
  "tenantId": "pb",
  "moduleName": "TradeLicense",
  "Penalty": [
    {
      "rate": 10,
      "minAmount": 0.0,
      "flatAmount": 0.0,
      "fromFY": "2018-19",
      "startingDay": "1/09/2018"
    },
    {
      "rate": 10,
      "minAmount": 0.0,
      "flatAmount": 0.0,
      "fromFY": "2015-16",
      "startingDay": "1/04/2016"

    }
  ]
}
```

#### **MDMS file for Rebate Calculation**

```text
{
  "tenantId": "pb",
  "moduleName": "TradeLicense",
  "Rebate": [
    {
      "rate": 10,
      "maxAmount": null,
      "flatAmount": 0.0,
      "fromFY": "2018-19",
      "endingDay": "31/03"

    },
    {
      "rate": 10,
      "maxAmount": null,
      "flatAmount": 0.0,
      "fromFY": "2019-20",
      "endingDay": "31/03"
    }
  ]  
}
```

### Actions & Role Action Mapping

#### **Actions**

```text
[
  {
    "id": {{PLACEHOLDER1}},
    "name": "TL BillingSlab Create",
    "url": "/tl-calculator/billingslab/_create",
    "displayName": "TL BillingSlab Create",
    "orderNumber": 1,
    "parentModule": "",
    "enabled": false,
    "serviceCode": "",
    "code": "null",
    "path": ""
  },
  {
    "id": {{PLACEHOLDER2}},
    "name": "TL BillingSlab Update",
    "url": "/tl-calculator/billingslab/_update",
    "displayName": "TL BillingSlab Update",
    "orderNumber": 1,
    "parentModule": "",
    "enabled": false,
    "serviceCode": "",
    "code": "null",
    "path": ""
  },
  {
    "id": {{PLACEHOLDER3}},
    "name": "TL BillingSlab Search",
    "url": "/tl-calculator/billingslab/_search",
    "displayName": "TL BillingSlab Search",
    "orderNumber": 1,
    "parentModule": "",
    "enabled": false,
    "serviceCode": "",
    "code": "null",
    "path": ""
  },
  {
    "id": {{PLACEHOLDER4}},
    "name": "TL Calculation",
    "url": "/tl-calculator/v1/_calculate",
    "displayName": "TL Calculation",
    "orderNumber": 1,
    "parentModule": "",
    "enabled": false,
    "serviceCode": "",
    "code": "null",
    "path": ""
  }
]
```

#### **Role Action Mapping**

```text
[
  {
    "rolecode": "TL_ADMIN",
    "actionid": "{{PLACEHOLDER1}}",
    "actioncode": "",
    "tenantId": "pb"
  },
  {
    "rolecode": "TL_ADMIN",
    "actionid": "{{PLACEHOLDER2}}",
    "actioncode": "",
    "tenantId": "pb"
  },
  {
    "rolecode": "TL_CREATOR",
    "actionid": "{{PLACEHOLDER3}}",
    "actioncode": "",
    "tenantId": "pb"
  },
  {
    "rolecode": "TL_CEMP",
    "actionid": "{{PLACEHOLDER3}}",
    "actioncode": "",
    "tenantId": "pb"
  },
  {
    "rolecode": "TL_CEMP",
    "actionid": "{{PLACEHOLDER4}}",
    "actioncode": "",
    "tenantId": "pb"
  }
]
```

## Integration Details

### Integration Scope

tl-calculator will be integrated with tl-services. tl-services internally invoke the tl-calculator service to calculate and generate demand for the charges.

### Integration Benefits

Tl calculator application is used to calculate the Trade license Fees based on the different billing slabs in the DB that's why the calculation and demand generation logic will be separated out from TL services.  
So in future, if calculation logic needs to modify then changes can be carried out for each implementation without modifying the TL services.

### Steps to Integration

1. TL application to call /tl-calculator/v1/\_calculate to calculate and generate the demand for the TL application
2. ULB Employee can create billing slab calling /tl-calculator/billingslab/\_create
3. ULB Employee can update billing slab calling /tl-calculator/billingslab/\_update
4. ULB Employee can search billing slab calling /tl-calculator/billingslab/\_search

### Interaction Diagram

TBD

## Reference Docs

#### Doc Links <a id="Doc-Links"></a>

| **Title** | **Link** |
| :--- | :--- |
| API Swagger Contract | [![](https://editor.swagger.io/dist/favicon-32x32.png)Swagger Editor](https://editor.swagger.io/?url=https://raw.githubusercontent.com/egovernments/egov-services/master/docs/rainmaker/trade-license/tl-calculator.yml#!/) |
| Trade License Document | [Trade License Service](https://digit-discuss.atlassian.net/l/c/WQ1uMqaa) |

#### API List <a id="API-List"></a>

| Title | **Link** |
| :--- | :--- |
| tl-calculator/billingslab/\_create | [https://www.getpostman.com/collections/a3d3bca66635df2395a3](https://www.getpostman.com/collections/a3d3bca66635df2395a3) |
| tl-calculator/billingslab/\_search | [https://www.getpostman.com/collections/a3d3bca66635df2395a3](https://www.getpostman.com/collections/a3d3bca66635df2395a3) |
| tl-calculator/billingslab/\_update | [https://www.getpostman.com/collections/a3d3bca66635df2395a3](https://www.getpostman.com/collections/a3d3bca66635df2395a3) |
| tl-calculator/v1/\_calculate | [https://www.getpostman.com/collections/a3d3bca66635df2395a3](https://www.getpostman.com/collections/a3d3bca66635df2395a3) |

_\(Note: All the API’s are in the same postman collection therefore the same link is added in each row\)_

\_\_

\_\_

> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)\_\_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_ ](https://egov.org.in/)_is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._

