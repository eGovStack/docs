# View Receipt - Cancel UI Flow

## **Objective**

Provide Employee to Cancel a Receipt against a Receipt number.

Route -[ ![](https://cdn.jsdelivr.net/npm/@egovernments/digit-ui-css/img/browser-icon.png)mSeva](https://qa.digit.org/digit-ui/employee/receipts/details/PT/PT%2F107%2F2021-22%2F226438)

![](<../../../.gitbook/assets/image (236).png>)

## **View Receipt**

After searching a receipt with a click of Receipt number it navigates to viewing the receipt details.

and view receipt details are mentioned over [https://github.com/egovernments/digit-ui-internals/blob/main/packages/modules/receipts/src/pages/ReceiptDetails.js](https://github.com/egovernments/digit-ui-internals/blob/main/packages/modules/receipts/src/pages/ReceiptDetails.js)![](blob:https://digit-discuss.atlassian.net/f0766308-749a-4e4d-9e96-3bda88f8c4dc#media-blob-url=true\&id=408d8006-466e-425f-acfa-28c104d9046a\&collection=contentId-1847132209\&contextId=1847132209\&mimeType=image%2Fpng\&name=image-20210727-101222.png\&size=66596\&width=1331\&height=665)

### **Technical Implementation Details**

* Initial MDMS call is being made on page load. CancelReceiptReason MDMS is used for showing multiple reasons for cancelling.

```
     moduleDetails: [
        {
          moduleName: "common-masters",
          masterDetails: [
            {
              name: "CancelReceiptReason"
            }
          ]
        }
      ]
```

## **Cancel Receipt**

Action modal, This comes up with the click of cancel receipt.\
This cancel receipt action will be shown only for the following state of receipt.

`Receipt?.paymentStatus !== "CANCELLED" && Receipt?.paymentStatus !== "DEPOSITED" && (Receipt?.instrumentStatus == "APPROVED" || Receipt?.instrumentStatus == "REMITTED"`![](blob:https://digit-discuss.atlassian.net/20bfa1cb-4e12-4f0c-915b-124728bf95a6#media-blob-url=true\&id=ee52085d-8104-4c76-9921-aa2dd8497578\&collection=contentId-1847132209\&contextId=1847132209\&mimeType=image%2Fpng\&name=image-20210727-101620.png\&size=80496\&width=1319\&height=667)

![](<../../../.gitbook/assets/image (224).png>)

**Data fetch, load and render**

Once the Receipt is searched using `collection-services/payments/{selectedbusinessService}/_search` API , then we can cancel the receipt using `/collection-services/payments/{selectedbusinessService}/_workflow` Api

**Acknowledgement screen**\
It gets shown once the cancel receipt is clicked\
File details,\
[https://github.com/egovernments/digit-ui-internals/blob/main/packages/modules/receipts/src/pages/ReceiptAcknowledgement.js](https://github.com/egovernments/digit-ui-internals/blob/main/packages/modules/receipts/src/pages/ReceiptAcknowledgement.js)

## **Role Action Mapping**

|                          |                                              |           |               |
| ------------------------ | -------------------------------------------- | --------- | ------------- |
| [**S.NO**](http://s.no/) | **API**                                      | **ROLES** | **ACTION ID** |
| 1                        | `egov-mdms-service/v1/_search`               | `CR_PT`   | `954`         |
| 2                        | `collection-services/payments/PT/_search`    | `CR_PT`   | `2029`        |
| 3                        | `/collection-services/payments/PT/_workflow` | `CR_PT`   | `2028`        |
