# Tech Enablement Training \(eDCR\) - Essential Skills and Prerequisites

## Introduction

This document aims to put together all the items which will enable to come up with a proper training plan for a partner team who will be working on the eDCR service used for the plan scrutiny.

## Technical Prerequisites

Below listed are the technical skillsets that are required to work on eDCR service. It is expected that the team planning on attending training is well versed with the mentioned technologies before they attend eGov training sessions.

### Skillset for the Development team

* Java and REST APIS
* Postgres 
* Maven
* Spring framework
* Basics of 2D CAD Drawings
* Git
* Postman
* YAML/JSON

### Skill Set for the DevOps team

* Strong working knowledge on Linux, command, VM Instances, networking, storage
* The session, cache, and tokens handling \(Redis-server\)
* Understanding of VM types, Linux OS types, LoadBalancer, VPC, Subnets, Security Groups, Firewall, Routing, DNS
* Experience setting up CI like Jenkins and create pipelines
* Artifactory - Nexus, verdaccio, DockerHub, etc
* Experience in setting up SSL certificates and renewal
* Gitops, Git branching, PR review process. Rules, Hooks, etc.
* JBoss Wildfly, Apache, Nginx, Redis and Postgres

### Hardware prerequisites

Trainees are expected to have laptops/ desktops configured as mentioned below with all the software required to run the eDCR service application.

* Laptop for hands-on training with 16GB RAM and OS preferably Ubuntu
* All developers need to have Git ids
* Install VSCode/IntelliJ/Eclipse
* Install [Git ](https://git-scm.com/downloads)
* Install [JDK 8 update 112 or higher](http://www.oracle.com/technetwork/java/javase/downloads)
* Install [maven v3.2.x](http://maven.apache.org/download.cgi)
* Install [PostgreSQL v9.](http://www.postgresql.org/download/)6
* Postman
* Install LibreCAD
* Application Server [JBoss Wildfly v11.x](https://devops.egovernments.org/Downloads/wildfly/wildfly-11.0.0.Final.zip)

### Software Assets

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
        <p>How to create database and set up privileges?</p>
        <p>How to add index on table?</p>
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
      <td style="text-align:left">JSON</td>
      <td style="text-align:left">
        <p><a href="https://www.tutorialspoint.com/json/index.htm">https://www.tutorialspoint.com/json/index.htm</a>
        </p>
        <p><a href="https://github.com/json-path/JsonPath"><img src="https://github.com/fluidicon.png" alt/>json-path/JsonPath</a>
        </p>
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
        <p>What is the difference between version and SNAPSHOT?</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">eDCR Approach Guide</td>
      <td style="text-align:left"><a href="https://digit-discuss.atlassian.net/l/c/Gh0kEwC6">eDCR Approach Guide</a>
      </td>
      <td style="text-align:left">How to configuring and customizing the eDCR engine as per the state/city
        rules and regulations.</td>
    </tr>
    <tr>
      <td style="text-align:left">eDCR Service setup</td>
      <td style="text-align:left">
        <p><a href="https://digit-discuss.atlassian.net/l/c/gLYMCaS7">Development Control Rules (Digit-DCR)</a>
        </p>
        <p><a href="https://digit-discuss.atlassian.net/l/c/8s5or1tz">Setting Up eDCR Service</a>
        </p>
      </td>
      <td style="text-align:left">Overall Flow of eDCr service, design and setup process</td>
    </tr>
  </tbody>
</table>





[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)_​_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in/) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._

