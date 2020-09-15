# Deploying Backbone Services

Once the cluster is ready and healthy you can start deploying backbones services.

            Deploy configuration and deployment in the following Services Lists

1.   Backbone \(Redis, ZooKeeper-v2, Kafka-v2,elasticsearch-data-v1, elasticsearch-client-v1, elasticsearch-master-v1\)
2.   Gateway \(Zuul, nginx-ingress-controller\)

### Prerequisites <a id="Prerequisites"></a>

* Understanding of VM Instances, LoadBalancers, SecurityGroups/Firewalls, nginx,   DB  Instance, Data Volumes.
* Experience of kubernetes, docker, jenkins, helm, golang, Infra-as-code.
* Install go tools \([https://golang.org/doc/install\#install](https://golang.org/doc/install#install)\)

 Deploy configuration and deployment backbone services:        

1. Clone the git repo[ ![](https://github.githubassets.com/favicon.ico)https://github.com/egovernments/eGov-infraOps](https://github.com/egovernments/eGov-infraOps) . Copy existing [dev.yaml](https://github.com/egovernments/eGov-infraOps/blob/master/helm/environments/dev.yaml) and [dev-secrets.yaml](https://github.com/egovernments/eGov-infraOps/blob/master/helm/environments/dev-secrets.yaml) with new environment name \(eg. &lt;new\_env&gt;.yaml and &lt;new\_env&gt;-secrets.yaml\) 
2.  Modify the global domain and set namespaces create to true

![](../.gitbook/assets/image%20%2811%29.png)

3.  Modify the below mentioned changes for each backbone services:

 Eg. For Kafka-v2 If you are using **AWS as cloud provider,** change the respective volume id’s and zone’s

 \(You will get the volume id’s and zone details from either remote state bucket or from AWS portal\)

![](../.gitbook/assets/image%20%2830%29.png)

Eg. Kafka-v2 If you are using **Azure cloud provider,** change the diskName and diskUri

 \(You will get the volume id’s and zone details from either remote state bucket or from Azure portal\)

![](../.gitbook/assets/image%20%2817%29.png)

 Eg. Kafka-v2 If you are using **ISCSI ,** change the targetPortal and iqn.  


![](../.gitbook/assets/image%20%2840%29.png)

4.  Deploy the backbone services using  go command

```text
cd /eGov-infraOps/egov-deployer
go run main.go deploy -e dev -p -c 'kafka-v2,redis,zookeeper-v2,elasticsearch-data-v1,elasticsearch-master-v1,playground,cert-manager,kafka-connect,kafka-connect-restart-tasks,kibana-v1,nginx-ingress'
```

Modify the “dev” environment name with your respective environment name.

**Flags**:

* e  --- Environment name
* p  --- Print the manifest 
* c  --- Enable Cluster Configs

5. Check the Status of pods

```text
kubectl get pods --all-namespaces
```



