# Cancel Bill UI Flow

## **Overview**

To provide users with the option to select cancel reasons and the options to cancel the bill.

## Workflow Details

![](<../../../../../.gitbook/assets/image (254).png>)

## **Implementation Details**

The screen development files are available in the egov-abg-dev folder within the below-mentioned link.

[<img src="https://github.com/fluidicon.png" alt="" data-size="line">frontend/cancelBill.js at master · egovernments/frontend](https://github.com/egovernments/frontend/blob/master/web/rainmaker/dev-packages/egov-abg-dev/src/ui-config/screens/specs/bills/cancelBill.js)

The reasons for bill cancellation options are fetched from the MDMS service.

[<img src="https://github.com/fluidicon.png" alt="" data-size="line">egov-mdms-data/CancelCurrentBillReasons.json at QA · egovernments/egov-mdms-data](https://github.com/egovernments/egov-mdms-data/blob/QA/data/pb/common-masters/CancelCurrentBillReasons.json)

**PREVIOUS STEP:** Clicking on the Previous Step option redirects users to the bill details screen.

![](<../../../../../.gitbook/assets/image (267).png>)

## **Cancel Bill**

![](<../../../../../.gitbook/assets/image (147) (1).png>)

Clicking on the cancel bill option triggers the cancel bill API (`billing-service/bill/v2/_cancelbill` ). Once the API call is successful it routes to the acknowledgement screen.

The Next Step button file is available in the below-mentioned file path.

[<img src="https://github.com/fluidicon.png" alt="" data-size="line">frontend/viewBillFooter.js at master · egovernments/frontend](https://github.com/egovernments/frontend/blob/master/web/rainmaker/dev-packages/egov-abg-dev/src/ui-config/screens/specs/bills/viewBillResource/viewBillFooter.js)

![](<../../../../../.gitbook/assets/image (214) (1).png>)

**Acknowledgement Screen**

file path: [<img src="https://github.com/fluidicon.png" alt="" data-size="line">frontend/acknowledgement.js at master · egovernments/frontend](https://github.com/egovernments/frontend/blob/master/web/rainmaker/dev-packages/egov-abg-dev/src/ui-config/screens/specs/bills/acknowledgement.js)

![](<../../../../../.gitbook/assets/image (259).png>)

## **Localisation**

For localisation, the “rainmaker-ws” and “rainmaker-abg” modules are re-used. In case they are any new keys, these are added under “rainmaker-abg”.

## **API Call Role Action Mapping**

| API                                   | Action ID | Roles                             |
| ------------------------------------- | --------- | --------------------------------- |
| `billing-service/bill/v2/_cancelbill` | `1936`    | `SUPERUSER`, `SW_CEMP`, `WS_CEMP` |
| `egov-mdms-service/v1/_search`        | `954`     |                                   |
