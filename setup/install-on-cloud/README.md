---
description: >-
  Complete DIGIT Installation step-by-step Instructions across various Infra
  types like Public & Private Clouds
---

# Full Installation

While [**Quickstart Guide**](../quickstart.md) would have helped you to get your hands dirty and build the Kubernetes cluster on a local/single VM instance, which you can consider for either local development, or to understand the details involved in infra and deployment.

However, DIGIT is a [**cloud-native**](https://www.appdynamics.com/topics/what-is-cloud-native-architecture#\~3-challenges) platform at the same time [**cloud agnostic**](https://looker.com/definitions/cloud-agnostic#:\~:text=Cloud%2Dagnostic%20platforms%20are%20environments,different%20features%20and%20price%20structures.), depending on the scale and performance running **DIGIT on production** requires advanced capabilities like HA, DRS, autoscaling, resiliency, etc.. all these capabilities are provided out of the box by the commercial clouds like **AWS, Google, Azure, VMware, OpenStack, etc..** and also the private clouds like **NIC** and **few SDCs implemented clouds**, all these cloud providers provide the **kubernetes-as-a-managed-service** that makes the entire infra setup and management seamless and automated, like **infra-as-code, config-as-code**.

Before we jump into the supported cloud providers, it is important to know DIGIT is completely cloud agnostic, be it a commercial clouds or on premise, the differentiator is just that when the cloud provider provides kubernetes as a managed service or not. In cased on managed services like [EKS, AKS, GKE](https://www.stackrox.io/blog/eks-vs-gke-vs-aks-jan2021/), etc we do not need to provision and manage the kubernetes from the ground up, just the working knowledge of the kubernetes is enough. When the kubernetes manages service is not available, we need to first create the kubernetes cluster out of available/required no of VMs and then ensure we manage the cluster itself apart from running just the workloads. To get more understanding on kubernetes and managed kubernetes services, please go through the following pre-read.&#x20;

## Pre-read:

* Know the basics of Kubernetes: [https://www.youtube.com/watch?v=PH-2FfFD2PU\&t=3s](https://www.youtube.com/watch?v=PH-2FfFD2PU\&t=3s)
* Know the [basics of kubectl](https://www.tutorialspoint.com/kubernetes/kubernetes\_kubectl\_commands.htm) commands
* Know kubernetes manifests: [https://www.youtube.com/watch?v=ohSUtEfDefc](https://www.youtube.com/watch?v=ohSUtEfDefc)
* Know how to manage env values, secrets of any service deployed in kubernetes [https://www.youtube.com/watch?v=OW244LxB4oI](https://www.youtube.com/watch?v=OW244LxB4oI)
* Know how to port forward to a pod running inside k8s cluster and work locally [https://www.youtube.com/watch?v=TT3nd5n5Yus](https://www.youtube.com/watch?v=TT3nd5n5Yus)
* Know sops to secure your keys/creds: [https://www.youtube.com/watch?v=DWzJ87KbwxA](https://www.youtube.com/watch?v=DWzJ87KbwxA)

## v1. Choose the Cloud

Choose your cloud and follow the Instruction to setup a Kubernetes cluster before moving on to the Deployment.

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

