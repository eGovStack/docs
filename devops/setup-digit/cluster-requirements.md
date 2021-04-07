# Infra Requirements

### Overview

This page discusses the infrastructure requirements for DIGIT services. It also explains why DIGIT services are containerised and deployed on Kubernetes.

### Requirements

DIGIT Infra is abstracted to **Kubernetes** which is an open-source containers orchestration platform that helps in abstracting variety of infra types that are being available across each state, like Physical, VMs, on-premises clouds\(**VMware, OpenStack, Nutanix**, etc.\), commercial clouds \(**Google, AWS, Azure, etc**.\), SDC and NIC into a standard infra type. Essentially it unifies various infra types into a standard and single type of infrastructure and thus DIGIT becomes **multi-cloud supported, portable, extensible, high-performant and scalable** containerized workloads and services. This facilitates both declarative configuration and automation. Kubernetes services, eco-system, support and tools are widely available.

### The basic need to provision Kubernetes Cluster

Kubernetes as such is a set of components that designated jobs of scheduling, controlling, monitoring 

#### Master Cluster <a id="master-cluster"></a>

* 3 or more machines running one of:
  * Ubuntu 16.04+
  * Debian 9
  * CentOS 7
  * RHEL 7
  * Container Linux \(tested with 1576.4.0\)
* 4 GB or more of RAM per machine \(any less will leave little room for your apps\)
* 2 CPUs or more

#### User Cluster <a id="user-cluster"></a>

* 3 or more machines running one of:
  * Ubuntu 16.04+
  * Debian 9
  * CentOS 7
  * RHEL 7
  * Container Linux \(tested with 1576.4.0\)
