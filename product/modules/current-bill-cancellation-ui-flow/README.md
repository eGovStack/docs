---
description: Frontend Repo
---

# Current Bill Cancellation UI Flow

Once the user login with `WS_CEMP` **or** `SW_CEMP` Roles, then the User will get the BillGenie tree option on the left side.

![](<../../../.gitbook/assets/image (157).png>)

on click on BillGenie will get two options like below

![](<../../../.gitbook/assets/image (136).png>)

on clicking on bill Cancellation, it will route to the search bill screen.

## **Search Bill**

### **Objective**

Provide Employee to search active bill, download bill and Cancel bill.

if tax head information can be wrong in a bill. So the bill needs to be cancelled.

Route -[ mSeva](https://qa.digit.org/employee/bills/billSearch)

![](<../../../.gitbook/assets/image (221).png>)

### Technical Implementation Details

* Initial page - [![](https://github.com/fluidicon.png)frontend/billSearch.js at master · egovernments/frontend](https://github.com/egovernments/frontend/blob/master/web/rainmaker/dev-packages/egov-abg-dev/src/ui-config/screens/specs/bills/billSearch.js)
* Initial MDMS call is being made on page load

![](<../../../.gitbook/assets/image (230).png>)

{% hint style="info" %}
Note: only for the enabled service we can search, cancel the bill and serviceCategory drop downs options .it can be configured in uiCommonPay config by setting **true** to `cancelBill` this path

[![](https://github.com/fluidicon.png)egov-mdms-data/uiCommonPay.json at QA · egovernments/egov-mdms-data](https://github.com/egovernments/egov-mdms-data/blob/QA/data/pb/common-masters/uiCommonPay.json)
{% endhint %}

example:

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

* Form rendering is taken care of in[ ![](https://github.com/fluidicon.png)frontend/billSearchCard.js at master · egovernments/frontend](https://github.com/egovernments/frontend/blob/master/web/rainmaker/dev-packages/egov-abg-dev/src/ui-config/screens/specs/bills/billSearchResources/billSearchCard.js)
* Table rendering is taken care of in[ ![](https://github.com/fluidicon.png)frontend/searchResults.js at master · egovernments/frontend](https://github.com/egovernments/frontend/blob/master/web/rainmaker/dev-packages/egov-abg-dev/src/ui-config/screens/specs/bills/billSearchResources/searchResults.js)
* The Bill search API and formatting data is in done in[ ![](https://github.com/fluidicon.png)frontend/function.js at master · egovernments/frontend](https://github.com/egovernments/frontend/blob/master/web/rainmaker/dev-packages/egov-abg-dev/src/ui-config/screens/specs/bills/billSearchResources/function.js)

**Table Structure**

* `MUIDataTable` is used to implement the Table component
* Every column entry is given as an Object

```
{
   labelName: "Bill No.",
   labelKey: "ABG_COMMON_TABLE_COL_BILL_NO"
}
```

* Any customizations at column level are by `customBodyRender` hook available in all the columns ‘option’ property.

![](<../../../.gitbook/assets/image (121).png>)

#### Data fetch, load and render <a href="#data-fetch-load-and-render" id="data-fetch-load-and-render"></a>

Once the data is fetched using `egov-searcher/bill-genie/billswithaddranduser/_get` API, the returned data is formatted and dispatched to redux

[![](https://github.com/fluidicon.png)frontend/function.js at master · egovernments/frontend](https://github.com/egovernments/frontend/blob/master/web/rainmaker/dev-packages/egov-abg-dev/src/ui-config/screens/specs/bills/billSearchResources/function.js)![](blob:https://digit-discuss.atlassian.net/d7d401f7-90dc-4940-8293-37c3c8fd2a08#media-blob-url=true\&id=379cbc6b-f53c-43ed-8a5b-e3922078b84d\&collection=contentId-1847263265\&contextId=1847263265\&mimeType=image%2Fpng\&name=image-20210727-103850.png\&size=111637\&width=947\&height=491)

![](<../../../.gitbook/assets/image (204).png>)

As we can see from the image above, the data is put to a specific path inside props.

[![](https://github.com/fluidicon.png)frontend/searchResults.js at master · egovernments/frontend](https://github.com/egovernments/frontend/blob/master/web/rainmaker/dev-packages/egov-abg-dev/src/ui-config/screens/specs/bills/billSearchResources/searchResults.js)

![](<../../../.gitbook/assets/image (181).png>)

The table component now fetches the data from its props as shown below.

![](<../../../.gitbook/assets/image (264).png>)

For employee Action as “cancel bill “ so that employee can cancel the active bill on click of cancel bill, it will navigate to the Bill details page where we can see the bill amount and other details from there we can do the Cancel.[ ![](https://github.com/fluidicon.png)frontend/viewBill.js at master · egovernments/frontend](https://github.com/egovernments/frontend/blob/master/web/rainmaker/dev-packages/egov-abg-dev/src/ui-config/screens/specs/bills/viewBill.js)

Bill details document is available here[ Bill Details](bill-details-ui-flow.md)

### **API Used**

1. `egov-mdms-service/v1/_search,`
2. `egov-searcher/bill-genie/billswithaddranduser/_get`

## **Role Action Mapping**

|                          |                                                      |                          |               |
| ------------------------ | ---------------------------------------------------- | ------------------------ | ------------- |
| [**S.NO**](http://s.no/) | **API**                                              | **ROLES**                | **ACTION ID** |
| 1                        | `egov-mdms-service/v1/_search`                       |                          | `954`         |
| 2                        | `egov-searcher/bill-genie/billswithaddranduser/_get` | `SUPERUSER` , `EMPLOYEE` | `1804`        |
