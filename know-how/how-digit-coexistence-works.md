# How DIGIT coexistence works

## Overview <a id="overview"></a>

![](https://digit-discuss.atlassian.net/wiki/download/thumbnails/28770500/coexistence%20HLD%20%283%29.jpeg?version=1&modificationDate=1557827003484&cacheVersion=1&api=v2&width=663&height=400)

## Technical details <a id="technical-details"></a>

This section will list some of the technical details of how each of the hooks is implemented in this coexistence framework.

### Where does the user data reside? <a id="where-does-the-user-data-reside"></a>

All user data, be it citizen or employee will reside in the Rainmaker product. This data will be called from other systems \(ERP finance or third-party system\) for authentication purpose.

### How does the login work? <a id="how-does-the-login-work"></a>

Login will always happen from the Rainmaker system, where a user will enter the username and password and select the city name. The system will generate an auth token after the authentication is successful. This auth token is stored in the local storage.

When any ERP menu tree links are accessed, the system will get this auth token from the local storage and pass it to ERP using a POST call using the hidden variable in the body. This auth token is stored in a hashmap in the Redis server along with the user id. When a second URL from ERP is accessed, the system will check if the auth- token coming as part of the request is the same as that of the auth-token available in the Redis server. If it is the same then the system allows proceeding with the transaction.

### How does logout happen? <a id="how-does-logout-happen"></a>

Log out option will be available only from the Rainmaker. Rainmaker makes a callback handler call, which is implemented by the ERP when logout is initiated. At this event, the auth-token stored in the Redis server by the ERP will be invalidated.

The same strategy will apply when an auth-token refresh happens. Both system to be configured with the same value for session timeout so that session expiry will be in sync.

### How does a single schema system and multi-schema system coexist? <a id="how-does-a-single-schema-system-and-multi-schema-system-coexist"></a>

Rainmaker is a single schema multi-tenant application which has a single login URL for all the tenants. At the time of login, the user will input the tenant reference along with the user credentials. This tenant will be used to frame the sub-domain URL for the ERP system. When a menu tree URL is accessed, the system will generate a dynamic URL which is recognizable by the ERP, based on the tenant available in the session.

Menu tree will be loaded in Rainmaker for all the application irrespective of the fact that the application resides in rainmaker or in ERP. Role action mapping data will be loaded in JSON format into MDMS for this. As of now only the navigation ULRs and REST URLs are added in the action list for access control. Any URLs that are accessed internally within the application does not go through access control.

### How do the items load in the inbox? <a id="how-do-the-items-load-in-the-inbox"></a>

Login to the application is through rainmaker and hence the inbox also should be available in the same. There are two ways of implementing this- 1\) show the ERP workflow items as a separate list 2\) Show the ERP workflow items along with the other Rainmaker workflow items.

The best approach is to have an inbox hook in Rainmaker where all module workflow items are listed in order. This will also contain items from ERP finance like, approve a payment, approve budget etc. along with Trade license. ERP system will expose a REST API to the rainmaker, this API will be called when rendering the inbox.

Currently, we have implemented the first approach, wherein the ERP items are shown as a separate list on click on the respective card.

### How are core services used in coexistence framework? <a id="how-are-core-services-used-in-coexistence-framework"></a>

Core services like user, employee, mdms, department, designation, user authentication etc are part of the Rainmaker product. ERP application will make a REST call to the Rainmaker to get information related to these services. Authentication will be done based on the logged in user credentials.

### How is the data managed in both the systems? <a id="how-is-the-data-managed-in-both-the-systems"></a>

There will be a single source of truth which means the data will be either available with the rainmaker database or with the ERP database and not in both places. Depending on where the source module is located \(owned\), the data will also be in the same location. There will not be any data syncing between the two systems.

### How does other system interact with ERP system? <a id="how-does-other-system-interact-with-erp-system"></a>

Rainmaker and **Water & Sewerage** standalone system will create vouchers in the ERP Finance system using the REST API. Rainmaker will access all finance master data from ERP Finance through REST calls whereas Water & Sewerage system will have the specific finance master data within the water system itself. The interaction of finance and water module are mainly two-fold.

* **Getting master data for receipt and remittance**
* **Voucher creation.**

Collection module will make REST calls to finance ERP for all master data and voucher creation.There are standard system integrator roles and users created for integrating finance and water system to Rainmaker. System integrator role will be mapped with all the permissible actions.

