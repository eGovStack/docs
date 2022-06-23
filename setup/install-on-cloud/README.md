---
description: >-
  Complete DIGIT Installation step-by-step Instructions across various Infra
  types like Public & Private Clouds
---

# Full Installation

While [**Quickstart Guide**](../quickstart.md) would have helped you to get your hands dirty and build the Kubernetes cluster on a local/single VM instance, which you can consider for either local development, or to understand the details involved in infra and deployment.

DIGIT is a [**cloud-native**](https://www.appdynamics.com/topics/what-is-cloud-native-architecture#\~3-challenges) and [**cloud agnostic**](https://looker.com/definitions/cloud-agnostic) **** open source eGov stack, depending on the scale and performance running **DIGIT on production** requires advanced capabilities like HA, DRS, autoscaling, resiliency, etc.. most of these capabilities are provided out of the box by the commercial clouds like **AWS, Google, Azure, VMware, OpenStack, etc..** and also the private clouds like **NIC** and **few SDCs implemented clouds**, all these cloud providers provide the **kubernetes-as-a-managed-service** that makes the entire infra setup and management seamless and automated, like **infra-as-code, config-as-code**.

Before we jump into the supported cloud providers, it is important to know DIGIT is completely cloud agnostic, be it a commercial clouds or on premise, the differentiator is just that when the cloud provider provides kubernetes as a managed service or not. In case of managed services like [EKS, AKS, GKE](https://www.stackrox.io/blog/eks-vs-gke-vs-aks-jan2021/), etc.. we do not need to provision and manage the kubernetes cluster components from the ground up, just the working knowledge of the kubernetes is enough. In the absence of managed kubernetes service, we need to first create the kubernetes cluster itself out of available/required no of VMs and then ensure we manage the cluster apart from running the actual workloads. To get more understanding on kubernetes and managed kubernetes services, please go through the following pre-read.&#x20;

## Pre-reads

* Know the basics of Kubernetes: [https://www.youtube.com/watch?v=PH-2FfFD2PU\&t=3s](https://www.youtube.com/watch?v=PH-2FfFD2PU\&t=3s)
* Know the [basics of kubectl](https://www.tutorialspoint.com/kubernetes/kubernetes\_kubectl\_commands.htm) commands
* Know kubernetes manifests: [https://www.youtube.com/watch?v=ohSUtEfDefc](https://www.youtube.com/watch?v=ohSUtEfDefc)
* Know how to manage env values, secrets of any service deployed in kubernetes [https://www.youtube.com/watch?v=OW244LxB4oI](https://www.youtube.com/watch?v=OW244LxB4oI)
* Know how to port forward to a pod running inside k8s cluster and work locally [https://www.youtube.com/watch?v=TT3nd5n5Yus](https://www.youtube.com/watch?v=TT3nd5n5Yus)
* Know sops to secure your keys/creds: [https://www.youtube.com/watch?v=DWzJ87KbwxA](https://www.youtube.com/watch?v=DWzJ87KbwxA)



## Prerequisites

* Unlike quickstart, full installation requires state/user-specific configurations ready before proceeding with the deployment.
* You need to have the fully qualified DNS (URL) (Should not be dummy)
* Persistent storage depending on the cloud you are using for the Kafka, ES, etc.
* Either a standalone or a hosted PostGres DB above v11.x
* MDMS with the master data like Roles, Access, Actions, tenants, etc. Sample is [here](https://github.com/egovernments/egov-mdms-data)
* Gov services specific Configs like persister, searcher configs etc. Sample is [here](https://github.com/egovernments/configs) &#x20;
* GeoLocation provider configs (Google Location API), SMS Gateway, Payment Gateway, etc.

## 1. Choose the Cloud

Choose your cloud and follow the Instruction to set up a Kubernetes cluster before moving on to the Deployment.

{% content-ref url="on-aws.md" %}
[on-aws.md](on-aws.md)
{% endcontent-ref %}

{% content-ref url="on-azure.md" %}
[on-azure.md](on-azure.md)
{% endcontent-ref %}

{% content-ref url="on-gcp.md" %}
[on-gcp.md](on-gcp.md)
{% endcontent-ref %}

{% content-ref url="on-nic.md" %}
[on-nic.md](on-nic.md)
{% endcontent-ref %}

{% content-ref url="on-sdc.md" %}
[on-sdc.md](on-sdc.md)
{% endcontent-ref %}

## 2. Deploy DIGIT

Post infra setup (Kubernetes Cluster), the deployment involves 2 stages and 2 modes. Check out the stages first and then the modes. As part of a sample exercise, we will deploy the PGR module. However, deployment steps are similar.  The prerequisites have to be configured accordingly.

### The 2 Stages

**Stage 1: Prepare an <**[**env.yaml> master config file**](https://github.com/egovernments/DIGIT-DevOps/blob/master/deploy-as-code/helm/environments/dev.yaml)**, you can provide any name to this file. The file has the following configurations and this env file needs to be in line with your cluster name.**

* each service global, local env variables
* credentials, secrets (You need to encrypt using [sops](https://github.com/mozilla/sops#updatekeys-command) and create a **\<env>-secret.yaml** separately)
* Number of replicas/scale of individual services (Depending on whether dev or prod)
* mdms, config repos (Master Data, ULB, Tenant details, Users, etc)
* sms g/w, email g/w, payment g/w
* GMap key (In case you are using Google Map services in your PGR, PT, TL, etc)
* S3 Bucket for Filestore
* URL/DNS on which the DIGIT will be exposed
* SSL Certificate for the above URL
* End-points configs (Internal/external)

**Stage 2: Run the digit\_setup deployment script and simply answer the questions that it asks.**

```
cd DIGIT-DevOps/deploy-as-code/egov-deployer

go run digit_setup.go

#Be prepared for the following questions
1. Do you have the Kubernetes Setup?
2. Provide the path of the intented env kubeconfig file
3. Which version of the DIGIT that you want to install
4. What DIGIT Modules that you choose to install (Choose PGR)
5. All, done, Now do you want to preview the deployment manifests 
6. Are you good to proceed with the DIGIT Installation

All Done.
```

All Done, wait and watch for 10 min, you'll have the DIGIT setup completed and the application will be running on the given URL.

### The 2 Modes of Deployment

Essentially, DIGIT deployment means that we need to generate Kubernetes manifests for each individual service. We use the tool called Helm, which is an easy, effective and customizable packaging and deployment solution. So depending on where and which env you initiate the deployment there are 2 modes that you can deploy.

1. From local machine - whatever we are trying in this sample exercise so far.
2. Advanced: From CI/CD System like Jenkins - Depending on how you want to set up your CI/CD and the expertise the steps will vary, however [here](../more-deploy-docs/deployment-key-concepts/cicd.md) you can find how we have set up CI/CD on Jenkins and the pipelines are created automatically without any manual intervention.

## 3. Post Deployment Steps

Post-deployment - the application is now accessible from the configured domain.

To try out PGR employee login - Create a sample tenant, city, user to login and assign LME employee role using the seed script.

* [x] Run the [kubectl port-forwarding](https://phoenixnap.com/kb/kubectl-port-forward) of the **egov-user** service from Kubernetes cluster to your localhost. This gives you access to egov-user service directly and you can now interact with the API directly.

```
kubectl port-forward svc/egov-user 8080:8080 -n egov
Forwarding from 127.0.0.1:8080 -> 8080
Forwarding from [::1]:8080 -> 8080
```

* [x] Seed the sample data.
* [x] Ensure you have the postman to run the following seed data API.  If not, [Install postman](https://www.postman.com/downloads/canary/) on your local machine.
* [x] Import the following postman collection into the postman and run it. This collection has the seed data that enable sample test users and localisation data.
  * [DIGIT Bootstrap](https://raw.githubusercontent.com/egovernments/DIGIT-DevOps/quickstart/deploy-as-code/bootstrap\_scripts/seed\_data.json)

![](<../../.gitbook/assets/image (112) (1).png>)

![](<../../.gitbook/assets/image (113) (1).png>)

## 4. Assessment of the DIGIT Deployment

By now we have successfully completed the DIGIT setup on the cloud. Use the URL that you mentioned in your env.yaml Eg: https://mysetup.digit.org and create a grievance to ensure the PGR module deployed is working fine. Refer to the product documentation below for the steps.

**Credentials:**

1. Citizen: You can use your default mobile number (9999999999) to sign in using the default Mobile OTP 123456.
2. Employee: Username: **GRO** and password: **eGov@4321**

{% content-ref url="../../product/modules/public-grievances-and-redressal/pgr-user-manual/" %}
[pgr-user-manual](../../product/modules/public-grievances-and-redressal/pgr-user-manual/)
{% endcontent-ref %}

Post grievance creation and assignment of the same to LME, capture the screenshot of the same and share it to ensure your setup is working fine.

## 5. Destroy the Cluster

Post validating the PGR functionality share the API response of the following request to assess the correctness of successful DIGIT PGR Deployment.

Finally, clean up the DIGIT Setup if you wish, using the following command. This will delete the entire cluster and other cloud resources that were provisioned for the DIGIT Setup.

```
cd DIGIT-DevOps/infra-as-code/terraform/my-digit-eks
terraform destroy
```

## Conclusion

All Done, we have successfully created infra on the cloud, deployed DIGIT, bootstrapped DIGIT, performed a transaction on PGR and finally destroyed the cluster.



[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)_​_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in/) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
