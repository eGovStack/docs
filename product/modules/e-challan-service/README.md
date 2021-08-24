# e-Challan Service

## Overview

<<<<<<< HEAD
=======
  
>>>>>>> 64dca8adbdf64336b1a8203199b3791fa23434fa
eChallan system enables employees to generate the challans for Adhoc services so that the payment can be recorded into the system along with service-specific details.

It also enables citizens to make payments online based on challan no.

## Pre-requisites

Before you proceed with the documentation, make sure the following pre-requisites are met -

* _Java 8_
* Kafka server is up and running
* egov-persister service is running and has workflow persister config path added in it
* PSQL server is running and a database is created to store workflow configuration and data

## Key Functionalities

* Allow the employee to capture service details for miscellaneous services and collect payment
* Allow the employee to update / cancel challan.
* Search, download, and print echallan / bill for miscellaneous service
* Generate and view echallan / bill pdf for all miscellaneous and ad-hoc services
* Send SMS and an email bill notification to the citizen with a payment link and bill link

## Interaction Diagram

![](../../../.gitbook/assets/flow.jpg)

![](../../../.gitbook/assets/update-challan.png)

![](../../../.gitbook/assets/cancel-challan.png)

## ![](blob:https://digit-discuss.atlassian.net/3fa80073-753e-4531-afa0-50c26d0ceb53#media-blob-url=true&id=98d6af92-57da-4510-a906-537d4365ec88&collection=contentId-1531740173&contextId=1531740173&mimeType=image%2Fjpeg&name=flow.jpg&size=68936&width=1200&height=750)Deployment Details

1. Add MDMS configs required for eChallan Service and calculator and restart MDMS service
2. Deploy the latest version of eChallan Service and calculator
3. Add eChallan Service persister yaml path in persister configuration and restart persister service
4. Add Role-Action mapping for API’s
5. Add pdf configuration file for challan and bill

### Integration <a id="Integration"></a>

### Integration Scope

The eChallan service is used to generate **e-challans / bill** for all miscellaneous / adhoc services which citizens avail from ULBs.

### Integration Benefits

* Can perform service-specific business logic without impacting the other module.
* Provides the capability of capturing the unique identifier of the entity for which the challan is generated.
* In the future, if we want to expose the application to citizen then it can be done easily.
* Workflow or Service-specific workflow can be enabled at the challan service level at any time without changing the design.
* Allow an employee to update / cancel challan

### Steps to Integration

1. To integrate, host of echallan-services module should be overwritten in helm chart.
2. echallan-services/eChallan/v1/\_create should be added as the create endpoint for creating eChallan in the system
3. echallan-services/eChallan/v1/\_search should be added as the search endpoint. This method handles all requests to search existing records depending on different search criteria
4. echallan-services/eChallan/v1/\_update should be added as the update endpoint. This method is used to update fields in existing records or to update the status of the application based on workflow.

## Reference Docs

#### Doc Links <a id="Doc-Links"></a>

<<<<<<< HEAD
| **Title** | **Link** |
=======
| **Title**  | **Link** |
>>>>>>> 64dca8adbdf64336b1a8203199b3791fa23434fa
| :--- | :--- |
| API Swagger Documentation | [Swagger Documentation](https://editor.swagger.io/?url=https://raw.githubusercontent.com/egovernments/municipal-services/develop/docs/e-Challan-v1.0.0.yaml#!/) |

#### API List <a id="API-List"></a>

| Title | **Link** |
| :--- | :--- |
<<<<<<< HEAD
| _echallan-services/eChallan/v1/\_create_ | [https://www.getpostman.com/collections/349413e52bf743d50b0a](https://www.getpostman.com/collections/349413e52bf743d50b0a) |
| _echallan-services/eChallan/v1/\_update_ | [https://www.getpostman.com/collections/349413e52bf743d50b0a](https://www.getpostman.com/collections/349413e52bf743d50b0a) |
| _echallan-services/eChallan/v1/\_search_ | [https://www.getpostman.com/collections/349413e52bf743d50b0a](https://www.getpostman.com/collections/349413e52bf743d50b0a) |
=======
|  _echallan-services/eChallan/v1/\_create_ | [https://www.getpostman.com/collections/349413e52bf743d50b0a](https://www.getpostman.com/collections/349413e52bf743d50b0a) |
| _echallan-services/eChallan/v1/\_update_ | [https://www.getpostman.com/collections/349413e52bf743d50b0a](https://www.getpostman.com/collections/349413e52bf743d50b0a) |
| _echallan-services/eChallan/v1/\_search_ | [https://www.getpostman.com/collections/349413e52bf743d50b0a](https://www.getpostman.com/collections/349413e52bf743d50b0a) |
|  _echallan-services/eChallan/v1/\_count_ | [https://www.getpostman.com/collections/773565d7b5866f0851e3](https://www.getpostman.com/collections/773565d7b5866f0851e3) |
>>>>>>> 64dca8adbdf64336b1a8203199b3791fa23434fa

_\(Note: All the API’s are in the same postman collection therefore the same link is added in each row\)_

\_\_

\_\_

> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in/) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._

