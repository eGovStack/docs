# Update - Cancel Challan UI Flow

## **Objective**

Challans are created using create Challan, it is explained in[ Challan Creation](challan-creation.md)

Provide Employee to update / Cancel / Pay Challan against a Challan number.

Route -[ ![](https://cdn.jsdelivr.net/npm/@egovernments/digit-ui-css/img/browser-icon.png)mSeva](https://qa.digit.org/digit-ui/employee/mcollect/challansearch/PB-CH-2021-07-27-000732)

## **View Challan**

After searching a Challan on a click of Challan number it navigates to viewing the Challan details.

and view Challan details is mentioned over[ ![](https://github.com/fluidicon.png)digit-ui-internals/EmployeeChallan.js at main · egovernments/digit-ui-internals](https://github.com/egovernments/digit-ui-internals/blob/main/packages/modules/mCollect/src/EmployeeChallan.js)

![](<../../../../../.gitbook/assets/image (162) (1).png>)

## **Technical Implementation Details**

### **Cancel Challan**

Action modal - This comes up on the click of cancel Challan.

![](<../../../../../.gitbook/assets/image (233).png>)

Click on yes, the challan will be cancelled and users will be routed to the acknowledgement screen.

File path of acknowledgement screen:[ ![](https://github.com/fluidicon.png)digit-ui-internals/EmployeeChallanAcknowledgement.js at main · egovernments/digit-ui-internals](https://github.com/egovernments/digit-ui-internals/blob/main/packages/modules/mCollect/src/pages/employee/EmployeeChallanAcknowledgement.js)

### **Update Challan**

Update Challan screen, This comes up on the click of update Challan ([![](https://cdn.jsdelivr.net/npm/@egovernments/digit-ui-css/img/browser-icon.png)mSeva](https://qa.digit.org/digit-ui/employee/mcollect/modify-challan/PB-CH-2021-07-26-000727) ).

File path:[ ![](https://github.com/fluidicon.png)digit-ui-internals/index.js at main · egovernments/digit-ui-internals](https://github.com/egovernments/digit-ui-internals/blob/main/packages/modules/mCollect/src/pages/employee/EditChallan/index.js)

![](<../../../../../.gitbook/assets/image (261).png>)

On click on update challan, it will update and route to the acknowledgement screen.

![](<../../../../../.gitbook/assets/image (119).png>)

File Path:[ ![](https://github.com/fluidicon.png)digit-ui-internals/EmployeeChallanAcknowledgement.js at main · egovernments/digit-ui-internals](https://github.com/egovernments/digit-ui-internals/blob/main/packages/modules/mCollect/src/pages/employee/EmployeeChallanAcknowledgement.js)

### **Pay Challan**

common pay screen, This comes up once the user clicks on the Pay Challan/Proceed button to payment from the acknowledgement screen.

This pay screen is common for all the modules.

![](<../../../../../.gitbook/assets/image (271).png>)

On Click on collect payment, payment will collect and it will route to the acknowledgement screen it is common for all modules.![](blob:https://digit-discuss.atlassian.net/913085bc-e9d1-441b-8b57-7d6794ed9437#media-blob-url=true\&id=278f82dd-54f4-4a35-a253-7b56a59943fc\&collection=contentId-1669955631\&contextId=1669955631\&mimeType=image%2Fpng\&name=image-20210728-022205.png\&size=48929\&width=1165\&height=546)

Click on Print Receipt, `qa.digit.org/collection-services/payments/{challanBusinessService}/_search` (we need to configure bussinessServices to the respective roles in the MDMS like below ) API, will get the payment response, by using that response again we need to call `pdf-service/v1/_create` API.

**Data fetch, load and render**

* Once the Challan is searched using `echallan-services/eChallan/v1/_search` API, then we can search for bill details using `billing-service/bill/v2/_search` for the tax head breakup information.
* For Updating/Cancelling the Challan, we can use the API `/echallan-services/eChallan/v1/_update`.
* download / print Challan using `egov-pdf/download/UC/mcollect-challan` API.

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

|                          |                                                                       |           |               |
| ------------------------ | --------------------------------------------------------------------- | --------- | ------------- |
| [**S.NO**](http://s.no/) | **API**                                                               | **ROLES** | **ACTION ID** |
| 1                        | `egov-mdms-service/v1/_search`                                        |           | `954`         |
| 2                        | `echallan-services/eChallan/v1/_update`                               | `UC_EMP`  | `2117`        |
| 3                        | `egov-pdf/download/UC/mcollect-challan`                               | `UC_EMP`  | `2115`        |
| 4                        | `echallan-services/eChallan/v1/_search`                               | `UC_EMP`  | `2114`        |
| 5                        | `billing-service/bill/v2/_search`                                     | `UC_EMP`  | `1861`        |
| 6                        | `billing-service/bill/v2/_fetchbill`                                  | `UC_EMP`  |               |
| 7                        | `collection-services/payments/ADVT.Gas_Balloon_Advertisement/_search` | `UC_EMP`  | `2138`        |
| 8                        | `collection-services/payments/_create`                                | `UC_EMP`  | `1862`        |
| 9                        | `pdf-service/v1/_create`                                              | `UC_EMP`  | `1834`        |

## **Related Links**

|                         |                                                           |
| ----------------------- | --------------------------------------------------------- |
| **Related Title**       | **Documentation**                                         |
| MCollect Create Challan | [Challan Creation](challan-creation.md)                   |
| MCollect Search Challan | [mCollect - Technical Documentation](mcollect-ui-flow.md) |
