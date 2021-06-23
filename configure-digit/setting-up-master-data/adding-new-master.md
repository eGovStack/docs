# Adding New Master

## Overview

For creating a new master in MDMS, create the JSON file with the master data and configure the newly created master in the master config file.

## Pre-requisites

Before proceeding with the configuration, make sure the following pre-requisites are met -

* User with permissions to edit the git repository where MDMS data is configured.

## Deployment Details

After adding the new master, the MDMS service needs to be restarted to read the newly added data.

## Configuration Details

**Creating Master JSON**  
The new JSON file needs to contain 3 keys as shown in the below code snippet.  
The new master can be created for Statewide or ULB wise. Tenant id and config in the master config file determines this.

```text
{
  "tenantId": "< TENANT ID >",
  "moduleName": "< MODULE NAME >",
  "< MASTER NAME >": []
}
```

**Configuring the master config file**  
The Master config file is structured as below. Each key in the Master config is a module and each key in the module is a master.

```text
{
  "<module1>":{
    "<master1>":{},
    "<master2>":{},
    ...
  },
  "<module2>":{
    <master3>:{},
    <master4>:{},
    ...
  },
  ...
}
```

Each master contain the following data and keys are self-explanatory

```text
"master":{
    "masterName": "<>",
    "isStateLevel": true,
    "uniqueKeys": []
}
```

## Reference Docs

### Doc Links

| **Title** | **Link** |
| :--- | :--- |
| Sample Master file | [https://github.com/egovernments/playground-mdms-data/blob/master/data/pg/PropertyTax/ConstructionType.json](https://github.com/egovernments/playground-mdms-data/blob/master/data/pg/PropertyTax/ConstructionType.json) |
| Sample Master configuration | [https://github.com/egovernments/playground-mdms-data/blob/081a232c26be11a9d803d4490e01d49a7e35985c/master-config.json\#L561](https://github.com/egovernments/playground-mdms-data/blob/081a232c26be11a9d803d4490e01d49a7e35985c/master-config.json#L561) |

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation ](https://egov.org.in/)is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).

