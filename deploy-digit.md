# Deploy DIGIT

## Pre-Requisites: <a id="pre-requisites"></a>

* On-premise/private cloud accounts
  * Interface to access and provision required infra
  * In case of SDC, NIC or private DC, it'll be VPN to a allocated vLan.
  * SSH access to the VMs/machines.
* Infra Requirements
  * Public cloud
    * Managed kubernetes service like AKS or EKS or GKE on Azure, AWS and GCP respectively
  * Private Clouds \(SDC, NIC\)
    * Clouds like VMware, OpenStack, Nutanix and more, may or may not have kubernetes as a managed service. If yes we may have to estimate only the worker nodes depending on number of ULBs and DIGIT's municipal services that you opt.
    * In the absence of the above, you have to provision kubernetes cluster from the plain VMs as per the general kubernetes setup instruction and add worker nodes.
* Skills
  * Understanding of Linux, containers, VM Instances, Load Balancers, Security Groups/Firewalls, nginx, DB Instance, Data Volumes.
  * Experience of kubernetes, docker, jenkins, helm, Infra-as-code, Terraform.
  * Experience on DevOps/SRE practice on a Microservices and modern infrastructure.

## High level action to deploy DIGIT <a id="high-level-action-to-deploy-digit"></a>

1. 2. Setting up the [persistent disk volumes](https://medium.com/asl19-developers/create-readwritemany-persistentvolumeclaims-on-your-kubernetes-cluster-3a8db51f98e3) to attach to DIGIT backbone [stateful containers](https://medium.com/swlh/stupid-simple-kubernetes-persistent-volumes-explained-by-examples-29f8fec08c4) like
   * ZooKeeper
   * Kafka
   * Elastic Search
3. Setting up the PostGres DB
   * On a public cloud, provision a Postgres RDS like instance.
   * Private cloud, provision a postgres DB on a VM with the backup, HA/DRS.
4. Preparing Deployment configuration for required DIGIT services using [Helm](https://medium.com/better-programming/docker-kubernetes-and-helm-4b5a5a87bc8f) Templates from the [InfraOps](https://github.com/egovernments/Train-InfraOps) like the following
   * Preparing DIGIT Service [helm templates](https://medium.com/ingeniouslysimple/deploying-kubernetes-applications-with-helm-81c9c931f9d3) to deploy on kubernetes cluster
   * K8s Secrets
   * K8s ConfigMaps
   * Environment variables of each microservices
5. Deploy the stable released version of DIGIT and Required services
6. Setting up Jenkins Job to build, bake images and deploy the components for the rolling updates.
7. 
