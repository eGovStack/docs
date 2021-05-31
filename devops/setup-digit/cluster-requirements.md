# Infra Requirements

## Overview

This page discusses the infrastructure requirements for DIGIT services. It also explains why DIGIT services are containerised and deployed on Kubernetes.

## Requirements

DIGIT Infra is abstracted to **Kubernetes** which is an open-source containers orchestration platform that helps in abstracting a variety of infra types that are being available across each state, like Physical, VMs, on-premises clouds\(**VMware, OpenStack, Nutanix**, etc.\), commercial clouds \(**Google, AWS, Azure, etc**.\), SDC and NIC into a standard infra type. Essentially it unifies various infra types into a standard and single type of infrastructure and thus DIGIT becomes **multi-cloud supported, portable, extensible, high-performant and scalable** containerized workloads and services. This facilitates both declarative configuration and automation. Kubernetes services, eco-system, support and tools are widely available.

## The basic need to provision Kubernetes Cluster

Kubernetes as such is a set of components that designated jobs of scheduling, controlling, monitoring

### Master Cluster <a id="master-cluster"></a>

* 3 or more machines running one of:
  * Ubuntu 16.04+
  * Debian 9
  * CentOS 7
  * RHEL 7
  * Container Linux \(tested with 1576.4.0\)
* 4 GB or more of RAM per machine \(any less will leave little room for your apps\)
* 2 CPUs or more

### User Cluster <a id="user-cluster"></a>

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

### Verify the MAC Address and `product_uuid` Are Unique for Every Node <a id="verify-the-mac-address-and-product_uuid-are-unique-for-every-node"></a>

* You can get the MAC address of the network interfaces using the command `ip link` or `ifconfig -a`
* The product\_uuid can be checked by using the command `sudo cat /sys/class/dmi/id/product_uuid`

