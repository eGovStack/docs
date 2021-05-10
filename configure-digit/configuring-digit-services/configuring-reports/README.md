# Configuring New Reports

## Overview <a id="Overview"></a>

Through report service, useful data get shown for a specific module based on some given criteria like date, locality, financial year, etc.

For example, PT dump report of property tax service you have to select from date to date, financial year etc and based on the criteria we can see all the data full filling the criteria. In the response we see all the details of a property which is paid between the given from date and to date, if we selected financial year then we can see the property which is paid for that specific financial year.

## Pre-requisites <a id="Pre-requisites"></a>

Before you proceed with the configuration, make sure the following pre-requisites are met -

* User with permissions to edit the git repository where Reports are configured and knowledge on YAML. 
* Prior Knowledge of YAML.
* Prior Knowledge of SQL queries.
* Prior Knowledge of the relation between the tables for which module you are going to write a report.

## Key Functionalities <a id="Key-Functionalities"></a>

* User can write queries \(like SQL queries\) for fetching the real-time data to display in a UI application.
* User can apply filters like from date, to date, financial year, etc based on the report configuration.
* User can download the result in PDF and XLS format.
* User can select or deselect the columns user wants to see.
* User can choose the number of records he/she wants to see on a page.

## Deployment Details <a id="Deployment-Details"></a>

1. Once the changes have been done in the report configuration file we have to restart the report service so the report service will read the new configuration.

## Configuration Details <a id="Configuration-Details"></a>

* To add a new report first add the file path in the reportFileLocationsv1\[[https://raw.githubusercontent.com/egovernments/configs/DEV/reports/reportFileLocationsv1.txt\]](https://raw.githubusercontent.com/egovernments/configs/DEV/reports/reportFileLocationsv1.txt%5D) \(In this file, the path of the report configuration files get stored\).
  * &lt;Module Name&gt;=file:///work-dir/configs/reports/config/&lt;report file name&gt;.yml
  * ex: pgr=file:///work-dir/configs/reports/config/pgr-reports.yml
* Once file path is added in the file reportFileLocationsv1, go to the folder /configs/reports/config \[[![](https://github.githubassets.com/favicon.ico)https://github.com/egovernments/configs/tree/DEV/reports/config%5D. - Connect to preview](https://github.com/egovernments/configs/tree/DEV/reports/config%5D.) Create a new file and name the file what you have given in file reportFileLocationsv1.
* Write the report configuration. Once it is done commit those changes.
* Add the role and actions for the new report.
* Restart the MDMS and report service.

## Reference Docs <a id="Reference-Docs"></a>

### Doc Links <a id="Doc-Links"></a>

| **Title** | **Link** |
| :--- | :--- |
| [reportFileLocationsv1](https://raw.githubusercontent.com/egovernments/configs/DEV/reports/reportFileLocationsv1.txt) file | [https://raw.githubusercontent.com/egovernments/configs/DEV/reports/reportFileLocationsv1.txt](https://raw.githubusercontent.com/egovernments/configs/DEV/reports/reportFileLocationsv1.txt) |
| report config folder | [![](https://github.githubassets.com/favicon.ico)https://github.com/egovernments/configs/tree/DEV/reports/config - Connect to preview](https://github.com/egovernments/configs/tree/DEV/reports/config) |

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)​](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation](https://egov.org.in/) is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).

