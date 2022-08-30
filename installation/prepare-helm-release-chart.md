---
description: Release chart helps to deploy the product specific modules in one click.
---

# Prepare Helm Release Chart

### Prepare New Release Chart For Existing Products.

#### Pre-requisites

1. Git&#x20;
2. [Install Visualstudio](https://code.visualstudio.com/download) IDE Code for better code visualization/editing capabilities

#### Steps To Prepare New Release Chart For Existing Products:

1. Clone the following [DIGIT-DevOps](https://github.com/egovernments/DIGIT-DevOps) where we have all the release charts for you to refer.

```
git clone --branch release https://github.com/egovernments/DIGIT-DevOps.git
cd config-as-code/product-release-charts/
```

As you can see we already have the below products, create a new release version into the products

![](<../.gitbook/assets/Screenshot 2022-07-20 at 11.32.56 AM.png>)

2\. Select your product and copy the previous release version file and rename it with your new version.

```
$cd DIGIT-DevOps/config-as-code/product-release-charts/DIGIT
$ls 
    dependancy_chart-digit-v2.0.yaml	
    dependancy_chart-digit-v2.1.yaml	
    dependancy_chart-digit-v2.2.yaml	
    dependancy_chart-digit-v2.3.yaml
    dependancy_chart-digit-v2.4.yaml
    dependancy_chart-digit-v2.5.yaml
    dependancy_chart-digit-v2.6.yaml

$cp dependancy_chart-digit-v2.6.yaml dependancy_chart-digit-<your_release_version>.yaml
```

Above, you have copied and renamed the dependancy\_chart-digit-v2.6.yaml with your new release version.

**Note**: replace \<your\_release\_version> with your new release version.



3\. Navigate to your release file on your local machine. Open the file using Visualstudio or any other file editor.

<details>

<summary>prepare release config </summary>

```
version: v2.6  # Update the release version "v2.6" with your release version.      
modules:
    - name: backbone
      services:
        - zookeeper-v2
        - kafka-v2
        - kafka-connect
        - kafka-connect-restart-tasks
        - elasticsearch-data-v1
        - elasticsearch-master-v1
        - kibana-v1
    - name: authn-authz
      services:
        - redis
        - nginx-ingress
        - cert-manager
        - zuul:v1.3.1-96b24b0d72-39      
    - name: core
      dependencies:
        - "backbone"
        - "authn-authz"    
      services:
        - egovio/egov-accesscontrol:v1.1.3-72f8a8f87b-24
        - egovio/egov-enc-service:v1.1.2-72f8a8f87b-9
        - egovio/egov-filestore:v1.2.3-2ee9ec37-4
        - egovio/egov-idgen:v1.2.3-72f8a8f87b-7
        - egovio/egov-indexer:v1.1.6-72f8a8f87b-10
        - egovio/egov-localization:v1.1.3-72f8a8f87b-6
        - egovio/egov-location:v1.1.4-72f8a8f87b-6
        - egovio/egov-mdms-service:v1.3.2-72f8a8f87b-12
        - egovio/egov-notification-mail:v1.1.2-72f8a8f87b-12
        - egovio/egov-notification-sms:v1.1.3-48a03ad7bb-10
        - egovio/egov-otp:v1.2.2-72f8a8f87b-12
        - egovio/egov-persister:v1.1.4-72f8a8f87b-6
        - egovio/egov-pg-service:v1.2.3-72f8a8f87b-14
        - egovio/egov-searcher:v1.1.5-72f8a8f87b-16
        - egovio/egov-url-shortening:v1.1.1-72f8a8f87b-20
        - egovio/egov-user:v1.2.6-96b24b0d72-87
        - egovio/user-otp:v1.1.4-96b24b0d72-15
        - egovio/egov-workflow-v2:v1.2.1-96b24b0d72-72
        - egovio/pdf-service:v1.1.6-96b24b0d72-83
        - egovio/report:v1.3.4-96b24b0d72-16
        - egovio/chatbot:v1.1.6-72f8a8f87b-8
        - egovio/xstate-chatbot:v1.1.1-96b24b0d72-21
        - egovio/egov-user-chatbot:v1.2.6-96b24b0d72-4 
        - egovio/nlp-engine:v1.0.0-fbea6fba-21
        - egovio/egov-document-uploader:v0.0.1-48a03ad7bb-26
        - egovio/playground:1.0
    - name: business
      dependencies:
        - "core"
      services:
        - egovio/collection-services:v1.1.6-72f8a8f87b-23
        - egovio/billing-service:v1.3.4-72f8a8f87b-39
        - egovio/egf-instrument:v1.1.4-72f8a8f87b-4
        - egovio/egf-master:v1.1.3-72f8a8f87b-15
        - egovio/egov-apportion-service:v1.1.5-72f8a8f87b-5
        - egovio/egov-hrms:v1.2.4-72f8a8f87b-27
        - egovio/finance-collections-voucher-consumer:v1.1.6-96b24b0d72-18
    - name: utilities
      dependencies:
        - "core"
      services:
        - egovio/egov-custom-consumer:v1.1.1-72f8a8f87b-3
        - egovio/egov-pdf:v1.1.2-344ffc814a-37
    - name: frontend         
      dependencies:
        - "business"
      services:
        - egovio/citizen:citizen-v1.5.0-c1825dd69-291
        - egovio/employee:v1.7.0-83c152772f-172
        - egovio/digit-ui:v1.4.0-29d4be1d4f-704  
    - name: m_pgr             #PGR
      dependencies:
        - "core"
        - "business"
      services:
        - egovio/pgr-services:v1.1.4-96b24b0d72-21
        - egovio/rainmaker-pgr:v1.1.4-48a03ad7bb-4
    - name: m_property-tax    #PT
      dependencies:
        - "core"
        - "business"
      services:
        - egovio/property-services:v1.1.7-96b24b0d72-138
        - egovio/pt-calculator-v2:v1.1.5-96b24b0d72-12
        - egovio/pt-services-v2:v1.0.0-48a03ad7bb-4
    - name: m_sewerage        #Sewerage
      dependencies:
        - "core"
        - "business"
      services:
        - egovio/sw-calculator:v1.3.2-96b24b0d72-15
        - egovio/sw-services:v1.4.2-96b24b0d72-31
    - name: m_bpa             #BPA
      dependencies:
          - "core"
          - "business"
      services:
          - egovio/bpa-services:v1.1.5-59f19cd017-74
          - egovio/bpa-calculator:v1.1.1-72f8a8f87b-8
          - egovio/land-services:v1.0.4-96b24b0d72-14
          - egovio/noc-services:v1.0.4-96b24b0d72-18
    - name: m_trade-license    #TL
      dependencies:
          - "core"
          - "business"
      services:
        - egovio/tl-calculator:v1.1.4-96b24b0d72-9
        - egovio/tl-services:v1.1.5-100cbc1a10-175     
    - name: m_firenoc         #Fire NOC
      dependencies:
          - "core"
          - "business"
      services:
          - egovio/firenoc-calculator:v1.2.0-d4a78bf8a3-19
          - egovio/firenoc-services:v1.3.2-12ed7e93c1-64
    - name: m_water-service   #Water
      dependencies:
          - "core"
          - "business"
      services:
        - egovio/ws-calculator:v1.3.2-96b24b0d72-26
        - egovio/ws-services:v1.4.2-96b24b0d72-65
    - name: m_dss   #dss
      dependencies:        
          - "frontend"
          - "core"
          - "business"
      services:
        - egovio/dashboard-analytics:v1.1.6-72f8a8f87b-5
        - egovio/dashboard-ingest:v1.1.4-72f8a8f87b-10
        - egovio/dss-dashboard:v1.7.0-b916c7d187-13
    - name: m_fsm   #fsm
      dependencies:
          - "core"
          - "business"
      services:
        - egovio/fsm:v1.0.4-96b24b0d72-13
        - egovio/fsm-calculator:v1.0.0-48a03ad7bb-5
        - egovio/vehicle:v1.0.3-96b24b0d72-6
        - egovio/vendor:v1.0.3-96b24b0d72-5
    - name: m_echallan   #eChallan
      dependencies:
          - "core"
          - "business"
      services:
        - egovio/echallan-services:v1.0.4-72f8a8f87b-17
        - egovio/echallan-calculator:v1.0.2-72f8a8f87b-14
    - name: Other             #Other Services
      dependencies:
        - "core"
        - "business"
      services:
        - egovio/egov-user-event:v1.1.4-48a03ad7bb-18
        - egovio/inbox:v1.1.0-96b24b0d72-79
        - egovio/turn-io-adapter:v1.0.1-96b24b0d72-5
    - name: m_edcr   #edcr
      dependencies:
          - "core"
      services:
        - egovio/egov-edcr:v2.1.0-db5adca27f-23 
    - name: m_finance         #Finance
      dependencies:
          - "core"
      services:
          - egovio/egov-finance:v3.0.2-0d0a8db8ff-28
```

</details>

1. Update the release version "v2.6" with your new release version.
2. Update the modules(core, business, utilities, m\_pgr, m\_property-tax,..etc) service images with new release service images.&#x20;

4\. Add new modules

```
    - name: m_finance         #Finance
      dependencies:
          - "core"
      services:
          - egovio/egov-finance:v3.0.2-0d0a8db8ff-28
    - name: m_module_1             #New module name
      dependencies:
        - "core"
        - "business"
      services:
        - egovio/egov-user-event:v1.1.4-48a03ad7bb-18
        - egovio/inbox:v1.1.0-96b24b0d72-79
        - egovio/turn-io-adapter:v1.0.1-96b24b0d72-5
    - name: m_module_2             #New module name
      dependencies:
        - "core"
        - "business"
      services:
        - egovio/egov-user-event:v1.1.4-48a03ad7bb-18
        - egovio/inbox:v1.1.0-96b24b0d72-79
        - egovio/turn-io-adapter:v1.0.1-96b24b0d72-5   
```

1. **name** - add your module name with "m\_demo" ideal format ie. "m" means module and "demo" would be your module name&#x20;
2. **dependencies** - add your module dependencies (name of other modules)
3. **services -** add your module specific new service images.

### Prepare New Release Chart For New Product.

#### Pre-requisites

1. Git
2. GitHub Organization Account
3. [Install Visualstudio](https://code.visualstudio.com/download) IDE Code for better code visualization/editing capabilities

When you have a new product to introduce, you can follow the below steps to create the release chart for a new product.

1.  &#x20;eGov partners can follow the below steps:

    1. Fork the [DIGIT-DevOps](https://github.com/egovernments/DIGIT-DevOps) repo to your GitHub organization account&#x20;
    2. Clone the forked DIGIT-DevOps repo to your local machine
       1.  `git clone --branch release https://github.com/<your_organization_account_name>/DIGIT-DevOps.git`

           **Note**: replace this \<your\_organization\_account\_name> with your github organization account name.
    3.  Navigate to the product-release-charts folder and create a new folder with your product name.\
        `cd DIGIT-DevOps/config-as-code/product-release-charts`\
        `mkdir <new_product_name>`

        **Note**: replace \<new\_product\_name> with your new product name.
    4. Create a new release chart file in above created product folder.

    &#x20;      `touch dependancy_chart-<new_product_name>-<release_version>.yaml`

    &#x20;        1\. Open your release chart file dependancy\_chart-<`new_product_name`>-\<release\_version>.yaml and start preparing as mentioned in the below release template.

<details>

<summary>prepare release config </summary>

```
version: v1.0     #Add your release version
modules:
    - name: backbone  #Add the necessary backbone services for the product.
      services:
        - zookeeper-v2
        - kafka-v2
        - kafka-connect
        - kafka-connect-restart-tasks
        - elasticsearch-data-v1
        - elasticsearch-master-v1
        - kibana-v1
        - redis
        - nginx-ingress
        - cert-manager
        - zuul 
        - playground:1.0
    - name: core    #Add the necessary core services for the product.
      dependencies:
        - "backbone"
      services:
        - egovio/egov-accesscontrol:v1.1.0-f9375a4
        - egovio/egov-common-masters:408-14b79e9
        - egovio/egov-data-uploader:7-uploader-demand-feature-44b0170
        - egovio/egov-enc-service:v1.1.0-f9375a4
        - egovio/egov-filestore:v1.2.0-3acc52b
        - egovio/egov-idgen:v1.2.0-f9375a4
        - egovio/egov-indexer:v1.1.1-da68594-7
        - egovio/egov-localization:v1.1.0-f9375a4
        - egovio/egov-location:v1.1.0-f9375a4
        - egovio/egov-mdms-service:v1.3.0-e50b9eb
        - egovio/egov-notification-mail:v1.1.0-40b5f2d
        - egovio/egov-notification-sms:v1.1.0-245443e
        - egovio/egov-otp:v1.2.0-f9375a4
        - egovio/egov-persister:v1.1.1-58f6da0-9
        - egovio/egov-pg-service:v1.1.0-f9375a4
        - egovio/egov-searcher:v1.1.0-59d3598
        - egovio/egov-url-shortening:v1.0.0-40cc090
        - egovio/egov-user:v1.2.1-4976757
        - egovio/user-otp:v1.1.0-2f36d3a
        - egovio/egov-workflow-v2:v1.1.0-42786ef
        - egovio/pdf-service:v1.1.0-09b11d9
        - egovio/report:v1.3.0-28b3c97
    - name: business  #Add the necessary business services for the product
      dependencies:
        - "core"
      services:
        - egovio/collection-services:v1.1.1-4f6c6f7-15
        - egovio/billing-service:v1.1.1-33b0fcf-14
        - egovio/egf-instrument:v1.1.0-005ff61
        - egovio/egf-master:v1.1.0-9959f29
        - egovio/egov-apportion-service:v1.1.2-3436cd5-4
        - egovio/egov-hrms:v1.1.0-43cb793
        - egovio/dashboard-analytics:v1.1.1-14637ce-14
        - egovio/dashboard-ingest:v1.1.1-3436cd5-2
    - name: m_module_1             #Add a new module and its necessary services.
      dependencies:
        - "core"
        - "business"
      services:
        - new-services-1:<image-tag>
        - new-services-2:<image-tag>
        - new-services-3:<image-tag>
    - name: m_module_2             #Add a new module and its necessary services.
      dependencies:
        - "core"
        - "business"
      services:
        - new-services-1:<image-tag>
        - new-services-2:<image-tag>
        - new-services-3:<image-tag>    
```

</details>



2\. eGov users can follow the below steps:

1. Clone the forked DIGIT-DevOps repo to your local machine
   1. `git clone --branch release https://github.com/egovernments/DIGIT-DevOps.git`
   2.  Navigate to the product-release-charts folder and create a new folder with your product name.\
       `cd DIGIT-DevOps/config-as-code/product-release-charts`\
       &#x20;`mkdir <new_product_name>`

       **Note**: replace \<new\_product\_name> with your new product name
2.  Create a new release chart file in above created product folder.

    `touch dependancy_chart-<new_product_name>-<release_version>.yaml`

    &#x20;        1\. Open your release chart file dependancy\_chart-<`new_product_name`>-\<release\_version>.yaml and start preparing as mentioned in the below release template.

<details>

<summary>prepare release config </summary>

```
version: v1.0     #Add your release version
modules:
    - name: backbone  #Add the necessary backbone services for the product.
      services:
        - zookeeper-v2
        - kafka-v2
        - kafka-connect
        - kafka-connect-restart-tasks
        - elasticsearch-data-v1
        - elasticsearch-master-v1
        - kibana-v1
        - redis
        - nginx-ingress
        - cert-manager
        - zuul 
        - playground:1.0
    - name: core    #Add the necessary core services for the product.
      dependencies:
        - "backbone"
      services:
        - egovio/egov-accesscontrol:v1.1.0-f9375a4
        - egovio/egov-common-masters:408-14b79e9
        - egovio/egov-data-uploader:7-uploader-demand-feature-44b0170
        - egovio/egov-enc-service:v1.1.0-f9375a4
        - egovio/egov-filestore:v1.2.0-3acc52b
        - egovio/egov-idgen:v1.2.0-f9375a4
        - egovio/egov-indexer:v1.1.1-da68594-7
        - egovio/egov-localization:v1.1.0-f9375a4
        - egovio/egov-location:v1.1.0-f9375a4
        - egovio/egov-mdms-service:v1.3.0-e50b9eb
        - egovio/egov-notification-mail:v1.1.0-40b5f2d
        - egovio/egov-notification-sms:v1.1.0-245443e
        - egovio/egov-otp:v1.2.0-f9375a4
        - egovio/egov-persister:v1.1.1-58f6da0-9
        - egovio/egov-pg-service:v1.1.0-f9375a4
        - egovio/egov-searcher:v1.1.0-59d3598
        - egovio/egov-url-shortening:v1.0.0-40cc090
        - egovio/egov-user:v1.2.1-4976757
        - egovio/user-otp:v1.1.0-2f36d3a
        - egovio/egov-workflow-v2:v1.1.0-42786ef
        - egovio/pdf-service:v1.1.0-09b11d9
        - egovio/report:v1.3.0-28b3c97
    - name: business  #Add the necessary business services for the product
      dependencies:
        - "core"
      services:
        - egovio/collection-services:v1.1.1-4f6c6f7-15
        - egovio/billing-service:v1.1.1-33b0fcf-14
        - egovio/egf-instrument:v1.1.0-005ff61
        - egovio/egf-master:v1.1.0-9959f29
        - egovio/egov-apportion-service:v1.1.2-3436cd5-4
        - egovio/egov-hrms:v1.1.0-43cb793
        - egovio/dashboard-analytics:v1.1.1-14637ce-14
        - egovio/dashboard-ingest:v1.1.1-3436cd5-2
    - name: m_module_1             #Add a new module and its necessary services.
      dependencies:
        - "core"
        - "business"
      services:
        - new-services-1:<image-tag>
        - new-services-2:<image-tag>
        - new-services-3:<image-tag>
    - name: m_module_2             #Add a new module and its necessary services.
      dependencies:
        - "core"
        - "business"
      services:
        - new-services-1:<image-tag>
        - new-services-2:<image-tag>
        - new-services-3:<image-tag>
```

</details>
