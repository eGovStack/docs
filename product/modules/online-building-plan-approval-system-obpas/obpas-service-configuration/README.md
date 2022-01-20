# OBPAS Service Configuration

## Description

Construction or renovation of buildings is regulated by Municipal Body in India. One must get permission from the ULB prior to construction. This process involves submitting the building plan to ULB along with other documents, ULB verifies the plan with other documents and approves the construction. The document which authorizes the construction is called “**Permit Order**” One must have this permit order with him till the completion of construction. ULB officials will inspect various stages of construction and make sure it is in compliance with the plan. When construction completed, after inspection Secretary provides a “**Completion certificate**” and finally will provide an “**Occupancy Certificate**”. This entire process is known as “Building Plan Approval”.

## Functionality

This section covers the high-level details of the functionalities available in the Building Plan Application system.

* Centralized login page for citizen, official and stakeholders
* Citizen functionalities
* Online application submission - New construction
* Occupancy certificate request
* FieldInspection Report Capture
* Pay fee online and generate permit order online
* Inspection of applications and online status
* Configurable workflow
* Auto fee calculation
* Online and offline payment collection
* Rejection process
* Revocation process
* Configurable functionalities

## **System Requirements**

* Knowledge of Java/J2EE(preferably Java 8 version)
* Knowledge of Spring Boot and spring-boot microservices
* Knowledge of Git or any version control system
* Knowledge of RESTful Web services
* Knowledge of the Lombok library will helpful
* knowledge of eGov-mdms service, eGov-persister, eGov-idgen, eGov-sms, eGov-email,eGov-user, eGov-localization, eGov-workflow-service,dcr, land-services, bpa-calculator will be helpful

## **Setup and usage** <a href="#setup-and-usage" id="setup-and-usage"></a>

