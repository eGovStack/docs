# BPA Calculator Service

### Description <a id="Description"></a>

BPA application and BPA Occupancy Certificate application has Fee involved. Based on the Application Type, RiskType and ServiceType Fee to be calculated and generates a demand for the calculated amount for Payment. This service used to generate Application Fee, Sanction Fee, Low Application Permit Fee, Deviation Charges for BPA application and Occupancy Certificate Application.

### **System Requirements** <a id="System-Requirements:"></a>

* Knowledge of Java/J2EE\(preferably Java 8 version\)
* Knowledge of Spring Boot and spring-boot microservices.
* Knowledge of Git or any version control system.
* Knowledge of RESTful Web services.
* Knowledge of the Lombok library will helpful.
* knowledge of eGov-mdms service, eGov-persister, eGov-idgen, eGov-sms, eGov-email, eGov-user, eGov-localization, bpa-services will be helpful.

### **Functionality**

bpa calculator services present in municipal services provide multiple functionalities like calculating Application Fee, Sanction Fee, Low Permit Fee, OC Deviation Charges, generating demands for a particular BPA, BPA OC applications, updating demands, The different functionalities provided by sewerage calculator services are:

#### **Setup and usage** <a id="Setup-and-usage:"></a>

The [**Application**](https://github.com/egovernments/municipal-services/tree/master) is present among the _**municipal services**_ group of applications available in the eGov-services git repository with the folder name **bpa-calculator**.  The spring boot application needs the **Lombok\*** extension added in your IDE to load it. Once the application is up and running API requests can be posted to the URL and ids can be generated. 

* in case of IntelliJ, the plugin can be installed directly, for eclipse the Lombok jar location has to be added in eclipse.ini file in this format  javaagent:lombok.jar

#### _**Application.properties File Information**_ <a id="Application.properties-File-Information:"></a>

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

* dcr-services \(Use Edcr data \)
* egov-mdms \( Configurations/master by MDMS \)
* billing-service \( Generate and update demands \)
* bpa-services \(Get the bpa application data for fee calculation \)

#### _**API Information**_ <a id="API-Information-:"></a>

* bpa-calculator/v1/\_calculate End point to calculate the Fee and create Demand with the applicable businessService and TaxHeads

#### MDMS Configuration: <a id="MDMS-Configuration:"></a>

<table>
  <thead>
    <tr>
      <th style="text-align:left"><b>MDMS Name</b>
      </th>
      <th style="text-align:left"><b>Path</b>
      </th>
      <th style="text-align:left"><b>Description</b>
      </th>
      <th style="text-align:left"><b>Example Json</b>
      </th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><b>CalculationType</b>
      </td>
      <td style="text-align:left"><a href="https://github.com/egovernments/egov-mdms-data/blob/master/data/pb/BPA/CalculationType.json">CalculationType</a>
      </td>
      <td style="text-align:left">
        <p>Used by bpa-calculator Service which Defines the Fee to be collected for
          Given ApplicationType, ServiceType, RiskType and feeType</p>
        <p>2. Second Example defines the calculation logic to figure out the fee
          for the Service, considering the different parameters from EDCR information
          of the BPA.</p>
        <p><b>ParameterPath</b> indicates the EDCR Response Data path to get the data
          point.</p>
        <p><b>from</b>
        </p>
        <p>Indicates the from value of the data point to be considered</p>
        <p><b>to</b>
        </p>
        <p>Indicates the to value of the data point to be considered</p>
        <p><b>MF</b>
        </p>
        <p>multiplication factor to be considered to multiple the datapoint value
          to calculate the value when data point value falls between from and to</p>
        <p><b>UOM</b>
        </p>
        <p>UOM to be considered to multiple the datapoint value and MF to calculate
          the Fee when data point value falls between from and to</p>
      </td>
      <td style="text-align:left">
        <p> <code>{ &quot;applicationType&quot;: &quot;BUILDING_PLAN_SCRUTINY&quot;, &quot;serviceType&quot;: &quot;ALL&quot;, &quot;riskType&quot;: &quot;LOW&quot;, &quot;feeType&quot;: &quot;SanctionFee&quot;, &quot;amount&quot;: 500 }, { &quot;applicationType&quot;: &quot;BUILDING_PLAN_SCRUTINY&quot;, &quot;serviceType&quot;: &quot;NEW_CONSTRUCTION&quot;, &quot;riskType&quot;: &quot;ALL&quot;, &quot;feeType&quot;: &quot;ApplicationFee&quot;, &quot;amount&quot;: 120 }, { &quot;applicationType&quot;: &quot;BUILDING_PLAN_SCRUTINY&quot;, &quot;serviceType&quot;: &quot;NEW_CONSTRUCTION&quot;, &quot;riskType&quot;: &quot;LOW&quot;, &quot;feeType&quot;: &quot;Low_ApplicationFee&quot;, &quot;amount&quot;: 100 }, { &quot;applicationType&quot;: &quot;BUILDING_OC_PLAN_SCRUTINY&quot;, &quot;serviceType&quot;: &quot;ALL&quot;, &quot;riskType&quot;: &quot;ALL&quot;, &quot;feeType&quot;: &quot;SanctionFee&quot;, &quot;amount&quot;: 500, &quot;calsiLogic&quot;: [ { &quot;parameter&quot;: &quot;builtuparea&quot;, &quot;tolerancelimit&quot;: 10, &quot;calculationType&quot;: &quot;number&quot;, &quot;deviation&quot;: [ { &quot;from&quot;: 11, &quot;to&quot;: 50, &quot;MF&quot;: 1, &quot;uom&quot;: 100 }, { &quot;from&quot;: 51, &quot;to&quot;: 100, &quot;MF&quot;: 2, &quot;uom&quot;: 150 }, { &quot;from&quot;: 101, &quot;to&quot;: 499, &quot;MF&quot;: 3, &quot;uom&quot;: 200 } ], &quot;paramPath&quot;: &quot;edcrDetail[0].planDetail.virtualBuilding.totalBuitUpArea&quot; } ] }</code>
        </p>
        <p>From the above example</p>
        <ol>
          <li>indicates SanctionFee is Rs 500 for applicationType=BuildingPlanScrutiny,
            RiskType=LOW and any ServiceType</li>
          <li>indicates applicationFee is Rs 120 for applicationType=BuildingPlanScrutiny,
            ServiceType=NEW_CONSTRUCTION and any RiskType
            <ol>
              <li>indicates applicationFee is Rs 100 for applicationType=BuildingPlanScrutiny,
                ServiceType=NEW_CONSTRUCTION and RiskType=LOW</li>
            </ol>
          </li>
        </ol>
      </td>
    </tr>
  </tbody>
</table>

**Access MDMS Config**

bpa-calculator cannot be accessed publicly, Only called by the bpa-calculator

**Billing Service MDMS Config**

[BusinessService.json](https://github.com/egovernments/egov-mdms-data/blob/master/data/pb/BillingService/BusinessService.json)

BusinessService Config for Fee’s to be collected

Application Fee, Sanction Fee BPA High/Medium Risk

```text
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

```text
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

```text
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

```text
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

```text
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

```text
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

```text
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

```text
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

```text
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

### Workflow <a id="Workflow"></a>

NA

### Persister configuration <a id="Persister-configuration"></a>

NA

### Database Schema <a id="Database-Schema"></a>

NA

### Notifications <a id="Notifications"></a>

NA

### PDF Configuration <a id="PDF-Configuration"></a>

NA

