---
description: >-
  Quickstart Installation helps you jump start with the DIGIT basic installation
  steps with the limited functionalities.
---

# Quickstart

## Demo/Evaluation Installations

Quickstart solutions that you give you the ability to try setting up DIGIT Infra quickly. These are not meant for production use as is.

If you want to install DIGIT on Lightweight Kubernetes ([k3d](https://github.com/rancher/k3d) ) for proofs of concept, see the open source project [k3d](https://github.com/rancher/k3d).  You can install DIGIT in a local or cloud VM when you have all the below pre-requisites and hardware requirement.

### Requirements

To use k3d, make sure your instance meets the following requirements:

* **Linux distribution** running in a VM or bare metal
  * Ubuntu 18.04 or Debian 10 (VM or bare metal)
  * 2 vCPUs (recommend 4)
  * 8GiB of RAM (recommend 16)
  * 30GiB of HDD (recommend 40+)
  * NAT or Bridged networking with access to the internet
  * Install `curl`, `wget` `git`, and `tar` (if they're not already installed):
    * `sudo apt-get install curl git wget tar`
  * Install [Docker](https://docs.docker.com/engine/install/ubuntu/)
  * [Install kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/) on Linux
  * Open terminal and Install k3d(v4.4.8) on Linux using the below command
    * `wget -q -O - https://raw.githubusercontent.com/k3d-io/k3d/main/install.sh | TAG=v4.4.8 bash`           &#x20;
*   **OSX**

    * Docker Desktop local Kubernetes cluster enabled
    * At least 6 GiB of memory allocated to Docker Desktop
    * Install [Docker Desktop](https://docs.docker.com/docker-for-mac/install/) and local Kubernetes cluster enabled
    * [Install kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl-macos/) on Mac
    * Install k3d(v4.4.8) on Mac, on terminal use [Homebrew](https://brew.sh) (Homebrew is available for MacOS) using the below command
      * `brew install k3d` &#x20;

    ****
* **Windows 10 or above**
  * [Docker Desktop for windows](https://docs.docker.com/docker-for-windows/install/#system-requirements-for-wsl-2-backend) need to be installed
  * [Install kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl-windows/) on Windows
  * [Install Chocolatey](https://chocolatey.org) package manager for windows
  * Install [GitBash](https://git-scm.com/download/win) as an alternative command prompt that allows most of the Linux commands on windows.
  * Now open gitbash and Install k3d(v4.4.8) on Windows using the below command
    * `choco install k3d`

## **1. Infra (Kubernetes Cluster) Creation**

**When the above prerequisites are met and the docker is up and running, run the following tasks depending upon your OS.**

1. &#x20;login/ssh into the machine and run the following in terminal/command prompt.
2. Create /Kube directory and change permission. This will be used as k3d cluster persistent storage to store metadata and container logs .&#x20;
   1.  ```
       mkdir /kube
       chmod 777 /kube

       if you are unable to create the /kube folder in the root, you can create it your user directory and provide the absolue path below
       ```


3. Create a k3d cluster with a single master node and 2 agents (Worker Nodes) and mount the above created directory (for data persistence).
   1. `k3d cluster create --k3s-server-arg "--no-deploy=traefik" --agents 2 -v "/kube:/kube@agent[0,1]" -v "/kube:/kube@server[0]" --port "80:80@loadbalancer"`
4. When cluster creation is successful, Get the kubeconfig file, which will allow you to connect the to the cluster.
   1. `k3d kubeconfig get k3s-default > myk3dconfig`
   2. `kubectl config use-context k3d-k3s-default --kubeconfig=myk3dconfig`
5. Verify the Cluster creation by running the following commands from your local machine where the kubectl is installed. It gives you the sample output as below if everything works fine.
   1.  `root@ip:/# kubectl cluster-info`

       `OutPut`

       ```
       Kubernetes control plane is running at https://0.0.0.0:33931
       CoreDNS is running at https://0.0.0.0:33931/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy
       Metrics-server is running at https://0.0.0.0:33931/api/v1/namespaces/kube-system/services/https:metrics-server:/proxy
       ```


   2.  `root@ip:/# k3d cluster list`

       `OutPut:`

       ```
       NAME          SERVERS   AGENTS   LOADBALANCER
       k3s-default   1/1       2/2      true
       ```


   3.  `root@ip:/# kubectl get nodes`

       `OutPut:`

       ```
       NAME                       STATUS   ROLES                  AGE     VERSION
       k3d-k3s-default-agent-0    Ready    <none>                 3d18h   v1.21.1+k3s1
       k3d-k3s-default-agent-1    Ready    <none>                 3d18h   v1.21.1+k3s1
       k3d-k3s-default-server-0   Ready    control-plane,master   3d18h   v1.21.1+k3s1

       ```


   4.  `root@ip:/# kubectl top nodes`

       `OutPut:`

       ```
       W0625 07:56:24.588781   12810 top_node.go:119] Using json format to get metrics. Next release will switch to protocol-buffers, switch early by passing --use-protocol-buffers flag
       NAME                       CPU(cores)   CPU%   MEMORY(bytes)   MEMORY%   
       k3d-k3s-default-agent-0    547m         6%     1505Mi          9%        
       k3d-k3s-default-agent-1    40m          0%     2175Mi          13%       
       k3d-k3s-default-server-0   59m          0%     2286Mi          14%  
       ```



If the above steps are completed successfully, your Cluster is now up and running ready to proceed with the DIGIT Deployment.

## **2. DIGIT Deployment on k3d**

Now that we have the Infra setup to proceed with the DIGIT Deployment. Following are the tools that need to be installed on the machine before proceeding with the DIGIT Services deployment.

**What we'll deploy in Quickstart:**

* DIGIT's core platform services
* PGR

### **Prerequisites**

1. DIGIT uses [golang](https://golang.org/doc/install#download) (required v1.13.3) automated scripts to deploy the builds on to Kubernetes - [Linux](https://golang.org/dl/go1.13.3.linux-amd64.tar.gz) or [Windows](https://golang.org/dl/go1.13.3.windows-amd64.msi) or [Mac](https://golang.org/dl/go1.13.3.darwin-amd64.pkg)
2. All DIGIT services are packaged using helm charts[ ![](https://helm.sh/img/favicon-152.png)Installing Helm](https://helm.sh/docs/intro/install/)
3. [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/) is a CLI to connect to the kubernetes cluster from your machine
4. Install [CURL](https://help.ubidots.com/en/articles/2165289-learn-how-to-install-run-curl-on-windows-macosx-linux) for making api calls
5. [Install Visualstudio](https://code.visualstudio.com/download) IDE Code for better code/configuration editing capabilities
6. [Install Postman](https://www.postman.com/downloads/) to run digit bootstrap scripts

### Prepare Deployment Configs

1. Clone the following [GitRepo](https://github.com/egovernments/DIGIT-DevOps), you may need to [install git](https://docs.github.com/en/github/creating-cloning-and-archiving-repositories/cloning-a-repository-from-github/cloning-a-repository) and then run [git clone](https://docs.github.com/en/github/creating-cloning-and-archiving-repositories/cloning-a-repository-from-github/cloning-a-repository) it to your machine.
   * ```
     root@ip:/# git clone -b quickstart https://github.com/egovernments/DIGIT-DevOps 
     ```
2. After cloning the repo CD into the folder DIGIT-DevOps and type the "code ." command that will open the visual editor and opens all the files from the repo DIGIT-DevOps
   * ```
     root@ip:/# cd DIGIT-DevOps
     root@ip:DIGIT-DevOps# code .
     ```
3. Create your deployment config file, you can use the following template  [sample deployment config file](https://github.com/egovernments/DIGIT-DevOps/blob/quickstart/deploy-as-code/helm/environments/quickstart-config.yaml) and update the required details if needed. (For a quick start you can run as it is)
   1. ```
      https://github.com/egovernments/DIGIT-DevOps/blob/quickstart/deploy-as-code/helm/environments/quickstart-config.yaml
      ```
4. Add the following entries in your host file /etc/hosts depending on your OS, instructions can be found below.
   * [ ] [Ubuntu](http://manpages.ubuntu.com/manpages/trusty/man5/hosts.5.html)
   * [ ] [Windows](https://www.groovypost.com/howto/edit-hosts-file-windows-10/)
   * [ ] [MacOS](https://www.imore.com/how-edit-your-macs-hosts-file-and-why-you-would-want#page1)
5. When you find it, add following lines to the hosts file, save and close the file.
   * `127.0.0.1 quickstart.local.digit`

### Deployment

Now we have all the deployments configs ready, we can now run the following command and provide the necessary details asked and this interactive installer will take care of the rest.

1. Run the egov-deployer go script&#x20;

```
root@ip:# cd DIGIT-DevOps/deploy-as-code/egov-deployer

root@ip:# go run digit_setup.go

#Be prepared for the following questions
1. Do you have the Kubernetes Setup?
2. Provide the path of the intented env kubeconfig file
3. Which version of the DIGIT that you want to install - Choose "Quickstart"
4. What DIGIT Modules that you choose to install
5. All, done, Now do you want to preview the deployment manifests 
6. Are you good to proceed with the DIGIT Installation

All Done.
```

2\. You can now test the Digit application status in command prompt/terminal by using the below command.

```
curl -Is http://quickstart.local.digit/employee/login |  head -n 1

OutPut:
HTTP/2 200
```

**Note**: Initially pgr-services would be in crashloopbackoff state, but after performing below Post Deployment Steps pgr-services will start running.&#x20;

## 3. Post Deployment Steps

Post deployment, now the application will be accessible from the configured domain.

To try out PGR employee login, Lets create a sample tenant, city, user to login and assign LME employee role through the seed script

1. We have to do the [kubectl port-forwarding](https://phoenixnap.com/kb/kubectl-port-forward) of the **egov-user** service running from kubernetes cluster to your localhost, this will now give you access to egov-user service directly and interact with the api directly.

```
kubectl port-forward svc/egov-user 8080:8080 -n egov
Forwarding from 127.0.0.1:8080 -> 8080
Forwarding from [::1]:8080 -> 8080
```

2\. Seed the sample data

* Ensure you have the postman to run the following seed data api, if not [Install postman](https://www.postman.com/downloads/canary/) on your local
* Import the following postman collection into the postman and run it, this will have the seed data that enable sample test users and localisation data.
  * [DIGIT Bootstrap](https://raw.githubusercontent.com/egovernments/DIGIT-DevOps/quickstart/deploy-as-code/bootstrap\_scripts/seed\_data.json)

![](<../.gitbook/assets/image (112) (1).png>)

![](<../.gitbook/assets/image (113) (1).png>)

To test the kubernetes operations through kubectl from you local machine, please execute the below commands.

```bash
#get the pods running in the cluster
kubectl get pods -n egov

Output:

NAME                                                    READY   STATUS    RESTARTS   AGE
citizen-79cf89659c-8glf4                                1/1     Running   0          14d
egov-accesscontrol-78b78dddb9-tfbkf                     1/1     Running   0          21d
egov-enc-service-574cd7b5b5-hmhh4                       1/1     Running   0          36d
egov-idgen-84954b565b-xsnqj                             1/1     Running   0          45d
egov-indexer-5f5fbb6f4b-58rtm                           1/1     Running   0          43d
egov-localization-6cc5977bb9-gm7f9                      1/1     Running   0          27d
egov-mdms-service-65d6d65d8c-t85d9                      1/1     Running   0          21d
egov-user-6676968d76-8n6t6                              1/1     Running   0          29d
egov-workflow-v2-5cdb96bcf5-dcgmf                       1/1     Running   0          36d
employee-749464fbfb-tptlh                               1/1     Running   0          14d
nginx-ingress-controller-b9678869c-mkslb                1/1     Running   0          49d
pgr-services-b9f4ffdbf-5h5kd                            1/1     Running   0          38d
zuul-788bf8cd8b-9nxfl                                   1/1     Running   0          41d


#Delete the pods so that it gets restarted automatically

kubectl delete pods zuul-788bf8cd8b-9nxfl egov-workflow-v2-5cdb96bcf5-dcgmf pgr-services-b9f4ffdbf-5h5kd -n egov

Output:

pod "zuul-788bf8cd8b-9nxfl" deleted
pod "egov-workflow-v2-5cdb96bcf5-dcgmf" deleted
pod "pgr-services-b9f4ffdbf-5h5kd" deleted
```

You have successfully completed the DIGIT Infra, Deployment setup and Installed a DIGIT - PGR module.

{% hint style="info" %}
You can try experimenting the different DIGIT modules by installing them in your cluster with your H/W or VM complying to higher level machine configuration of increased number of vCPUs. RAM and storage size.
{% endhint %}
