---
description: Service configuration details
---

# Property Tax Service

### **Overview** <a id="Overview:"></a>

One of the major applications of the eGov stack which helps municipal and citizens to handle property tax payments and other related functions on the property such as assessments, mutation, and so on.

## **Pre-requisites**

* Prior Knowledge of Java/J2EE.
* Prior Knowledge of Spring Boot.
* Prior Knowledge of REST APIs and related concepts like path parameters, headers, JSON etc.
* Prior knowledge of Git
* Prior knowledge of the demand-based systems.
* Following services should be up and running:
  * user
  * MDMS
  * Persister
  * Location
  * Localization
  * Id-Gen
  * Billing-service
  * URL-shortener

## **Key Functionality**

The Property Service provides multiple functionalities starting from serving as a central repository where property information is registered for reference of citizens and other municipality-provided services such as water connection and sewerage management.  
An assessment can be done so as to calculate and pay tax on the property. The different services provided by the property services are

* Property Registry
* Assessment
* Mutation
* Bifurcation
* Consolidation

**Registry Explanation**

* The registry flow helps the citizen/Employee to create a property in the system with the minimal information required.
* Other workflows such as assessment or mutation can be triggered on the existing ACTIVE Property in the registry.
* The property can be created, updated, cancelled, searched, Followed by the process of Mutation and Assessment.
* The same entry in the registry can be referred by other modules for their business purposes\(Water charges\).

## **Configuration Details**

