# Monitoring & Alerting Setup for cluster

[Prometheus](https://github.com/prometheus) is an open-source systems monitoring and alerting toolkit originally built at [SoundCloud](https://soundcloud.com/)  


![](../.gitbook/assets/image%20%2837%29.png)



[prometheus-operator](https://github.com/egovernments/eGov-infraOps/tree/master/helm/charts/backbone-services/prometheus-operator) chart includes multiple components and is suitable for a variety of use-cases.

The default installation is intended to suit monitoring a kubernetes cluster the chart is deployed onto. It closely matches the kube-prometheus project.

* [prometheus-operator](https://github.com/coreos/prometheus-operator)
* [prometheus](https://prometheus.io/)
* [alertmanager](https://prometheus.io/)
* [node-exporter](https://github.com/helm/charts/tree/master/stable/prometheus-node-exporter)
* [kube-state-metrics](https://github.com/helm/charts/tree/master/stable/kube-state-metrics)
* [grafana](https://github.com/helm/charts/tree/master/stable/grafana)
* service monitors to scrape internal kubernetes components
  * kube-apiserver
  * kube-scheduler
  * kube-controller-manager
  * etcd
  * kube-dns/coredns
  * kube-proxy

With the installation, the chart also includes dashboards and alerts.

**Deployment steps:**

1.  Add environment variable to the respective env config file

![](../.gitbook/assets/image%20%2831%29.png)

       Update the configs branch \(like for qa.yaml added qa branch\)

     2.   Add [monitoring-dashboards](https://github.com/egovernments/configs/tree/master/monitoring-dashboards) folder to respective configs branch.

     3. Enable the nginx-ingress monitoring and redeploy the nginx-ingress.      

![](../.gitbook/assets/image%20%2838%29.png)

4. Add alertmanager secret in respective &lt;env&gt;.secrets.yaml

 If you want you can change the slack channel and other details like group\_wait ,    group\_interval and repeat\_interval according to your values.

![](../.gitbook/assets/image%20%2833%29.png)



5. Deploy the prometheus-operator using go cmd or deploy using Jenkins.

```text
go run main.go deploy -e  <environment_name> -c 'prometheus-operator,grafana,prometheues-kafka-exporter'
```

**To create a new panel in the existing dashboard:-**  

1.  Login to dashboard and click on add panel  

![](../.gitbook/assets/image%20%2839%29.png)

    2. Set all required queries and apply the changes. Export the JSON file by clicking on t    the save dashboard

![](../.gitbook/assets/image%20%2819%29.png)

3. Update the existing \*-dashboard.json file from configs monitoring-dashboards folder with a newly exported JSON file.



