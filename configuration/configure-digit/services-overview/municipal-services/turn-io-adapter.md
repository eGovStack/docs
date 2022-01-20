# Turn-Io-Adapter

## **Transform API**

### **Objective**

Reap benefit system is one of the vendors that provide the chatbot services using the[ ![](https://images.squarespace-cdn.com/content/v1/5eb455d61e1add207522fffc/1591612739969-PES60R7VHOQ9YRQDXBA8/favicon.ico?format=100w)turn](http://turn.io) as backend services to communicate with citizen through chatbot. As part of the requirement, we need to create a complaint in digit platform when ever citizen has raised the complaint through reap benefit chatbot.

## Overview

turn-io-adapter service is a wrapper to transform reap benfit request format to digit pgr request format. this service will have \_transform api and it will construct requried pgr request from the request message sent by reap benfit system. Reap benfit system will consume \_tranform api to communicate with digit pgr mdoule.

In this process, once a complaint is created it sends a Whatsapp message to the citizen with a track link. Whenever some action taken by ULB employes on complaint, we will send whatsapp message to citizen.

## Pre-requisites

Before you proceed with the configuration, make sure the following pre-requisites are met -

* _Java 8_
* Rainmaker-PGR service is running

## Key Functionalities

* Complaint can create in digit platform from reapbenfit system chatbot
* message will sent to citizen through whatsapp when employee perform some action on complaint

## Deployment Details

Please deploy the following builds

* **rainmaker-pgr-db:v1.1.3-bb2961cf-13**
* **turn-io-adapter:v1.1.3-bb2961cf-19**
* **egov-searcher:v1.1.3-d43c421c-5**
* **nlp-engine:v1.0.0-c3889d14-10**

**Note:** Please refer to the following url for nlp-engine techical documentation.

[NLP Engine Service](../core-services/nlp-engine-service.md)

**Frontend commits**

[![](https://github.com/fluidicon.png)RAIN-2852 : PGR complaint details to show the complaint category issu… · egovernments/frontend@b7aa519](https://github.com/egovernments/frontend/commit/b7aa5196eb4d15cc5d76268d76a5a8a82adb15c7)

[![](https://github.com/fluidicon.png)RAIN2851 : Citizen Otp screen fix to get previous logged session · egovernments/frontend@da2da15](https://github.com/egovernments/frontend/commit/da2da150d8a9bd04143ab4d48546adbdcb95ed93)

## Infra Configuration Details

1\) turn-io-adapter: "[http://turn-io-adapter.egov:8080/](http://turn-io-adapter.egov:8080)" (In service host configuration)

`2) Add /turn-io-adapter/_transform in egov-mixed-mode-endpoints-whitelist configuration`

3\) Once you are done with 2nd step restart zuul pod

### **MDMS Data**

We need to add name filed in complaint category master in pgr. Please find the below link for data.

[https://raw.githubusercontent.com/egovernments/egov-mdms-data/DEV/data/pb/RAINMAKER-PGR/ServiceDefs.json](https://raw.githubusercontent.com/egovernments/egov-mdms-data/DEV/data/pb/RAINMAKER-PGR/ServiceDefs.json)

### **LOCALIZATION DATA**

Push the localization data for all the locality data with module as rainmaker-chatbot. Please find the below sample localization object.

**{ "code": "SC1", "message": "Azad Nagar - WARD\_1", "module": "rainmaker-chatbot", "locale": "en\_IN" }**

## Business Service / Workflow Configuration

NA

## Actions & Role Action Mapping

### **Actions**

```
{
      "id": 2116,
      "name": "Create Turn Io Adapter",
      "url": "/turn-io-adapter/_transform",
      "displayName": "Turn Io Adapter",
      "orderNumber": 1,
      "enabled": true,
      "serviceCode": "turn-io-adapter",
      "code": "null",
      "path": ""
    }
```

### **Role Mapping**

```
{
      "code": "ANONYMOUS",
      "name": "Any User",
      "description": "Can Transform the Data"
    }
```

### **RoleAction Mapping**

```
{
     "rolecode":"ANONYMOUS",
     "actionid":2116,
     "actioncode":"",
     "tenantId":"pb"
  }
```

### Data Setup

This is the samplerequest for \_transform api to create a complaint

```
curl --location --request POST 'https://dev.digit.org/turn-io-adapter/_transform' \
--header 'Content-Type: application/json' \
--data-raw '{
    "contacts": [
        {
            "profile": {
                "name": "Rohit"
            },
            "wa_id": "9199999999992"
        }
    ],
    "messages": [
        {
            "_vnd": {
                "v1": {
                    "author": {
                        "id": "917391904467",
                        "name": "The_Subtle_Guy",
                        "type": "OWNER"
                    },
                    "chat": {
                        "assigned_to": null,
                        "owner": "+917391904467",
                        "permalink": "https://app.turn.io/c/ac1ad367-1631-41b8-a29c-024ed19c1547",
                        "state": "OPEN",
                        "state_reason": "Re-opened by inbound message.",
                        "unread_count": 21,
                        "uuid": "ac1ad367-1631-41b8-a29c-024ed19c1547"
                    },
                    "direction": "inbound",
                    "faq_uuid": null,
                    "in_reply_to": null,
                    "inserted_at": "2021-05-19T19:21:33.809218Z",
                    "labels": [],
                    "rendered_content": null
                }
            },
            "from": "917391904467",
            "id": "ABEGkXORkERnAhBOXKjR8Jyyk-Iar8Gd2yeo",
            "text": {
                "body": "4"
            },
            "timestamp": "1621452093",
            "type": "text"
        },
        {
            "_vnd": {
                "v1": {
                    "author": {
                        "id": "fc89d3d7-bcab-4734-a82f-bf06fa99a980",
                        "name": "Complaint Selection",
                        "type": "THREAD"
                    },
                    "chat": {
                        "assigned_to": null,
                        "owner": "+917391904467",
                        "permalink": "https://app.turn.io/c/ac1ad367-1631-41b8-a29c-024ed19c1547",
                        "state": "OPEN",
                        "state_reason": "Re-opened by inbound message.",
                        "unread_count": 21,
                        "uuid": "ac1ad367-1631-41b8-a29c-024ed19c1547"
                    },
                    "direction": "outbound",
                    "faq_uuid": null,
                    "in_reply_to": null,
                    "inserted_at": "2021-05-19T19:21:35.313898Z",
                    "labels": [],
                    "rendered_content": null
                }
            },
            "from": "15550152059",
            "id": "gBEGkXORkERnAglCxuTiC7G_ERg",
            "preview_url": false,
            "recipient_type": "individual",
            "text": {
                "body": "Please provide landmark or additional details of your locality.\\nOtherwise type and send *No*"
            },
            "timestamp": "1621452095",
            "to": "917391904467",
            "type": "text"
        },
        {
            "_vnd": {
                "v1": {
                    "author": {
                        "id": "917391904467",
                        "name": "The_Subtle_Guy",
                        "type": "OWNER"
                    },
                    "chat": {
                        "assigned_to": null,
                        "owner": "+917391904467",
                        "permalink": "https://app.turn.io/c/ac1ad367-1631-41b8-a29c-024ed19c1547",
                        "state": "OPEN",
                        "state_reason": "Re-opened by inbound message.",
                        "unread_count": 21,
                        "uuid": "ac1ad367-1631-41b8-a29c-024ed19c1547"
                    },
                    "direction": "inbound",
                    "faq_uuid": null,
                    "in_reply_to": null,
                    "inserted_at": "2021-05-19T19:21:40.701184Z",
                    "labels": [
                        {
                            "confidence": 0.3339659565,
                            "metadata": {
                                "nlu": {
                                    "confidence": 0.3339659565,
                                    "intent": "await_reply",
                                    "model_name": "nlu-general-spacy-ngrams-20191014"
                                }
                            },
                            "uuid": "df376fa2-9358-4088-a6d0-8f3db031158b",
                            "value": "Unclassified"
                        }
                    ],
                    "rendered_content": null
                }
            },
            "from": "917391904467",
            "id": "ABEGkXORkERnAhBgzXDW_hlyiVg_IS6NxTMH",
            "text": {
                "body": "No"
            },
            "timestamp": "1621452100",
            "type": "text"
        },
        {
            "_vnd": {
                "v1": {
                    "author": {
                        "id": "fc89d3d7-bcab-4734-a82f-bf06fa99a980",
                        "name": "Complaint Selection",
                        "type": "THREAD"
                    },
                    "chat": {
                        "assigned_to": null,
                        "owner": "+917391904467",
                        "permalink": "https://app.turn.io/c/ac1ad367-1631-41b8-a29c-024ed19c1547",
                        "state": "OPEN",
                        "state_reason": "Re-opened by inbound message.",
                        "unread_count": 21,
                        "uuid": "ac1ad367-1631-41b8-a29c-024ed19c1547"
                    },
                    "direction": "outbound",
                    "faq_uuid": null,
                    "in_reply_to": null,
                    "inserted_at": "2021-05-19T19:21:41.297301Z",
                    "labels": [],
                    "rendered_content": null
                }
            },
            "from": "15550152059",
            "id": "gBEGkXORkERnAgnMDgDG2-YCOv0",
            "preview_url": false,
            "recipient_type": "individual",
            "text": {
                "body": "Please enter the category of your issue from the options given below.\\n\\n1. Garbage\\n2. Street Lights\\n3. Water and Sewerage\\n4. Roads And Footpaths\\n5. Public Toilets\\n6. Land Violations\\n7. Animals and Insect"
            },
            "timestamp": "1621452101",
            "to": "917391904467",
            "type": "text"
        },
        {
            "_vnd": {
                "v1": {
                    "author": {
                        "id": "917391904467",
                        "name": "The_Subtle_Guy",
                        "type": "OWNER"
                    },
                    "chat": {
                        "assigned_to": null,
                        "owner": "+917391904467",
                        "permalink": "https://app.turn.io/c/ac1ad367-1631-41b8-a29c-024ed19c1547",
                        "state": "OPEN",
                        "state_reason": "Re-opened by inbound message.",
                        "unread_count": 21,
                        "uuid": "ac1ad367-1631-41b8-a29c-024ed19c1547"
                    },
                    "direction": "inbound",
                    "faq_uuid": null,
                    "in_reply_to": null,
                    "inserted_at": "2021-05-19T19:21:44.672489Z",
                    "labels": [],
                    "rendered_content": null
                }
            },
            "from": "917391904467",
            "id": "ABEGkXORkERnAhARhnoBHV4O_DOlR9CNENoq",
            "text": {
                "body": "1"
            },
            "timestamp": "1621452104",
            "type": "text"
        },
        {
            "_vnd": {
                "v1": {
                    "author": {
                        "id": "fc89d3d7-bcab-4734-a82f-bf06fa99a980",
                        "name": "Complaint Selection",
                        "type": "THREAD"
                    },
                    "chat": {
                        "assigned_to": null,
                        "owner": "+917391904467",
                        "permalink": "https://app.turn.io/c/ac1ad367-1631-41b8-a29c-024ed19c1547",
                        "state": "OPEN",
                        "state_reason": "Re-opened by inbound message.",
                        "unread_count": 21,
                        "uuid": "ac1ad367-1631-41b8-a29c-024ed19c1547"
                    },
                    "direction": "outbound",
                    "faq_uuid": null,
                    "in_reply_to": null,
                    "inserted_at": "2021-05-19T19:21:46.759132Z",
                    "labels": [],
                    "rendered_content": null
                }
            },
            "from": "15550152059",
            "id": "gBEGkXORkERnAgnskmr3neFP1ec",
            "preview_url": false,
            "recipient_type": "individual",
            "text": {
                "body": "Pick a issue from the options given below which describes closest to what you are facing.\\n\\n1. Garbage Needs To be Cleared\\n2. Damaged Garbage Bin\\n3. Burning Of Garbage"
            },
            "timestamp": "1621452106",
            "to": "917391904467",
            "type": "text"
        },
        {
            "_vnd": {
                "v1": {
                    "author": {
                        "id": "917391904467",
                        "name": "The_Subtle_Guy",
                        "type": "OWNER"
                    },
                    "chat": {
                        "assigned_to": null,
                        "owner": "+917391904467",
                        "permalink": "https://app.turn.io/c/ac1ad367-1631-41b8-a29c-024ed19c1547",
                        "state": "OPEN",
                        "state_reason": "Re-opened by inbound message.",
                        "unread_count": 21,
                        "uuid": "ac1ad367-1631-41b8-a29c-024ed19c1547"
                    },
                    "direction": "inbound",
                    "faq_uuid": null,
                    "in_reply_to": null,
                    "inserted_at": "2021-05-19T19:21:51.967923Z",
                    "labels": [],
                    "rendered_content": null
                }
            },
            "from": "917391904467",
            "id": "ABEGkXORkERnAhBhofKX9wPf4-6xzUNnNJ5x",
            "text": {
                "body": "2"
            },
            "timestamp": "1621452111",
            "type": "text"
        },
        {
            "_vnd": {
                "v1": {
                    "author": {
                        "id": "fc89d3d7-bcab-4734-a82f-bf06fa99a980",
                        "name": "Complaint Selection",
                        "type": "THREAD"
                    },
                    "chat": {
                        "assigned_to": null,
                        "owner": "+917391904467",
                        "permalink": "https://app.turn.io/c/ac1ad367-1631-41b8-a29c-024ed19c1547",
                        "state": "OPEN",
                        "state_reason": "Re-opened by inbound message.",
                        "unread_count": 21,
                        "uuid": "ac1ad367-1631-41b8-a29c-024ed19c1547"
                    },
                    "direction": "outbound",
                    "faq_uuid": null,
                    "in_reply_to": null,
                    "inserted_at": "2021-05-19T19:21:53.336395Z",
                    "labels": [],
                    "rendered_content": null
                }
            },
            "from": "15550152059",
            "id": "gBEGkXORkERnAglgp1wnhrkeJb0",
            "preview_url": false,
            "recipient_type": "individual",
            "text": {
                "body": "Please select from below option\\n\\n1. To submit complaint details\\n2. To re-enter the complaint details"
            },
            "timestamp": "1621452113",
            "to": "917391904467",
            "type": "text"
        },
        {
            "_vnd": {
                "v1": {
                    "author": {
                        "id": "917391904467",
                        "name": "The_Subtle_Guy",
                        "type": "OWNER"
                    },
                    "chat": {
                        "assigned_to": null,
                        "owner": "+917391904467",
                        "permalink": "https://app.turn.io/c/ac1ad367-1631-41b8-a29c-024ed19c1547",
                        "state": "OPEN",
                        "state_reason": "Re-opened by inbound message.",
                        "unread_count": 21,
                        "uuid": "ac1ad367-1631-41b8-a29c-024ed19c1547"
                    },
                    "direction": "inbound",
                    "faq_uuid": null,
                    "in_reply_to": null,
                    "inserted_at": "2021-05-19T19:21:58.364053Z",
                    "labels": [],
                    "rendered_content": null
                }
            },
            "from": "917391904467",
            "id": "ABEGkXORkERnAhCpESguA5JfsAlvKVTgoD0H",
            "text": {
                "body": "1"
            },
            "timestamp": "1621452118",
            "type": "text"
        }
    ],
    "thread": {
        "contact": {
            "arts": null,
            "birthday": null,
            "city": "pb.amritsar",
            "cityset": true,
            "complaint_category": "Garbage",
            "complaint_image": "No",
            "complaint_sub_category": "Dirty Water Supply",
            "complaintset": false,
            "complaintsetvalue": "To submit complaint details",
            "language": null,
            "locality": "JLC833",
            "localityset": true,
            "location": null,
            "math": null,
            "name": null,
            "opted_in": false,
            "opted_in_at": null,
            "space": null,
            "surname": null,
            "whatsapp_id": "917391904467",
            "whatsapp_profile_name": "Rohit"
        }
    },
    "RequestInfo": {
        "userInfo": {
            "id": 23342,
            "uuid": "f212e8aa-53ba-456f-9013-89fb806dc24b",
            "userName": "7878787878",
            "name": "Aditya",
            "mobileNumber": "7878787878",
            "emailId": "",
            "locale": "en_IN",
            "type": "CITIZEN",
            "roles": [
                {
                    "name": "Citizen",
                    "code": "CITIZEN",
                    "tenantId": "pb"
                }
            ],
            "active": true,
            "tenantId": "pb",
            "permanentCity": "pb.amritsar"
        }
    }
}'
```

## Integration

### Integration Scope

Turn-io-adapter will be integrated with Rainmaker-pgr Application. Turn-io-adapter Application internally invokes the rainmaker-pgr service to generate the complaint.

### Steps to Integration

1. Turn-Io-adapter application to call `turn-io-adapter/_transform` to generate the complaint and takes the data from the pgr.
