---
description: DIGIT Installation step-by-step Instructions across various Infra types
---

# Install

The [Quickstart Guide](../quickstart.md) would have helped you to get your hands dirty and build the Kubernetes cluster on a local/single VM instance, which you can consider for either local development, or to understand the details involved in infra and deployment.

 However, DIGIT is a [**cloud-native**](https://www.appdynamics.com/topics/what-is-cloud-native-architecture#~3-challenges) platform at the same time [**cloud agnostic**](https://looker.com/definitions/cloud-agnostic#:~:text=Cloud%2Dagnostic%20platforms%20are%20environments,different%20features%20and%20price%20structures.), depending on the scale and performance running **DIGIT on production** requires advanced capabilities like HA, DRS, autoscaling, resiliency, etc.. all these capabilities are provided out of the box by the commercial clouds like **AWS, Google, Azure, VMware, OpenStack, etc..** and also the private clouds like **NIC** and **few SDCs implemented clouds**, all these cloud providers provide the **kubernetes-as-a-managed-service** that makes the entire infra setup and management seamless and automated, like **infra-as-code, config-as-code**. 

## 1. Choose the Cloud

* \*\*\*\*[**AWS**](on-aws.md)\*\*\*\*
* \*\*\*\*[**Azure**](on-azure.md)\*\*\*\*
* \*\*\*\*[**GCP**](on-gcp.md)\*\*\*\*
* \*\*\*\*[**NIC**](on-nic.md)\*\*\*\*
* \*\*\*\*[**SDC**](on-sdc.md)\*\*\*\*

## 2. Deploy DIGIT

Post infra setup \(Kubernetes Cluster\), the deployment has got 2 stages and 2 modes. We can see the stages first and then the modes.

### 2 Stages

**Stage 1: Prepare a &lt;**[**env.yaml&gt; master config file**](https://github.com/egovernments/DIGIT-DevOps/blob/master/deploy-as-code/helm/environments/dev.yaml) **per env like dev, qa or prod, which will have the following configurations, this env file need to be in line with your cluster name.** 

* each service global, local env variables 
* credentials, secrets \(You need to encrypt using [sops](https://github.com/mozilla/sops#updatekeys-command) and create a **&lt;env&gt;-secret.yaml** separately\)
* Number of replicas/scale of individual services  \(Depending on whether dev or prod\)
* mdms, config repos \(Master Data, ULB, Tenant details, Users, etc\)
* sms g/w, email g/w, payment g/w
* GMap key \(In case you are using Google Map services in your PGR, PT, TL, etc\)
* S3 Bucket for Filestore
* URL/DNS on which the DIGIT will be exposed
* SSL Certificate for the above URL
* End-points configs \(Internal/external\)

**Stage 2: Run the digit\_setup deployment script and simply answer the questions that it asks.**

```text
cd DIGIT-DevOps/deploy-as-code/egov-deployer

go run digit_setup.go

#Be prepared for the following questions
1. Do you have the Kubernetes Setup?
2. Provide the path of the intented env kubeconfig file
3. Which version of the DIGIT that you want to install
4. What DIGIT Modules that you choose to install
5. All, done, Now do you want to preview the deployment manifests 
6. Are you good to proceed with the DIGIT Installation

All Done.
```

All Done, wait and watch for 10 min, you'll have the DIGIT setup completed and the application will be running on the given URL.

### The 2 Modes of Deployment

Essentially, DIGIT deployment means that we need to generate Kubernetes manifests for each individual service. We use the tool called helm, which is an easy, effective and customizable packaging and deployment solution. So depending on where and which env you initiate the deployment there are 2 modes that you can deploy.

1. From local machine
2. From CI/CD System like Jenkins













