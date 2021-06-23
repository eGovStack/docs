# Configure SMS and Email

## Overview <a id="Overview"></a>

* Notification service can notify the user through SMS and email for there action on DIGIT as an acknowledgement that their action has been successfully completed.
* ex: actions like property create, TL create, etc.
* To send SMS we need the help of 2 services, one on which the user is taking action and the second SMS service.
* To send an email we need the help of 2 services, one on which the user is taking action and second email service.

## Pre-requisites <a id="Pre-requisites"></a>

Before you proceed with the configuration, make sure the following pre-requisites are met -

* Prior Knowledge of Spring boot.
* Prior Knowledge of Kafka.
* Prior Knowledge of localization service.

## Key Functionalities <a id="Key-Functionalities"></a>

* For a specific action of the user, he/she will get a SMS and email as an acknowledgment.
* Users can get SMS and email based on the localization language.

## Configuration Details <a id="Configuration-Details"></a>

* If you want to take action for a specific action on that action the service has to listen to a particular topic so that each time any record comes to the topic consumer will know that action has been taken and can trigger a notification for it.
  * ex: if you want to trigger a notification for Property create then the property service’s NotificationConsumer class should listen to topic egov.pt.assessment.create.topic so that each time any record comes to the topic egov.pt.assessment.create.topic NotificationConsumer will know that Property creates action that has been taken and can trigger a notification for it.
* when any record comes into the topic first the service will fetch all the required data like user name, property id, mobile number, tenant id, etc from the record which we fetched from the topic.
* Then we will fetch the message contain from localization and the service replaces the placeholders with the actual data.
* Then put the record in SMS topic in which SMS service is listening.
* email service is also listening to the same topic which SMS service is listening.

## Reference Docs <a id="Reference-Docs"></a>

### Doc Links <a id="Doc-Links"></a>

| **Title** | **Link** |
| :--- | :--- |
| NotificationConsumer | [https://github.com/egovernments/municipal-services/blob/master/property-services/src/main/java/org/egov/pt/consumer/NotificationConsumer.java](https://github.com/egovernments/municipal-services/blob/master/property-services/src/main/java/org/egov/pt/consumer/NotificationConsumer.java) |
|  |  |

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)​](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation](https://egov.org.in/) is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).

