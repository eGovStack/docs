---
description: Technical Configuration Doc
---

# User Events Services

## Overview <a href="#overview" id="overview"></a>

eGov-User-Events service provide a common point to manage all the events generated for the users in the system. Events include updates from multiple applications like PT, PGR, TL; events created by the employee addressing the citizen etc. This service provides the users with APIs to create , update and search the events.

## Pre-requisites <a href="#pre-requisites" id="pre-requisites"></a>

Before you proceed make sure the following pre-requisites are met -

* _Java 8_
* Kafka server is up and running
* egov-persister service is running and has egov-user-events persister config path added in it
* PSQL server is running  and database is created

## Key Functionalities <a href="#key-functionalities" id="key-functionalities"></a>

* Provide a common platform to create, manage and notify events
* Events can be created either by an API call or by pushing records to the Kafka queue

## Interaction Diagram <a href="#interaction-diagram" id="interaction-diagram"></a>

![](<../../../.gitbook/assets/image (274).png>)

## Deployment Details <a href="#deployment-details" id="deployment-details"></a>

1. Add the MDMS configs required for egov-user-events
2. Add the Role-Action mapping details for APIs
3. Deploy the latest version of egov-user-events
4. Add egov-user-events file in config folder in git and add that path in the persister . _(The file path should be added in environment yaml file in param called_ `persist-yml-path` _)_

## Configuration Details <a href="#configuration-details" id="configuration-details"></a>

Add master data in MDMS service with the module name as **mseva**. The sample master data for the service is given below:\
\
**Event Categories**

```
{
  "tenantId": "pb",
  "moduleName": "mseva",
  "EventCategories": [
    {
      "code": "PUBLICHEALTH",
      "eventType":"EVENTSONGROUND",
      "active": true
    },
    {
      "code": "CULTURAL",
      "eventType":"EVENTSONGROUND",
      "active": true
    },
    {
      "code": "WARDCOMMITTEEMEETING",
      "eventType":"EVENTSONGROUND",
      "active": true
    }
  ]
}
```

**Event Types**

```
{
  "tenantId": "pb",
  "moduleName": "mseva",
  "EventTypes": [
    {
      "code": "BROADCAST",
      "active": true
    },
    {
      "code": "EVENTSONGROUND",
      "active": true
    },
    {
      "code": "SYSTEMGENERATED",
      "active": true
    },
    {
      "code": "OTHERS",
      "active": true
    }
  ]
}
```

Use `/localization/messages/v1/_upsert` to add localisation (templates) for notification messages to be sent. The product notification templates are given below:

```
{
  "messages": [
    {
      "code": "egovuserevents.notification.counterevent.ondelete",
      "message": "<event_name> has been deleted. Please remove from your calendar.",
      "module": "egov-user-events",
      "locale": "en_IN"
    },
    {
      "code": "egovuserevents.notification.counterevent.onupdate",
      "message": "Details of <event_name> have been updated.",
      "module": "egov-user-events",
      "locale": "en_IN"
    }
  ]
}
```

**Configurable Properties**

The following properties are configurable in the application.properties file in egov-user-events service.

| **Property**                                        | **Value**                         | **Remarks**                                                                                                                                            |
| --------------------------------------------------- | --------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------ |
| <p>kafka.topics.persister.save.events</p><p> </p>   | <p>save-user-events</p><p> </p>   | This is the persister topic onto which user-events pushes records for persistence. This is for creating events.                                        |
| <p>kafka.topics.persister.update.events</p><p> </p> | <p>update-user-events</p><p> </p> | This is the persister topic onto which user-events pushes records for persistence. This is for updating events.                                        |
| <p>kafka.topics.lat.details</p><p> </p>             | <p>user-events-lat</p><p> </p>    | This is the persister topic onto which user-events pushes records for persistence. This is for storing last-access-time / last-login-time of the user. |
| <p>kafka.topics.save.events</p><p> </p>             | persist-user-events-async         | Topic to which the user-events consumer is subscribed. Producers willing to create events must push records to this topic.                             |
| kafka.topics.update.events                          | update-user-events-async          | Topic to which the user-events consumer is subscribed. Producers willing to update events must push records to this topic                              |
| <p>mseva.notif.search.offset</p><p> </p>            | 0                                 | Default pagination offset.                                                                                                                             |
| <p>mseva.notif.search.limit</p><p> </p>             | 200                               | Default pagination limit.                                                                                                                              |

**Entities**

**Events:** Model to capture the events information. This object captures all event details that is either created or updated.

**EventDetails:** Captures details of the event such as organiser, location, time etc are captured here. This is the child object to the Events object. This holds significance only if the type of the event is ‘EVENTSONGROUND’.

**Action:** This captures the user-actions involved in the event. For instance, the pay now option, reopen option, download certificate option etc.

**Recipient:** Every event is addressed to a crowd to which a notification for the same is sent. This model captures information about the recipients of the notification of this event or can also be framed as details of the addressee of the event.

**Event Type:** Events are divided into multiple types as follows:

1. BROADCAST - These are messages broadcasted addressing a group of people. For instance, “There’s road blockage near the bus stand, please use a different route”
2. EVENTSONGROUND - These are events organised by a group of people addressing another group of people. Usually, it is the ULB organising events for the citizens. It can be any activity like a 10K Marathon, Polio Drive, Property Tax collection drive etc.&#x20;
3. SYSTEMGENERATED - These events are generated by different systems on the egov platform like PT, TL, PGR etc addressing a group of people. For instance, “Dear Citizen, Your TL has been approved please proceed to pay \<PAY\_NOW>”
4. OTHERS - Events that don’t belong to the types mentioned above.

The following are configured in MDMS.

Event Category: Events are categorised into the following:

