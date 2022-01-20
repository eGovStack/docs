---
description: Configure billing services to allow bill amendments
---

# Bill Amendment

### Overview

The consumer sometimes needs additional amounts (Amendments) added to their bill due to reasons external to the system. The addition of amounts happen with respect to the consumer-code of the entity in the product(PT, WS etc..,), any unpaid demand in the system is a candidate for amendments.

### **Functionality**

Amendment mainly works with two types of functionality as follows:

* Amendment
* Demand

### **Objective**

The main objective of the Bill-Amendment module is to create Credit/ Debit Notes against the bills for consumers who need an additional amount to be added to their bill.

### **Feature List**

* Create Amendment
* Search Amendment
* Update Demand
* Update Amendment

### **API DEFINITION**

[API SPEC FOR BILL-AMENDMENT](https://raw.githubusercontent.com/egovernments/business-services/master/Docs/billingservice/BillAmendment/v1.0.yml)

### **POSTMAN-COLLECTION**

[API COLLECTION BILL\_AMENDMENT](https://www.getpostman.com/collections/b195d3b1d354c767b6bd)

### **Functionality**

Bill Amendment provides a separate flow to enable workflow and validation for the process of adding additional amount into the existing demands which were done through the respective modules only till this point in time. An amendment will be allowed only when the reason arises from out of the system to add or reduce the amount from the existing bill belonging to an entity. The reasons are as listed below -

1. Court case settlement
2. One time waiver
3. Write-offs
4. DCB correction (Old demands in paid status)
5. Remission for Property Tax

### **Criteria**

There are certain prerequisites to create an amendment,

1. Presence of demand in the billing system
2. One of the reasons listed above
3. Valid document proof for the reason
4. No other Amendment already in workflow

### **PROCEDURE**

The process of adding Amendment is as follows

There are two scenarios on how an amendment will be completed which is based on the paid status of the existing demands in the system.

_**1. When demand is unpaid/partially paid**_

1. create a demand (Or an existing demand can be used) with demand detail → DD1.
2. Do not pay the bill or make payment partially.
3. Create an amendment for the same consumer-code (with demand detail → DD2).
4. approve the amendment, the response should return an amendment with status CONSUMED.
5. search the demand or fetch bill for the consumer-code, demand/bill should contain demand details of demand and amendment together DD1 and DD2 in the same demand/bill.

_**2. When demand is completely paid**_

1. create demand and make complete payment or choose a consumer-code which is fully paid.
2. create amendment (with demand detail → DD1).
3. Approve amendment, the response should be APPROVED this time.
4. create new demand for the consumer -code (with demand detail → DD3), demand response should contain two demand details DD1 and DD2 saved to the demand.
5. Now amendment search will return CONSUMED status after the demand is created.

### IMPACT

Does not impact any other functionality other than adding demand details to demands on APPROVAL.

IMPACTED BY:

Existence of demands in the system.

### **WORKFLOW CONFIG**

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

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation ](https://egov.org.in)is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).
