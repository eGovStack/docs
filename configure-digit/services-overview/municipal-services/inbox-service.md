# Inbox Service

The inbox service is an aggregation service which aggregates data of municipal services and workflow based on given complex search criteria and returns applications and workflow data in paginated manner. The service also returns the total count matching the search criteria.\
This service allows to search both the module objects as well as `processInstance`(Workflow record) based on the provided criteria for any of the municipal services. For this, it uses a module specific configuration which is stored in application.properties as a key value map, where the key is the businessService name while the value is the configuration map. An sample configuration is attached below -

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

Here, the key of the config map are the business services of PT module for which inbox has to be configured. Now, inside the search definition -

1. `searchPath` - Points to the search URL of the municipal module
2. `dataRoot` - This is the search response key that we get from module search, e.g. in Property module, the search response returns response objects inside “Properties” key.
3. `applNosParam` - This is the parameter with which workflow search is called once the module objects are retrieved from module search. This parameter is the filed on which module table is joined with the workflow process instance table, e.g. in case of Property module it is “acknowldgementNumber”.
4. `businessIdProperty` - This is the parameter with which we search module objects in case of empty `moduleSearchCriteria` by performing the workflow search first. Again, this parameter is the field on which we join module table and workflow process instance table, e.g. in case of Property module it is “acknowldgementNumber”.
5. `applsStatusParam` - This is the application status field name for the module upon which search is being performed, e.g. in case of Property module, it is “status”.

#### Searcher Integration: <a href="#searcher-integration" id="searcher-integration"></a>

To provide pagination and total count across multiple modules, the inbox service is integrated with searcher. The searcher provides the list of ids and the total count of applications, based on those further enrichment is done by inbox service and results are returned to the API. Sample configuration link for PT and TL module is attached below:

[Property Service Inbox Searcher Configuration](https://raw.githubusercontent.com/egovernments/configs/qa/egov-searcher/inboxpropertysearch.yml)

[Trade License Service Inbox Searcher Configuration](https://raw.githubusercontent.com/egovernments/configs/qa/egov-searcher/inboxTLSearch.yml)
