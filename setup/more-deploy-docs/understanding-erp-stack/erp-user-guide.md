# ERP User Guide

This section contains steps that are involved in the build and deploy the application.\
FAQ related to various deployment and development issues are discussed [here](https://digit-discuss.atlassian.net/wiki/spaces/FAQ/overview)

### Setup with auto-installer <a href="#setup-with-auto-installer" id="setup-with-auto-installer"></a>

* Clone the eGov repository (development is done on the develop branch).

`1$ mkdir -p ${HOME}/egovgithub && cd egovgithub 2$ git clone -b develop --single-branch <https://github.com/egovernments/egov-smartcity-suite.git>`

* First time setup which will install the stacks, build the source code, and deploys the artefact to Wildfly

`1$ cd ${HOME}/egovgithub/egov-smartcity-suite && make all`

* To install the prerequisites Phoenix stacks

`1$ cd ${HOME}/egovgithub/egov-smartcity-suite && make install`

* To build the source code base

`1$ cd ${HOME}/egovgithub/egov-smartcity-suite && make build`

* To deploy the artefact to WILDFLY

`1$ cd ${HOME}/egovgithub/egov-smartcity-suite && make deploy`

### Manual Setup Instruction <a href="#manual-setup-instruction" id="manual-setup-instruction"></a>

**Prerequisites**

* Install [maven v3.2.x](http://maven.apache.org/download.cgi)
* Install [PostgreSQL v9.4](http://www.postgresql.org/download/)
* Install [Elastic Search v2.4.x](https://download.elasticsearch.org/elasticsearch/elasticsearch/elasticsearch-2.4.1.zip)
* Install [Jboss Wildfly v10.x](https://devops.egovernments.org/Downloads/wildfly/wildfly-11.0.0.Final.zip)
* Install [Git 2.8.3](https://git-scm.com/downloads)
* Install [JDK 8 update 112 or higher](http://www.oracle.com/technetwork/java/javase/downloads)

**Database Setup**

1. Create a database and user in postgres
2. Create a schema called generic
3. Execute ALTER ROLE \<your\_login\_role> SET search\_path TO generic,public;

**Elastic Search Setup**

Elastic search server properties need to be configured in elasticsearch.yml under \<ELASTICSEARCH\_INSTALL\_DIR>/config`1## Your local elasticsearch clustername, DO NOT use default clustername 2cluster.name: elasticsearch-<username> 3## This is the default port 4transport.tcp.port: 9300 5`

NB: \<username> user name of the logged-in system, enter the below command in terminal to find the username.`1$ id -un`

**Building Source**

1. Clone the eGov repository (development is done on the develop branch.

`1$ mkdir egovgithub 2$ cd egovgithub 3$ git clone <https://github.com/egovernments/egov-smartcity-suite.git> 4$ git checkout develop`

1. Change directory to \<CLONED\_REPO\_DIR>/egov/egov-config/src/main/resources/config/ and create a file called egov-erp-\<username>.properties and enter the following values based on your environment config.

`1##comma separated list of host names 2elasticsearch.hosts=localhost 3elasticsearch.port=9300 4elasticsearch.cluster.name=elasticsearch-<username> 5`

If required, you can override any default settings available in /egov/egov-egi/src/main/resources/config/application-config.properties by overriding the value in egov-erp-\<username>.properties.

1. Change directory back to \<CLONED\_REPO\_DIR>/egov
2. Run the following commands. This will clean, compile, test, migrate the database and generate ear artefact along with jars and wars appropriately.

`1mvn clean package -s settings.xml -Ddb.user=<db_username> -Ddb.password=<db_password> -Ddb.driver=org.postgresql.Driver -Ddb.url=<jdbc_url>`

**Redis Server Setup**

By default eGov suit uses an embedded redis server (work only in Linux & OSx), to make the eGov suit work in Windows OS or if you want to run redis server as a standalone then follow the installation steps below.

1. Installing redis server on Linux

`1sudo apt-get install redis-server`

1. Installing redis server on Windows:- There is no official installable available for Windows OS. To install redis on Windows OS, follow the instruction given in [https://chocolatey.org/packages/redis-64](https://chocolatey.org/packages/redis-64)
2. Once installed, set the below property in egov-erp-override.properties or egov-erp-\<username>.properties.

`1## true by default 2redis.enable.embedded=false`

to control the redis server host and port use the following property values (only required if installed with non-default).`1## Replace <your_redis_server_host> with your redis host, localhost by default 2redis.host.name=<your_redis_server_host> 3## Replace <your_redis_server_port> with your redis port, 6379 by default 4redis.host.port=<your_redis_server_port>`

**Deploying Application**

**Configuring JBoss Wildfly**

1. Download and unzip the customized JBoss Wildfly Server from [here](https://devops.egovernments.org/Downloads/wildfly/wildfly-11.0.0.Final.zip). This server contains some additional jars that are required for the ERP.
2. In case, properties needs to be overridden, edit the below file (This is only required if egov-erp-\<username>.properties is not present)

`1<JBOSS_HOME>/modules/system/layers/base/ 2 3org 4└── egov 5 └── settings 6 └── main 7 ├── config 8 │ └── egov-erp-override.properties 9 └── module.xml`

1. Update settings in standalone.xml under \<JBOSS\_HOME>/standalone/configuration

* Check Datasource setting is in sync with your database details.

`1<connection-url>jdbc:postgresql://localhost:5432/<YOUR_DB_NAME></connection-url> 2<security> 3 <user-name><YOUR_DB_USER_NAME></user-name> 4 <password><YOUR_DB_USER_PASSWORD></password 5</security>`

* Check HTTP port configuration is correct in

`1<socket-binding name="http" port="${jboss.http.port:8080}"/>`

1. Change directory back to \<CLONED\_REPO\_DIR>/egov/dev-utils/deployment/ and run the below command

`1$ chmod +x deploy.sh 2$ ./deploy.sh`

Alternatively, this can be done manually by following the below steps.

* Copy the generated exploded ear \<CLONED\_REPO\_DIR>/egov/egov-ear/target/egov-ear-\<VERSION>.ear in to your JBoss deployment folder \<JBOSS\_HOME>/standalone/deployments
* Create or touch a file named egov-ear-\<VERSION>.ear.dodeploy to make sure JBoss picks it up for auto-deployment

1. Start the wildfly server by executing the below command

`1 $ cd <JBOSS_HOME>/bin/ 2 $ nohup ./standalone.sh -b 0.0.0.0 & 3`

In Mac OSx, it may also required to specify -Djboss.modules.system.pkgs=org.jboss.byteman

\-b 0.0.0.0 only required if the application accessed using an IP address or domain name.

1. Monitor the logs and in case of successful deployment, just hit \<http://localhost:\<YOUR\_HTTP\_PORT>/egi> in your favourite browser.
2. Log in using the username as egovernments and password demo

**Accessing the application using IP address and domain name**

This section is to be referred to only if you want the application to run using any IP address or domain name.

**1. To access the application using an IP address:**

* Have an entry in eg\_city table in the database with an IP address of the machine where the application server is running (for ex: domainurl="172.16.2.164") to access the application using the IP address.
* Access the application using the URL [http://172.16.2.164:8080/egi/](http://172.16.2.164:8080/egi/) where 172.16.2.164 is the IP and 8080 is the port of the machine where the application server is running.

**2. To access the application using the domain name:**

* Have an entry in eg\_city table in the database with the domain name (for ex: domainurl= "[www.egoverpphoenix.org](http://www.egoverpphoenix.org)") to access the application using the domain name.
* Add the entry in the host file of your system with details as 172.16.2.164 [www.egoverpphoenix.org](http://www.egoverpphoenix.org) (This needs to be done both in server machine as well as the machines in which the application needs to be accessed since this is not a public domain).
* Access the application using an URL [http://www.egoverpphoenix.org:8080/egi/](http://www.egoverpphoenix.org:8080/egi/) where [www.egoverpphoenix.org](http://www.egoverpphoenix.org) is the domain name and 8080 is the port of the machine where the application server is running.

Always start the wildfly server with the below command to access the application using IP address or domain name.`1 nohup ./standalone.sh -b 0.0.0.0 &`

### Developer Guide <a href="#developer-guide" id="developer-guide"></a>

This section gives more details regarding developing and contributing to the eGov suit.

**Repository Structure**

egov - folder contains all the source code of eGov opensource projects

**Check out sources**

git clone git@github.com:egovernments/egov-smartcity-suite.git or git clone \<https://github.com/egovernments/egov-smartcity-suite.git>

**Prerequisites**

* Install your favourite IDE for the Java project. Recommended Eclipse or IntelliJ IDEA
* Install [maven >= v3.2.x](http://maven.apache.org/download.cgi)
* Install [PostgreSQL >= v9.4](http://www.postgresql.org/download/)
* Install [Elastic Search >= v2.4.x](https://download.elasticsearch.org/elasticsearch/elasticsearch/elasticsearch-2.4.1.zip)
* Install [Jboss Wildfly v10.x](https://devops.egovernments.org/Downloads/wildfly/wildfly-11.0.0.Final.zip)
* Install [Git 2.8.3](https://git-scm.com/downloads)
* Install [JDK 8 update 112 or later](http://www.oracle.com/technetwork/java/javase/downloads)

**Note**: Please check-in \[eGov Tools Repository] for any of the above software installables before downloading from the Internet.

**1. Eclipse Deployment**

* Install [Eclipse Mars](https://eclipse.org/downloads/packages/release/Mars/M1) [Eclipse Mars](https://eclipse.org/downloads/packages/release/Mars/M1)
* Import the cloned git repo using maven Import Existing Project.
* Install Jboss Tools and configure Wildfly Server.
* Since jasperreport related jar's are not available in maven central, we have to tell eclipse to find jar's in alternative place for that navigate to Windows -> Preference -> Maven -> User Settings -> Browse Global Settings and point settings.xml available under egov-erp/
* Now add your EAR project into the configured Wildfly server.
* Start Wildfly in debug mode, this will enable hot deployment.

**2. Intellij Deployment**

* Install Intellij
* Open project
* In project settings set JDK to 1.8
* Add a run configuration for JBoss and point the JBOSS home to the wildfly unzipped folder
* Run

**3. Database Migration Procedure**

* Any new sql files created should be added under directory \<CLONED\_REPO\_DIR>/egov/egov-\<javaproject>/src/main/resources/db/migration
* Core product DDL and DML should be added under \<CLONED\_REPO\_DIR>/egov/egov-\<javaproject>/src/main/resources/db/migration/main
* Core product sample data DML should be added under \<CLONED\_REPO\_DIR>/egov/egov-\<javaproject>/src/main/resources/db/migration/sample
* All SQL scripts should be named in the following format.
* Format V\<timestamp-in-YYYYMMDDHHMMSS-format>\_\_\<module-name>\_\<description>.sql
* DB migration will automatically happen when the application server starts, in case required while maven build to use the above-given maven command.

**Migration file name sample**

`1V20150918161507__egi_initial_data.sql 2`

For more details refer [Flyway](http://flywaydb.org/documentation/)

Note: This system is supported

OS:-

* Linux (Recommended)
* Mac
* Windows (If Redis server standalone installed).

Browser:-

* Chrome (Recommended)
* Firefox
* Internet Explorer

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)​](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation](https://egov.org.in) is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).
