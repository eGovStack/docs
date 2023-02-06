# Technical Script/Steps For Migration Process

## Overview

This specifies the migration steps which are specific to the payment index.

## Steps <a href="#step-1.-adding-a-target-index" id="step-1.-adding-a-target-index"></a>

#### Step 1. Adding a target index <a href="#step-1.-adding-a-target-index" id="step-1.-adding-a-target-index"></a>

Add index name dss-payment\_v2 as below:

In Kibana dev tools, apply the below command

|                                                                                                     |
| --------------------------------------------------------------------------------------------------- |
| <p>PUT dss-payment_v2</p><p>{} // add mapping file content here. mapping.json as attached below</p> |

{% hint style="info" %}
**Note:** This name should be the value present in ingest es.index.namemapping.json24 May 2021, 11:15 AM
{% endhint %}

#### Step 2. Optional changes required in Ingest application properties <a href="#step-2.-optional-changes-required-in-ingest-application-properties" id="step-2.-optional-changes-required-in-ingest-application-properties"></a>

Ingest pipeline application properties contain **es.direct.push** supposed to be set **true** for testing.

| Property Name  | Value | Description                                                          |
| -------------- | ----- | -------------------------------------------------------------------- |
| es.direct.push | true  | the transformed data will be pushed to ES index directly.            |
| es.direct.push | false | the transformed data will be lying at egov-dss-ingest-enriched topic |

#### Step 3. Run migration API, which migrates the data from the source index to the target index. <a href="#step-3.-run-migration-api-which-migrate-the-data-from-the-source-index-to-target-index." id="step-3.-run-migration-api-which-migrate-the-data-from-the-source-index-to-target-index."></a>

| Name                                     | Description                                                                                                                                                                                                                                                                                                                                                                                              |
| ---------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <p>Method</p><p>End Point</p><p>Body</p> | <p>POST</p><p>{host}/dashboard-ingest/ingest/migrate/paymentsindex-v1/v2</p><p>{"RequestInfo":{"authToken":"2ba70924-1bba-4a9b-b55d-2e9471bf3081"}}</p>                                                                                                                                                                                                                                                  |
| CURL                                     | <p>curl -X POST<br><a href="https://dev.digit.org/dashboard-ingest/ingest/migrate/paymentsindex-v1/v2">https://dev.digit.org/dashboard-ingest/ingest/migrate/paymentsindex-v1/v2</a><br>-H 'cache-control: no-cache'<br>-H 'content-type: application/json'<br>-H 'postman-token: d83fc136-116d-265f-3b83-ea41e3d5bb57'<br>-d '{"RequestInfo":{"authToken":"2ba70924-1bba-4a9b-b55d-2e9471bf3081"}}'</p> |

{% hint style="info" %}
**Note:** After migration ensures dss-payment\_v2 data has been populated and is available.
{% endhint %}

In Kibana dev tools verify using the below command

```
GET dss-payment_v2/_search
```

