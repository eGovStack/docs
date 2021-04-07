# Operational Best practices

### **Introduction**

This article provides DIGIT Infra overview, Guidelines for Operational Excellence while DIGIT is deployed on SDC, NIC or any commercial clouds along with the recommendations and [segregation of duties \(SoD\)](https://medium.com/@jeehad.jebeile/devops-and-segregation-of-duties-9c1a1bea022e). It helps to plan the procurement and build the necessary capabilities to deploy and implement DIGIT.

In a shared control, the state program team/partners can consider these guidelines and must provide their own control implementation to the state’s cloud infrastructure and partners for a standard and smooth operational excellence.

### Operational Recommendations

DIGIT strongly recommends [Site reliability engineering](https://medium.com/@alexbmeng/site-reliability-engineering-principals-fd52229bfcd6) \(SRE\) principles as a key means to bridge between development and operations by applying a software engineering mindset to system and IT administration topics.  In general, an SRE team is responsible for availability, latency, performance, efficiency, change management, monitoring, emergency response, and capacity planning.   


Monitoring Tools Recommendations: Commercial clouds like [AWS](https://aws.amazon.com/cloudwatch/), [Azure](https://adinermie.com/azure-monitoring-tools-explained-part-10-network-watcher/) and GCP offer sophisticated monitoring solutions across various infra levels like CloudWatch and StackDriver, in the absence of such managed services to monitor we can look at various best practices and tools listed below which helps [debugging and troubleshooting](https://raygun.com/blog/best-practices-microservices/) efficiently.

* [**Network monitoring**](https://www.dnsstuff.com/network-scanning)**,** [**Diagnosis**](https://www.dnsstuff.com/network-troubleshooting-steps)**,** [**Assessment**](https://www.dnsstuff.com/best-network-assessment-tools-and-network-assessment-checklist)**,**  [**Identify the latency**](https://www.dnsstuff.com/network-latency) ****
* [**Systems**](https://www.dnsstuff.com/systems)
* [**Application monitoring**](https://medium.com/@Alibaba_Cloud/system-monitoring-using-prometheus-and-grafana-8007d3aaf400)
* [**Web application monitoring**](https://medium.com/flask-monitoringdashboard-turtorial/monitor-your-flask-web-application-automatically-with-flask-monitoring-dashboard-d8990676ce83)
* [**Alert management**](https://medium.com/@abhishekbhardwaj510/alertmanager-integration-in-prometheus-197e03bfabdf)**,** [**Alert Types**](https://awesome-prometheus-alerts.grep.to/rules.html)
* [**Distributed Tracing**](https://medium.com/velotio-perspectives/a-comprehensive-tutorial-to-implementing-opentracing-with-jaeger-a01752e1a8ce)
* [**Telemetry**](https://medium.com/jaegertracing/jaeger-and-opentelemetry-1846f701d9f2)

### **Key Standard Operating Procedures \(SOPs\):**

* Segregation of duties and responsibilities.
* SME and SPOCs for [L1.5](https://www.quora.com/What-is-L1-5-support-in-the-IT-industry-especially-in-Cognizant-What-is-the-scope-in-this-type-of-project) support along with the SLAs defined.
* [Ticketing system](https://medium.com/swlh/incident-management-process-5655ba586cf4) to manage incidents, converge and collaborate on various operational issues.
* Monitoring dashboards at various levels like Infrastructure, Network and applications.
* Transparency of monitoring data and collaboration between teams.
* Periodic remote sync up meetings, acceptance and attendance to the meeting.
* Ability to see stakeholders availability of calendar time to schedule meetings.
* Periodic \(weekly, monthly\) summary reports of the various infra, operations incident categories.
* Communication channels and synchronization on a regular basis and also upon critical issues, changes, upgrades, releases etc.

### **Segregation of Duties:** 

While DIGIT is deployed at state cloud infrastructure, it is essential to identify and distinguish the responsibilities between Infrastructure, Operations and Implementation partners. Identify these teams and assign SPOC, define responsibilities and Incident management is followed to visualize, track issues and manage dependencies between teams. Essentially these are monitored through dashboards and alerts are sent to the stakeholders proactively. eGov team can provide consultation and training on the need basis depending any of the below categories.

* **State program team -** Refers to the owner for the whole DIGIT implementation, application rollouts, capacity building. Responsible for identifying and synchronizing the operating mechanism between the below teams. 
* **Implementation partner -** Refers to the DIGIT Implementation, application performance monitoring for errors, logs scrutiny, TPS on peak load, distributed tracing, DB queries analisis, etc. 
* **Operations team -** this team could be an extension of the implementation team who is responsible for DIGIT deployments, configurations, CI/CD, change management, traffic monitoring and alerting, log monitoring and dashboard, application security, DB Backups, application uptime, etc.
* **State IT/Cloud team -**Refers to state infra team for the Infra, network architecture, LAN network speed, internet speed, OS Licensing and upgrade, patch, compute, memory, disk, firewall, IOPS, security, access, SSL, DNS, data backups/recovery, snapshots, capacity monitoring dashboard.  

### **Skills Required to Set up, Operate and Maintain DIGIT on SDC:**

<table>
  <thead>
    <tr>
      <th style="text-align:left"><b>Tools/Skills</b>
      </th>
      <th style="text-align:left"><b>Specification</b>
      </th>
      <th style="text-align:left"><b>Weightage (1-5)</b>
      </th>
      <th style="text-align:left"><b>Yes/No</b>
      </th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">System Administration</td>
      <td style="text-align:left">Linux Administration, troubleshooting, OS Installation, Package Management,
        Security Updates, Firewall configuration, Performance tuning, Recovery,
        Networking, Routing tables, etc</td>
      <td style="text-align:left">4</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Containers/Dockers</td>
      <td style="text-align:left">Build/Push docker containers, tune and maintain containers, Startup scripts,
        Troubleshooting dockers containers.</td>
      <td style="text-align:left">2</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Kubernetes</td>
      <td style="text-align:left">
        <p>Setup kubernetes cluster on bare-metal and VMs using kubeadm/kubespary,
          terraform, etc. Strong understanding of various kubernetes components,
          configurations, kubectl commands, RBAC. Creating and attaching persistent
          volumes, log aggregation, deployments, networking, service discovery, Rolling
          updates. Scaling pods, deployments, worker nodes, node affinity, secrets,
          configMaps, etc..</p>
        <p></p>
      </td>
      <td style="text-align:left">3</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Database Administration</td>
      <td style="text-align:left">Setup PostGres DB, Set up read replicas, Backup, Log, DB RBAC setup, SQL
        Queries</td>
      <td style="text-align:left">3</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Docker Registry</td>
      <td style="text-align:left">Setup docker registry and manage</td>
      <td style="text-align:left">2</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">SCM/Git</td>
      <td style="text-align:left">Source Code management, branches, forking, tagging, Pull Requests, etc.</td>
      <td
      style="text-align:left">4</td>
        <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">CI Setup</td>
      <td style="text-align:left">Jenkins Setup, Master-slave configuration, plugins, jenkinsfile, groovy
        scripting, Jenkins CI Jobs for Maven, Node application, deployment jobs,
        etc.</td>
      <td style="text-align:left">4</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Artifact management</td>
      <td style="text-align:left">Code artifact management, versioning</td>
      <td style="text-align:left">1</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Apache Tomcat</td>
      <td style="text-align:left">Web server setup, configuration, load balancing, sticky sessions, etc</td>
      <td
      style="text-align:left">2</td>
        <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">WildFly JBoss</td>
      <td style="text-align:left">Application server setup, configuration, etc.</td>
      <td style="text-align:left">3</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Spring Boot</td>
      <td style="text-align:left">Build and deploy spring boot applications</td>
      <td style="text-align:left">2</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">NodeJS</td>
      <td style="text-align:left">NPM Setup and build node applications</td>
      <td style="text-align:left">2</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Scripting</td>
      <td style="text-align:left">Shell scripting, python scripting.</td>
      <td style="text-align:left">4</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Log Management</td>
      <td style="text-align:left">Aggregating system, container logs, troubleshooting. Monitoring Dashboard
        for logs using prometheus, fluentd, Kibana, Grafana, etc.</td>
      <td style="text-align:left">3</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">WordPress</td>
      <td style="text-align:left">Multi-tenant portal setup and maintain</td>
      <td style="text-align:left"><b>2</b>
      </td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>

