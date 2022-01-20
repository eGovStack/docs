---
description: CI/CD setup
---

# CI/CD SetUp

## Prerequisites <a href="#prerequisites" id="prerequisites"></a>

1. GitHub Organization account
2. [Fork](https://docs.github.com/en/get-started/quickstart/fork-a-repo) the belo repo's to your GitHub Organization account 1. [https://github.com/egovernments/DIGIT-DevOps](https://github.com/egovernments/DIGIT-DevOps) and 2. [https://github.com/egovernments/CIOps](https://github.com/egovernments/CIOps)
3. [AWS KMS](https://docs.aws.amazon.com/kms/index.html)
4. [Go lang](https://golang.org/doc/install) (version 1.13.X)
5. [SOPS](https://github.com/mozilla/sops#updatekeys-command)
6. [GitHub user](https://docs.github.com/en/get-started/signing-up-for-github/signing-up-for-a-new-github-account)
7. [Docker Hub account](https://hub.docker.com/signup)
8. ​[**AWS account**](https://portal.aws.amazon.com/billing/signup?nc2=h\_ct\&src=default\&redirect\_url=https%3A%2F%2Faws.amazon.com%2Fregistration-confirmation#/start) with the admin access to provision EKS Service, you can always subscribe to free AWS account to learn the basics and try, but there is a limit to [**what is offered as free**](https://aws.amazon.com/free/), for this demo you need to have a commercial subscription to the EKS service, if you want to try out for a day or two, it might cost you about Rs 500 - 1000. **(Note: Post the Demo, for the internal folks, eGov will provide a 2-3 hrs time bound access to eGov's AWS account based on the request and available number of slots per day)**
9. Install [**kubectl**](https://kubernetes.io/docs/tasks/tools/) on your local machine that helps you interact with the kubernetes cluster
10. Install [**Helm**](https://helm.sh/docs/intro/install/) that helps you package the services along with the configurations, envs, secrets, etc into a [**kubernetes manifests**](https://devspace.cloud/docs/cli/deployment/kubernetes-manifests/what-are-manifests)
11. Install [**terraform**](https://releases.hashicorp.com/terraform/0.14.10/) version (0.14.10) for the Infra-as-code (IaC) to provision cloud resources as code and with desired resource graph and also it helps to destroy the cluster at one go.
12. **​**[**Install AWS CLI**](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-install.html) on your local machine so that you can use aws cli commands to provision and manage the cloud resources on your account.
13. Install [**AWS IAM Authenticator**](https://docs.aws.amazon.com/eks/latest/userguide/install-aws-iam-authenticator.html) that helps you authenticate your connection from your local machine so that you should be able to deploy DIGIT services.
14. Use the [**AWS IAM User**](https://docs.aws.amazon.com/IAM/latest/UserGuide/id\_users\_create.html) **credentials provided** for the Terraform ([**Infra-as-code**](https://devops.digit.org/devops-general/infra-as-code)) to connect with your AWS account and provision the cloud resources.

    ​

    1. You'll get a **Secret Access Key** and **Access Key ID**. **Save them safely.**
    2. Open the terminal and Run the following command you have already installed the AWS CLI and you have the credentials saved. (Provide the credentials and you can leave the region and output format as blank)

    ```
    aws configure --profile cicd-infra-account 

    AWS Access Key ID []:<Your access key>
    AWS Secret Access Key []:<Your secret key>
    Default region name []: ap-south-1
    Default output format []: text
    ```

    1. The above will create the following file In your machine as /Users/.aws/credentials

    ```
    [cicd-infra-account] 
    aws_access_key_id=*********** 
    aws_secret_access_key=****************************
    ```

## CI/CD Cluster Setup

[**Terraform**](https://www.terraform.io/intro/index.html) helps you build a graph of all your resources, and parallelizes the creation and modification of any non-dependent resources. Because of this, Terraform builds infrastructure as efficiently as possible, and operators get insight into dependencies in their infrastructure.

Before we provision the cloud resources, we need to understand and be sure about what resources need to be provisioned by terraform to deploy CI/CD.

The following is the resource graph that we are going to provision using terraform in a standard way so that every time and for every env, it'll have the same infra.

* EKS Control Plane (Kubernetes Master)
* Work node group (VMs with the estimated number of vCPUs, Memory)
* EBS Volumes (Persistent Volumes)
* VPCs (Private network)
* Users to access, deploy and read-only

## Understand the **Resource Graph in** Terraform script: <a href="#set-up-and-initialize-your-terraform-workspace" id="set-up-and-initialize-your-terraform-workspace"></a>

* Ideally, one would write the terraform script from the scratch using this [doc](https://learn.hashicorp.com/collections/terraform/modules).
* Here we have already written the terraform script that provisions the production-grade DIGIT Infra and can be customized with the specified configuration.
* Let's Clone the [DIGIT-DevOps GitHub repo](https://github.com/egovernments/DIGIT-DevOps/tree/release) where the terraform script to provision EKS cluster is available and below is the structure of the files.

```
git clone --branch release https://github.com/egovernments/DIGIT-DevOps.git
cd DIGIT-DevOps/infra-as-code/terraform


└── modules
    ├── kubernetes
    │   └── aws
    │       ├── eks-cluster
    │       │   ├── main.tf
    │       │   ├── outputs.tf
    │       │   └── variables.tf
    │       ├── network
    │       │   ├── main.tf
    │       │   ├── outputs.tf
    │       │   └── variables.tf
    │       └── workers
    │           ├── main.tf
    │           ├── outputs.tf
    │           └── variables.tf
    └── storage
        └── aws
            ├── main.tf
            ├── outputs.tf
            └── variables.tf
```

In here, you will find the **main.tf** under each of the modules that has the provisioning definition for resources like EKS cluster, and Storage, etc. All these are modularized and reacts as per the customized options provided.

**Example:**

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
* **Storage Module**
  * Configuration in this directory creates EBS volume and attaches it together.
* The following main.tf with create s3 bucket to store all the state of the execution to keep track
* ```
  DIGIT-DevOps/Infra-as-code/terraform/egov-cicd/remote-state

  [**main.tf**](https://github.com/egovernments/DIGIT-DevOps/blob/release/infra-as-code/terraform/egov-cicd/remote-state/main.tf)\*\*\*\*
  ```

```
provider "aws" {
  region = "ap-south-1"
}

#This is a bucket name that you can name as you wish
resource "aws_s3_bucket" "terraform_state" {
  bucket = "try-cicd-workshop-yourname" 

  versioning {
    enabled = true
  }

  lifecycle {
    prevent_destroy = true
  }
}

#This is a bucket name that you can name as you wish
resource "aws_dynamodb_table" "terraform_state_lock" {
  name           = "try-cicd-workshop-yourname"
  read_capacity  = 1
  write_capacity = 1
  hash_key       = "LockID"

  attribute {
    name = "LockID"
    type = "S"
  }
}
```

1.  The following main.tf contains the detailed resource definitions that need to be provisioned, please have a look at it.

    Dir: DIGIT-DevOps/Infra-as-code/terraform/egov-cicd
2. [**main.tf**](https://raw.githubusercontent.com/egovernments/DIGIT-DevOps/release/infra-as-code/terraform/egov-cicd/main.tf)

```
terraform {
  backend "s3" {
    bucket = "try-cicd-workshop-yourname"
    key = "terraform"
    region = "ap-south-1"
  }
}

module "network" {
  source             = "../modules/kubernetes/aws/network"
  vpc_cidr_block     = "${var.vpc_cidr_block}"
  cluster_name       = "${var.cluster_name}"
  availability_zones = "${var.network_availability_zones}"
}

module "iam_user_deployer" {
  source  = "terraform-aws-modules/iam/aws//modules/iam-user"

  name          = "${var.cluster_name}-kube-deployer"
  force_destroy = true  
  create_iam_user_login_profile = false
  create_iam_access_key         = true

  # User "egovterraform" has uploaded his public key here - https://keybase.io/egovterraform/pgp_keys.asc
  pgp_key = "${var.iam_keybase_user}"
}

module "iam_user_admin" {
  source  = "terraform-aws-modules/iam/aws//modules/iam-user"

  name          = "${var.cluster_name}-kube-admin"
  force_destroy = true  
  create_iam_user_login_profile = false
  create_iam_access_key         = true

  # User "egovterraform" has uploaded his public key here - https://keybase.io/egovterraform/pgp_keys.asc
  pgp_key = "${var.iam_keybase_user}"
}

module "iam_user_user" {
  source  = "terraform-aws-modules/iam/aws//modules/iam-user"

  name          = "${var.cluster_name}-kube-user"
  force_destroy = true  
  create_iam_user_login_profile = false
  create_iam_access_key         = true

  # User "test" has uploaded his public key here - https://keybase.io/test/pgp_keys.asc
  pgp_key = "${var.iam_keybase_user}"
}

data "aws_eks_cluster" "cluster" {
  name = "${module.eks.cluster_id}"
}

data "aws_eks_cluster_auth" "cluster" {
  name = "${module.eks.cluster_id}"
}
provider "kubernetes" {
  host                   = "${data.aws_eks_cluster.cluster.endpoint}"
  cluster_ca_certificate = "${base64decode(data.aws_eks_cluster.cluster.certificate_authority.0.data)}"
  token                  = "${data.aws_eks_cluster_auth.cluster.token}"
  load_config_file       = false
  version                = "~> 1.11"
}

module "eks" {
  source          = "terraform-aws-modules/eks/aws"
  cluster_name    = "${var.cluster_name}"
  cluster_version = "${var.kubernetes_version}"
  subnets         = "${concat(module.network.private_subnets, module.network.public_subnets)}"

  tags = "${
    map(
      "kubernetes.io/cluster/${var.cluster_name}", "owned",
      "KubernetesCluster", "${var.cluster_name}"
    )
  }"

  vpc_id = "${module.network.vpc_id}"

  worker_groups_launch_template = [
    {
      name                    = "spot"
      subnets                 = "${slice(module.network.private_subnets, 0, length(var.availability_zones))}"
      override_instance_types = "${var.override_instance_types}"
      asg_max_size            = "${var.number_of_worker_nodes}"
      asg_desired_capacity    = "${var.number_of_worker_nodes}"
      kubelet_extra_args      = "--node-labels=node.kubernetes.io/lifecycle=spot"
      spot_allocation_strategy= "lowest-price"
      spot_max_price          = "${var.spot_max_price}"
      spot_instance_pools     = 1
      cpu_credits             = "standard"
    },
  ]
  
  map_users    = [
    {
      userarn  = "${module.iam_user_deployer.this_iam_user_arn}"
      username = "${module.iam_user_deployer.this_iam_user_name}"
      groups   = ["system:masters"]
    },
    {
      userarn  = "${module.iam_user_admin.this_iam_user_arn}"
      username = "${module.iam_user_admin.this_iam_user_name}"
      groups   = ["global-readonly", "digit-user"]
    },
    {
      userarn  = "${module.iam_user_user.this_iam_user_arn}"
      username = "${module.iam_user_user.this_iam_user_name}"
      groups   = ["global-readonly"]
    },    
  ]
}

module "jenkins" {

  source = "../modules/storage/aws"
  storage_count = 1
  environment = "${var.cluster_name}"
  disk_prefix = "jenkins-home"
  availability_zones = "${var.availability_zones}"
  storage_sku = "gp2"
  disk_size_gb = "20"
  
}
```

## Custom variables/configurations: <a href="#set-up-an-environment" id="set-up-an-environment"></a>

You can define your configurations in **variables.tf** and provide the env specific cloud requirements so that using the same terraform template you can customize the configurations.

```
├── egov-cicd
│   ├── main.tf 
│   ├── outputs.tf
│   ├── providers.tf
│   ├── remote-state
│   │   └── main.tf
│   └── variables.tf
```

Following are the values that you need to mention in the following files, the blank ones will be prompted for inputs while execution.

\*\*\*\*[**variables.tf**](https://raw.githubusercontent.com/egovernments/DIGIT-DevOps/release/infra-as-code/terraform/egov-cicd/variables.tf)

```
#
# Variables Configuration
#

variable "cluster_name" {
  default = "<Desired Cluster name>"  #eg: my-digit-cicd
}

variable "vpc_cidr_block" {
  default = "192.168.0.0/16"
}

variable "network_availability_zones" {
  default = ["ap-south-1b", "ap-south-1a"]
}

variable "availability_zones" {
  default = ["ap-south-1b"]
}

variable "kubernetes_version" {
  default = "1.18"
}

variable "instance_type" {
  default = "t3a.xlarge"
}

variable "override_instance_types" {
  default = ["t3.xlarge", "r5ad.xlarge", "r5a.xlarge", "t3a.xlarge"]
}

variable "number_of_worker_nodes" {
  default = "1"
}

variable "spot_max_price" {
  default = "0.0538"
}

variable "ssh_key_name" {
  default = "egov-cicd"
}
variable "iam_keybase_user" {
  default = "keybase:egovterraform"
}
```

### **Important: Create your own keybase key before you run the terraform**

* Use this URL [https://keybase.io/](https://keybase.io) to [create your own PGP key](https://pgpkeygen.com), this will create both public and private key in your machine, upload the public key into the [keybase](https://keybase.io) account that you have just created, and give a name to it and ensure that you mention that in your terraform. This allows to encrypt all the sensitive information.
  * Example user keybase user in eGov case is "_egovterraform_" needs to be created and has to uploaded his public key here - [https://keybase.io/egovterraform/pgp\_keys.asc](https://keybase.io/egovterraform/pgp\_keys.asc)
  * you can use this [portal](https://8gwifi.org/pgpencdec.jsp) to Decrypt your secret key. To decrypt PGP Message, Upload the PGP Message, PGP Private Key and Passphrase.

## Run terraform

Now that we know what the terraform script does, the resources graph that it provisions and what custom values should be given with respect to your env.

Let's begin to run the terraform scripts to provision infra required to Deploy DIGIT on AWS.

1. First CD into the following directory and run the following command 1-by-1 and watch the output closely.

```
cd DIGIT-DevOps/infra-as-code/terraform/egov-cicd/remote-state
terraform init
terraform plan
terraform apply


cd DIGIT-DevOps/infra-as-code/terraform/egov-cicd
terraform init
terraform plan
terraform apply
```

Upon Successful execution following resources gets created which can be verified by the command "terraform output"

* **s3 bucket:** to store terraform state.
* **Network:** VPC, security groups.
* **IAM users auth:** using keybase to create admin, deployer, the user. Use this URL [https://keybase.io/](https://keybase.io) to [create your own PGP key](https://pgpkeygen.com), this will create both public and private key in your machine, upload the public key into the [keybase](https://keybase.io) account that you have just created, and give a name to it and ensure that you mention that in your terraform. This allows to encrypt all the sensitive information.
  * Example user keybase user in eGov case is "_egovterraform_" needs to be created and has to uploaded his public key here - [https://keybase.io/egovterraform/pgp\_keys.asc](https://keybase.io/egovterraform/pgp\_keys.asc)
  * you can use this [portal](https://8gwifi.org/pgpencdec.jsp) to Decrypt your secret key. To decrypt PGP Message, Upload the PGP Message, PGP Private Key and Passphrase.
* **EKS cluster:** with master(s) & worker node(s).
* **Storage(s):** for es-master, es-data-v1, es-master-infra, es-data-infra-v1, zookeeper, kafka, kafka-infra.
* Use this link to [get the kubeconfig from EKS](https://docs.aws.amazon.com/eks/latest/userguide/create-kubeconfig.html) to get the kubeconfig file and being able to connect to the cluster from your local machine so that you should be able to deploy DIGIT services to the cluster.

```
aws sts get-caller-identity

# Run the below command and give the respective region-code and the cluster name
aws eks --region <region-code> update-kubeconfig --name <cluster_name>
```

1. Finally, Verify that you are able to connect to the cluster by running the following command

```
kubectl config use-context <your cluster name>

kubectl get nodes

NAME                                             STATUS AGE   VERSION               OS-Image           
ip-192-168-xx-1.ap-south-1.compute.internal   Ready  45d   v1.18.10-eks-bac369   Amazon Linux 2   
```

Whola! All set and now you can go **Deploy Jenkins**...

## 2. Jenkins Deployment

Post infra setup (Kubernetes Cluster), We start with deploying the Jenkins and kaniko-cache-warmer.

### Prerequisites:

* Sub Domain to expose CI/CD URL
* GitHub [Oauth App](https://docs.github.com/en/developers/apps/building-oauth-apps/creating-an-oauth-app)
* [GitHub User ssh key](https://docs.github.com/en/developers/apps/building-oauth-apps/creating-an-oauth-app)
* With [GitHub user generate a personal read only access token](https://docs.github.com/en/github/authenticating-to-github/keeping-your-account-and-data-secure/creating-a-personal-access-token)
* [Docker hub account details](https://hub.docker.com/signup) (username and password)
* SSL Certificate for the sub-domain

**Prepare an <**[**ci.yaml> master config file**](https://github.com/egovernments/DIGIT-DevOps/blob/release/deploy-as-code/helm/environments/ci-demo.yaml) **and <**[**ci-secrets.yaml**](https://github.com/egovernments/DIGIT-DevOps/blob/release/deploy-as-code/helm/environments/ci-demo-secrets.yaml)**>, you can name this file as you wish which will have the following configurations.**

* credentials, secrets (You need to encrypt using [sops](https://github.com/mozilla/sops#updatekeys-command) and create a **ci-secret.yaml** separately)
* Check and Update [**ci-secrets.yaml**](https://github.com/egovernments/DIGIT-DevOps/blob/release/deploy-as-code/helm/environments/ci-demo-secrets.yaml) \*\*\*\*details (like githuh Oauth app clientId and clientSecret, GitHub user details gitReadSshPrivateKey and gitReadAccessToken etc..)
* To create Jenkins namespace mark this [flag](https://github.com/egovernments/DIGIT-DevOps/blob/release/deploy-as-code/helm/environments/ci-demo.yaml#L5) **true**
* Add your env's kubconfigs under kubConfigs like [https://github.com/egovernments/DIGIT-DevOps/blob/release/deploy-as-code/helm/environments/ci-demo-secrets.yaml#L12](https://github.com/egovernments/DIGIT-DevOps/blob/release/deploy-as-code/helm/environments/ci-demo-secrets.yaml#L12)
* KubeConfig env's name and deploymentJobs name from ci.yaml should be the same
* Update the [CIOps](https://github.com/egovernments/DIGIT-DevOps/blob/release/deploy-as-code/helm/charts/backbone-services/jenkins/values.yaml#L419) and [DIGIT-DevOps](https://github.com/egovernments/DIGIT-DevOps/blob/release/deploy-as-code/helm/charts/backbone-services/jenkins/values.yaml#L484) repo name with your forked repo name and provide read-only access to github user to those repo's.
* SSL Certificate for the sub-domain

```
cd DIGIT-DevOps/tree/release/deploy-as-code
```

```
kubectl config use-context <your cluster name>
go run main.go deploy -c -e ci 'jenkins,kaniko-cache-warmer,nginx-ingress'
```

You have launch the Jenkins, Same you can access through your sub-domain which you configured in ci.yaml
