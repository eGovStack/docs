# Report Service

## Overview <a href="#overview" id="overview"></a>

Reporting Service is a service running independently on a separate server. The main objective of this service is to provide a common framework for generating reports. This service loads the report configuration from a yaml file at the run time and provides the report details by using a couple of APIs.

## Pre-requisites <a href="#pre-requisites" id="pre-requisites"></a>

Before you proceed with the documentation, make sure the following pre-requisites are met -

* Prior Knowledge of Java/J2EE.
* Prior Knowledge of SpringBoot.
* Advanced Knowledge of PostgreSQL.
* Prior Knowledge of REST APIs and related concepts like path parameters, headers, JSON etc.
* JSONPath for filtering required data from json objects.

## Key Functionalities <a href="#key-functionalities" id="key-functionalities"></a>

* Provides an easy way to add reports on the fly just by adding configurations without any coding effort.
* Provides flexibility to customise result column names in the config.
* Provides flexibility to fetch data from DB and also from some other service returning required json objects when it is not possible to get all required data from DB.
* Provides functionality to add filters as per requirements before actually fetching data for the report.

## Configuration Details <a href="#configuration-details" id="configuration-details"></a>

#### **Definitions** <a href="#definitions" id="definitions"></a>

1. **Config file**
   * A YAML (xyz.yml) file contains configuration for report requirements.&#x20;
2. **API**
   * A REST endpoint to fetch data based on the configuration.
3. **Inline-table**
   * If we also want to show data from some external service with data coming from DB  in reports we use inline-tables. The data from external service is stored in inline-table and then used as any normal DB table to get data. This table is short lived and stays only for the time when a query is being executed. It is never stored in DB. We provide JSON paths in an ordered manner corresponding to each column in the table. These JSON paths will be used to extract required data from the external service’s response. For configs please see ‘How to Use’ section.&#x20;

#### How to Use <a href="#how-to-use" id="how-to-use"></a>

**Configuration**&#x20;

As mentioned above, report service uses a config file per module to store all the configurations of reports pertaining to that module. Report service reads multiple such files at start-up to support reports of all the configured modules. The file contains the following keys:

* **reportName:** name of report, to be used with module name to identify any report config
* **summary:** summary of report
* **version:** version of the report
* **moduleName:** name of the module to which the report belongs to
* **externalService**: To be used when some of the report data needs to be fetched from external service through inline-tables. It contains the following fields
  1. **entity**: JSON Path to filter json arrays(result to be turned into tables) from returned json&#x20;
  2. **apiURL:** API URL of the external service
  3. **keyOrder:** order of JSON object keys to form table columns from JSON  object arrays
  4. **tableName:** name to be given to represent this transformed data which will be used as a table in the SQL query
* **sourceColumns :** These represent the final data sent by service on GET\_DATA API call. The order of sourceColumns in the Config is the same as that of columns in the result.  Each sourceColumns represent one column in the result. For each column, data is picked after executing the final SQL query formed after appending groupby, orderby, search params into base query
  * **name**: name of the column to fetch data from query results, must be there in query results
  * **label**: custom column label
  * **type**: data type of column
  * **source**: module name
  * **total**: whether column total required on the front end
