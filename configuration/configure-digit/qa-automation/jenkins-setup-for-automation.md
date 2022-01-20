# Jenkins Setup for Automation

## Overview

This tutorial will guide you through the step by step procedure to set up Jenkins on a ubuntu machine for automation purposes.

Connect to the remote machine using SSH and follow the steps mentioned below.

## Install Java 8

* sudo apt update
* sudo apt-get install openjdk-8-jdk
* java -version

## Install Jenkins

* sudo wget -q -O - [https://pkg.jenkins.io/debian-stable/jenkins.io.key](https://pkg.jenkins.io/debian-stable/jenkins.io.key) | sudo apt-key add -
* sudo sh -c 'echo deb[ ![](https://www.jenkins.io/sites/default/files/jenkins\_favicon.ico)Debian Jenkins Packages](http://pkg.jenkins.io/debian-stable) binary/ > /etc/apt/sources.list.d/jenkins.list'
* sudo apt update
* sudo apt install jenkins
* sudo systemctl start jenkins
* sudo systemctl status jenkins (should be active)

#### Install and setup apache2 for Jenkins

* sudo apt install apache2
* sudo a2enmod proxy
* sudo a2enmod proxy\_http
* sudo a2enmod headers
* **sudo vi /etc/apache2/sites-available/000-default.conf** and add following code inside **VirtualHost** xml tag:

```
##### ############################################################ ####
##### ============================================================ ####
##### The Build Business Websites Jenkins and Apache Configuration ####
##### ============================================================ ####
##### ############################################################ ####

ProxyPass         /jenkins  http://localhost:8080/jenkins nocanon
ProxyPassReverse  /jenkins  http://localhost:8080/jenkins

ProxyRequests     Off
AllowEncodedSlashes NoDecode

<Proxy http://localhost:8080/jenkins*>
  Order deny,allow
  Allow from all
</Proxy>

##### ============================================================ ####
##### ############################################################ ####
```

* **sudo vi /etc/default/jenkins** and make sure

```
JENKINS_ARGS="--webroot=/var/cache/$NAME/war --httpPort=$HTTP_PORT --prefix=/jenkins"
```

* sudo systemctl restart jenkins
* sudo systemctl restart apache2
* Open port 80 of the remote machine to make it accessible from the local machine

## Setup Jenkins

* sudo vi /var/lib/jenkins/secrets/initialAdminPassword
* copy the initial password inside the file
* now open remote-host-ip/jenkins in local browser
* paste the password, select the required plugin to install and start the installation

> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)\_\_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_ ](https://egov.org.in)_is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
