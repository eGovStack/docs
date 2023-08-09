# TL Service Configuration

## Overview <a href="#overview" id="overview"></a>

This service is used to issue a license to the user after verification. The service is designed in such a way that it can be used to serve different type of licenses. Currently used to issue trade licenses, perform stakeholder registration and issue lockdown pass. The service is integrated with workflow where we can define the steps for approval of the application. Once the application is approved the license is generated.

## Pre-requisites <a href="#pre-requisites" id="pre-requisites"></a>

Before you proceed with the documentation, make sure the following pre-requisites are met -

* Java 8
* Kafka server is up and running
* egov-persister service is running and has tl-services persister config path added in it
* PSQL server is running  and database is created

## Key Functionalities <a href="#key-functionalities" id="key-functionalities"></a>

* Used for license generations in trade licenses, stakeholder registration and issue lockdown pass
* Define roles to applicants on successful application to access Building Plan Approval services at the time of stakeholder registration
* Generate application number and license number
* Support workflows
* Provide notification on various status changes for an application

## Interaction Diagram <a href="#interaction-diagram" id="interaction-diagram"></a>

![](<../../.gitbook/assets/image (101) (2).png>)

## Deployment Details <a href="#deployment-details" id="deployment-details"></a>

1. Add MDMS configs required for Trade License and BPA stakeholder registration and restart MDMS service
2. Deploy the latest version of tl-services service
3. Add tl-service persister yaml path in persister configuration and restart persister service
4. Add Role-Action mapping for API’s
5. Create businessService (workflow configuration) according to trade license and stakeholder registration
6. Add tl-service indexer yaml path in indexer service configuration and restart indexer service

## Configuration Details <a href="#configuration-details" id="configuration-details"></a>

Following application properties in the Trade License service are configurable.

| Property                                     | Value                                                                                                                                 | Remarks                                                      |
| -------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------ |
| egov.idgen.tl.applicationNum.format          | PB-TL-\[cy:yyyy-MM-dd]-\[SEQ\_EG\_TL\_APL]                                                                                            | The format of the TL application number                      |
| egov.idgen.tl.licensenumber.format           | PB-TL-\[cy:yyyy-MM-dd]-\[SEQ\_EG\_PT\_LN]                                                                                             | The format of the TL license number                          |
| egov.idgen.bpa.applicationNum.format         | PB-SK-\[cy:yyyy-MM-dd]-\[SEQ\_EG\_TL\_APL]                                                                                            | The format of the Stake holder application number            |
| egov.idgen.bpa.licensenumber.format          | PB-SK-\[cy:yyyy-MM-dd]-\[SEQ\_EG\_PT\_LN]                                                                                             | The format of the Stake holder license number                |
| egov.tl.max.limit                            | 100                                                                                                                                   | Max number of records to be returned                         |
| citizen.allowed.search.params                | tenantId, applicationNumber, limit, offset, licenseNumbers                                                                            | The search parameters on which citizen can search            |
| employee.allowed.search.params               | tenantId, applicationNumber, applicationType, status, mobileNumber, fromDate, toDate, licenseNumbers, oldLicenseNumber, limit, offset | The search parameters on which employee can search           |
| persister.save.tradelicense.topic            | save-tl-tradelicense                                                                                                                  | The name of kafka topic on which create request is published |
| persister.update.tradelicense.topic          | update-tl-tradelicense                                                                                                                | The name of kafka topic on which update request is published |
| persister.update.tradelicense.workflow.topic | update-tl-workflow                                                                                                                    | The name of kafka topic on which update request is published |

## Integration <a href="#integration" id="integration"></a>

### Integration Scope <a href="#integration-scope" id="integration-scope"></a>

The trade-license service is currently used to issue trade licenses, perform stakeholder registration and issue lockdown pass.

### Integration Benefits <a href="#integration-benefits" id="integration-benefits"></a>

* Provide backend support for the different license registration process.
* Mseva and SMS notifications on application status changes.
* The elastic search index for creating visualizations and Dashboards.
* Bpa Stakeholder registration provides new roles to the user to access the Building Plan Approval system.
* Supports workflow which is configurable

### Steps to Integration <a href="#steps-to-integration" id="steps-to-integration"></a>

1. To integrate, host of tl-services service should be overwritten in the helm chart.
2. {servicename}/\_create/ \_create should be added as the create endpoint for creating any license in the system
3. {servicename}/\_search/ \_search should be added as the search endpoint. This method handles all requests to search existing records depending on different search criteria
4. {servicename}/\_update/ \_update should be added as the update endpoint. This method is used to update fields in existing records or to update the status of the application based on workflow.

## Reference Docs <a href="#reference-docs" id="reference-docs"></a>

### Doc Links <a href="#doc-links" id="doc-links"></a>

{% file src="../../.gitbook/assets/billing-slabs (1).pdf" %}

{% file src="../../.gitbook/assets/encryption-service (2).pdf" %}

{% file src="../../.gitbook/assets/bpa_stakeholder_registration-3-1- (1).yaml" %}
API Swagger Documentation
{% endfile %}

{% file src="../../.gitbook/assets/bpa-stakeholder-registration-release-doc (1).pdf" %}

| **Title**                                 | **Link**                                                                                                                             |
| ----------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| Local Setup                               | [LOCALSETUP.md](https://github.com/egovernments/core-services/blob/4a74fd3be04ab0a2fe0641f10b57b7e9b9f82aff/egov-user/LOCALSETUP.md) |
| API Swagger Documentation (Trade License) | [Swagger Documentation TL](https://raw.githubusercontent.com/egovernments/egov-services/master/docs/common/contracts/v1-0-0.yml)     |

### API List <a href="#api-list" id="api-list"></a>

In all below endpoints if the service name is BPAREG it is treated as a stakeholder registration application and if it is TL or if it is absent then the application is treated as trade license application.

Stakeholder registration APIs:- [https://www.getpostman.com/collections/d18b79ccfb69ee8bb526](https://www.getpostman.com/collections/d18b79ccfb69ee8bb526)

Trade-License APIs:- [https://www.getpostman.com/collections/99f98723c45f97024831](https://www.getpostman.com/collections/99f98723c45f97024831)

| API                                       | Description                                                                                                                                                                                                                                                                            |
| ----------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| {servicename}/\_create, \_create          | This API is used to create an application for the license in the system. Whenever an application is created an application number is generated and assigned to the application for future reference.                                                                                   |
| {servicename}/\_search, /\_search         | This API is used to search the applications in the system based on various search parameters like mobile number, the application number, status etc.                                                                                                                                   |
| {servicename}/\_update, \_update          | <p>The _update API is used to update the application information or to forward the application from one state to another.</p><p>In the case of the stakeholder registration if the application reaches the last stage the role depending on the license type is given to the user.</p> |
| {servicename}/{jobname}/\_batch, /\_batch | Searches trade licenses which are expiring and send a reminder SMS to owner's of the licenses                                                                                                                                                                                          |

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation ](https://egov.org.in/)is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).
