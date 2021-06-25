# Tech Enablement Training - Essential Skills and Pre-requisites

## Introduction <a id="Introduction"></a>

This document aims to put together all the items which will enable us to come up with a proper training plan for a partner team that will be working on the DIGIT platform.

## Technical Prerequisites <a id="Technical-Prerequisites"></a>

Below listed are the technical skill sets that are required to work on the DIGIT stack. It is expected the team planning on attending training is well versed with the mentioned technologies before they attend eGov training sessions.

### Skillset for the Development team <a id="Skillset-for-the-Development-team"></a>

* Open API Contract - Swagger2.0
* YAML/JSON
* Postman
* Postgres 
* Java and REST APIS
* Basics of Elasticsearch
* Maven
* Springboot
* Kafka
* Zuul
* NodeJS, ReactJS
* WordPress
* PHP

### Skill Set for the DevOps team <a id="Skill-Set-for-the-DevOps-team"></a>

* Understanding of the microservice architecture.
* Experience of AWS, Azure, GCP, NIC Cloud.
* Strong working knowledge of Linux, command, VM Instances, networking, storage.
* To create Kubernetes cluster on AWS, Azure, GCP on NIC Cloud.
* Kubectl installation & commands \(apply, get, edit, describe k8s objects\)
* Terraform for infra-as-code for cluster or VM provisioning.
* Understanding of VM types, Linux OS types, LoadBalancer, VPC, Subnets, Security Groups, Firewall, Routing, DNS\)
* Experience setting up CI like Jenkins and create pipelines.
* Deployment strategies - Rolling updates, Canary, Blue/Green.  
* Scripting - Shell, Groovy, Python and GoLang.
* Experience in Baking Containers and Dockers. 
* Artifactory - Nexus, Verdaccio, DockerHub, etc.
* Experience on Kubernetes ingress, setting up SSL certificates and renewal
* Understanding on Zuul gateway
* Gitops, Git branching, PR review process. Rules, Hooks, etc.
* Experience in Helm, packaging and deploying.
* JBoss Wildfly, Apache, Nginx, Redis and Postgres.

## Hardware prerequisites <a id="Hardware-prerequisites"></a>

Trainees are expected to have laptops/ desktops configured as mentioned below with all the software required to run the DIGIT application

