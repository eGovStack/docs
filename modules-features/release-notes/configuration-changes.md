---
description: DIGIT 2.0 - Technical Details of the Changes
---

# Configuration Changes

## **MDMS changes**

| **Feature** | **Status** | **Changes** | **Description** |
| :--- | :--- | :--- | :--- |
| BPA | New | [PR-1123](https://github.com/egovernments/egov-mdms-data/pull/1123/files) | To add an order for the documents |
| BPA | Deprecate | [PR-1037](https://github.com/egovernments/egov-mdms-data/pull/1037/files) | removed the sanction for OC low application |
| BPA | Update | [PR-1118](https://github.com/egovernments/egov-mdms-data/pull/1118/files) | To update disclaimer |
| BPA | Update | [PR-1062](https://github.com/egovernments/egov-mdms-data/pull/1062/files) | Changed URL - BPA to land |
| BPA | New | [PR-1019](https://github.com/egovernments/egov-mdms-data/pull/1019/files) | Added id Format for OC |
| BPA | New | [PR-1016](https://github.com/egovernments/egov-mdms-data/pull/1016/files) | Added checklist for OC |
| BPA | Update | [PR-1008](https://github.com/egovernments/egov-mdms-data/pull/1008/files) | Updated usages |
| BPA | Update | [PR-1007](https://github.com/egovernments/egov-mdms-data/pull/1007/files) | Updated Sub occupancy type |
| BPA | Update | [PR-1006](https://github.com/egovernments/egov-mdms-data/pull/1006) | Updated Occupancy type |
| BPA | New | [PR-997](https://github.com/egovernments/egov-mdms-data/pull/997) | Added tax period for OC |
| BPA | New | [PR-996](https://github.com/egovernments/egov-mdms-data/pull/996/files) | Added tax headmaster for OC |
| BPA | New | [PR-995](https://github.com/egovernments/egov-mdms-data/pull/995/files) | Added billing service for OC |
| BPA | Update | [PR-1162](https://github.com/egovernments/egov-mdms-data/pull/1162/files) | Changed id format for BPA permit |
| W&S | Update | [PR-1043](https://github.com/egovernments/egov-mdms-data/pull/1043) | To update the ID format |
| W&S | Update | [PR-1058](https://github.com/egovernments/egov-mdms-data/pull/1058) | to update application types |
| TL | Update | [PR-1160](https://github.com/egovernments/egov-mdms-data/pull/1160) | Updated URL for Required doc screen |
| TL | Update | [PR-1125](https://github.com/egovernments/egov-mdms-data/pull/1125) | Updated rebate and penalty |
| TL | Update | [PR-1133](https://github.com/egovernments/egov-mdms-data/pull/1133) | TL Renewal changes |
| UC | New | [PR-1106](https://github.com/egovernments/egov-mdms-data/pull/1106) | Added disclaimer in the footer |
| Localization | New | [PR-1073](https://github.com/egovernments/egov-mdms-data/pull/1073) | Added new action for v2 localisation search |
| Reports | Deprecate | [PR-1170](https://github.com/egovernments/egov-mdms-data/pull/1170) | Disabling the Reports and UI localization Links |

## Backend Config Changes

| **Module** | **Action** | **PR** | **Description** |
| :--- | :--- | :--- | :--- |
| W&S | Update | [PR-357](https://github.com/egovernments/configs/pull/357) | To update bill PDF advance adjusted changes |
| W&S | Update | [PR-340](https://github.com/egovernments/configs/pull/340) | To Update PDF format |
| W&S | Update | [PR-342](https://github.com/egovernments/configs/pull/342) | To add Advance and pending amount conditional logic |
| W&S | Update | [water-meter.yml](https://github.com/egovernments/configs/commit/d213b8fbc71c8adc67df393b30c8be9ea923e24f#diff-cad1acac07cf6e6c1843536937285a4d) | To add tenant Id in the eg\_ws\_meterreading table |
| W&S | Update | [ws-bill.json](https://github.com/egovernments/configs/commit/900e8e1c59ebc12f4bea49f52063f524aabf3830#diff-b5d08abcd9524da252a33fcff4c515f8) | To update the WS bill PDF format |
| BillGenie | Update | [bill-genie.yml](https://github.com/egovernments/configs/commit/0f3708cdcf6fba00aa36aab5baeae9a7eeb3ab62#diff-9352898a62515ccb3822f24506a37090) | To Update lower cases search |
| BPA | Update | [land-persister.yml](https://github.com/egovernments/configs/commit/5682f1adb60b40663fe13d545e0c865ad4537b08) | Added audit details for owner |
| BPA | Deprecate | [bpa-persister.yml](https://github.com/egovernments/configs/commit/9ae764474a702249cd3aaefa806a3331a37e0364) | Removed land info from bpa-persister |
| BPA | New | [egov-bpa-indexer.yml](https://github.com/egovernments/configs/commit/47528052b4904ce5ab679324f13165458a83d05a) | Added indexer for BPA |
| BPA | New | [rainmaker-bpastakeholder-indexer.yml](https://github.com/egovernments/configs/commit/47528052b4904ce5ab679324f13165458a83d05a) | Added indexer for stakeholder Registration |
| BPA | Update | [bpa-revocation.json](https://github.com/egovernments/configs/commit/47528052b4904ce5ab679324f13165458a83d05a) | Changed owners to land info and added revocation letter content |
| BPA | New | [buildingpermit-low.json](https://github.com/egovernments/configs/commit/47528052b4904ce5ab679324f13165458a83d05a) | Added report run date |
| BPA | New | [buildingpermit.json](https://github.com/egovernments/configs/commit/47528052b4904ce5ab679324f13165458a83d05a) | Added report run date |
| BPA | New | [occupancy-certificate.json](https://github.com/egovernments/configs/commit/47528052b4904ce5ab679324f13165458a83d05a) | Added OC certificate |
| BPA | Update | [bpa-revocation.json](https://github.com/egovernments/configs/commit/47528052b4904ce5ab679324f13165458a83d05a) | Updated texts |
| BPA | Update | [buildingpermit.json](https://github.com/egovernments/configs/commit/47528052b4904ce5ab679324f13165458a83d05a) | Changed alignment and added QA code |
| BPA | New | [occupancy-certificate.json](https://github.com/egovernments/configs/commit/47528052b4904ce5ab679324f13165458a83d05a) | Added for OC |
| BPA | Update | [buildingpermit-low.json](https://github.com/egovernments/configs/commit/3da5fcefeedda4b13eda3128b42c8e87aea6697a) | Changed alignment and added QA code |
| BPA | New | [occupancy-certificate.json](https://github.com/egovernments/configs/commit/143dda97f86e06544868ec92d5816766ea128e75) | Added for OC |
| BPA | Update | [noc-persister.yml](https://github.com/egovernments/configs/commit/b94803a5d2e700b56c35b89b8cde5e1e32cfdbc4) | Changed filestore to filestoreId |
| BPA | Update | [noc-persister.yml](https://github.com/egovernments/configs/commit/5f7eafdf3339d49a736d31c50037333a11c0f114) | Updated NOC persister |

## Infra/Deployment Config Changes

<table>
  <thead>
    <tr>
      <th style="text-align:left">Module</th>
      <th style="text-align:left">File Name</th>
      <th style="text-align:left">Action</th>
      <th style="text-align:left">Code Change</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">W&amp;S</td>
      <td style="text-align:left">helm/charts/municipal-services/sw-services/values.yaml</td>
      <td style="text-align:left">Removed the following details from values.yml</td>
      <td style="text-align:left"><code>scid-format: &quot;SW/[CITY.CODE]/[fy:yyyy-yy]/[SEQ_EGOV_COMMON]&quot;</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">EGOV_IDGEN_SCID_FORMAT</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><code>value: {{ index .Values &quot;scid-format&quot; | quote }}</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">helm/charts/municipal-services/ws-services/values.yaml</td>
      <td style="text-align:left">Removed the following details from values.yml</td>
      <td style="text-align:left"><code>wcid-format: &quot;WS/[CITY.CODE]/[fy:yyyy-yy]/[SEQ_EGOV_COMMON]&quot;</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">EGOV_IDGEN_WCID_FORMAT</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><code>value: {{ index .Values &quot;wcid-format&quot; | quote }}</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">helm/environments/&lt;env&gt;.yaml</td>
      <td style="text-align:left">Autocreate-new-seq flag must be enabled in IdGen Service of the environment
        file</td>
      <td style="text-align:left"><code>autocreate-new-seq: &quot;true&quot;</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">helm/environments/qa.yaml</td>
      <td style="text-align:left">Change the key from allowed-file-formats: to <b>allowed-file-formats-map</b>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">helm/charts/municipal-services/firenoc-services/values.yaml</td>
      <td style="text-align:left">Added EGOV_DEFAULT_STATE_ID in fire NOC environment file to pick up proper
        tenant during search call</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">SMS Notification Service</td>
      <td style="text-align:left">helm/charts/core-services/egov-notification-sms/values.yaml</td>
      <td style="text-align:left">
        <p>Added sms.config.map property for SMS changes-Remove the sms.config.map
          from the values.yml file</p>
        <p>It should move to <b>helm/environments/&lt;env&gt;.yaml</b>
        </p>
      </td>
      <td style="text-align:left"><code>sms-config-map: &quot;{&apos;User&apos;:&apos;$username&apos;, &apos;passwd&apos;: &apos;$password&apos;, &apos;sid&apos;:&apos;$senderid&apos;, &apos;mobilenumber&apos;:&apos;$mobileno&apos;, &apos;message&apos;:&apos;$message&apos;, &apos;mtype&apos;:&apos;N&apos;, &apos;DR&apos;:&apos;N&apos;, &apos;smsservicetype&apos;:&apos;singlemsg&apos;}&quot;</code>
      </td>
    </tr>
  </tbody>
</table>

## Service Build Artefacts

<table>
  <thead>
    <tr>
      <th style="text-align:left">C<b>ategory</b>
      </th>
      <th style="text-align:left"><b>Services</b>
      </th>
      <th style="text-align:left"><b>GIT TAGS</b>
      </th>
      <th style="text-align:left"><b>Docker Artifact ID</b>
      </th>
      <th style="text-align:left">MDMS Changes</th>
      <th style="text-align:left">Config Changes</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><b>Frontend</b>  <a href="https://github.com/egovernments/municipal-services/tree/v2.0"><b>v2.0</b></a>
      </td>
      <td style="text-align:left">Citizen</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/frontend/tree/citizen-v1.0.0">citizen-v1.0.0</a>
      </td>
      <td style="text-align:left">citizen:v1.0.0-5c70cea1d</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">Employee</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/frontend/tree/employee-v1.0.0">employee-v1.0.0</a>
      </td>
      <td style="text-align:left">employee:v1.0.0-5c70cea1d</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">DSS Dashboard</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/frontend/tree/dashboard-v1.0.0">dashboard-v1.0.0</a>
      </td>
      <td style="text-align:left">dss-dashboard:v1.0.0-766ef5a0a</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Core Services</b>  <a href="https://github.com/egovernments/core-services/tree/v2.0"><b>v2.0</b></a>
      </td>
      <td style="text-align:left">Encryption</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/core-services/tree/enc-service-v1.1.0">enc-service-v1.1.0</a>
      </td>
      <td style="text-align:left">egov-enc-service:v1.1.0-f9375a4</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">Searcher</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/core-services/tree/searcher-v1.1.0">searcher-v1.1.0</a>
      </td>
      <td style="text-align:left">egov-searcher:v1.1.0-59d3598</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">Payment Gateway</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/core-services/tree/pg-service-v1.1.0">pg-service-v1.1.0</a>
      </td>
      <td style="text-align:left">egov-pg-service:v1.1.0-f9375a4</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">Filestore</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/core-services/tree/filestore-v1.2.0">filestore-v1.2.0</a>
      </td>
      <td style="text-align:left">egov-filestore:v1.2.0-3acc52b</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">Zuul - API Gateway</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/core-services/tree/zuul-v1.1.0">zuul-v1.1.0</a>
      </td>
      <td style="text-align:left">zuul:v1.1.0-582ddd0</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">Mail Notification</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/core-services/tree/notification-mail-v1.1.0">notification-mail-v1.1.0</a>
      </td>
      <td style="text-align:left">egov-notification-mail:v1.1.0-40b5f2d</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">SMS Notification</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/core-services/tree/notification-sms-v1.1.0">notification-sms-v1.1.0</a>
      </td>
      <td style="text-align:left">egov-notification-sms:v1.1.0-245443e</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">Localization</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/core-services/tree/localization-v1.1.0">localization-v1.1.0</a>
      </td>
      <td style="text-align:left">egov-localization:v1.1.0-f9375a4</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/egov-mdms-data/pull/1073">PR-1073</a>
      </td>
      <td style="text-align:left">
        <p><a href="https://raw.githubusercontent.com/egovernments/releasekit/master/localisation/data.json">Localisation data</a>
        </p>
        <p><a href="https://raw.githubusercontent.com/egovernments/releasekit/master/localisation/ws_30_07_2020.json">WS Localisation data</a>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">Persister</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/core-services/tree/persister-v1.1.0">persister-v1.1.0</a>
      </td>
      <td style="text-align:left">egov-persister:v1.1.0-9994513</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">ID Gen</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/core-services/tree/idgen-v1.2.0">idgen-v1.2.0</a>
      </td>
      <td style="text-align:left">egov-idgen:v1.2.0-f9375a4</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">User</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/core-services/tree/user-v1.2.1">user-v1.2.1</a>
      </td>
      <td style="text-align:left">egov-user:v1.2.1-4976757</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">User Chatbot</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/core-services/tree/user-chatbot-v1.2.1">user-chatbot-v1.2.1</a>
      </td>
      <td style="text-align:left">egov-user-chatbot:v1.2.1-4976757</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">MDMS</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/core-services/tree/mdms-service-v1.3.0">mdms-service-v1.3.0</a>
      </td>
      <td style="text-align:left">egov-mdms-service:v1.3.0-e50b9eb</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">URL Shortening</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/core-services/tree/url-shortening-v1.0.0">url-shortening-v1.0.0</a>
      </td>
      <td style="text-align:left">egov-url-shortening:v1.0.0-40cc090</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">Indexer</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/core-services/tree/indexer-v1.1.0">indexer-v1.1.0</a>
      </td>
      <td style="text-align:left">egov-indexer:v1.1.0-07592ae</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">
        <p><a href="https://github.com/egovernments/configs/commit/47528052b4904ce5ab679324f13165458a83d05a">egov-bpa-indexer.yml</a>
        </p>
        <p><a href="https://github.com/egovernments/configs/commit/47528052b4904ce5ab679324f13165458a83d05a">rainmaker-bpastakeholder-indexer.yml</a>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">Report</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/core-services/tree/report-v1.3.0">report-v1.3.0</a>
      </td>
      <td style="text-align:left">report:v1.3.0-28b3c97</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/egov-mdms-data/pull/1170">PR-1170</a>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">Workflow</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/core-services/tree/workflow-v2-v1.1.0">workflow-v2-v1.1.0</a>
      </td>
      <td style="text-align:left">egov-workflow-v2:v1.1.0-42786ef</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">PDF Generator</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/core-services/tree/pdf-service-v1.1.0">pdf-service-v1.1.0</a>
      </td>
      <td style="text-align:left">pdf-service:v1.1.0-09b11d9</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">Chatbot</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/core-services/tree/chatbot-v1.0.0">chatbot-v1.0.0</a>
      </td>
      <td style="text-align:left">chatbot:v1.0.0-f905f54</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">Access Control</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/core-services/tree/accesscontrol-v1.1.0">accesscontrol-v1.1.0</a>
      </td>
      <td style="text-align:left">egov-accesscontrol:v1.1.0-f9375a4</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">Location</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/core-services/tree/location-v1.1.0">location-v1.1.0</a>
      </td>
      <td style="text-align:left">egov-location:v1.1.0-f9375a4</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">OTP</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/core-services/tree/otp-v1.2.0">otp-v1.2.0</a>
      </td>
      <td style="text-align:left">egov-otp:v1.2.0-f9375a4</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">User OTP</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/core-services/tree/user-otp-v1.1.0">user-otp-v1.1.0</a>
      </td>
      <td style="text-align:left">user-otp:v1.1.0-2f36d3a</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Business Services</b>  <a href="https://github.com/egovernments/business-services/tree/v2.0"><b>v2.0</b></a>
      </td>
      <td style="text-align:left">Apportion</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/business-services/tree/apportion-service-v1.1.0">apportion-service-v1.1.0</a>
      </td>
      <td style="text-align:left">egov-apportion-service:v1.1.0-5553009</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">Collection</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/business-services/tree/collection-services-v1.1.0">collection-services-v1.1.0</a>
      </td>
      <td style="text-align:left">collection-services:v1.1.0-afb3913</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/egov-mdms-data/pull/1106">PR-1106</a>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">Billing</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/business-services/tree/billing-service-v1.1.0">billing-service-v1.1.0</a>
      </td>
      <td style="text-align:left">billing-service:v1.1.0-4367159</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><a href="https://github.com/egovernments/configs/commit/0f3708cdcf6fba00aa36aab5baeae9a7eeb3ab62#diff-9352898a62515ccb3822f24506a37090">bill-genie.yml</a>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">HRMS</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/business-services/tree/hrms-v1.1.0">hrms-v1.1.0</a>
      </td>
      <td style="text-align:left">egov-hrms:v1.1.0-43cb793</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">Dashboard Analytics</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/business-services/tree/dashboard-analytics-v1.1.0">dashboard-analytics-v1.1.0</a>
      </td>
      <td style="text-align:left">dashboard-analytics:v1.1.0-de5ab6d</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">Dashboard Ingest</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/business-services/tree/dashboard-ingest-v1.1.0">dashboard-ingest-v1.1.0</a>
      </td>
      <td style="text-align:left">dashboard-ingest:v1.1.0-5cc43bf</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">EGF Instrument</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/business-services/tree/egf-instrument-v1.1.0">egf-instrument-v1.1.0</a>
      </td>
      <td style="text-align:left">egf-instrument:v1.1.0-87dfb2d</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">EGF Master</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/business-services/tree/egf-master-v1.1.0">egf-master-v1.1.0</a>
      </td>
      <td style="text-align:left">egf-master:v1.1.0-9959f29</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">Finance Collection Voucher Consumer</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/business-services/tree/finance-collections-voucher-consumer-v1.1.0">finance-collections-voucher-consumer-v1.1.0</a>
      </td>
      <td style="text-align:left">finance-collections-voucher-consumer:v1.1.0-004e14a</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Municipal Services</b>  <a href="https://github.com/egovernments/municipal-services/releases/tag/v2.0"><b>v2.0</b></a>
      </td>
      <td style="text-align:left">Trade License</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/municipal-services/tree/tl-services-v1.1.0">tl-services-v1.1.0</a>
      </td>
      <td style="text-align:left">tl-services:v1.1.0-be11a0f5</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/egov-mdms-data/pull/1160">PR-1160</a>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">Trade License Calculator</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/municipal-services/tree/tl-calculator-v1.1.0">tl-calculator-v1.1.0</a>
      </td>
      <td style="text-align:left">tl-calculator:v1.1.0-c52ffe21</td>
      <td style="text-align:left">
        <p><a href="https://github.com/egovernments/egov-mdms-data/pull/1125">PR-1125</a>
        </p>
        <p><a href="https://github.com/egovernments/egov-mdms-data/pull/1133">PR-1133</a>
        </p>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">Fire NOC</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/municipal-services/tree/firenoc-services-v1.0.0">firenoc-services-v1.0.0</a>
      </td>
      <td style="text-align:left">firenoc-services:v1.0.0-4abf83d8</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">Fire NOC Calculator</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/municipal-services/tree/firenoc-calculator-v1.0.0">firenoc-calculator-v1.0.0</a>
      </td>
      <td style="text-align:left">firenoc-calculator:v1.0.0-ae96e930</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">Property Services</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/municipal-services/tree/property-services-v1.0.0">property-services-v1.0.0</a>
      </td>
      <td style="text-align:left">property-services:v1.0.0-ecf3410a</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">Property Tax Calculator</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/municipal-services/tree/pt-calculator-v2-v1.1.0">pt-calculator-v2-v1.1.0</a>
      </td>
      <td style="text-align:left">pt-calculator-v2:v1.1.0-63e20365</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">Property Tax</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/municipal-services/tree/pt-services-v2-v1.0.0">pt-services-v2-v1.0.0</a>
      </td>
      <td style="text-align:left">pt-services-v2:v1.0.0-ecf3410a</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">Water Charges</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/municipal-services/tree/ws-services-v1.0.0">ws-services-v1.0.0</a>
      </td>
      <td style="text-align:left">ws-services:v1.0.0-67c2139c</td>
      <td style="text-align:left">
        <p><a href="https://github.com/egovernments/egov-mdms-data/pull/1043">PR-1043</a>
        </p>
        <p><a href="https://github.com/egovernments/egov-mdms-data/pull/1058">PR-1058</a>
        </p>
      </td>
      <td style="text-align:left">
        <p><a href="https://github.com/egovernments/configs/pull/357">PR-357</a>
        </p>
        <p><a href="https://github.com/egovernments/configs/pull/340">PR-340</a>
        </p>
        <p><a href="https://github.com/egovernments/configs/commit/900e8e1c59ebc12f4bea49f52063f524aabf3830#diff-b5d08abcd9524da252a33fcff4c515f8">ws-bill.json</a>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">Water Charges Calculator</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/municipal-services/tree/ws-calculator-v1.0.0">ws-calculator-v1.0.0</a>
      </td>
      <td style="text-align:left">ws-calculator:v1.0.0-d7529cf4</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><a href="https://github.com/egovernments/configs/pull/342">PR-342</a>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">Sewerage Charges</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/municipal-services/tree/sw-services-v1.0.0">sw-services-v1.0.0</a>
      </td>
      <td style="text-align:left">sw-services:v1.0.0-a2ee0ed4</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><a href="https://github.com/egovernments/configs/commit/d213b8fbc71c8adc67df393b30c8be9ea923e24f#diff-cad1acac07cf6e6c1843536937285a4d">water-meter.yml</a>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">Sewerage Charges Calculator</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/municipal-services/tree/sw-calculator-v1.0.0">sw-calculator-v1.0.0</a>
      </td>
      <td style="text-align:left">sw-calculator:v1.0.0-67e5a1bc</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">BPA Calculator</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/municipal-services/tree/bpa-calculator-v1.0.0">bpa-calculator-v1.0.0</a>
      </td>
      <td style="text-align:left">bpa-calculator:v1.0.0-1aeb87df</td>
      <td style="text-align:left">
        <p><a href="https://github.com/egovernments/egov-mdms-data/pull/996/files">PR-996</a>
        </p>
        <p><a href="https://github.com/egovernments/egov-mdms-data/pull/995/files">PR-995</a>
        </p>
        <p><a href="https://github.com/egovernments/egov-mdms-data/pull/1162/files">PR-1162</a>
        </p>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">BPA Services</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/municipal-services/tree/bpa-services-v1.0.0">bpa-services-v1.0.0</a>
      </td>
      <td style="text-align:left">bpa-services:v1.0.0-b5520589</td>
      <td style="text-align:left">
        <p><a href="https://github.com/egovernments/egov-mdms-data/pull/1118/files">PR-1118</a>
        </p>
        <p><a href="https://github.com/egovernments/egov-mdms-data/pull/1062/files">PR-1062</a>
        </p>
        <p><a href="https://github.com/egovernments/egov-mdms-data/pull/1019/files">PR-1019</a>
        </p>
        <p><a href="https://github.com/egovernments/egov-mdms-data/pull/1016/files">PR-1016</a>
        </p>
        <p><a href="https://github.com/egovernments/egov-mdms-data/pull/1008/files">PR-1008</a>
        </p>
        <p><a href="https://github.com/egovernments/egov-mdms-data/pull/1007/files">PR-1007</a>
        </p>
        <p><a href="https://github.com/egovernments/egov-mdms-data/pull/1006">PR-1006</a>
        </p>
        <p><a href="https://github.com/egovernments/egov-mdms-data/pull/997">PR-997</a>
        </p>
      </td>
      <td style="text-align:left">
        <p><a href="https://github.com/egovernments/configs/commit/5682f1adb60b40663fe13d545e0c865ad4537b08">land-persister.yml</a>
        </p>
        <p><a href="https://github.com/egovernments/configs/commit/9ae764474a702249cd3aaefa806a3331a37e0364">bpa-persister.yml</a>
        </p>
        <p><a href="https://github.com/egovernments/configs/commit/47528052b4904ce5ab679324f13165458a83d05a">bpa-revocation.json</a>
        </p>
        <p><a href="https://github.com/egovernments/configs/commit/47528052b4904ce5ab679324f13165458a83d05a">buildingpermit-low.json</a>
        </p>
        <p><a href="https://github.com/egovernments/configs/commit/47528052b4904ce5ab679324f13165458a83d05a">buildingpermit.json</a>
        </p>
        <p><a href="https://github.com/egovernments/configs/commit/47528052b4904ce5ab679324f13165458a83d05a">occupancy-certificate.json</a>
        </p>
        <p><a href="https://github.com/egovernments/configs/commit/5f7eafdf3339d49a736d31c50037333a11c0f114">noc-persister.yml</a>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">User Event</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/municipal-services/tree/user-event-v1.1.0">user-event-v1.1.0</a>
      </td>
      <td style="text-align:left">egov-user-event:v1.1.0-e518861c</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">PGR</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/municipal-services/tree/rainmaker-pgr-v1.1.0">rainmaker-pgr-v1.1.0</a>
      </td>
      <td style="text-align:left">rainmaker-pgr:v1.1.0-5058d47e</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">Land Services</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/municipal-services/tree/land-services-v1.0.0">land-services-v1.0.0</a>
      </td>
      <td style="text-align:left">land-services:v1.0.0-ae5cee9f</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Utilities Services</b>  <a href="https://github.com/egovernments/utilities/tree/v2.0"><b>v2.0</b></a>
      </td>
      <td style="text-align:left">Custom Consumer</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/utilities/tree/custom-consumer-v1.1.0">custom-consumer-v1.1.0</a>
      </td>
      <td style="text-align:left">egov-custom-consumer:v1.1.0-7a6db73</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">PDF</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/utilities/tree/pdf-v1.1.0">pdf-v1.1.0</a>
      </td>
      <td style="text-align:left">egov-pdf:v1.0.0-009661c</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Others Service</b>  <a href="https://github.com/egovernments/eGov-dcr-service/releases/tag/v2.0"><b>v2.0</b></a>
      </td>
      <td style="text-align:left">eDCR</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/eGov-dcr-service/tree/egov-edcr-v1.0.0">egov-edcr-v1.0.0</a>
      </td>
      <td style="text-align:left">egov-edcr:v1.0.0-04ff1e5</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">Finance</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>InfraOps v2.0</b>
      </td>
      <td style="text-align:left">Prometheus</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><a href="http://quay.io/prometheus/prometheus:v2.15.2">quay.io/prometheus/prometheus:v2.15.2</a>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">Prometheus Operator</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><a href="http://quay.io/coreos/prometheus-operator:v0.37.0">quay.io/coreos/prometheus-operator:v0.37.0</a>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">Kubestate metrics</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><a href="http://quay.io/coreos/kube-state-metrics:v1.9.7">quay.io/coreos/kube-state-metrics:v1.9.7</a>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">Kuberhealthy</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">Grafana</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">grafana/grafana:7.0.5</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">Alert manager</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><a href="http://quay.io/prometheus/alertmanager:v0.20.0">quay.io/prometheus/alertmanager:v0.20.0</a>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">Minio</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">PG Admin</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">Spot Instance Terminator</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">kubeaws/kube-spot-termination-notice-handler:1.13.7-1</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">OAuth for Kibana, Jaeger</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">Digit-Jenkins-as-service</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">DIGIT-CI/CD-as-service</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>

## Deprecated Features

* egov-data-uploader
* egov-common-masters
* egov-index-custom-consumer

