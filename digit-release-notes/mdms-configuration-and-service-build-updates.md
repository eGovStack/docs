---
description: Configuration changes and service build details
---

# MDMS Configuration & Service Build Updates

### MDMS Changes <a id="MDMS-changes"></a>

<table>
  <thead>
    <tr>
      <th style="text-align:left"><b>Feature</b>
      </th>
      <th style="text-align:left"><b>Service Name</b>
      </th>
      <th style="text-align:left"><b>Changes</b>
      </th>
      <th style="text-align:left"><b>Description</b>
      </th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Financial Year 21-22 Addition</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">
        <p><a href="https://github.com/egovernments/egov-mdms-data/pull/1771">1771</a>
        </p>
        <p><a href="https://github.com/egovernments/egov-mdms-data/pull/1772">1772</a>
        </p>
        <p><a href="https://github.com/egovernments/egov-mdms-data/pull/1859">1859</a>
        </p>
        <p><a href="https://github.com/egovernments/egov-mdms-data/pull/1778">1778</a>
        </p>
      </td>
      <td style="text-align:left">
        <ul>
          <li>Updated Financial year for 2021-22 for WS</li>
          <li>Updated Tax Period for 2021-22 for WS</li>
          <li>Added 21-22 Financial year for PT,TL,UC,W&amp;S,FN</li>
          <li>Added 2021-2022 financial year for PT</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Digit 2.4 Common Changes
        <br />(eChallan,PT)</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">
        <p><a href="https://github.com/egovernments/egov-mdms-data/pull/1801">1801</a>
        </p>
        <p><a href="https://github.com/egovernments/egov-mdms-data/pull/1859">1859</a>
        </p>
        <p><a href="https://github.com/egovernments/egov-mdms-data/pull/1860">1860</a>
        </p>
        <p><a href="https://github.com/egovernments/egov-mdms-data/pull/1861">1861</a>
        </p>
        <p><a href="https://github.com/egovernments/egov-mdms-data/pull/1800">1800</a>
        </p>
        <p><a href="https://github.com/egovernments/egov-mdms-data/pull/1802">1802</a>
        </p>
        <p><a href="https://github.com/egovernments/egov-mdms-data/pull/1769">1769</a>
        </p>
        <p><a href="https://github.com/egovernments/egov-mdms-data/pull/1777">1777</a>
        </p>
        <p><a href="https://github.com/egovernments/egov-mdms-data/pull/1779">1779</a>
        </p>
        <p><a href="https://github.com/egovernments/egov-mdms-data/pull/1886">1886</a>
        </p>
        <p><a href="https://github.com/egovernments/egov-mdms-data/pull/1891">1891</a>
        </p>
      </td>
      <td style="text-align:left">
        <ul>
          <li>eChallan Role Action Mapping</li>
          <li>eChallan Common Pay Changes,Updated pt Tax Head Order, Updated create
            complaint action to CSR.</li>
          <li>Added mdms for payment gateway,Updated the Bill genie url for echallan,Added
            quickpay in cityModule.json,Added tl billing slab search access,Updated
            action and roles for pdf download,PT edit action in case of citizen action
            pending,Updated Billing service for few Services,Updated Tax Period for
            few service types,Removed user search access from Employee,Updated Id Format.json,Updated
            display name for mcollect,Updated Actions , Role Actions for receipt download.</li>
          <li>PGR Role Action Updation,Mutation receipt download access added to PT
            cemp and citizen,Added entry for PT locality search url,Added TL receipt
            download action to citizen and counter emp,Added help text for PT,PT Documents
            required updated,Disabled arrears for PT Mutation,PT added a default map
            config,Added PDF module for All,Updated role action for payment receipt
            download.</li>
          <li>Added firenoc receipt access</li>
          <li>Added business service search access</li>
          <li>Added Changes for payment gateway</li>
          <li>Added mutation tax period for 21-22</li>
          <li>Business service search access added</li>
          <li>Added 2021-2022 financial year for PT</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">BPA</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">
        <p><a href="https://github.com/egovernments/egov-mdms-data/pull/1781">1781</a>
        </p>
        <p><a href="https://github.com/egovernments/egov-mdms-data/pull/1783">1783</a>
        </p>
        <p><a href="https://github.com/egovernments/egov-mdms-data/pull/1675">1675</a>
        </p>
        <p><a href="https://github.com/egovernments/egov-mdms-data/pull/1676">1676</a>
        </p>
      </td>
      <td style="text-align:left">
        <ul>
          <li>Updated Action for EDCR.</li>
          <li>Updated the Roles For EDCR</li>
          <li>Updated role action mapping for noc and TL users</li>
          <li>Added noc searcher access to BPA users</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">TL</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><a href="https://github.com/egovernments/egov-mdms-data/pull/1773">1773</a>
      </td>
      <td style="text-align:left">
        <ul>
          <li>Updated Trade license document object</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">FSM</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><a href="https://github.com/egovernments/egov-mdms-data/pull/1799">1799</a>
      </td>
      <td style="text-align:left">
        <ul>
          <li>Updated FSM Common fields deatils</li>
        </ul>
      </td>
    </tr>
  </tbody>