* **searchParams**:
  * **name**: name of search param. Must match variable used in search clause
  * **label**: a custom label for viewing on the front end
  * **type**: type of search params. If type is ‘singlevaluelist’ then  use pattern to populate searchparams possible values to select from by the user\
    Ex:-number,string,singlevaluelist etc
  * **source**: module name
  * **isMandatory**: If the user must fill this searchparam before requesting report data
  * **searchClause:** SQL search clause for corresponding search params to filter results, to be appended in base query Ex:- AND fnoc.tenantId IN ($ulb)\
    Here $ulb will be replaced by user inputs
  * **Pattern:** This field will be used only when ‘type’ is set to ‘singlevaluelist’. It is the external service URL combined with JSON Paths separated by ‘|’. The first JSON path is for codes and the second for values. Values will be shown to the user in drop down. And codes corresponding to user selected value will be sent to the report service and will be used in searchClauses mentioned in the last point.\
    Ex:-[http://egov-mdms-service:8080/egov-mdms-service/v1/\_get?tenantId=$tenantid\&moduleName=tenant\&masterName=tenants|$.MdmsRes.tenant.tenants.\*.code|$.MdmsRes.tenant.tenants.\*.name](https://digit-discuss.atlassian.net/wiki/spaces/EPE/pages/226557957/Report+Framework)
* **Query:** Main/base query clause for fetching report data from DB and custom tables formed after fetching data from external service&#x20;
* **Orderby:** order by clause to be appended into base query
* **Groupby:** group by clause to be appended into base query
* **additionalConfig:** to provide additional custom configs which are not present above

**Call the MDMS or any other API with the post method**

1. Configuring the post object in the yaml itself like below.\
   externalService:
   * entity: $.MdmsRes.egf-master.FinancialYear
     * apiURL: [http://](http://localhost:8094/egov-mdms-service/v1/\_search)[egov-mdms-service:8080](https://digit-discuss.atlassian.net/wiki/spaces/EPE/pages/226557957/Report+Framework)[/egov-mdms-service/v1/\_search](http://localhost:8094/egov-mdms-service/v1/\_search)
     * keyOrder: finYearRange,startingDate,endingDate,tenantId
     * tableName: tbl\_financialyear
     * stateData: true
     * postObject:
       * tenantId: $tenantid
       * moduleDetails:
         * moduleName: egf-master
         * masterDetails:
           * name: FinancialYear filter: "\[?(@.id IN \[2,3] && @.active == true)]"
2. Keep the post object in a separate json file externally and call at runtime.

#### Sample yaml Configuration <a href="#sample-yaml-configuration" id="sample-yaml-configuration"></a>

```
ReportDefinitions:
- reportName: EmployeeReport
  decryptionPathId: EmployeeReport
  summary: Fetches employee data based on provided search parameters
  version: 1.0.0
  moduleName: hrms
  externalService:
  - entity: $.MdmsRes.common-masters.Department
    apiURL: http://egov-mdms-service:8080/egov-mdms-service/v1/_get?moduleName=common-masters&masterName=Department&tenantId=$tenantId
    keyOrder: name,code
    tableName: tbl_def_dept
  - entity: $.MdmsRes.common-masters.Designation
    apiURL: http://egov-mdms-service:8080/egov-mdms-service/v1/_get?moduleName=common-masters&masterName=Designation&tenantId=$tenantId
    keyOrder: name,code
    tableName: tbl_def_desig
  - entity: $.MdmsRes.ACCESSCONTROL-ROLES.roles
    apiURL: http://egov-mdms-service:8080/egov-mdms-service/v1/_get?moduleName=ACCESSCONTROL-ROLES&masterName=roles&tenantId=$tenantId
    keyOrder: name,code
    tableName: tbl_def_roles
  sourceColumns:
  - name: id
    label: reports.hrms.id
    type: string
    source: eg_hrms_employee
  - name: name
    label: reports.hrms.name
    type: string
    source: eg_hrms_employee
  - name: rolecodes
    label: reports.hrms.role
    type: stringarray
    source: eg_hrms_employee
    isLocalisationRequired: true
    localisationPrefix: ACCESSCONTROL_ROLES_ROLES_
  - name: designation
    label: reports.hrms.designation
    type: string
    source: eg_hrms_employee
    isLocalisationRequired: true
    localisationPrefix: COMMON_MASTERS_DESIGNATION_
  - name: department
    label: reports.hrms.department
    type: string
    source: eg_hrms_employee
    isLocalisationRequired: true
    localisationPrefix: COMMON_MASTERS_DEPARTMENT_
  - name: status
    label: reports.hrms.status
    type: string
    source: eg_hrms_employee
    isLocalisationRequired: true
    localisationPrefix: EGOV_HRMS_EMPLOYEESTATUS_
  searchParams:
  - name: ulb
    label: ULB
    type: singlevaluelist
    pattern: http://egov-mdms-service:8080/egov-mdms-service/v1/_get?tenantId=$tenantid&moduleName=tenant&masterName=tenants|$.MdmsRes.tenant.tenants.*.code|$.MdmsRes.tenant.tenants.*.name
    source: pt
    wrapper: true
    isMandatory: true
    searchClause: AND emp_data.tenantid = $ulb
  - name: status
    label: reports.hrms.status
    type: multivaluelist
    pattern: http://egov-mdms-service:8080/egov-mdms-service/v1/_get?tenantId=pb&moduleName=egov-hrms&masterName=EmployeeStatus|$.MdmsRes.egov-hrms.EmployeeStatus[?(@.active)].code|$.MdmsRes.egov-hrms.EmployeeStatus[?(@.active)].code
    source: seva
    isMandatory: false
    isLocalisationRequired: true
    localisationPrefix: EGOV_HRMS_EMPLOYEESTATUS_
    searchClause: AND emp_data.employeestatus IN ( $status )
  - name: role
    label: reports.hrms.role
    type: multivaluelist
    pattern: http://egov-mdms-service:8080/egov-mdms-service/v1/_get?tenantId=pb&moduleName=ACCESSCONTROL-ROLES&masterName=roles|$.MdmsRes.ACCESSCONTROL-ROLES.roles[?(@.code nin ['CITIZEN'])].code|$.MdmsRes.ACCESSCONTROL-ROLES.roles[?(@.code nin ['Citizen'])].code
    isMandatory: false
    isLocalisationRequired: true
    localisationPrefix: ACCESSCONTROL_ROLES_ROLES_
    searchClause: AND ARRAY[ $role ]::varchar[] && emp_data.rolecodes::varchar[]
  - name: deptname
    label: reports.pgr.dept.name
    type: multivaluelist
    source: eg_pgr_service
    pattern: http://egov-mdms-service:8080/egov-mdms-service/v1/_get?tenantId=$tenantid&moduleName=common-masters&masterName=Department|$.MdmsRes.common-masters.Department[*].code|$.MdmsRes.common-masters.Department[*].code
    isMandatory: false
    isLocalisationRequired: true
    localisationPrefix: COMMON_MASTERS_DEPARTMENT_
    searchClause: AND deptmap_def.code IN ($deptname)
  query: |
    WITH emp_data AS (SELECT DISTINCT
      ehe.id,
      ehe.uuid,
      ehe.tenantid,
      eu.name,
      (SELECT ARRAY(SELECT DISTINCT er.name from eg_user eu LEFT JOIN eg_userrole_v1 eur ON eu.id=eur.user_id AND eu.tenantid=eur.user_tenantid LEFT JOIN (VALUES tbl_def_roles) AS er(name,code) ON eur.role_code=er.code WHERE eu.uuid=ehe.uuid AND er.name IS NOT NULL)) as role,
      (SELECT ARRAY(SELECT DISTINCT er.code from eg_user eu LEFT JOIN eg_userrole_v1 eur ON eu.id=eur.user_id AND eu.tenantid=eur.user_tenantid LEFT JOIN (VALUES tbl_def_roles) AS er(name,code) ON eur.role_code=er.code WHERE eu.uuid=ehe.uuid AND er.code IS NOT NULL)) as rolecodes,
      eha.designation,
      eha.department,
      ehe.employeestatus
      FROM eg_hrms_employee ehe
      LEFT OUTER JOIN eg_user eu ON ehe.uuid = eu.uuid
      LEFT OUTER JOIN eg_hrms_assignment eha ON eu.uuid = eha.employeeid
      WHERE eu.active = true)
    SELECT emp_data.id as id,
      emp_data.name as name,
      ARRAY_TO_STRING(emp_data.role, ',') as role,
      ARRAY_TO_STRING(emp_data.rolecodes, ',') as rolecodes,
      desigmap_def.code as designation,
      deptmap_def.code as department,
      emp_data.employeestatus as status
    FROM emp_data
    INNER JOIN (VALUES tbl_def_dept) AS deptmap_def(name,code) ON deptmap_def.code=emp_data.department
    INNER JOIN (VALUES tbl_def_desig) AS desigmap_def(name,code) ON desigmap_def.code=emp_data.designation
    WHERE 1=1
  order by: ehe.id ASC


```

#### API Details <a href="#api-details" id="api-details"></a>

There are two API calls to report service ‘GET METADATA’ and ‘GET DATA’.&#x20;

**GET METADATA**

This request to report service is made to get metadata for any report. The metadata contains information about search filters to be used in the report before actually sending request to get actual data. The user selected values are then used in GET\_DATA request to filter data.

**endpoint:** /report/{moduleName}/{report name}/metadata/\_get

**moduleName**:- It is used to define the names of module which contains current report

**Body**: The Body consists of the following:

1. RequestInfo: Header details as used on the egov platform
2. tenantId: tenantId of ULB
3. reportName: name of the report to be used

**Instance**

**URL:** [https://{domain name}/report/rainmaker-tl/metadata/\_get](https://egov-micro-dev.egovernments.org/report/rainmaker-tl/metadata/\_get)

**Body**

```
{
  "RequestInfo": {
    "apiId": "emp",
    "ver": "1.0",
    "ts": 1558889531536,
    "action": "create",
    "did": "1",
    "key": "abcdkey",
    "msgId": "20170310130900",
    "requesterId": "",
    "authToken": "{auth Token}"
  },
  "tenantId": "pb.amritsar",
  "reportName": "TradeWiseCollectionReport"
}
```

**GET DATA**

This request to report service is used to get data for the report. Inputs given by the user for filters are sent in the request body. These filter values are used while querying data from DB.

**endpoint:** report/{moduleName}/{report name}/\_get

**moduleName:** It is used to define the names of module which contains current repo

**Body**: The Body consists of the following:

1. RequestInfo: Header details as used on the egov platform
2. tenantId: tenantId of ULB
3. reportName: name of the report to be used
4. Array of search params corresponding to each of the filled filters by the user. Each searchparam contains:-
   1. Name: name of the filter
   2. Input: user**-**selected value&#x20;

**Instance**

**URL:** [https://{domain name}/report/rainmaker-tl/\_get](https://egov-micro-dev.egovernments.org/report/rainmaker-tl/\_get)

**Body**

```
{
  "RequestInfo": {
    "apiId": "emp",
    "ver": "1.0",
    "ts": 1558888480562,
    "action": "create",
    "did": "1",
    "key": "abcdkey",
    "msgId": "20170310130900",
    "requesterId": "",
    "authToken": "{auth Token}"
  },
  "tenantId": "pb.amritsar",
  "reportName": "TradeLicenseRegistryReport",
  "searchParams": [
    {
      "name": "fromDate",
      "input": 1556649000000
    }
  ]
}
```

## Deployment Details <a href="#deployment-details" id="deployment-details"></a>

1. Write configuration as per your requirement. The structure of the config file is explained in the Configuration Details section.
2. Check-in the config file to a remote location preferably Github. Currently, the files are checked into this folder - [<img src="https://github.com/fluidicon.png" alt="" data-size="line">configs/reports/config at DEV · egovernments/configs](https://github.com/egovernments/configs/tree/DEV/reports/config) for dev and QA environment.
3. Add module name and corresponding report path in the same format as used in [<img src="https://github.com/fluidicon.png" alt="" data-size="line">configs/reportFileLocationsv1.txt at DEV · egovernments/configs](https://github.com/egovernments/configs/blob/DEV/reports/reportFileLocationsv1.txt)
4. Provide the absolute path of the file mentioned in Point 3  to DevOps, to add it to the file-read path of the report service. The file is added to the environment manifest file for it to be read at the start-up of the application.
5. Deploy the latest version of the report service app.
6. Add Role-Action mapping for APIs.
7. Use the module-name as path parameters in the URL of the requests for report service with the required request body.

## Integration <a href="#integration" id="integration"></a>

### Integration Scope <a href="#integration-scope" id="integration-scope"></a>

The report service provides a common framework to generate reports and show the report details base on the search criteria.

### Integration Benefits <a href="#integration-benefits" id="integration-benefits"></a>

* Provide a common framework for generating reports
* Provide functionality to create new ad-hoc reports with minimal efforts
* Avoid writing code again in case of new report requirements
* Makes it possible to create reports with only knowledge of SQL and JSONPath&#x20;
* Provides metadata about the report.
* Provides the data for the report.
* Reload the configuration at runtime

### Steps to Integration <a href="#steps-to-integration" id="steps-to-integration"></a>

1. To integrate, a host of echallan-services modules should be overwritten in the helm chart.
2. The API should be mentioned in ACCESSCONTROL-ACTIONS-TEST. Refer example below.
3. Add Role-Action mapping for APIs.

```
//This entry is for to decide the location of report on UI screen
{
      "id": {Placeholder1},
      "name": "{Report name}",
      "url": "url",
      "displayName": "{Display name}",
      "orderNumber": 1,
      "parentModule": "",
      "enabled": true,
      "serviceCode": "",
      "code": "null",
      "path": "{path}", // here we need to mentioned the path
      "navigationURL": "{Naviagtion url}",
      "leftIcon": "action:assignment",
      "rightIcon": ""
    },

//This entry is to add GET DATA API of the report
    {
      "id": {Placeholder2},
      "name": "MCollectCollectionReport",
      "url": "/report/{moduleName}/{report name}/_get",
      "displayName": "{Display Name}",
      "orderNumber": 0,
      "enabled": true,
      "serviceCode": "{Service code}",
      "code": "null",
      "path": "{path}"
    },
    
//This entry is to add GET METADATA API of the report
    {
      "id": 2155,
      "name": "MCollectCollectionReport",
      "url": "/report/{moduleName}/{report name}/metadata/_get",
      "displayName": "Collection Report",
      "orderNumber": 1,
      "enabled": true,
      "serviceCode": "{Service code}",
      "code": "null",
      "path": "{path}"
    },
```

## Reference Docs

#### Doc Links <a href="#doc-links" id="doc-links"></a>

| **Title**                 | **Link**                                                                                                                                                                        |
| ------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| API Swagger Documentation | [Swagger Documentation](https://editor.swagger.io/?url=https://raw.githubusercontent.com/egovernments/egov-services/master/docs/reportinfra/contracts/reportinfra-1-0-0.yml#!/) |
| Local Setup               | [Local Setup](https://github.com/egovernments/DIGIT-Dev/blob/master/core-services/report/LOCALSETUP.md)                                                                         |



> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)_​_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in/) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
