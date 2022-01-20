# Finance Service Configuration

### **Overview** <a href="#overview" id="overview"></a>

This document describes the steps to be followed to set up a new instance of Finance. When a new state or city is to be set up, there are some activities to be executed in a defined order. Setting up an instance of an application server and configuration changes etc are a few of the key activities.

### **Technical Prerequisites** <a href="#technical-prerequisites" id="technical-prerequisites"></a>

* Prior Knowledge of Java/J2EE.
* Prior Knowledge of Spring and Hibernate
* Prior knowledge of Maven
* Prior knowledge of Git.

### **Hardware/Software Prerequisites** <a href="#hardware-software-prerequisites" id="hardware-software-prerequisites"></a>

* Maven v3.2.x
* PostgreSQL v9.6
* [Customized Wildfly Image](https://github.com/egovernments/Train-InfraOps/tree/master/dockerfiles/wildfly)
* Git 2.8.3
* JDK 8 update 112 or higher
* Create subdomains under the main domain for each of the cities that are to be set up
* Create a schema per city in the database

### **Configurations and Setup** <a href="#configurations-and-setup" id="configurations-and-setup"></a>

The [Co-existence repository](https://github.com/egovernments/egov-coexistence) is the base repository for the finance product and the client-specific data needs to be defined in the [Client implementation repository](https://github.com/egovernments/eGov-Punjab-Implementation/tree/punjab-financeerp-impl)

#### **How to set up a client implementation repository** <a href="#how-to-set-up-a-client-implementation-repository" id="how-to-set-up-a-client-implementation-repository"></a>

1. Fork and create a client implementation repository from [Client implementation repository](https://github.com/egovernments/eGov-Punjab-Implementation/tree/punjab-financeerp-impl) to keep client-specific data and configurations.
2. Any configurations and data specific to the client should be added in the client repository.

#### **Application Configuration** <a href="#application-configuration" id="application-configuration"></a>

* The default application configurations of the finance service are present in the [application configuration](https://github.com/egovernments/egov-coexistence/blob/master/egov/egov-egi/src/main/resources/config/application-config.properties) file. To enable or disable any feature, either update the values in the [application configuration](https://github.com/egovernments/egov-coexistence/blob/master/egov/egov-egi/src/main/resources/config/application-config.properties) file or the [override configuration](https://github.com/egovernments/Train-InfraOps/blob/master/helm/charts/business-services/egov-finance/templates/override-configmap.yaml) file.
* The [override configuration](https://github.com/egovernments/Train-InfraOps/blob/master/helm/charts/business-services/egov-finance/templates/override-configmap.yaml) is the template and the values for the template are present either in the [finance service values](https://github.com/egovernments/Train-InfraOps/blob/master/helm/charts/business-services/egov-finance/values.yaml) yaml file or in the environment named yaml file. The [finance service values](https://github.com/egovernments/Train-InfraOps/blob/master/helm/charts/business-services/egov-finance/values.yaml) yaml is the common file to override the default values and the changes made to this file are applicable for all environments (dev, qa, uat, prod etc).
* Any specific configuration change is required for any specific environment then update the environment named yaml file.

Sample environment named yaml files for your reference

```
https://github.com/egovernments/Train-InfraOps/blob/master/helm/environments/qa.yaml
https://github.com/egovernments/Train-InfraOps/blob/master/helm/environments/uat.yaml
```

#### **Database configuration** <a href="#database-configuration" id="database-configuration"></a>

Add or update the db url in the [environment specific](https://github.com/egovernments/Train-InfraOps/blob/master/helm/environments/qa.yaml) file using the below property

```
erp-db-url: "jdbc:postgresql://egov-dev-db.ctm6jbmr5mnj.ap-south-1.rds.amazonaws.com:5432/finance_qa_db"
```

Update the db username and password, which are configured in the environment named secrets yaml file.

For example, for the qa environment, update the qa-secrets.yaml

```
secrets:
        db:
            username: <username value> 
            password:  <password value>
```

#### **Set up a schema-based multi-tenant database** <a href="#set-up-a-schema-based-multi-tenant-database" id="set-up-a-schema-based-multi-tenant-database"></a>

Finance co-existence service uses schema-based multi-tenancy, this means there will be one schema present for a city. The following are the configuration changes to set up this kind of database.

* Enable multi-tenancy by enabling the following property

```
multitenancy: true  
```

* Each ULB is enabled by adding a schema name and domain name. Schema names should follow a naming standard, It should be the same as that of the city name.
* Each ULB can be configured by adding an entry like **tenant.\<domain\_name>=schema\_name (city\_name)**
* The default tenants are configured in the [finance service yaml](https://github.com/egovernments/Train-InfraOps/blob/master/helm/charts/business-services/egov-finance/values.yaml) file using the below configuration.

```
tenants: |
 tenant.citya.egovernments.org=citya
 tenant.cityb.egovernments.org=cityb
```

* To override and have separate tenants for a specific environment then update the environment-specific file like below.

```
FinanceTenants: |
 tenant.citya.egovernments.org=citya
 tenant.cityb.egovernments.org=cityb
```

* Here **citya.egovernments.org, cityb.egovernments.org** are the domains and **citya, cityb** are the schemas/tenants.

Example [environment specific configuration](https://github.com/egovernments/Train-InfraOps/blob/master/helm/environments/qa.yaml) file for your reference.

* Update the domainurl in the eg\_city table.
* Domain URL value should be the same as configured tenant domain\_name Ex:

```
For citya, domain url should be citya.egovernments.org
For cityb, domain url should be cityb.egovernments.org 
```

#### **Database migration settings** <a href="#database-migration-settings" id="database-migration-settings"></a>

The default database migration configurations are present in the [application configuration](https://github.com/egovernments/egov-coexistence/blob/master/egov/egov-egi/src/main/resources/config/application-config.properties) file.

```
#Enable/Disable flyway migration
db.migration.enabled=true

#Enable/Disable flyway migration validation
db.flyway.validateon.migrate=false

#Enable/Disable repairing of flyway migration checksum
db.flyway.migration.repair=false

#Various flyway migration sql script file paths
db.flyway.main.migration.file.path=classpath:/db/migration/main/
db.flyway.sample.migration.file.path=classpath:/db/migration/sample/
db.flyway.tenant.migration.file.path=classpath:/db/migration/%s/
db.flyway.statewide.migration.file.path=classpath:/db/migration/statewide/

#Enable/Disable to run migration sql's inside "statewide" migration folder (resources/db/migration/statewide)
statewide.migration.required=false

#Schema name where statewide migration to be executed, value must be your default schema name (see default.schema.name)
statewide.schema.name=generic

#Enable/Disable dev mode, this must be set to false in all non dev environments
dev.mode=false
```

Override the default values by updating the properties either in the [finance service values](https://github.com/egovernments/Train-InfraOps/blob/master/helm/charts/business-services/egov-finance/values.yaml) yaml file or the environment-specific yaml file. The following are different properties.

```
# Enable/Disable to execute the sample sql scripts.
dev_mode: false
# Enable/Disable flyway migration validation
db_flyway: true
#Enable/Disable to run migration sql's inside "statewide" migration folder (resources/db/migration/statewide)
statewide_migration: true
#Enable or Disable Multitenancy
multitenancy: true
```

#### System Integration User Details Configuration <a href="#system-integration-user-details-configuration" id="system-integration-user-details-configuration"></a>

Configure the following property either in the [finance service values](https://github.com/egovernments/Train-InfraOps/blob/master/helm/charts/business-services/egov-finance/values.yaml) yaml file or the environment-specific yaml file.

```
Systemintegration: |
 si.microservice.user=${si-microservice-user}
 si.microservice.password=${si-microservice-password}
 si.microservice.usertype=SYSTEM
 si.microservice.scope=read
 si.microservice.granttype=password
 
 env: |
  - name: si-microservice-password
    valueFrom:
      secretKeyRef:  
        name: egov-si-microservice
        key: si-microservice-password
  - name: si-microservice-user
    valueFrom:
      secretKeyRef:  
        name: egov-si-microservice
        key: si-microservice-user
```

* Add one user in the system for system integration - SIFINANCE mapped with role SYS\_INTEGRATOR\_FINANCE by using the user service createnovalidate API.
* Find the createnovalidate API details below

```
{
	"info": {
		"_postman_id": "81469f7c-793c-43b2-8e05-9ce6c8174cd4",
		"name": "SIUSER_Creation",
		"schema": "https://schema.getpostman.com/json/collection/v2.1.0/collection.json"
	},
	"item": [
		{
			"name": "createnovalidate",
			"request": {
				"method": "POST",
				"header": [
					{
						"key": "Content-Type",
						"value": "application/json"
					}
				],
				"body": {
					"mode": "raw",
					"raw": "{\n \"RequestInfo\": {\n   \"api_id\": \"1\",\n   \"ver\": \"1\",\n   \"ts\": null,\n   \"action\": \"create\",\n   \"did\": \"\",\n   \"key\": \"\",\n   \"msg_id\": \"\",\n   \"requester_id\": \"\",\n   \"auth_token\": \"12e8753e-099f-42cb-b2ec-402b10215610\"\n },\n \"User\": {\n  \"userName\": \"SIFINANCE\",\n  \"name\": \"SYS INTG FINANCE\",\n  \"gender\": \"Male\",\n  \"mobileNumber\": \"\",\n  \"active\": true,\n  \"type\": \"SYSTEM\",\n  \"password\": \"sifinance123@\",\n  \"tenantId\":\"pg.citya\",\n  \"roles\": [\n       {\n                   \"tenantId\": \"pg.citya\",\n                   \"code\": \"SYS_INTEGRATOR_FINANCE\",\n                   \"name\": \"System Integrator Finance\"\n               }\n   ]\n }\n}\n"
				},
				"url": {
					"raw": "https://egov-micro-qa.egovernments.org/user/users/_createnovalidate",
					"protocol": "https",
					"host": [
						"egov-micro-qa",
						"egovernments",
						"org"
					],
					"path": [
						"user",
						"users",
						"_createnovalidate"
					]
				},
				"description": "user create with no OTP validation"
			},
			"response": []
		}
	]
}
```

#### **Elastic Dashboard Configuration** <a href="#elastic-dashboard-configuration" id="elastic-dashboard-configuration"></a>

To enable or disable an event to push the bills and vouchers to the elastic search indexer the below need to be configured either in the [finance service values](https://github.com/egovernments/Train-InfraOps/blob/master/helm/charts/business-services/egov-finance/values.yaml) yaml file or the environment-specific yaml file.

```
finance: true
```

#### **File store Configuration** <a href="#file-store-configuration" id="file-store-configuration"></a>

Configure the following property either in the [finance service values](https://github.com/egovernments/Train-InfraOps/blob/master/helm/charts/business-services/egov-finance/values.yaml) yaml file or the environment-specific yaml file.

```
filestore: /tmp/egovfilestore
```

#### **Quartz Scheduler Configuration** <a href="#quartz-scheduler-configuration" id="quartz-scheduler-configuration"></a>

Configure the following property either in the [finance service values](https://github.com/egovernments/Train-InfraOps/blob/master/helm/charts/business-services/egov-finance/values.yaml) yaml file or the environment-specific yaml file.

```
scheduler: true
```

#### DIGIT integration configuration <a href="#digit-integration-configuration" id="digit-integration-configuration"></a>

Finance service reads data from multiple other DIGIT services. The following are the different services finance system reads data from. Update the domain URL of the respective service based on the service where it is running.

```
microservice: |
  egov.default.services.endpoint=https://egov-micro-dev.egovernments.org/
  egov.hrms.service.endpoint=http://egov-hrms.egov:8080/
  egov.accesscontrol.service.endpoint=http://egov-accesscontrol.egov:8080/
  egov.hr.masters.service.endpoint=http://hr-masters.egov:8080/
  egov.user.service.endpoint=http://egov-user.egov:8080/
  egov.common.masters.endpoint=http://egov-common-masters.egov:8080/
  egov.billing.service.endpoint=http://billing-service.egov:8080/
  egov.collection.service.endpoint=http://collection-services.egov:8080/
  egov.egf.master.service.endpoint=http://egf-master.egov:8080/
  egov.egf.instrument.service.endpoint=http://egf-instrument.egov:8080/
  egov.mdms.service.endpoint=http://egov-mdms-service.egov:8080/
  egov.indexer.service.endpoint=http://egov-indexer.egov:8080/
  egov.services.billing.service.bill.generate=billing-service/bill/v2/_fetchbill
  egov.filestore.service.endpoint=http://egov-filestore.egov:8080/
```

#### MDMS Configuration <a href="#mdms-configuration" id="mdms-configuration"></a>

* The following master data is present in the [MDMS repository](https://github.com/egovernments/egov-mdms-data).
  * Department
  * Designation
  * BusinessServiceMapping
  * TaxHeadMasterGlCodeMapping
  * InstrumentGLcodeMapping
  * AccountCodeTemplate
  * FinanceInstrumentStatusMapping
  * tenants
  * OnlineGLCodeMapping
* Define all the departments in the [Departments](https://github.com/egovernments/egov-mdms-data/blob/DEV/data/pb/common-masters/Department.json) json
* Define all the designations in the [Designations](https://github.com/egovernments/egov-mdms-data/blob/DEV/data/pb/common-masters/Designation.json) json
* Configure finance tenants in the [Citymodule](https://github.com/egovernments/egov-mdms-data/blob/DEV/data/pb/tenant/citymodule.json) json to enable finance module in the ULB.

```
{
      "module": "Finance",
      "code": "Finance",
      "tenants": [
        {
          "code": "pb.jalandhar"
        },
        {
          "code": "pb.nawanshahr"
        }
      ]
    },
```

* Define business services mapping in the [Business Service Mapping](https://github.com/egovernments/egov-mdms-data/blob/DEV/data/pb/FinanceService/BusinessServiceMapping.json) json to integrate different business services like Property Tax, Trade License and FireNOC etc with Finance and to post vouchers like demand and receipt vouchers. Enabling and disabling voucher posting for any service can be configured here.
* Define the Tax head and instrument glcode mappings in the [Account Head Mapping](https://github.com/egovernments/egov-mdms-data/blob/DEV/data/pb/FinanceService/AccountheadMapping.json) json. This file contains each tax head wise glcode mapping and each instrument wise glcode mappings.
* Different instrument statuses can be defined in the [Instrument Status Mapping](https://github.com/egovernments/egov-mdms-data/blob/DEV/data/pb/FinanceService/EgfInstrumentStatusMapping.json) json file.
* Different types of contractor bill templates are defined in the [AccountCode Template](https://github.com/egovernments/egov-mdms-data/blob/DEV/data/pb/FinanceService/AccountCodeTemplate.json) file. These templates will be used in the contractor bill creation screen to auto-populate the account codes.
* Service-wise glcode mapping for the online instrument type for the particular city is defined in the [Online Instrument Type](https://github.com/egovernments/egov-mdms-data/blob/DEV/data/pb/amritsar/FinanceService/OnlineInstrumentType.json) json.
* Define the business service wise bank account mappings in the [BankAccount Service Mapping](https://github.com/egovernments/egov-mdms-data/blob/DEV/data/pb/jalandhar/FinanceService/BankAccountServiceMapping.json) json file. These details to be configured city wise as the bank details are specific to a city.

MDMS serach url is configured in the [Application Configuration](https://github.com/egovernments/egov-coexistence/blob/master/egov/egov-egi/src/main/resources/config/application-config.properties) file.

#### Changes required to setup workspace in local machine <a href="#changes-required-to-setup-workspace-in-local-machine" id="changes-required-to-setup-workspace-in-local-machine"></a>

1. Setup Finance service workspace by following the instructions provided in [README](https://github.com/egovernments/egov-coexistence/blob/master/README.md).
2. After set up is done, make the changes to the host file in the local machine, by mapping the domain URLs with a local IP address and save the changes. Restart your local machine to make the host mapping effective.

```
$ vim /etc/hosts

127.0.0.1 egov-micro-dev.egovernments.org
```

### **Reference Docs**

|                                         |                                                                                                                       |
| --------------------------------------- | --------------------------------------------------------------------------------------------------------------------- |
| **Title**                               | **Link**                                                                                                              |
| API Contracts                           | [Voucher APIs](https://github.com/egovernments/egov-coexistence/blob/master/docs/voucher\_apis.yaml)                  |
| Co-existence finance code available     | [Co-existence repository](https://github.com/egovernments/egov-coexistence)                                           |
| Sample client implementation repository | [Punjab implementation repository](https://github.com/egovernments/eGov-Punjab-Implementation)                        |
| Configuring MDMS                        | [Configuring Master Data](https://digit-discuss.atlassian.net/wiki/spaces/DD/pages/644349987/Configuring+Master+Data) |
| Adding new service and CI/CD            | [CI/CD process](https://digit-discuss.atlassian.net/wiki/spaces/DOPS/pages/19333450/MS+-+Adding+new+service)          |

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)​](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation](https://egov.org.in) is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).
