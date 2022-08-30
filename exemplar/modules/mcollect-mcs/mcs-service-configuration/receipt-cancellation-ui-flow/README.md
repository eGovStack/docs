# Receipt Cancellation UI Flow

## **Search Receipt**

## **Objective**

Provide employees with the option to search receipts specific to a module, download receipts, check its current status and cancel selected receipts.

Once the user login with **CR\_PT** role, the system displays the Receipts module card along with the  Total Receipts count.

![](<../../../../../.gitbook/assets/image (131).png>)

Clicking on Search receipts redirects users to the Inbox/search receipt screen.

Route -[ ![](https://cdn.jsdelivr.net/npm/@egovernments/digit-ui-css/img/browser-icon.png)mSeva](https://qa.digit.org/digit-ui/employee/receipts/inbox)

![](<../../../../../.gitbook/assets/image (185).png>)

Inbox File details\
[https://github.com/egovernments/digit-ui-internals/blob/main/packages/modules/receipts/src/pages/ReceiptInbox.js](https://github.com/egovernments/digit-ui-internals/blob/main/packages/modules/receipts/src/pages/ReceiptInbox.js)

## Technical Implementation Details

MDMS Configs used in this inbox screen `ReceiptStatus` show the required status in the inbox similarly `uiCommonPay` fetches the service categories.

```
    MdmsCriteria: {
      tenantId: tenantId,
      moduleDetails: [
        {
          moduleName: "common-masters",
          masterDetails: [
            {
              name: "uiCommonPay"
            }
            {
              name: "ReceiptStatus"
            }
           ]
        },
      ]
    }
```

The Search and Cancel Receipts option is available only for enabled services. This is configured in uiCommonPay config by setting **true** the `cancelReceipt.`

```
arrears: true
billKey: "property-bill"
cancelReceipt: true
code: "PT"
headerBandLabel: "PT_COMMON_TABLE_COL_PT_ID"
receiptKey: "property-receipt"
```

**Table Structure**

* Uses the same table component similar to other modules.

#### Data fetch <a href="#data-fetch" id="data-fetch"></a>

* Once the data is fetched using `collection-services/payments/{selectedbusinessService}/_search` API is used to search and get the required receipt details.
* The Same API `collection-services/payments/{selectedbusinessService}/_search` with a flag `isCountRequest` to get the required count of total receipts.

## **Cancel Receipt**

On the search results page, users can click on the receipt number to cancel any receipt. The details of this are available in the following document - [View Receipt and Cancel](view-receipt-cancel-ui-flow.md)

**Localisation Modules used**

rainmaker-common\
rainmaker-receipts

**To enable multiple business services -**

1. MDMS needs to be updated as`cancelReceipt : true`for that specific business service.
2. Role Actions, update the payment search and workflow API for the new USER Role.
3. Function logic should be updated to support multiple services. `getDefaultReceiptService = () => { return RECEIPTS_DEFAULT_SERVICE;}` [https://github.com/egovernments/digit-ui-internals/blob/main/packages/modules/receipts/src/utils/index.js](https://github.com/egovernments/digit-ui-internals/blob/main/packages/modules/receipts/src/utils/index.js)

## **Role Action Mapping**

Only the CR\_PT role is allowed to use this module.

|                                           |           |               |
| ----------------------------------------- | --------- | ------------- |
| **API**                                   | **ROLES** | **ACTION ID** |
| `egov-mdms-service/v1/_search`            | `CR_PT`   | `954`         |
| `collection-services/payments/PT/_search` | `CR_PT`   | `2029`        |
