# Email Notification Service

## Overview <a href="#overview" id="overview"></a>

The objective of this service is to create a common point to manage all the email notifications being sent out of the platform. Notification email service consumes email requests from the Kafka notification topic and processes them to send it to a third party service. Modules like PT, TL, PGR etc make use of this service to send messages through the Kafka Queue.

## Pre-requisites <a href="#pre-requisites" id="pre-requisites"></a>

Before you proceed with the documentation, make sure the following pre-requisites are met -

* Prior Knowledge of Java/J2EE
* Prior Knowledge of SpringBoot
* Prior Knowledge of third party API integration
* Prior Knowledge of REST APIs and related concepts like path parameters, headers, JSON etc
* Prior Knowledge of Kafka and related concepts like Producer, Consumer, Topic etc.

## Key Functionalities <a href="#key-functionalities" id="key-functionalities"></a>

* Provide a common platform to send email notifications to the users
* Support localised email.

## Configuration Details <a href="#configuration-details" id="configuration-details"></a>

egov-notification-mail is a consumer that listens to the egov.core.notification.email topic, reads the message and generates email using the SMTP Protocol. The services need that the senders email is configured. On the other hand, if the senders email is not configured, the service gets the email id by internally calling egov-user service to fetch email id. Once the email is generated, the content is localized by egov-localization service after which it is notified to the email id.&#x20;

## Deployment Details <a href="#deployment-details" id="deployment-details"></a>

1. Deploy the latest version of the notification email service.
2. Make sure the consumer topic name for email service is added in deployment configs.

## Integration <a href="#integration" id="integration"></a>

### Integration Scope <a href="#integration-scope" id="integration-scope"></a>

The email notification service is used to send out email notifications for all miscellaneous / adhoc services that citizens avail of from the ULBs.

### Integration Benefits <a href="#integration-benefits" id="integration-benefits"></a>

* Can perform service-specific business logic without impacting the other modules.
* In the future, if we want to expose the application to citizens then it can be done easily.

### Steps to Integration <a href="#steps-to-integration" id="steps-to-integration"></a>

1. To integrate, the client service should send email requests to the email notification consumer topic.



> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)_​_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
