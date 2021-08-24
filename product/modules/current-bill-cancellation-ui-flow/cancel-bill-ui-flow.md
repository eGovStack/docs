# Cancel Bill UI Flow

## **Objective**

To provide users for selecting reasons and options to cancel the bill.

![](../../../.gitbook/assets/image%20%28254%29.png)

## **Implementation Details**

This screen is developed under the egov-abg-dev folder in the below file:

[![](https://github.com/fluidicon.png)frontend/cancelBill.js at master · egovernments/frontend](https://github.com/egovernments/frontend/blob/master/web/rainmaker/dev-packages/egov-abg-dev/src/ui-config/screens/specs/bills/cancelBill.js)

The reasons for bill cancellation options are fetching from MDMS service.

[ ![](https://github.com/fluidicon.png)egov-mdms-data/CancelCurrentBillReasons.json at QA · egovernments/egov-mdms-data](https://github.com/egovernments/egov-mdms-data/blob/QA/data/pb/common-masters/CancelCurrentBillReasons.json)

**PREVIOUS STEP:** on click on this it will go back to the bill details screen.

![](../../../.gitbook/assets/image%20%28267%29.png)

## **Cancel Bill**

![](../../../.gitbook/assets/image%20%28147%29.png)

On click on cancel bill, cancel bill API \(`billing-service/bill/v2/_cancelbill` \)will trigger and after the success of the cancel bill, it will route to the acknowledgement screen.

next step button file present in the below file path:

[![](https://github.com/fluidicon.png)frontend/viewBillFooter.js at master · egovernments/frontend](https://github.com/egovernments/frontend/blob/master/web/rainmaker/dev-packages/egov-abg-dev/src/ui-config/screens/specs/bills/viewBillResource/viewBillFooter.js)

![](../../../.gitbook/assets/image%20%28214%29.png)

**Acknowledgement Screen**

file path: [ ![](https://github.com/fluidicon.png)frontend/acknowledgement.js at master · egovernments/frontend](https://github.com/egovernments/frontend/blob/master/web/rainmaker/dev-packages/egov-abg-dev/src/ui-config/screens/specs/bills/acknowledgement.js)

![](../../../.gitbook/assets/image%20%28259%29.png)

## **Localisation**

for these modules, we are re-using the “rainmaker-ws” and “rainmaker-abg” modules, if they are any new keys, we are adding under “rainmaker-abg”.

## **API Call Role Action Mapping**

| [**S.No**](http://s.no/)**.** | **API** | **Action id** | **Roles** |
| :--- | :--- | :--- | :--- |
| 1 | `billing-service/bill/v2/_cancelbill` | `1936` | `SUPERUSER`, `SW_CEMP`, `WS_CEMP` |
| 2 | `egov-mdms-service/v1/_search` | `954` |  |

