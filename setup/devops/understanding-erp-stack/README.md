# Understanding ERP Stack

This section contains steps that are involved in the build and deploy the application. 

### **Build Stages**

1. Checking out code from github
2. Maven Build process \(includes the Junit tests\):

&gt; **Apache Maven**: to manage dependencies for projects. Maven can be installed as a command**-**line tool.

1. Creating Artifacts \(EAR\) on successful build process:

&gt; An artefact is an assembly of any project assets that you put together to test, deploy or distribute your software solution or its part.  
&gt; Examples are a collection of compiled Java classes or a Java application packaged in a Java archive, a Web application as a directory structure or a Web application archive, etc.  
&gt; An artefact can be an archive file or a directory structure that includes the following structural elements:

1. Compilation output for one or more of your modules
2. Libraries included in module dependencies
3. Collections of resources \(web pages, images, descriptor files, etc.\)
4. Other artefacts
5. Individual files, directories and archives.
6. Deploy the same to the respective environments:

&gt; maven deploy to nexus - Nexus is the option for hosting third-party artefacts, as well as for reusing internal artefacts across development streams.  
&gt; **Nexus** \(sonatype\) is a repository manager - It allows you to proxy, collect, and manage your dependencies so that you are not constantly juggling a collection of JARs. It makes it easy to distribute your software. Internally, you configure your build to publish artefacts to **Nexus** and they then become available to other developers.  
  
**Inside ERP Stack:**   
Fig.1.0: Graphical Representation of ERP Architecture

![](https://digit-discuss.atlassian.net/wiki/download/thumbnails/8716301/worddav665bdb5f17de344bd1557562a65638e7.png?version=1&modificationDate=1553666606212&cacheVersion=1&api=v2&width=712&height=405)

#### **1. Apache Web servers for Load Balancer**:

1.1 **Load Balancer** - A load balancer is a device that distributes network or application traffic across a cluster of servers. Load balancing improves responsiveness and increases the availability of applications.  
1.2 **Apache** HTTP server - is a cross-platform web server. A web server is the software application that receives your request to access a web page. It runs a few security checks on your HTTP request and takes you to the web page.

#### **2. WildFly for Application Servers** with instances \(with java as a prerequisite\)

2.1 Application Server - An application server is a software framework that provides both facilities to create web applications and a server environment to run them  
2.1 WildFly - is a Java EE 8 certified application server. It provides a list of services as,

1. JDBC connection pool
2. **ArtemisMQ -** messaging broker
3. Resource adapter
4. EJB container - where you can deploy remote services
5. **Undertow -** lightweight and performant web server
6. Batch job scheduler to execute tasks and jobs
7. **Redis cache** for \(Tokens, auth, sessions, etc.,\)
8. **Elastic Search**
9. **Postgres as DB**

Our ERP application architecture follows the 3-tier architecture for web applications\*.

### **Accessing the application using IP address and domain name**

This section is to be referred to only if you want the application to run using any IP address or domain name.

1. Domains should be registered with hosts
2. Sub-domains must be created and should point to the Load Balancer IP \(elasticIP\)

&gt; Sub-domains are like: multi-tenant based, environment\(DEV/QA/UAT\) based, and others like issues.jira, etc.,  
&gt; create name-based virtual hosts for the sub-domains, which helps in picking up the right application servers, and schemas likewise.  
tenant.env.domain = name  
name → hosts, schemas, etc., which helps to access the application at right hosts pointing to.

1. To access the application using IP address:

   Have an entry in the table \(eg\_city\) in the database with an IP address of the machine where the application server is running \(for ex: domainurl="172.16.2.164"\) to access the application using the IP address.  
   &gt; Access the application using the URL [http://172.16.2.164:8080/egi/](http://172.16.2.164:8080/egi/) where 172.16.2.164 is the IP and 8080 is the port of the machine where the application server is running.

2.  To access the application using a domain name: 

   &gt;Have an entry in the table \(eg\_city\) in the database with a domain name \(for ex: domainurl= "www.egoverpphoenix.org"\) to access the application using a domain name.  
   &gt; Add the entry in the hosts file of your system with details as 172.16.2.164 www.egoverpphoenix.org \(This needs to be done both in server machine as well as the machines in which the application needs to be accessed since this is not a public domain\).  
   &gt; Access the application using the URL [http://www.egoverpphoenix.org:8080/egi/](http://www.egoverpphoenix.org:8080/egi/) where www.egoverpphoenix.org is the domain name and 8080 is the port of the machine where the application server is running.  
   Always start the wildfly server with the below command to access the application using the IP address or domain name.  
   **nohup ./standalone.sh -b 0.0.0.0 &**

**Two ways of Deployments**

1. Manual Deployment - Copy the EAR files on the deployment folder and start the server.
2. Hot Deployment - using WildFly management console\(it always listens at 9990\), and using curl upload and publish the EAR.

**Release Process**  
Fig.2.0: Release Process Diagram  
_**\*References:**_  
**3-Tier Architecture in ERP:**

![](https://digit-discuss.atlassian.net/wiki/download/thumbnails/8716301/worddav50180a8c1ed02e7def72ed57ac5d09b6.png?version=1&modificationDate=1553666609164&cacheVersion=1&api=v2&width=624&height=355)

A typical enterprise application consists of at least three different types of components:

1. Presentation layer – Components that handle HTTP requests and implement either a \(REST\) API or an HTML‑based web UI. In an application that has a sophisticated user interface, the presentation tier is often a substantial body of code.
2. Business logic layer – Components that are the core of the application and implement the business rules.
3. Data‑access layer – Components that access infrastructure components such as databases and message brokers.

A three-tier architecture is a client-server architecture in which the functional process logic, data access, computer data storage and user interface are developed and maintained as independent modules on separate platforms. Three-tier architecture is a software design pattern and a well-established software architecture.

Fig.3.0: AWS 3-Tier Architecture Diagram

![](https://digit-discuss.atlassian.net/wiki/download/thumbnails/8716301/worddav4faa0e315d2eb20c1297023c7aa65d51.png?version=1&modificationDate=1553666611915&cacheVersion=1&api=v2&width=649&height=459)



 [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)​](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation](https://egov.org.in/) is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).

