# Building New Dashboards

## Overview <a id="Overview"></a>

This documentation talks about building a new dashboard in the DSS and also it defines the configurations required for the analytics service. Analytics microservice which is responsible for building, fetching, aggregating, and computing the data on ElasticSearch to a consumable data response. Which shall be later used for visualizations and graphical representations.

## Pre-requisites <a id="Pre-requisites"></a>

Before you proceed with the configuration, make sure the following pre-requisites are met -

* Prior Knowledge on JSON
* Prior Knowledge on Elasticsearch Query Language
* Prior Knowledge on Kibana
* DSS setup

## Adding New Dashboard Configurations

## Key Functionalities

1. Adding new Roles for Dashboards
2. Adding a new Dashboard
3. Adding new Visualizations in existing Dashboard
4. Adding new charts for visualizations :

### **1. Adding Roles and Dashboards :**

* To add a new role, We have to make changes in the RoleDashboardMappingsConf.json \(**roles** node\) configuration file has to be modified as below. In the roles array, every JSON object is unique based on the id. The name of the role is defined in the roleName attribute.
* If we want to assign any dashboard to a particular role, Add the id and name of the dashboard in the dashboards array. This dashboard id is unique and it’s referred to as the MasterDashboardConfig.json file configuration.

{% hint style="info" %}
Any number of roles & dashboards can be added
{% endhint %}

Below is a sample to add a new role object

![](../../../../.gitbook/assets/image-20201021-142505.png)

**2. Adding a new Dashboard**

* To add a new dashboard, We have to make changes in the MasterDashboardConfig.json \(**dashboards** node\) that has to be modified as below.
* Add the new JSON object in the dashboards array. Add the dashboard name in the name attribute, Id should be unique, which is used for assigning a role for the dashboard. We will talk about visualizations below.

{% hint style="info" %}
Dashboards array add a new dashboard as given below
{% endhint %}

![](../../../../.gitbook/assets/image-20201021-142630%20%281%29%20%287%29%20%285%29.png)

### **3. Adding new Visualizations in existing Dashboard**

* To add new visualizations, We have to make changes again in the MasterDashboardConfig.json \(**vizArray** node\) that has to be modified as below. Add the visualization name to the name attribute. We will add all the visualizations in the vizArray array.vizArray will contain the name of the visualization, vizType as visual type, noUnit, and charts.
* charts array contains chart API configuration query details. The id is referred to as the chartapiconfig.json file’s key to fetch the required data from elastic search’s index. And the name attribute is referred to as the name of the chart in localization.

![](../../../../.gitbook/assets/image-20201021-164344.png)

{% hint style="info" %}
vizArray is to hold multiple visualizations![](blob:https://digit-discuss.atlassian.net/4bcc3dff-7ba9-4b79-97b6-9c232f286a37#media-blob-url=true&id=0805fa3a-3b2f-4719-94a8-8cc08340fa38&collection=contentId-772178112&contextId=772178112&mimeType=image%2Fpng&name=image-20201021-164344.png&size=27448&width=474&height=468)
{% endhint %}

### 4.Adding charts for visualizations

* To add a new chart, chartApiConf.json has to be modified as shown below.  A new chartid \(key of the JSON\) has to be added with the chart node object. In the chartid JSON contains the chart name, chart type, valueType, documentType, aggregationPaths and queries attribute.
* Types of the chart: **Metric**, **Pie**, **Line**, **Table,** and **xtable**
* AggregationPaths: Query result will take from this path.
* valueType: Based on the value type result will be shown in the UI. Different types of valueType are **Amount, percentage,** and **number.**
* queries array will contain the information of the module, requestQueryMap \(request param of the API\), dateRefField \(Based on this field date data will be filtered\), indexName, and aggrQuery. We can add multiple modules queries in a single chart.

![](../../../../.gitbook/assets/image-20201021-171351.png)

{% hint style="info" %}
For more information please refer the reference documents listed below.
{% endhint %}

## Reference Docs <a id="Reference-Docs"></a>

### Doc Links <a id="Doc-Links"></a>

| **Title** | **Link** |
| :--- | :--- |
| DSS Backend Configuration Manual | [DSS Backend Configuration Manual](https://digit-discuss.atlassian.net/wiki/spaces/EPE/pages/117244081/DSS+Backend+Configuration+Manual) |
| DSS Dashboard - Technical Document for UI | [https://digit-discuss.atlassian.net/wiki/spaces/EPE/pages/283017217/DSS+Dashboard+-+Technical+Document+for+UI](https://digit-discuss.atlassian.net/wiki/spaces/EPE/pages/283017217/DSS+Dashboard+-+Technical+Document+for+UI) |
| DSS Technical Documentation | [DSS Technical Documentation](https://digit-discuss.atlassian.net/wiki/spaces/EPE/pages/118521886/DSS+Technical+Documentation) |

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)​](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation](https://egov.org.in/) is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).

