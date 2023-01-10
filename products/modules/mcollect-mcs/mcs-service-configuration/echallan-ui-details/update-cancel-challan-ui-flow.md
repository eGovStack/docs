# Update - Cancel Challan UI Flow

## **Overview**

Challans are created using create Challan, it is explained in[ Challan Creation](challan-creation.md)

## Workflow Details

Provide Employee to update / Cancel / Pay Challan against a Challan number.

Route -[ ![](https://cdn.jsdelivr.net/npm/@egovernments/digit-ui-css/img/browser-icon.png)mSeva](https://qa.digit.org/digit-ui/employee/mcollect/challansearch/PB-CH-2021-07-27-000732)

### **View Challan**

After searching for a Challan with a click on the Challan number it navigates to viewing the Challan details. The view Challan details is mentioned over[ <img src="https://github.com/fluidicon.png" alt="" data-size="line">digit-ui-internals/EmployeeChallan.js at main · egovernments/digit-ui-internals](https://github.com/egovernments/digit-ui-internals/blob/main/packages/modules/mCollect/src/EmployeeChallan.js)

![](<../../../../../.gitbook/assets/image (162) (1).png>)

## **Technical Implementation Details**

### **Cancel Challan**

Action modal - This comes up on the click of cancel Challan.

![](<../../../../../.gitbook/assets/image (233).png>)

Click on yes, the challan will be cancelled and users will be routed to the acknowledgement screen.

File path of acknowledgement screen:[ <img src="https://github.com/fluidicon.png" alt="" data-size="line">digit-ui-internals/EmployeeChallanAcknowledgement.js at main · egovernments/digit-ui-internals](https://github.com/egovernments/digit-ui-internals/blob/main/packages/modules/mCollect/src/pages/employee/EmployeeChallanAcknowledgement.js)

### **Update Challan**

Update Challan screen, This comes up on the click of update Challan ([![](https://cdn.jsdelivr.net/npm/@egovernments/digit-ui-css/img/browser-icon.png)mSeva](https://qa.digit.org/digit-ui/employee/mcollect/modify-challan/PB-CH-2021-07-26-000727) ).

File path:[ <img src="https://github.com/fluidicon.png" alt="" data-size="line">digit-ui-internals/index.js at main · egovernments/digit-ui-internals](https://github.com/egovernments/digit-ui-internals/blob/main/packages/modules/mCollect/src/pages/employee/EditChallan/index.js)

![](<../../../../../.gitbook/assets/image (261).png>)

Clicking on the Update Challan option updates and routes users to the acknowledgement screen.

![](<../../../../../.gitbook/assets/image (119).png>)

File Path:[ <img src="https://github.com/fluidicon.png" alt="" data-size="line">digit-ui-internals/EmployeeChallanAcknowledgement.js at main · egovernments/digit-ui-internals](https://github.com/egovernments/digit-ui-internals/blob/main/packages/modules/mCollect/src/pages/employee/EmployeeChallanAcknowledgement.js)

### **Pay Challan**

The common pay screen is visible once the user clicks on the Pay Challan/Proceed button to payment from the acknowledgement screen.

This pay screen is common for all the modules.

![](<../../../../../.gitbook/assets/image (271).png>)

Clicking on the Collect Payment button payment allows users to collect and route to the acknowledgement screen it is common for all modules.

<figure><img src="../../../../../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

Click on Print Receipt, `qa.digit.org/collection-services/payments/{challanBusinessService}/_search` (we need to configure bussinessServices to the respective roles in the MDMS like below ) API will get the payment response, by using that response again we need to call `pdf-service/v1/_create` API.

**Data fetch, load and render**

* Once the Challan is searched using `echallan-services/eChallan/v1/_search` API, then we can search for bill details using `billing-service/bill/v2/_search` for the tax head breakup information.
* For Updating/Cancelling the Challan, we can use the API `/echallan-services/eChallan/v1/_update`.
* download/print Challan using `egov-pdf/download/UC/mcollect-challan` API.

## **Localisation Module**

`rainmaker-uc`

## **API Used**

1. `egov-mdms-service/v1/_search`
2. `echallan-services/eChallan/v1/_update`
3. `egov-pdf/download/UC/mcollect-challan`
4. `echallan-services/eChallan/v1/_search`
5. `billing-service/bill/v2/_search`
6. `collection-services/payments/ADVT.Gas_Balloon_Advertisement/_search` **we need to pass the businessService** (`collection-services/payments/{businessService}/_search` ).
7. `collection-services/payments/_create`
8. `billing-service/bill/v2/_fetchbill`
9. `pdf-service/v1/_create`

## **Role Action Mapping**

| API                                                                   | Roles    | Action ID |
| --------------------------------------------------------------------- | -------- | --------- |
| `egov-mdms-service/v1/_search`                                        |          | `954`     |
| `echallan-services/eChallan/v1/_update`                               | `UC_EMP` | `2117`    |
| `egov-pdf/download/UC/mcollect-challan`                               | `UC_EMP` | `2115`    |
| `echallan-services/eChallan/v1/_search`                               | `UC_EMP` | `2114`    |
| `billing-service/bill/v2/_search`                                     | `UC_EMP` | `1861`    |
| `billing-service/bill/v2/_fetchbill`                                  | `UC_EMP` |           |
| `collection-services/payments/ADVT.Gas_Balloon_Advertisement/_search` | `UC_EMP` | `2138`    |
| `collection-services/payments/_create`                                | `UC_EMP` | `1862`    |
| `pdf-service/v1/_create`                                              | `UC_EMP` | `1834`    |

## **Related Links**

| Related Title           | Documentation                                             |
| ----------------------- | --------------------------------------------------------- |
| MCollect Create Challan | [Challan Creation](challan-creation.md)                   |
| MCollect Search Challan | [mCollect - Technical Documentation](mcollect-ui-flow.md) |
