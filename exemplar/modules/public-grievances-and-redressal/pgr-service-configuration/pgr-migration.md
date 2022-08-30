---
description: Learn more about module migration details
---

# PGR Migration

## Setup <a href="#setup" id="setup"></a>

|                                  |                                                                                                                                                                                    |
| -------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Config/Service Name**          | **Path/Build**                                                                                                                                                                     |
| Persister yml for bulk migration | [https://github.com/egovernments/configs/blob/DEV/egov-persister/pgr-migration-batch.yml](https://github.com/egovernments/configs/blob/DEV/egov-persister/pgr-migration-batch.yml) |
| pgr-services                     | pgr-services-db:pgr-migration-2475ec38-56                                                                                                                                          |
| rainmaker-pgr                    | rainmaker-pgr-db:pgr-migration-c046a264-20                                                                                                                                         |

The above build has to be deployed to perform the migration. The batch persister config has to be added in config Repo. After adding the file in the repo, update the persister path in environment yml file. Make sure the persister.bulk.enabled is set to true. Once done restart the persister pod.

To start the migration call the following API with tenantId as param it will migrate data belonging to that tenantId. The API does not have role action mapping and should be used by port forwarding rainmaker-pgr pod.

```
curl --location --request POST 'http://localhost:8083/rainmaker-pgr/v2/_migrate?tenantIds=pb.jalandhar' \
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
        "authToken": "6fc5bb66-f3f1-49fa-b750-34f7b33d80d4",
        "userInfo": {
        "id": 23287,
        "uuid": "4632c941-cb1e-4b83-b2d4-200022c1a137",
        "userName": "PalashS",
        "name": "Palash S",
        "mobileNumber": "9949032246",
        "emailId": null,
        "locale": null,
        "type": "EMPLOYEE",
        "roles": [
            {
                "name": "PGR Last Mile Employee",
                "code": "PGR_LME",
                "tenantId": "pb.amritsar"
            },
            {
                "name": "Employee",
                "code": "EMPLOYEE",
                "tenantId": "pb"
            },
            {
                "name": "Employee",
                "code": "EMPLOYEE",
                "tenantId": "pb.amritsar"
            }
        ],
        "active": true,
        "tenantId": "pb.amritsar"
    }
    }
}'
```

## WSD <a href="#wsd" id="wsd"></a>

![](<../../../../.gitbook/assets/image (97) (1).png>)

## Validation Queries <a href="#validation-queries" id="validation-queries"></a>

```
select  distinct(action),count(*) from eg_pgr_action group by  action
select st.state,count(*) from eg_wf_processinstance_v2 pi INNER JOIN eg_wf_state_v2 st ON st.uuid = pi.status  where businessService ='PGR' group by st.state

select tenantId,count(*) from eg_pgr_service group by tenantId;
select tenantId,count(*) from eg_pgr_service_v2 group by tenantId;

select servicecode,count(*) from eg_pgr_service group by servicecode;
select servicecode,count(*) from eg_pgr_service_v2 group by servicecode;

select active,count(*) from eg_pgr_service group by active;
select active,count(*) from eg_pgr_service_v2 group by active;

select count(*) from eg_pgr_address
select count(*) from eg_pgr_address_v2

-- Assignee count match
select count(*) from eg_pgr_action where assignee is not null;
select count(*) from eg_wf_assignee_v2;

select count(*)  from eg_pgr_action  where media NOT in ('[]','null')
select count(*) from eg_wf_document_v2 where processinstanceid IN (select id from eg_wf_processinstance_v2 where businessService ='PGR')
```

_\*(Last query related to document might need little modification as values in NOT IN clause can be more than the 2 specified)_

## Prod Data Insights <a href="#prod-data-insights" id="prod-data-insights"></a>

1. null value is stored in action for adding comments in the old system it’s mapped to COMMENT in new system.
2. The Locality attribute in new eg\_pgr\_address\_v2 table does not allow NULL values whereas the locality attribute in the old eg\_pgr\_address in Punjab prod data has NULL values. Those values are filled in migration with dummy value NOT\_AVAILABLE.
3. For 128 records accountId is NULL and so they won’t be associated with any citizen login.
4. For some records in the media column corrupt data is present. For example, in one case instead of fileStore uuid some normal text describing the complaint is present. While some other records have values like no. For data with such text having a length greater than 64 are set to null, else DB validations are violated.
5. In the old system-id is stored for referencing user data. In new systems we use uuid to refer user, therefore all id is mapped to respective uuid which are then migrated to the new system. If some user has uuid as NULL default value NOT\_SPECIFIED will be used.
6. Some 1104 complaints has value in the column named feedback which seems to be from some set of predefined values like "Resolution Time", "Quality of work", ”others” etc. The new structure does not have any such column so we will be storing this in additionalDetails.
7. Address and landmark column in eg\_pgr\_service has values in some column they are also stored in additionalDetails.
8. Phone column contains phone numbers, we are not migrating that column as it has PII data and will be already present in user service as well.
9. If sla is not found in the old config (will only happen if some complaint category is removed from MDMS and complaints are present in the system of that category) default SLA value will be used.

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation ](https://egov.org.in/)is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).
