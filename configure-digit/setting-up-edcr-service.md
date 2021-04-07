# Setting Up eDCR Service

## Overview

This document mainly covers all the steps that one needs to do for setting up a new instance of eDCR \(Development Control Regulations\). Say when a new State is to be set up, there are some activities to be executed in a defined order. Setting up an instance of an application server and configuring customer-specific rules, and data, etc are a few of the key activities.

* Centralized Server hosting all the ULBs within a state
* All ULBs access the software over API calls.
* Uniform code base supporting all the ULBs for the state. City-specific changes are maintained using client-specific implementation repositories.
* A separate schema for each ULB in the database.

## Prerequisites

* Prior Knowledge of Java/J2EE.
* Prior Knowledge of Spring and Hibernate
* Prior knowledge of Maven
* Prior knowledge of Git.
* Install the below version of the software in local machine
  * maven v3.2.x
  * PostgreSQL v9.6
  * [JBoss Wildfly v11.x](https://devops.egovernments.org/Downloads/wildfly/wildfly-11.0.0.Final.zip)
  * Git 2.8.3
  * JDK 8 update 112 or higher

## Configurations and Setup

eDCR Service repository will be used to define default rules. The statewide rules to be defined within the client implementation repository.

**How to set up a client implementation repository**

Branch out and create a eDCR service repository from [![](https://github.githubassets.com/favicon.ico)https://github.com/egovernments/eGov-dcr-service - Connect to preview](https://github.com/egovernments/eGov-dcr-service) master repository. Refer [![](https://github.githubassets.com/favicon.ico)https://github.com/egovernments/egov-dcr-client - Connect to preview](https://github.com/egovernments/egov-dcr-client) for the client implementation setup has been done.

After creating a client implementation repository, If you want to override rules processing for features, then create a project under egov directory like **egov-client-impl.**

The client-specific rules are configurable in the individual client implementation module. Here the rules are fetched by state wise, district wise, ULB wise, or grade-wise.

**How to override rule processing across the state for a feature**

The EG\_CITY table, master data is used to decide the rules.

1. If the rules are the same for a feature across the state then the filename must need to keep like Far\_{Client.id}.
2. Here client id nothing but a state name, the client.id need to update with the state name in **application-config-client.properties** file \(Available in [https://github.com/egovernments/egov-dcr-client/blob/master/egov/egov-client-impl/src/main/resources/config/application-config-client.properties](https://github.com/egovernments/egov-dcr-client/blob/master/egov/egov-client-impl/src/main/resources/config/application-config-client.properties)\) or in **egov-erp-override.properties** file\(Available in **Wildfly server** under **${HOME\_DIR}/wildfly-11.0.0.Final/modules/system/layers/base/org/egov/settings/main/config**\).
3. The client id used with the feature class name and configures in the properties file should match, then only the system will pick features and process otherwise it won't pick the file.
4. Eg: [https://github.com/egovernments/egov-dcr-client/blob/master/egov/egov-client-impl/src/main/java/org/egov/client/edcr/Far\_Client.java](https://github.com/egovernments/egov-dcr-client/blob/master/egov/egov-client-impl/src/main/java/org/egov/client/edcr/Far_Client.java) Here filename to be added as Far\_Assam.java for the Assam state rules.

**How to override rule processing district, city, and grade wise for a feature**

1. If the rules varying across district, city, and grade wise within a state then must need to follow the following naming conventions.
2. If the rules are varying from district to district, then the respective district-related rules need code under separate files with a filename like Far\_{District Name}. eg: Far\_Udalguri.
3. Similarly, if rules varying for city and grade wise then those respective rules need to code under separate files with a filename like Far\_{City Name}, Far\_{Grade}. eg: Far\_Dispur, Far\_Corp
4. The district, city, and grade information will be reading from the eg\_city table, so in this table need to update that information before starting the coding.
5. In a state, only for one or two cities if the rules are changing then need to override rules only for those cities in a separate file, for other all cities the default code will pick. Here default code is state level \(Far\_{Client id}\) configured one.

**Configuration Changes to setup State and Cities**

1. The state is configured by adding property **tenant.{domain\_name}=schema\_name \(state\_name\)** in egov-erp-override.properties**.**
2. Each new ULB is enabled by adding a schema name and domain name in egov-erp-override.properties file\(Available in **Wildfly server** under **${HOME\_DIR}/wildfly-11.0.0.Final/modules/system/layers/base/org/egov/settings/main/config**\). Schema names should follow a naming standard, It should be the same as that of the city name.
3. Each ULB can be configured by adding an entry like **tenant.{domain\_name}=schema\_name \(city\_name\)** in **egov-erp-override.properties** file.
4. Insert data into eg\_city, in the city table domain URL value should be the same as configured tenant domain\_name in the **egov-erp-override.properties**.

**Changes required for local machine workspace setup**

1. Setup your eDCR service workspace by following the instructions provided in [https://github.com/egovernments/eGov-dcr-service/blob/master/README.md](https://github.com/egovernments/eGov-dcr-service/blob/master/README.md)
2. After set up is done, the local ubuntu machine need to update the domain URLs in the host file which you are going to use for scrutinizing and fetching the plan.
3. Navigate to the root directory and from there open the host config file available in the location 'etc/hosts'. Map the domain URLs with a local IP address in the hosts file and save the changes.
4. Update settings in `standalone.xml` under **${HOME\_DIR}/wildfly-11.0.0.Final`/standalone/configuration`**
5. Add 'max-post-size' attribute with value 100mb in bytes in the below location,
6. &lt;server name="default-server"&gt; &lt;http-listener name="default" socket-binding="http" max-post-size="104857600" redirect-socket="https" enable-http2="true"/&gt; &lt;https-listener name="https" max-post-size="104857600"  socket-binding="https" security-realm="ApplicationRealm" enable-http2="true"/&gt; &lt;host name="default-host" alias="localhost"&gt; &lt;location name="/" handler="welcome-content"/&gt; &lt;http-invoker security-realm="ApplicationRealm"/&gt; &lt;/host&gt; &lt;/server&gt;

**MDMS Integration**

If you want to fetch master data from MDMS for following ApplicationType, ServiceType, OccupancyType, SubOccupancyType, Usages then the following configurations are needed,

{% hint style="info" %}
Enable fetch master data from MDMS by adding mdms.enable=true property in **application-config-client.properties** file \(Available in [https://github.com/egovernments/egov-dcr-client/blob/master/egov/egov-client-impl/src/main/resources/config/application-config-client.properties](https://github.com/egovernments/egov-dcr-client/blob/master/egov/egov-client-impl/src/main/resources/config/application-config-client.properties)\) or in **egov-erp-override.properties** file\(Available in **Wildfly server** under **${HOME\_DIR}/wildfly-11.0.0.Final/modules/system/layers/base/org/egov/settings/main/config**\).
{% endhint %}

{% hint style="info" %}
Add the property and update the MDMS hostname, mdms.host=[{](https://egov-micro-dev.egovernments.org/)HOST\_NAME} in **application-config-client.properties** file or **egov-erp-override.properties** file
{% endhint %}

{% hint style="info" %}
Add the property and update the MDMS search URL, mdms.searchurl=/egov-mdms-service/v1/\_search in **application-config-client.properties** file or **egov-erp-override.properties** file
{% endhint %}

{% hint style="info" %}
1. By default, the master data will be fetched from the database.
2. If you want to fetch from MDMS instead of the database then the above configurations are required.
{% endhint %}

{% hint style="info" %}
1. After setup is done APIs one must use state domain URL and in the contract tenantId of concern, the city has to be passed to scrutinize multiple cities.
2. One should not use the city domain URL to scrutinize or fetch plan if used that way, the response will be empty.
3. The tenantId used should follow {state\_name.city\_name} naming convention, then the state\_name passed in the request and city code in the state schema must be the same.
{% endhint %}

## References

| Title | Link |
| :--- | :--- |
| Design and Architecture | [Development Control Rules \(Digit-DCR\)](https://digit-discuss.atlassian.net/wiki/spaces/BPA/pages/49709173) |
| API Contracts | [https://github.com/egovernments/digit-bpa/blob/master/egov/egov-edcr/dcrasservice.yaml](https://github.com/egovernments/digit-bpa/blob/master/egov/egov-edcr/dcrasservice.yaml) |
| Repository the default rule processing code available | [https://github.com/egovernments/eGov-dcr-service](https://github.com/egovernments/eGov-dcr-service) |
| Sample client implementation repository | [https://github.com/egovernments/egov-dcr-client](https://github.com/egovernments/egov-dcr-client) |
| Configuring MDMS | [Configuring Master Data](https://digit-discuss.atlassian.net/wiki/spaces/DD/pages/644349987/Configuring+Master+Data) |

