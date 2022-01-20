# Sewerage Calculator Service

## Overview

Sewerage Calculator Service is one of the major business logic services which is used for calculation of sewerage charge, generating demand, update existing demand, SMS & email notification to the ULB officials on-demand generation and also triggering demands(job scheduler) at some intervals and estimation of sewerage charge(one-time cost) which involves cost like road-cutting charge, form fee, scrutiny fee etc.

## Pre-requisites

Before you proceed with the documentation, make sure the following pre-requisites are met -

* _Java 8_
* Kafka server is up and running
* egov-persister service is running and has sewerage service persister configs path added in it
* PSQL server is running and a database is created to store sewerage connection / application data
* Following services should be up and running:
  * egov-perister
  * egov-mdms
  * sw-services
  * billing-service

## Key Functionalities

Sewerage calculator services present in municipal services provide multiple functionalities like calculating sewerage charges, generating demands for a particular sewerage connection, updating demands, SMS & email notification to the ULB officials on-demand generation and also triggering demands(job scheduler) at some intervals and estimation of sewerage charge(one-time cost) which involves cost like road-cutting charge, form fee, scrutiny fee etc. The different functionalities provided by sewerage calculator services are:

* Sewerage charge calculation
* Demand generation(here as its always non-metered demand will be generated based on time period)
* Sewerage charge estimation (one-time cost which involves cost like road-cutting charge, form fee, scrutiny fee etc.)

## Deployment Details

1. Deploy the latest version of sw-service and sw-calculator
2. Add sewerage-persist.yml file in config folder in git and add that path in persister . _(The file path is to be added in environment yaml file in param called_ persist-yml-path _)_

## Configuration Details

### MDMS Configuration

#### **Billing Slabs**

Criteria :

1. connection type
2. building type
3. calculation attribute
4. property usage type

