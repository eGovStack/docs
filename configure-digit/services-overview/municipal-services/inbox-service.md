# Inbox Service

## Overview

The inbox service is an aggregation service which aggregates data of municipal services and workflow based on given complex search criteria and returns applications and workflow data in a paginated manner. The service also returns the total count matching the search criteria.

## Sample Configuration

This service allows searching of both the module objects as well as `processInstance`(Workflow record) based on the given criteria for any of the municipal services. For this, it uses a module-specific configuration which is stored in application.properties as a key value map, where the key is the businessService name while the value is the configuration map. A sample configuration is attached below -

```
{
  "FSM": {
    "searchPath": "http://localhost:9098/fsm/v1/_search",
    "dataRoot": "fsm",
    "applNosParam": "applicationNos",
    "businessIdProperty": "applicationNo",
    "applsStatusParam": "applicationStatus"
  },
  "FSM_VEHICLE_TRIP": {
    "searchPath": "http://localhost:8061/vehicle/trip/v1/_search",
    "dataRoot": "vehicleTrip",
    "applNosParam": "applicationNos",
    "businessIdProperty": "applicationNo",
    "applsStatusParam": "applicationStatus"
  },
  "PT.CREATE,PT.MUTATION,PT.UPDATE": {
    "searchPath": "http://localhost:8088/property-services/property/_search",
    "dataRoot": "Properties",
    "applNosParam": "acknowldgementNumber",
    "businessIdProperty": "acknowldgementNumber",
    "applsStatusParam": "status"
  },
  "NewTL,EDITRENEWAL,DIRECTRENEWAL": {
    "searchPath": "http://localhost:8088/tl-services/v1/_search",
    "dataRoot": "Licenses",
    "applNosParam": "applicationNumber",
    "businessIdProperty": "applicationNumber",
    "applsStatusParam": "status"
  }
}
```

Here, the key of the config map is the business services of the PT module for which the inbox has to be configured. Now, inside the search definition -

1. `searchPath` - Points to the search URL of the municipal module
2. `dataRoot` - This is the search response key that we get from module search, e.g. in the Property module, the search response returns response objects inside the “Properties” key.
3. `applNosParam` - This is the parameter with which workflow search is called once the module objects are retrieved from module search. This parameter is the field on which the module table is joined with the workflow process instance table, e.g. in the case of the Property module it is “acknowldgementNumber”.
4. `businessIdProperty` - This is the parameter with which we search module objects in case of empty `moduleSearchCriteria` by performing the workflow search first. Again, this parameter is the field on which we join the module table and workflow process instance table, e.g. in the case of the Property module it is “acknowldgementNumber”.
5. `applsStatusParam` - This is the application status field name for the module upon which the search is being performed, e.g. in the case of the Property module, it is “status”.

### Service Integration  <a href="#searcher-integration" id="searcher-integration"></a>

To provide pagination and total count across multiple modules, the inbox service is integrated with the searcher. The searcher provides the list of ids and the total count of applications, based on those further enrichment is done by inbox service and results are returned to the API. The sample configuration link for PT and TL modules is given below:

[Property Service Inbox Searcher Configuration](https://raw.githubusercontent.com/egovernments/configs/qa/egov-searcher/inboxpropertysearch.yml)

[Trade License Service Inbox Searcher Configuration](https://raw.githubusercontent.com/egovernments/configs/qa/egov-searcher/inboxTLSearch.yml)
