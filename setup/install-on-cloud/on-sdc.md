# On SDC

Running Kubernetes on-premise gives a cloud-native experience on SDC when it comes to Deploying DIGIT.

Whether States have their own on-premise data centre or have decided to forego the various managed cloud solutions, there are a few things one should know when getting started with on-premise K8s.

One should be familiar with Kubernetes and the [control plane](https://kubernetes.io/docs/concepts/overview/components/#master-components) consists of the Kube-apiserver, Kube-scheduler, Kube-controller-manager and an ETCD datastore. For managed cloud solutions like [Google’s Kubernetes Engine (GKE)](https://cloud.google.com/kubernetes-engine/) or [Azure’s Kubernetes Service (AKS)](https://azure.microsoft.com/en-us/services/kubernetes-service/) it also includes the cloud-controller-manager. This is the component that connects the cluster to the external cloud services to provide networking, storage, authentication, and other feature support.

To successfully deploy a bespoke Kubernetes cluster and achieve a cloud-like experience on SDC, one need to replicate all the same features you get with a managed solution. At a high-level this means that we probably want to:

* Automate the deployment process
* Choose a networking solution
* Choose the right storage solution
* Handle security and authentication

Let us look at each of these challenges individually, and we’ll try to provide enough of an overview to aid you in getting started.

## Automating the deployment process

Using a tool like an ansible can make deploying Kubernetes clusters on-premise trivial.

When deciding to manage your own Kubernetes clusters, we need to set up a few proof-of-concept (PoC) clusters to learn how everything works, perform performance and conformance tests, and try out different configuration options.

After this phase, automating the deployment process is an important if not necessary step to ensure consistency across any clusters you build. For this, you have a few options, but the most popular are:

* [**kubeadm**](https://kubernetes.io/docs/reference/setup-tools/kubeadm/kubeadm/): a low-level tool that helps you bootstrap a minimum viable Kubernetes cluster that conforms to best practices
* [**kubespray**](https://github.com/kubernetes-sigs/kubespray): an ansible playbook that helps deploy production-ready clusters

If you already using ansible, kubespray is a great option otherwise we recommend writing automation around kubeadm using your preferred playbook tool after using it a few times. This will also increase your confidence and knowledge in the tooling surrounding Kubernetes.



[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)_​_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in/) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