MDMS CONFIG:[ ![](https://github.githubassets.com/favicon.ico)https://github.com/egovernments/egov-mdms-data/tree/DEV/data/pb/PropertyTax - Connect to preview](https://github.com/egovernments/egov-mdms-data/tree/DEV/data/pb/PropertyTax)

**Persister File Config**

The persister File config for property services can be found in the Config repo of eGov Git, which needs to be added in the persister service - [property-services-registry.yml](https://github.com/egovernments/configs/blob/master/egov-persister/property-services-registry.yml)

**Workflow-configs**

Each flow in property has a workflow associated with it, which can be controlled by the following configs

The Boolean field which can enable/disable Workflow - same field controls the update and create the workflow

| **name** | **value** | **description** |
| :--- | :--- | :--- |
| **is.workflow.enabled** | true/false | enable disbale workflow |
| [**property.workflow.name**](http://property.workflow.name/) | **PT.CREATE** | the name should match the config name in the workflow businessservice JSON |
| [**property.legacy.entry.workflow.name**](http://property.legacy.entry.workflow.name/) | **PT.LEGACY** |  |
| [**property.update.workflow.name**](http://property.update.workflow.name/) | **PT.UPDATE** |  |

Workflow Config for property create if the source is from **WATER CONNECTION** module

For the creation of property from the water and sewerage module, as per the use case mentioned in this [ticket](https://digit-discuss.atlassian.net/browse/RAIN-1772), a different workflow config is used.  
For each use case, to identify which workflow to use can be identified from this [mdms file](https://github.com/egovernments/egov-mdms-data/blob/DEV/data/pb/PropertyTax/PTWorkflow.json).

```text
{
 "tenantId": "pb",
 "moduleName": "PropertyTax",
 "PTWorkflow":[
     {
         "businessService":"PT.CREATEWITHWNS",
         "initialAction":"OPEN",
         "inWorkflowStatusAllowed":false,
         "enable":false
     },
     {
      "businessService":"PT.CREATE",
      "initialAction":"open",
      "inWorkflowStatusAllowed":true,
      "enable":true
  }

 ]
}
```

**For use case 1** which says, The property which is creating from Water and sewerage module should have one step workflow.  
for this requirement in the above MDMS file businessService with PT.CREATEWITHWNS object must have enabled the field to set as true.  
Then for all the property creation from Water and Sewerage module would have one step workflow and property would be created with an ACTIVE state.

**Fields in the above MDMS file**

| **MDMS Fields** | **Description** |
| :--- | :--- |
| **businessService** | Name of workflow config |
| **initialAction** | Indicate the start\(initial\) action of the particular workflow mention in businessService. |
| **inWorkflowStatusAllowed** | This field indicate whether the property with application status as “**inWorkflow**” can be use with water and sewerage connection creation. If this field is true then for that particular use case, the property with “**inWorkflow**” status can be use with water and sewerage connection creation and vice versa |
| **enable** | If this filed is set as true, then the other fields associate with the particular object is use for property creation. |

{% hint style="info" %}
Note: The above objects indicate each use case mentioned in this [ticket](https://digit-discuss.atlassian.net/browse/RAIN-1772), so at a time only one object \(use case\) enable field must set as true
{% endhint %}

Sample workflow config for use case 1 where property creation is from water and sewerage module with one step workflow

```text
{
    "BusinessServices": [
      {
        "tenantId": "pb",
        "businessService": "PT.CREATEWITHWNS",
        "business": "PT",
        "businessServiceSla": null,
        "states": [
          {
            "sla": null,
            "state": null,
            "applicationStatus": "INWORKFLOW",
            "docUploadRequired": false,
            "isStartState": true,
            "isTerminateState": false,
            "isStateUpdatable": false,
            "actions": [
              {
                "action": "OPEN",
                "nextState": "INITIATED",
                "roles": [
                  "CITIZEN",
                  "WS_CEMP",
                  "SW_CEMP"
                ]
              }
            ]
          },
          {
            "sla": null,
            "state": "INITIATED",
            "applicationStatus": "INWORKFLOW",
            "docUploadRequired": false,
            "isStartState": true,
            "isTerminateState": false,
            "isStateUpdatable": true,
            "actions": [
              {
                "action": "SUBMIT",
                "nextState": "APPROVED",
                "roles": [
                  "EMPLOYEE",
                  "CITIZEN",
                  "SW_CEMP",
                  "WS_CEMP"
                ]
              },
              {
                "action": "BACK",
                "nextState": "INWORKFLOW",
                "roles": [
                  "EMPLOYEE",
                  "CITIZEN",
                  "SW_CEMP",
                  "WS_CEMP"
                ]
              }
            ]
          },
          {
            "sla": null,
            "state": "INWORKFLOW",
            "applicationStatus": "INWORKFLOW",
            "docUploadRequired": false,
            "isStartState": true,
            "isTerminateState": false,
            "isStateUpdatable": true,
            "actions": [
              {
                "action": "SUBMIT",
                "nextState": "APPROVED",
                "roles": [
                  "EMPLOYEE",
                  "CITIZEN",
                  "SW_CEMP",
                  "WS_CEMP"
                ]
              }
            ]
          },
          {
            "sla": null,
            "state": "APPROVED",
            "applicationStatus": "ACTIVE",
            "docUploadRequired": false,
            "isStartState": false,
            "isTerminateState": true,
            "isStateUpdatable": false,
            "actions": null
          }
        ]
      }
    ]
  }
```

Sample workflow config - \(The same PT.CREATE can be used for update workflow also since both involve the same functionality\)

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
    "businessService": "PT.CREATE",
    "business": "PT",
    "businessServiceSla": null,
    "states": [
        {
            "tenantId": "pb",
            "sla": null,
            "state": null,
            "applicationStatus": "INWORKFLOW",
            "docUploadRequired": false,
            "isStartState": true,
            "isTerminateState": false,
            "actions": [
                {
                    "tenantId": "pb",
                    "action": "OPEN",
                    "nextState": "OPEN",
                    "roles": [
                        "CITIZEN",
                        "EMPLOYEE"
                    ]
                }
            ]
        },
        {
            "tenantId": "pb",
            "sla": null,
            "state": "OPEN",
            "applicationStatus": "INWORKFLOW",
            "docUploadRequired": false,
            "isStartState": true,
            "isTerminateState": false,
            "actions": [
                {
                    "tenantId": "pb",
                    "action": "VERIFY",
                    "nextState": "DOCVERIFIED",
                    "roles": [
                        "PT_DOC_VERIFIER"
                    ]
                },
                {
                  "tenantId": "pb",
                  "action": "REJECT",
                  "nextState": "REJECTED",
                  "roles": [
                      "PT_DOC_VERIFIER"
                  ]
              },
              {
                "tenantId": "pb",
                "action": "SENDBACKTOCITIZEN",
                "nextState": "CORRECTIONPENDING",
                "roles": [
                    "PT_DOC_VERIFIER"
                ]
            }
            ]
        },
        {
            "tenantId": "pb",
            "sla": null,
            "state": "DOCVERIFIED",
            "applicationStatus": "INWORKFLOW",
            "docUploadRequired": false,
            "isStartState": false,
            "isTerminateState": false,
            "actions": [
                {
                    "tenantId": "pb",
                    "action": "FORWARD",
                    "nextState": "FIELDVERIFIED",
                    "roles": [
                        "PT_FIELD_INSPECTOR"
                    ]
                }
            ]
        },
        {
            "tenantId": "pb",
            "sla": null,
            "state": "FIELDVERIFIED",
            "applicationStatus": "INWORKFLOW",
            "docUploadRequired": false,
            "isStartState": false,
            "isTerminateState": false,
            "actions": [
                {
                    "tenantId": "pb",
                    "action": "APPROVE",
                    "nextState": "APPROVED",
                    "roles": [
                        "PT_APPROVER"
                    ]
                },
                {
                    "tenantId": "pb",
                    "action": "REJECT",
                    "nextState": "REJECTED",
                    "roles": [
                        "PT_APPROVER"
                    ]
                }
            ]
        },
        {
            "tenantId": "pb",
            "sla": null,
            "state": "REJECTED",
            "applicationStatus": "INACTIVE",
            "docUploadRequired": false,
            "isStartState": false,
            "isTerminateState": true,
            "actions": null
        },
        {
            "tenantId": "pb",
            "sla": null,
            "state": "APPROVED",
            "applicationStatus": "ACTIVE",
            "docUploadRequired": false,
            "isStartState": false,
            "isTerminateState": true,
            "actions": null
        },
        {
          "tenantId": "pb",
          "sla": null,
          "state": "CORRECTIONPENDING",
          "applicationStatus": "INWORKFLOW",
          "docUploadRequired": false,
          "isStartState": false,
          "isTerminateState": false,
          "isStateUpdatable": true,
          "actions": [
              {
                  "tenantId": "pb",
                  "action": "REOPEN",
                  "nextState": "OPEN",
                  "roles": [
                    "CITIZEN",
                    "PT_CEMP"
                  ]
              },
              {
                  "tenantId": "pb",
                  "action": "REJECT",
                  "nextState": "REJECTED",
                  "roles": [
                    "CITIZEN",
                    "PT_CEMP"
                  ]
              }
          ]
      }
    ]
}
  ]
}
```

**PT.LEGACY workflow config**

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
      "authToken": "{{authToken_amritsar}}"
    },
    "BusinessServices": [
      {
        "tenantId": "pb",
        "businessService": "PT.LEGACY",
        "business": "PT",
        "businessServiceSla": null,
        "states": [
          {
            "tenantId": "pb",
            "sla": null,
            "state": null,
            "applicationStatus": "INWORKFLOW",
            "docUploadRequired": false,
            "isStartState": true,
            "isTerminateState": false,
            "actions": [
              {
                "tenantId": "pb",
                "action": "OPEN",
                "nextState": "APPROVALPENDING",
                "roles": [
                  "CITIZEN",
                  "EMPLOYEE"
                ]
              }
            ]
          },
          {
            "tenantId": "pb",
            "sla": null,
            "state": "APPROVALPENDING",
            "applicationStatus": "INWORKFLOW",
            "docUploadRequired": false,
            "isStartState": true,
            "isTerminateState": false,
            "actions": [
              {
                "tenantId": "pb",
                "action": "APPROVE",
                "nextState": "APPROVED",
                "roles": [
                  "EMPLOYEE"
                ]
              },
              {
                "tenantId": "pb",
                "action": "REJECT",
                "nextState": "REJECTED",
                "roles": [
                  "EMPLOYEE"
                ]
              }
            ]
          },
          {
            "tenantId": "pb",
            "sla": null,
            "state": "REJECTED",
            "applicationStatus": "INACTIVE",
            "docUploadRequired": false,
            "isStartState": false,
            "isTerminateState": true,
            "actions": null
          },
          {
            "tenantId": "pb",
            "sla": null,
            "state": "APPROVED",
            "applicationStatus": "INACTIVE",
            "docUploadRequired": false,
            "isStartState": false,
            "isTerminateState": true,
            "actions": null
          }
        ]
      }
    ]
  }
```

Notifications :

To enable or disable notifcation  
**notif.sms.enabled**=true

\#notif urls - makes use of the UI app host in notification service  
**egov.notif.commonpay =** citizen/egov-common/pay?consumerCode={CONSUMERCODE}&tenantId={TENANTID}  
**egov.notif.view.property** = citizen/property-tax/my-properties/property/{PROPERTYID}/{TENANTID}  
**egov.notif.view.mutation** = citizen/pt-mutation/search-preview?applicationNumber={APPID}&tenantId={TENANTID}

The Current localization messages for notification

```text
[
        {
            "code": "PT_NOTIF_WF_STATE_LOCALE_OPEN",
            "message": "Open",
            "module": "rainmaker-pt",
            "locale": "en_IN"
        },
        {
            "code": "PT_NOTIF_WF_STATE_LOCALE_DOCVERIFIED",
            "message": "Document Verified",
            "module": "rainmaker-pt",
            "locale": "en_IN"
        },
        {
            "code": "PT_NOTIF_WF_STATE_LOCALE_FIELDVERIFIED",
            "message": "Field verified",
            "module": "rainmaker-pt",
            "locale": "en_IN"
        },
        {
            "code": "PT_NOTIF_WF_STATE_LOCALE_APPROVED",
            "message": "Approved",
            "module": "rainmaker-pt",
            "locale": "en_IN"
        },
        {
            "code": "PT_NOTIF_WF_STATE_LOCALE_REJECTED",
            "message": "Rejected",
            "module": "rainmaker-pt",
            "locale": "en_IN"
        },
        {
            "code": "PT_NOTIF_WF_STATE_LOCALE_PAID",
            "message": "Paid",
            "module": "rainmaker-pt",
            "locale": "en_IN"
        },
        {
            "code": "PT_NOTIF_WF_MT_OPEN",
            "message": "Dear {OWNER_NAME}, Your application to edit ownership details of property ID {PROPERTYID} has been submitted successfully. Your application no. for future reference is {APPID}. You can track your application on the link given below - {MTURL} Thank you",
            "module": "rainmaker-pt",
            "locale": "en_IN"
        },
        {
            "code": "PT_NOTIF_WF_MT_STATE_CHANGE",
            "message": "Dear {OWNER_NAME}, Status for your application no. {APPID} for property {PROPERTYID} to edit ownership has been changed to {STATUS}. You can track your application on the link given below - {MTURL} Thank you",
            "module": "rainmaker-pt",
            "locale": "en_IN"
        },
        {
            "code": "PT_NOTIF_WF_MT_PAYMENT_PENDING",
            "message": "Dear {OWNER_NAME}, Payment is pending for your application no. {APPID} for property ID {PROPERTYID} to edit ownership. You can pay your mutation fee on the below link - {PAYLINK} or visit your ULB to pay your dues. Thank you",
            "module": "rainmaker-pt",
            "locale": "en_IN"
        },
        {
            "code": "PT_NOTIF_WF_MT_PAID",
            "message": "Dear {OWNER_NAME}, You’ve successfully paid mutation fee - INR {AMOUNT} for application no. {APPID} for property ID {PROPERTYID}. You can download your receipt on the below link - {MTURL} Thank you ",
            "module": "rainmaker-pt",
            "locale": "en_IN"
        },
        {
            "code": "PT_NOTIF_WF_MT_APPROVED",
            "message": "Dear {OWNER_NAME}, Your property ownership has been changed as per the application no. {APPID} for property {PROPERTYID}. You can download your mutation certificate on the below link - {MTURL} Thank you",
            "module": "rainmaker-pt",
            "locale": "en_IN"
        },
        {
            "code": "PT_NOTIF_WF_MT_NONE",
            "message": "Dear {OWNER_NAME}, Your property with property-id {PROPERTYID} has been mutated. You can view your property on the link given below - {MTURL} Thank you",
            "module": "rainmaker-pt",
            "locale": "en_IN"
        },
        {
            "code": "PT_NOTIF_WF_OPEN",
            "message": "Dear {OWNER_NAME}, Your application to {updated/created} property with Id {PROPERTYID} has been submitted successfully. Your application no. for future reference is {APPID}. You can track your application on the link given below - {PTURL} Thank you",
            "module": "rainmaker-pt",
            "locale": "en_IN"
        },
        {
            "code": "PT_NOTIF_WF_STATUS_CHANGE",
            "message": "Dear {OWNER_NAME}, Status for your application no. {APPID} for property {PROPERTYID} to {updated/created} property has been changed to {STATUS}. You can track your application on the link given below - {PTURL} Thank you",
            "module": "rainmaker-pt",
            "locale": "en_IN"
        },
        {
            "code": "PT_NOTIF_WF_APPROVED",
            "message": "Dear {OWNER_NAME}, Your property has been {updated/created} as per the application no. {APPID} for property {PROPERTYID}. You can view your property on the link given below - {PTURL} Thank you",
            "module": "rainmaker-pt",
            "locale": "en_IN"
        },
        {
            "code": "PT_NOTIF_WF_UPDATE_NONE",
            "message": "Dear {OWNER_NAME}, Your property with property-id {PROPERTYID} has been {updated/created}. You can view your property on the link given below - {PTURL} Thank you",
            "module": "rainmaker-pt",
            "locale": "en_IN"
        }
    ]
```

Configs in App.props

| **name** | **value** |
| :--- | :--- |
| egov.idgen.ack.format | PB-AC-\[cy:yyyy-MM-dd\]-\[SEQ\_EG\_PT\_ACK\] |
| egov.idgen.mutation.format | PB-MT-\[CITY\]-\[SEQ\_EG\_PT\_MUTATION\] |
| egov.idgen.assm.format | PB-AS-\[cy:yyyy-MM-dd\]-\[SEQ\_EG\_PT\_ASSM\] |
| egov.idgen.ptid.format | PB-PT-\[cy:yyyy-MM-dd\]-\[SEQ\_EG\_PT\_PTID\] |
| citizen.allowed.search.params | accountId,ids,propertyDetailids,mobileNumber,oldpropertyids |
| employee.allowed.search.params | accountId,ids,propertyDetailids,mobileNumber,oldpropertyids |

## Integration

### Integration Scope <a id="Integration-Scope"></a>

Property service can be integrated with any organization or system that wants to maintain a record of the property and collect taxes with ease.

### Integration Benefits

* Easy to create and simple process of self-assessment to avoid the hassle.
* Helps maintain property data which can be used in the integration of other essential services like asset management, water connection and so on.
* provides additional functionalities like mutation, assessment of properties.

### Steps to Integration

1. Customer can create a property using the /property/\_create
2. Search the property using /property/\_searchendpoint
3. /property/\_update endpoint to update the property demand as per need.
4. Mutation can be carried out with the help of /property/\_update itself, no extra API is needed.

## **Reference Docs**

**Doc Links**

| **Title** | **Link** |
| :--- | :--- |
| USER Service | [ User Service](https://digit-discuss.atlassian.net/wiki/spaces/DD/pages/669450371/User+Service) |
| url-shortening | [URL Shortening service](https://digit-discuss.atlassian.net/wiki/spaces/DD/pages/896892936/URL+Shortening+service) |
| MDMS | [MDMS \(Master Data Management Service\)](https://digit-discuss.atlassian.net/wiki/spaces/DD/pages/723189807) |
| Billing-service | [ Billing Service](https://digit-discuss.atlassian.net/wiki/spaces/DD/pages/1620672528/Billing+Service) |
| Location | [ Location Service](https://digit-discuss.atlassian.net/wiki/spaces/DD/pages/664338482/Location+Service) |
| Workflow | [ Workflow Service](https://digit-discuss.atlassian.net/wiki/spaces/DD/pages/664174657/Workflow+Service) |
| Persister | _\*\*_ |
| Localization |  |
| Id-Gen service |  |

API LIST:

| **Title** | **Link** |
| :--- | :--- |
| /Property/\_create | [https://www.getpostman.com/collections/02d01e7b46c79c140863](https://www.getpostman.com/collections/02d01e7b46c79c140863) |
| /Property/\_update | [https://www.getpostman.com/collections/02d01e7b46c79c140863](https://www.getpostman.com/collections/02d01e7b46c79c140863) |
| /property/\_search | [https://www.getpostman.com/collections/02d01e7b46c79c140863](https://www.getpostman.com/collections/02d01e7b46c79c140863) |

> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)\_\_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_ ](https://egov.org.in/)_is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._

