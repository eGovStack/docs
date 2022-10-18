# Bill Amendment Service Configuration

## **Overview**

The consumer sometimes needs additional amounts (Amendments) added to their bill due to reasons from outside of the system. The addition of amounts happens with respect to the consumer code of the entity in the product(PT, WS, etc..,), any unpaid demand in the system is a candidate for amendments.

## **Pre-requisites**

* Prior knowledge of billing-service in the DIGIT framework.

## **Key Functionalities**

Amendment mainly works with two types of functionality as follows:

* Amendment
* Demand

Bill Amendment provides a separate flow that triggers the workflow for validating the process of adding additional amounts to existing demands. This validation was earlier available only to the respective modules. An amendment is allowed only when there is a need to add or reduce the amount from the existing bill belonging to an entity. The reasons for such cases could be:

1. Court case settlement
2. One time waiver
3. Write-offs
4. DCB correction (old demands in paid status)
5. Property tax remission

**Criteria:**

Below are certain prerequisites to creating an amendment,

1. presence of demand in the billing system
2. any one of the reasons listed above
3. valid document proof for the reason
4. there is no other amendment already in the workflow

**Procedure:**

The process of adding an amendment in specific scenarios is given below.

There are two scenarios on how an amendment is completed based on the paid status of the existing demands in the system.

_**1. when demand is unpaid/partially paid**_

1. Create a demand (Or an existing demand can be used) with demand detail → DD1.
2. Do not pay the bill or make a partial payment.
3. Create an amendment for the same consumer code (with demand detail → DD2).
4. Approve the amendment - the response should return an amendment with the status CONSUMED.
5. Search the demand or fetch the bill for the consumer code. The demand/bill should contain demand details of the demand and amendment together with DD1 and DD2 in the same demand/bill.

_**2. when demand is completely paid**_

1. Create demand and make complete payment or choose a consumer code which is fully paid.
2. Create amendment (with demand detail → DD1).
3. Approve amendment - the response should be APPROVED.
4. Create new demand for the consumer code (with demand detail → DD3). The demand response should contain two demand details DD1 and DD2 saved to the demand.
5. The amendment search returns CONSUMED status after the demand is created.

IMPACT: Does not impact any other functionality other than adding demand details to demands on APPROVAL.

IMPACTED BY: Existence of demands in the system.

## **Configuration Details**

[Billing Service | Configuration-Details:](./#configuration-details) ​Refer to billing-service config for MDMS data. The amendment makes use of the same data set.

**WORKFLOW CONFIG:**

```
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
      "businessService": "BS.AMENDMENT",
      "business": "BS",
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
          "docUploadRequired": true,
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
          "applicationStatus": "ACTIVE",
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

## Integration **Details**

### Integration Scope

Amendment integration helps organizations add additional value to the demand without any change in the system.

### Integration Benefits

* Easy to create and simple process of updating demands
* Helps ease changes into the system which are not part of normal functionality - Amendment of bills in case of legal requirements.

### Steps to Integration

This is integrated into the billing system by default.

1. The amendment facility can be used in case of a legal issue to add values to existing demands using /amendment/\_create. The parameter /amendment/\_update is used to cancel the created updates or update configured workflows.

### Interaction Diagram <a href="#interaction-diagram" id="interaction-diagram"></a>

{yet to be added}

## **Doc Links**

**API Definition**

[API SPEC FOR BILL-AMENDMENT](https://raw.githubusercontent.com/egovernments/business-services/master/Docs/billingservice/BillAmendment/v1.0.yml)

**API List**

| Description                   | Link                                                                                                                       |
| ----------------------------- | -------------------------------------------------------------------------------------------------------------------------- |
| /amendment/\_create, \_update | [https://www.getpostman.com/collections/b195d3b1d354c767b6bd](https://www.getpostman.com/collections/b195d3b1d354c767b6bd) |

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)_​_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in/) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
