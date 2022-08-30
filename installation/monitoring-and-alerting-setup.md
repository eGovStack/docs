---
description: >-
  This doc will cover how you can set up the monitoring and alerting on existing
  k8s cluster either with help of go lang script or Jenkins deployment Jobs.
---

# Monitoring & Alerting Setup

## Pre-requisites:

* [Oauth2-proxy](https://oauth2-proxy.github.io/oauth2-proxy/)(provides authentication using Providers (Google, GitHub, and others) to validate accounts by email, domain or group.)
* [Oauth-App](https://docs.github.com/en/developers/apps/building-oauth-apps/creating-an-oauth-app)
* Install [**kubectl**](https://kubernetes.io/docs/tasks/tools/) on your local machine to interact with the Kubernetes cluster.
* Install [**Helm**](https://helm.sh/docs/intro/install/) to help package the services along with the configurations, environment, secrets, etc into a [**Kubernetes manifests**](https://devspace.cloud/docs/cli/deployment/kubernetes-manifests/what-are-manifests)**.**
* [Go lang](https://golang.org/doc/install) (version 1.13.X)



[Prometheus](https://github.com/prometheus) is an open-source system monitoring and alerting toolkit originally built at [SoundCloud](https://soundcloud.com/)

![Architecture ](<../.gitbook/assets/image (41).png>)

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

**Oauth2-proxy Deployment steps:**

1.  Add Oauth2-proxy config in your \<env>.yaml

    ```
    oauth2-proxy:
      config:
        configFile: |-
          email_domains = [ "*" ]
          github_org = "<github_organization_name>" #REPLACE it with your GitHub organization name
          github_team = "<github_team_1>,<github_team_2>" #REPLACE it with GitHub team, Member of this teams would have the access on monitoring/tracing/kibana 
          upstreams = [ "file:///dev/null" ]
    ```
2. Generate and Add Oauth2-proxy secrets in your \<env>-secrets.yaml
   1. Generate [Oauth-App](https://docs.github.com/en/developers/apps/building-oauth-apps/creating-an-oauth-app) in your GitHub organization.
      1. Under `Authorization callback URL` enter the correct url ie `https://<domain_name>/oauth2/callback`
   2.  &#x20;Add below Oauth2-proxy secrets in your \<env>-secrets.yaml. You can generate any randome values for cookieSecret.&#x20;

       ```
       oauth2-proxy:
                   clientID: <clientID> #REPLACE with Oauth app client id
                   clientSecret: <clientSecret>  #REPLACE with Oauth app client secret
                   cookieSecret: c2RqU2RXeThwa1dXdC0FBR2t5aTRGWW1VeGVnbis=
       ```

3\. Deploy Oauth2-proxy using Go lang

&#x20;   `go run main.go deploy -e <environment_name> -c "oauth2-proxy"`



**Monitoring and alerting Deployment steps:**

1. Add the below grafana init container parameters to your [env config file](https://github.com/egovernments/DIGIT-DevOps/tree/master/deploy-as-code/helm/environments)
   1. Chose your env config file, if you are deploying **monitoring and alerting** into the qa environment chose qa.yaml similarly for uat, dev, and other environments.

<pre><code>grafana:
  initContainers:
    gitSync:
      enabled: true
      repo: "git@github.com:egovernments/configs" #REPLACE with your configs repo
<strong>      branch: "&#x3C;branch_name>" #REPLACE with config repo branch name
</strong>  dashboardsFolder: /work-dir/configs/monitoring-dashboards    </code></pre>

Depending upon your environment config file update the configs repo branch (like for qa.yaml add qa branch and uat.yaml it would be UAT the branch)

2\. Verify the [monitoring-dashboards](https://github.com/egovernments/configs/tree/master/monitoring-dashboards) folder is available to your configs repo's branch which you have selected in 1st step.

3\. Enable the serviceMonitor in the nginx-ingress configs which are available in the same \<env>.yaml and redeploy the nginx-ingress.

```
nginx-ingress:
  replicas: 1
  default-backend-service: "egov/nginx"
  namespace: egov
  cert-issuer: "letsencrypt-prod"
  ssl-protocols: "TLSv1.2 TLSv1.3"
  ssl-ciphers: "EECDH+CHACHA20:EECDH+AES"
  ssl-ecdh-curve: "X25519:prime256v1:secp521r1:secp384r1"
  controller:
    image:
      repository: egovio/nginx-ingress-controller
      tag: "0.26.1"     
    metrics:            #To collect the matrics data from nginx-ingress.
      enabled: true
      serviceMonitor:   #To enable the service monitoring of nginx-ingress
        enabled: true
    service:
      prometheusRule:
        enabled: true
```

4\. To enable alerting, Add alertmanager secret in \<env>-secrets.yaml

If you want you can change the slack channel and other details like group\_wait, group\_interval, and repeat\_interval according to your values.

```
alertmanager:
    config:
        global:
            resolve_timeout: 5m
        route:
            receiver: slack-notifications
            group_by:
                - alertname
            routes:
                - receiver: slack-notifications
                  match:
                    alertname: Watchdog
            group_wait: 30s
            group_interval: 4h
            repeat_interval: 12h
        receivers:
            - name: slack-notifications
              slack_configs:
                - send_resolved: true
                  api_url: <slack_hook_api>  #REPLACE Slack Hook Api url
                  channel: '#<slack_channel_name>' #REPLACE slack channel name
                  username: Alertmanager
                  title: '{{ template "slack.message.title" . }}'
                  text: '{{ template "slack.message.body" . }}'
        templates:
            - /etc/alertmanager/configmaps/alertmanager-templatefiles/template_1.tmpl
```

5\.  You can deploy the prometheus-operator using one of the below methods.

&#x20;    1\. Deploy using go lang deployer

&#x20;       `go run main.go deploy -e <environment_name> -c 'prometheus-operator,grafana,prometheus-kafka-exporter'`

&#x20;   `go run main.go deploy -e <environment_name> -c 'nginx-ingress'`

&#x20;   2\. Deploy using Jenkin’s deployment job. (here we are using deploy-to-dev, you can choose your environment specific deployment job )

![](<../.gitbook/assets/image (40).png>)

You can connect to the Jaeger console at [https://](https://qa.digit.org/monitoring/?orgId=1)[\<your\_domin\_name>/](https://egov-micro-qa.egovernments.org/tracing/search)[monitoring/](https://qa.digit.org/monitoring/?orgId=1)

## **To create a new panel in the existing dashboard:-**   <a href="#to-create-a-new-panel-in-the-existing-dashboard" id="to-create-a-new-panel-in-the-existing-dashboard"></a>

1. &#x20;Login to the dashboard and click on add panel &#x20;

![](<../.gitbook/assets/image (9).png>)

1. Set all required queries and apply the changes. Export the JSON file by clicking on the save dashboard

![](<../.gitbook/assets/image (61).png>)

3\. Go to the configs repo and select your branch. In the branch look for monitoring-dashboards folder and update the existing \*-dashboard.json with a newly exported JSON file.



### Additional Instructions:

If due for some reason you are not able to access the monitoring dashboard from your sub-domain, You can use the below command to access the monitoring dashboard

```
kubectl port-forward svc/grafana 8080:3000 -n monitoring
```

**Note**: port 8080 is for local access, if you are utilizing the 8080 port you can use the different port as well.

To access the monitoring hit the browser with this **localhost:8080** url.
