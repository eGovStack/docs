# Dashboard Analytics - Backend

## DSS Backend Configuration Manual <a id="DSS-Backend-Configuration-Manual"></a>

## Overview <a id="Overview"></a>

DSS has two sides to it. One is the process in which the Data is pooled to ElasticSearch and the other being the way it is fetched, aggregated, computed, transformed and sent across. As this revolves around a variety of Data Set, there is a need for making this configurable. So that, tomorrow, given a new scenario is introduced, then it is just a configuration away from getting the newly introduced scenario involved in this flow of the process. 

This document explains the steps on how to define the configurations for both sides of DSS. Analytics and Ingest Pipeline Services. 

## Abbreviations <a id="Abbreviations"></a>

**Ingest:** Micro Service which runs as a pipeline and manages to validate, transform and enrich the incoming data and pushes the same to ElasticSearch Index

**Analytics:** Micro Service which is responsible for building, fetching, aggregating and computing the Data on ElasticSearch to a consumable Data Response. Which shall be later used for visualizations and graphical representations. 

**JOLT:** JSON to JSON transformation library written in Java where the "specification" for the transform is itself a JSON document

**Modules / Domain Level:** These are the Services in this context. Each of the services, such as Property Tax, Trade License, Water and Sewerages are considered as Modules / Domains

**Chart:** Each individual graphical representation is considered as a Chart in specific. For example, a Metric of Total Collection is considered as a Chart. 

**Visualization:** Group of different Charts is considered as a Visualization. For example, the group of Total Collection, Target Collection and Target Achieved is considered as a Metric Collection of Charts and thus it becomes a Visualization.  

## Ingest Pipeline Configurations <a id="Ingest-Pipeline-Configurations"></a>

Below is the list of configurations -

1. Topic Context Configurations
2. Validator Schema
3. JOLT Transformation Schema
4. Enrichment Domain Configuration 
5. JOLT Domain Transformation Schema

**Descriptions**

Topic Context Configurations

Topic Context Configuration is an outline to define which data is received on which Kafka Topic. 

Indexer Service and many other services are sending out data on different Kafka Topics. If the Ingest Service is asked to receive those data and pass it through the pipeline, the context and the version of the data being received has to be set. This configuration is used to identify which kafka topic consumed the data and what is the mapping for that.

![Figure 1](../../../../.gitbook/assets/110.png)

