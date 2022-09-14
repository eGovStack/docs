# BPA Calculator Service

### Description <a href="#description" id="description"></a>

BPA application and BPA Occupancy Certificate application has Fee involved. Based on the Application Type, RiskType and ServiceType Fee to be calculated and generates a demand for the calculated amount for Payment. This service used to generate Application Fee, Sanction Fee, Low Application Permit Fee, Deviation Charges for BPA application and Occupancy Certificate Application.

### **System Requirements** <a href="#system-requirements" id="system-requirements"></a>

* Knowledge of Java/J2EE(preferably Java 8 version)
* Knowledge of Spring Boot and spring-boot microservices.
* Knowledge of Git or any version control system.
* Knowledge of RESTful Web services.
* Knowledge of the Lombok library will helpful.
* knowledge of eGov-mdms service, eGov-persister, eGov-idgen, eGov-sms, eGov-email, eGov-user, eGov-localization, bpa-services will be helpful.

### **Functionality**

bpa calculator services present in municipal services provide multiple functionalities like calculating Application Fee, Sanction Fee, Low Permit Fee, OC Deviation Charges, generating demands for a particular BPA, BPA OC applications, updating demands, The different functionalities provided by sewerage calculator services are:

#### **Setup and usage** <a href="#setup-and-usage" id="setup-and-usage"></a>

