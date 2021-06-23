---
description: Ownership Transfer Technical documentation
---

# Property Mutation & Mutation Calculator

## **Overview**

The mutation service provides a facility to change ownership of a property in relation to sales, inheritance of property. it helps by providing a workflow on config and allows the municipality to collect payment with ease on approval of the process. The mutation flows ad APIs exist within the property-services code base and makes use of all the mentioned external services and configured values, in addition to those the rest can be used to control mutation flow.

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

Enables the user to create a mutation and transfer the ownership to the new owner.

## **Configuration Details**

**Workflow config:**

| **name** | **value** | **description** |
| :--- | :--- | :--- |
| is.mutation.workflow.enabled | true/false | enables/disbales the workflow |
| [mutation.workflow.name](http://mutation.workflow.name/) | PT.MUTATION | workfow config name |

In Addition to property information and the extra owner information being added, some other information is required for workflow

The Creation Reason in the property should be sent as **MUTATION** for the request to be considered as a mutation request.

Along with the workflow name for mutation, a few extra details have to be provided in the additional details field of the property. Also either a new owner has to be added or an existing one has to be set to inactive for a valid mutation request.

```text
    "workflow": {
        "tenantId": "pb.amritsar",
        "businessService": "PT.MUTATION",
        "action": "OPEN",
        "moduleName": "PT"
    }, 

    "additionalDetails": {
        "documentDate": 1580722677000,
        "marketValue" : 1000,
        "documentValue": "1897",
        "documentNumber": "Xar34",
        "reasonForTransfer": "Sale",
        "isPropertyUnderGovtPossession": true
        "govtAcquisitionDetails": ""
        "isMutationInCourt":true,
        "caseDetails": "",
    }
```

The business workflow config follows the structure given for property workflow with respective name changes.

Workflow sample config for Mutation.

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
      "authToken": "{{Auth_Token}}"
    },
   "BusinessServices": [
        {
            "tenantId": "pb",
            "businessService": "PT.MUTATION",
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
                            "action": "PAY",
                            "nextState": "PAID",
                            "roles": [
                                "CITIZEN",
                                "PT_CEMP"
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
                    "state": "PAID",
                    "applicationStatus": "INWORKFLOW",
                    "docUploadRequired": false,
                    "isStartState": false,
                    "isTerminateState": false,
                    "isStateUpdatable": false,
                    "actions": [
                        {
                            "tenantId": "pb",
                            "action": "APPROVE",
                            "nextState": "APPROVED",
                            "roles": [
                                "PT_APPROVER"
                            ]
                        }
                    ]
                },
                {
                    "tenantId": "pb",
                    "sla": null,
                    "state": "APPROVED",
                    "applicationStatus": "ACTIVE",
                    "docUploadRequired": false,
                    "isStartState": false,
                    "isTerminateState": true,
                    "isStateUpdatable": false,
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
                            "action": "REJECT",
                            "nextState": "REJECTED",
                            "roles": [
                                "CITIZEN",
                                "PT_CEMP"
                            ]
                        },
                        {
                            "tenantId": "pb",
                            "action": "REOPEN",
                            "nextState": "OPEN",
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

The property services will make a call to the mutation calculator at the required interval during the mutation flow.

## Integration Details

### Integration Scope

The mutation service belongs to the property service itself and provides the same ease of access for the functionality.

### Steps to Integration

* Pick a property id that is already created in the system.
* call the property/update API by changing the owner information or adding new owner information.
* workflow information must be added mandatorily before submitting the request.

## Mutation Calculator <a id="Mutation-calculator:"></a>

### **Calculation Logic** <a id="Calculation-Logic"></a>

The calculation logic for mutation fee depends on the usage type of property \(RESIDENTIAL, NON-RESIDENTIAL, etc \) and the current market value of the property.

| Usage type | Minimum Market value | Maximum Market Value | Rate Percentage | Fixed amount | Calculation Type |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Residential | 0 | X lacs | A% of CMV | INR G | FLAT |
| Non -Residential | 0 | X lacs | E% of CMV | INR Q | RATE |
| Residential | X+1 Lacs | Y Lacs | B% of CMV | INR H | FLAT |
| Non -Residential | X+1 Lacs | Y Lacs | B% of CMV | INR H | RATE |
| Residential | Y+1 Lacs | &gt;Y+1Lacs | D% of CMV | INR L | FLAT |
| Non -Residential | Y+1 Lacs | &gt;Y+1Lacs | C% of CMV | INR I | RATE |

If the current market value \(CMV\) of the property comes in between the minimum and maximum market value range of billing slab and the usage type of property match with the usage type for that billing slab then the mutation fees for that property is the amount mentioned in that particular billing slab.

Further, there are two calculation types which are FLAT and RATE which have to set by state/ULB for their billing slab for property mutation. If the calculation type is set as FLAT then mutation fee is the fixed amount mentioned in the billing slab which is used for the property.

If the calculation type is set as RATE the Mutation fee is X% of the current market value, where X is the percentage rate mentioned in the billing slab which is used for the property.

Other factors influencing calculation can be :

* Ownership type
* Property type
* Locality

### **Rebate and Penalty**

When the property is registered for mutation/transfer of ownership and all the document is submitted, then the mutation fees have to pay within a specified period of time of property mutation registration date. If a person fails to pay the amount of the fee before the deadline date, then some penalty charges have to pay. The penalty charge is Y% of the tax amount. The penalty percentage is set by the state/ULB. If a person pays the amount of the fees within the specified month of the property mutation registration date, then a certain amount is rebated from the tax amount. The rebate charge is Z% of the tax amount. The rebate percentage is set by state/ULB.

Note: For mutation fees calculation, document date value \(means the date at which property is registered for mutation\), market value of property, usage type value of the property is essential.

## **Reference Docs**

Please refer to the parent for external services:[ Property Services \| Doc-Links ](./)

| **Title** | **Link** |
| :--- | :--- |
| API contract for MT calculator | [mutation-calculator.yml](https://raw.githubusercontent.com/egovernments/municipal-services/master/docs/property-services/property-mutation-fees-calculator_API_Contract.yml) |
| API list to create Mutation Slabs  mutation/\_create, \_search, \_update | [API COLLECTION MT\_SLABS](https://www.getpostman.com/collections/02965abc6345b5e1a633) |
| API list for MT-Calculator  mutation/\_calculate | [POSTMAN API COLLECTION - MT-CALCULATE](https://www.getpostman.com/collections/e044d1f64feeafe82f70) |

> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)\_\_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_ ](https://egov.org.in/)_is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._

