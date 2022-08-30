# BPA Service Configuration

### **Software to install**

* Java 1.8
* Eclipse
* Postgres
* PhpPgAdmin
* Postman (Application)
* Respective Git MiddleWare
* Kubectl
* Kafka

Take the code pull from the git:

Need to consider 2 repositories for code to run locally

1. Municipal services - where our BPA code exists and some dependency services also available here [![](https://github.githubassets.com/favicon.ico)https://github.com/egovernments/municipal-services.git - Connect to preview](https://github.com/egovernments/municipal-services.git)
2. Core Services - Where dependency services exist to run our code locally [![](https://github.githubassets.com/favicon.ico)https://github.com/egovernments/core-services.git - Connect to preview](https://github.com/egovernments/core-services.git)

Import the required projects to eclipse

From municipal-services import bpa-services, bpa-calculator and land-services.\
From core-services import user service, idgen service, mdms service, location service, localization service, workflow service, egov-persister.

Before running the application make sure the following setups are complete to ensure the application runs smoothly.

* kafka set up in your system which is running fine. Download the latest version of kafka from here. [https://kafka.apache.org/downloads](https://kafka.apache.org/downloads)

Run the below commands based on your system types

**For linux: in kafka folder path**

**Example:** D:\kafka\_2.13-2.4.0

\> bin/zookeeper-server-start.sh config/zookeeper.properties\
\> bin/kafka-server-start.sh config/server.properties

**Ref:** [**https://kafka.apache.org/quickstart**](https://kafka.apache.org/quickstart)

**For Windows: in windows path**

**Example:** D:\kafka\_2.13-2.4.0\bin\windows\
start zookeeper-server-start.bat ....\config\zookeeper.properties\
start kafka-server-start.bat ....\config\server.properties

* And lombok setup for eclipse **For ref:** [**https://www.journaldev.com/18124/java-project-lombok**](https://www.journaldev.com/18124/java-project-lombok)
* Kubectl setup based on the requirement **To get the pods:** kubectl get pods **To port forward:** kubectl port-forward <\<pod name>> <\<port number>>:8080 **To get the logs:** kubectl get logs

After all the setups are done successfully, try to run the application locally.

BPA-Services How to run the application in local:

Check the services which are connected to local and which are connected to dev

* Which are connected to dev no need to change anything.
* If it is connected to local check the services are in below list _**IDGEN –** can run locally or can point to dev from cmd prompt_ _**PERSISTER –** can run locally_ _**MDMS –** can directly point to dev or can run in local_ _**LOCATION –** can directly point to dev_ _**WORKFLOW –** can point to dev or can run locally_ _**LOCALIZATIONS** – we can directly point this to dev_ _**USER-SERVICE –** need to point to dev from cmd prompt_ _**LAND-SERVICE –** need to run locally_ _**BPA-CALCULATOR** – can run locally or can point to dev._
* If the changes are from these services follow the below process to run those respective services.

**For core services:**

_**IDGEN:**_

Approach 1: Directly point this to dev from the application.properties in bpa-services\
Approach 2: Point this to local and give the port forward to dev by using kubctl.

{% hint style="info" %}
**Note**: We are not running this service locally.
{% endhint %}

_**PERSISTER:**_

U need to run it in local and need to add respective yaml files in persister resource folder which are bpa-persister.yml and egov-workflow-v2-persister.yml and also land-persister.yml

And need to add these in persister application.properties repo path

{% hint style="info" %}
**Note:** Please check whether data is is saving or not in local data base(DB).
{% endhint %}

_**MDMS:**_

**to run local:**\
For running this in local need to change in 2 file that is application.properties and MDMSApplicationRunnerImpl

In application.properties need to change the paths for the master-config url as path of master-config.json and for config path as upto pb/bh

In MDMS ApplicationRunnerImpl need to change the data in a function from the path to file.

**to point to dev:**\
Approach 1: Directly point this to dev from the application.properties in bpa-services

Approach 2: Give it as local connection in BPA application.properties and port forward to dev by using kubectl.

**Postman Collection** [https://www.getpostman.com/collections/c59b5c6190719ecd306a](https://www.getpostman.com/collections/c59b5c6190719ecd306a)

_**LOCATION**_

Approach 1: Give it a local connection in BPA application.properties and port forward to dev by using kubectl.

Approach 2: Directly point this to dev from the application.properties in bpa-services

{% hint style="info" %}
**Note:** Not tried it in local / may got errors so pointing to dev.
{% endhint %}

**Postman collection** [https://www.getpostman.com/collections/4f6a25a4fb32572af5ff](https://www.getpostman.com/collections/4f6a25a4fb32572af5ff)

_**WORKFLOW**_

**to point to dev:**\
Approach 1: Directly point this to dev from the application.properties in bpa-services

Approach 2: Give it as local connection in BPA application.properties and port forward to dev by using kubectl.

**to run local:**

can run locally by pointing to the local database, but for this need to create the workflow locally using the workflow create API.

**Postman collection** [https://www.getpostman.com/collections/aa30be8a8b9de4c13aa8](https://www.getpostman.com/collections/aa30be8a8b9de4c13aa8)

_**USER-SERVICE**_\
Approach 1: Give it as local connection in BPA application.properties and port forward to dev by using kubectl.

Approach 2: Directly point this to dev from the application.properties in bpa-services

{% hint style="info" %}
**Note:** In local not able to run the application successfully, so the following dev.
{% endhint %}

**Postman Collection**: [https://www.getpostman.com/collections/60bbd6aed27605dcc270](https://www.getpostman.com/collections/60bbd6aed27605dcc270)

_**LOCALIZATIONS**_

Approach 1: Directly point this to dev from the application.properties in bpa-services

Approach 2: Give it as local connection in BPA application.properties and port forward to dev by using kubectl.

**Postman Collection** [https://www.getpostman.com/collections/12cc4c3855be9699c278](https://www.getpostman.com/collections/12cc4c3855be9699c278)

**Changes from Municipal services**

_**BPA-Calculator:**_

**to run local:**

can run locally by pointing to the local database.

**to point to dev:**\
Approach 1: Directly point this to dev from the application.properties in bpa-services

Approach 2: Give it as local connection in BPA application.properties and port forward to dev by using kubectl.

_**Land-Service:**_

**to run local:**

can run locally by pointing to the local database.

**to point to dev:**\
Approach 1: Directly point this to dev from the application.properties in bpa-services

Approach 2: Give it as local connection in BPA application.properties and port forward to dev by using kubectl.

Other than these services can directly by pointing to dev url.

{% hint style="info" %}
**Note:** After running the application successfully please check if the data is saving in db or not.
{% endhint %}

### All Dependent Services <a href="#all-dependent-services" id="all-dependent-services"></a>

* **egov-user** - (Manage user)
* **tl-services** - Stakeholder Registration (Registration process of Stakeholder is handled by this service)
* **egov-user-event** (What’s New and Events)
* **egov-filestore** (To store the documents uploaded by the user)
* **egov-idgen** (To generate the application No, Permit No)
* **egov-indexer** (To index the BPA data)
* **egov-localization** (To use the localized messages)
* **egov-location** (To store the address locality)
* **egov-mdms** (Configurations/master data used in the application is served by MDMS)
* **egov-notification-sms** (Service to send SMS to the users involved in the application)
* **egov-persister** (Helps to persist the data)
* **egov-searcher** (Search query used to simplify the search)
* **egov-workflow-v2** (Workflow configuration for different BPA application is configured)
* **pdf-service** (Receipt’s, permitorder etc.. and prepared)
* **billing-service** (Create demands and bills for the fees to be collected)
* **collection-services** (Create a receipt for the payment received for the bills)
* **bpa-calculator** (Calculates the fees to be collected at different stages)
* **land-services** (land information related to BPA application is stored)
* **dcr-services** (get and validate EDCR data)

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation ](https://egov.org.in/)is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).
