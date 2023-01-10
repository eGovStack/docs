# View Receipt - Cancel UI Flow

## **Overview**

Provide employees with the option to Cancel a Receipt for a specific receipt number.

## Workflow Details

Route -[ ![](https://cdn.jsdelivr.net/npm/@egovernments/digit-ui-css/img/browser-icon.png)mSeva](https://qa.digit.org/digit-ui/employee/receipts/details/PT/PT%2F107%2F2021-22%2F226438)

![](<../../../../../.gitbook/assets/image (236).png>)

## **View Receipt**

The search page displays the receipts. Click on the specific receipt number navigates the user to view the receipt details.

View receipt details are available here [https://github.com/egovernments/digit-ui-internals/blob/main/packages/modules/receipts/src/pages/ReceiptDetails.js](https://github.com/egovernments/digit-ui-internals/blob/main/packages/modules/receipts/src/pages/ReceiptDetails.js)

## **Technical Implementation**&#x20;

The initial MDMS call is made on page load. CancelReceiptReason MDMS is used to display multiple reasons for cancelling.

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

Action modal - This appears with the click of Cancel Receipt.\
The cancel receipt action is shown only for the following state of receipt.

`Receipt?.paymentStatus !== "CANCELLED" && Receipt?.paymentStatus !== "DEPOSITED" && (Receipt?.instrumentStatus == "APPROVED" || Receipt?.instrumentStatus == "REMITTED"`

![](<../../../../../.gitbook/assets/image (224).png>)

**Data fetch, load and render**

Once the Receipt is searched using `collection-services/payments/{selectedbusinessService}/_search` API, the user can cancel the receipt using `/collection-services/payments/{selectedbusinessService}/_workflow` API

**Acknowledgement screen**\
It gets shown once the cancel receipt is clicked.\
File details - [https://github.com/egovernments/digit-ui-internals/blob/main/packages/modules/receipts/src/pages/ReceiptAcknowledgement.js](https://github.com/egovernments/digit-ui-internals/blob/main/packages/modules/receipts/src/pages/ReceiptAcknowledgement.js)

## **Role Action Mapping**

| API                                          | Roles   | Action ID |
| -------------------------------------------- | ------- | --------- |
| `egov-mdms-service/v1/_search`               | `CR_PT` | `954`     |
| `collection-services/payments/PT/_search`    | `CR_PT` | `2029`    |
| `/collection-services/payments/PT/_workflow` | `CR_PT` | `2028`    |