It is very likely that hardware devices will have unique addresses, although some virtual machines may have identical values. Kubernetes uses these values to uniquely identify the nodes in the cluster. If these values are not unique to each node, the installation process may [fail](https://github.com/kubernetes/kubeadm/issues/31).

## Check Network Adapters

If you have more than one network adapter, and your Kubernetes components are not reachable on the default route, we recommend you add IP route\(s\) so Kubernetes cluster addresses go via the appropriate adapter.

### Check Required Ports <a id="check-required-ports"></a>

## **Master Cluster Master Node\(s\)**

| Protocol | Direction | Port Range | Purpose |
| :--- | :--- | :--- | :--- |
| TCP | Inbound | 6443\* | Kubernetes API server |
| TCP | Inbound | 2379-2380 | etcd server client API |
| TCP | Inbound | 10250 | kubelet API |
| TCP | Inbound | 10251 | kube-scheduler |
| TCP | Inbound | 10252 | kube-controller-manager |
| TCP | Inbound | 10255 | Read-only kubelet API |

## **Worker Node\(s\)& User Cluster Worker Nodes**

| Protocol | Direction | Port Range | Purpose |
| :--- | :--- | :--- | :--- |
| TCP | Inbound | 10250 | kubelet API |
| TCP | Inbound | 10255 | Read-only kubelet API |
| TCP | Inbound | 30000-32767 | NodePort Services\*\* |

\*\* Default port range for [NodePort Services](https://kubernetes.io/docs/concepts/services-networking/service/).

Any port numbers marked with \* are overridable, so you will need to ensure any custom ports you provide are also open.

## **Complete Infra Specifications**

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
      <td style="text-align:left">User Accounts/VPN</td>
      <td style="text-align:left">Dev, UAT and Prod Envs</td>
      <td style="text-align:left">3</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">User Roles</td>
      <td style="text-align:left">Admin, Deploy, ReadOnly</td>
      <td style="text-align:left">3</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">OS</td>
      <td style="text-align:left">Any Linux (preferably Ubuntu/RHEL)</td>
      <td style="text-align:left">All</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Kubernetes as a managed service or on-prem VMs to provision Kubernetes</td>
      <td
      style="text-align:left">
        <p>Managed Kubernetes service with HA/DRS</p>
        <p>(Or) VMs with 2 vCore, 4 GB RAM, 20 GB Disk</p>
        </td>
        <td style="text-align:left">
          <p>If no managed k8s</p>
          <p>3 VMs/env</p>
        </td>
        <td style="text-align:left">
          <p>Dev - 3 VMs</p>
          <p>UAT - 3VMs</p>
          <p>Prod - 3VMs
            <br />
          </p>
        </td>
    </tr>
    <tr>
      <td style="text-align:left">Kubernetes worker nodes or VMs to provision Kube worker nodes.</td>
      <td
      style="text-align:left">VMs with 4 vCore, 16 GB RAM, 20 GB Disk / per env</td>
        <td style="text-align:left">3-5 VMs/env</td>
        <td style="text-align:left">
          <p>DEV - 3VMs</p>
          <p>UAT - 4VMs</p>
          <p>PROD - 5VMs</p>
        </td>
    </tr>
    <tr>
      <td style="text-align:left">Storage (NFS/iSCSI)</td>
      <td style="text-align:left">Storage with backup, snapshot, dynamic inc/dec</td>
      <td style="text-align:left">1 TB/env</td>
      <td style="text-align:left">
        <p>Dev - 1000 GB</p>
        <p>UAT - 800 GB</p>
        <p>PROD - 1.5 TB</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">VM Instance IOPS</td>
      <td style="text-align:left">Max throughput 1750 MB/s</td>
      <td style="text-align:left">1750 MS/s</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Storage IOPS</td>
      <td style="text-align:left">Max throughput 1000 MB/s</td>
      <td style="text-align:left">1000 MB/s</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Internet Speed</td>
      <td style="text-align:left">Min 100 MB - 1000MB/Sec (dedicated bandwidth)</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Public IP/NAT or LB</td>
      <td style="text-align:left">Internet-facing 1 public ip per env</td>
      <td style="text-align:left">3</td>
      <td style="text-align:left">3 Ips</td>
    </tr>
    <tr>
      <td style="text-align:left">Availability Region</td>
      <td style="text-align:left">VMs from the different region is preferable for the DRS/HA</td>
      <td style="text-align:left">at least 2 Regions</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Private vLan</td>
      <td style="text-align:left">Per env all VMs should within private vLan</td>
      <td style="text-align:left">3</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Gateways</td>
      <td style="text-align:left">NAT Gateway, Internet Gateway, Payment and SMS gateway, etc</td>
      <td style="text-align:left">1 per env</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Firewall</td>
      <td style="text-align:left">Ability to configure Inbound, Outbound ports/rules</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>Managed DataBase</p>
        <p>(or) VM Instance</p>
      </td>
      <td style="text-align:left">
        <p>Postgres 12 above Managed DB with backup, snapshot, logging.</p>
        <p>(Or) 1 VM with 4 vCore, 16 GB RAM, 100 GB Disk per env.</p>
      </td>
      <td style="text-align:left">per env</td>
      <td style="text-align:left">
        <p>DEV - 1VMs</p>
        <p>UAT - 1VMs</p>
        <p>PROD - 2VMs</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">CI/CD server self-hosted (or) Managed DevOps</td>
      <td style="text-align:left">
        <p>Self Hosted Jenkins: Master, Slave (VM 4vCore, 8 GB each)</p>
        <p>(Or) Managed CI/CD: NIC DevOps or AWS CodeDeploy or Azure DevOps</p>
      </td>
      <td style="text-align:left">2 VMs (Master, Slave)</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Nexus Repo</td>
      <td style="text-align:left">Self-hosted Artifactory Repo (Or) NIC Nexus Artifactory</td>
      <td style="text-align:left">1</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">DockerRegistry</td>
      <td style="text-align:left">DockerHub (Or) SelfHosted private docker reg</td>
      <td style="text-align:left">1</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Git/SCM</td>
      <td style="text-align:left">GitHub (Or) Any Source Control tool</td>
      <td style="text-align:left">1</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">DNS</td>
      <td style="text-align:left">main domain &amp; ability to add more sub-domain</td>
      <td style="text-align:left">1</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">SSL Certificate</td>
      <td style="text-align:left">NIC managed (Or) SDC managed SSL certificate per URL</td>
      <td style="text-align:left">2 URLs per env</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">SMS Gateway</td>
      <td style="text-align:left">Transactional SMS/OTP</td>
      <td style="text-align:left">per env</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">GMap Key</td>
      <td style="text-align:left">For Location API, GeoCode API</td>
      <td style="text-align:left">Per Tenant</td>
      <td style="text-align:left">for users to select address from the map</td>
    </tr>
  </tbody>
</table>

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)​](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation](https://egov.org.in/) is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).