</table>

### Config Changes   <a id="Config-Changes"></a>

<table>
  <thead>
    <tr>
      <th style="text-align:left"><b>Module</b>
      </th>
      <th style="text-align:left"><b>Action</b>
      </th>
      <th style="text-align:left"><b>PR</b>
      </th>
      <th style="text-align:left"><b>Description</b>
      </th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Digit 2.4 Common Changes</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">
        <p><a href="https://github.com/egovernments/configs/pull/860">860</a>
        </p>
        <p><a href="https://github.com/egovernments/configs/pull/900">900</a>
        </p>
        <p><a href="https://github.com/egovernments/configs/pull/895">895</a>
        </p>
        <p><a href="https://github.com/egovernments/configs/pull/888">888</a>
        </p>
      </td>
      <td style="text-align:left">
        <p>Changes in :</p>
        <ul>
          <li>Updated changes in billgenie for w&amp;s,pt,Updated localitySearcher.yml
            for property-services,Updated format config for mCollect,Updated data config
            for mcollect,Added comma&apos;s in address field in challan PDF,Corrected
            localisation details for address,Fixed WS total connections chart config,Added
            persister file, pdf changes and report changes for eChallan,Added road
            Cutting Info details in water and sewerage yml file,FSM receipt.</li>
          <li>Updated module name for mcollectbill</li>
          <li>Updated Bill genie search by propertyid</li>
          <li>Updated Module Name in data config for mcollectbill.json</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">egov-persister</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">
        <p><a href="https://github.com/egovernments/configs/pull/738">738</a>
        </p>
        <p><a href="https://github.com/egovernments/configs/pull/924">924</a>
        </p>
      </td>
      <td style="text-align:left">
        <ul>
          <li>Added #10 and #45 for rating</li>
          <li>For auto populating provisional firenoc details while creating New application</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">egov-dss-Dashboard</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">
        <p><a href="https://github.com/egovernments/configs/pull/786">786</a>
        </p>
        <p><a href="https://github.com/egovernments/configs/pull/789">789</a>
        </p>
      </td>
      <td style="text-align:left">
        <ul>
          <li>Fixed WS total connections chart config</li>
          <li>Updated DSS config changes for WS</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Report - HRMS and PGR Reports</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><a href="https://github.com/egovernments/configs/pull/829">829</a>
      </td>
      <td style="text-align:left">
        <ul>
          <li>Fixes GRO and LME name not being shown in pgr-reports.</li>
          <li>Updated Employee Reports</li>
        </ul>
      </td>
    </tr>
  </tbody>
</table>

### Infra Changes <a id="Infra-Change"></a>