The [**Application**](https://github.com/egovernments/municipal-services/tree/master) is present among the _**municipal services**_ group of applications available in the eGov-services git repository with the folder name **bpa-calculator**. The spring boot application needs the **Lombok\*** extension added in your IDE to load it. Once the application is up and running API requests can be posted to the URL and ids can be generated.

* in case of IntelliJ, the plugin can be installed directly, for eclipse the Lombok jar location has to be added in eclipse.ini file in this format javaagent:lombok.jar

#### _**Application.properties File Information**_ <a href="#application.properties-file-information" id="application.properties-file-information"></a>

* Business service codes for
  * BPA High/Medium Risk Application Fee
    * egov.demand.appl.businessservice=BPA.NC\_APP\_FEE
  * BPA High/Medium Risk Sanction Fee
    * egov.demand.sanc.businessservice=BPA.NC\_SAN\_FEE
  * BPA Low Risk Permit Fee
    * egov.demand.lowriskpermit.businessservice=BPA.LOW\_RISK\_PERMIT\_FEE
  * BPA OC Application Fee
    * egov.demand.oc.appl.businessservice=BPA.NC\_OC\_APP\_FEE
  * BPA OC Sanction Fee
    * egov.demand.oc.sanc.businessservice=BPA.NC\_OC\_SAN\_FEE
* Tax Head Code for
  * BPA High/Medium Risk Application Fee
    * egov.appl.fee=BPA\_APPL\_FEES
  * BPA High/Medium Risk Sanction Fee
    * egov.sanc.fee= BPA\_SANC\_FEES
  * BPA Low Risk Sanction Fee
    * egov.low.sanc.fee= BPA\_LOW\_SANC\_FEES
  * BPA Low Risk Application Fee
    * egov.low.appl.fee=BPA\_LOW\_APPL\_FEES
  * BPA OC Application Fee
    * egov.oc.appl.fee=BPA\_OC\_APPL\_FEES
  * BPA OC Sanction Fee
    * egov.oc.sanc.fee= BPA\_OC\_SANC\_FEES

_**External Application references**_

* dcr-services (Use Edcr data )
* egov-mdms ( Configurations/master by MDMS )
* billing-service ( Generate and update demands )
* bpa-services (Get the bpa application data for fee calculation )

#### _**API Information**_ <a href="#api-information" id="api-information"></a>

* bpa-calculator/v1/\_calculate End point to calculate the Fee and create Demand with the applicable businessService and TaxHeads

#### MDMS Configuration: <a href="#mdms-configuration" id="mdms-configuration"></a>

|                     |                                                                                                                |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| ------------------- | -------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **MDMS Name**       | **Path**                                                                                                       | **Description**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        | **Example Json**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| **CalculationType** | [CalculationType](https://github.com/egovernments/egov-mdms-data/blob/master/data/pb/BPA/CalculationType.json) | <p>Used by bpa-calculator Service which Defines the Fee to be collected for Given ApplicationType, ServiceType, RiskType and feeType</p><p>2. Second Example defines the calculation logic to figure out the fee for the Service, considering the different parameters from EDCR information of the BPA.</p><p><strong>ParameterPath</strong> indicates the EDCR Response Data path to get the data point.</p><p><strong>from</strong></p><p>Indicates the from value of the data point to be considered</p><p><strong>to</strong></p><p>Indicates the to value of the data point to be considered</p><p><strong>MF</strong></p><p>multiplication factor to be considered to multiple the datapoint value to calculate the value when data point value falls between from and to</p><p><strong>UOM</strong></p><p>UOM to be considered to multiple the datapoint value and MF to calculate the Fee when data point value falls between from and to</p> | <p><code>{ "applicationType": "BUILDING_PLAN_SCRUTINY", "serviceType": "ALL", "riskType": "LOW", "feeType": "SanctionFee", "amount": 500 }, { "applicationType": "BUILDING_PLAN_SCRUTINY", "serviceType": "NEW_CONSTRUCTION", "riskType": "ALL", "feeType": "ApplicationFee", "amount": 120 }, { "applicationType": "BUILDING_PLAN_SCRUTINY", "serviceType": "NEW_CONSTRUCTION", "riskType": "LOW", "feeType": "Low_ApplicationFee", "amount": 100 }, { "applicationType": "BUILDING_OC_PLAN_SCRUTINY", "serviceType": "ALL", "riskType": "ALL", "feeType": "SanctionFee", "amount": 500, "calsiLogic": [ { "parameter": "builtuparea", "tolerancelimit": 10, "calculationType": "number", "deviation": [ { "from": 11, "to": 50, "MF": 1, "uom": 100 }, { "from": 51, "to": 100, "MF": 2, "uom": 150 }, { "from": 101, "to": 499, "MF": 3, "uom": 200 } ], "paramPath": "edcrDetail[0].planDetail.virtualBuilding.totalBuitUpArea" } ] }</code></p><p>From the above example</p><ol><li>indicates SanctionFee is Rs 500 for applicationType=BuildingPlanScrutiny, RiskType=LOW and any ServiceType</li><li><p>indicates applicationFee is Rs 120 for applicationType=BuildingPlanScrutiny, ServiceType=NEW_CONSTRUCTION and any RiskType</p><ol><li>indicates applicationFee is Rs 100 for applicationType=BuildingPlanScrutiny, ServiceType=NEW_CONSTRUCTION and RiskType=LOW</li></ol></li></ol> |

**Access MDMS Config**

bpa-calculator cannot be accessed publicly, Only called by the bpa-calculator

**Billing Service MDMS Config**

[BusinessService.json](https://github.com/egovernments/egov-mdms-data/blob/master/data/pb/BillingService/BusinessService.json)

BusinessService Config for Fee’s to be collected

Application Fee, Sanction Fee BPA High/Medium Risk

```
 {
      "businessService": "BPA.NEWCONSTRUCTION_APP_FEE",
      "code": "BPA.NC_APP_FEE",
      "collectionModesNotAllowed": [
        "DD"
      ],
      "partPaymentAllowed": false,
      "isAdvanceAllowed": false,
      "isVoucherCreationEnabled": true,
      "isActive": true
    },
    {
      "businessService": "BPA.NEWCONSTRUCTION_SANC_FEE",
      "code": "BPA.NC_SAN_FEE",
      "collectionModesNotAllowed": [
        "DD"
      ],
      "partPaymentAllowed": false,
      "isAdvanceAllowed": false,
      "isVoucherCreationEnabled": true,
      "isActive": true
    },
    
```

**Application Fee, Sanction Fee for BPA Low Risk**

```
{
      "businessService": "BPA.NEWCONSTRUCTION_LOW_RISK_PERMIT_FEE",
      "code": "BPA.LOW_RISK_PERMIT_FEE",
      "collectionModesNotAllowed": [
        "DD"
      ],
      "partPaymentAllowed": false,
      "isAdvanceAllowed": false,
      "isVoucherCreationEnabled": true,
      "isActive": true
    },
```

**Application Fee, Sanction Fee for BPA OC**

```
{
      "businessService": "BPA.NEWCONSTRUCTION_OC_APP_FEE",
      "code": "BPA.NC_OC_APP_FEE",
      "collectionModesNotAllowed": [
        "DD"
      ],
      "partPaymentAllowed": false,
      "isAdvanceAllowed": false,
      "isVoucherCreationEnabled": true,
      "isActive": true
    },
    {
      "businessService": "BPA.NEWCONSTRUCTION_OC_SANC_FEE",
      "code": "BPA.NC_OC_SAN_FEE",
      "collectionModesNotAllowed": [
        "DD"
      ],
      "partPaymentAllowed": false,
      "isAdvanceAllowed": false,
      "isVoucherCreationEnabled": true,
      "isActive": true
    }
```

**TaxHead MDMS**

[TaxHeader.json](https://github.com/egovernments/egov-mdms-data/blob/master/data/pb/BillingService/TaxHeadMaster.json)

Tax Head for BPA High/Medium Risk

```
{
      "category": "FEE",
      "service": "BPA.NC_APP_FEE",
      "name": "BPA Application fees",
      "code": "BPA_APPL_FEES",
      "isDebit": false,
      "isActualDemand": true,
      "order": "1",
      "isRequired": false
    },
    {
      "category": "FEE",
      "service": "BPA.NC_SAN_FEE",
      "name": "BPA Sanction fees",
      "code": "BPA_SANC_FEES",
      "isDebit": false,
      "isActualDemand": true,
      "order": "2",
      "isRequired": false
    },
   
```

TaxHead config for BPA Low Risk

```
 {
      "category": "FEE",
      "service": "BPA.LOW_RISK_PERMIT_FEE",
      "name": "BPA Low Risk Appllication Fees",
      "code": "BPA_LOW_APPL_FEES",
      "isDebit": false,
      "isActualDemand": true,
      "order": "1",
      "isRequired": false
    },
    {
      "category": "FEE",
      "service": "BPA.LOW_RISK_PERMIT_FEE",
      "name": "BPA Low Risk Permit Fees",
      "code": "BPA_LOW_SANC_FEES",
      "isDebit": false,
      "isActualDemand": true,
      "order": "1",
      "isRequired": false
    },
```

TaxHead config for BPA OC

```
 {
      "category": "FEE",
      "service": "BPA.NC_OC_APP_FEE",
      "name": "BPA Application fees",
      "code": "BPA_OC_APPL_FEES",
      "isDebit": false,
      "isActualDemand": true,
      "order": "1",
      "isRequired": false
    },
    {
      "category": "FEE",
      "service": "BPA.NC_OC_SAN_FEE",
      "name": "BPA Sanction fees",
      "code": "BPA_OC_SANC_FEES",
      "isDebit": false,
      "isActualDemand": true,
      "order": "2",
      "isRequired": false
    },
```

**TaxPeriod MDMS Config**

[TaxPeriod.json](https://github.com/egovernments/egov-mdms-data/blob/master/data/pb/BillingService/TaxPeriod.json)

TaxPeriod MDMS for BPA High/Medium Risk

```
{
      "fromDate": 1522540801000,
      "toDate": 1838159999000,
      "periodCycle": "FORTENYEARS",
      "service": "BPA.NC_APP_FEE",
      "code": "BPA10YRS2018",
      "financialYear": "2018-28"
    },
    {
      "fromDate": 1522540801000,
      "toDate": 1838159999000,
      "periodCycle": "FORTENYEARS",
      "service": "BPA.NC_SAN_FEE",
      "code": "BPA10YRS2018",
      "financialYear": "2018-28"
    },
```

TaxPeriod MDMS for BPA Low Risk

```
{
      "fromDate": 1522540801000,
      "toDate": 1838159999000,
      "periodCycle": "FORTENYEARS",
      "service": "BPA.LOW_RISK_PERMIT_FEE",
      "code": "BPA10YRS2018",
      "financialYear": "2018-28"
    },
```

TaxPeriod Config for BPA OC

```
{
      "fromDate": 1522540801000,
      "toDate": 1838159999000,
      "periodCycle": "FORTENYEARS",
      "service": "BPA.NC_OC_APP_FEE",
      "code": "BPAOCAPP10YRS2018",
      "financialYear": "2018-28"
    },
    {
      "fromDate": 1522540801000,
      "toDate": 1838159999000,
      "periodCycle": "FORTENYEARS",
      "service": "BPA.NC_OC_SAN_FEE",
      "code": "BPAOCSAN10YRS2018",
      "financialYear": "2018-28"
    }
```

### Workflow <a href="#workflow" id="workflow"></a>

NA

### Persister configuration <a href="#persister-configuration" id="persister-configuration"></a>

NA

### Database Schema <a href="#database-schema" id="database-schema"></a>

NA

### Notifications <a href="#notifications" id="notifications"></a>

NA

### PDF Configuration <a href="#pdf-configuration" id="pdf-configuration"></a>

NA

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation ](https://egov.org.in/)is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).
