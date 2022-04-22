---
description: Provision infra for DIGIT on Azure using Terraform
---

# On Azure

[Azure Kubernetes Service (AKS)](https://docs.microsoft.com/en-us/azure/aks/) manages your hosted Kubernetes environment. AKS allows you to deploy and manage containerized applications without container orchestration expertise. AKS also enables you to do many common maintenance operations without taking your app offline. These operations include provisioning, upgrading, and scaling resources on demand.



### **Prerequisites** <a href="#prerequisites" id="prerequisites"></a>

* Azure subscription: If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?ref=microsoft.com) before you begin.
* Configure Terraform: Follow the directions in the article, [Terraform and configure access to Azure](https://docs.microsoft.com/en-us/azure/developer/terraform/get-started-cloud-shell)
* Azure service principal: Follow the directions in the Create the service principal section in the article, [Create an Azure service principal with Azure CLI](https://docs.microsoft.com/en-us/cli/azure/create-an-azure-service-principal-azure-cli?view=azure-cli-latest). Take note of the values for the appId, displayName, password, and tenant.

### **Provision Kubernetes cluster stapes** <a href="#provision-kubernetes-cluster-stapes" id="provision-kubernetes-cluster-stapes"></a>

1. &#x20; **Clone the following repository:**

```
git clone --branch release https://github.com/egovernments/DIGIT-DevOps.git
cd DIGIT-DevOps/infra-as-code/terraform
```

&#x20;        Copy the existing azure tf.    &#x20;

```
├── sample-azure
│       ├── main.tf
│       ├── outputs.tf
│       ├── providers.tf
│       ├── remote-state
│       │            └── main.tf
│       └── variables.tf
└── modules
     ├── db
     │    ├── aws
     │    |    ├── main.tf
     │    │    ├── outputs.tf
     │    |    └── variables.tf
     │    └── azure
     │         ├── main.tf
     │         └── variables.tf
     │── kubernetes
     │    └── azure
     │         │   	
     │         ├── main.tf
     │         ├── outputs.tf
     |         └── variables.tf
     └── storage
    	  └── azure
          ├── main.tf
     	  ├── outputs.tf
     	  └── variables.tf                 
```

2\. Change the [main.tf](https://github.com/egovernments/DIGIT-DevOps/blob/release/infra-as-code/terraform/sample-azure/main.tf) according to your requirements,

```
provider "azurerm" {
  # whilst the `version` attribute is optional, we recommend pinning to a given version of the Provider
  version = "=1.28.0"
  subscription_id  = ""  // Add azure subscription id 
  tenant_id        = ""  // Add tenant id
  client_id = "${var.client_id}"
  client_secret = "${var.client_secret}"
}

resource "azurerm_resource_group" "resource_group" {
  name     = "${var.resource_group}"
  location = "${var.location}"
  tags = {
     environment = "${var.environment}"
  }
}

module "kubernetes" {
  source = "../modules/kubernetes/azure"
  environment = "${var.environment}"
  name = "demo"
  location = "${azurerm_resource_group.resource_group.location}"
  resource_group = "${azurerm_resource_group.resource_group.name}"
  client_id = "${var.client_id}"
  client_secret = "${var.client_secret}"
  nodes = "4"
}

module "zookeeper" {
  source = "../modules/storage/azure"
  environment = "${var.environment}"
  itemCount = "3"
  disk_prefix = "zookeeper"
  location = "${azurerm_resource_group.resource_group.location}"
  resource_group = "${module.kubernetes.node_resource_group}"
  storage_sku = "Premium_LRS"
  disk_size_gb = "5"
  
}

module "kafka" {
  source = "../modules/storage/azure"
  environment = "${var.environment}"
  itemCount = "3"
  disk_prefix = "kafka"
  location = "${azurerm_resource_group.resource_group.location}"
  resource_group = "${module.kubernetes.node_resource_group}"
  storage_sku = "Standard_LRS"
  disk_size_gb = "50"
  
}
module "es-master" {
  source = "../modules/storage/azure"
  environment = "${var.environment}"
  itemCount = "3"
  disk_prefix = "es-master"
  location = "${azurerm_resource_group.resource_group.location}"
  resource_group = "${module.kubernetes.node_resource_group}"
  storage_sku = "Premium_LRS"
  disk_size_gb = "2"
  
}
module "es-data-v1" {
  source = "../modules/storage/azure"
  environment = "${var.environment}"
  itemCount = "2"
  disk_prefix = "es-data-v1"
  location = "${azurerm_resource_group.resource_group.location}"
  resource_group = "${module.kubernetes.node_resource_group}"
  storage_sku = "Premium_LRS"
  disk_size_gb = "50"
  
}

module "postgres-db" {
  source = "../modules/db/azure"
  server_name = "demo"
  resource_group = "${module.kubernetes.node_resource_group}"  
  sku_cores = "2"
  location = "${azurerm_resource_group.resource_group.location}"
  sku_tier = "Basic"
  storage_mb = "51200"
  backup_retention_days = "7"
  administrator_login = "demo"
  administrator_login_password = "${var.db_password}"
  ssl_enforce = "Disabled"
  db_name = "demo_ms"
  environment= "${var.environment}"
  
}
```

3\. **Declare the variables in** [**variables.tf**](https://github.com/egovernments/DIGIT-DevOps/blob/release/infra-as-code/terraform/sample-azure/variables.tf)****

```
variable "environment" {

    default = "Environment_Name"

}

variable "resource_group" {

    default = "Resource_Group_Name”

}

variable "location" {

    default = "SouthIndia"

}

variable "db_password" {

}

variable "client_id" {

}

variable "client_secret" {

}
```

Save the file and exit the editor&#x20;

4\. **Create a Terraform output file (**[**output.tf**](https://github.com/egovernments/DIGIT-DevOps/blob/release/infra-as-code/terraform/sample-azure/outputs.tf)**) and Paste the following code into file.**

```
output "zookeeper_storage_ids" {

  value = "${module.zookeeper.storage_ids}"

}

output "kafka_storage_ids" {

  value = "${module.kafka.storage_ids}"

}

output "es_master_storage_ids" {

  value = "${module.es-master.storage_ids}"

}

output "es_data_v1_storage_ids" {

  value = "${module.es-data-v1.storage_ids}"

}
```

5\. **Create the Kubernetes cluster**

&#x20;     1\.  In this section, you see how to use the terraform init command to create the resources defined in the configuration files you created in the previous steps.

The **terraform init** command displays the success of initializing the backend and provider plug-in:

![](<../../.gitbook/assets/image (51).png>)

&#x20;    2\. Run the **terraform plan** command to create the Terraform plan that defines the infrastructure elements.

The terraform plan command displays the resources that will be created when you run the terraform apply command

![](<../../.gitbook/assets/image (52).png>)

&#x20;    3\. Run the **terraform apply** command to apply the plan to create the Kubernetes cluster and other resources.

The process to create a Kubernetes cluster can take several minutes.&#x20;

```
terraform apply out.plan
```

The terraform apply command displays the results of creating the resources defined in your configuration files:

![](<../../.gitbook/assets/image (40).png>)

&#x20;      4\. In the Azure portal, select All resources in the left menu to see the resources created for your new Kubernetes cluster.



**6. Test the Kubernetes cluster**

The Kubernetes tools can be used to verify the newly created cluster.

&#x20;   1\. Once **terraform apply** execution is done it will generate the Kubernetes configuration file or you can get it from Terraform state.

&#x20;  2\.  Set an environment variable so that kubectl picks up the correct config.

```
export KUBECONFIG=./kube_config_file_name 
```

&#x20;`3.` Verify the health of the cluster.

```
kubectl get nodes
```

&#x20;   You should see the details of your worker nodes, and they should all have a status Ready, as shown in the following image:

![](<../../.gitbook/assets/image (42).png>)

