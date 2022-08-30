---
description: CI/CD setup
---

# CI/CD Setup on SDC

**On this page:**

* [Pre-requisites for CI/CD setup](ci-cd-setup-on-sdc.md#prerequisites)
* [Cluster setup ](ci-cd-setup-on-sdc.md#ci-cd-cluster-setup-with-kubespray)
* [Jenkins deployment](ci-cd-setup-on-sdc.md#ci-cd-build-job-pipeline-setup)

## Pre-requisites <a href="#prerequisites" id="prerequisites"></a>

1. [GitHub Organization account](https://docs.github.com/en/organizations/collaborating-with-groups-in-organizations/creating-a-new-organization-from-scratch)
2. [Fork](https://docs.github.com/en/get-started/quickstart/fork-a-repo) the repos below to your GitHub Organization account&#x20;
   * &#x20;[https://github.com/egovernments/DIGIT-DevOps](https://github.com/egovernments/DIGIT-DevOps)
   * [https://github.com/egovernments/CIOps](https://github.com/egovernments/CIOps)
3. [Go lang](https://golang.org/doc/install) (version 1.13.X)
4. [SOPS](https://github.com/mozilla/sops#updatekeys-command)
5. [GitHub user](https://docs.github.com/en/get-started/signing-up-for-github/signing-up-for-a-new-github-account)
6. [Docker Hub account](https://hub.docker.com/signup)
7. Install [**kubectl**](https://kubernetes.io/docs/tasks/tools/) on your local machine to interact with the Kubernetes cluster.
8. Install [**Helm**](https://helm.sh/docs/intro/install/) to help package the services along with the configurations, environment, secrets, etc into a [**Kubernetes manifests**](https://devspace.cloud/docs/cli/deployment/kubernetes-manifests/what-are-manifests)**.**

### Hardware <a href="#hardware" id="hardware"></a>

* One Bastion machine to run Kubespray.
* HA-PROXY machine which acts as a load balancer with Public IP. (CPU: 2Core , Memory: 4Gb)&#x20;
* one machine which acts as a master node. (CPU: 2Core , Memory: 4Gb)&#x20;
* one machine which acts as a worker node. (CPU: 8Core , Memory: 16Gb)
* ISCSI volumes for persistence volume. (number of quantity: 2 )
  * kaniko-cache-claim:- 10Gb
  * jenkins home:- 100Gb

### **Software**&#x20;

1. **Kubernetes nodes**
   1. Ubuntu 18.04
   2. SSH&#x20;
   3. Privileged user
   4. python
2. #### Bastion machine
   1. Ansible
   2. git
   3. pytho

## CI/CD Cluster Setup with kubespray



Kubespray is a composition of [Ansible](https://docs.ansible.com/) playbooks, [inventory](https://github.com/kubernetes-sigs/kubespray/blob/master/docs/ansible.md), provisioning tools, and domain knowledge for generic OS/Kubernetes clusters configuration management tasks. Kubespray provides:

* a highly available cluster
* composable attributes
* support for most popular Linux distributions
* continuous integration tests

## Preparing the nodes <a href="#preparing-the-nodes" id="preparing-the-nodes"></a>

Run follow instructions on all nodes.

### Install Python <a href="#install-python" id="install-python"></a>

Ansible needs python to be installed on all the machines**.**

`apt-get update && apt-get install python3-pip -y`

### Disable Swap <a href="#disable-swap" id="disable-swap"></a>

```
sudo swapoff -a
sudo sed -i '/ swap /d' /etc/fstab
```

### Setup SSH using key-based authentication

&#x20;**All the machines should be in the same network with ubuntu or centos installed.**

ssh key should be generated from the Bastion machine and must be copied to all the servers part of your inventory.

* Generate the ssh key `ssh-keygen -t rsa`
*   Copy over the public key to all nodes.

    ```shell
    ssh-copy-id root@<node-ip-address>
    ```

### Setup Ansible Controller machine Setup kubespray

* Clone the official repository

```
git clone https://github.com/kubernetes-incubator/kubespray.git
```

```
cd kubespray
```

* Install dependencies from `requirements.txt`

```
sudo pip install -r requirements.txt
```

* Create Inventory

```
cp -rfp inventory/sample inventory/mycluster
```

\
where mycluster is the custom configuration name. Replace with whatever name you would like to assign to the current cluster.

Create inventory using inventory generator.

```
declare -a IPS=(10.67.53.158 10.67.53.159 )
CONFIG_FILE=inventory/mycluster/hosts.yaml python3 contrib/inventory_builder/inventory.py ${IPS[@]}
```

Once it run, you can see an inventory file that looks like below:

```
all:
  hosts:
    node1:
      ansible_host: 10.67.53.158
      ip: 10.67.53.158
      access_ip: 10.67.53.158
    node2:
      ansible_host: 10.67.53.159
      ip: 10.67.53.159
      access_ip: 10.67.53.159  
  children:
    kube-master:
      hosts:
        node1:
    kube-node:
      hosts:
        node1:
        node2:
    etcd:
      hosts:
        node1:
    k8s-cluster:
      children:
        kube-master:
        kube-node:
    calico-rr:
      hosts: {}

```

* Review and change parameters under `inventory/mycluster/group_vars`

```
vim inventory/mycluster/group_vars/all/all.yml
...
## External LB example config
## apiserver_loadbalancer_domain_name: "elb.some.domain"
apiserver_loadbalancer_domain_name: "10.211.55.101"
loadbalancer_apiserver:
  address: 10.211.55.101
  port: 443
```

* Deploy Kubespray with Ansible Playbook - run the playbook as ubuntu
  * The option `--become` is required, as for example writing SSL keys in /etc/,
  * installing packages and interacting with various systemd daemons.
  * **Note**: Without --become the playbook will fail to run!

```
ansible-playbook -i inventory/mycluster/hosts.yaml  --become --become-user=ubuntu cluster.yml
```

Kubernetes cluster will be created with three masters and four nodes with the above process.

Kube config will be generated in a .Kubefolder. The Cluster can be accessible via kubeconfig.



## **HA-Proxy:**

* Install haproxy package in a haproxy machine that will be allocated for proxy

`sudo apt-get install haproxy -y`

* IPs need to be whitelisted as per the requirements in config.

`sudo vim /etc/haproxy/haproxy.cfg`

```
global
	log /dev/log	local0
	log /dev/log	local1 notice
	chroot /var/lib/haproxy
	stats socket /run/haproxy/admin.sock mode 660 level admin expose-fd listeners
	stats timeout 30s
	user haproxy
	group haproxy
	daemon

	# Default SSL material locations
       # ca-base /etc/ssl/certs
      #	crt-base /etc/ssl/private

	# Default ciphers to use on SSL-enabled listening sockets.
	# For more information, see ciphers(1SSL). This list is from:
	#  https://hynek.me/articles/hardening-your-web-servers-ssl-ciphers/
	# An alternative list with additional directives can be obtained from
	#  https://mozilla.github.io/server-side-tls/ssl-config-generator/?server=haproxy
	#ssl-default-bind-ciphers 
	#ssl-default-bind-options no-sslv3

defaults
	log	global
	mode	http
	option	httplog
	option	dontlognull
            timeout connect 5000
            timeout check   5000
            timeout client  30000
             timeout server  60000

frontend http-in
    bind *:80
    mode tcp
    default_backend http-servers
    http-request redirect scheme https unless { ssl_fc }

frontend https-in
    bind *:443
    mode tcp
    default_backend https-servers

frontend kube-in
    bind *:8383
    mode tcp
    timeout client 3h
    #Jenkins_CD eGov_ACT eGov_Spectra 
    #acl network_allowed src 35.244.58.192 106.51.69.20 180.151.198.122 103.122.14.159 35.154.77.83 35.154.203.141 125.16.100.118 10.67.53.252  52.71.194.45 132.154.83.214 27.6.189.204 10.67.53.120
    #tcp-request connection reject if !network_allowed
    default_backend kube-servers

frontend kube2-in
    bind *:6363
    mode tcp
    timeout client 3h
    #Jenkins_CD eGov_ACT eGov_Spectra
    acl network_allowed src 35.244.58.192 106.51.69.20 180.151.198.122 103.122.14.159 35.154.77.83 35.154.203.141 125.16.100.118 10.67.53.252  52.71.194.45 132.154.83.214 27.6.189.204 10.67.53.120
    tcp-request connection reject if !network_allowed
    default_backend kube-servers


backend http-servers
        mode tcp
        balance roundrobin
        server srv4 10.67.53.159:32080 send-proxy

backend https-servers
        mode tcp
        balance roundrobin
        server srv4 10.67.53.159:32443 send-proxy

backend kube-servers
        mode tcp     
        option log-health-checks
        timeout server 3h
        server master1 10.67.53.158:6443 check check-ssl verify none inter 10000
        balance roundrobin  
```

## **Volumes:**

Iscsi volumes will be provided by SDC team as per the requisition and the same can be used for statefulsets.

```
sudo iscsiadm -m discovery -t sendtargets -p 10.67.49.8:3260
```



### CI/CD Build Job Pipeline Setup

{% content-ref url="../../jenkins-setup/ci-cd-build-job-pipeline-setup.md" %}
[ci-cd-build-job-pipeline-setup.md](../../jenkins-setup/ci-cd-build-job-pipeline-setup.md)
{% endcontent-ref %}