1. PUBLICHEALTH - Events related to public health
2. CULTURAL - Cultural events
3. WARDCOMMITEEMEETING - Events for recurring meetings of the ward committee

These event categories are mapped to event types internally. The categories mentioned here are for EVENTSONGROUND type. These are configured in MDMS.

**How does it work**

This service manages user events on the egov-platform, which means all the events about which the user (essentially citizen) has to be notified are stored and retrieved through this service. Events can be created either by an API call or by pushing records to the Kafka queue.&#x20;

Every event contains information about the event type, event category, event name, description, recipient, actions, event details etc. Based on the type of event, the list of mandatory fields varies.&#x20;

MDMS configurations file link: [<img src="https://github.com/fluidicon.png" alt="" data-size="line">egov-mdms-data/data/pb/mseva at master · egovernments/egov-mdms-data](https://github.com/egovernments/egov-mdms-data/tree/master/data/pb/mseva)

Once the event is sent for creation, the service validates all the required fields and assigns a recipient list to that event. An event can be addressed to a particular person, group of people, a user type and also roles. Events like updates on the TL application are addressed to the TL owners while events like Polio drive are addressed to the entire ULB. Some events like mass Bill generation are addressed only to those who are required to pay those bills. A recipient list is generated based on the request and stored in the system.&#x20;

When an event is updated a counter-event is generated. Counter events are of 2 types: Counter event on Delete and Counter event on Update. When an event in ACTIVE status is made INACTIVE or CANCELLED, counter-event on delete is generated. When details of an event are updated irrespective of the status a counter-event on update is generated. These counter-events are stored along with the actual events in the system. However, when a counter-event on delete is generated, its corresponding actual event is marked INACTIVE. &#x20;

One of the important aspects of this service is the search API. Searching for the events stored in the user-events system is different for different roles. When citizens search, all the events addressed to the citizens are retrieved. The events that contain corresponding counter-events are deduplicated and only the latest ACTIVE events are returned.&#x20;

We have a use case where past events have to be marked INACTIVE. This applies to all the BROADCAST and EVENTSONGROUND types of events which are time-capped. If a BROADCAST event is active from 1/Jan to 10/Jan, it will be marked inactive post 10/Jan, after which the citizens stop receiving any updates to that event. This change of status of the events is achieved by a lazy-update technique instead of a cron-job. Due to this, the search API not only returns the events but also updates the status of events before returning it to the user based on whether it has expired.&#x20;

When an employee searches, all the EVENTSONGROUND posted in the particular ULB are returned by default irrespective of the status. Once the actions are performed on the events that are active, the notifications are triggered to the citizens.

Employees can search for events based on the date range. The events created or last modified in that range are displayed in the search response. So, to get the details about event in a particular date range pass the value in **fromDate** and **toDate** field of search criteria.

_**fromDate**_ and _**toDate**_ fields accept epoch values only.&#x20;

And to get details about the Delete event, pass Status as **CANCELLED.** To get details about the Broadcast event pass eventType as **BROADCAST.**

Review the code and descriptions for every method to understand the use-cases and flow-of-logic in a better way.

## Integration <a href="#integration" id="integration"></a>

### Integration Scope <a href="#integration-scope" id="integration-scope"></a>

eGov-user-events can be integrated with any organisation or system which wants to send the events generated for the user in the system

### Integration Benefits <a href="#integration-benefits" id="integration-benefits"></a>

* Easy management of user events on the system - which means all the events about which the user (essentially citizen) has to be notified are stored and retrieved through this service.

### Steps to Integration

1. Employees can create events in the system using `/egov-user-event/v1/events/_create` endpoint
2. Employees can update events in the system using `/egov-user-event/v1/events/_update` endpoint
3. Events are searched in the system using `/egov-user-event/v1/events/_search` endpoint
4. `/egov-user-event/v1/events/notifications/_count` API is used to fetch the count of the total unread and read notifications.
5. `/egov-user-event/v1/events/lat/_update` API is used to update the last-login-time of the user. We store the last-login-time of the user through this API thereby deciding which notifications have been read.

## Reference Docs <a href="#reference-docs" id="reference-docs"></a>

#### Doc Links <a href="#doc-links" id="doc-links"></a>

| **Title**                 | **Link**                                                                                                                                                           |
| ------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| API Swagger Documentation | [Swagger Documentation](https://editor.swagger.io/?url=https://raw.githubusercontent.com/egovernments/DIGIT-OSS/master/municipal-services/docs/user-events.yml#!/) |

#### API List <a href="#api-list" id="api-list"></a>



| <h4 id="title"><strong>Title</strong> </h4>      | **Link**                                                                                                                   |
| ------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------- |
|  _/egov-user-event/v1/events/\_create_           | [https://www.getpostman.com/collections/14812d58dff5565bd3d9](https://www.getpostman.com/collections/14812d58dff5565bd3d9) |
| _/egov-user-event/v1/events/\_update_            | [https://www.getpostman.com/collections/14812d58dff5565bd3d9](https://www.getpostman.com/collections/14812d58dff5565bd3d9) |
| _/egov-user-event/v1/events/\_search_            | [https://www.getpostman.com/collections/14812d58dff5565bd3d9](https://www.getpostman.com/collections/14812d58dff5565bd3d9) |
| /egov-user-event/v1/events/notifications/\_count | [https://www.getpostman.com/collections/14812d58dff5565bd3d9](https://www.getpostman.com/collections/14812d58dff5565bd3d9) |
| /egov-user-event/v1/events/lat/\_update          | [https://www.getpostman.com/collections/14812d58dff5565bd3d9](https://www.getpostman.com/collections/14812d58dff5565bd3d9) |

_(Note: All the APIs are in the same postman collection therefore the same link is added in each row)_

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in/) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
