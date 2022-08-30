# Bill Details UI Flow

## **Objective**

To provide users with the bill details and the options to cancel the bill.

![](<../../../../../.gitbook/assets/image (255).png>)

## **Implementation Details**

The screen development file is available in the egov-abg-dev folder within the below link:

[<img src="https://github.com/fluidicon.png" alt="" data-size="line">frontend/viewBill.js at master · egovernments/frontend](https://github.com/egovernments/frontend/blob/master/web/rainmaker/dev-packages/egov-abg-dev/src/ui-config/screens/specs/bills/viewBill.js)

The details of the Bill is fetched by calling BillingService fetchBill API and the [Consumer.No](http://consumer.no/) is used in the query param.

FetchBill API returns the Bill Object which contains all the details about the bill including Billing Period, Due Amount, Due Date, and information about the Tax, Cess, Rebate, Penalty applied in this bill.

NextStep - On clicking on the next step, the screen navigates to the cancel bill screen. The user must select the option that best states the reason for bill cancellation. More details for the cancel bill screen is available on this page -[ Cancel Bill](cancel-bill-ui-flow.md)

The Next Step button file is available in the file path below: [<img src="https://github.com/fluidicon.png" alt="" data-size="line">frontend/viewBillFooter.js at master · egovernments/frontend](https://github.com/egovernments/frontend/blob/master/web/rainmaker/dev-packages/egov-abg-dev/src/ui-config/screens/specs/bills/viewBillResource/viewBillFooter.js)

![](<../../../../../.gitbook/assets/image (239) (4).png>)

## **API Call Role Action Mapping**

|                                          |               |                       |
| ---------------------------------------- | ------------- | --------------------- |
| **API**                                  | **Action id** | **Roles**             |
| `/ws-calculator/meterConnection/_search` | `1936`        | `EMPLOYEE`            |
| `/billing-service/bill/v2/_fetchbill`    | `1862`        | `EMPLOYEE`            |
| `/ws-services/wc/_search`                | `1900`        | `SW_CEMP , WS_CEMP`   |
| `/sw-services/swc/_search`               | `1940`        | `SW_CEMP , WS_CEMP`   |
| `/property-services/property/_search`    | `1897`        | `SW_CEMP` , `WS_CEMP` |
