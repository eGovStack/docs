---
description: DIGIT 2.2 - Technical Details of the Changes
---

# Configuration Changes

### MDMS changes <a id="MDMS-changes"></a>

| **Feature** | **Service Name** | **Changes** | **Description** |
| :--- | :--- | :--- | :--- |
| Common Pay |  | [\#1289](https://github.com/egovernments/egov-mdms-data/pull/1289) | Arrears Tax head changes for Common pay |
| WS |  | [\#1290](https://github.com/egovernments/egov-mdms-data/pull/1290) | Updated the one-time fee format for WS |
| All |  | [\#1393](https://github.com/egovernments/egov-mdms-data/pull/1393), [\#1394](https://github.com/egovernments/egov-mdms-data/pull/1394) | Digit 2.2 Release changes |
| PGR |  | [\#1400](https://github.com/egovernments/egov-mdms-data/pull/1400), [\#1402](https://github.com/egovernments/egov-mdms-data/pull/1402), [\#1403](https://github.com/egovernments/egov-mdms-data/pull/1403), [\#1408](https://github.com/egovernments/egov-mdms-data/pull/1408), [\#1410](https://github.com/egovernments/egov-mdms-data/pull/1410) | PGR UI V2 navigation URL changes and added pin codes for City A and City B |
| Role Action Mapping |  | [\#1406](https://github.com/egovernments/egov-mdms-data/pull/1406), [\#1407](https://github.com/egovernments/egov-mdms-data/pull/1407) | Added Workflow Process Count access to TL, Fire NOC, WS and BPA Employees |
| DSS |  | [\#1415](https://github.com/egovernments/egov-mdms-data/pull/1415), [\#1416](https://github.com/egovernments/egov-mdms-data/pull/1416) | Added mandatory DDRname for all tenants |

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
      <td style="text-align:left">WS</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><a href="https://github.com/egovernments/configs/pull/560">#560</a>
      </td>
      <td style="text-align:left">Updated searcher query for W&amp;S in UAT</td>
    </tr>
    <tr>
      <td style="text-align:left">WS</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><a href="https://github.com/egovernments/configs/pull/568">#568</a>
      </td>
      <td style="text-align:left">WS persister changes and order rearranged for PGR Reports</td>
    </tr>
    <tr>
      <td style="text-align:left">All</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><a href="https://github.com/egovernments/configs/pull/597">#597</a>
      </td>
      <td style="text-align:left">Digit 2.2 Release changes</td>
    </tr>
    <tr>
      <td style="text-align:left">HRMS</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><a href="https://github.com/egovernments/configs/pull/599">#599</a>
      </td>
      <td style="text-align:left">HRMS Employee create changes</td>
    </tr>
    <tr>
      <td style="text-align:left">Common Pay</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><a href="https://github.com/egovernments/configs/pull/600">#600</a>
      </td>
      <td style="text-align:left">Payer details changes in Payment Receipt</td>
    </tr>
    <tr>
      <td style="text-align:left">BPA</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><a href="https://github.com/egovernments/configs/pull/606">#606</a>,
        <a
        href="https://github.com/egovernments/configs/pull/608">#608</a>, <a href="https://github.com/egovernments/configs/pull/620">#620</a>
      </td>
      <td style="text-align:left">Collection search endpoint changes</td>
    </tr>
    <tr>
      <td style="text-align:left">DSS</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><a href="https://github.com/egovernments/configs/pull/610">#610</a>,
        <a
        href="https://github.com/egovernments/configs/pull/623">#623</a>
      </td>
      <td style="text-align:left">Indexer config fix for PGR Services and DSS related config changes for
        UAT</td>
    </tr>
    <tr>
      <td style="text-align:left">PGR</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">
        <p><a href="https://github.com/egovernments/configs/pull/614">#614</a>,</p>
        <p><a href="https://github.com/egovernments/configs/pull/625">#625</a>
        </p>
      </td>
      <td style="text-align:left">Created PGR migration batch file</td>
    </tr>
  </tbody>
</table>

### Infra Change <a id="Infra-Change"></a>

| **Feature** | **Feature** | **Description** |
| :--- | :--- | :--- |
| PGR | [\#1200](https://github.com/egovernments/eGov-infraOps/pull/1200) | Digit-ui Configuration |
| WS | [\#1203](https://github.com/egovernments/eGov-infraOps/pull/1203) | Digit 2.2 Release changes for UAT |
| Filestore | [\#1209](https://github.com/egovernments/eGov-infraOps/pull/1209) | Disabled Minio in UAT |
| PGR Service | [\#1221](https://github.com/egovernments/eGov-infraOps/pull/1221), [\#1225](https://github.com/egovernments/eGov-infraOps/pull/1225), [\#1227](https://github.com/egovernments/eGov-infraOps/pull/1227) | Path to pgr-services.yml indexer config |