<table>
  <thead>
    <tr>
      <th style="text-align:left"><b>Feature</b>
      </th>
      <th style="text-align:left"><b>Feature</b>
      </th>
      <th style="text-align:left"><b>Description</b>
      </th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Digit 2.4 Common Changes</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/DIGIT-DevOps/pull/84">84</a>
      </td>
      <td style="text-align:left">
        <ul>
          <li>Added eChallan services configs</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">WS Service</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/DIGIT-DevOps/pull/16">16</a>
      </td>
      <td style="text-align:left">
        <ul>
          <li>Added is-external-workflow-enabled for WS service</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Public Domain Search</td>
      <td style="text-align:left">
        <p><a href="https://github.com/egovernments/DIGIT-DevOps/pull/100/commits/4e50248928b2d020cb4721dc440ba0b87c186969">100</a>
        </p>
        <p><a href="https://github.com/egovernments/DIGIT-DevOps/pull/99">99</a>
        </p>
      </td>
      <td style="text-align:left">
        <ul>
          <li>Added consolidated receipt link in mixed</li>
        </ul>
      </td>
    </tr>
  </tbody>
</table>

### Service Build Updates

| Category | Services | GIT TAGS | Docker Artifact ID | **Remarks** |
| :--- | :--- | :--- | :--- | :--- |
| **Frontend** [**v2.4**](https://github.com/egovernments/frontend/releases/tag/v2.4) | Citizen | [citizen-v1.5.0](https://github.com/egovernments/frontend/releases/tag/citizen-v1.5.0) | citizen:v1.5.0-c1825dd69-291 |   |
|   | Employee | [employee-v1.5.0](https://github.com/egovernments/frontend/releases/tag/employee-v1.5.0) | employee:v1.5.0-c1825dd69-292 |   |
|   | DSS Dashboard | [dashboard-v1.5.0](https://github.com/egovernments/frontend/releases/tag/dashboard-v1.5.0) | dss-dashboard:v1.5.0-7e9587a65-13 |   |
|  **DIGIT UI** | DIGIT UI | [digit-ui-v1.2](https://github.com/egovernments/digit-ui/releases/tag/digit-ui-v1.2), [digit-ui-v1.2.0](https://github.com/egovernments/digit-ui-internals/releases/tag/digit-ui-v1.2.0) | digit-ui:v1.2.0-4016cc5-233 |   |
| **Core Services** [**v2.4**](https://github.com/egovernments/core-services/releases/tag/v2.4) | Encryption | [enc-service-v1.1.1](https://github.com/egovernments/core-services/releases/tag/enc-service-v1.1.1) | egov-enc-service:v1.1.1-19a3ba19-5 | No changes in the current release. |
|   | xState Chatbot | [xstate-chatbot-v1.0.1](https://github.com/egovernments/core-services/releases/tag/xstate-chatbot-v1.0.1) | xstate-chatbot:v1.0.1-2ee9ec37-19 | New Service |
|   | Searcher | [searcher-v1.1.3](https://github.com/egovernments/core-services/releases/tag/searcher-v1.1.3) | egov-searcher:v1.1.3-2ee9ec37-2 |   |
|   | Payment Gateway | [pg-service-v1.2.2](https://github.com/egovernments/core-services/releases/tag/pg-service-v1.2.2) | egov-pg-service:v1.2.2-2ee9ec37-17 |   |
|   | Filestore | [filestore-v1.2.3](https://github.com/egovernments/core-services/releases/tag/filestore-v1.2.3) | egov-filestore:v1.2.3-2ee9ec37-4 |   |
|   | Zuul - API Gateway | [zuul-v1.3.0](https://github.com/egovernments/core-services/releases/tag/zuul-v1.3.0) | zuul:v1.3.0-667cb3d3-8 |   |
|   | Mail Notification | [notification-mail-v1.1.1](https://github.com/egovernments/core-services/releases/tag/notification-mail-v1.1.1) | egov-notification-mail:v1.1.1-19a3ba19-5 | No changes in the current release. |
|   | SMS Notification | [notification-sms-v1.1.2](https://github.com/egovernments/core-services/releases/tag/notification-sms-v1.1.2) | egov-notification-sms:v1.1.2-2ee9ec37-3 |    |
|   | Localization | [localization-v1.1.2](https://github.com/egovernments/core-services/releases/tag/localization-v1.1.2) | egov-localization:v1.1.2-2ee9ec37-2 |   |
|   | Persist | [persister-v1.1.3](https://github.com/egovernments/core-services/releases/tag/persister-v1.1.3) | egov-persister:v1.1.3-2ee9ec37-2 |   |
|   | ID Gen | [idgen-v1.2.2](https://github.com/egovernments/core-services/releases/tag/idgen-v1.2.2) | egov-idgen:v1.2.2-2ee9ec37-3 |   |
|   | User | [user-v1.2.4](https://github.com/egovernments/core-services/releases/tag/user-v1.2.4) | egov-user:v1.2.4-d1d62cdf-11 |   |
|   | User Chatbot | [user-chatbot-v1.2.1](https://github.com/egovernments/core-services/releases/tag/user-chatbot-v1.2.1) | egov-user-chatbot:v1.2.1-4976757 | No changes in the current release. |
|   | MDMS | [mdms-service-v1.3.1](https://github.com/egovernments/core-services/releases/tag/mdms-service-v1.3.1) | egov-mdms-service:v1.3.1-2ee9ec37-3 |   |
|   | URL Shortening | [url-shortening-v1.1.0](https://github.com/egovernments/core-services/releases/tag/url-shortening-v1.1.0) | egov-url-shortening:v1.1.0-19a3ba19-1 | No changes in the current release. |
|   | Indexer | [indexer-v1.1.4](https://github.com/egovernments/core-services/releases/tag/indexer-v1.1.4) | egov-indexer:v1.1.4-2ee9ec37-3 |   |
|   | Report | [report-v1.3.2](https://github.com/egovernments/core-services/releases/tag/report-v1.3.2) | report:v1.3.2-07a30430-5 |   |
|   | Workflow | [workflow-v2-v1.1.5](https://github.com/egovernments/core-services/releases/tag/workflow-v2-v1.1.5) | egov-workflow-v2:v1.1.5-2ee9ec37-9 |   |
|   | PDF Generator | [pdf-service-v1.1.4](https://github.com/egovernments/core-services/releases/tag/pdf-service-v1.1.4) | pdf-service:v1.1.4-a4e9bb2c-6 |   |
|   | Chatbot | [chatbot-v1.1.4](https://github.com/egovernments/core-services/releases/tag/chatbot-v1.1.4) | chatbot:v1.1.4-2ee9ec37-7 |   |
|   | Access Control | [accesscontrol-v1.1.2](https://github.com/egovernments/core-services/releases/tag/accesscontrol-v1.1.2) | egov-accesscontrol:v1.1.2-2ee9ec37-1 |   |
|   | Location | [location-v1.1.3](https://github.com/egovernments/core-services/releases/tag/location-v1.1.3) | egov-location:v1.1.3-2ee9ec37-1 |   |
|   | OTP | [otp-v1.2.1](https://github.com/egovernments/core-services/releases/tag/otp-v1.2.1) | egov-otp:v1.2.1-07a30430-2 |   |
|   | User OTP | [user-otp-v1.1.3](https://github.com/egovernments/core-services/releases/tag/user-otp-v1.1.3) | user-otp:v1.1.3-2ee9ec37-6 |   |
| **Business Services** [**v2.4**](https://github.com/egovernments/business-services/releases/tag/v2.4) | Apportion | [apportion-service-v1.1.4](https://github.com/egovernments/business-services/releases/tag/apportion-service-v1.1.4) | apportion-service:v1.1.4-ec514d1-12 | No changes in the current release. |
|   | Collection | [collection-services-v1.1.4](https://github.com/egovernments/business-services/releases/tag/collection-services-v1.1.4) | collection-services:v1.1.4-c3cba4b-15 |   |
|   | Billing | [billing-service-v1.3.2](https://github.com/egovernments/business-services/releases/tag/billing-service-v1.3.2) | billing-service:v1.3.2-7dfa157-22 |   |
|   | HRMS | [hrms-v1.2.2](https://github.com/egovernments/business-services/releases/tag/hrms-v1.2.2) | egov-hrms:v1.2.2-57f79eb-1 |   |
|   | Dashboard Analytics | [dashboard-analytics-v1.1.4](https://github.com/egovernments/business-services/releases/tag/dashboard-analytics-v1.1.4) | dashboard-analytics:v1.1.4-97898f7-1 |   |
|   | Dashboard Ingest | [dashboard-ingest-v1.1.3](https://github.com/egovernments/business-services/releases/tag/dashboard-ingest-v1.1.3) | dashboard-ingest:v1.1.3-6cb5d67-5 |   |
|   | EGF Instrument | [egf-instrument-v1.1.3](https://github.com/egovernments/business-services/releases/tag/egf-instrument-v1.1.3) | egf-instrument:v1.1.3-b5944f0-1 |   |
|   | EGF Master | [egf-master-v1.1.2](https://github.com/egovernments/business-services/releases/tag/egf-master-v1.1.2) | egf-master:v1.1.2-b5944f0-2 |   |
|   | Finance Collection Voucher Consumer | [finance-collections-voucher-consumer-v1.1.4](https://github.com/egovernments/business-services/releases/tag/finance-collections-voucher-consumer-v1.1.4) | finance-collections-voucher-consumer:v1.1.4-665e9d7-8 |   |
| **Municipal Services** [**v2.4**](https://github.com/egovernments/municipal-services/releases/tag/v2.4) | Trade License | [tl-services-v1.1.4](https://github.com/egovernments/municipal-services/releases/tag/tl-services-v1.1.4) | tl-services:v1.1.4-a8da9ece-6 |   |
|   | Trade License Calculator | [tl-calculator-v1.1.3](https://github.com/egovernments/municipal-services/releases/tag/tl-calculator-v1.1.3) | tl-calculator:v1.1.3-0b2efd7f-3 |   |
|   | Fire NOC | [firenoc-services-v1.3.0](https://github.com/egovernments/municipal-services/releases/tag/firenoc-services-v1.3.0) | firenoc-services:v1.3.0-090c647b-26 |   |
|   | Fire NOC Calculator | [firenoc-calculator-v1.2.0](https://github.com/egovernments/municipal-services/releases/tag/firenoc-calculator-v1.2.0) | firenoc-calculator:v1.2.0-a8da9ece-3 |  |
|   | Property Services | [property-services-v1.1.5](https://github.com/egovernments/municipal-services/releases/tag/property-services-v1.1.5) | property-services:v1.1.5-a8da9ece-26 |   |
|   | Property Tax Calculator | [pt-calculator-v2-v1.1.4](https://github.com/egovernments/municipal-services/releases/tag/pt-calculator-v2-v1.1.4) | pt-calculator-v2:v1.1.4-ef94c644-20 |   |
|   | Property Tax | [pt-services-v2-v1.0.0](https://github.com/egovernments/municipal-services/releases/tag/pt-services-v2-v1.0.0) | pt-services-v2:v1.0.0-ecf3410a | Deprecated. No changes in the current release. |
|   | Water Charges | [ws-services-v1.4.0](https://github.com/egovernments/municipal-services/releases/tag/ws-services-v1.4.0) | ws-services:v1.4.0-a8da9ece-9 |   |
|   | Water Charges Calculator | [ws-calculator-v1.3.1](https://github.com/egovernments/municipal-services/releases/tag/ws-calculator-v1.3.1) | ws-calculator:v1.3.1-a8da9ece-41 |   |
|   | Sewerage Charges | [sw-services-v1.4.0](https://github.com/egovernments/municipal-services/releases/tag/sw-services-v1.4.0) | sw-services:v1.4.0-a8da9ece-8 |   |
|   | Sewerage Charges Calculator | [sw-calculator-v1.3.1](https://github.com/egovernments/municipal-services/releases/tag/sw-calculator-v1.3.1) | sw-calculator:v1.3.1-a8da9ece-32 |   |
|   | BPA Calculator | [bpa-calculator-v1.1.0](https://github.com/egovernments/municipal-services/releases/tag/bpa-calculator-v1.1.0) | bpa-calculator:v1.1.0-4ee62c15-1 |  No changes in the current release. |
|   | BPA Services | [bpa-services-v1.1.3](https://github.com/egovernments/municipal-services/releases/tag/bpa-services-v1.1.3) | bpa-services:v1.1.3-2e687e00-7 |   |
|   | User Event | [user-event-v1.1.3](https://github.com/egovernments/municipal-services/releases/tag/user-event-v1.1.3) | egov-user-event:v1.1.3-a8da9ece-3 |   |
|   | PGR | [rainmaker-pgr-v1.1.3](https://github.com/egovernments/municipal-services/releases/tag/rainmaker-pgr-v1.1.3) | rainmaker-pgr:v1.1.3-22e87ed4-38 |  v1 |
|   | PGR Service | [pgr-services-v1.1.2](https://github.com/egovernments/municipal-services/releases/tag/pgr-services-v1.1.2) | pgr-services:v1.1.2-a8da9ece-4 |  v2 |
|   | Land Services | [land-services-v1.0.2](https://github.com/egovernments/municipal-services/releases/tag/land-services-v1.0.2) | land-services:v1.0.2-a8da9ece-2 |   |
|   | NOC Services | [noc-services-v1.0.2](https://github.com/egovernments/municipal-services/releases/tag/noc-services-v1.0.2) | noc-services:v1.0.2-a8da9ece-1 |   |
|   | FSM | [fsm-v1.0.1](https://github.com/egovernments/municipal-services/releases/tag/fsm-v1.0.1) | fsm:v1.0.1-28439fcd-10 |   |
|   | FSM Calculator | [fsm-calculator-v1.0.0](https://github.com/egovernments/municipal-services/releases/tag/fsm-calculator-v1.0.0) | fsm-calculator:v1.0.0-39678039-14 | No changes in the current release. |
|   | Vehicle | [vehicle-v1.0.1](https://github.com/egovernments/municipal-services/releases/tag/vehicle-v1.0.1) | vehicle:v1.0.1-a8da9ece-6 |   |
|   | Vendor | [vendor-v1.0.1](https://github.com/egovernments/municipal-services/releases/tag/vendor-v1.0.1) | vendor:v1.0.1-a8da9ece-6 |   |
|   | eChallan Services | [echallan-services-v1.0.1](https://github.com/egovernments/municipal-services/releases/tag/echallan-services-v1.0.1) | echallan-services:v1.0.1-a8da9ece-14 | New Service |
|   | eChallan Calculator | [echallan-calculator-v1.0.0](https://github.com/egovernments/municipal-services/releases/tag/echallan-calculator-v1.0.0) | echallan-calculator:v1.0.0-a8da9ece-2 | New Service |
| **Utilities Services** [**v2.4**](https://github.com/egovernments/utilities/releases/tag/v2.4) | Custom Consumer | [custom-consumer-v1.1.0](https://github.com/egovernments/utilities/releases/tag/custom-consumer-v1.1.0) | egov-custom-consumer:v1.1.0-7a6db73 | No changes in the current release. |
|   | PDF | [pdf-v1.1.0-2](https://github.com/egovernments/utilities/releases/tag/pdf-v1.1.0-2) | egov-pdf:v1.1.0-12bed31-9 |   |
| **Others Service** | eDCR | [egov-edcr-v1.2.0](https://github.com/egovernments/eGov-dcr-service/releases/tag/egov-edcr-v1.2.0) | egov-edcr:v1.2.0-cb71c93-10 |   |
|   | Finance | [egov-coexistence-v3.0.1](https://github.com/egovernments/egov-coexistence/releases/tag/egov-coexistence-v3.0.1) |  egov-finance:v3.0.1-0da425612c-25 |   |
| **Configs** [**v2.4**](https://github.com/egovernments/configs/releases/tag/v2.4) |   |   |   |   |
|  **MDMS** [**v2.4**](https://github.com/egovernments/egov-mdms-data/releases/tag/v2.4) |   |   |   |   |
|  **Localization** [**v2.4**](https://github.com/egovernments/releasekit/releases/tag/v2.4) |   |   |   |   |
| **QA Automation** [**v2.4** ](https://github.com/egovernments/test-automation/releases/tag/v2.4) |   |   |   |   |







> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_ ](https://egov.org.in/)_is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._

