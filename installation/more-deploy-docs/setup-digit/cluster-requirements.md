# Infra Requirements

### Overview

This page discusses the infrastructure requirements for DIGIT services. It also explains why DIGIT services are containerised and deployed on Kubernetes.

### Requirements

DIGIT Infra is abstracted to **Kubernetes** which is an open-source containers orchestration platform that helps in abstracting a variety of infra types that are being available across each state, like Physical, VMs, on-premises clouds(**VMware, OpenStack, Nutanix**, etc.), commercial clouds (**Google, AWS, Azure, etc**.), SDC and NIC into a standard infra type. Essentially it unifies various infra types into a standard and single type of infrastructure and thus DIGIT becomes **multi-cloud supported, portable, extensible, high-performant and scalable** containerized workloads and services. This facilitates both declarative configuration and automation. Kubernetes services, eco-system, support and tools are widely available.

### The basic need to provision Kubernetes Cluster

Kubernetes as such is a set of components that designated jobs of scheduling, controlling, monitoring

#### Master Cluster <a href="#master-cluster" id="master-cluster"></a>

* 3 or more machines running one of:
  * Ubuntu 16.04+
  * Debian 9
  * CentOS 7
  * RHEL 7
  * Container Linux (tested with 1576.4.0)
* 4 GB or more of RAM per machine (any less will leave little room for your apps)
* 2 CPUs or more

#### User Cluster <a href="#user-cluster" id="user-cluster"></a>

* 3 or more machines running one of:
  * Ubuntu 16.04+
  * Debian 9
  * CentOS 7
  * RHEL 7
  * Container Linux (tested with 1576.4.0)
