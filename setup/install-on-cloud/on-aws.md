---
description: Provision infra for DIGIT on AWS using Terraform
---

# On AWS

The [**Amazon Elastic Kubernetes Service \(EKS\)**](https://docs.aws.amazon.com/eks/latest/userguide/what-is-eks.html) is one of the AWS services for deploying, managing, and scaling any distributed and containerized workloads, here we can provision the EKS cluster on AWS from ground up and using an automated way \(infra-as-code\) using [**terraform**](https://www.terraform.io/intro/index.html) and then deploy the DIGIT Services config-as-code using [**Helm**](https://helm.sh/docs/).

## Prerequisites <a id="Prerequisites"></a>

1. [**AWS account**](https://portal.aws.amazon.com/billing/signup?nc2=h_ct&src=default&redirect_url=https%3A%2F%2Faws.amazon.com%2Fregistration-confirmation#/start) with the admin access to provision EKS Service, you can always subscribe to free AWS account to learn the basics and try, but there is a limit to [**what is offered as free**](https://aws.amazon.com/free/), for this demo you need to have a commercial subscription to the EKS service, if you want to try out for a day or two, it might cost you about Rs 500 - 1000.
2. Install [**kubectl**](https://kubernetes.io/docs/tasks/tools/) on your local machine that helps you interact with the kubernetes cluster
3.  Install [**Helm**](https://helm.sh/docs/intro/install/) that helps you package the services along with the configurations, envs, secrets, etc into a ****[**kubernetes manifests**](https://devspace.cloud/docs/cli/deployment/kubernetes-manifests/what-are-manifests) 
4. \*\*\*\*[**Install AWS CLI**](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-install.html) ****on your local machine so that you can use aws cli commands to provision and manage the cloud resources on your account.
5. Install [**AWS IAM Authenticator**](https://docs.aws.amazon.com/eks/latest/userguide/install-aws-iam-authenticator.html) that helps you authenticate your connection from your local machine so that you should be able to deploy DIGIT services.
6. Create an [**AWS IAM User**](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_users_create.html) ****for the Terraform \([**Infra-as-code**](https://devops.digit.org/devops-general/infra-as-code)\) to connect with your AWS account and provision the cloud resources.

   1. Login to AWS Console =&gt; go to the **IAM section =&gt; Create User**
   2. **Create Group** by attaching the following access and add it to the above User 
      * AdministratorAccess
      * AmazonEKSClusterPolicy
   3. After these steps, you'll get a **Secret Access Key** and **Access Key ID**. **Save them safely** because this will be displayed only one time.
   4. Open the terminal and Run the following command you have already installed the AWS CLI and you have the credentials saved. \(Provide the credentials and you can leave the region and output format as blank\)

   ```text
   aws configure --profile egov-test-account 

   AWS Access Key ID []:<Your access key>
   AWS Secret Access Key []:<Your secret key>
   Default region name []: ap-south-1
   Default output format []: text
   ```

   5. The above will create the following file In your machine as /Users/&lt;your username&gt;/.aws/credentials

   ```text
   [egov-test-account] 
   aws_access_key_id=*********** 
   aws_secret_access_key=****************************
   ```

## **Resource Graph** <a id="Set-up-and-initialize-your-Terraform-workspace"></a>

Terraform builds a graph of all your resources, and parallelizes the creation and modification of any non-dependent resources. Because of this, Terraform builds infrastructure as efficiently as possible, and operators get insight into dependencies in their infrastructure.

Before we provision the cloud resources, we need to understand and be sure about what resources need to be provisioned by terraform to deploy DIGIT. The following picture shows the various key components. \(EKS, Worker Nodes, PostGres DB, EBS Volumes, Load Balancer\)

![EKS Architecture for DIGIT Setup](../../.gitbook/assets/image%20%28109%29.png)

Considering the above deployment architecture, the following is the resource graph that we are going to provision using terraform in a standard way so that every time and for every env, it'll have the same infra.

* EKS Control Plane \(Kubernetes Master\)
* Work node group \(VMs with the estimated number of vCPUs, Memory\)
* EBS Volumes \(Persistent Volumes\)
* RDS \(PostGres\)
* VPCs \(Private network\)
* Users to access, deploy and read-only

## Understand the Terraform script: <a id="Set-up-and-initialize-your-Terraform-workspace"></a>

* Ideally, one would write the terraform script from the scratch using this [doc](https://learn.hashicorp.com/collections/terraform/modules).
* Here we have already written the terraform script that provisions the production-grade DIGIT Infra and can be customized with the specified configuration.
* Let's Clone the [DIGIT-DevOps](https://github.com/egovernments/DIGIT-DevOps.git) GitHub repo where the terraform script to provision EKS cluster is available and below is the structure of the files.

```text
git clone https://github.com/egovernments/DIGIT-DevOps.git
cd DIGIT-DevOps/infra-as-code/terraform


└── modules
    ├── db
    │   └── aws
    │       ├── main.tf
    │       ├── outputs.tf
    │       └── variables.tf
    ├── kubernetes
    │   └── aws
    │       ├── eks-cluster
    │       │   ├── main.tf
    │       │   ├── outputs.tf
    │       │   └── variables.tf
    │       ├── network
    │       │   ├── main.tf
    │       │   ├── outputs.tf
    │       │   └── variables.tf
    │       └── workers
    │           ├── main.tf
    │           ├── outputs.tf
    │           └── variables.tf
    └── storage
        └── aws
            ├── main.tf
            ├── outputs.tf
            └── variables.tf
```

In here, you will find the modules used to provision a EKS cluster, RDS, and Storage. All these are modularized and reacts as per the customized options are provided.  

* **VPC Resources:**
  * VPC
  * Subnets
  * Internet Gateway
  * Route Table
* **EKS Cluster Resources:**
  * IAM Role to allow EKS service to manage other AWS services
  * EC2 Security Group to allow networking traffic with EKS cluster
  * EKS Cluster
* **EKS Worker Nodes Resources:**
  * IAM role allowing Kubernetes actions to access other AWS services
  * EC2 Security Group to allow networking traffic
  * Data source to fetch latest EKS worker AMI
  * AutoScaling Launch Configuration to configure worker instances
  * AutoScaling Group to launch worker instances
* **Database**
  * Configuration in this directory creates set of RDS resources including DB instance, DB subnet group, and DB parameter group.
* **Storage Module**
  * Configuration in this directory creates EBS volume and attaches it together.

## Choose the environment <a id="Set-up-an-environment"></a>

Here, you can define your env and provide the env specific cloud requirements so that using the same terraform template you can customize the configurations.

```text
├── dev
│   ├── main.tf 
│   ├── outputs.tf
│   ├── providers.tf
│   ├── remote-state
│   │   └── main.tf
│   └── variables.tf
├── qa
    ├── main.tf
    ├── outputs.tf
    ├── providers.tf
    ├── remote-state
    │   └── main.tf
    └── variables.tf
```

Following are the values that you need to mention in the following files, the blank ones will be prompted for inputs while execution.

```text
## Add Cluster Name
variable "cluster_name" {
  default = "<Desired Cluster name>"  #eg: digit-qa
}

## Add vpc_cidr_block
variable "vpc_cidr_block" {
  default = "CIDR" 
}

# If you want prod grade N/W, you can define HA, DRS with multi zone
variable "network_availability_zones" {  
  default = ["ap-south-1b", "ap-south-1a"]
}

# Which zone, it matters
variable "availability_zones" {
  default = ["ap-south-1b"]
}

variable "kubernetes_version" {
  default = "1.18"
}

# instance type for your worker nodes like r5a.large is 8 vCPU and 16GB RAM
variable "instance_type" {
  default = "r5a.large"
}

# spot instance configuration
variable "override_instance_types" {
  default = ["r5a.large", "r5ad.large", "r5d.large", "t3a.xlarge"] 
}

# number of machines as per estimate
variable "number_of_worker_nodes" {
  default = "3"
}

##Add ssh key in case you want to ssh to nodes
variable "ssh_key_name" {
  default = "ssh key name"
}

# terraform users ssh public key
variable "iam_keybase_user" {
  default = "keybase:egovterraform"
}

# will be prompted to provide during the execution
variable "db_password" {}

```

## Run terraform

Now that we know what the terraform does, the resources graph that it provisions and what values should be given with respect to the type of env. 

Let's being with running the script to provision infra required to Deploy DIGIT on AWS.

1. CD into the following directory and run the following command 1-by-1 and watch the output closely.

```text
cd DIGIT-DevOps/infra-as-code/terraform/dev
terraform init
terraform plan
terraform apply
terraform output
```

 Upon Successful execution following resources gets created which can be verified by the command "terraform output"

* **s3 bucket:** to store terraform state.
* **Network:** VPC, security groups.
* **IAM users auth:** using keybase to create admin, deployer, the user.
  * Example user keybase user"_egovterraform_" needs to be created and has to uploaded his public key here - [https://keybase.io/egovterraform/pgp\_keys.asc](https://keybase.io/egovterraform/pgp_keys.asc)
* **EKS cluster:** with master\(s\) & worker node\(s\).
* **Storage\(s\):** for es-master, es-data-v1, es-master-infra, es-data-infra-v1, zookeeper, kafka, kafka-infra.

2. Use this link to [get the kubeconfig from EKS](https://docs.aws.amazon.com/eks/latest/userguide/create-kubeconfig.html) to get the kubeconfig file and being able to connect to the cluster from your local machine so that you should be able to deploy DIGIT services to the cluster.

```text
aws sts get-caller-identity

# Run the below command and give the respective region-code and the cluster name
aws eks --region <region-code> update-kubeconfig --name <cluster_name>
```

3. Finally, Verify that you are able to connect to the cluster by running the following command

```text
kubectl get nodes

NAME                                             STATUS AGE   VERSION               OS-Image           
ip-192-168-xx-1.ap-south-1.compute.internal   Ready  45d   v1.15.10-eks-bac369   Amazon Linux 2   
ip-192-168-xx-2.ap-south-1.compute.internal   Ready  45d   v1.15.10-eks-bac369   Amazon Linux 2   
ip-192-168-xx-3.ap-south-1.compute.internal   Ready  45d   v1.15.10-eks-bac369   Amazon Linux 2   
ip-192-168-xx-4.ap-south-1.compute.internal   Ready  45d   v1.15.10-eks-bac369   Amazon Linux 2 
```

Whola! All set and now you can go Deploy DIGIT...
