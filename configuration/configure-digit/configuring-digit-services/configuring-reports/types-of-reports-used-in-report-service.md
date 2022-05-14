# Types Of Reports Used In Report Service

### Overview <a href="#overview" id="overview"></a>

Configuring Report for a module requires adding the required report configuration as per the standard format and with the minimum development time.

UI can have different types of filters such as date, dropdown etc.. and even the sum of a column can also be easily displayed in UI. Pagination and downloading the report in pdf format, xls format is already present in the report UI.

Type of Reports which can be configured :

1. Count of applications
2. Statewide collections
3. Application status
4. Cancelled receipts
5. Migrated records / Data entry records

Limitation of this framework is for reports having requirements with complex queries with multiple joins as the report uses the query to fetch the data from the database, It is resource-intensive and response might be slow in those scenarios.

### Pre-requisites <a href="#pre-requisites" id="pre-requisites"></a>

Before you proceed with the configuration, make sure the following pre-requisites are met -

* User with permissions to edit the git repository to add the report configuration
* User with permissions to add action and role action in the mdms

### Key Functionalities <a href="#key-functionalities" id="key-functionalities"></a>

* Showcase the data in the required and cleaner format.
* The UI is rendered with the help of configuration in the report and there is no extra effort in building UI for different reports.
* For Implementation specific report requirements, customization is easy and turn around time is less.

### Deployment Details <a href="#deployment-details" id="deployment-details"></a>

1. After adding the new report/ editing existing report configuration in the respective module, the report service needs to be restarted.

### Configuration Details <a href="#configuration-details" id="configuration-details"></a>

1. Create a reports.yml file and add report configuration as per standard format.
2. Add the action and role action in the mdms.
3. Add the github raw path of the report.yml file in the report.config file

### Reference Docs <a href="#reference-docs" id="reference-docs"></a>

#### Doc Links <a href="#doc-links" id="doc-links"></a>

|                           |                                                                                                                                                                                                                |
| ------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Title**                 | **Link**                                                                                                                                                                                                       |
| Sample report.yml file    | [![](https://github.githubassets.com/favicon.ico)pt-reports.yml](https://github.com/egovernments/ukd-rainmaker-customization/blob/master/configs/reports/configs/pt-reports.yml)                               |
| Sample report.config file | [https://github.com/egovernments/ukd-rainmaker-customization/blob/master/configs/reports/report.config](https://github.com/egovernments/ukd-rainmaker-customization/blob/master/configs/reports/report.config) |

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)​](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation](https://egov.org.in/) is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).