* 2 GB or more of RAM per machine \(any less will leave little room for your apps\)
* 2 CPUs or more
* Full network connectivity between all machines in the cluster \(public or private network is fine\)
* Unique hostname, MAC address, and product\_uuid for every node. Click [here](cluster-requirements.md#verify-the-mac-address-and-product-uuid-are-unique-for-every-node) for more details.
* Certain ports are open on your machines. See below for more details
* Swap disabled. You **MUST** disable swap in order for the Kubelet to work properly

#### Verify the MAC Address and `product_uuid` Are Unique for Every Node <a id="verify-the-mac-address-and-product_uuid-are-unique-for-every-node"></a>

* You can get the MAC address of the network interfaces using the command `ip link` or `ifconfig -a`
* The product\_uuid can be checked by using the command `sudo cat /sys/class/dmi/id/product_uuid`

It is very likely that hardware devices will have unique addresses, although some virtual machines may have identical values. Kubernetes uses these values to uniquely identify the nodes in the cluster. If these values are not unique to each node, the installation process may [fail](https://github.com/kubernetes/kubeadm/issues/31).

### Check Network Adapters

If you have more than one network adapter, and your Kubernetes components are not reachable on the default route, we recommend you add IP route\(s\) so Kubernetes cluster addresses go via the appropriate adapter.

#### Check Required Ports <a id="check-required-ports"></a>

### **Master Cluster Master Node\(s\)**

| Protocol | Direction | Port Range | Purpose |
| :--- | :--- | :--- | :--- |
| TCP | Inbound | 6443\* | Kubernetes API server |
| TCP | Inbound | 2379-2380 | etcd server client API |
| TCP | Inbound | 10250 | kubelet API |
| TCP | Inbound | 10251 | kube-scheduler |
| TCP | Inbound | 10252 | kube-controller-manager |
| TCP | Inbound | 10255 | Read-only kubelet API |

### **Worker Node\(s\)& User Cluster Worker Nodes**

| Protocol | Direction | Port Range | Purpose |
| :--- | :--- | :--- | :--- |
| TCP | Inbound | 10250 | kubelet API |
| TCP | Inbound | 10255 | Read-only kubelet API |
| TCP | Inbound | 30000-32767 | NodePort Services\*\* |

\*\* Default port range for [NodePort Services](https://kubernetes.io/docs/concepts/services-networking/service/).

Any port numbers marked with \* are overridable, so you will need to ensure any custom ports you provide are also open.



### **Complete Infra Specifications:**

<table>
  <thead>
    <tr>
      <th style="text-align:left"><b>Systems</b>
      </th>
      <th style="text-align:left"><b>Specification</b>
      </th>
      <th style="text-align:left"><b>Spec/Count</b>
      </th>
      <th style="text-align:left"><b>Comment</b>
      </th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><b>User Accounts/VPN</b>
      </td>
      <td style="text-align:left"><b>Dev, UAT and Prod Envs</b>
      </td>
      <td style="text-align:left"><b>3</b>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>User Roles</b>
      </td>
      <td style="text-align:left"><b>Admin, Deploy, ReadOnly</b>
      </td>
      <td style="text-align:left"><b>3</b>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>OS</b>
      </td>
      <td style="text-align:left"><b>Any Linux (preferably Ubuntu/RHEL)</b>
      </td>
      <td style="text-align:left"><b>All</b>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Kubernetes as a managed service or VMs to provision Kubernetes</b>
      </td>
      <td style="text-align:left">
        <p><b>Managed Kubernetes service with HA/DRS</b>
        </p>
        <p><b>(Or) VMs with 2 vCore, 4 GB RAM, 20 GB Disk</b>
        </p>
      </td>
      <td style="text-align:left">
        <p><b>If no managed k8s</b>
        </p>
        <p><b>3 VMs/env</b>
        </p>
      </td>
      <td style="text-align:left">
        <p><b>Dev - 3 VMs</b>
        </p>
        <p><b>UAT - 3VMs</b>
        </p>
        <p><b>Prod - 3VMs<br /></b>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Kubernetes worker nodes or VMs to provision Kube worker nodes.</b>
      </td>
      <td style="text-align:left"><b>VMs with 4 vCore, 16 GB RAM, 20 GB Disk / per env</b>
      </td>
      <td style="text-align:left"><b>3-5 VMs/env </b>
      </td>
      <td style="text-align:left">
        <p><b>DEV - 3VMs</b>
        </p>
        <p><b>UAT - 4VMs</b>
        </p>
        <p><b>PROD - 5VMs</b>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Storage (NFS/iSCSI) </b>
      </td>
      <td style="text-align:left"><b>Storage with backup, snapshot, dynamic inc/dec</b>
      </td>
      <td style="text-align:left"><b>1 TB/env</b>
      </td>
      <td style="text-align:left">
        <p><b>Dev - 1000 GB</b>
        </p>
        <p><b>UAT - 800 GB</b>
        </p>
        <p><b>PROD - 1.5 TB</b>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>VM Instance IOPS</b>
      </td>
      <td style="text-align:left"><b>Max throughput 1750 MB/s</b>
      </td>
      <td style="text-align:left"><b>1750 MS/s</b>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Storage IOPS</b>
      </td>
      <td style="text-align:left"><b>Max throughput 1000 MB/s</b>
      </td>
      <td style="text-align:left"><b>1000 MB/s</b>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Internet Speed</b>
      </td>
      <td style="text-align:left"><b>Min 100 MB - 1000MB/Sec (dedicated bandwidth)</b>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Public IP/NAT or LB</b>
      </td>
      <td style="text-align:left"><b>Internet-facing 1 public ip per env</b>
      </td>
      <td style="text-align:left"><b>3</b>
      </td>
      <td style="text-align:left"><b>3 Ips</b>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Availability Region</b>
      </td>
      <td style="text-align:left"><b>VMs from the different region is preferable for the DRS/HA</b>
      </td>
      <td style="text-align:left"><b>at least 2 Regions</b>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Private vLan</b>
      </td>
      <td style="text-align:left"><b>Per env all VMs should within private vLan</b>
      </td>
      <td style="text-align:left"><b>3</b>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Gateways</b>
      </td>
      <td style="text-align:left"><b>NAT Gateway, Internet Gateway, Payment and SMS gateway,etc</b>
      </td>
      <td style="text-align:left"><b>1 per env</b>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Firewall</b>
      </td>
      <td style="text-align:left"><b>Ability to configure Inbound, Outbound ports/rules </b>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p><b>Managed DataBase </b>
        </p>
        <p><b>(or) VM Instance</b>
        </p>
      </td>
      <td style="text-align:left">
        <p><b>Postgres 12 above Managed DB with backup, snapshot, logging. </b>
        </p>
        <p><b>(Or) 1 VM with 4 vCore, 16 GB RAM, 100 GB Disk per env.</b>
        </p>
      </td>
      <td style="text-align:left"><b>per env</b>
      </td>
      <td style="text-align:left">
        <p><b>DEV - 1VMs</b>
        </p>
        <p><b>UAT - 1VMs</b>
        </p>
        <p><b>PROD - 2VMs</b>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>CI/CD server self hosted (or) Managed DevOps</b>
      </td>
      <td style="text-align:left">
        <p><b>Self Hosted Jenkins : Master, Slave (VM 4vCore, 8 GB each) </b>
        </p>
        <p><b>(Or) Managed CI/CD:  NIC DevOps or AWS  CodeDeploy or Azure DevOps </b>
        </p>
      </td>
      <td style="text-align:left"><b>2 VMs (Master, Slave)</b>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Nexus Repo</b>
      </td>
      <td style="text-align:left"><b>Self hosted Artifactory Repo (Or) NIC Nexus Artifactory</b>
      </td>
      <td style="text-align:left"><b>1</b>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>DockerRegistry</b>
      </td>
      <td style="text-align:left"><b>DockerHub (Or) SelfHosted private docker reg</b>
      </td>
      <td style="text-align:left"><b>1</b>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Git/SCM</b>
      </td>
      <td style="text-align:left"><b>GitHub (Or) Any Source Control tool</b>
      </td>
      <td style="text-align:left"><b>1</b>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>DNS </b>
      </td>
      <td style="text-align:left"><b>main domain &amp; ability to add more sub-domain</b>
      </td>
      <td style="text-align:left"><b>1</b>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>SSL Certificate</b>
      </td>
      <td style="text-align:left"><b>NIC managed (Or) SDC managed SSL certificate per URL</b>
      </td>
      <td style="text-align:left"><b>2 urls per env</b>
      </td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>

