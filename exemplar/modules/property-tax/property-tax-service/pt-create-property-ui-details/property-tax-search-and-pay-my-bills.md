---
description: Bill details and payer details
---

# Property Tax - Search And Pay My Bills

**Objective:** The Search and Pay feature enables the user to search the property (with or without login) and pay any pending dues. It provides the user with the option to load all the bills linked to the registered mobile number and pay the bill.

## **Search Property**

Users can search for Property with or without login. Property can be searched either using Property Id or using property details.

![](<../../../../../.gitbook/assets/Screenshot from 2022-03-03 10-39-23.png>) ![](<../../../../../.gitbook/assets/Screenshot from 2022-03-03 10-43-26.png>)

Once the user provides certain parameters it calls the search property API and displays the search results accordingly.

![](<../../../../../.gitbook/assets/Screenshot from 2022-03-03 10-46-08.png>)

Clicking on the View Details button redirects the user to the bill details page. The users can pay the dues from this page.

![](<../../../../../.gitbook/assets/Screenshot from 2022-03-03 10-50-21.png>)

Users can view the break-up of the total amount due and select full or partial payment as required. They can enter the amount to be paid in case the partial payment option is selected.&#x20;

Clicking on the Proceed To Pay **** button redirects the users to the Payer’s Details page.

* For _Logged In Users_, the below information is captured.
  1. &#x20;I am making the payment as the owner/ consumer of the service.
  2. &#x20;I am making the payment on the behalf of the owner/ consumer of the service.
     * In case of option (i) is selected, the owner’s detail is linked with the receipt.
     * In case option (ii) is selected, the user’s profile detail is linked with the receipt.
* For _without login users_, the below information is captured.
  1. &#x20;I am making the payment as the owner/ consumer of the service.
  2. &#x20;I am making the payment on the behalf of the owner/ consumer of the service.
     * In case of option (i) is selected, the owner’s detail is linked with the receipt.
     * In case option (ii) is selected, the user is asked to enter the Name and Mobile No. and the same is linked with the receipt.

![](<../../../../../.gitbook/assets/Screenshot from 2022-03-03 12-39-51.png>)

Based on the selected option the user is redirected to the total amount page. The flow is same as DIGIT Payments from this screen.

## **Technical Implementation**

File link for the code for payer details: [![](https://github.githubassets.com/favicon.ico)https://github.com/egovernments/DIGIT-Dev/tree/develop/frontend/micro-ui/web/micro-ui-internals/packages/modules/common/src/payments/citizen/payers-details - Connect to preview](https://github.com/egovernments/DIGIT-Dev/tree/develop/frontend/micro-ui/web/micro-ui-internals/packages/modules/common/src/payments/citizen/payers-details)

The payer information for the payments API is added based on the mentioned criteria.

## &#x20;**Role Action Mapping**

| **API**                                   | **Action id** | **Roles**           |
| ----------------------------------------- | ------------- | ------------------- |
| `/access/v1/actions/mdms/_get`            | `870`         | `CITIZEN`           |
| `/egov-mdms-service/v1/_search`           | `954`         | `CITIZEN`           |
| `/localization/messages/v1/_search`       | `1531`        | `CITIZEN`           |
| `/billing-service/bill/v2/_fetchbill`     | `1862`        | `CITIZEN`,          |
| `/pg-service/transaction/v1/_create`      | `1571`        | `CITIZEN`           |
| `/collection-services/payments/_search`   | `1864`        | `CITIZEN`           |
| `/pg-service/transaction/v1/_update`      | `1572`        | `CITIZEN`           |
| `collection-services/payments/PT/_search` | `2029`        | `PTCEMP,` `CITIZEN` |

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation ](https://egov.org.in/)is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).
