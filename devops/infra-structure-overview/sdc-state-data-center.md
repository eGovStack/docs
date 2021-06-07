---
description: State Data Centres with On-Premise Kubernetes Clusters
---

# SDC

## What to know when deploying Kubernetes on SDC

Running Kubernetes on-premise gives a cloud-native experience or SDC becomes cloud-agnostic when it comes to the experience of Deploying DIGIT.

Whether States have their own on-premise data centre, have decided to forego the various managed cloud solutions, there are few things one should know when getting started with on-premise K8s.

One should be familiar with Kubernetes and one should know that the [control plane](https://kubernetes.io/docs/concepts/overview/components/#master-components) consists of the Kube-apiserver, Kube-scheduler, Kube-controller-manager and an ETCD datastore. For managed cloud solutions like [Google’s Kubernetes Engine \(GKE\)](https://cloud.google.com/kubernetes-engine/) or [Azure’s Kubernetes Service \(AKS\)](https://azure.microsoft.com/en-us/services/kubernetes-service/) it also includes the cloud-controller-manager. This is the component that connects the cluster to the external cloud services to provide networking, storage, authentication, and other feature support.

To successfully deploy a bespoke Kubernetes cluster and achieve a cloud-like experience on SDC, one need to replicate all the same features you get with a managed solution. At a high-level this means that we probably want to:

* Automate the deployment process
* Choose a networking solution
* Choose a storage solution
* Handle security and authentication

Let us look at each of these challenges individually, and we’ll try to provide enough of an overview to aid you in getting started.

## Automating the deployment process

Using a tool like an ansible can make deploying Kubernetes clusters on-premise trivial.

When deciding to manage your own Kubernetes clusters, we need to set up a few proof-of-concept \(PoC\) clusters to learn how everything works, perform performance and conformance tests, and try out different configuration options.

After this phase, automating the deployment process is an important if not necessary step to ensure consistency across any clusters you build. For this, you have a few options, but the most popular are:

* \*\*\*\*[**kubeadm**](https://kubernetes.io/docs/reference/setup-tools/kubeadm/kubeadm/): a low-level tool that helps you bootstrap a minimum viable Kubernetes cluster that conforms to best practices
* [**kubespray**](https://github.com/kubernetes-sigs/kubespray): an ansible playbook that helps deploy production- ready clusters

If you already using ansible, kubespray is a great option otherwise we recommend writing automation around kubeadm using your preferred playbook tool after using it a few times. This will also increase your confidence and knowledge in the tooling surrounding Kubernetes.

## Choosing a network solution

When designing clusters, choosing the right container networking interface \(CNI\) plugin can be the hardest part. This is because choosing a CNI that will work well with an existing network topology can be tough. Do you need BGP peering capabilities? Do you want an overlay network using vxlan? How close to bare-metal performance are you trying to get?

There are a lot of articles that compare the various CNI provider solutions \(calico, weave, flannel, kube-router, etc.\) that are must-reads like the [_benchmark results of Kubernetes network plugins_](https://itnext.io/benchmark-results-of-kubernetes-network-plugins-cni-over-10gbit-s-network-updated-april-2019-4a9886efe9c4) article. We usually recommend Project Calico for its maturity, continued support, and large feature set or flannel for its simplicity.

For ingress traffic, you’ll need to pick a load-balancer solution. For a simple configuration, you can use MetalLB, but if you’re lucky enough to have F5 hardware load-balancers available we recommend checking out the [K8s F5 BIG-IP Controller](https://clouddocs.f5.com/containers/v2/kubernetes/). The controller supports connecting your network plugin to the F5 either through either vxlan or BGP peering. This gives the controller full visibility into pod health and provides the best performance.

## Choosing a storage solution

Kubernetes provides a number of [included storage volume plugins](https://kubernetes.io/docs/concepts/storage/storage-classes/#provisioner). If you’re going on-premise you’ll probably want to use network-attached storage \(NAS\) option to avoid forcing pods to be pinned to specific nodes.

For a cloud-like experience, you’ll need to add a plugin to dynamically create persistent volume objects that match the user’s persistent volume claims. You can use dynamic provisioning to reclaim these volume objects after a resource has been deleted.

Pure Storage has a great example helm chart, the [_Pure Service Orchestrator_ \(PSO\)](https://github.com/purestorage/helm-charts), that provides smart provisioning although it only works for Pure Storage products.

## Handle security and authentication

As anyone familiar with security knows, this is a rabbit-hole. You can always make your infrastructure more secure and should be investing in continual improvements.

Including different Kubernetes plugins can help build a secure, cloud-like experience for your users

When designing on-premise clusters you’ll have to decide where to draw the line. To really harden your cluster’s security you can add plugins like:

* [istio](https://istio.io/): provides the underlying secure communication channel, and manages authentication, authorization, and encryption of service communication at scale
* [gVisor](https://github.com/google/gvisor): is a user-space kernel, written in Go, that implements a substantial portion of the Linux system surface
* [vault](https://www.vaultproject.io/docs/): secure, store and tightly control access to tokens, passwords, certificates, encryption keys for protecting secrets and other sensitive data

For user authentication, we recommend checking out [guard](https://github.com/appscode/guard) which will integrate with an existing authentication provider. If you’re already using Github teams to then this could be a no-brainer.

## Other Considerations

Hope this has given you a good idea of deploying, networking, storage, and security for you to take the leap into deploying your own on-premise Kubernetes clusters. Like we mentioned above, the team will want to build proof-of-concept clusters, run conformance and performance tests, and really become experts on Kubernetes if you’re going to be using it to run DIGIT on production.

We’ll leave you with a few other things the team should be thinking of:

* Externally backing up Kubernetes YAML, namespaces, and configuration files
* Running applications across clusters in an active-active configuration to allow for zero-downtime updates
* Running game days like deleting the CNI to measure and improve time-to-recovery

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)​](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation](https://egov.org.in/) is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).

