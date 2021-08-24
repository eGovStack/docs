# Receipt Cancellation UI Flow

## **Search Receipt**

### **Objective**

Provide Employee to search Receipt specific to a module, download receipt, check its current status and cancel selected receipt.  
  
Once the user login with **CR\_PT** Role, then the User will get the Receipts module card with Total receipts count.

![](../../../.gitbook/assets/image%20%28131%29.png)

Clicking of Search receipts it navigates to the Inbox/search receipt screen.  
  
Route -[ ![](https://cdn.jsdelivr.net/npm/@egovernments/digit-ui-css/img/browser-icon.png)mSeva](https://qa.digit.org/digit-ui/employee/receipts/inbox)

![](../../../.gitbook/assets/image%20%28185%29.png)

Inbox File details  
[https://github.com/egovernments/digit-ui-internals/blob/main/packages/modules/receipts/src/pages/ReceiptInbox.js](https://github.com/egovernments/digit-ui-internals/blob/main/packages/modules/receipts/src/pages/ReceiptInbox.js)

## Technical Implementation Details

MDMS Configs used in this inbox screen

`ReceiptStatus` to show all required status in the inbox

similarly `uiCommonPay` to get service categories

```text

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

only for the enabled service we can search and cancel the receipt .it can be configured in uiCommonPay config by setting **true** to `cancelReceipt`

```text
arrears: true
billKey: "property-bill"
cancelReceipt: true
code: "PT"
headerBandLabel: "PT_COMMON_TABLE_COL_PT_ID"
receiptKey: "property-receipt"

```

**Table Structure**

* Uses the same table component similar to other modules.

#### Data fetch <a id="Data-fetch,"></a>

* Once the data is fetched using `collection-services/payments/{selectedbusinessService}/_search` API is being used to search and get the required receipt details.
* The Same API `collection-services/payments/{selectedbusinessService}/_search` with a flag `isCountRequest` to get the required count of total receipts.

## **Cancel Receipt**

On search Results we can click on the receipt number to cancel any receipt, it is explained in the following documentation

[View Receipt and Cancel](view-receipt-cancel-ui-flow.md)  
  
**Localisation Modules used,**

rainmaker-common,  
rainmaker-receipts

**To enable multiple business services -**

1. MDMS needs to be updated as`cancelReceipt : true`for that specific business service.
2. Role Actions, update the payment search and workflow API for the new USER Role.
3. Function logic should be updated to support multiple services.  `getDefaultReceiptService = () => { return RECEIPTS_DEFAULT_SERVICE;}` [https://github.com/egovernments/digit-ui-internals/blob/main/packages/modules/receipts/src/utils/index.js](https://github.com/egovernments/digit-ui-internals/blob/main/packages/modules/receipts/src/utils/index.js) 

## **Role Action Mapping**

Only the Role CR\_PT is allowed to use this module.

| [**S.NO**](http://s.no/) | **API** | **ROLES** | **ACTION ID** |
| :--- | :--- | :--- | :--- |
| 1 | `egov-mdms-service/v1/_search` | `CR_PT` | `954` |
| 2 | `collection-services/payments/PT/_search` | `CR_PT` | `2029` |