* Laptop for hands-on training with 16GB RAM and OS preferably Ubuntu
* All developers need to have Git ids
* Install VSCode/IntelliJ/Eclipse
* Install [Git ](https://git-scm.com/downloads)
* Install [JDK 8 update 112 or higher](http://www.oracle.com/technetwork/java/javase/downloads)
* Install [maven v3.2.x](http://maven.apache.org/download.cgi)
* Install [PostgreSQL v9.](http://www.postgresql.org/download/)6
* Install [Elastic Search v2.4.x](https://download.elasticsearch.org/elasticsearch/elasticsearch/elasticsearch-2.4.1.zip)
* Postman

## Software Assets <a id="Software-Assets"></a>

There are knowledge assets available in the Net for general items and eGov assets for DIGIT services. Here you can find references to each of the topics of importance. It is mandated the trainees do a self-study of all the software mentioned in the prerequisites using the reference materials shared.

<table>
  <thead>
    <tr>
      <th style="text-align:left"><b>Topic</b>
      </th>
      <th style="text-align:left"><b>Reference</b>
      </th>
      <th style="text-align:left"><b>Preparedness Check</b>
      </th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Git</td>
      <td style="text-align:left">
        <p><a href="https://www.atlassian.com/git">https://www.atlassian.com/git</a>
        </p>
        <p><a href="https://www.tutorialspoint.com/git/index.htm">https://www.tutorialspoint.com/git/index.htm</a>
        </p>
        <p><a href="https://www.udemy.com/course/git-complete/">https://www.udemy.com/course/git-complete/</a>
        </p>
      </td>
      <td style="text-align:left">
        <p>Do you have a Git account?</p>
        <p>Do you know how to clone a repository, pull updates, push updates?</p>
        <p>Do you know how to give a pull request and merge the pull request?</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Microservice Architecture</td>
      <td style="text-align:left">
        <p><a href="https://www.tutorialspoint.com/microservice_architecture/index.htm">https://www.tutorialspoint.com/microservice_architecture/index.htm</a>
        </p>
        <p><a href="https://www.udemy.com/course/microservices-with-spring-boot-and-spring-cloud/">https://www.udemy.com/course/microservices-with-spring-boot-and-spring-cloud/</a>
        </p>
      </td>
      <td style="text-align:left">
        <p>Do you know when to create a new service?</p>
        <p>How to access other services?</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">ReactJS</td>
      <td style="text-align:left">
        <p><a href="https://reactjs.org/tutorial/tutorial.html">https://reactjs.org/tutorial/tutorial.html</a>
        </p>
        <p><a href="https://www.udemy.com/course/react-the-complete-guide-incl-redux">https://www.udemy.com/course/react-the-complete-guide-incl-redux</a>
        </p>
        <p><a href="https://www.tutorialspoint.com/reactjs/reactjs_overview.htm">https://www.tutorialspoint.com/reactjs/reactjs_overview.htm</a>
        </p>
      </td>
      <td style="text-align:left">
        <p>How to create react app?</p>
        <p>How to create a Stateful and Stateless Component?</p>
        <p>How to use HOC as a wrapper?</p>
        <p>Validations at form level using React.js and Redux</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Postgres</td>
      <td style="text-align:left">
        <p><a href="https://www.postgresqltutorial.com/">https://www.postgresqltutorial.com/</a>
        </p>
        <p><a href="https://www.udemy.com/course/the-complete-python-postgresql-developer-course/">https://www.udemy.com/course/the-complete-python-postgresql-developer-course/</a>
        </p>
        <p><a href="https://www.tutorialspoint.com/postgresql/index.htm">https://www.tutorialspoint.com/postgresql/index.htm</a>
        </p>
      </td>
      <td style="text-align:left">
        <p>How to create a database and set up privileges?</p>
        <p>How to add an index on a table?</p>
        <p>How to use aggregation functions in psql?</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Postman</td>
      <td style="text-align:left">
        <p><a href="https://www.postman.com/resources/videos-tutorials/">https://www.postman.com/resources/videos-tutorials/</a>
        </p>
        <p><a href="https://www.udemy.com/course/postman-the-complete-guide/">https://www.udemy.com/course/postman-the-complete-guide/</a>
        </p>
      </td>
      <td style="text-align:left">
        <p>Call a REST API from Postman with proper payload and show the response</p>
        <p>Setup any service locally(MDMS or user service has least dependencies)
          and check the API&#x2019;s using postman</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">REST APIs</td>
      <td style="text-align:left">
        <p><a href="https://www.tutorialspoint.com/rest_api/index.asp">https://www.tutorialspoint.com/rest_api/index.asp</a>
        </p>
        <p><a href="https://www.youtube.com/watch?v=rtWH70_MMHM">https://www.youtube.com/watch?v=rtWH70_MMHM</a>
        </p>
      </td>
      <td style="text-align:left">
        <p>What are the principles to be followed when making a REST API?</p>
        <p>When to use POST and GET?</p>
        <p>How to define the request and response parameters?</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Kafka</td>
      <td style="text-align:left">
        <p><a href="https://www.udemy.com/course/apache-kafka/">https://www.udemy.com/course/apache-kafka/</a>
        </p>
        <p><a href="https://kafka.apache.org/intro">https://kafka.apache.org/intro</a>
        </p>
        <p><a href="https://www.tutorialspoint.com/apache_kafka/apache_kafka_introduction.htm">https://www.tutorialspoint.com/apache_kafka/apache_kafka_introduction.htm</a>
        </p>
      </td>
      <td style="text-align:left">
        <p>How to push messages on Kafka topic?</p>
        <p>How does the consumer group work?</p>
        <p>What are partitions?</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Docker and Kubernetes</td>
      <td style="text-align:left">
        <p><a href="https://www.tutorialspoint.com/kubernetes/index.htm">https://www.tutorialspoint.com/kubernetes/index.htm</a>
        </p>
        <p><a href="https://www.udemy.com/course/docker-and-kubernetes-the-complete-guide/">https://www.udemy.com/course/docker-and-kubernetes-the-complete-guide/</a>
        </p>
        <p><a href="https://www.tutorialspoint.com/docker/index.htm">https://www.tutorialspoint.com/docker/index.htm</a>
        </p>
      </td>
      <td style="text-align:left">
        <p>How to edit deployment configuration?</p>
        <p>How to read logs?</p>
        <p>How to go inside a Kubernetes pod?</p>
        <p>How to create a docker file using a base image?</p>
        <p>How to port-forward the pod to the local port?</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">JSON</td>
      <td style="text-align:left"><a href="https://www.tutorialspoint.com/json/index.htm">https://www.tutorialspoint.com/json/index.htm</a> 
        <a
        href="https://github.com/json-path/JsonPath">json-path/JsonPath</a>
      </td>
      <td style="text-align:left">How to write filters to extract specific data using jsonPaths?</td>
    </tr>
    <tr>
      <td style="text-align:left">YAML</td>
      <td style="text-align:left"><a href="https://www.udemy.com/course/yaml-essentials/">https://www.udemy.com/course/yaml-essentials/</a>
      </td>
      <td style="text-align:left">How to read an API contract using swagger?</td>
    </tr>
    <tr>
      <td style="text-align:left">Zuul</td>
      <td style="text-align:left"><a href="https://www.javatpoint.com/zuul-api-gateway">https://www.javatpoint.com/zuul-api-gateway</a>s</td>
      <td
      style="text-align:left">What does Zuul do?</td>
    </tr>
    <tr>
      <td style="text-align:left">Maven</td>
      <td style="text-align:left">
        <p><a href="https://www.udemy.com/course/maven-quick-start/">https://www.udemy.com/course/maven-quick-start/</a>
        </p>
        <p><a href="https://www.tutorialspoint.com/maven/index.htm">https://www.tutorialspoint.com/maven/index.htm</a>
        </p>
      </td>
      <td style="text-align:left">
        <p>What is POM?</p>
        <p>What is the purpose of maven clean install and how to do it?</p>
        <p>What is the difference between the version and SNAPSHOT?</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Springboot</td>
      <td style="text-align:left">
        <p><a href="https://www.tutorialspoint.com/spring_boot/index.htm">https://www.tutorialspoint.com/spring_boot/index.htm</a>
        </p>
        <p><a href="https://www.udemy.com/course/spring-hibernate-tutorial/">https://www.udemy.com/course/spring-hibernate-tutorial/</a>
        </p>
      </td>
      <td style="text-align:left">
        <p>How does Autowiring work in spring?</p>
        <p>How to write a consumer/producer using spring Kafka?</p>
        <p>How to make an API call to another service using restTemplate?</p>
        <p>How to execute queries using JDBC Template?</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Elastic search</td>
      <td style="text-align:left">
        <p><a href="https://www.udemy.com/course/elasticsearch-complete-guide/">https://www.udemy.com/course/elasticsearch-complete-guide/</a>
        </p>
        <p><a href="https://www.tutorialspoint.com/elasticsearch/index.htm">https://www.tutorialspoint.com/elasticsearch/index.htm</a>
        </p>
      </td>
      <td style="text-align:left">How to write basic queries to fetch data from elastic search index?</td>
    </tr>
    <tr>
      <td style="text-align:left">Wordpress</td>
      <td style="text-align:left">
        <p><a href="https://www.tutorialspoint.com/wordpress/index.htm">https://www.tutorialspoint.com/wordpress/index.htm</a>
        </p>
        <p><a href="https://www.udemy.com/course/wordpress-for-beginners-course/">https://www.udemy.com/course/wordpress-for-beginners-course/</a>
        </p>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">DIGIT Architecture</td>
      <td style="text-align:left">
        <p><a href="https://digit-discuss.atlassian.net/wiki/spaces/EPE/pages/85557250/Orientation+-+Platform+Overview">Orientation - Platform Overview</a>
        </p>
        <p><a href="https://digit-discuss.atlassian.net/wiki/spaces/DOPS/pages/112721941/DIGIT+Architecture+and+Technical+overview">DIGIT Architecture and Technical overview</a>
        </p>
      </td>
      <td style="text-align:left">
        <p>What comes as part of core service, business service and municipal services?</p>
        <p>How to calls APIs from one service in another service?</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">DIGIT Core Services</td>
      <td style="text-align:left"><a href="https://digit-discuss.atlassian.net/l/c/DYNz7y84">Product requirements</a>
      </td>
      <td style="text-align:left">Which are the core services in the DIGIT framework?</td>
    </tr>
    <tr>
      <td style="text-align:left">DIGIT DevOps</td>
      <td style="text-align:left">
        <p><a href="https://digit-discuss.atlassian.net/wiki/spaces/DOPS/pages/113705013/DevOps+Partners+-+KT+Content">DevOps Partners - KT Content</a>
        </p>
        <p><a href="https://digit-discuss.atlassian.net/wiki/spaces/DOPS/pages/27459718/DIGIT+Deployment">DIGIT Deployment</a>
        </p>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">DIGIT MDMS</td>
      <td style="text-align:left"><a href="https://digit-discuss.atlassian.net/wiki/spaces/DOPS/pages/110952456">MDMS Configuration:</a>
      </td>
      <td style="text-align:left">
        <p>How to read a master date from MDMS?</p>
        <p>How to add new data in an existing Master?</p>
        <p>Where is the MDMS data stored?</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">DIGIT UI Framework</td>
      <td style="text-align:left"><a href="https://digit-discuss.atlassian.net/wiki/spaces/EGR/pages/53051775/Egov+UI+framework">Getting started</a>
      </td>
      <td style="text-align:left">
        <p>How to add a new component to the framework?</p>
        <p>How to use an existing component?</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">DSS</td>
      <td style="text-align:left"><a href="https://digit-discuss.atlassian.net/wiki/spaces/EPE/pages/118554635/Product+-+DSS">Product - DSS</a>
      </td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation ](https://egov.org.in/)is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).