The combination of the above can be used to define the billing slab. Billing Slab is defined in MDMS under sw-services-calculation folder with the [SCBillingSlab](https://github.com/egovernments/egov-mdms-data/blob/QA/data/pb/sw-services-calculation/SCBillingSlab.json). The following is the sample slab.

```
{
  "tenantId": "pb",
  "moduleName": "sw-services-calculation",
  "SCBillingSlab": [
    {
      "id": "1",
      "buildingType": "RESIDENTIAL",
      "calculationAttribute": "No. of water closets",
      "connectionType": "Non Metered",
      "minimumCharge": 0,
      "slabs": [
        {
          "from": 0,
          "to": 1000000000,
          "charge": 15
        }
      ]
    },
    {
      "id": "2",
      "buildingType": "RESIDENTIAL",
      "calculationAttribute": "No. of toilets",
      "connectionType": "Non Metered",
      "minimumCharge": 0,
      "slabs": [
        {
          "from": 0,
          "to": 1000000000,
          "charge": 15
        }
      ]
    },
    {
      "id": "3",
      "buildingType": "NONRESIDENTIAL",
      "calculationAttribute": "No. of water closets",
      "connectionType": "Non Metered",
      "minimumCharge": 0,
      "slabs": [
        {
          "from": 0,
          "to": 1000000000,
          "charge": 30
        }
      ]
    },
    {
      "id": "4",
      "buildingType": "NONRESIDENTIAL",
      "calculationAttribute": "No. of toilets",
      "connectionType": "Non Metered",
      "minimumCharge": 0,
      "slabs": [
        {
          "from": 0,
          "to": 1000000000,
          "charge": 30
        }
      ]
    },
    {
      "id": "5",
      "buildingType": "Commercial",
      "calculationAttribute": "No. of water closets",
      "connectionType": "Non Metered",
      "minimumCharge": 0,
      "slabs": [
        {
          "from": 0,
          "to": 1000000000,
          "charge": 30
        }
      ]
    },
    {
      "id": "6",
      "buildingType": "Commercial",
      "calculationAttribute": "No. of toilets",
      "connectionType": "Non Metered",
      "slabs": [
        {
          "from": 0,
          "to": 1000000000,
          "charge": 30
        }
      ]
    },
    {
      "id": "7",
      "buildingType": "Government",
      "calculationAttribute": "No. of water closets",
      "connectionType": "Non Metered",
      "slabs": [
        {
          "from": 0,
          "to": 1000000000,
          "charge": 30
        }
      ]
    },
    {
      "id": "8",
      "buildingType": "Government",
      "calculationAttribute": "No. of toilets",
      "connectionType": "Non Metered",
      "slabs": [
        {
          "from": 0,
          "to": 1000000000,
          "charge": 30
        }
      ]
    },
    {
      "id": "9",
      "buildingType": "Partly Commercial",
      "calculationAttribute": "No. of water closets",
      "connectionType": "Non Metered",
      "slabs": [
        {
          "from": 0,
          "to": 1000000000,
          "charge": 25
        }
      ]
    },
    {
      "id": "10",
      "buildingType": "Partly Commercial",
      "calculationAttribute": "No. of toilets",
      "connectionType": "Non Metered",
      "slabs": [
        {
          "from": 0,
          "to": 1000000000,
          "charge": 25
        }
      ]
    },
    {
      "id": "11",
      "buildingType": "RESIDENTIAL",
      "calculationAttribute": "Flat",
      "connectionType": "Non Metered",
      "minimumCharge": 100,
      "slabs": []
    },
    {
      "id": "12",
      "buildingType": "NONRESIDENTIAL",
      "calculationAttribute": "Flat",
      "connectionType": "Non Metered",
      "minimumCharge": 250,
      "slabs": []
    },
    {
      "id": "13",
      "buildingType": "Commercial",
      "calculationAttribute": "Flat",
      "connectionType": "Non Metered",
      "minimumCharge": 250,
      "slabs": []
    },
    {
      "id": "14",
      "buildingType": "Government",
      "calculationAttribute": "Flat",
      "connectionType": "Non Metered",
      "minimumCharge": 350,
      "slabs": []
    },
    {
      "id": "15",
      "buildingType": "Partly commercial",
      "calculationAttribute": "Flat",
      "connectionType": "Non Metered",
      "minimumCharge": 200,
      "slabs": []
    }
  ]
}
```

If all criteria will match for that sewerage connection this slab will use for calculation.

#### Estimation

For application one-time fee, the estimation will return all the related tax head based on criteria. For estimation, all configuration is present in sw-services-calculation.

1. [FeeSlab.json](https://github.com/egovernments/egov-mdms-data/blob/master/data/pb/sw-services-calculation/FeeSlab.json)
2. [PlotSizeSlab.json](https://github.com/egovernments/egov-mdms-data/blob/master/data/pb/sw-services-calculation/PlotSizeSlab.json)
3. [RoadType.json](https://github.com/egovernments/egov-mdms-data/blob/master/data/pb/sw-services-calculation/RoadType.json)

All the above master configuration is used for estimation.

Following are the exemptions and taxes that are calculated:

* Form fee
* Scrutiny fee
* Other charges
* Road cutting charges
* One time fee
* Security charges
* Tax and cess

### Sewerage Charge and Tax

Sewerage charge is based on billing slab, for sewerage application charge will be based on slab and tax based on master configuration.

**Interest**

Below is a sample of master data JSON for interest :

```
{
  "tenantId": "pb",
  "moduleName": "sw-services-calculation",
  "Interest": [
    {
      "rate": 5,
      "minAmount": null,
      "applicableAfterDays":0,
      "flatAmount": null,
      "maxAmount": null,
      "fromFY": "2019-20",
      "startingDay": "1/01/2019"
    }
  ]
}
```

**Penalty**

Below is a sample of master data JSON for penalty\*\*:\*\*

```
{
  "tenantId": "pb",
  "moduleName": "sw-services-calculation",
  "Penalty": [
    {
      "rate": 10,
      "minAmount": null,
      "applicableAfterDays": 0,
      "flatAmount": null,
      "fromFY": "2019-20",
      "startingDay": "1/01/2019"
    }
  ]
}
```

**Round Off**

If the fraction is greater than equal to 0.5 the number is round up else it’s round down. eg: 100.4 will be rounded to 100 while 100.6 will be rounded to 101.

### Actions & Role Action Mapping

#### **Actions**

```
[
  {
      "id": {{PLACEHOLDER1}},
      "name": "Sewerage Calculation",
      "url": "/sw-calculator/sewerageCalculator/_calculate",
      "displayName": "Sewerage Calculation",
      "orderNumber": 0,
      "enabled": false,
      "serviceCode": "sw-calculator",
      "code": "null",
      "path": ""
    },
    {
      "id": {{PLACEHOLDER2}},
      "name": "Calculate Fee For Sewerage Application",
      "url": "/sw-calculator/sewerageCalculator/_estimate",
      "displayName": "Fee Calculation For Sewerage Application",
      "orderNumber": 0,
      "enabled": false,
      "serviceCode": "sw-calculator",
      "code": "null",
      "path": ""
    },
    {
      "id": {{PLACEHOLDER3}},
      "name": "Add adhoc tax to sewerage",
      "url": "/sw-calculator/sewerageCalculator/_applyAdhocTax",
      "displayName": "Add adhoc tax",
      "orderNumber": 0,
      "enabled": false,
      "serviceCode": "sw-calculator",
      "code": "null",
      "path": ""
    }
]


```

**Role Action Mapping**

```
[
    {
      "rolecode": "SW_CEMP",
      "actionid": {{PLACEHOLDER1}},
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "SW_CLERK",
      "actionid": {{PLACEHOLDER1}},
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "SW_DOC_VERIFIER",
      "actionid": {{PLACEHOLDER1}},
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "SW_FIELD_INSPECTOR",
      "actionid": {{PLACEHOLDER1}},
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "SW_APPROVER",
      "actionid": {{PLACEHOLDER1}},
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "SW_CEMP",
      "actionid": {{PLACEHOLDER2}},
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "SW_CLERK",
      "actionid": {{PLACEHOLDER2}},
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "SW_DOC_VERIFIER",
      "actionid": {{PLACEHOLDER2}},
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "SW_FIELD_INSPECTOR",
      "actionid": {{PLACEHOLDER2}},
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "SW_APPROVER",
      "actionid": {{PLACEHOLDER2}},
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "CITIZEN",
      "actionid": {{PLACEHOLDER2}},
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "SW_CEMP",
      "actionid": {{PLACEHOLDER2}},
      "actioncode": "",
      "tenantId": "pb"
    }

]
```

#### Demand Generation

Once sewerage is sent to the calculator, its tax estimates are calculated. Using the tax head estimates demand details are created. For every tax head, the estimated demand generates function will create a corresponding demand detail.

Whenever \_calculate API is called demand is first searched based on the connection no or application no and the demand from and to period. If demand already exists the same demand is updated else new demand is generated with consumer code as connection no or application no and demand from and to a period equal to financial year start and end period.

In the case of an update, if the tax head estimates change, the difference in amount for that tax head is added as new demand detail. For example, if the initial demand has one demand detail with SEWERAGE\_CHARGE equal to 120

```
"demandDetails": [
                {
                    "id": "77ba1e93-a535-409c-b9d1-a312c409bd45",
                    "demandId": "687c3176-305b-461d-9cec-2fa26a30c88f",
                    "taxHeadMasterCode": "SEWERAGE_CHARGE",
                    "taxAmount": 120,
                    "collectionAmount": 120,
                    "additionalDetails": null,
                    "auditDetails": {
                        "createdBy": "04956309-87cd-4526-b4e6-48123abd4f3d",
                        "lastModifiedBy": "04956309-87cd-4526-b4e6-48123abd4f3d",
                        "createdTime": 1583675275873,
                        "lastModifiedTime": 1583675298705
                    },
                    "tenantId": "pb.amritsar"
                }
            ],
```

After updating if the SEWERAGE\_CHARGE increases to 150 we add one more demand detail to account for the increased amount. The demand detail will be updated to:

```
"demandDetails": [
                {
                    "id": "77ba1e93-a535-409c-b9d1-a312c409bd45",
                    "demandId": "687c3176-305b-461d-9cec-2fa26a30c88f",
                    "taxHeadMasterCode": "SEWERAGE_CHARGE",
                    "taxAmount": 120,
                    "collectionAmount": 0,
                    "additionalDetails": null,
                    "auditDetails": {
                        "createdBy": "04956309-87cd-4526-b4e6-48123abd4f3d",
                        "lastModifiedBy": "04956309-87cd-4526-b4e6-48123abd4f3d",
                        "createdTime": 1583675275873,
                        "lastModifiedTime": 1583675298705
                    },
                    "tenantId": "pb.amritsar"
                },
                {
                    "id": "0d83f4b0-6442-11ea-bc55-0242ac130003 ",
                    "demandId": "687c3176-305b-461d-9cec-2fa26a30c88f",
                    "taxHeadMasterCode": "SEWERAGE_CHARGE",
                    "taxAmount": 30,
                    "collectionAmount": 0,
                    "additionalDetails": null,
                    "auditDetails": {
                        "createdBy": "04956309-87cd-4526-b4e6-48123abd4f3d",
                        "lastModifiedBy": "04956309-87cd-4526-b4e6-48123abd4f3d",
                        "createdTime": 1583675275873,
                        "lastModifiedTime": 1583675298705
                    },
                    "tenantId": "pb.amritsar"
                }
            ],
```

RoundOff is bill based i.e every time bill is generated round off is adjusted so that the payable amount is the whole number. Individual SW\_ROUNDOFF in demand detail can be greater than 0.5 but the sum of all SW\_ROUNDOFF will always be less than 0.5.

### Scheduler for generating the demand <a href="#scheduler-for-generating-the-demand" id="scheduler-for-generating-the-demand"></a>

#### **Description**

For generating the demand for non metered connection we have a feature for generating the demand in batch. The scheduler is responsible for generating the demand based on the tenant.

* The scheduler can be hit by scheduler API or we can schedule cron job or we can put config to kubectl which will hit scheduler based on config.
* After the scheduler been hit we will search the list of the tenant (city) present in the database.
* After getting the tenants we will pick up tenant one by one and generate the demand for that tenant.
* We will load the consumer codes for the tenant and push the calculation criteria to Kafka. Calculation criteria contain minimal information (We are not pushing large data to Kafka), calculation criteria contain consumer code and one boolean variable.
* After pushing the data into Kafka we are consuming the records based on the batch configuration. Ex:-> if the batch configuration is 50 so we will consume the 50 calculation criteria at a time.
* After consuming the record(Calculation criteria) we will process the batch for generating the demand. If the batch is successful so will log the consumer codes which have been processed.
* If some records failed in batch so we will push the batch into dead letter batch topic. From the dead letter batch topic, we will process the batch one by one.
* If the record is successful we will log the consumer code, If the record is failed so we will push the data into a dead letter single topic.
* Dead letter single topic contains information about failure records in Kafka.

_**Use cases**_

1. If the same job trigger multiple time what will happen?

If the same job triggers multiple times we will process again as mentioned above but at the demand level we will check the demand based on consumer code and billing period, If demand already exists then we will update the demand otherwise we will create the demand.

1. Are we maintaining success or failure status anywhere?

Currently, we are maintaining the status of failed records in Kafka.

_**Configuration**_

We need to configure the batch size for Kafka consumer. This configuration is for how much data will be processed at a time.`1sw.demand.based.batch.size=10`

## Integration Details

### Integration Scope

sw-calculator will be integrated with sw-service. sw-services internally invoke the sw-calculator service to calculate and generate demand for the charges.

### Integration Benefits

SW calculator application is used to calculate the sewerage application one time Fees and connection charges based on the different billing slabs that's why the calculation and demand generation logic will be separated out from SW service.\
So in future, if calculation logic needs to modify then changes can be carried out for each implementation without modifying the SW service.

### Steps to Integration

1. To Activate the Sewerage Service application, the user needs to pay the ONE\_TIME\_FEE for the connection. To calculate the ONE\_TIME\_FEE sw-calculator/sewerageCalculator/\_estimate API is use.
2. To generate the demand for non-metered sewerage connection /sw-calculator/sewerageCalculator/\_calculate API is use.
3. User can pay partial / full / advance amount for the Non-Metered connection bill. In these cases, Billing service would call back /sw-calculator/sewerageCalculator/\_updateDemandAPI to update the details of the demand generated.
4. /sw-calculator/sewerageCalculator/\_jobscheduler API is use to generate demand for Non-metered connections. This API can be called periodically.
5. /sw-calculator/sewerageCalculator/\_applyAdhocTax API is used to add Rebate or Penalty on any bill and based on that the bill amount will be adjusted.

## Reference Docs

#### Doc Links <a href="#doc-links" id="doc-links"></a>

|                           |                                                                                                                                                                                                                  |
| ------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Title**                 | **Link**                                                                                                                                                                                                         |
| API Swagger Contract      | [![](https://editor.swagger.io/dist/favicon-32x32.png)Swagger Editor](https://editor.swagger.io/?url=https://raw.githubusercontent.com/egovernments/municipal-services/master/docs/water-sewerage-services.yaml) |
| Sewerage Service Document | [Sewerage Service](https://digit-discuss.atlassian.net/l/c/ZYtv10g0)                                                                                                                                             |

#### API List <a href="#api-list" id="api-list"></a>

|                                                   |                                                                                                                            |
| ------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------- |
| Title                                             | **Link**                                                                                                                   |
| /sw-calculator/sewerageCalculatorr/\_estimate     | [https://www.getpostman.com/collections/e283373559ef0646d412](https://www.getpostman.com/collections/e283373559ef0646d412) |
| /sw-calculator/sewerageCalculator/\_calculate     | [https://www.getpostman.com/collections/e283373559ef0646d412](https://www.getpostman.com/collections/e283373559ef0646d412) |
| /sw-calculator/sewerageCalculator/\_updateDemand  | [https://www.getpostman.com/collections/e283373559ef0646d412](https://www.getpostman.com/collections/e283373559ef0646d412) |
| /sw-calculator/sewerageCalculator/\_jobscheduler  | [https://www.getpostman.com/collections/e283373559ef0646d412](https://www.getpostman.com/collections/e283373559ef0646d412) |
| /sw-calculator/sewerageCalculator/\_applyAdhocTax | [https://www.getpostman.com/collections/e283373559ef0646d412](https://www.getpostman.com/collections/e283373559ef0646d412) |

_(Note: All the API’s are in the same postman collection therefore same link is added in each row)_

\_\_

\_\_

> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)\_\_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_ ](https://egov.org.in)_is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
