# PT Calculator

## Overview

PT-Calculator Service is used for creating demands based on property assessments, mutations, and updating demands with the penalty, interest in case of payment delay.

## Pre-requisites

Before you proceed with the documentation, make sure the following pre-requisites are met -

* _Java 8_
* Kafka server is up and running
* PSQL server is running and a database is created to store property/application data
* Following services should be up and running:
  * MDMS
  * property-services
  * billing-service

## Key Functionalities

* Calculate property tax, mutation fee based on billing slab.
* create and update demand.

## Deployment Details

1. Deploy the latest version of property service and pt-calculator

#### Billing Slabs

Criteria:

* Property Type
* Property Subtype
* Usage Category Major
* Usage Category Minor
* Usage Category Subminor
* Usage Category Detail
* Ownership Category
* Sub Ownership Category
* Plot Size
* Floor Number
* Area Type

The combination of the above variables can be used to define a billing slab. The billing slabs are stored in db in the table named “eg\_pt\_billingslab\_v2”. To perform CRUD operations on the billing slabs API’s are provided in the module. Following is a sample create request:

```text
{
    "RequestInfo": {
        "apiId": "string",
        "ver": "string",
        "ts": 0,
        "action": "string",
        "did": "string",
        "key": "string",
        "msgId": "string",
        "requesterId": "string",
        "authToken": "cfc03668-a90f-4bf8-a955-53b8691dc112"
    },
    "BillingSlab": [
        {
            "tenantId": "pb.amritsar",
            "id": "7d32f05b-1e0a-f618-d26a-1ea65272a289",
            "propertyType": "BUILTUP",
            "propertySubType": "SHAREDPROPERTY",
            "usageCategoryMajor": "RESIDENTIAL",
            "usageCategoryMinor": "ALL",
            "usageCategorySubMinor": "ALL",
            "usageCategoryDetail": "ALL",
            "ownerShipCategory": "INDIVIDUAL",
            "subOwnerShipCategory": "ALL",
            "areaType": "AREA1",
            "fromPlotSize": 55.57,
            "toPlotSize": null,
            "occupancyType": "SELFOCCUPIED",
            "fromFloor": 2,
            "toFloor": 31,
            "unitRate": 2,
            "isPropertyMultiFloored": true,
            "unBuiltUnitRate": 2,
            "arvPercent": 0,
            "auditDetails": {
                "createdBy": "23594",
                "lastModifiedBy": null,
                "createdTime": 1535100744685,
                "lastModifiedTime": 0
            }
        }
    ]
}
```

The ‘ALL' keyword can be used if the slab is independent of that particular variable. If ‘fromPlotSize’ or ‘toPlotSize’ values are null they will set to positive infinity and negative infinity, a similar process will be for ‘fromFloor’ and 'toFloor’ values.

#### Estimation

The estimation service class loops through all the units and calculates the tax based on the applicable billing slab. The exemptions are calculated using master data in MDMS Service. Each tax or exemption is added to the tax head estimate. Following are the exemptions and taxes that are calculated:

* Property Base Tax
* Owner Exemption
* Unit Exemption
* Penalty
* Rebate
* Interest
* Fire Cess
* Cancer Cess

  From the above charges and exemptions penalty, interest and rebate are time-based. Rebate is given if the payment is done before the rebate deadline date specified in Rebate master data. Similarly, the penalty is charged if payment is not done before the deadline to pay tax. After the deadline to pay tax is passed daily interest is charged according to the rate defined in the master.

#### Property Tax <a id="Property-Tax:"></a>

Property tax is calculated by adding the tax for each unit calculated using the billing slab for that unit. The formula for calculating tax for the unit is:

```text
unitTax = unitArea * slabRate
```

In case the unit is commercial and rented the formula is as follows:

```text
unitTax = arv * slabArvPercent/100
```

ARV stands for Annual rent value.

If the property contains ground units \(i.e unit with floor number = 0\) then tax is also calculated for the unbuilt area. The formula for calculating the tax on the unbuilt area is as follows:

```text
diffArea = landArea - builtUpArea
unbuilt tax = (unBuiltRate / groundUnitsCount) * (diffArea)
```

#### Interest <a id="Interest:"></a>

Below is a sample of master data JSON for interest :

```text
{
  "tenantId": "pb",
  "moduleName": "PropertyTax",
  "Interest": [
    {
      "rate": 18,
      "minAmount": null,
      "flatAmount": null,
      "maxAmount": null,
      "fromFY": "2015-16",
      "startingDay": "1/01/2016"
    },
    {
      "rate": 12,
      "minAmount": null,
      "flatAmount": null,
      "maxAmount": null,
      "fromFY": "2015-16",
      "startingDay": "1/04/2016"
    },
    {
      "rate": 9,
      "minAmount": null,
      "flatAmount": null,
      "maxAmount": null,
      "fromFY": "2018-19",
      "startingDay": "11/12/2018"
    }
  ]
}
```

If the given year rate is not defined the service will recursively fall back on the previous year until it finds a defined rate slab. The time for which interest is applicable is calculated by subtracting the epoch value of starting day \(At 00:00 AM\) from the end of the day \(23:59 PM\) epoch value of the current date. In the case of partial payment, the interest is calculated for each interval between payments and summed as the applicable amount for interest won’t be constant throughout.