The [**Application**](https://github.com/egovernments/municipal-services/tree/master) is present among the _**municipal services**_ group of applications available in the eGov-services git repository with the folder name **bpa-services**. The spring boot application needs the **Lombok\*** extension added in your IDE to load it. Once the application is up and running API requests can be posted to the URL and ids can be generated.

* in the case of IntelliJ, the plugin can be installed directly, for eclipse the Lombok jar location has to be added in eclipse.ini file in this format javaagent:lombok.jar

## _**API Information**_ <a href="#api-information" id="api-information"></a>

* Please refer to Swagger API for YAML file details. Link - [API Specs](https://github.com/egovernments/municipal-services/blob/master/docs/bpa/bpa-service.yaml).

## _**Application.properties File Information**_ <a href="#application.properties-file-information" id="application.properties-file-information"></a>

Here we are listing the configs apart from dependent service host, URLs, DB and Flyway configs.

* kafka topics persister configs for eGov persister to save and update BPA Data
  * `persister.save.buildingplan.topic=save-bpa-buildingplan`
  * `persister.update.buildingplan.topic=update-bpa-buildingplan`
  * `persister.update.buildingplan.workflow.topic=update-bpa-workflow`
  * `persister.update.buildingplan.adhoc.topic=update-bpa-adhoc-buildingplan`
* Receipt kafka topics where BPA application listens to move the application Status after payment completion
  * `kafka.topics.receipt.create=egov.collection.payment-create`
* Config for Demand Business service codes for different fees to be paid for BPA
  * **egov.receipt.businessservice**=
    * BPA.NC\_APP\_FEE := Building Plan Approval Application Fee
    * BPA.NC\_SAN\_FEE := Building Plan Approval Sanction Fee
    * BPA.LOW\_RISK\_PERMIT\_FEE := Building Plan Approval Low Risk Permit Fee
    * BPA.NC\_OC\_APP\_FEE := Building Plan Approval Occupancy Certificate Application Fee
    * BPA.NC\_OC\_SAN\_FEE := Building Plan Approval Occupancy Certificate Sanction Fee
* Application and Permit Number Formats
  * `egov.idgen.bpa.applicationNum.format=PB-BP-[cy:yyyy-MM-dd]-[SEQ_EG_BP_APN]`
  * `egov.idgen.bpa.permitNum.format=PB-BP-[cy:yyyy-MM-dd]-[SEQ_EG_BP_PN]`
* SMS Notification Topic to push the SMS and Notification’s to be sent by BPA module
  * `kafka.topics.notification.sms=egov.core.notification.sms`
* Payment Notification Config
  * `egov.ui.app.host=https://egov-micro-dev.egovernments.org`
  * `egov.usr.events.create.topic=persist-user-events-async`
  * `egov.usr.events.pay.link=citizen/otpLogin?mobileNo=$mobile&redirectTo=egov-common/pay?consumerCode=$applicationNo&tenantId=$tenantId&businessService=$businessService`
  * `egov.usr.events.pay.code=PAY`
* List of Application Statuses on which payment notification to be sent
  * `egov.usr.events.pay.triggers=PENDING_SANC_FEE_PAYMENT,PENDING_APPL_FEE,PENDING_FEE`
* Validity of the permit order generated in no of months
  * `egov.bpa.validity.date.in.months=36`
* Workflow code for the combination of applicationType , ServiceType
  * `appSrvTypeBussSrvCode={"BUILDING_PLAN_SCRUTINY":{"NEW_CONSTRUCTION":"BPA,BPA_LOW"},"BUILDING_OC_PLAN_SCRUTINY":{"NEW_CONSTRUCTION":"BPA_OC"}}`
* Application Status on which SKIP\_PAYMENT action to be considered
  * `egov.bpa.skippayment.status=PENDING_APPL_FEE,PENDING_SANC_FEE_PAYMENT,PENDING_FEE`
* Business Service Code for WorkflowCode and Application Status
  * `workflowStatusFeeBusinessSrvMap={"BPA":{"PENDING_APPL_FEE":"BPA.NC_APP_FEE","PENDING_SANC_FEE_PAYMENT":"BPA.NC_SAN_FEE"},"BPA_LOW":{"PENDING_FEE":"BPA.LOW_RISK_PERMIT_FEE"},"BPA_OC":{"PENDING_APPL_FEE":"BPA.NC_OC_APP_FEE","PENDING_SANC_FEE_PAYMENT":"BPA.NC_OC_SAN_FEE"}}`
* NOC application Integration configs
  * Config to validate the status of applicable noc’s status to allow the application to move forward from NOC\_VERIFICATION\_PENDING Workflow State
    * `validate.required.nocs.statuses=APPROVED,AUTO_APPROVED,REJECTED,VOIDED`
  * NOC workflow initiate action code to initiate the workflow of the NOC when the appliation reachers the respective nocTrigerState
    * `egov.noc.initiate.action=INITIATE`
  * NOC workflow void action code to void the applicable NOC’s, when the application moved to REJECTED State
    * `egov.noc.void.action=VOID`
  * NOC workflow action goes for AutoAprove to auto-approve offline NOC , while moving from NOC\_VERIFICATION\_PENDING to the next state
    * `egov.noc.autoapprove.action=AUTO_APPROVE`

## **External API References**

* **egov-user** - (Manage user)
* **tl-services** - Stakeholder Registration (Registration process of Stakeholder is handled by this service)
* **egov-user-event** (What’s New and Events)
* **egov-filestore** (To store the documents uploaded by the user)
* **egov-idgen** (To generate the application No, Permit No)
* **egov-indexer** (To index the BPA data)
* **egov-localization** (To use the localized messages)
* **egov-location** (To store the address locality)
* **egov-mdms** (Configurations/master data used in the application is served by MDMS)
* **egov-notification-sms** (Service to send SMS to the users involved in the application)
* **egov-persister** (Helps to persist the data)
* **egov-searcher** (Search query used to simplify the search)
* **egov-workflow-v2** (Workflow configuration for different BPA application is configured)
* **pdf-service** (Receipt’s, permit order etc.. and prepared)
* **billing-service** (Create demands and bills for the fees to be collected)
* **collection-services** (Create a receipt for the payment received for the bills)
* **bpa-calculator** (Calculates the fees to be collected at different stages)
* **land-services** (land information related to BPA application is stored)
* **dcr-services** (get and validate EDCR data)
* **noc-services** (NOC application)

## **Configuration** <a href="#configuration" id="configuration"></a>

### _**BPA Specific Mdms configuration**_ <a href="#bpa-specific-mdms-configuration" id="bpa-specific-mdms-configuration"></a>

[MDMS Github Repo](https://github.com/egovernments/egov-mdms-data/tree/master)

Under the data/\<state code> folder you can find the **BPA** which has all the MDMS JSON’s

master-config.json for BPA

```
"BPA": {
    "ServiceType": {
      "masterName": "ServiceType",
      "isStateLevel": true,
      "uniqueKeys": [
        "$.code"
      ]
    },
    "ApplicationType": {
      "masterName": "ApplicationType",
      "isStateLevel": true,
      "uniqueKeys": [
        "$.code"
      ]
    },
    "DocTypeMapping": {
      "masterName": "DocTypeMapping",
      "isStateLevel": true,
      "uniqueKeys": [
        "$.code"
      ]
    },
    "CalculationType": {
      "masterName": "CalculationType",
      "isStateLevel": true,
      "uniqueKeys": []
    },
    "RiskTypeComputation": {
      "masterName": "RiskTypeComputation",
      "isStateLevel": true,
      "uniqueKeys": []
    },
    "OccupancyType": {
      "masterName": "OccupancyType",
      "isStateLevel": true,
      "uniqueKeys": [
        "$.code"
      ]
    },
    "SubOccupancyType": {
      "masterName": "SubOccupancyType",
      "isStateLevel": true,
      "uniqueKeys": [
        "$.code"
      ]
    },
    "CheckList": {
      "masterName": "CheckList",
      "isStateLevel": true,
      "uniqueKeys": [
        "$.question"
      ]
    }
  }
```

### MDMS Details <a href="#mdms-details" id="mdms-details"></a>

|                         |                                                                                                                        |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| ----------------------- | ---------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **MDMS Name**           | **MDMS Path**                                                                                                          | **Description**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 | **Example**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| **ServiceType**         | [ServiceType](https://github.com/egovernments/egov-mdms-data/blob/master/data/pb/BPA/ServiceType.json)                 | Values for ServiceType Dropdown                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 | NA                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| **Application Type**    | [ApplicationType](https://github.com/egovernments/egov-mdms-data/blob/master/data/pb/BPA/ApplicationType.json)         | Values for Application Type Dropdown                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            | NA                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| **Occupancy Type**      | [OccupancyType](https://github.com/egovernments/egov-mdms-data/blob/master/data/pb/BPA/OccupancyType.json)             | Values for Occupancy Type Dropdown                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              | NA                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| **SubOccupancy Type**   | [SubOccupancyType](https://github.com/egovernments/egov-mdms-data/blob/master/data/pb/BPA/SubOccupancyType.json)       | Values for SubOccupancy Type Dropdown                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           | NA                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| **DocumentTypeMapping** | [DocumentTypeMapping](https://github.com/egovernments/egov-mdms-data/blob/master/data/pb/BPA/DocTypeMapping.json)      | <p>List’s out the documents required at the given stage of the application for Given ApplicationType, ServiceType, RiskType and WorklowState.</p><p>In the docTypes we have</p><ul><li>Order - Indicates the sequence of the document</li><li>Code - Refers to the DocumentType parentGroup from <a href="https://github.com/egovernments/egov-mdms-data/blob/master/data/pb/common-masters/DocumentType.json">DocumentTypes</a> from common masters MDMS</li><li>allow - Indicates allow to edit</li><li>required - Mandatory at given stage</li></ul>                                                                                                                         | <p><code>{ "applicationType": "BUILDING_PLAN_SCRUTINY", "ServiceType": "NEW_CONSTRUCTION", "RiskType": "LOW", "WFState": "INPROGRESS", "docTypes": [ { "code": "APPL.IDENTITYPROOF", "required": false, "allow": "false", "order": 1 }, { "code": "APPL.ADDRESSPROOF", "required": true, "allow": "true", "order": 2 } ]}</code></p><p>Above example indicates Documents from the common-master documentTypes starting with code(s) in the above example should be displayed in BPA Application UI when the Application of <strong>ApplicationType</strong> -BUILDINGPLAN_SCRUTINY<br><strong>ServiceType-</strong> NEW_CONSTRUCTION<br><strong>RiskType-</strong> LOW<br><strong>Workflow State -</strong> INPROGRESS<br><br>Out of this,<br>IDENTITY documentType is not allowed to upload in this stage and not mandatory.<br>ADDRESSPROOF documentType is allowed to upload in this stage and mandatory to move forward from this stage.</p>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| **CalculationType**     | [CalculationType](https://github.com/egovernments/egov-mdms-data/blob/master/data/pb/BPA/CalculationType.json)         | Used by bpa-calculator Service which Defines the Fee to be collected for Given ApplicationType, ServiceType, RiskType and feeType                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | <p><code>{ "applicationType": "BUILDING_PLAN_SCRUTINY", "serviceType": "ALL", "riskType": "LOW", "feeType": "SanctionFee", "amount": 500 }, { "applicationType": "BUILDING_PLAN_SCRUTINY", "serviceType": "NEW_CONSTRUCTION", "riskType": "ALL", "feeType": "ApplicationFee", "amount": 120 }, { "applicationType": "BUILDING_PLAN_SCRUTINY", "serviceType": "NEW_CONSTRUCTION", "riskType": "LOW", "feeType": "Low_ApplicationFee", "amount": 100 },</code></p><p>From the above example<br><br></p><ol><li>indicates SanctionFee is Rs 500 for applicationType=BuildingPlanScrutiny, RiskType=LOW and any ServiceType</li><li><p>indicates applicationFee is Rs 120 for applicationType=BuildingPlanScrutiny, ServiceType=NEW_CONSTRUCTION and any RiskType</p><ol><li>indicates applicationFee is Rs 100 for applicationType=BuildingPlanScrutiny, ServiceType=NEW_CONSTRUCTION and RiskType=LOW</li></ol></li></ol>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| **RiskTypeComputation** | [RiskTypeComputation](https://github.com/egovernments/egov-mdms-data/blob/master/data/pb/BPA/RiskTypeComputation.json) | Helps to Defines the RiskType of the Application based on the building Height and plotArea received from the EDCR System                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        | `{"fromPlotArea": 500, "toPlotArea": 9999999999, "fromBuildingHeight": 15, "toBuildingHeight":9999999999, "riskType": "HIGH", "note": "(Heigh 15 Mt or More) or ( Plot area >=800 sq.Mt)" }`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| **CheckList**           | [CheckList](https://github.com/egovernments/egov-mdms-data/blob/master/data/pb/BPA/CheckList.json)                     | <ol><li>Used to Define the List of Questions and Documents to be attached on Field Inspection Pending Stage by Field Inspector.</li></ol><p>The Example indicates</p><p>Four Questions with fieldType “YES/NO/NA“ ( Which indicates that field of type dropdown with Yes, NO and NA options) should be asked.</p><p>Readable question will be available in</p><p>2. Used to configure the conditions for Approval Stage</p><p>Condition checkboxes to be shown before approve which can be considered as Conditions for Approval</p>                                                                                                                                            | <ol><li>Field Inspection Questions &#x26; Documents <code>{ "applicationType": "BUILDING_PLAN_SCRUTINY", "ServiceType": "NEW_CONSTRUCTION", "RiskType": "LOW", "WFState": "FIELDINSPECTION_PENDING", "questions": [ { "question": "RIVER_EXISTS_ON_SITE", "fieldType": "YES/NO/NA", "active": true }, { "question": "TREE_EXISTS_ON_SITE", "fieldType": "YES/NO/NA", "active": true }, { "question": "PLAN_AS_PER_THE_SITE", "fieldType": "YES/NO/NA", "active": true }, { "question": "ROADWIDTH_AS_PER_THE_PLAN", "fieldType": "YES/NO/NA", "active": true } ], "docTypes": [ { "code": "FI.FIR", "required": true }, { "code": "FI.SINS", "required": true }, { "code": "FI.SISS", "required": true }, { "code": "FI.SIES", "required": true }, { "code": "FI.SIWS", "required": true } ] }</code></li></ol><p>2. Conditions for Approval Stage <code>{ "applicationType": "BUILDING_PLAN_SCRUTINY", "ServiceType": "NEW_CONSTRUCTION", "RiskType": "HIGH", "WFState": "PENDINGAPPROVAL", "conditions": [ "The development shall be undertaken strictly according to plans enclosed with necessary permission endorsement.", "The land in question must be in lawful ownership and peaceful possession of the applicant.", "The permission is valid for period of X(this is the validity period in years) years with effect from the date of issue.", "Permission accorded under the provision cannot be construed as evidence in respect of right title interest of the plot over which the plan is approved.", "Any dispute arising out of land record or in respect of right/ title/ interest after this approval the plan shall be treated automatically cancelled during the period of dispute.", "Adequate safety precaution shall be provided at all stages of construction for safe guarding the life of workers and any public hazard.", "The land/ Building shall be used exclusively for the above occupancy for which you applied and the uses shall not be changed to any other use without prior approval of this Authority.", "Adequate space mentioned in the approved plan shall be kept open for parking and no part of it will be built upon.", "The land over which construction is proposed is accessible by an approved means of access with sufficient road width." ] }</code></p> |
| NocTypeMapping          | [NocTypeMaping](https://github.com/egovernments/egov-mdms-data/blob/master/data/pb/BPA/NocTypeMapping.json)            | <p>Mapping of the NOC Types applicable for BPA ApplicationType, ServiceType and riskType</p><p>From the Example</p><p><strong>AIRPORT_AUTHORITY, NOC_FIRE</strong> NOC’s are applicable for applicationType → BULDING_PLAN_SCRUTINY</p><p>serviceType-> NEW_CONSTRUCTION</p><p>riskType-> ALL ( Any )</p><p>NocTypes-> list out the NOC Type object</p><p>and NOC Applications get created when BPA is created by the NOC’s Workflow would be initiated when the BPA application Status is equl to the nocTriggerState configured. ( According to this example, when the application status changes to Citizen Approval Pending, all the NOc’s workflow would be initiated)</p> | `{ "applicationType": "BUILDING_PLAN_SCRUTINY", "serviceType": "NEW_CONSTRUCTION", "riskType": "ALL", "nocTriggerState": "CITIZEN_APPROVAL_INPROCESS", "nocTypes": [ { "type": "AIRPORT_AUTHORITY", "required": true }, { "type": "FIRE_NOC", "required": false } ] }`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |

### Access MDMS Config <a href="#access-mdms-config" id="access-mdms-config"></a>

**Action Test : URL Actions adding**

[action-test.json](https://github.com/egovernments/egov-mdms-data/blob/master/data/pb/ACCESSCONTROL-ACTIONS-TEST/actions-test.json)\`\`

```
  {
      "id": 1971,
      "name": "BPA-PermitOrderEDCR Report",
      "url": "/bpa-services/v1/bpa/_permitorderedcr",
      "displayName": "Apply",
      "orderNumber": 0,
      "enabled": false,
      "serviceCode": "BPA",
      "code": "null",
      "path": ""
    }, {
      "id": 1975,
      "name": "Locality searcher endpoint for BPA",
      "url": "/egov-searcher/locality/bpa-services/_get",
      "displayName": "BPA locality searcher",
      "orderNumber": 0,
      "enabled": false,
      "serviceCode": "egov-searcher",
      "code": "null",
      "path": ""
    },{
      "id": 1924,
      "name": "BPA-Applyforservice",
      "url": "/bpa-services/v1/bpa/_create",
      "displayName": "Apply",
      "orderNumber": 0,
      "enabled": false,
      "serviceCode": "BPA",
      "code": "null",
      "path": ""
    }, {
      "id": 1930,
      "name": "BPA-applicationsearch",
      "url": "/bpa-services/v1/bpa/_search",
      "displayName": "Search",
      "orderNumber": 0,
      "enabled": false,
      "serviceCode": "BPA",
      "code": "null",
      "path": ""
    },{
      "id": 1931,
      "name": "BPA-updateapplicationservice",
      "url": "/bpa-services/v1/bpa/_update",
      "displayName": "Apply",
      "orderNumber": 0,
      "enabled": false,
      "serviceCode": "BPA",
      "code": "null",
      "path": ""
    },
```

**Access to the Roles for the above Actions**

[roleacton.json](https://github.com/egovernments/egov-mdms-data/blob/master/data/pb/ACCESSCONTROL-ROLEACTIONS/roleactions.json)\`\`

```
{
      "rolecode": "CEMP",
      "actionid": 1971,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "BPA_TOWNPLANNER",
      "actionid": 1971,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "BPA_BUILDER",
      "actionid": 1971,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "BPA_STRUCTURALENGINEER",
      "actionid": 1971,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "BPA_SUPERVISOR",
      "actionid": 1971,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "BPA_VERIFIER",
      "actionid": 1971,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "BPA_FIELD_INSPECTOR",
      "actionid": 1971,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "BPA_NOC_VERIFIER",
      "actionid": 1971,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "BPA_APPROVER",
      "actionid": 1971,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "BPA_ARCHITECT",
      "actionid": 1971,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "CITIZEN",
      "actionid": 1971,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "BPA_ENGINEER",
      "actionid": 1971,
      "actioncode": "",
      "tenantId": "pb"
    },
     {
      "rolecode": "BPA_VERIFIER",
      "actionid": 1975,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "BPA_FIELD_INSPECTOR",
      "actionid": 1975,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "BPA_NOC_VERIFIER",
      "actionid": 1975,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "BPA_APPROVER",
      "actionid": 1975,
      "actioncode": "",
      "tenantId": "pb"
    },
     {
      "rolecode": "BPA_ARCHITECT",
      "actionid": 1924,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "BPA_ARCHITECT",
      "actionid": 1931,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "CITIZEN",
      "actionid": 1931,
      "actioncode": "",
      "tenantId": "pb"
    }, {
      "rolecode": "BPA_VERIFIER",
      "actionid": 1931,
      "actioncode": "",
      "tenantId": "pb"
    }, {
      "rolecode": "BPA_APPROVER",
      "actionid": 1931,
      "actioncode": "",
      "tenantId": "pb"
    },
     {
      "rolecode": "BPA_FIELD_INSPECTOR",
      "actionid": 1931,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "BPA_NOC_VERIFIER",
      "actionid": 1931,
      "actioncode": "",
      "tenantId": "pb"
    },{
      "rolecode": "BPA_ARCHITECT",
      "actionid": 1930,
      "actioncode": "",
      "tenantId": "pb"
    },{
      "rolecode": "BPA_VERIFIER",
      "actionid": 1930,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "CEMP",
      "actionid": 1930,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "BPA_APPROVER",
      "actionid": 1930,
      "actioncode": "",
      "tenantId": "pb"
    },  {
      "rolecode": "CITIZEN",
      "actionid": 1930,
      "actioncode": "",
      "tenantId": "pb"
    }, {
      "rolecode": "BPA_FIELD_INSPECTOR",
      "actionid": 1930,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "BPA_NOC_VERIFIER",
      "actionid": 1930,
      "actioncode": "",
      "tenantId": "pb"
    },{
      "rolecode": "AIRPORT_AUTHORITY_APPROVER",
      "actionid": 1930,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "FIRE_NOC_APPROVER",
      "actionid": 1930,
      "actioncode": "",
      "tenantId": "pb"
    },
    {
      "rolecode": "NOC_DEPT_APPROVER",
      "actionid": 1930,
      "actioncode": "",
      "tenantId": "pb"
    }
```

### Billing Service MDMS Config <a href="#billing-service-mdms-config" id="billing-service-mdms-config"></a>

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

Application Fee, Sanction Fee for BPA Low Risk

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

Application Fee, Sanction Fee for BPA OC

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

### TaxHead MDMS <a href="#taxhead-mdms" id="taxhead-mdms"></a>

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

### TaxPeriod MDMS Config <a href="#taxperiod-mdms-config" id="taxperiod-mdms-config"></a>

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

### ID Gen Config for BPA Numbers <a href="#id-gen-config-for-bpa-numbers" id="id-gen-config-for-bpa-numbers"></a>

[idFormats.json](https://github.com/egovernments/egov-mdms-data/blob/master/data/pb/common-masters/IdFormat.json)

BPA Application Number format Config

```
{
      "idname":"egov.idgen.bpa.applicationNum",
      "format":"PB-BP-[cy:yyyy-MM-dd]-[SEQ_EG_BP_APN]"
    },
```

BPA Permit Number format Config

```
{
      "idname":"egov.idgen.bpa.applicationNum",
      "format":"PB-BP-[cy:yyyy-MM-dd]-[SEQ_EG_BP_PN]"
    },
```

BPA Receipt Number format config

```
 {
      "format": "BPA/[CITY.CODE]/[fy:yyyy-yy]/[SEQ_EGOV_COMMON]",
      "idname": "bpa.nc_app_fee.receipt.id"
    },
    {
      "format": "BPA/[CITY.CODE]/[fy:yyyy-yy]/[SEQ_EGOV_COMMON]",
      "idname": "bpa.nc_san_fee.receipt.id"
    },
```

BPA OC Receipt Number format config

```
  {
      "format": "BPA/OC/[CITY.CODE]/[fy:yyyy-yy]/[SEQ_EGOV_COMMON]",
      "idname": "bpa.nc_oc_app_fee.receipt.id"
    },
    {
      "format": "BPA/OC/[CITY.CODE]/[fy:yyyy-yy]/[SEQ_EGOV_COMMON]",
      "idname": "bpa.nc_oc_san_fee.receipt.id"
    },
```

### _**Persister configuration**_ <a href="#persister-configuration" id="persister-configuration"></a>

[BPA Persister YAML](https://github.com/egovernments/configs/blob/master/egov-persister/bpa-persist.yml)

### Indexer Configuration <a href="#indexer-configuration" id="indexer-configuration"></a>

[BPA Indexer YAML](https://github.com/egovernments/configs/blob/master/egov-indexer/egov-bpa-indexer.yml)

### Locality Search Configuration <a href="#locality-search-configuration" id="locality-search-configuration"></a>

Setup the locality Search query in the [localitySearcher.yml](https://github.com/egovernments/configs/blob/master/egov-searcher/localitySearcher.yml) as **a** new entry. Add RoleAction Test and Role Action for the URL **`“`**`/egov-searcher/locality/bpa-services/_get`**`“`**

```
  - name: bpa-services
    query:
      baseQuery: |
        Select row_to_json(result) from
        (
          select applicationNo as referenceNumber,locality from eg_bpa_buildingplan bpa
          INNER JOIN eg_land_Address ad ON ad.landInfoId = bpa.landid
        ) result  $where
      groupBy:
      orderBy:
    searchParams:
      condition: AND
      params:
      - name: result.referenceNumber
        isMandatory: true
        jsonPath: $.searchCriteria.referenceNumber
        operator: 

    output:
      jsonFormat: {"ResponseInfo": {}}
      outJsonPath: $.Localities
      responseInfoPath: $.ResponseInfo
```

### Database Schema <a href="#database-schema" id="database-schema"></a>

![](<../../../../.gitbook/assets/image (106).png>)

## Postman Links <a href="#postman-links" id="postman-links"></a>

[Postman Collection](https://www.getpostman.com/collections/667f52a25918f7f5ba25)

## Workflow Configuration <a href="#workflow-configuration" id="workflow-configuration"></a>

[BPA](https://github.com/egovernments/municipal-services/blob/master/bpa-services/src/main/resources/workflow-config.json) - Building Plan Approval Apply High/Medium Risk

[BPA Low](https://github.com/egovernments/municipal-services/blob/master/bpa-services/src/main/resources/Lowrisk\_Workflow.json) – Building Plan Approval Apply Low Risk

[BPA OC](https://github.com/egovernments/municipal-services/blob/master/bpa-services/src/main/resources/OC\_WorkflowConfig.json) - Building Plan Approval Occupancy Certificate Apply

**BPA and BPA OC Workflow Stages**

BPA workflow configuration is for Building Plan Approval Apply High and Medium Risk Types.

BPA OC workflow configuration is for Building Plan Approval Occupancy Certificate irrespective of RiskTypes

Both the workflow flows as depicted below.

![](<../../../../.gitbook/assets/image (107).png>)

In the above Flow Chart

* Rectangle Indicates the Workflow State
* Line connecting two states indicates the action
  * Action name is in black colour text
  * User Role who can take action is in Blue colour Text

**Specific Configurations and How To’s**

* System allows configuring the Documents that can be visible, allowed to upload and Mandatory to move from the current state in **DocumentTypeMapping** **MDMS** as described in MDMS Details Table DocumentTypeMapping Row
* **Application Creation Sage**
  * Process
    * DCR system is integrated to get the applicationType, serviceType and riskType based on the EDCR Number populated by the architect.
    * DCR system is integrated to validate the status of the EDCRNumber populated
    * New BPA or BPAOC application cannot be created if there is existing **un ended**( application status other than approved or rejected is considered as unended) application with the same EDCR
  * How To add new Document
    * Should add new documentType group in **DocumentTypeMapping** MDMS with the applicable applicationType, serviceType, riskType, wfState (refer existing sample for understanding)
    * Can configure allow, required as well as the order for each documentType
    * Make sure the new documentType added exists in documentType of [common-masters](https://github.com/egovernments/egov-mdms-data/blob/master/data/pb/common-masters/DocumentType.json)
* **Initiated Stage**
  * Process
    * NOC’s from the **NocTypeMapping** MDMS matching to the application data will get created
  * How To add new NocType
    * Should add new NOCType in **NocTypeMapping** MDMS
    * New NocType should add in noc-services application as well
* **Citizen Approval Pending Stage**
  * Process
    * According to the example in the **NocTypeMapping** Data in the **MDMS Details** Table, Once BPA or BPA OC reaches this Staus all the Applicable Noc’s workflow would be initiated.
  * How to change NOC workflow initiation step
    * Should change the nocTriggerState in **NocTypeMapping** to the desired application status.
* **InProgress Stage**
  * Process
    * Application fee Demand gets generated by the bpa-calculator
    * Notification to the Stakeholder and owner will be sent regarding the fee payment
  * How To change the Fee Amount
    * Will be discussed in bpa-calculator service
* **Document Verification Pending Stage**
  * Process
    * Nothing Specific
  * How To
    * NA
* **FieldInspection Pending Stage**
  * Process
    * At this stage, FieldInspector should answer the checklist questions and attached the documents which will be configured in **checklist** MDMS, as described in MDMS Details Table CheckList Row
    * Field Inspector can create multiple FieldInspection Reports
  * How to add new questions and documents
    * Should add/modify the questions for the desired combination of applicationType, serviceType, risktype
    * with the localization code for question text
    * specify the fieldType ( ass of now only YES/NO/NA only supported )
    * Should add/modify documents for the desired combination of applicationType, serviceType, risktype
* **Noc Verification Pending State**
  * Process
    * NOC verifier can upload the Documents to the NOC application’s if available.
    * Offline Noc’s would get auto-approved while NOC verifier is forwarding the BPA or BPAOC application from the current state
    * BPA or BPAOC application cannot be forwarded if any NOC is not in matching the status configured for validate.required.nocs.statuses in application.properties
  * How to change the NOC application status to be verified to move forward
    * should update the validate.required.nocs.statuses property in value in application.properties with the list of status to be considered to move forward
* **Approval Pending Stage**
  * Process
    * Approver can select the predefined conditions for approval updated in **CheckList** MDMS, as described in MDMS Details Table checkList Row
    * Approver can add new conditions as well for approval
    * Sanction fee Demand gets generated by the bpa-calculator
    * Notification to the Stakeholder and owner will be sent regarding the fee payment
  * How to add/remove/modify conditions
    * Should add/modify the conditions array for the desired combination of applicationType, serviceType, riskType
* **Approved Stage**
  * Process
    * System generates PermitOrder for the application
    * System Stamps the validate date for the permit Order by adding the no of months configured for the property egov.bpa.validity.date.in.months in application.properties
  * How to change the validity period of the permit order which will generate from now
    * Change the value of the property egov.bpa.validity.date.in.months in application.properties file to the desired no of months
  * How to change Permit Order
    * Can be changed by changing the data and format configs of the permit order, please refer to PDFs section of Permit Order
* **Rejected Stage**
  * Process
    * NA

**BPA LOW Workflow**

BPA with risk Type low has a separate workflow, which is almost the same as the BPA workflow as depicted below.

![](<../../../../.gitbook/assets/image (108).png>)

In the above Flow Chart

* Rectangle Indicates the Workflow State
* Line connecting two states indicates the action
  * Action name is in black colour text
  * User Role who can take action is in Blue colour Text

**Specific Configurations and How To’s which are not common to BPA Workflow**

* **InProgress Stage**
  * Process
    * Application and Sanction Fee together gets calculated and Demand gets generated by the bpa-calculator
    * Notification to the Stakeholder and owner will be sent regarding the fee payment
  * How To change the Fee Amount
    * Will be discussed in bpa-calculator service
* **Document Verification Pending Stage**
  * Process
    * System generates PermitOrder for the application
    * System Stamps the validate date for the permit Order by adding the no of months configured for the property egov.bpa.validity.date.in.months in application.properties
  * How to change the validity period of the permit order which will generate from now
    * Change the value of the property egov.bpa.validity.date.in.months in application.properties file to the desired no of months
* **Approved Stage**
  * Process
    * NA
* **Revocated Stage**
  * Process
    * System generates Revocation letter
  * How to change Revocation Letter format
    * Can be changed by changing the data and format configs of the revocation letter, please refer PDF’s section of Revocation letter

## Validations included <a href="#validations-included" id="validations-included"></a>

* On Workflow action of Every Stage, System verifies the Documents Configured for the given stage of the workflow from the **DocumentTypeMapping** MDMS and validates the required Documents attached to move forward
* DropDown values to be validated against the MDMS values, Value in those fields should be one of the MDMS value.

## Notifications <a href="#notifications" id="notifications"></a>

Notifications Message codes for SMS and User Events are prepared as follows

ApplicationType\_ServiceType\_WorkflowAction\_ApplicationStatus.

Example BPA Apply Application (i.e applicationType is **BUILDING\_PLAN\_SCRUTINY**) with ServiceType **NEW\_CONSTRUCTION** and the current application status is **DOCUMENT\_VERIFICATION\_PENDING** and workflow Action of the request is **FORWARD** then the localized message for this notification will be looked for the code: **BUILDING\_PLAN\_SCRUTINY**\_**NEW\_CONSTRUCTION**\_**FORWARD**\_**DOCUMENT\_VERIFICATION\_PENDING**

The message text for the above code is sent through SMS and Notification filling in the owner, serviceType, application Number and other values.

## PDFS used <a href="#pdfs-used" id="pdfs-used"></a>

BPA supports below PDF’s

|                       |                                                                                                   |                                                                                                                                                                                                                                                                                    |
| --------------------- | ------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **PDF Name**          | **Description**                                                                                   | **Config’s**                                                                                                                                                                                                                                                                       |
| BPA Permit Order      | PDF Generated for the Permit Order on approval of the BPA HIGH and MEDIUM RISK Applications       | <p><a href="https://github.com/egovernments/configs/blob/master/pdf-service/data-config/buildingpermit.json">Data Config</a></p><p><a href="https://github.com/egovernments/configs/blob/master/pdf-service/format-config/buildingpermit.json">Format Config</a></p>               |
| BPA LOW Permit Order  | PDF Generated for the Permit Order on approval of the BPA LOW RISK Applications                   | <p><a href="https://github.com/egovernments/configs/blob/master/pdf-service/data-config/buildingpermit-low.json">Data Config</a></p><p><a href="https://github.com/egovernments/configs/blob/master/pdf-service/format-config/buildingpermit-low.json">Format Config</a></p>       |
| Revocation Letter     | PDF of the Revocation Letter Generated when the LOW RISK BPA Application is Rejected              | <p><a href="https://github.com/egovernments/configs/blob/master/pdf-service/data-config/bpa-revocation.json">Data Config</a></p><p><a href="https://github.com/egovernments/configs/blob/master/pdf-service/format-config/bpa-revocation.json">Format Config</a></p>               |
| Occupancy Certificate | PDF Germinated for the Occupancy Certificate on Approval of the Occupancy Certificate Application | <p><a href="https://github.com/egovernments/configs/blob/master/pdf-service/data-config/occupancy-certificate.json">Data Config</a></p><p><a href="https://github.com/egovernments/configs/blob/master/pdf-service/format-config/occupancy-certificate.json">Format Config</a></p> |

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation ](https://egov.org.in)is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).
