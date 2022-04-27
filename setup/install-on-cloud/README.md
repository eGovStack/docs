---
description: >-
  Complete DIGIT Installation step-by-step Instructions across various Infra
  types like Public & Private Clouds
---

# Full Installation

While [**Quickstart Guide**](../quickstart/) \*\*\*\*would have helped you to get your hands dirty and build the Kubernetes cluster on a local/single VM instance, which you can consider for either local development, or to understand the details involved in infra and deployment.

However, DIGIT is a [**cloud-native**](https://www.appdynamics.com/topics/what-is-cloud-native-architecture#\~3-challenges) platform at the same time [**cloud agnostic**](https://looker.com/definitions/cloud-agnostic#:\~:text=Cloud%2Dagnostic%20platforms%20are%20environments,different%20features%20and%20price%20structures.), depending on the scale and performance running **DIGIT on production** requires advanced capabilities like HA, DRS, autoscaling, resiliency, etc.. all these capabilities are provided out of the box by the commercial clouds like **AWS, Google, Azure, VMware, OpenStack, etc..** and also the private clouds like **NIC** and **few SDCs implemented clouds**, all these cloud providers provide the **kubernetes-as-a-managed-service** that makes the entire infra setup and management seamless and automated, like **infra-as-code, config-as-code**.

## Pre-read:

* Know the basics of Kubernetes: [https://www.youtube.com/watch?v=PH-2FfFD2PU\&t=3s](https://www.youtube.com/watch?v=PH-2FfFD2PU\&t=3s)
* Know the [basics of kubectl](https://www.tutorialspoint.com/kubernetes/kubernetes\_kubectl\_commands.htm) commands
* Know kubernetes manifests: [https://www.youtube.com/watch?v=ohSUtEfDefc](https://www.youtube.com/watch?v=ohSUtEfDefc)
* Know how to manage env values, secrets of any service deployed in kubernetes [https://www.youtube.com/watch?v=OW244LxB4oI](https://www.youtube.com/watch?v=OW244LxB4oI)
* Know how to port forward to a pod running inside k8s cluster and work locally [https://www.youtube.com/watch?v=TT3nd5n5Yus](https://www.youtube.com/watch?v=TT3nd5n5Yus)
* Know sops to secure your keys/creds: [https://www.youtube.com/watch?v=DWzJ87KbwxA](https://www.youtube.com/watch?v=DWzJ87KbwxA)

## v1. Choose the Cloud

Choose you cloud and follow the Instruction to setup a Kubernetes cluster before moving on to the Deployment.

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

Post infra setup (Kubernetes Cluster), the deployment has got 2 stages and 2 modes. We can see the stages first and then the modes. As part of a sample exercise we can deploy PGR, however deployment steps are similar, just that the prerequisites will have to be configured accordingly.

### The 2 Stages

**Stage 1:** I**t's important to prepare an <**[**env.yaml> master config file**](https://github.com/egovernments/DIGIT-DevOps/blob/release/deploy-as-code/helm/environments/egov-demo-sample.yaml) **and** [**\<env-secrets.yaml>**](https://github.com/egovernments/DIGIT-DevOps/blob/release/deploy-as-code/helm/environments/egov-demo-sample-secrets.yaml) **file before starting DIGIT deployment, you can name this file as you wish which will have the following configurations, this env file needs to be in line with your cluster name**.

* credentials, secrets (You need to encrypt using [sops](https://github.com/mozilla/sops#updatekeys-command) and create a [**\<env>-secret.yaml**](https://github.com/egovernments/DIGIT-DevOps/blob/release/deploy-as-code/helm/environments/egov-demo-sample-secrets.yaml) separately)
* **Note**: For demo purposes, you can use the [egov-demo-secrets.yaml](https://github.com/egovernments/DIGIT-DevOps/blob/release/deploy-as-code/helm/environments/egov-demo-secrets.yaml) as it is, By changing the file name and adding your respective secret details. But we would urge you to use the [sops](https://github.com/mozilla/sops#updatekeys-command) to encrypt your secrets.
* Number of replicas/scale of individual services (Depending on whether dev or prod)
* It is important to [fork](https://docs.github.com/en/get-started/quickstart/fork-a-repo) the [mdms](https://github.com/egovernments/egov-mdms-data), and [config](https://github.com/egovernments/configs) repos (Master Data, ULB, Tenant details, Users, etc) to your respective github account.
* Once you fork the repos, Create one [github user account](https://docs.github.com/en/get-started/signing-up-for-github/signing-up-for-a-new-github-account), and for ssh authentication [generate new SSH key ](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)and [add it to your account](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account).
* New github user should have the access to earlier forked repo's and add your ssh private key which you generated in the previous step to [\<env-secrets.yaml>](https://github.com/egovernments/DIGIT-DevOps/blob/release/deploy-as-code/helm/environments/egov-demo-sample-secrets.yaml#L36)
* You must update sms g/w, email g/w, payment g/w details <[env.yaml>](https://github.com/egovernments/DIGIT-DevOps/blob/release/deploy-as-code/helm/environments/egov-demo-sample.yaml) and [\<env-secrets.yaml>](https://github.com/egovernments/DIGIT-DevOps/blob/release/deploy-as-code/helm/environments/egov-demo-sample-secrets.yaml) to work the notifaction and payment gateway services.
* Update GMap key (In case you are using Google Map services in your PGR, PT, TL, etc)
* You must create one private s3 Bucket for Filestore and one public bucket for logos and add the bucket details to [\<env.yaml>](https://github.com/egovernments/DIGIT-DevOps/blob/release/deploy-as-code/helm/environments/egov-demo-sample.yaml#L94)and [\<env.yaml>](https://github.com/egovernments/DIGIT-DevOps/blob/release/deploy-as-code/helm/environments/egov-demo-sample.yaml#L20) respectively and create an IAM user with the s3 bucket access. Add IAM user details to [\<env-secrets.yaml>](https://github.com/egovernments/DIGIT-DevOps/blob/release/deploy-as-code/helm/environments/egov-demo-sample-secrets.yaml#L11).
* Terraform output provides you the ebs volumes id's for kafka-v2, zookeeper-v2, elasticsearch-data-v1 ,and elasticsearch-master-v1 add those volumes id's in [\<env.yaml>](https://github.com/egovernments/DIGIT-DevOps/blob/release/deploy-as-code/helm/environments/egov-demo-sample.yaml#L290-L546)
* URL/DNS on which the DIGIT will be exposed
* SSL Certificate for the above URL
* End-points configs (Internal/external)

****[**SOPS Configuration**](https://github.com/mozilla/sops#2usage)**:**

&#x20;     1\. Generate PGP keys [https://fedingo.com/how-to-generate-pgp-key-in-ubuntu/](https://fedingo.com/how-to-generate-pgp-key-in-ubuntu/)

&#x20;      **Optional**: 2. Create KMS keys [https://docs.aws.amazon.com/kms/latest/developerguide/create-keys.html](https://docs.aws.amazon.com/kms/latest/developerguide/create-keys.html)

&#x20;      3\. Once you generate your encryption key,  create a **.sops.yaml** configuration file at the helm directory to define which keys are used for which filename. refer to the sops [doc](https://github.com/mozilla/sops#211using-sopsyaml-conf-to-select-kmspgp-for-new-files) for info.

&#x20;   &#x20;

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

**Once deployment is done, Create** [**cname**](https://in.godaddy.com/help/add-a-cname-record-19236) **record with load balancer id and domain.**

### The 2 Modes of Deployment

Essentially, DIGIT deployment means that we need to generate Kubernetes manifests for each individual service. We use the tool called helm, which is an easy, effective and customizable packaging and deployment solution. So depending on where and which env you initiate the deployment there are 2 modes that you can deploy.

1. From local machine - whatever we are trying in this sample exercise so far.
2. Advanced: From CI/CD System like Jenkins - Depending on how you want to setup your CI/CD and the expertise the steps will vary, however [here](../more-deploy-docs/deployment-key-concepts/cicd.md) you can find how we have setup CI/CD on Jenkins and the pipelines are created automatically without any manual intervention.

## 3. Post Deployment Steps

Post deployment, now the application will be accessible from the configured domain.

To try out PGR employee login, Lets create a sample tenant, city, user to login and assign LME employee role through the seed script

1. We have to do the [kubectl port-forwarding](https://phoenixnap.com/kb/kubectl-port-forward) of the **egov-user** service running from kubernetes cluster to your localhost, this will now give you access to egov-user service directly and interact with the api directly.

```
kubectl port-forward svc/egov-user 8080:8080 -n egov
Forwarding from 127.0.0.1:8080 -> 8080
Forwarding from [::1]:8080 -> 8080
```

1. Seed the sample data

* Ensure you have the postman to run the following seed data api, if not [Install postman](https://www.postman.com/downloads/canary/) on your local
* Import the following postman collection into the postman and run it, this will have the seed data that enable sample test users and localisation data.
  * [DIGIT Bootstrap](https://raw.githubusercontent.com/egovernments/DIGIT-DevOps/quickstart/deploy-as-code/bootstrap\_scripts/seed\_data.json)

![](<../../.gitbook/assets/image (112) (1).png>)

![](<../../.gitbook/assets/image (113) (1).png>)

## 4. Assessment of the DIGIT Deployment

By now we have successfully completed the digit setup on cloud, use the URL that you mentioned in your env.yaml Eg: https://mysetup.digit.org and create a grievance to ensure the PGR module deployed is working fine. Refer the below product documentation for the steps.

**Credentials:**

1. Citizen: You can use your default mobile number (9999999999) to signin using the default Mobile OTP 123456.
2. Employee: Username: **GRO** and password: **eGov@4321**

{% content-ref url="../../product/modules/public-grievances-and-redressal/pgr-user-manual/" %}
[pgr-user-manual](../../product/modules/public-grievances-and-redressal/pgr-user-manual/)
{% endcontent-ref %}

Post grievance creation and assignment of the same to LME, capture the screenshot of the same and share it to ensure your setup is working fine.

## 5. Destroy the Cluster

Post validating the PGR functionality share the API response of the following request to assess the correctness of successful DIGIT PGR Deployment.

Finally, cleanup the DIGIT Setup if you wish, using the following command. This will delete the entire cluster and other cloud resources that were provisioned for the DIGIT Setup.

```
cd DIGIT-DevOps/infra-as-code/terraform/my-digit-eks
terraform destroy
```

## Conclusion:

All Done, we have successfully Created infra on Cloud, Deployed Digit, Bootstrapped DIGIT, Performed a Transaction on PGR and Finally Destroyed the cluster.
