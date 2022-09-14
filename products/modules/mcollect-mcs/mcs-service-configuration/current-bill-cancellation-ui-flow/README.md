---
description: Frontend Repo
---

# Current Bill Cancellation UI Flow

## Objective

Once the user logs in with `WS_CEMP` **or** `SW_CEMP` roles the BillGenie tree option is available on the left panel on the screen.

![](<../../../../../.gitbook/assets/image (157) (1).png>)

Clicking on the BillGenie displays two options as seen in the screenshot below.

![](<../../../../../.gitbook/assets/image (136).png>)

Click on the Bill Cancellation option. This routes the user to the search bill screen.

## **Search Bill**

### **Objective**

This option allows employees to search for active bills, download bills, or cancel bills.

For instance, a bill can be cancelled if the tax head information is entered wrong in a bill.&#x20;

Route -[ mSeva](https://qa.digit.org/employee/bills/billSearch)

![](<../../../../../.gitbook/assets/image (221).png>)

## Technical Implementation Details

* Initial page - [<img src="https://github.com/fluidicon.png" alt="" data-size="line">frontend/billSearch.js at master · egovernments/frontend](https://github.com/egovernments/frontend/blob/master/web/rainmaker/dev-packages/egov-abg-dev/src/ui-config/screens/specs/bills/billSearch.js)
* Initial MDMS call is made on page load

![](<../../../../../.gitbook/assets/image (230) (1).png>)

{% hint style="info" %}
Note: The search, cancel bill and service category options are available only for enabled services. This is configured in uiCommonPay config by marking the following`cancelBill` path as **true**.

[<img src="https://github.com/fluidicon.png" alt="" data-size="line">egov-mdms-data/uiCommonPay.json at QA · egovernments/egov-mdms-data](https://github.com/egovernments/egov-mdms-data/blob/QA/data/pb/common-masters/uiCommonPay.json)
{% endhint %}

Example:

```
{
   "code": "WS",
   "headerBandLabel": "PAYMENT_COMMON_CONSUMER_CODE",
   "pdfModule":"WNS",
   "receiptKey": "ws-onetime-receipt",
   "cancelReceipt":false,
   "cancelBill": true,
   "billKey": "ws-bill",
   "arrears": true,
   "buttons": [
    {
      "label": "COMMON_BUTTON_HOME",
      "citizenUrl": "/wns-citizen/home",
      "employeeUrl": "/wns/search"
    }
  ]
}
```

* Form rendering details available in[ <img src="https://github.com/fluidicon.png" alt="" data-size="line">frontend/billSearchCard.js at master · egovernments/frontend](https://github.com/egovernments/frontend/blob/master/web/rainmaker/dev-packages/egov-abg-dev/src/ui-config/screens/specs/bills/billSearchResources/billSearchCard.js)
* Table rendering details available in[ <img src="https://github.com/fluidicon.png" alt="" data-size="line">frontend/searchResults.js at master · egovernments/frontend](https://github.com/egovernments/frontend/blob/master/web/rainmaker/dev-packages/egov-abg-dev/src/ui-config/screens/specs/bills/billSearchResources/searchResults.js)
* The Bill Search API and formatting data is available in[ <img src="https://github.com/fluidicon.png" alt="" data-size="line">frontend/function.js at master · egovernments/frontend](https://github.com/egovernments/frontend/blob/master/web/rainmaker/dev-packages/egov-abg-dev/src/ui-config/screens/specs/bills/billSearchResources/function.js)

**Table Structure**

* `MUIDataTable` is used to implement the table component.
* Every column entry is treated as an object.

```
{
   labelName: "Bill No.",
   labelKey: "ABG_COMMON_TABLE_COL_BILL_NO"
}
```

* Any customizations at column level are done through the `customBodyRender` hook available with the _option_ property of the columns.

![](<../../../../../.gitbook/assets/image (121) (1).png>)

#### Data fetch, load and render <a href="#data-fetch-load-and-render" id="data-fetch-load-and-render"></a>

Once the data is fetched using `egov-searcher/bill-genie/billswithaddranduser/_get` API, the returned data is formatted and dispatched to redux.

[<img src="https://github.com/fluidicon.png" alt="" data-size="line">frontend/function.js at master · egovernments/frontend](https://github.com/egovernments/frontend/blob/master/web/rainmaker/dev-packages/egov-abg-dev/src/ui-config/screens/specs/bills/billSearchResources/function.js)![](blob:https://digit-discuss.atlassian.net/d7d401f7-90dc-4940-8293-37c3c8fd2a08#media-blob-url=true\&id=379cbc6b-f53c-43ed-8a5b-e3922078b84d\&collection=contentId-1847263265\&contextId=1847263265\&mimeType=image%2Fpng\&name=image-20210727-103850.png\&size=111637\&width=947\&height=491)

![](<../../../../../.gitbook/assets/image (204) (1).png>)

As seen in the above screenshot, the data is assigned to a specific path inside props.

[<img src="https://github.com/fluidicon.png" alt="" data-size="line">frontend/searchResults.js at master · egovernments/frontend](https://github.com/egovernments/frontend/blob/master/web/rainmaker/dev-packages/egov-abg-dev/src/ui-config/screens/specs/bills/billSearchResources/searchResults.js)

![](<../../../../../.gitbook/assets/image (181) (1).png>)

The table component now fetches the data from its props as shown below.

![](<../../../../../.gitbook/assets/image (264).png>)

To cancel bills, employees have to click on the Cancel Bill option. The system navigates to the Bill Details page that displays the bill amount and other details. The bill can be cancelled from this page.[ ](https://github.com/egovernments/frontend/blob/master/web/rainmaker/dev-packages/egov-abg-dev/src/ui-config/screens/specs/bills/viewBill.js)

[<img src="https://github.com/fluidicon.png" alt="" data-size="line">frontend/viewBill.js at master · egovernments/frontend](https://github.com/egovernments/frontend/blob/master/web/rainmaker/dev-packages/egov-abg-dev/src/ui-config/screens/specs/bills/viewBill.js)

For bill details refer to the document here - [Bill Details](bill-details-ui-flow.md).

### **API Used**

1. `egov-mdms-service/v1/_search,`
2. `egov-searcher/bill-genie/billswithaddranduser/_get`

## **Role Action Mapping**

|                                                      |                          |               |
| ---------------------------------------------------- | ------------------------ | ------------- |
| **API**                                              | **ROLES**                | **ACTION ID** |
| `egov-mdms-service/v1/_search`                       |                          | `954`         |
| `egov-searcher/bill-genie/billswithaddranduser/_get` | `SUPERUSER` , `EMPLOYEE` | `1804`        |
