# State Level Vs City Level Master

### Overview <a id="Overview"></a>

MDMS supports the configuration of data at different levels. While we enable a state there can be data that is common to all the ULB’s of the state and data specific to each ULB’s. The data further can be configured at each module level as state-specific or ULB’s specific.

### Pre-requisites <a id="Pre-requisites"></a>

Before you proceed with the configuration, make sure the following pre-requisites are met -

* Prior Knowledge of Java/J2EE.
* Prior Knowledge of Spring Boot.
* Prior Knowledge of REST APIs and related concepts like path parameters, headers, JSON, etc.
* Prior knowledge of Git.
* Advanced knowledge on how to operate JSON data would be an added advantage to understand the service.

### Key Functionalities <a id="Key-Functionalities"></a>

* State Level Masters are maintained in a common folder.
* ULB Level Masters are maintained in separate folders named after the ULB.
* Module Specific State Level Masters are maintained by a folder named after the specific module that is placed outside the common folder.

### Deployment Details <a id="Deployment-Details"></a>

* For deploying the changes\(adding new data, updating existing data or deletion\) in MDMS, the MDMS service needs to be restarted.

### Configuration Details <a id="Configuration-Details"></a>

**State Level Master Configuration**

* The common master data across all ULB’s and modules like department, designation, etc are placed under the **common-masters** folder which is under the tenant folder of the MDMS repository.

 ex: [**egov-mdms-data**](https://github.com/egovernments/egov-mdms-data)**/**[**data**](https://github.com/egovernments/egov-mdms-data/tree/DEV/data)**/**[**pb**](https://github.com/egovernments/egov-mdms-data/tree/DEV/data/pb)**/common-masters/** Here “**pb**” is the tenant folder name.

* The common master data across all ULB’s and are module-specific are placed in a folder named after each module. These folders are placed directly under the tenant folder. 

 ex: [**egov-mdms-data**](https://github.com/egovernments/egov-mdms-data)**/**[**data**](https://github.com/egovernments/egov-mdms-data/tree/DEV/data)**/**[**pb**](https://github.com/egovernments/egov-mdms-data/tree/DEV/data/pb)**/TradeLicense/** Here “**pb**” is the tenant folder name and “**TradeLicense**“ is the module name.

**ULB Level Master Configuration**

* Modules data that are specific to each ULB like boundary data, interest, penalty, etc are configured each ULBwise. There will be a folder per ULB under the tenant folder and all the ULB’s module-specific data are placed under this folder.

 ex: [**egov-mdms-data**](https://github.com/egovernments/egov-mdms-data)**/**[**data**](https://github.com/egovernments/egov-mdms-data/tree/DEV/data)**/**[**pb**](https://github.com/egovernments/egov-mdms-data/tree/DEV/data/pb)**/**[**amritsar**](https://github.com/egovernments/egov-mdms-data/tree/DEV/data/pb/amritsar)**/TradeLicense/** Here “**amritsar**“ is the ULB name and “**TradeLicense**“ is the module name. All the data specific to this module for the ULB are configured inside this folder.

### Reference Docs <a id="Reference-Docs"></a>

#### Doc Links <a id="Doc-Links"></a>

| **Title**  | **Link** |
| :--- | :--- |
|  State Level Common-Master Data |  [![](https://github.githubassets.com/favicon.ico)https://github.com/egovernments/egov-mdms-data/tree/DEV/data/pb/common-masters - Connect to preview](https://github.com/egovernments/egov-mdms-data/tree/DEV/data/pb/common-masters) |
|  State Level Module Specific Common-Master Data |  [![](https://github.githubassets.com/favicon.ico)https://github.com/egovernments/egov-mdms-data/tree/DEV/data/pb/TradeLicense - Connect to preview](https://github.com/egovernments/egov-mdms-data/tree/DEV/data/pb/TradeLicense) |
| ULB Specific Data | [![](https://github.githubassets.com/favicon.ico)https://github.com/egovernments/egov-mdms-data/tree/DEV/data/pb/amritsar - Connect to preview](https://github.com/egovernments/egov-mdms-data/tree/DEV/data/pb/amritsar) |

#### API List <a id="API-List"></a>

|  | **Link** |
| :--- | :--- |
| API Contract Reference  |  [https://raw.githubusercontent.com/egovernments/egov-services/master/docs/mdms/contract/v1-0-0.yml](https://raw.githubusercontent.com/egovernments/egov-services/master/docs/mdms/contract/v1-0-0.yml) |

