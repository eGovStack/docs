# Technical Script/Steps For Migration Process

This specifies the migration steps which is specific to payment index .

## Step 1. Adding a target index <a id="Step-1.-Adding-a-target-index"></a>

Add index name dss-payment\_v2 as below:

In kibana, dev tools, apply the below command

<table>
  <thead>
    <tr>
      <th style="text-align:left">
        <p>PUT dss-payment_v2</p>
        <p>{} // add mapping file content here. mapping.json as attached below</p>
      </th>
    </tr>
  </thead>
  <tbody></tbody>
</table>

Note: This name should be as the value present in ingest es.index.namemapping.json24 May 2021, 11:15 AM

## Step 2. Optional changes required in Ingest application properties <a id="Step-2.-Optional-changes-required-in-Ingest-application-properties"></a>

Ingest pipeline application properties contain **es.direct.push** supposed to be set **true** for testing.

| **Sno** | **Property name** | **Value** | **Description** |
| :--- | :--- | :--- | :--- |
| 1. | es.direct.push | true | the transformed data will be pushed to ES index directly. |
| 2. | es.direct.push | false | the transformed data will be lying at egov-dss-ingest-enriched topic |

## Step 3. Run migration Api, which migrate the data from the source index to target index. <a id="Step-3.-Run-migration-Api,-which-migrate-the-data-from-the-source-index-to-target-index."></a>

<table>
  <thead>
    <tr>
      <th style="text-align:left"><b>SNo</b>
      </th>
      <th style="text-align:left"><b>Name</b>
      </th>
      <th style="text-align:left"><b>Description</b>
      </th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">
        <p>Method</p>
        <p>End Point</p>
        <p>Body</p>
      </td>
      <td style="text-align:left">
        <p>POST</p>
        <p>{host}/dashboard-ingest/ingest/migrate/paymentsindex-v1/v2</p>
        <p>{&quot;RequestInfo&quot;:{&quot;authToken&quot;:&quot;2ba70924-1bba-4a9b-b55d-2e9471bf3081&quot;}}</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">2.</td>
      <td style="text-align:left">CURL</td>
      <td style="text-align:left">curl -X POST
        <br /><a href="https://dev.digit.org/dashboard-ingest/ingest/migrate/paymentsindex-v1/v2">https://dev.digit.org/dashboard-ingest/ingest/migrate/paymentsindex-v1/v2</a>
        <br
        />-H &apos;cache-control: no-cache&apos;
        <br />-H &apos;content-type: application/json&apos;
        <br />-H &apos;postman-token: d83fc136-116d-265f-3b83-ea41e3d5bb57&apos;
        <br
        />-d &apos;{&quot;RequestInfo&quot;:{&quot;authToken&quot;:&quot;2ba70924-1bba-4a9b-b55d-2e9471bf3081&quot;}}&apos;</td>
    </tr>
  </tbody>
</table>

**Note:** After migration ensure dss-payment\_v2 data has been populated and available

In kibana, dev tools verify using below command

| GET dss-payment\_v2/\_search |
| :--- |


> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)\_\_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_ ](https://egov.org.in/)_is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._

