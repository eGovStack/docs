# Assessment of Property

For **overview** Please refer to the parent file -[ Property Services](./)

## **Key Functionality**

The assessment set of services inside the property module is used for assessing the value of a property in a given time frame and collect taxes for the same. Assessment is a snapshot of Property for a given transaction on that Property. These APIs provide functionalities to create/update/search the assessments. An assessment cannot exist without property.

## **Configuration Details** <a id="Configuration-Details:"></a>

MDMS CONFIG:[https://github.com/egovernments/egov-mdms-data/tree/DEV/data/pb/PropertyTax](https://github.com/egovernments/egov-mdms-data/tree/DEV/data/pb/PropertyTax)To show a preview of this link, connect your Github account.![](https://github.githubassets.com/favicon.ico)GithubConnect

Configs

Assessment shares most of the configs with Property as mentioned above, only exclusive properties are mentioned in this section.

| **name** | **value** | **description** |
| :--- | :--- | :--- |
| assessment id format | PB-AS-\[cy:yyyy-MM-dd\]-\[SEQ\_EG\_PT\_ASSM\] |  |
| kafka create assessment topic | save-pt-assessment |  |
| kafka update assesmsent topic | update-pt-assessment |  |
| assessment.workflow.enabled | true/false | Workflow integration can be controlled by the following two properties |
| assessment.workflow.trigger.param | usageCategory,occupancyType,occupancyDate |  |

**PERSISTER CONFIG**: [https://raw.githubusercontent.com/egovernments/configs/master/egov-persister/assessment-persister.yml?token=AE4Z2KFWEQBDCUY6AZLGGIK6AM3QQ](https://raw.githubusercontent.com/egovernments/configs/master/egov-persister/assessment-persister.yml?token=AE4Z2KFWEQBDCUY6AZLGGIK6AM3QQ)\`\`

```text
serviceMaps:
  serviceName: property-services
  mappings:
  - version: 1.0
    description: Persists assessment details to eg_pt_asmt_assessment table
    fromTopic: save-pt-assessment
    isTransaction: true
    queryMaps:

    - query: INSERT INTO eg_pt_asmt_assessment(id, tenantid, assessmentnumber, financialyear, propertyid, status, source, channel, assessmentdate, additionaldetails, createdby, createdtime, lastmodifiedby, lastmodifiedtime) VALUES (?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?);
      basePath: Assessment
      jsonMaps:

      - jsonPath: $.Assessment.id

      - jsonPath: $.Assessment.tenantId

      - jsonPath: $.Assessment.assessmentNumber

      - jsonPath: $.Assessment.financialYear

      - jsonPath: $.Assessment.propertyId

      - jsonPath: $.Assessment.status

      - jsonPath: $.Assessment.source

      - jsonPath: $.Assessment.channel

      - jsonPath: $.Assessment.assessmentDate

      - jsonPath: $.Assessment.additionalDetails
        type: JSON
        dbType: JSONB

      - jsonPath: $.Assessment.auditDetails.createdBy

      - jsonPath: $.Assessment.auditDetails.createdTime

      - jsonPath: $.Assessment.auditDetails.lastModifiedBy

      - jsonPath: $.Assessment.auditDetails.lastModifiedTime



    - query: INSERT INTO eg_pt_asmt_unitusage (tenantid, id, assessmentid, unitid, usagecategory, occupancytype, occupancydate, active, createdby, createdtime, lastmodifiedby, lastmodifiedtime) VALUES (?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?);
      basePath: Assessment.unitUsageList.*
      jsonMaps:

      - jsonPath: $.Assessment.unitUsageList.*.tenantId

      - jsonPath: $.Assessment.unitUsageList.*.id

      - jsonPath: $.Assessment[?({id} in @.unitUsageList[*].id)].id

      - jsonPath: $.Assessment.unitUsageList.*.unitId

      - jsonPath: $.Assessment.unitUsageList.*.usageCategory

      - jsonPath: $.Assessment.unitUsageList.*.occupancyType

      - jsonPath: $.Assessment.unitUsageList.*.occupancyDate

      - jsonPath: $.Assessment.unitUsageList.*.active

      - jsonPath: $.Assessment.unitUsageList.*.auditDetails.createdBy

      - jsonPath: $.Assessment.unitUsageList.*.auditDetails.createdTime

      - jsonPath: $.Assessment.unitUsageList.*.auditDetails.lastModifiedBy

      - jsonPath: $.Assessment.unitUsageList.*.auditDetails.lastModifiedTime



    - query: INSERT INTO eg_pt_asmt_document (id, tenantid, entityid, documenttype, filestoreid, documentuid, status, createdby, lastmodifiedby, createdtime, lastmodifiedtime) VALUES (?, ?, ?, ?, ?, ?, ?, ?, ?, ?);
      basePath: $.Assessment.documents.*
      jsonMaps:

      - jsonPath: $.Assessment.documents.*.id

      - jsonPath: $.Assessment.tenantId

      - jsonPath: $.Assessment.id

      - jsonPath: $.Assessment.documents.*.documentType

      - jsonPath: $.Assessment.documents.*.fileStoreId

      - jsonPath: $.Assessment.documents.*.documentUid

      - jsonPath: $.Assessment.documents.*.status

      - jsonPath: $.Assessment.documents.*.auditDetails.createdBy

      - jsonPath: $.Assessment.documents.*.auditDetails.lastModifiedBy

      - jsonPath: $.Assessment.documents.*.auditDetails.createdTime

      - jsonPath: $.Assessment.documents.*.auditDetails.lastModifiedTime



  - version: 1.0
    description: Updates assessment details to eg_pt_asmt_assessment table
    fromTopic: update-pt-assessment
    isTransaction: true
    queryMaps:

    - query: INSERT INTO eg_pt_asmt_assessment_audit SELECT *, (SELECT extract(epoch from now())) FROM eg_pt_asmt_assessment WHERE id = ?;
      basePath: Assessment
      jsonMaps:

      - jsonPath: $.Assessment.id


    - query: INSERT INTO eg_pt_asmt_unitusage_audit SELECT *, (SELECT extract(epoch from now())) FROM eg_pt_asmt_unitusage WHERE id = ?;
      basePath: Assessment.unitUsageList.*
      jsonMaps:

      - jsonPath: $.Assessment.unitUsageList.*.id


    - query: UPDATE eg_pt_asmt_assessment SET financialyear = ?, status = ?, source = ?, assessmentDate = ?, additionaldetails = ?, lastmodifiedby = ?, lastmodifiedtime = ? WHERE id = ?;
      basePath: Assessment
      jsonMaps:

      - jsonPath: $.Assessment.financialYear

      - jsonPath: $.Assessment.status

      - jsonPath: $.Assessment.source

      - jsonPath: $.Assessment.assessmentDate

      - jsonPath: $.Assessment.additionalDetails
        type: JSON
        dbType: JSONB

      - jsonPath: $.Assessment.auditDetails.lastModifiedBy

      - jsonPath: $.Assessment.auditDetails.lastModifiedTime

      - jsonPath: $.Assessment.id




    - query: INSERT INTO eg_pt_asmt_unitusage (tenantid, id, assessmentId, unitid, usageCategory, occupancyType, occupancyDate, active, createdby, createdtime, lastmodifiedby, lastmodifiedtime) VALUES (?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?) ON CONFLICT (id) DO UPDATE SET usageCategory = ?, occupancyType = ?, occupancyDate = ?, active = ?, lastmodifiedby = ?, lastmodifiedtime = ?;
      basePath: Assessment.unitUsageList.*
      jsonMaps:

      - jsonPath: $.Assessment.unitUsageList.*.tenantId

      - jsonPath: $.Assessment.unitUsageList.*.id

      - jsonPath: $.Assessment[?({id} in @.unitUsageList[*].id)].id

      - jsonPath: $.Assessment.unitUsageList.*.unitId

      - jsonPath: $.Assessment.unitUsageList.*.usageCategory

      - jsonPath: $.Assessment.unitUsageList.*.occupancyType

      - jsonPath: $.Assessment.unitUsageList.*.occupancyDate

      - jsonPath: $.Assessment.unitUsageList.*.active

      - jsonPath: $.Assessment.unitUsageList.*.auditDetails.createdBy

      - jsonPath: $.Assessment.unitUsageList.*.auditDetails.createdTime

      - jsonPath: $.Assessment.unitUsageList.*.auditDetails.lastModifiedBy

      - jsonPath: $.Assessment.unitUsageList.*.auditDetails.lastModifiedTime

      - jsonPath: $.Assessment.unitUsageList.*.usageCategory

      - jsonPath: $.Assessment.unitUsageList.*.occupancyType

      - jsonPath: $.Assessment.unitUsageList.*.occupancyDate

      - jsonPath: $.Assessment.unitUsageList.*.active

      - jsonPath: $.Assessment.unitUsageList.*.auditDetails.lastModifiedBy

      - jsonPath: $.Assessment.unitUsageList.*.auditDetails.lastModifiedTime




    - query: INSERT INTO eg_pt_asmt_document (id, tenantid, entityid, documenttype, filestoreid, documentuid, status, createdby, lastmodifiedby, createdtime, lastmodifiedtime) VALUES (?, ?, ?, ?, ?, ?, ?, ?, ?, ?) ON CONFLICT (id) DO UPDATE documenttype = ?, documentuid = ?, status = ?, lastmodifiedby = ?, lastmodifiedtime = ?;
      basePath: $.Assessment.documents.*
      jsonMaps:

      - jsonPath: $.Assessment.documents.*.id

      - jsonPath: $.Assessment.tenantId

      - jsonPath: $.Assessment.id

      - jsonPath: $.Assessment.documents.*.documentType

      - jsonPath: $.Assessment.documents.*.fileStoreId

      - jsonPath: $.Assessment.documents.*.documentUid

      - jsonPath: $.Assessment.documents.*.status

      - jsonPath: $.Assessment.documents.*.auditDetails.createdBy

      - jsonPath: $.Assessment.documents.*.auditDetails.lastModifiedBy

      - jsonPath: $.Assessment.documents.*.auditDetails.createdTime

      - jsonPath: $.Assessment.documents.*.auditDetails.lastModifiedTime

      - jsonPath: $.Assessment.documents.*.documentType

      - jsonPath: $.Assessment.documents.*.documentUid

      - jsonPath: $.Assessment.documents.*.status

      - jsonPath: $.Assessment.documents.*.auditDetails.lastModifiedBy

      - jsonPath: $.Assessment.documents.*.auditDetails.lastModifiedTime
```

**Workflow Config**

The first property switches workflow on or off, while the second property provides a way to control which field change can trigger the workflow. A businessService needs to be created using the workflow [/egov-workflow-v2/egov-wf/businessservice/\_create](https://digit-discuss.atlassian.net/egov-workflow-v2/egov-wf/businessservice/_create) API.

Sample businessService create API body for Assessment workflow:

```text
{
  "RequestInfo": {
    "apiId": "Rainmaker",
    "action": "",
    "did": 1,
    "key": "",
    "msgId": "20170310130900|en_IN",
    "requesterId": "",
    "ts": 1513579888683,
    "ver": ".01",
    "authToken": "b39181b1-5c6b-484a-b825-6be2f62012b8"
  },
 "BusinessServices": [
    {
      "tenantId": "pb",
      "businessService": "ASMT",
      "business": "pt-services",
      "businessServiceSla": 172800000,
      "states": [
        {
          "sla": null,
          "state": null,
          "applicationStatus": null,
          "docUploadRequired": false,
          "isStartState": true,
          "isTerminateState": false,
          "isStateUpdatable": true,
          "actions": [
            {
              "action": "INITIATE",
              "nextState": "INITIATED",
              "roles": [
                "CITIZEN",
                "PT_CEMP"
              ]
            }
          ]
        },
        {
          "sla": null,
          "state": "INITIATED",
          "applicationStatus": "INITIATED",
          "docUploadRequired": false,
          "isStartState": true,
          "isTerminateState": false,
          "actions": [
            {
              "action": "APPLY",
              "nextState": "APPLIED",
              "roles": [
                "CITIZEN",
                "PT_CEMP"
              ]
            },
            {
              "action": "INITIATE",
              "nextState": "INITIATED",
              "roles": [
                "CITIZEN",
                "PT_CEMP"
              ]
            }
          ]
        },
        {
          "sla": null,
          "state": "APPLIED",
          "applicationStatus": "APPLIED",
          "docUploadRequired": false,
          "isStartState": false,
          "isTerminateState": false,
          "isStateUpdatable": true,
          "actions": [
            {
              "action": "FORWARD",
              "nextState": "FIELDINSPECTION",
              "roles": [
                "PT_DOC_VERIFIER"
              ]
            },
            {
              "action": "REJECT",
              "nextState": "REJECTED",
              "roles": [
                "PT_DOC_VERIFIER"
              ]
            },
            {
              "action" : "SENDBACKTOCITIZEN",
              "nextState" : "INITIATED",
              "roles":["PT_DOC_VERIFIER"]
            }
          ]
        },
        {
          "sla": null,
          "state": "REJECTED",
          "applicationStatus": "REJECTED",
          "isStateUpdatable": false,
          "docUploadRequired": false,
          "isStartState": false,
          "isTerminateState": true
        },
        {
          "sla": 86400000,
          "state": "FIELDINSPECTION",
          "applicationStatus": "FIELDINSPECTION",
          "docUploadRequired": false,
          "isStartState": false,
          "isStateUpdatable": true,
          "isTerminateState": false,
          "actions": [
            {
              "action": "FORWARD",
              "nextState": "PENDINGAPPROVAL",
              "roles": [
                "PT_FIELD_INSPECTOR"
              ]
            },
            {
              "action": "REJECT",
              "nextState": "REJECTED",
              "roles": [
                "PT_FIELD_INSPECTOR"
              ]
            },
            {
              "action": "SENDBACK",
              "nextState": "APPLIED",
              "roles": [
                "PT_FIELD_INSPECTOR"
              ]
            }
          ]
        },
        {
          "sla": 43200000,
          "state": "PENDINGAPPROVAL",
          "applicationStatus": "PENDINGAPPROVAL",
          "docUploadRequired": false,
          "isStartState": false,
          "isStateUpdatable": false,
          "isTerminateState": false,
          "actions": [
            {
              "action": "APPROVE",
              "nextState": "PENDINGPAYMENT",
              "roles": [
                "PT_APPROVER"
              ]
            },
            {
              "action": "REJECT",
              "nextState": "REJECTED",
              "roles": [
                "PT_APPROVER"
              ]
            },
            {
              "action": "SENDBACK",
              "nextState": "FIELDINSPECTION",
              "roles": [
                "PT_APPROVER"
              ]
            }
          ]
        },
        {
          "sla": 43200000,
          "state": "PENDINGPAYMENT",
          "applicationStatus": "PENDINGPAYMENT",
          "docUploadRequired": false,
          "isStartState": false,
          "isTerminateState": false,
          "isStateUpdatable": false,
          "actions": [
            {
              "action": "PAY",
              "nextState": "APPROVED",
              "roles": [
                "CITIZEN",
                "PT_CEMP",
                "SYSTEM_PAYMENT"
              ]
            },
            {
              "action": "ADHOC",
              "nextState": "PENDINGPAYMENT",
              "roles": [
                "PT_CEMP"
              ]
            }
          ]
        },
        {
          "sla": null,
          "state": "APPROVED",
          "applicationStatus": "APPROVED",
          "isStateUpdatable": false,
          "docUploadRequired": false,
          "isStartState": false,
          "isTerminateState": true
        }
      ]
    }
  ]
}
```

Other system-level configs are the same as PT-Registry as mentioned above.

**Notification Configs**

**Payment Notification**

```text
    {
      "code": "PT_NOTIFICATION_PAYMENT_FAIL",
      "message": "Dear Citizen, Your payment of Rs. <insert amount to pay> for Property Tax Unique ID <insert ID> has failed. Your assessment is pending. Please try again. Ignore this message if you have completed your payment. You can pay your Property Tax online here - <payLink>",
      "module": "rainmaker-pt",
      "locale": "en_IN"
    },
    {
      "code": "PT_NOTIFICATION_PAYMENT_OFFILE",
      "message": "Dear Citizen,  Your Property Tax payment of Rs. <amount>  has been accepted. Mode of Payment: <insert mode of payment> Pending Amount: <Enter pending amount>.",
      "module": "rainmaker-pt",
      "locale": "en_IN"
    },
    {
      "code": "PT_NOTIFICATION_PAYMENT_ONLINE",
      "message": "Dear Citizen, Your payment of Rs.< insert amount paid> with payment transaction id < insert payment transaction id from PG> has been made successfully. Assessment for Property Tax Unique ID <insert Property Tax Assessment ID>  was succesful. Property Tax due is Rs.<pt due>.",
      "module": "rainmaker-pt",
      "locale": "en_IN"
    },
    {
      "code": "PT_NOTIFICATION_PAYMENT_PARTIAL_OFFLINE",
      "message": "Dear Citizen,  Your Property Tax payment of Rs. <amount>  has been accepted. Mode of Payment: <insert mode of payment> Pending Amount: <Enter pending amount>. You can pay your Property Tax online here - <payLink>",
      "module": "rainmaker-pt",
      "locale": "en_IN"
    },
    {
      "code": "PT_NOTIFICATION_PAYMENT_PARTIAL_ONLINE",
      "message": "Dear Citizen, Your payment of Rs.< insert amount paid> with payment transaction id < insert payment transaction id from PG> has been made successfully. Assessment for Property Tax Unique ID <insert ID>  was succesful. Property Tax due is Rs.<pt due>. You can pay your Property Tax here - <payLink>",
      "module": "rainmaker-pt",
      "locale": "en_IN"
    }
```

### Assessment Notification <a id="Assessment-Notification:"></a>

```text
    {
      "code": "ASMT_APPLIED",
      "message": "Applied",
      "module": "rainmaker-pt",
      "locale": "en_IN"
    },
    {
      "code": "ASMT_APPROVED",
      "message": "Approved",
      "module": "rainmaker-pt",
      "locale": "en_IN"
    },
    {
      "code": "ASMT_CREATE",
      "message": "Dear {OWNER_NAME}, Your assessment with {ASSESSMENTNUMBER} for financial year {FINANCIALYEAR} and property id {PROPERTYID} is created.",
      "module": "rainmaker-pt",
      "locale": "en_IN"
    },
    {
      "code": "ASMT_UPDATE",
      "message": "Dear {OWNER_NAME}, Your assessment with {ASSESSMENTNUMBER} for financial year {FINANCIALYEAR} and property id {PROPERTYID} is reassessed.",
      "module": "rainmaker-pt",
      "locale": "en_IN"
    },
    {
      "code": "ASMT_MSG_APPLIED",
      "message": "Dear {OWNER_NAME}, Your assessment with {ASSESSMENTNUMBER} for financial year {FINANCIALYEAR} and property id {PROPERTYID} is updated to {STATUS}.",
      "module": "rainmaker-pt",
      "locale": "en_IN"
    },
    {
      "code": "ASMT_MSG_APPROVED",
      "message": "Dear {OWNER_NAME}, Your assessment with {ASSESSMENTNUMBER} for financial year {FINANCIALYEAR} and property id {PROPERTYID} is {STATUS}.",
      "module": "rainmaker-pt",
      "locale": "en_IN"
    }
```

For adding localization for any status append ASMT\_ prefix to the status and for adding a message for any status add ASMT\_MSG\_ before the status.

Assessment _\*\*_\(Property Calculator\) -

The calculator service Prepares and property tax and files the demand in the billing service for payment. It has the ‘estimate’ API to give the estimated property tax without persisting data and a calculated API to create demand for payments.

The calculator service[ PT Calculator](pt-calculator.md)

## Integration

### Integration Scope <a id="Integration-Scope"></a>

Assessment integration helps citizens to assess their property with ease and helps them verify their tax values by themselves which gives more control to the citizens and hep the municipality collect taxes with ease.

### Integration Benefits

* Easy to create and simple process of self-assessment to avoid the hassle.
* Integrated payment for multiple years enables by digit platform.

### Steps to Integration

1. Customer can create an assessment on a given property using the /assessment/\_create
2. Search the assessment and its workflow status by using /assessment/\_searchendpoint
3. /assessment/\_update endpoint to update the assessment and its workflow states as per need.

## **Reference Docs**

please refer to the property document[ Property Services \| Doc-Links](./)

**API LIST**

| **Title** | **Link** |
| :--- | :--- |
| /assessment/\_create | [https://www.getpostman.com/collections/d1a02a29203d110df289](https://www.getpostman.com/collections/d1a02a29203d110df289) |
| /assessment/\_update | [https://www.getpostman.com/collections/d1a02a29203d110df289](https://www.getpostman.com/collections/d1a02a29203d110df289) |
| /assessment/\_search | [https://www.getpostman.com/collections/d1a02a29203d110df289](https://www.getpostman.com/collections/d1a02a29203d110df289) |

> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)\_\_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_ ](https://egov.org.in/)_is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._

