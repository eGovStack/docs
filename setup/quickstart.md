---
description: >-
  Quickstart solutions gives you the ability to try DIGIT out quickly. These are
  not meant for production use as is.
---

# Quickstart

DIGIT is a distributed microservice based platform that comprise of many services which are containerized and can be run on any container supported orchestration platform like dockers, kubernetes, etc,

Here in this Quickstart guide we'll create a lightweight kubernetes cluster called [k3d](https://github.com/rancher/k3d) on either local machine or on a VM of a specific H/W requirement. Below is the H/W requirement to ensure before we proceed further.

## 1. Machine Requirements

To setup k3d \(a minimal installation of Kubernetes\), make sure your windows/Linux/Mac instance meets the following requirements:

### **H/W  or VM Size:**

* 8 vCPUs \(recommend 8\)
* 16GiB of RAM \(recommend 16\)
* 30GiB of HDD \(recommend 40+\)

### **OS Specifications:** 

* **Linux distribution running in a VM or bare metal**
  * Ubuntu 18.04 or Debian 10 \(VM or bare metal\)
  * Install [Docker](https://docs.docker.com/engine/install/ubuntu/)
  * [Install kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/) on Linux
* **OSX or MacBook**
  * [Docker Desktop](https://docs.docker.com/docker-for-mac/install/) local Kubernetes cluster enabled
  * [Install kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl-macos/) on Mac
* **Windows 10 or above**
  * [Docker Desktop for windows](https://docs.docker.com/docker-for-windows/install/#system-requirements-for-wsl-2-backend) need to be installed
  * [Install Chocolatey](https://chocolatey.org) package manager for windows 
  * [Install kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl-windows/) on Windows

## **2. Install K3d:**

**Please follow this** [**instructions**](https://github.com/rancher/k3d) **with respect to your OS and install the k3d on the machine.** 

## **3. Setup DIGIT**

**Prerequisites:** Following are the tools that need to be installed on the machine before proceeding with the DIGIT Services deployment

**Tools:**

* DIGIT uses [golang](https://www.systutorials.com/how-to-install-go-1-13-x-on-ubuntu-18-04/) \(required v1.13\) automated scripts to deploy the builds on to kubernetes. 
* Install sops[ mozilla/sops](https://github.com/mozilla/sops#download) in case you need to use encrypted configurations like userid/pwd
* All DIGIT services are packaged using helm charts[ ![](https://helm.sh/img/favicon-152.png)Installing Helm](https://helm.sh/docs/intro/install/)
* kubectl is a cli to connect to the kuberntes cluster from your machine[ ![](https://kubernetes.io/images/favicon.png)Install and Set Up kubectl on Linux](https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/)
* aws-cli[ Installing, updating, and uninstalling the AWS CLI version 2 on Linux - AWS Command Line Interface](https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2-linux.html)
* git[ ![](https://git-scm.com/favicon.ico)Git - Installing Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
* aws-iam-authenticator [Install aws-iam-authenticator](https://docs.aws.amazon.com/eks/latest/userguide/install-aws-iam-authenticator.html)
* Visualstudio Code [https://code.visualstudio.com/download](https://code.visualstudio.com/download)
* Terraform \(v14.10\)[![](https://www.terraform.io/assets/images/favicons/apple-touch-icon-5c2d0048.png)Terraform](https://www.terraform.io/docs/cli/install/apt.html)