#### Round Off <a id="Round-Off:"></a>

If the fraction is greater than equal to 0.5 the number is round up else it’s round down. eg: 100.4 will be rounded to 100 while 100.6 will be rounded to 101

#### Penalty <a id="Penalty:"></a>

The following is the format of penalty master data:

```text
{
  "tenantId": "pb",
  "moduleName": "PropertyTax",
  "Penalty": [
    {
      "rate": 10,
      "minAmount": null,
      "flatAmount": null,
      "fromFY": "2018-19",
      "startingDay": "1/01/2019"
    }
  }
```

If the time during the demand creation date is greater than the penalty starting day, a penalty of x% will be applied. The x% is defined in the rate field. The penalty also provides a fallback for master data i.e if for a particular year entry is not present it will recursively search for the previous year and apply that rate.

#### Owner Exemption <a id="Owner-Exemption:"></a>

Depending on the owner type of user flat amount or percentage of tax amount is given as exemption. In the case of multiple owners, the exemption is calculated for each owner and summed. Following is a sample master data:

```text
{
  "tenantId": "pb",
  "moduleName": "PropertyTax",
  "OwnerType": [
    {
      "name": "Freedom Fighter",
      "code": "FREEDOMFIGHTER",
      "active": true,
      "fromFY": "2015-16",
      "exemption": {
        "rate": 100,
        "maxAmount": null,
        "flatAmount": null
      }
    },
    {
      "name": "Handicapped Person",
      "code": "HANDICAPPED",
      "active": true,
      "fromFY": "2015-16",
      "exemption": {
        "rate": null,
        "maxAmount": null,
        "flatAmount": 5000
      }
    }
    {
      "name": "None of the above",
      "code": "NONE",
      "active": true,
      "fromFY": "2015-16"
    }
  ]
}
```

#### Demand Generation

Once the property is sent to the calculator its tax estimates are calculated. Using these tax head estimates demand details are created. For every tax head, the estimate-demand function will create a corresponding demand detail.

Whenever \_calculate API is called demand is first searched based on the property id and the demand from and to period. If demand already exists the same demand is updated else new demand is generated with consumer code as property and demand from and to a period equal to financial year start and end period. In the case of Reassessment, the demand is always updated for the given year.

In case of update, if the tax head estimates changes, the difference in amount for that tax head is added as new demand detail. For example, if the initial demand has one demand detail with PT\_TAX equal to 100

```text
            "demandDetails": [
                {
                    "id": "77ba1e93-a535-409c-b9d1-a312c409bd45",
                    "demandId": "687c3176-305b-461d-9cec-2fa26a30c88f",
                    "taxHeadMasterCode": "PT_TAX",
                    "taxAmount": 100,
                    "collectionAmount": 100,
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

After updating if the PT\_TAX increases to 150 we add one more demand detail to account for the increased amount. The demand detail will be updated to:

```text
            "demandDetails": [
                {
                    "id": "77ba1e93-a535-409c-b9d1-a312c409bd45",
                    "demandId": "687c3176-305b-461d-9cec-2fa26a30c88f",
                    "taxHeadMasterCode": "PT_TAX",
                    "taxAmount": 100,
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
                    "taxHeadMasterCode": "PT_TAX",
                    "taxAmount": 50,
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

RoundOff is bill-based i.e every time bill is generated round-off is adjusted so that the payable amount is the whole number. Individual PT\_ROUNDOFF in demand detail can be greater than 0.5 but the sum of all PT\_ROUNDOFF will always be less than 0.5.

#### Example: <a id="Example:"></a>

If demand is created and the total tax is supposed 100.40, then a negative round-off amount of -0.40 is added so that the tax becomes 100. If during reassessment the tax changes and becomes 111.70, to round it off estimate will give tax head estimate of +0.3. The demand generation logic will add a new demand detail by taking the difference in the old and new tax amount for that tax head. Therefore a new demand detail of 0.3-\(-0.4\)=0.7 will be added. There will be now two PT\_ROUNDOFF tax heads one with an amount -0.4 and the other with 0.7 making the total round-off amount \(-0.4+0.7\)= 0.3 which with the tax amount of 111.70 will give a bill amount of 111.70+0.3=112.

## Integration Details

### Integration Scope

PT-calculator should be integrated with property-services which internally invokes the calculator service to calculate and generate demand for the charges.

### Integration Benefits

Carries out the process of creating demand and updating them on a need basis as per the requirement of assessment and mutation.

### Steps to Integration

1. /\_caluclate should be exposed internally for property-services integration.
2. /\_estimate API should be exposed for UI integration, which enables users to view the estimate before proceeding.
3. /demand/\_update API should be configured in billing service for demand update function on bill expiry.

## Reference Docs

Property-services[ Property Services](./)

API Collection - [https://www.getpostman.com/collections/d7c858f62b53d17c4335](https://www.getpostman.com/collections/d7c858f62b53d17c4335)

> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)\_\_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_ ](https://egov.org.in/)_is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._

