# Workflow Auto Escalation

## Overview

The objective of this functionality is to provide a mechanism to trigger action on applications that satisfy certain predefined criteria.&#x20;

## Sample Configuration

Looking at sample use cases, the majority of use cases can be summarised as performing action ‘X’ on applications in state ‘Y’ and have exceeded the state SLA by ‘Z’ days. We can write one query builder which takes this state ‘Y’ and SLA exceeded by ‘Z’ as search params and then we can perform action X on the search response. This has been achieved by defining an MDMS config like below:

```
{
  "tenantId": "pb",
  "moduleName": "Workflow",
  "AutoEscalation": [
    {
      "businessService": "PGR",
      "module": "pgr-services",
      "state": "RESOLVED",
      "action": "CLOSERESOLVEDCOMPLAIN",
      "active": "true",
      "stateSLA": 1.0,
      "businessSLA": null,
      "topic" : "pgr-auto-escalation"
    }
  ]
}
```

In the above configuration, we define the condition for triggering the escalation of applications. The above configuration triggers escalation for applications in `RESOLVED` state which have exceeded stateSLA by more than `1.0` day and it will trigger the escalation by performing `CLOSERESOLVEDCOMPLAIN` on the applications. Once the applications are escalated the processInstances are pushed on the `pgr-auto-escalation` topic. We have done a sample implementation for pgr-services, where we have updated the persister configuration to listen on this topic and update the complaint status accordingly.

```
  - version: 1.0
    description: Updates pgr status for auto escalate
    fromTopic: pgr-auto-escalation
    isTransaction: true
    queryMaps:

    - query: UPDATE eg_pgr_service_v2 SET applicationstatus=?, lastmodifiedby=?, lastmodifiedtime=? WHERE serviceRequestId=? AND tenantId=?;
      basePath: ProcessInstances.*
      jsonMaps:
      - jsonPath: $.ProcessInstances.*.state.applicationStatus

      - jsonPath: $.ProcessInstances.*.auditDetails.lastModifiedBy

      - jsonPath: $.ProcessInstances.*.auditDetails.lastModifiedTime

      - jsonPath: $.ProcessInstances.*.businessId

      - jsonPath: $.ProcessInstances.*.tenantId
```

The auto-escalation for businessService `PGR` will be triggered when the following API is called:

```
curl --location --request POST 'http://localhost:8081/egov-workflow-v2/egov-wf/auto/PGR/_escalate' \
--header 'Content-Type: application/json' \
--data-raw '{
    "RequestInfo": {
        "apiId": "Rainmaker",
        "action": "",
        "did": 1,
        "key": "",
        "msgId": "20170310130900|en_IN",
        "requesterId": "",
        "ts": 1513579888683,
        "ver": ".01",
        "authToken": "c66ee6b0-854c-4dde-b1a6-4b9f9b03a62f",
        "userInfo": {
            "id": 18397,
            "uuid": "cf209669-88e4-4da8-951b-a0173b3edcae",
            "userName": "TRUPTI",
            "name": "Trupti",
            "mobileNumber": "8970064765",
            "emailId": "",
            "locale": null,
            "type": "EMPLOYEE",
            "roles": [
                {
                    "name": "Auto Escalation Employee",
                    "code": "AUTO_ESCALATE",
                    "tenantId": "pb"
                }
            ],
            "active": true,
            "tenantId": "pb.amritsar",
            "permanentCity": null
        }
    }
}'
```

Note that the businessService is a path param. (For example, if the escalation has to be done for tl-services NewTL workflow the URL will be '`http://egov-workflow-v2.egov:8080/egov-workflow-v2/egov-wf/auto/NewTL/_escalate`').

These APIs have to be configured in the cron job config so that they can be triggered periodically according to the requirements. Only users with role `AUTO_ESCALATE` can trigger auto-escalation so first create users with statelevel `AUTO_ESCALATE` roles first and then add that user in the userInfo of the requestInfo. This step has to be done because the cron job does internal API calls and Zuul won’t enrich the userInfo.

For setting up autoescalation trigger the workflow also needs to be updated. For example to add auto escalate trigger on `RESOLVED` state with action `CLOSERESOLVEDCOMPLAIN` in `PGR` businessService, we will have to search the businessService and add the following action in the Actions array of `RESOLVED` state and call update API.

```
{
    "action": "CLOSERESOLVEDCOMPLAIN",
    "nextState": "CLOSEDAFTERRESOLUTION",
    "roles": [
    "AUTO_ESCALATE"
    ]
}
```

Suppose an application gets auto-escalated from state ‘X' to state 'Y’, employees can look at these escalated applications through the escalate search API. The following sample cURL can be used to search auto-escalated applications of the PGR module belonging to Amritsar tenant -

```
curl --location --request POST 'https://dev.digit.org/egov-workflow-v2/egov-wf/escalate/_search?tenantId=pb.amritsar&businessService=PGR' \
--header 'Content-Type: application/json' \
--data-raw '{
    "RequestInfo": {
        "apiId": "Rainmaker",
        "action": "",
        "did": 1,
        "key": "",
        "msgId": "20170310130900|en_IN",
        "requesterId": "",
        "ts": "",
        "ver": ".01",
        "authToken": "ef5dd6d8-a76b-40a2-94e1-c810a46eb50b"
    }
}'
```



[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_ ](https://egov.org.in/)_is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
