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
      <td style="text-align:left">Common</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><a href="https://github.com/egovernments/egov-mdms-data/pull/2004">#2004</a>
      </td>
      <td style="text-align:left">
        <ul>
          <li>Digit 2.5 common changes</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Digit Employee Inbox</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><a href="https://github.com/egovernments/egov-mdms-data/pull/2006">#2006</a>,
        <a
        href="https://github.com/egovernments/egov-mdms-data/pull/2022">#2022</a>
      </td>
      <td style="text-align:left">
        <ul>
          <li>Employee navigation to Digit UI</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Role Action</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><a href="https://github.com/egovernments/egov-mdms-data/pull/2007">#2007</a>,
        <a
        href="https://github.com/egovernments/egov-mdms-data/pull/2010">#2010</a>, <a href="https://github.com/egovernments/egov-mdms-data/pull/2011">#2011</a>,
          <a
          href="https://github.com/egovernments/egov-mdms-data/pull/2014">#2014</a>, <a href="https://github.com/egovernments/egov-mdms-data/pull/2019">#2019</a>,
            <a
            href="https://github.com/egovernments/egov-mdms-data/pull/2025">#2025</a>
      </td>
      <td style="text-align:left">
        <ul>
          <li>FSM inbox correction</li>
          <li>Updated role action mapping</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Property Tax</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><a href="https://github.com/egovernments/egov-mdms-data/pull/2008">#2008</a>
      </td>
      <td style="text-align:left">
        <ul>
          <li>Updated documents for PT create and mutation flow</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Auto Escalation</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><a href="https://github.com/egovernments/egov-mdms-data/pull/2013">#2013</a>,
        <a
        href="https://github.com/egovernments/egov-mdms-data/pull/2017">#2017</a>
      </td>
      <td style="text-align:left">
        <ul>
          <li>Auto Escalation specific changes</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">FSM-DSS</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><a href="https://github.com/egovernments/egov-mdms-data/pull/2015">#2015</a>,
        <a
        href="https://github.com/egovernments/egov-mdms-data/pull/2016">#2016</a>, <a href="https://github.com/egovernments/egov-mdms-data/pull/2020">#2020</a>
      </td>
      <td style="text-align:left">
        <ul>
          <li>Added districtTenantCode for each city</li>
          <li>Added fsm &amp; ulb-fsm in uiCommonConstants</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Product Ontology</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><a href="https://github.com/egovernments/egov-mdms-data/pull/2023">#2023</a>,
        <a
        href="https://github.com/egovernments/egov-mdms-data/pull/2032">#2032</a>, <a href="https://github.com/egovernments/egov-mdms-data/pull/2033">#2033</a>
      </td>
      <td style="text-align:left">
        <ul>
          <li>Product Ontology Changes</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">NLP chatbot</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><a href="https://github.com/egovernments/egov-mdms-data/pull/2028">#2028</a>
      </td>
      <td style="text-align:left">
        <ul>
          <li>NLP chatbot specific changes</li>
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
      <td style="text-align:left">Common</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><a href="https://github.com/egovernments/configs/pull/1043">#1043</a>,
        <a
        href="https://github.com/egovernments/configs/pull/1044">#1044</a>, <a href="https://github.com/egovernments/configs/pull/1081">#1081</a>
      </td>
      <td style="text-align:left">
        <ul>
          <li>Digit 2.5 common changes</li>
          <li>Indentation correction for Indexer</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">FSM-DSS and FSM Reports</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><a href="https://github.com/egovernments/configs/pull/1046">#1046</a>,
        <a
        href="https://github.com/egovernments/configs/pull/1047">#1047</a>, <a href="https://github.com/egovernments/configs/pull/1048">#1048</a>,
          <a
          href="https://github.com/egovernments/configs/pull/1049">#1049</a>, <a href="https://github.com/egovernments/configs/pull/1087">#1087</a>
      </td>
      <td style="text-align:left">
        <ul>
          <li>Updated Mater Dashboard config for FSM DSS</li>
          <li>Added FSM DSS configurations</li>
          <li>Updated Chart Api changes for fsm dss</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Inbox API</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><a href="https://github.com/egovernments/configs/pull/1054">#1054</a>,
        <a
        href="https://github.com/egovernments/configs/pull/1057">#1057</a>, <a href="https://github.com/egovernments/configs/pull/1068">#1068</a>,
          <a
          href="https://github.com/egovernments/configs/pull/1070">#1070</a>, <a href="https://github.com/egovernments/configs/pull/1071">#1071</a>,
            <a
            href="https://github.com/egovernments/configs/pull/1072">#1072</a>, <a href="https://github.com/egovernments/configs/pull/1073">#1073</a>,
              <a
              href="https://github.com/egovernments/configs/pull/1075">#1075</a>, <a href="https://github.com/egovernments/configs/pull/1077">#1077</a>
      </td>
      <td style="text-align:left">
        <ul>
          <li>Added Inbox searcher config for TL</li>
          <li>Updated searcher config for sorting application</li>
          <li>Added config for count TL search,</li>
          <li>Provided custom sorting for PT inbox</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">PT Reports</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><a href="https://github.com/egovernments/configs/pull/1058">#1058</a>,
        <a
        href="https://github.com/egovernments/configs/pull/1069">#1069</a>
      </td>
      <td style="text-align:left">
        <ul>
          <li>Removed duplicate records for PT reports</li>
          <li>Corrected duplicate owner issue</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">PDF</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><a href="https://github.com/egovernments/configs/pull/1082">#1082</a>,
        <a
        href="https://github.com/egovernments/configs/pull/1085">#1085</a>, <a href="https://github.com/egovernments/configs/pull/1088">#1088</a>
      </td>
      <td style="text-align:left">
        <ul>
          <li>Changes for localization for Receipt Cancellation</li>
          <li>Changes for mcollect challan for Hindi localization</li>
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
      <td style="text-align:left">Common</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/DIGIT-DevOps/pull/236">#236</a>,
        <a
        href="https://github.com/egovernments/DIGIT-DevOps/pull/237">#237</a>, <a href="https://github.com/egovernments/DIGIT-DevOps/pull/239">#239</a>
      </td>
      <td style="text-align:left">
        <ul>
          <li>Digit 2.5 common changes</li>
          <li>Corrected the indentation for Inbox</li>
          <li>State level tenant ID for workflow v2</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Open Payment (PT &amp; WS)</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/DIGIT-DevOps/pull/243">#243</a>
      </td>
      <td style="text-align:left">
        <ul>
          <li>Added mixed end point for PT and WS</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">TL Searcher</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/DIGIT-DevOps/pull/245">#245</a>
      </td>
      <td style="text-align:left">
        <ul>
          <li>Added searcher for Inbox TL</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">nlp-engine</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/DIGIT-DevOps/pull/253">#253</a>
      </td>
      <td style="text-align:left">
        <ul>
          <li>Added NLP specific changes</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">turn-io-adapter</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/DIGIT-DevOps/pull/254">#254</a>,
        <a
        href="https://github.com/egovernments/DIGIT-DevOps/pull/263">#263</a>
      </td>
      <td style="text-align:left">
        <ul>
          <li>Changes for turn-IO adapter</li>
        </ul>
      </td>
    </tr>
  </tbody>
