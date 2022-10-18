# Notification Enhancement Based on Different Channels

## Overview <a href="#overview" id="overview"></a>

* Configuration of the notification messages for a business service based on the channel for the same event.

## **Key Functionalities** <a href="#key-functionalities" id="key-functionalities"></a>

* For a specific action of the user, they get an SMS and email as an acknowledgement.
* Users can get SMS, Event, and email-based on different channels.
* The application allows one to either send different messages across all channels based on their actions.

### **Enhancement Details** <a href="#details-of-enhancement" id="details-of-enhancement"></a>

* To have this functionality for different business services, a channel names file was created and added to the MDMS data.&#x20;
* It contains information about the combination of different actions and channels for a particular business service. Example -

```
 "channelList": [
 {   "businessService": "PT.CREATE",
     "module": "PT",
     "action" : "OPEN",
     "channelNames": ["SMS", "EMAIL", "EVENT"]
 }]
```

* The Different channels are
  * SMS: ID (Mobile Number)
  * Event&#x20;
  * Email: ID (Email ID)
* This feature enabled the functionality which would first check for the channels present in the file and send the notification accordingly.&#x20;
* For SMS event, it would send the SMS notification and log “Sending SMS Notification”, for Event it would log, “Event Notification Sent”, and for Email, it would log, “Email Notification Sent”.

### **Steps for Enabling/Disabling Channels**  <a href="#steps-for-enabling-disabling-channels-for-a-particular-business-service" id="steps-for-enabling-disabling-channels-for-a-particular-business-service"></a>

To add/delete any particular channel for a business service -

* Update channelNames array in [Channel List](https://github.com/egovernments/egov-mdms-data/blob/DEV/data/pb/Channel/channelList.json) file and add/delete the channel you want a business service’s action to have.
* Restart egov-mdms-service to apply the changes.
* Configure your business service with the steps mentioned below to configure the business service.

### **Business Service Configuration**  <a href="#configuration-for-a-particular-business-service" id="configuration-for-a-particular-business-service"></a>

* Add the details about the particular action and the channels you want that action to trigger in the [Channel List](https://github.com/egovernments/egov-mdms-data/blob/DEV/data/pb/Channel/channelList.json) file in egov-mdms-data repository.
* For any record that comes into the topic first, the service should fetch all the required data like user name, property id, mobile number, tenant id, etc from the record that is fetched from the topic.
* Fetch the message content from localization and the service replaces the placeholders with the actual data.
* Place the record in whichever channel’s topic that the SMS/email service is listening to.

