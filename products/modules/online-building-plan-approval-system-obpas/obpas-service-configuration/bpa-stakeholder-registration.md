---
description: Feature release doc
---

# BPA Stakeholder Registration

## Overview

The Stakeholder registration process is done to allow any user access to the Building plan approval portal. The user registers the application for the desired role. Upon approval of the application, the user gets the role based on the application. This role will be stake level role. The user can also register on behalf of the organisation.

{% hint style="info" %}
**Notes:**

* Users can register for one role with a mobile number only once
* After submission of the application user login is required to pay and view the status of his application
* The citizen will get a state-level role on approval of his application
* Employees performing actions on user applications must have suitable state-level roles\

{% endhint %}

**License types**: Engineer, Town Planner, Builder, Architect, Structural Engineer

**Actors:** Citizen, Document Verifier, Approver

**States of any application:** Initiated, Pending for payment, Pending for document      verification, Pending for approval, Approved, Rejected

{% file src="../../../../.gitbook/assets/bpa_stakeholder_registration (3) (1).yaml" %}

## **Promotion Steps**

### **Backend**

Promote latest MDMS

**MDMS**

* TradeLicense:- added type field in existing records and added new trade types

[<img src="https://github.com/fluidicon.png" alt="" data-size="line">egov-mdms-data/TradeType.json at master · egovernments/egov-mdms-data](https://github.com/egovernments/egov-mdms-data/blob/master/data/pb/TradeLicense/TradeType.json)

* StakeholderRegistraition:- Contains additional information for each of the trade types being used in BPA registration&#x20;

[<img src="https://github.com/fluidicon.png" alt="" data-size="line">egov-mdms-data/TradeTypetoRoleMapping.json at master · egovernments/egov-mdms-data](https://github.com/egovernments/egov-mdms-data/blob/master/data/pb/StakeholderRegistraition/TradeTypetoRoleMapping.json)

* [<img src="https://github.com/fluidicon.png" alt="" data-size="line">egov-mdms-data/data/pb/ACCESSCONTROL-ROLEACTIONS at master · egovernments/egov-mdms-data](https://github.com/egovernments/egov-mdms-data/tree/master/data/pb/ACCESSCONTROL-ROLEACTIONS)
* [<img src="https://github.com/fluidicon.png" alt="" data-size="line">egov-mdms-data/data/pb/ACCESSCONTROL-ACTIONS-TEST at master · egovernments/egov-mdms-data](https://github.com/egovernments/egov-mdms-data/tree/master/data/pb/ACCESSCONTROL-ACTIONS-TEST)
* [<img src="https://github.com/fluidicon.png" alt="" data-size="line">egov-mdms-data/TaxHeadMaster.json at master · egovernments/egov-mdms-data](https://github.com/egovernments/egov-mdms-data/blob/master/data/pb/BillingService/TaxHeadMaster.json)
* [<img src="https://github.com/fluidicon.png" alt="" data-size="line">egov-mdms-data/data/pb/ACCESSCONTROL-ROLES at master · egovernments/egov-mdms-data](https://github.com/egovernments/egov-mdms-data/tree/master/data/pb/ACCESSCONTROL-ROLES)
* [<img src="https://github.com/fluidicon.png" alt="" data-size="line">egov-mdms-data/DecryptionABAC.json at master · egovernments/egov-mdms-data](https://github.com/egovernments/egov-mdms-data/blob/master/data/pb/DataSecurity/DecryptionABAC.json)
* [<img src="https://github.com/fluidicon.png" alt="" data-size="line">egov-mdms-data/IdFormat.json at master · egovernments/egov-mdms-data](https://github.com/egovernments/egov-mdms-data/blob/master/data/pb/common-masters/IdFormat.json)

&#x20;**Endpoints:**&#x20;

Please whitelist the endpoint from Zuul wherever required

* /tl-services/v1/BPAREG/\_create:- mixed (both whitelisted and auth based)
* /tl-services/v1/BPAREG/\_update:- mixed (both whitelisted and auth based)

&#x20;Auth based access:- CITIZEN,BPAREG\_DOC\_VERIFIER, BPAREG\_EMPLOYEE, BPAREG\_APPROVER

* /tl-services/v1/BPAREG/\_search :- Citizen, Approver, Document Verifier
* /tl-calculator/v1/BPAREG/\_getbill:- mixed (both whitelisted and auth based)

Auth based access:- CITIZEN,BPAREG\_DOC\_VERIFIER, BPAREG\_EMPLOYEE, BPAREG\_APPROVER

**Users:**

* Create users with state level roles(tenantId=’pb’) , BPAREG\_DOC\_VERIFIER, EMPLOYEE, BPAREG\_APPROVER
* Create an anonymous user(related to whitelisting). Please refer to the end of this doc
* Workflow config file -&#x20;

{% file src="../../../../.gitbook/assets/BPA Stakeholder Registration workflow config.docx" %}

Service Builds (use these or newer builds from master)

* Billing-service-5f944c55c5-4dqcx
* **TL-service: tl-services-db:42-bpa-work-9371fe2**
* **TL-calculator: tl-calculator-db:10-bpa-work-128d676**
* Citizen - citizen:210-Nov-15-Release-49699801
* Employee - employee:238-Nov-15-Release-49699801
* Zuul: **zuul:21-master-5368046**
* Workflow: egov-workflow-v2:9-WF\_MULTITENANCY-40d533f
* Restart user and encryption service

Persister Config

* [<img src="https://github.com/fluidicon.png" alt="" data-size="line">configs/tradelicense-persister-bpachanges.yml at master · egovernments/configs](https://github.com/egovernments/configs/blob/master/egov-persister/tradelicense-persister-bpachanges.yml)

Localisation File:&#x20;

{% file src="../../../../.gitbook/assets/BPAREG_Localisation.xlsx" %}

**SQL Query:**&#x20;

Please run the below SQL script to add state-level bank account:

insert into egf\_bank ( id,code,name,active,tenantid) values ( '23','AXIS','AXIS BANK',t,'pb')

insert into egf\_bankbranch(id,bankid,code,name,address,city,state,contactperson,active,createddate ,lastmodifieddate,tenantid)  values ('8','23','123','Axis\_Bank\_Ltd\_Punjab','Amritsar','Amrisar','Punjab','ABCD','t','2019-08-16 21:04:32.064' ,'2019-08-16 21:04:32.064','pb')

insert into egf\_bankaccount(id,bankbranchid ,chartofaccountid,fundid , accountnumber,accounttype , active ,type, createddate, lastmodifieddate ,tenantid)  values ('8','123','1234','12', '91101055559123', 'SAVINGS' ,'t' ,'RECEIPTS\_PAYMENTS', '2018-08-16 21:24:48.837','2018-08-16 21:24:48.837','pb')

Add ANONYMOUS  role and create a system user as given below

```
{
 "requestInfo": {
   "apiId": "Rainmaker",
   "ver": ".01",
   "ts": null,
   "action": "_update",
   "did": "1",
   "key": "",
   "msgId": "20170310130900|en_IN",
   "authToken": "5a445d2c-c742-4e07-aaac-2a11e06830fc",
   "userInfo": {
     "id": 301,
     "userName": "EMP10",
     "name": "Employee 10",
     "type": "EMPLOYEE",
     "mobileNumber": "9999405321",
     "emailId": "",
     "roles": [
       {
         "id": 58,
         "name": "Employee",
         "code": "EMPLOYEE"
       }
     ],
     "tenantId": "pb.amritsar",
     "uuid": "dbbb4668-3bba-4f37-8fff-d072b84eb01b"
   }
 },
 "user": {
   "userName": "SYSTEM1",
   "name": "System User",
   "gender": null,
   "mobileNumber": "9191919191",
   "type": "SYSTEM",
   "roles": [
     {
       "id": null,
       "name": "Anonymous User",
       "code": "ANONYMOUS",
       "description": null,
       "createdBy": null,
       "createdDate": null,
       "lastModifiedBy": null,
       "lastModifiedDate": null,
       "tenantId": null
     },
    {
       "id": null,
       "name": "Employee",
       "code": "EMPLOYEE",
       "description": null,
       "createdBy": null,
       "createdDate": null,
       "lastModifiedBy": null,
       "lastModifiedDate": null,
       "tenantId": ‘pb“
     }
   ],
   "tenantId": "pb"
 }
}

```

&#x20;[https://egov-micro-qa.egovernments.org/user/users/\_createnovalidate](https://egov-micro-qa.egovernments.org/user/users/\_createnovalidate)

\
\