</table>

### Service Build Updates

<table>
  <thead>
    <tr>
      <th style="text-align:left">Category</th>
      <th style="text-align:left">Services</th>
      <th style="text-align:left">GIT TAGS</th>
      <th style="text-align:left">Docker Artifact ID</th>
      <th style="text-align:left"><b>Remarks</b>
      </th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><b>Frontend</b>  <a href="https://github.com/egovernments/frontend/releases/tag/v2.5"><b>v2.5</b></a>
      </td>
      <td style="text-align:left">Citizen</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/frontend/releases/tag/citizen-v1.6.0">citizen-v1.6.0</a>
      </td>
      <td style="text-align:left">citizen:v1.6.0-f2e14587d-616</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">Employee</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/frontend/releases/tag/employee-v1.6.0">employee-v1.6.0</a>
      </td>
      <td style="text-align:left">employee:v1.6.0-f2e14587d-618</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">DSS Dashboard</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/frontend/releases/tag/dashboard-v1.6.0">dashboard-v1.6.0</a>
      </td>
      <td style="text-align:left">dss-dashboard:v1.6.0-520453001-21</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Digit-UI</b>  <a href="https://github.com/egovernments/digit-ui/releases/tag/v2.5"><b>v2.5</b></a>  <b>Digit-UI-Internals</b> 
        <a
        href="https://github.com/egovernments/digit-ui-internals/releases/tag/v2.5"><b>v2.5</b>
          </a>
      </td>
      <td style="text-align:left">DIGIT UI</td>
      <td style="text-align:left">
        <p><a href="https://github.com/egovernments/digit-ui/releases/tag/digit-ui-v1.3.0">digit-ui-v1.3.0</a>
        </p>
        <p><a href="https://github.com/egovernments/digit-ui-internals/releases/tag/digit-ui-v1.3.0">digit-ui-internals-v1.3.0</a>
        </p>
      </td>
      <td style="text-align:left">digit-ui:v1.3.0-e03ec9d-664</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Core Services</b>  <a href="https://github.com/egovernments/core-services/releases/tag/v2.5"><b>v2.5</b></a>
      </td>
      <td style="text-align:left">Encryption</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/core-services/releases/tag/enc-service-v1.1.1">enc-service-v1.1.1</a>
      </td>
      <td style="text-align:left">egov-enc-service:v1.1.1-19a3ba19-5</td>
      <td style="text-align:left">No changes in the current release.</td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">xState Chatbot</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/core-services/releases/tag/xstate-chatbot-v1.0.2">xstate-chatbot-v1.0.2</a>
      </td>
      <td style="text-align:left">xstate-chatbot:v1.0.2-196178f4-190</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">Searcher</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/core-services/releases/tag/searcher-v1.1.4">searcher-v1.1.4</a>
      </td>
      <td style="text-align:left">egov-searcher:v1.1.4-196178f4-7</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">Payment Gateway</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/core-services/releases/tag/pg-service-v1.2.2">pg-service-v1.2.2</a>
      </td>
      <td style="text-align:left">egov-pg-service:v1.2.2-2ee9ec37-17</td>
      <td style="text-align:left">No changes in the current release.</td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">Filestore</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/core-services/releases/tag/filestore-v1.2.3">filestore-v1.2.3</a>
      </td>
      <td style="text-align:left">egov-filestore:v1.2.3-2ee9ec37-4</td>
      <td style="text-align:left">No changes in the current release.</td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">Zuul - API Gateway</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/core-services/releases/tag/zuul-v1.3.0">zuul-v1.3.0</a>
      </td>
      <td style="text-align:left">zuul:v1.3.0-667cb3d3-8</td>
      <td style="text-align:left">No changes in the current release.</td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">Mail Notification</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/core-services/releases/tag/notification-mail-v1.1.1">notification-mail-v1.1.1</a>
      </td>
      <td style="text-align:left">egov-notification-mail:v1.1.1-19a3ba19-5</td>
      <td style="text-align:left">No changes in the current release.</td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">SMS Notification</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/core-services/releases/tag/notification-sms-v1.1.2">notification-sms-v1.1.2</a>
      </td>
      <td style="text-align:left">egov-notification-sms:v1.1.2-2ee9ec37-3</td>
      <td style="text-align:left">No changes in the current release.</td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">Localization</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/core-services/releases/tag/localization-v1.1.2">localization-v1.1.2</a>
      </td>
      <td style="text-align:left">egov-localization:v1.1.2-4517fb39-3</td>
      <td style="text-align:left">No changes in the current release.</td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">Persist</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/core-services/releases/tag/persister-v1.1.3">persister-v1.1.3</a>
      </td>
      <td style="text-align:left">egov-persister:v1.1.3-2ee9ec37-2</td>
      <td style="text-align:left">No changes in the current release.</td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">ID Gen</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/core-services/releases/tag/idgen-v1.2.2">idgen-v1.2.2</a>
      </td>
      <td style="text-align:left">egov-idgen:v1.2.2-2ee9ec37-3</td>
      <td style="text-align:left">No changes in the current release.</td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">User</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/core-services/releases/tag/user-v1.2.5">user-v1.2.5</a>
      </td>
      <td style="text-align:left">egov-user:v1.2.5-196178f4-28</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">User Chatbot</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/core-services/releases/tag/user-chatbot-v1.2.1">user-chatbot-v1.2.1</a>
      </td>
      <td style="text-align:left">egov-user-chatbot:v1.2.1-4976757</td>
      <td style="text-align:left">No changes in the current release.</td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">MDMS</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/core-services/releases/tag/mdms-service-v1.3.1">mdms-service-v1.3.1</a>
      </td>
      <td style="text-align:left">egov-mdms-service:v1.3.1-2ee9ec37-3</td>
      <td style="text-align:left">No changes in the current release.</td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">URL Shortening</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/core-services/releases/tag/url-shortening-v1.1.0">url-shortening-v1.1.0</a>
      </td>
      <td style="text-align:left">egov-url-shortening:v1.1.0-19a3ba19-1</td>
      <td style="text-align:left">No changes in the current release.</td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">Indexer</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/core-services/releases/tag/indexer-v1.1.5">indexer-v1.1.5</a>
      </td>
      <td style="text-align:left">egov-indexer:v1.1.5-196178f4-9</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">Report</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/core-services/releases/tag/report-v1.3.3">report-v1.3.3</a>
      </td>
      <td style="text-align:left">report:v1.3.3-c1315264-15</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">Workflow</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/core-services/releases/tag/workflow-v2-v1.2.0">workflow-v2-v1.2.0</a>
      </td>
      <td style="text-align:left">egov-workflow-v2:v1.2.0-f8601b36-49</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">PDF Generator</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/core-services/releases/tag/pdf-service-v1.1.4">pdf-service-v1.1.4</a>
      </td>
      <td style="text-align:left">pdf-service:v1.1.4-a4e9bb2c-16</td>
      <td style="text-align:left">No changes in the current release.</td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">Chatbot</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/core-services/releases/tag/chatbot-v1.1.5">chatbot-v1.1.5</a>
      </td>
      <td style="text-align:left">chatbot:v1.1.5-196178f4-9</td>
      <td style="text-align:left">Deprecated.</td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">Access Control</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/core-services/releases/tag/accesscontrol-v1.1.2">accesscontrol-v1.1.2</a>
      </td>
      <td style="text-align:left">egov-accesscontrol:v1.1.2-2ee9ec37-1</td>
      <td style="text-align:left">No changes in the current release.</td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">Location</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/core-services/releases/tag/location-v1.1.3">location-v1.1.3</a>
      </td>
      <td style="text-align:left">egov-location:v1.1.3-2ee9ec37-1</td>
      <td style="text-align:left">No changes in the current release.</td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">OTP</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/core-services/releases/tag/otp-v1.2.1">otp-v1.2.1</a>
      </td>
      <td style="text-align:left">egov-otp:v1.2.1-07a30430-2</td>
      <td style="text-align:left">No changes in the current release.</td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">User OTP</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/core-services/releases/tag/user-otp-v1.1.3">user-otp-v1.1.3</a>
      </td>
      <td style="text-align:left">user-otp:v1.1.3-2ee9ec37-6</td>
      <td style="text-align:left">No changes in the current release.</td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">NLP Engine</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/core-services/releases/tag/nlp-engine-v1.0.0">nlp-engine-v1.0.0</a>
      </td>
      <td style="text-align:left">nlp-engine:v1.0.0-fbea6fba-21</td>
      <td style="text-align:left">New Service</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Business Services</b>  <a href="https://github.com/egovernments/business-services/releases/tag/v2.5"><b>v2.5</b></a>
      </td>
      <td style="text-align:left">Apportion</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/business-services/releases/tag/apportion-service-v1.1.4">apportion-service-v1.1.4</a>
      </td>
      <td style="text-align:left">egov-apportion-service:v1.1.4-ec514d1-12</td>
      <td style="text-align:left">No changes in the current release.</td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">Collection</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/business-services/releases/tag/collection-services-v1.1.5">collection-services-v1.1.5</a>
      </td>
      <td style="text-align:left">collection-services:v1.1.5-33d01f1-38</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">Billing</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/business-services/releases/tag/billing-service-v1.3.3">billing-service-v1.3.3</a>
      </td>
      <td style="text-align:left">billing-service:v1.3.3-581d2eb-54</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">HRMS</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/business-services/releases/tag/hrms-v1.2.3">hrms-v1.2.3</a>
      </td>
      <td style="text-align:left">egov-hrms:v1.2.3-464d95d-17</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">Dashboard Analytics</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/business-services/releases/tag/dashboard-analytics-v1.1.5">dashboard-analytics-v1.1.5</a>
      </td>
      <td style="text-align:left">dashboard-analytics:v1.1.5-33d01f1-20</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">Dashboard Ingest</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/business-services/releases/tag/dashboard-ingest-v1.1.3">dashboard-ingest-v1.1.3</a>
      </td>
      <td style="text-align:left">dashboard-ingest:v1.1.3-6cb5d67-5</td>
      <td style="text-align:left">No changes in the current release.</td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">EGF Instrument</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/business-services/releases/tag/egf-instrument-v1.1.3">egf-instrument-v1.1.3</a>
      </td>
      <td style="text-align:left">egf-instrument:v1.1.3-b5944f0-1</td>
      <td style="text-align:left">No changes in the current release.</td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">EGF Master</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/business-services/releases/tag/egf-master-v1.1.2">egf-master-v1.1.2</a>
      </td>
      <td style="text-align:left">egf-master:v1.1.2-b5944f0-2</td>
      <td style="text-align:left">No changes in the current release.</td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">Finance Collection Voucher Consumer</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/business-services/releases/tag/finance-collections-voucher-consumer-v1.1.5">finance-collections-voucher-consumer-v1.1.5</a>
      </td>
      <td style="text-align:left">finance-collections-voucher-consumer:v1.1.5-cb9776c-11</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Municipal Services</b>  <a href="https://github.com/egovernments/municipal-services/releases/tag/v2.5"><b>v2.5</b></a>
      </td>
      <td style="text-align:left">Trade License</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/municipal-services/releases/tag/tl-services-v1.1.5">tl-services-v1.1.5</a>
      </td>
      <td style="text-align:left">tl-services:v1.1.5-d3163d602-29</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">Trade License Calculator</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/municipal-services/releases/tag/tl-calculator-v1.1.3">tl-calculator-v1.1.3</a>
      </td>
      <td style="text-align:left">tl-calculator:v1.1.3-0b2efd7f-3</td>
      <td style="text-align:left">No changes in the current release.</td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">Fire NOC</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/municipal-services/releases/tag/firenoc-services-v1.3.1">firenoc-services-v1.3.1</a>
      </td>
      <td style="text-align:left">firenoc-services:v1.3.1-e3052c649-28</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">Fire NOC Calculator</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/municipal-services/releases/tag/firenoc-calculator-v1.2.0">firenoc-calculator-v1.2.0</a>
      </td>
      <td style="text-align:left">firenoc-calculator:v1.2.0-a8da9ece-3</td>
      <td style="text-align:left">No changes in the current release.</td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">Property Services</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/municipal-services/releases/tag/property-services-v1.1.6">property-services-v1.1.6</a>
      </td>
      <td style="text-align:left">property-services:v1.1.6-dea64712f-117</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">Property Tax Calculator</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/municipal-services/releases/tag/pt-calculator-v2-v1.1.4">pt-calculator-v2-v1.1.4</a>
      </td>
      <td style="text-align:left">pt-calculator-v2:v1.1.4-ef94c644-20</td>
      <td style="text-align:left">No changes in the current release.</td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">Property Tax</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/municipal-services/releases/tag/pt-services-v2-v1.0.0">pt-services-v2-v1.0.0</a>
      </td>
      <td style="text-align:left">pt-services-v2:v1.0.0-ecf3410a</td>
      <td style="text-align:left">Deprecated. No changes in the current release.</td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">Water Charges</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/municipal-services/releases/tag/ws-services-v1.4.1">ws-services-v1.4.1</a>
      </td>
      <td style="text-align:left">ws-services:v1.4.1-e3052c649-26</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">Water Charges Calculator</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/municipal-services/releases/tag/ws-calculator-v1.3.1">ws-calculator-v1.3.1</a>
      </td>
      <td style="text-align:left">ws-calculator:v1.3.1-a8da9ece-41</td>
      <td style="text-align:left">No changes in the current release.</td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">Sewerage Charges</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/municipal-services/releases/tag/sw-services-v1.4.1">sw-services-v1.4.1</a>
      </td>
      <td style="text-align:left">sw-services:v1.4.1-e3052c649-22</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">Sewerage Charges Calculator</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/municipal-services/releases/tag/sw-calculator-v1.3.1">sw-calculator-v1.3.1</a>
      </td>
      <td style="text-align:left">sw-calculator:v1.3.1-a8da9ece-32</td>
      <td style="text-align:left">No changes in the current release.</td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">BPA Calculator</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/municipal-services/releases/tag/bpa-calculator-v1.1.0">bpa-calculator-v1.1.0</a>
      </td>
      <td style="text-align:left">bpa-calculator:v1.1.0-4ee62c15-1</td>
      <td style="text-align:left">No changes in the current release.</td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">BPA Services</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/municipal-services/releases/tag/bpa-services-v1.1.4">bpa-services-v1.1.4</a>
      </td>
      <td style="text-align:left">bpa-services:v1.1.4-ebe6a2b30-20</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">User Event</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/municipal-services/releases/tag/user-event-v1.1.3">user-event-v1.1.3</a>
      </td>
      <td style="text-align:left">egov-user-event:v1.1.3-a8da9ece-3</td>
      <td style="text-align:left">No changes in the current release.</td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">PGR</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/municipal-services/releases/tag/rainmaker-pgr-v1.1.4">rainmaker-pgr-v1.1.4</a>
      </td>
      <td style="text-align:left">rainmaker-pgr:v1.1.4-39d6a23fb-20</td>
      <td style="text-align:left">v1 - Deprecated.</td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">PGR Service</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/municipal-services/releases/tag/pgr-services-v1.1.3">pgr-services-v1.1.3</a>
      </td>
      <td style="text-align:left">pgr-services:v1.1.3-e3052c649-13</td>
      <td style="text-align:left">v2</td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">Land Services</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/municipal-services/releases/tag/land-services-v1.0.3">land-services-v1.0.3</a>
      </td>
      <td style="text-align:left">land-services:v1.0.3-e3052c649-6</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">NOC Services</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/municipal-services/releases/tag/noc-services-v1.0.3">noc-services-v1.0.3</a>
      </td>
      <td style="text-align:left">noc-services:v1.0.3-d89ad8118-11</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">FSM</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/municipal-services/releases/tag/fsm-v1.0.3">fsm-v1.0.3</a>
      </td>
      <td style="text-align:left">fsm:v1.0.3-e3052c649-62</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">FSM Calculator</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/municipal-services/releases/tag/fsm-calculator-v1.0.0">fsm-calculator-v1.0.0</a>
      </td>
      <td style="text-align:left">fsm-calculator:v1.0.0-39678039-14</td>
      <td style="text-align:left">No changes in the current release.</td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">Vehicle</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/municipal-services/releases/tag/vehicle-v1.0.2">vehicle-v1.0.2</a>
      </td>
      <td style="text-align:left">vehicle:v1.0.2-e3052c649-25</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">Vendor</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/municipal-services/releases/tag/vendor-v1.0.2">vendor-v1.0.2</a>
      </td>
      <td style="text-align:left">vendor:v1.0.2-e3052c649-23</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">eChallan Services</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/municipal-services/releases/tag/echallan-services-v1.0.3">echallan-services-v1.0.3</a>
      </td>
      <td style="text-align:left">echallan-services:v1.0.3-fe3e42537-25</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">eChallan Calculator</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/municipal-services/releases/tag/echallan-calculator-v1.0.1">echallan-calculator-v1.0.1</a>
      </td>
      <td style="text-align:left">echallan-calculator:v1.0.1-e3052c649-7</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">Inbox</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/municipal-services/releases/tag/inbox-v1.0.0">inbox-v1.0.0</a>
      </td>
      <td style="text-align:left">inbox:v1.0.0-dd430b7a8-28</td>
      <td style="text-align:left">New Service</td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">Turn-IO</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/municipal-services/releases/tag/turn-io-adapter-v1.0.0">turn-io-adapter-v1.0.0</a>
      </td>
      <td style="text-align:left">turn-io-adapter:v1.0.0-e3052c649-33</td>
      <td style="text-align:left">New Service</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Utilities Services</b>  <a href="https://github.com/egovernments/utilities/releases/tag/v2.5"><b>v2.5</b></a>
      </td>
      <td style="text-align:left">Custom Consumer</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/utilities/releases/tag/custom-consumer-v1.1.0">custom-consumer-v1.1.0</a>
      </td>
      <td style="text-align:left">egov-custom-consumer:v1.1.0-7a6db73</td>
      <td style="text-align:left">No changes in the current release.</td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">PDF</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/utilities/releases/tag/pdf-v1.1.1">pdf-v1.1.1</a>
      </td>
      <td style="text-align:left">egov-pdf:v1.1.1-caf76f9-17</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Others Service</b>
      </td>
      <td style="text-align:left">eDCR</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/eGov-dcr-service/releases/tag/egov-edcr-v2.0.0">egov-edcr-v2.0.0</a>
      </td>
      <td style="text-align:left">egov-edcr:v2.0.0-baa4485-19</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">Finance</td>
      <td style="text-align:left"><a href="https://github.com/egovernments/egov-coexistence/releases/tag/egov-coexistence-v3.0.2">egov-coexistence-v3.0.2</a>
      </td>
      <td style="text-align:left">egov-finance:v3.0.2-0d0a8db8ff-28</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Configs</b>  <a href="https://github.com/egovernments/configs/releases/tag/v2.5"><b>v2.5</b></a>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"> <b>MDMS</b>  <a href="https://github.com/egovernments/egov-mdms-data/releases/tag/v2.5"><b>v2.5</b></a>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"> <b>Localization</b>  <a href="https://github.com/egovernments/releasekit/releases/tag/v2.5"><b>v2.5</b></a>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>QA Automation</b>  <a href="https://github.com/egovernments/test-automation/releases/tag/v2.5"><b>v2.5</b></a>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>





> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_ ](https://egov.org.in/)_is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._

