# XState Core Chatbot

## Overview

Goal: To onboard developers onto the XState-Chatbot code base so that they can modify existing flows or create new ones.

This document sticks to explaining the chatbot's core features and does not dive into the use cases implemented by the chatbot.&#x20;

### Chatbot Fundamentals

This chatbot solves the basic form-filling aspect of a chat flow. By collecting the information from the user, an API call is made to the rainmaker backend services to fulfil the user requirements. It uses the concept of [StateCharts](https://statecharts.github.io/) (similar to State Machines) to maintain the state of the user in a chat flow and store the information provided by the user. [XState](https://xstate.js.org/docs/) is a JavaScript implementation of StateCharts. All chat flows are coded inside the XState framework.

This chatbot does not have any Natural Language Processing component. In the future, we can extend the chatbot to add such features.

### Basic Introduction to XState

XState is a JavaScript implementation of StateCharts. There is detailed documentation available to study XState. Some concepts of XState used in the Chatbot are listed below. Basic knowledge of these concepts is necessary. It can also be learned while going through the chat flow implementation of pilot use cases in PGR and Bills.

1. [State](https://xstate.js.org/docs/guides/states.html)
   * [State Nodes](https://xstate.js.org/docs/guides/statenodes.html)
   * [Hierarchical State Nodes](https://xstate.js.org/docs/guides/hierarchical.html)
2. Actions
   * onEntry
   * [invoke…onDone…onError](https://xstate.js.org/docs/guides/communication.html#the-invoke-property)
3. [Guard Conditions](https://xstate.js.org/docs/guides/guards.html#guards-condition-functions)

Few tips about using XState. These have been followed throughout the pilot chat flows.

1. To move to any state which is not at the same hierarchical level, assign a unique ID value. If it has an ID value, address it using the # qualifier in the target attribute.
2. Since the ID should be unique, make sure there are no multiple states having the same ID value. If there is a duplicate, the application will not function as expected.
3. Any actions (like onEntry) should be surrounded by assign.

```
assign( (context, event) => { ... } )
```

This includes almost all functions except the guard condition code snippets.

## Pre-requisites

* NodeJS
* [XState](https://xstate.js.org/docs/)
* PostgreSQL
* Kafka\_(optional)\_

## Key Functionalities

* Build a chat flow to facilitate a user to interact with rainmaker modules
* Link a chat flow with backend services

## Deployment Details

1. Deploy the latest version of xstate-chatbot
2. Configure /xstate-chatbot to be a whitelisted open endpoint in zuul
3. Add [indexer-config](https://github.com/egovernments/configs/blob/DEV/egov-indexer/chatbot-telemetry-v2.yaml) to the egov-indexer to index all the telemetry messages

| Environmental Variables | Description                                                                                                                                                                                                                                                                                           |
| ----------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `WHATSAPP_PROVIDER`     | <p>The provider through which WhatsApp messages are sent &#x26; received. An adapter for ValueFirst is written. If there is any new provider a separate adapter will have to be implemented.</p><p>A default <code>console</code> adapter is provided for developers to test the chatbot locally.</p> |
| `REPO_PROVIDER`         | <p>The database used to store the chat state. Currently, an adapter for PostgreSQL is provided.</p><p>An <code>InMemory</code> adapter is provided to test the chatbot locally</p>                                                                                                                    |
| `SERVICE_PROVIDER`      | <p>If it’s value is configured to be eGov, it will call the backend rainmaker services. If the value is configured as Dummy, dummy data would be used rather than fetching data from APIs.</p><p>Dummy option is provided for initial dialog development, and is only to be used locally.</p>         |
| `SUPPORTED_LOCALES`     | A list of comma-separated locales supported by the chatbot.                                                                                                                                                                                                                                           |

Other configuration details are mentioned in the [XState-Chatbot Integration Document](https://digit-discuss.atlassian.net/l/c/gg4EmH3k).

## Chat Flow&#x20;

All the interactions with the user - sending a message to the user and processing an incoming message from the user are coded as a state in the State Machine. It would be a nice start to test any chat flow with the supplementary react-app provided for the developers to execute the state machine locally. (Please follow the guidelines in the README of the react-app.)

We have applied some standard patterns to code any chat interaction. Please try to follow these patterns to code any new chat flow. These patterns are explained below. You can also study those by browsing through the code of the pilot use cases of PGR and Bills.

1. The chat states would only include dialogue-specific code. Any code related to the backend service should be written as a part of a separate …-service.js file.
2. Any code that does not include any asynchronous API call can be written as a part of the onEntry function or action.
3. If the function needs to make an API call, that would have to be written with the invoke-on Done pattern. The asynchronous function should be written as a part of the service file. The consolidated data returned by it can be processed in the state of the dialogue file.
4. Helper functions are written in`dialog.js`file. It is advised to use those functions as much as possible rather than writing any custom logic in dialogue files.

## Scaffolding

Apart from the chat flow and its backend service API calls, a few other components are present in the project. These components do NOT need to be modified to code any new chat flow or changed for an existing chat flow. These components with a short description for each are listed below:

1. **Session Manager:** It manages the sessions of all the users on a server. It will store the user’s state in a datastore, update it, and read it when any new message is received on the server. Based on the state of the user, it creates a state machine and sends the incoming message event to the state machine. It sanctifies the state (any sensitive data like the name and mobile number of a user are removed) before storing the state in the datastore.
2. **Repository:** It is the datastore where the states of the users get stored. To reduce dependency, an in-memory repository is also provided, which can be used by configuring an environment variable. So to run the chatbot service, PostgreSQL isn’t a hard dependency, but it is advisable to use the PostgreSQL repo provider.
3. **Channel Provider:** There can be many different WhatsApp Providers. Any one of the providers will be configured to be used. A separate `console` WhatsApp Provider is present for the developer to test the chatbot server locally. Postman collection to mimic receiving messages from a user to the server is present in the project directory.
4. **Localization:** Every message to be sent to the user is stored within the chatbot. Localization service is not being used. These messages are present near the bottom of the dialogue files. A separate localization-service.js is provided to get the messages for the localization codes for the messages that are not owned by the chatbot. For example, the PGR complaint types data is under the ownership of the PGR module, and the messages for such can be fetched from the egov-localization-service using the functions provided in the localization-service.js.
5. **Service Provider:** To ease the initial dialogue development, instead of coding API calls to the backend services, we can configure the chat flow to use a dummy service. This can be configured using an environment variable and modifying the `service-loader.js` file.
6.  **Telemetry:** Chatbot logs telemetry events to a Kafka topic. (Any sensitive data will get masked before indexing the events onto ElasticSearch by egov-indexer.) The following events get logged:

    1. Incoming message
    2. Outgoing message
    3. Transition of state



[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)_​_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in/) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