* 2 GB or more of RAM per machine (any less will leave little room for your apps)
* 2 CPUs or more
* Full network connectivity between all machines in the cluster (public or private network is fine)
* Unique hostname, MAC address, and product\_uuid for every node. Click [here](cluster-requirements.md#verify-the-mac-address-and-product-uuid-are-unique-for-every-node) for more details.
* Certain ports are open on your machines. See below for more details
* Swap disabled. You **MUST** disable swap in order for the Kubelet to work properly

#### Verify the MAC Address and `product_uuid` Are Unique for Every Node <a href="#verify-the-mac-address-and-product_uuid-are-unique-for-every-node" id="verify-the-mac-address-and-product_uuid-are-unique-for-every-node"></a>

* You can get the MAC address of the network interfaces using the command `ip link` or `ifconfig -a`
* The product\_uuid can be checked by using the command `sudo cat /sys/class/dmi/id/product_uuid`

It is very likely that hardware devices will have unique addresses, although some virtual machines may have identical values. Kubernetes uses these values to uniquely identify the nodes in the cluster. If these values are not unique to each node, the installation process may [fail](https://github.com/kubernetes/kubeadm/issues/31).

### Check Network Adapters

If you have more than one network adapter, and your Kubernetes components are not reachable on the default route, we recommend you add IP route(s) so Kubernetes cluster addresses go via the appropriate adapter.

#### Check Required Ports <a href="#check-required-ports" id="check-required-ports"></a>

### **Master Cluster Master Node(s)**

| Protocol | Direction | Port Range | Purpose                 |
| -------- | --------- | ---------- | ----------------------- |
| TCP      | Inbound   | 6443\*     | Kubernetes API server   |
| TCP      | Inbound   | 2379-2380  | etcd server client API  |
| TCP      | Inbound   | 10250      | kubelet API             |
| TCP      | Inbound   | 10251      | kube-scheduler          |
| TCP      | Inbound   | 10252      | kube-controller-manager |
| TCP      | Inbound   | 10255      | Read-only kubelet API   |

### **Worker Node(s)& User Cluster Worker Nodes**

| Protocol | Direction | Port Range  | Purpose               |
| -------- | --------- | ----------- | --------------------- |
| TCP      | Inbound   | 10250       | kubelet API           |
| TCP      | Inbound   | 10255       | Read-only kubelet API |
| TCP      | Inbound   | 30000-32767 | NodePort Services\*\* |

\*\* Default port range for [NodePort Services](https://kubernetes.io/docs/concepts/services-networking/service/).

Any port numbers marked with \* are overridable, so you will need to ensure any custom ports you provide are also open.

### **Complete Infra Specifications**

|                                                                |                                                                                                                                         |                                          |                                                             |
| -------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------- | ----------------------------------------------------------- |
| **Systems**                                                    | **Specification**                                                                                                                       | **Spec/Count**                           | **Comment**                                                 |
| User Accounts/VPN                                              | Dev, UAT and Prod Envs                                                                                                                  | 3                                        |                                                             |
| User Roles                                                     | Admin, Deploy, ReadOnly                                                                                                                 | 3                                        |                                                             |
| OS                                                             | Any Linux (preferably Ubuntu/RHEL)                                                                                                      | All                                      |                                                             |
| Kubernetes as a managed service or VMs to provision Kubernetes | <p>Managed Kubernetes service with HA/DRS</p><p>(Or) VMs with 2 vCore, 4 GB RAM, 20 GB Disk</p>                                         | <p>If no managed k8s</p><p>3 VMs/env</p> | <p>Dev - 3 VMs</p><p>UAT - 3VMs</p><p>Prod - 3VMs<br></p>   |
| Kubernetes worker nodes or VMs to provision Kube worker nodes. | VMs with 4 vCore, 16 GB RAM, 20 GB Disk / per env                                                                                       | 3-5 VMs/env                              | <p>DEV - 3VMs</p><p>UAT - 4VMs</p><p>PROD - 5VMs</p>        |
| Storage (NFS/iSCSI)                                            | Storage with backup, snapshot, dynamic inc/dec                                                                                          | 1 TB/env                                 | <p>Dev - 1000 GB</p><p>UAT - 800 GB</p><p>PROD - 1.5 TB</p> |
| VM Instance IOPS                                               | Max throughput 1750 MB/s                                                                                                                | 1750 MS/s                                |                                                             |
| Storage IOPS                                                   | Max throughput 1000 MB/s                                                                                                                | 1000 MB/s                                |                                                             |
| Internet Speed                                                 | Min 100 MB - 1000MB/Sec (dedicated bandwidth)                                                                                           |                                          |                                                             |
| Public IP/NAT or LB                                            | Internet-facing 1 public ip per env                                                                                                     | 3                                        | 3 Ips                                                       |
| Availability Region                                            | VMs from the different region is preferable for the DRS/HA                                                                              | at least 2 Regions                       |                                                             |
| Private vLan                                                   | Per env all VMs should within private vLan                                                                                              | 3                                        |                                                             |
| Gateways                                                       | NAT Gateway, Internet Gateway, Payment and SMS gateway, etc                                                                             | 1 per env                                |                                                             |
| Firewall                                                       | Ability to configure Inbound, Outbound ports/rules                                                                                      |                                          |                                                             |
| <p>Managed DataBase</p><p>(or) VM Instance</p>                 | <p>Postgres 12 above Managed DB with backup, snapshot, logging.</p><p>(Or) 1 VM with 4 vCore, 16 GB RAM, 100 GB Disk per env.</p>       | per env                                  | <p>DEV - 1VMs</p><p>UAT - 1VMs</p><p>PROD - 2VMs</p>        |
| CI/CD server self-hosted (or) Managed DevOps                   | <p>Self Hosted Jenkins: Master, Slave (VM 4vCore, 8 GB each)</p><p>(Or) Managed CI/CD: NIC DevOps or AWS CodeDeploy or Azure DevOps</p> | 2 VMs (Master, Slave)                    |                                                             |
| Nexus Repo                                                     | Self-hosted Artifactory Repo (Or) NIC Nexus Artifactory                                                                                 | 1                                        |                                                             |
| DockerRegistry                                                 | DockerHub (Or) SelfHosted private docker reg                                                                                            | 1                                        |                                                             |
| Git/SCM                                                        | GitHub (Or) Any Source Control tool                                                                                                     | 1                                        |                                                             |
| DNS                                                            | main domain & ability to add more sub-domain                                                                                            | 1                                        |                                                             |
| SSL Certificate                                                | NIC managed (Or) SDC managed SSL certificate per URL                                                                                    | 2 URLs per env                           |                                                             |

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)​](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation](https://egov.org.in/) is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).
