---
description: Master Data Management System
---

# MDMS

Master Data Management Service

One of the applications in the eGov core group of services aims to reduce the time spent by developers on writing codes to store and fetch master data \( primary data needed for module functionality \) which doesn’t have any business logic associated with them. Instead of writing APIs, creating tables in every different service to store and retrieve data that is seldom changed MDMS service keeps them at a single location for all modules and provides data on will with the help of no more than three lines of configuration.

**Requirements:**

1. Prior Knowledge of Java/J2EE.
2. Prior Knowledge of Spring Boot.
3. Prior Knowledge of REST APIs and related concepts like path parameters, headers, JSON etc.
4. Prior knowledge of Git.
5. Advanced knowledge on how to operate JSON data would be an added advantage to understand the service.

**FUNCTIONALITY:**

The mdms service takes the data from a set of json files in the provided location, it can either be an online location \(readable json files from online\) or an offline \(json files stored in local memory\). The application starts by reading all the json files provided they are in the prescribed format and stores the data in a map were the tenantID of the file serves as a key and a map of the master data name and details as values.

Once the data is stored in the map the same can be retrieved by making an API request to the mdms service. Filters can be applied in the request to retrieve data based on some values in existing fields of json.

**SETUP AND USAGE:**

The [**Application**](https://github.com/egovernments/egov-services/tree/master/core/egov-mdms-service) is present among the core group of applications available in the eGov-services git repository. The spring boot application needs **lombok** extension added in your IDE to load it. Once the application is up and running API requests can be posted to the url and ids can be generated.

\*\*in case of intellij the plugin can be installed directly, for eclipse the lombok jar location has to be added in eclipse.ini file in this format **-javaagent:lombok.jar**.

For the API information please refer the swagger yaml

GOTO : [https://editor.swagger.io/](https://editor.swagger.io/) and click on file -&gt; import url

Then add the raw url of the API doc in the pop up.

[https://raw.githubusercontent.com/egovernments/egov-services/master/docs/mdms/contract/v1-0-0.yml](https://raw.githubusercontent.com/egovernments/egov-services/master/docs/mdms/contract/v1-0-0.yml)

Incase the url is unavailable, please go to the [docs folder](https://github.com/egovernments/egov-services/tree/master/docs) of egov-services git repo and find the yaml for egov-filestroe.

**CONFIGURATIONS AND STRUCTURE:**

The config json files to be written should follow the listed rules

1. The config files should have json extension .  
2. The file should mention the tenantId, modulename and the master name first before defining the data. **{**

   **"tenantId": "pb",**

**"moduleName": "BillingService",**

**"{$MasterName}":\[ \]**

**}**

The master name in the example should be replaced by the actual name of the data. Then the following array will contain the data in it.

Example of a data set containing business-service master of billing-service module, which is a state level data and applies to all tenants.

The tenant Id value “pb” indicates that the data is state level for punjab.

The data belong to the module “BillingService”

{

"tenantId": "pb",

"moduleName": "BillingService",

"BusinessService": \[

```text
{

  "businessService": "PropertyTax",

  "code": "PT",

  "collectionModesNotAllowed": \[ "DD" \],

  "partPaymentAllowed": true,

  "isAdvanceAllowed": true,

  "isVoucherCreationEnabled": true

}
```

\]

}

