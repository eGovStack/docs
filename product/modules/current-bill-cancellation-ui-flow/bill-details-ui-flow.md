# Bill Details UI Flow

## **Objective**

To provide users with the details of the Bills and options to cancel the bill.

![](<../../../.gitbook/assets/image (255).png>)

## **Implementation Details**

This screen is developed under the egov-abg-dev folder in the below file:

[![](https://github.com/fluidicon.png)frontend/viewBill.js at master · egovernments/frontend](https://github.com/egovernments/frontend/blob/master/web/rainmaker/dev-packages/egov-abg-dev/src/ui-config/screens/specs/bills/viewBill.js)

The details of the Bill is fetched by calling BillingService fetchBill API and the [Consumer.No](http://consumer.no) is used in the query param.

FetchBill API returns the Bill Object which contains all the details about the bill including Billing Period, Due Amount, Due Date, and information about the Tax, Cess, Rebate, Penalty applied in this bill.

NextStep

On click on next step, it will go to cancel bill screen, there we need to select the options for reason for bill cancellation. Find more details here for the cancel bill screen -[ Cancel Bill](cancel-bill-ui-flow.md)

next step button file present in the below file path: [![](https://github.com/fluidicon.png)frontend/viewBillFooter.js at master · egovernments/frontend](https://github.com/egovernments/frontend/blob/master/web/rainmaker/dev-packages/egov-abg-dev/src/ui-config/screens/specs/bills/viewBillResource/viewBillFooter.js)

![](<../../../.gitbook/assets/image (239) (4).png>)

## **API Call Role Action Mapping**

|                              |                                          |               |                       |
| ---------------------------- | ---------------------------------------- | ------------- | --------------------- |
| [**S.No**](http://s.no)**.** | **API**                                  | **Action id** | **Roles**             |
| 1                            | `/ws-calculator/meterConnection/_search` | `1936`        | `EMPLOYEE`            |
| 2                            | `/billing-service/bill/v2/_fetchbill`    | `1862`        | `EMPLOYEE`            |
| 3                            | `/ws-services/wc/_search`                | `1900`        | `SW_CEMP , WS_CEMP`   |
| 4                            | `/sw-services/swc/_search`               | `1940`        | `SW_CEMP , WS_CEMP`   |
| 5                            | `/property-services/property/_search`    | `1897`        | `SW_CEMP` , `WS_CEMP` |
