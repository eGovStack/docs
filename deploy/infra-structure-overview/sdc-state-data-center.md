# Provision k8s Cluster \(SDC\)

**Pre requisites:** 

Below Servers are to be provided by the SDC team.

One Bastion machine to run Kubespray.

1. HA-PROXY machine which acts as load balancer.
2. Three machines which act as master nodes.
3. Four machines which act as worker nodes.
4. One machine for database configuration.

  
All the machines should be in the same network with ubuntu or centos installed.

**Key Generation:**

ssh key should be generated form Bastion machine and  must be copied to all the servers part of your inventory.

Generate ssh-keygen

\#Copy the key to all the nodes

```text
ssh-copy-id root@IP of node
```

**Kubespray:**

Install git

```text
git clone https://github.com/kubernetes-sigs/kubespray.git 
```

install python

```text
apt-get update && apt-get install python3-pip -y
cd kubespray 
```

\# Install dependencies from \`\`requirements.txt\`\`

```text
sudo pip3 install -r requirements.txt
```

\# Copy \`\`inventory/sample\`\` as \`\`inventory/mycluster\`\`

```text
cp -rfp inventory/sample inventory/mycluster
```

\# Update Ansible inventory file with inventory builder

declare -a IPS=\(10.67.53.158 10.67.53.159 10.67.53.160 10.67.53.161 10.67.53.162 10.67.53.163 10.67.53.164\)

CONFIG\_FILE=inventory/mycluster/hosts.yaml python3 contrib/inventory\_builder/inventory.py ${IPS\[@\]}

\# Review and change parameters under \`\`inventory/mycluster/group\_vars\`\`

```text
cat inventory/mycluster/group_vars/all/all.yml
cat inventory/mycluster/group_vars/k8s-cluster/k8s-cluster.yml
```

\# Deploy Kubespray with Ansible Playbook - run the playbook as root

\# The option \`--become\` is required, as for example writing SSL keys in /etc/,

\# installing packages and interacting with various systemd daemons.

\# Without --become the playbook will fail to run!

ansible-playbook -i inventory/mycluster/hosts.yaml  --become --become-user=root cluster.yml

Kubernetes cluster will be created with three masters and four nodes with the above process.

Kube config will be generated in .Kubefolder. Cluster can be accessible via kubeconfig.

**HA-Proxy:**

Install haproxy for the machine that was allocated for proxy

```text
sudo apt-get install haproxy -y
```

IPs need to be whitelisted as per the requirements in config.

```text
sudo vi /etc/haproxy/haproxy.cfg
```

**Volumes:**

Iscsi volumes will be provided by SDC team as per the requisition and the same can be used for statefulsets.

```text
sudo iscsiadm -m discovery -t sendtargets -p 10.67.49.8:3260
```



