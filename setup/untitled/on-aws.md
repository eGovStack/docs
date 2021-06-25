---
description: Provision infra for DIGIT on AWS using Terraform
---

# On AWS

The Amazon Elastic Kubernetes Service \(EKS\) is the AWS service an abstracted infrastructure requirement for deploying, managing, and scaling DIGIT on AWS.

## Prerequisites <a id="Prerequisites"></a>

* [AWS account](https://portal.aws.amazon.com/billing/signup?nc2=h_ct&src=default&redirect_url=https%3A%2F%2Faws.amazon.com%2Fregistration-confirmation#/start) with the IAM permissions listed on the [EKS module documentation](https://github.com/terraform-aws-modules/terraform-aws-eks/blob/master/docs/iam-permissions.md)
* AWS CLI configured
* AWS IAM Authenticator
* kubectl

### Set up Terraform with AWS <a id="Set-up-Terraform-with-AWS"></a>

The first thing to **set up** is **your Terraform**. We will **create an AWS IAM user for Terraform**.

In your **AWS console**, go to the **IAM section** and **create a user named “FullAccess”**. Then **add your user to a group** named “FullAccessGroup”. Attaches to this group the following rights:

* **AdministratorAccess**
* **AmazonEKSClusterPolicy**

After these steps, AWS will provide you a **Secret Access Key and Access Key ID**. **Save them precisely** because this will be the only time AWS gives it to you.

In your own console, create a ~/.aws/credentials file and put your credentials in it:

```text
[default] 
aws_access_key_id=*********** 
aws_secret_access_key=****************************
```

The last step is to **create this file**:

```text
[default]
 region=eu-west-3
```

## Set up and initialize your Terraform workspace <a id="Set-up-and-initialize-your-Terraform-workspace"></a>

‌Clone the following repository:

```text
git clone https://github.com/egovernments/DIGIT-DevOps.git
cd DIGIT-DevOps/infra-as-code/terraform
```

```text
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

In here, you will find three modules used to provision a EKS cluster, RDS, and Storage.

![EKS Architecture for DIGIT Setup](../../.gitbook/assets/image%20%28109%29.png)

#### Kubernetes module: <a id="Kubernetes-module:"></a>

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

#### Database Module: <a id="Database-Module:"></a>

Configuration in this directory creates set of RDS resources including DB instance, DB subnet group, and DB parameter group.

#### Storage Module: <a id="Storage-Module:"></a>

Configuration in this directory creates EBS volume and attaches it together.

## Set up an environment <a id="Set-up-an-environment"></a>

Here, you will find five files used to provision a VPC, security groups, IAM users, storages, EKS cluster, s3 bucket. The final product should be similar to this:

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

The source for each module in the [main.tf](http://main.tf/) is from the modules like:

```text
../modules/storage/aws
../modules/kubernetes/aws/eks-cluster
```

Configuration in this directory creates a set of:

* **s3 bucket:** to store terraform state.
* **Network:** VPC, security groups.
* **IAM users auth:** using keybase to create admin, deployer, the user.
  * Example user keybase user"_egovterraform_" needs to be created and has to uploaded his public key here - [https://keybase.io/egovterraform/pgp\_keys.asc](https://keybase.io/egovterraform/pgp_keys.asc)
* **EKS cluster:** with master\(s\) & worker node\(s\).
* **Storage\(s\):** for es-master, es-data-v1, es-master-infra, es-data-infra-v1, zookeeper, kafka, kafka-infra.

```text
cd eGov-infraOps/terraform/dev
terraform init
terraform plan
terraform apply
terraform output
```

The Kubernetes tools can be used to verify the newly created cluster. Once terraform apply execution is done it will generate the Kubernetes configuration file or you can get it from terraform state.

Set an environment variable so that kubectl picks up the correct config. Use this link to [get the kubeconfig from EKS](https://docs.aws.amazon.com/eks/latest/userguide/create-kubeconfig.html)

Verify the health of the cluster.

`kubectl get nodes`

You should see the details of your worker nodes, and they should all have a status Ready.![](blob:https://digit-discuss.atlassian.net/e26a285f-6386-4624-ab5a-3a151727a7fd#media-blob-url=true&id=d24de44e-31fc-4b61-8857-497b9a38e14c&collection=contentId-695861499&contextId=695861499&mimeType=image%2Fpng&name=assets%252F-MERG_iQW5oN4ukgXP8K%252F-MGDl14gRpdtvzEHtsDS%252F-MGDq14LK9hilL256Npl%252FScreenshot%2520from%25202020-09-02%252018-10-14.png%3Falt%3Dmedia%26token%3Da32b2594-3ec3-4323-83c4-da7a308f0223&size=26187&width=743&height=92)

