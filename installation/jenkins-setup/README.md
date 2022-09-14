---
description: CI/CD setup
---

# CI/CD SetUp

**On this page:**

* [Pre-requisites for CI/CD setup](./#prerequisites)
* [Cluster setup ](./#ci-cd-cluster-setup)
* [Resource graph in Terraform script](./#set-up-and-initialize-your-terraform-workspace)
* &#x20;[Configurations & custom variables](./#set-up-an-environment)
* [Run Terraform Scripts](./#run-terraform)
* [Jenkins deployment](./#2.-jenkins-deployment)

## Pre-requisites <a href="#prerequisites" id="prerequisites"></a>

1. [GitHub Organization account](https://docs.github.com/en/organizations/collaborating-with-groups-in-organizations/creating-a-new-organization-from-scratch)
2. [Fork](https://docs.github.com/en/get-started/quickstart/fork-a-repo) the repos below to your GitHub Organization account&#x20;
   * &#x20;[https://github.com/egovernments/DIGIT-DevOps](https://github.com/egovernments/DIGIT-DevOps)
   * [https://github.com/egovernments/CIOps](https://github.com/egovernments/CIOps)
3. [AWS KMS](https://docs.aws.amazon.com/kms/index.html)
4. [Go lang](https://golang.org/doc/install) (version 1.13.X)
5. [SOPS](https://github.com/mozilla/sops#updatekeys-command)
6. [GitHub user](https://docs.github.com/en/get-started/signing-up-for-github/signing-up-for-a-new-github-account)
7. [Docker Hub account](https://hub.docker.com/signup)
8. ​[**AWS account**](https://portal.aws.amazon.com/billing/signup?nc2=h\_ct\&src=default\&redirect\_url=https%3A%2F%2Faws.amazon.com%2Fregistration-confirmation#/start) with admin access to provision EKS Service. Try subscribing to a free AWS account to learn the basics. There is a limit on [**what is offered as free**](https://aws.amazon.com/free/)**.** This demo requires a commercial subscription to the EKS service. The cost for a one or two days trial might range between Rs 500-1000. **(Note: Post the demo, for the internal folks, eGov will provide a 2-3 hrs time-bound access to eGov's AWS account based on the request and the available number of slots per day).**
9. Install [**kubectl**](https://kubernetes.io/docs/tasks/tools/) on your local machine to interact with the Kubernetes cluster.
10. Install [**Helm**](https://helm.sh/docs/intro/install/) to help package the services along with the configurations, environment, secrets, etc into a [**Kubernetes manifests**](https://devspace.cloud/docs/cli/deployment/kubernetes-manifests/what-are-manifests)**.**
11. Install [**terraform**](https://releases.hashicorp.com/terraform/0.14.10/) version (0.14.10) for the Infra-as-code (IaC) to provision cloud resources as code and with desired resource graph. It also helps destroy the cluster in one go.
12. **​**[**Install AWS CLI**](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-install.html) on your local machine so that you can use AWS CLI commands to provision and manage the cloud resources on your account.
13. Install [**AWS IAM Authenticator**](https://docs.aws.amazon.com/eks/latest/userguide/install-aws-iam-authenticator.html) to help authenticate your connection from your local machine and deploy DIGIT services.
14. Use the [**AWS IAM User**](https://docs.aws.amazon.com/IAM/latest/UserGuide/id\_users\_create.html) **credentials provided** for the Terraform ([**Infra-as-code**](https://devops.digit.org/devops-general/infra-as-code)) to connect to the AWS account and provision the cloud resources.

    ​

    * You will receive a **Secret Access Key** and **Access Key ID**. **Save the keys.**
    * Open the terminal and run the command given below. The AWS CLI is already installed and the credentials are saved. (Provide the credentials, leave the region and output format blank).

    ```
    aws configure --profile cicd-infra-account 

    AWS Access Key ID []:<Your access key>
    AWS Secret Access Key []:<Your secret key>
    Default region name []: ap-south-1
    Default output format []: text
    ```

    * The above creates the following file on your machine as /Users/.aws/credentials.

    ```
    [cicd-infra-account] 
    aws_access_key_id=*********** 
    aws_secret_access_key=****************************
    ```

## CI/CD Cluster Setup

[**Terraform**](https://www.terraform.io/intro/index.html) helps you build a graph of all your resources and parallelizes the creation or modification of any non-dependent resources. Thus, Terraform builds infrastructure as efficiently as possible while providing the operators clear insight into the dependencies on the infrastructure.

Before we provision the cloud resources, we need to understand and be sure about what resources need to be provisioned by Terraform to deploy CI/CD.

The following is the resource graph that we are going to provision using terraform in a standard way so that every time and for every environment, the infra is the same.

* EKS Control Plane (Kubernetes master)
* Work node group (VMs with the estimated number of vCPUs, Memory)
* EBS Volumes (Persistent volumes)
* VPCs (Private networks)
* Users to access, deploy and read-only

## **Resource Graph In** Terraform Script <a href="#set-up-and-initialize-your-terraform-workspace" id="set-up-and-initialize-your-terraform-workspace"></a>

* Ideally, one would write the terraform script from the scratch using this [doc](https://learn.hashicorp.com/collections/terraform/modules).
* Here we have already written the terraform script that provisions the production-grade DIGIT Infra and can be customized with the specified configuration.
* Clone the [DIGIT-DevOps GitHub repo](https://github.com/egovernments/DIGIT-DevOps/tree/release). The terraform script to provision EKS cluster is available in this repo. The structure of the files is given below.

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

Here, you will find the **main.tf** under each of the modules that have the provisioning definition for resources like EKS cluster, storage, etc. All these are modularized and react as per the customized options provided.

**Example:**

* **VPC Resources:**
  * VPC
  * Subnets
  * Internet Gateway
  * Route Table
* **EKS Cluster Resources:**
  * IAM Role to allow EKS service to manage other AWS services
  * EC2 Security Group to allow networking traffic with the EKS cluster
  * EKS Cluster
* **EKS Worker Nodes Resources:**
  * IAM role allowing Kubernetes actions to access other AWS services
  * EC2 Security Group to allow networking traffic
  * Data source to fetch the latest EKS worker AMI
  * AutoScaling launch configuration to configure worker instances
  * AutoScaling group to launch worker instances
* **Storage Module**
  * Configuration in this directory creates EBS volume and attaches it together.

The following main.tf with create s3 bucket to store all the states of the execution to keep track.

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

The following main.tf contains the detailed resource definitions that need to be provisioned.

Dir: DIGIT-DevOps/Infra-as-code/terraform/egov-cicd

[**main.tf**](https://raw.githubusercontent.com/egovernments/DIGIT-DevOps/release/infra-as-code/terraform/egov-cicd/main.tf)

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
  #load_config_file       = false
}
  
module "eks" {
  source          = "terraform-aws-modules/eks/aws"
  version         = "17.24.0"
  cluster_name    = "${var.cluster_name}"
  vpc_id          = "${module.network.vpc_id}"
  cluster_version = "${var.kubernetes_version}"
  subnets         = "${concat(module.network.private_subnets, module.network.public_subnets)}"

  worker_groups = [
    {
      name                          = "spot"
      subnets                       = "${concat(slice(module.network.private_subnets, 0, length(var.availability_zones)))}"
      override_instance_types       = "${var.override_instance_types}"
      kubelet_extra_args            = "--node-labels=node.kubernetes.io/lifecycle=spot"
      additional_security_group_ids = ["${module.network.worker_nodes_sg_id}"]
      asg_max_size                  = "${var.number_of_worker_nodes}"
      asg_desired_capacity          = "${var.number_of_worker_nodes}"
      spot_allocation_strategy      = "capacity-optimized"
      spot_instance_pools           = null
    }
  ]
  tags = "${
    tomap({
      "kubernetes.io/cluster/${var.cluster_name}" = "owned",
      "KubernetesCluster" = "${var.cluster_name}"
    })
  }"
 
}

module "jenkins" {

  source = "../modules/storage/aws"
  storage_count = 1
  environment = "${var.cluster_name}"
  disk_prefix = "jenkins-home"
  availability_zones = "${var.availability_zones}"
  storage_sku = "gp2"
  disk_size_gb = "50"
  
}
```

## Custom Variables/Configurations <a href="#set-up-an-environment" id="set-up-an-environment"></a>

Define your configurations in **variables.tf** and provide the environment-specific cloud requirements. The same terraform template can be used to customize the configurations.

```
├── egov-cicd
│   ├── main.tf 
│   ├── outputs.tf
│   ├── providers.tf
│   ├── remote-state
│   │   └── main.tf
│   └── variables.tf
```

Following are the values that you need to mention in the following files. The blank ones will prompt for inputs during execution.

[**variables.tf**](https://raw.githubusercontent.com/egovernments/DIGIT-DevOps/release/infra-as-code/terraform/egov-cicd/variables.tf)

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
```

## Run Terraform Scripts

We have covered what the terraform script does, the resources graph that it provisions and what custom values should be given with respect to the selected environment.

Now, run the Terraform scripts to provision infra required to Deploy DIGIT on AWS.

Use the 'cd' command to change to the following directory and run the following commands. Check the output.

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

After successful execution, the following resources get created and can be verified by the command "terraform output".

* **s3 bucket:** to store terraform state
* **Network:** VPC, security groups
* **IAM users auth:** using keybase to create admin, deployer, the user

Use the URL [https://keybase.io/](https://keybase.io/) to [create your own PGP key](https://pgpkeygen.com/). This creates both public and private keys on the machine, upload the public key into the [keybase](https://keybase.io/) account that you have just created, give a name to it and ensure that you mention that in your terraform. This allows you to encrypt sensitive information.

* Example: Create user keybase. This is "_egovterraform_" in the case of eGov. Upload the public key here - [https://keybase.io/egovterraform/pgp\_keys.asc](https://keybase.io/egovterraform/pgp\_keys.asc)
* Use this [portal](https://8gwifi.org/pgpencdec.jsp) to Decrypt the secret key. To decrypt the PGP message, upload the PGP Message, PGP Private Key and Passphrase.
* **EKS cluster:** with master(s) & worker node(s).
* **Storage(s):** for es-master, es-data-v1, es-master-infra, es-data-infra-v1, zookeeper, kafka, kafka-infra.
* Use this link to [get the kubeconfig from EKS](https://docs.aws.amazon.com/eks/latest/userguide/create-kubeconfig.html) to fetch the kubeconfig file. This enables you to connect to the cluster from your local machine and deploy DIGIT services to the cluster.

```
aws sts get-caller-identity

# Run the below command and give the respective region-code and the cluster name
aws eks --region <region-code> update-kubeconfig --name <cluster_name>
```

Finally, verify that you are able to connect to the cluster by running the command below:

```
export KUBECONFIG=<path-to-your-kube_config>
kubectl config use-context <your cluster name>

kubectl get nodes

NAME                                             STATUS AGE   VERSION               OS-Image           
ip-192-168-xx-1.ap-south-1.compute.internal   Ready  45d   v1.18.10-eks-bac369   Amazon Linux 2   
```

Whola! All set and now you can **Deploy Jenkins**...

## Jenkins Deployment

Post infra setup (Kubernetes Cluster), we start with deploying the Jenkins and kaniko-cache-warmer.

### Pre-requisites

* Sub domain to expose CI/CD URL
* GitHub [Oauth App](https://docs.github.com/en/developers/apps/building-oauth-apps/creating-an-oauth-app) (this provides you with the [clientId](https://github.com/egovernments/DIGIT-DevOps/blob/release/config-as-code/environments/ci-demo-secrets.yaml#L4), [clientSecret](https://github.com/egovernments/DIGIT-DevOps/blob/release/config-as-code/environments/ci-demo-secrets.yaml#L5))
  * Under `Authorization callback URL` enter the below url ie (Replace \<domain\_name> with your domain) https://\<domain\_name>/securityRealm/finishLogin
* [Github User ](https://docs.github.com/en/get-started/signing-up-for-github/signing-up-for-a-new-github-account)
* [Generate a new ssh key for the above user](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent) (this provides the ssh public and private key)
* Add earlier created ssh public key to Github user [account](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account)
* Add  ssh private key to the [gitReadSshPrivateKey](https://github.com/egovernments/DIGIT-DevOps/blob/release/config-as-code/environments/ci-demo-secrets.yaml#L6)
* With previously created [GitHub users generate a personal read-only access token](https://docs.github.com/en/github/authenticating-to-github/keeping-your-account-and-data-secure/creating-a-personal-access-token)
* [Docker hub account details](https://hub.docker.com/signup) (username and password)
* SSL certificate for the sub-domain

**Prepare an <**[**ci.yaml> master config file**](https://github.com/egovernments/DIGIT-DevOps/blob/release/config-as-code/environments/ci-demo.yaml) **and <**[**ci-secrets.yaml**](https://github.com/egovernments/DIGIT-DevOps/blob/release/config-as-code/environments/ci-demo-secrets.yaml)**>. Name this file as desired. It has the following configurations:**

* credentials, secrets (you need to encrypt using [sops](https://github.com/mozilla/sops#updatekeys-command) and create a **ci-secret.yaml** separately)
* Add subdomain name in [ci.yaml](https://github.com/egovernments/DIGIT-DevOps/blob/release/config-as-code/environments/ci-demo.yaml#L2)
* Check and add your project specific [**ci-secrets.yaml**](https://github.com/egovernments/DIGIT-DevOps/blob/release/config-as-code/environments/ci-demo-secrets.yaml) details (like github Oauth app [clientId](https://github.com/egovernments/DIGIT-DevOps/blob/release/config-as-code/environments/ci-demo-secrets.yaml#L4), [clientSecret](https://github.com/egovernments/DIGIT-DevOps/blob/release/config-as-code/environments/ci-demo-secrets.yaml#L5), [gitReadSshPrivateKey](https://github.com/egovernments/DIGIT-DevOps/blob/release/config-as-code/environments/ci-demo-secrets.yaml#L6), [gitReadAccessToken](https://github.com/egovernments/DIGIT-DevOps/blob/release/config-as-code/environments/ci-demo-secrets.yaml#L35), [dockerConfigJson](https://github.com/egovernments/DIGIT-DevOps/blob/release/config-as-code/environments/ci-demo-secrets.yaml#L36), [dockerUsername](https://github.com/egovernments/DIGIT-DevOps/blob/release/config-as-code/environments/ci-demo-secrets.yaml#L47) and [dockerPassword](https://github.com/egovernments/DIGIT-DevOps/blob/release/config-as-code/environments/ci-demo-secrets.yaml#L48))
* To create Jenkins namespace mark this [flag](https://github.com/egovernments/DIGIT-DevOps/blob/release/config-as-code/environments/ci-demo.yaml#L7) **true**
* Add your environment-specific kubconfigs under kubConfigs like [https://github.com/egovernments/DIGIT-DevOps/blob/release/config-as-code/environments/ci-demo-secrets.yaml#L50](https://github.com/egovernments/DIGIT-DevOps/blob/release/config-as-code/environments/ci-demo-secrets.yaml#L50)
* KubeConfig [environment](https://github.com/egovernments/DIGIT-DevOps/blob/release/config-as-code/environments/ci-demo-secrets.yaml#L50) name and deploymentJobs name from [ci.yaml ](https://github.com/egovernments/DIGIT-DevOps/blob/release/config-as-code/environments/ci-demo.yaml#L37)should be the same
* Update the [CIOps](https://github.com/egovernments/DIGIT-DevOps/blob/release/config-as-code/helm/charts/backbone-services/jenkins/values.yaml#L414) and [DIGIT-DevOps](https://github.com/egovernments/DIGIT-DevOps/blob/release/config-as-code/helm/charts/backbone-services/jenkins/values.yaml#L479) repo ssh url with the forked repo's ssh url.
* Make sure earlier created github users have read-only access to the forked DIGIT-DevOps and CIOps repos.
* SSL Certificate for the sub-domain.

#### **Prepare CIOps Configs**

* Update the [DOCKER\_NAMESPACE](https://github.com/egovernments/CIOps/blob/master/vars/jobBuilder.groovy#L32) with your docker hub organization name.
* Update the repo name "egovio" with your docker hub organization name in [buildPipeline.groovy](https://github.com/egovernments/CIOps/blob/master/vars/buildPipeline.groovy#L101)
* Update the cache repo name [https://github.com/egovernments/CIOps/blob/master/vars/buildPipeline.groovy#L166](https://github.com/egovernments/CIOps/blob/master/vars/buildPipeline.groovy#L166)[https://github.com/egovernments/CIOps/blob/master/vars/buildPipeline.groovy#L185](https://github.com/egovernments/CIOps/blob/master/vars/buildPipeline.groovy#L185)
* Remove the below env:
  * [https://github.com/egovernments/CIOps/blob/master/vars/buildPipeline.groovy#L35-L54](https://github.com/egovernments/CIOps/blob/master/vars/buildPipeline.groovy#L35-L54)
  * [https://github.com/egovernments/CIOps/blob/master/vars/buildPipeline.groovy#L156-L159](https://github.com/egovernments/CIOps/blob/master/vars/buildPipeline.groovy#L156-L159)
  * [https://github.com/egovernments/CIOps/blob/master/vars/buildPipeline.groovy#L176-L179](https://github.com/egovernments/CIOps/blob/master/vars/buildPipeline.groovy#L176-L179)
  * [https://github.com/egovernments/CIOps/blob/master/vars/buildPipeline.groovy#L33-L34](https://github.com/egovernments/CIOps/blob/master/vars/buildPipeline.groovy#L33-L34)
* Remove the below volumeMounts:
  * [https://github.com/egovernments/CIOps/blob/master/vars/buildPipeline.groovy#L60-L61](https://github.com/egovernments/CIOps/blob/master/vars/buildPipeline.groovy#L60-L61)
  * [https://github.com/egovernments/CIOps/blob/master/vars/deployer.groovy#L20-L21](https://github.com/egovernments/CIOps/blob/master/vars/deployer.groovy#L20-L21)
* Remove the below volume:
  * [https://github.com/egovernments/CIOps/blob/master/vars/buildPipeline.groovy#L80-L87](https://github.com/egovernments/CIOps/blob/master/vars/buildPipeline.groovy#L80-L87)
  * [https://github.com/egovernments/CIOps/blob/master/vars/deployer.groovy#L32-L39](https://github.com/egovernments/CIOps/blob/master/vars/deployer.groovy#L32-L39)











```
cd DIGIT-DevOps/deploy-as-code/deployer
```

```
export KUBECONFIG=<path-to-your-kube_config>
kubectl config use-context <your cluster name>
go run main.go deploy -c -e ci 'jenkins,kaniko-cache-warmer,nginx-ingress,cert-manager'
```

Jenkins is launched. You can access the same through your sub-domain configured in ci.yaml.



[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)_​_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in/) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