[Click here for Full Configuration](https://github.com/egovernments/configs/blob/master/egov-dss-dashboards/dashboard-ingest/TopicContextConfiguration.json)

| **Parameter Name** | **Description** |
| :--- | :--- |
| topic | Holds the name of the Kafka Topic on which the data is being received |
| dataContext | Context Name which needs to be set for further actions in the pipeline |
| dataContextVersion | Version of the Data Structure is set here as there might be different structured data at a different point in time |

2. Validator Schema

Validator Schema is a configuration Schema Library from **Everit**By passing the data against this schema, it ensures whether the data abides by the rules and requirements of the schema which has been defined. 

![Figure 2](../../../../.gitbook/assets/111.png)

[Click here for an example configuration](https://github.com/egovernments/configs/blob/master/egov-dss-dashboards/dashboard-ingest/validator_transaction_v1.json)

3. JOLT Transformation Schema

JOLT is a JSON to JSON Transformation Library. In order to change the structure of the data and transform it in a generic way, JOLT has been used. 

While the transformation schemas are written for each Data Context, the data is transformed against the schema to obtain a transformed data. 

[Follow the slide deck for JOLT Transformations](https://docs.google.com/presentation/d/1sAiuiFC4Lzz4-064sg1p8EQt2ev0o442MfEbvrpD1ls/edit#slide=id.p)

![Figure 3](../../../../.gitbook/assets/112.png)

[Click here for an example configuration](https://github.com/egovernments/configs/blob/master/egov-dss-dashboards/dashboard-ingest/transform_collection_v1.json)

4. Enrichment Domain Configuration 

This configuration defines and directs the Enrichment Process which the data goes through. 

For example, if the Data which is incoming is belonging to a Collection Module data, then the Collection Domain Config is picked. And based on the Business Type specified in the data, the right config is picked. 

In order to enhance the data of Collection, the domain index specified in the configuration is queried with the right arguments and the response data is obtained, transformed and set. 

[Click here for an example configuration](https://github.com/egovernments/configs/blob/master/egov-dss-dashboards/dashboard-ingest/DomainConfig.json)

<table>
  <thead>
    <tr>
      <th style="text-align:left"><b>Paremter Name</b>
      </th>
      <th style="text-align:left"><b>Description</b>
      </th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">id</td>
      <td style="text-align:left">Unique Identifier for the Configuration within the configuration document</td>
    </tr>
    <tr>
      <td style="text-align:left">businessType</td>
      <td style="text-align:left">This defines as in which kind of Domain / Service is the data related
        to. Based on this business type, query and enhancements are decided</td>
    </tr>
    <tr>
      <td style="text-align:left">indexName</td>
      <td style="text-align:left">Based on Business Type, Index Name is defined as to which index has to
        be queried to get the enhancements done from</td>
    </tr>
    <tr>
      <td style="text-align:left">query</td>
      <td style="text-align:left">Query to execute to get the Domain Level Object is defined here.</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>targetReferences</p>
        <p>sourceReference</p>
      </td>
      <td style="text-align:left">Fields which are variables in order to get the domain level objects are
        defined here. The variables and where all the values has to be picked from
        are documented here</td>
    </tr>
  </tbody>
</table>

5. JOLT Domain Transformation Schema

As a part of Enhancement, once the domain level object is obtained, we might not need the complete document as is in the end data product. 

Only those parameters which should be or can be used for aggregation and representation are to be held and others are to be discarded. 

In order to do that, we make use of JOLT again and write schemas to keep the required ones and discard the unwanted ones. 

The above configuration is used to transform the data response in the enrichment layer. 

![Figure 4](../../../../.gitbook/assets/113.png)

[Click here for an example configuration](https://github.com/egovernments/configs/blob/master/egov-dss-dashboards/dashboard-ingest/transform_tl_v1.json)

6.  Use case:- JOLT Transformation Schema for collection V2

 JOLT transformation schema for payment-v1 has taken as a use case to explain the context collection and context version v2. The payment records are processed/transformed with the schema. The schema supports splitting the billing records into an independent new record. So if there are 2 bill items in the collection/payment incoming data then this results in 2 collection records in turn.

![Figure 5](../../../../.gitbook/assets/114.png)

[Click here for an example configuration](https://github.com/egovernments/configs/blob/master/egov-dss-dashboards/dashboard-ingest/transform_collection_v2.json)

Here: **$i**, the variable value that gets incremented for the number of records of paymentDetails 

**$j**, the variable value that gets incremented for the number of records of billDetails.

**Note:** For kafka connect to work, Ingest pipeline application properties or in environments direct push must be disabled.

es.push.direct=false

## Analytics Configurations  <a id="Analytics-Configurations"></a>

Below is the list of configurations

1. Chart API Configuration
2. Master Dashboard Configuration
3. Role Dashboard Mappings Configuration

**Description**

Chart API Configuration

Each Visualization has its own properties. Each Visualization comes from different data sources \(Sometimes it is a combination of different data sources\) 

In order to configure each visualization and its properties, we have Chart API Configuration Document. 

In this, Visualization Code, which happens to be the key, will be having its properties configured as a part of the configuration and are easily changeable.

![Figure 6](../../../../.gitbook/assets/115.png)

[Click here for an example configuration](https://github.com/egovernments/configs/blob/master/egov-dss-dashboards/dashboard-analytics/ChartApiConfig.json)

<table>
  <thead>
    <tr>
      <th style="text-align:left"><b>Parameter Name</b>
      </th>
      <th style="text-align:left"><b>Description</b>
      </th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Key (e.g: totalApplication)</td>
      <td style="text-align:left">This is the Visualization Code. This key will be referred to in further
        visualization configurations. This is the key that will be used by the
        client application to indicate which visualization is needed for display.</td>
    </tr>
    <tr>
      <td style="text-align:left">chartName</td>
      <td style="text-align:left">The name of the Chart has to be used as a label on the Dashboard. The
        name of the Chart will be a detailed name. In this configuration, the Name
        of the Chart will be the code of Localization which will be used by Client
        Side</td>
    </tr>
    <tr>
      <td style="text-align:left">queries</td>
      <td style="text-align:left">Some visualizations are derived from a specific data source. While some
        others are derived from different data sources and are combined together
        to get a meaningful representation. The queries of aggregation which are
        to be used to fetch out the right data in the right aggregated format are
        configured here.</td>
    </tr>
    <tr>
      <td style="text-align:left">queries.module</td>
      <td style="text-align:left">The module / domain level, on which the query should be applied on. Property
        Tax is PT, Trade License is TL. If the query is applied across all modules,
        the module has to be defined as COMMON</td>
    </tr>
    <tr>
      <td style="text-align:left">queries.indexName</td>
      <td style="text-align:left">The name of the index upon which the query has to be executed is configured
        here.</td>
    </tr>
    <tr>
      <td style="text-align:left">queries.aggrQuery</td>
      <td style="text-align:left">The aggregation query in itself is added here. Based on the Module and
        the Index name specified, this query is attached to the filter part of
        the complete search request and then executed against that index</td>
    </tr>
    <tr>
      <td style="text-align:left">queries.requestQueryMap</td>
      <td style="text-align:left">Client Request would carry certain fields which are to be filtered. The
        parameters specified in the Client Request are different from the parameters
        in each of these indexed documents. In order to map the parameters of the
        request to the parameters of the ElasticSearch Document, this mapping is
        maintained</td>
    </tr>
    <tr>
      <td style="text-align:left">queries.dateRefField</td>
      <td style="text-align:left">
        <p>Each of these modules has separate indexes. And all of them have their
          own date fields.</p>
        <p>When there is a date filter applied against these visualizations, each
          of them has to apply it against their own date reference fields. In order
          to maintain what is the date field in which index, we have this configured
          in this configuration parameter</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">chartType</td>
      <td style="text-align:left">
        <p>As there are different types of visualizations, this field defines as
          what is the type of chart / visualization that this data should be used
          to represent.</p>
        <p><b>Chart types available are</b>:</p>
        <p><b>metric</b> - this represents the aggregated amount/value for records
          filter by the aggregate es query</p>
        <p><b>pie</b> - this represents the aggregated data on grouping. This is can
          be used to represent any line graph, bar graph, pie chart or donuts</p>
        <p><b>line</b> - this graph/chart is data representation on date histograms
          or date groupings</p>
        <p><b>perform</b> - this chart represents groping data as performance-wise.</p>
        <p><b>table</b> - represents a form of plots and value with headers as grouped
          on and list of its key, values pairs.</p>
        <p><b>xtable -</b> represents an advanced feature of the table, it has additional
          capabilities for dynamic adding header values.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">valueType</td>
      <td style="text-align:left">In any case of data, the values which are sent to plot might be a percentage,
        sometimes an amount and sometimes it is just a count. In order to represent
        them and differentiate the numbers from the amount from percentage, this
        field is used to indicate the type of value that this Visualization will
        be sending.</td>
    </tr>
    <tr>
      <td style="text-align:left">action</td>
      <td style="text-align:left">
        <p>Some of the visualizations are not just aggregating on data source. There
          might be some cases where we have to do a post aggregation computation.
          For Example, in the case of Top 3 Performing ULBs, the Target and Total
          Collection is obtained and then the percentage is calculated.</p>
        <p>In these kinds of cases, what is the action that has to be performed on
          that data obtained, is defined in this parameter.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">documentType</td>
      <td style="text-align:left">The type of document upon which the query has to be executed is defined
        here.</td>
    </tr>
    <tr>
      <td style="text-align:left">drillChart</td>
      <td style="text-align:left">
        <p>If there is a drill down on the visualization, then the code of the Drill
          Down Visualization is added here.</p>
        <p>This will be used by Client Service to manage drill-downs</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">aggregationPaths</td>
      <td style="text-align:left">All the queries will be having Aggregation names in it. In order to fetch
        the value out of each Aggregation Responses, the name of the aggregation
        in the query will be an easy bet. These aggregation paths will have the
        names of Aggregation in it.</td>
    </tr>
    <tr>
      <td style="text-align:left">_comment</td>
      <td style="text-align:left">In order to display information on the &#x201C;i&#x201D; symbol of each
        visualization, Visualization Information is maintained in this field.</td>
    </tr>
  </tbody>
</table>

2. Master Dashboard Configuration

Master Dashboard Configuration is the main configuration that defines which Dashboards that are to be painted on the screen. 

It includes all the Visualizations, their groups, the charts which comes within them and even their dimensions as what should be their height and width.

![Figure 7](../../../../.gitbook/assets/116.png)

[Click here for an example configuration](https://github.com/egovernments/configs/blob/master/egov-dss-dashboards/dashboard-analytics/MasterDashboardConfig.json)

<table>
  <thead>
    <tr>
      <th style="text-align:left"><b>Parameter Name</b>
      </th>
      <th style="text-align:left"><b>Description</b>
      </th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">name</td>
      <td style="text-align:left">Name of the Dashboard which has to be displayed as Page Heading</td>
    </tr>
    <tr>
      <td style="text-align:left">id</td>
      <td style="text-align:left">Unique Identifier of the Dashboard which should be used later for Querying
        each of these Visualizations</td>
    </tr>
    <tr>
      <td style="text-align:left">isActive</td>
      <td style="text-align:left">Active Indicator which can be used to quickly disable a dashboard if required.</td>
    </tr>
    <tr>
      <td style="text-align:left">style</td>
      <td style="text-align:left">Style of the Dashboard. Whether it should be a linear one or a tabbed
        one. This information is maintained in this parameter.</td>
    </tr>
    <tr>
      <td style="text-align:left">visualizations</td>
      <td style="text-align:left">The list of visualizations that are to be displayed in the Dashboard is
        listed out here.</td>
    </tr>
    <tr>
      <td style="text-align:left">visualizations.row</td>
      <td style="text-align:left">The row identifier for each Visualization are mentioned here</td>
    </tr>
    <tr>
      <td style="text-align:left"><a href="http://visualizations.name/">visualizations.name</a>
      </td>
      <td style="text-align:left">The name of an individual visualization is added here</td>
    </tr>
    <tr>
      <td style="text-align:left">visualizations.vizArray</td>
      <td style="text-align:left">The list of Charts within the Visualization is specified in this list.</td>
    </tr>
    <tr>
      <td style="text-align:left"><a href="http://visualizations.vizarray.id/">visualizations.vizArray.id</a>
      </td>
      <td style="text-align:left">Group of Charts is given an ID to have a placement on the Dashboard. This
        unique identifier is maintained in this field.</td>
    </tr>
    <tr>
      <td style="text-align:left"><a href="http://visualizations.vizarray.name/">visualizations.vizArray.name</a>
      </td>
      <td style="text-align:left">Group of Charts is given a name that can be displayed on the group on
        Dashboard in that row.</td>
    </tr>
    <tr>
      <td style="text-align:left">visualizations.vizArray.dimensions</td>
      <td style="text-align:left">Each of these group of charts is given a dimension based on which they
        are placed in a specific row in a dashboard</td>
    </tr>
    <tr>
      <td style="text-align:left">visualizations.vizArray.vizType</td>
      <td style="text-align:left">
        <p>As there are multiple charts grouped into one visualization, the type
          of Visualization needs to be specified in order to indicate to the client
          application what goes inside each of these visualizations and charts inside
          them</p>
        <p>vizType used for any other dashboards:- metric-collection, chart, performing-metric</p>
        <p>metric-collection:- Used to specify the type as single or group of metric
          chart type</p>
        <p>2. performing-metric:- Used perform chart type</p>
        <p>3. chart:- Used chart type for pie, donut, table, bar, horizontal bar,
          line</p>
        <p>vizType used for the Home page:- collection, module</p>
        <p>collection: used in UI style as full width</p>
        <p>2. module: used in UI style for specific width.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>visualizations.vizArray.noUnit</p>
        <p>visualizations.vizArray.isCollapsible</p>
        <p>visualizations.vizArray.ref</p>
      </td>
      <td style="text-align:left">
        <p>The value types of these charts are different. Some are numbers, some
          are amounts, some are percentage.</p>
        <p>In the case of amounts, there is a requirement to display in Lakhs, Crores
          and Units. In order to indicate the client application whether to display
          these units or not, we have this boolean to control that</p>
        <p>The value type is for card/visualisation collapsible as boolean values.</p>
        <p>This object contains url (as mandatory), logoUrl (optional), type(optional).</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">visualizations.vizArray.charts</td>
      <td style="text-align:left">The list of individual charts inside a Visualization Group is maintained
        in this array list</td>
    </tr>
    <tr>
      <td style="text-align:left"><a href="http://visualizations.vizarray.charts.id/">visualizations.vizArray.charts.id</a>
      </td>
      <td style="text-align:left">Individual Chart Number Identifier to indicate the uniqueness of Charts</td>
    </tr>
    <tr>
      <td style="text-align:left"><a href="http://visualizations.vizarray.charts.name/">visualizations.vizArray.charts.name</a>
      </td>
      <td style="text-align:left">Name of the Chart which can be a header label for Charts within a Visualization</td>
    </tr>
    <tr>
      <td style="text-align:left">visualizations.vizArray.charts.code</td>
      <td style="text-align:left">Code of the Chart is the indicator that has to be sent to Server Side
        to get the data for representing the Visualization.</td>
    </tr>
    <tr>
      <td style="text-align:left">visualizations.vizArray.charts.chartType</td>
      <td style="text-align:left">
        <p>Type of Chart which has to represent the data result set that is obtained
          is specified here</p>
        <p>chartType:- bar, horizontalBar, line, donut, pie, metric, table</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">visualizations.vizArray.charts.filters</td>
      <td style="text-align:left">Filters that can be applied to the Visualization and what are the fields
        which are filterable are mentioned here.</td>
    </tr>
    <tr>
      <td style="text-align:left">visualizations.vizArray.charts.headers</td>
      <td style="text-align:left">In some cases, there are headers which can be a title or additional information
        for the Chart Data which gets represented. This field is kept open to accommodate
        the information which can be sent along with the Chart Data in itself.</td>
    </tr>
  </tbody>
</table>

3. Role Dashboard Mappings Configuration

Master Dashboard Configuration which was explained earlier hold the list of Dashboards that are available. Given the instance where Role Action Mapping is not maintained in the Application Service, this configuration will act as Role - Dashboard Mapping Configuration 

In this, each Role is mapped against the Dashboard which they are authorized to see

This was used earlier when the Role Action Mapping of eGov was not integrated. Later, when the Role Action Mapping started controlling the Dashboards to be seen on the client-side, this configuration is just used to enable the Dashboards for viewing. 

![Figure 8](../../../../.gitbook/assets/119.png)

[Click here for an example configuration](https://github.com/egovernments/configs/blob/master/egov-dss-dashboards/dashboard-analytics/RoleDashboardMappingsConf.json)

| **Parameter Name** | **Description** |
| :--- | :--- |
| roles | List of Roles that are available in the system |
| roles.\_comment | Role Description and comment on why does this role has an entry in this configuration and sums up the summary as to what are the things that are to be enabled. |
| roles.roleId | Unique Identifier of the Role for which Access is being given |
| roles.roleName | Name of the Role for which the access is being given |
| roles.isSuper | Boolean flag which defines whether the Role is a Super User or not |
| roles.orgId | Organization to which the Role belongs to |
| roles.dashboards | List of Dashboards that are enabled for the Role |
| [roles.dashboards.name](http://roles.dashboards.name/) | Name of the individual Dashboard which has been enabled |
| [roles.dashboards.id](http://roles.dashboards.id/) | Identifier of the individual Dashboard which has been enabled |

## Adding Configurations <a id="Adding-Configurations"></a>

Adding Roles and Dashboards :

To add a new role, RoleDashboardMappingsConf.json \(**roles** node\) configuration file has to be modified as below 

{% hint style="info" %}
Note: Any number of roles & dashboards can be added    
{% endhint %}

Below as in Figure 9. is a sample to add a new role object, new dashboard object 

![Figure 9](../../../../.gitbook/assets/120.png)

To add a new dashboard, MasterDashboardConfig.json \(**dashboards** node\) has to be modified as below in Figure 10.

{% hint style="info" %}
Note: dashboards array add a new dashboard as given below
{% endhint %}

![Figure 10](../../../../.gitbook/assets/121.png)

## Adding Visualizations in existing Dashboard

To add new visualisations, again MasterDashboardConfig.json \(**vizArray** node\) has to be modified as below as shown in Figure 11.

Note: vizArray is to hold multiple visualizations

![Figure 11](../../../../.gitbook/assets/122.png)

## Adding charts for visualizations

To add a new chart, chartApiConf.json has to be modified as shown below.  A new chartid has to be added with the chart node object.

**Metric chart Sample as shown in Figure 12.**

![Figure 12](../../../../.gitbook/assets/123.png)

**Pie chart Sample as shown in Figure 13.**

![Figure 13](../../../../.gitbook/assets/124.png)

**Line chart Sample as shown in Figure 14.**

![Figure 14](../../../../.gitbook/assets/125.png)

\*\*\*\*

**Table  chart Sample:** This chart comes **in** 2 kind - table and xtable.

table \(as shown in Figure 15.\) type allows to added aggregated fields added as available in the query keys, hence to extract the values based on the key, **aggegationPaths** needs to add along with their data type as in **pathDataTypeMapping**.

![Figure 15](../../../../.gitbook/assets/126.png)

xtable\(as shown in Figure 16.\) type allows to add multiple computed fields with the aggregated fields dynamically added.

To add multiple computed columns, **computedFields** \[\] where actionName \(IComputedField&lt;T&gt; interface\), fields \[\] names as in existing in query key, newField as name to appear for computation must be defined.

![Figure 16](../../../../.gitbook/assets/127.png)

[https://github.com/egovernments/configs/blob/master/egov-dss-dashboards/dashboard-analytics/ChartApiConfig.json](https://github.com/egovernments/configs/blob/master/egov-dss-dashboards/dashboard-analytics/ChartApiConfig.json) for the full configuration in detail.

Steps to create charts and visualise are:

* Create/Add a chart in chartApiConf.json
* Add a visualization for the existing dashboard in MasterDashboardConfig.json  as defined above.
* Or in order to create/add  a new dashboard create the dashboard in MasterDashboardConfig.json and create a role in RoleDashboardConfig.json

**Configuration Changes for DrillThrough :**

 1. Example Drill through in Ward table in Property Dashboard.

wardDrillDown is the visualization code for PT Drill Down. kind is the attribute that shows the type of visualization code. Apart from two things all the attributes are common.

![](../../../../.gitbook/assets/128.png)

 2. Example Drill through in ComplaintList table in PGR Dashboard.

complaintDrillDown is the visualization code for PGR Drill Down.

![](../../../../.gitbook/assets/129.png)

The above complaintDrillDown visualization code called in the drill chart parameter.

![](../../../../.gitbook/assets/130.png)







> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)\_\_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_ ](https://egov.org.in/)_is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
