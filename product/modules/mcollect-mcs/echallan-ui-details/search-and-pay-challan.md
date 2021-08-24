# Search and Pay Challan

## Overview

This page offers the UI details for the search and pay challan feature. Once a Challan is created, in order to Pay the challan or update the challan, we have to find the relevant challan.

<<<<<<< HEAD
## **Search and Pay**
=======
## **Search and Pay** 
>>>>>>> 64dca8adbdf64336b1a8203199b3791fa23434fa

**A citizen** can only search the challan, download the challan, and pay for the challan.

In order to make any payment for challans, both _**Citizen and Employee**_ roles, use the **Bill genie** screens to get the bill and can proceed for payment.

[BillGenie](https://digit-discuss.atlassian.net/wiki/spaces/EGR/pages/436502610/BillGenie)

To Enable the service category to search we have to configure `billGineiURL` in MDMS as follow.

```text
{
  "businessService": "Taxes.No Dues Certificate",
  "code": "TX.No_Dues_Certificate",
  "collectionModesNotAllowed": [
    "DD"
  ],
  "partPaymentAllowed": false,
  "isAdvanceAllowed": false,
  "demandUpdateTime": 86400000,
  "isVoucherCreationEnabled": true,
  "type": "Adhoc",
  "billGineiURL": "egov-searcher/bill-genie/mcollectbills/_get"
}
```

Once `billGineiURL` is configured for a service, we get an option in bill genie to search for it.

<<<<<<< HEAD
Once the challan is created to Update or cancel challan we use Challan Search.

![](../../../../.gitbook/assets/image-20210514-112938.png)

Click here to find the [Search Challan file](https://github.com/egovernments/frontend/blob/39ffbeb4f5446bbb08729e9ce6cf0d519f2f748c/web/rainmaker/dev-packages/egov-uc-dev/src/ui-config/screens/specs/uc/search.js) and the [Search Results file](https://github.com/egovernments/frontend/blob/39ffbeb4f5446bbb08729e9ce6cf0d519f2f748c/web/rainmaker/dev-packages/egov-uc-dev/src/ui-config/screens/specs/uc/universalCollectionResources/searchChallanResults.js).
=======
Once the challan is created to Update or cancel challan we use Challan Search. 

![](../../../../.gitbook/assets/image-20210514-112938.png)

Click here to find the [Search Challan file](https://github.com/egovernments/frontend/blob/39ffbeb4f5446bbb08729e9ce6cf0d519f2f748c/web/rainmaker/dev-packages/egov-uc-dev/src/ui-config/screens/specs/uc/search.js) and the [Search Results file](https://github.com/egovernments/frontend/blob/39ffbeb4f5446bbb08729e9ce6cf0d519f2f748c/web/rainmaker/dev-packages/egov-uc-dev/src/ui-config/screens/specs/uc/universalCollectionResources/searchChallanResults.js). 
>>>>>>> 64dca8adbdf64336b1a8203199b3791fa23434fa

## **Localisation Module**

`rainmaker-uc`

**API Used**

1. `egov-mdms-service/v1/_search`
2. `echallan-services/eChallan/v1/_search`

## **Role Action Mapping**

| **S.No.** | **API** | **ROLES** | **ACTION ID** |
| :--- | :--- | :--- | :--- |
<<<<<<< HEAD
| 1 | `egov-mdms-service/v1/_search` |  | 954 |
=======
| 1 | `egov-mdms-service/v1/_search` |   | 954 |
>>>>>>> 64dca8adbdf64336b1a8203199b3791fa23434fa
| 2 | `echallan-services/eChallan/v1/_search` | UC\_EMP | 2114 |

## **Documents and Resource Links**

| **Related Title** | **Documentation** |
| :--- | :--- |
| MCollect Create Challan | [eChallan - Technical Documentation](./) |
| MCollect Pay Challan | [BillGenie](https://digit-discuss.atlassian.net/wiki/spaces/EGR/pages/436502610/BillGenie) |
| MCollect Edit / Update Challan | [Edit/Cancel Challan](edit-cancel-challan.md) |

<<<<<<< HEAD
[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)​](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation](https://egov.org.in/) is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).
=======


 [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)​](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation](https://egov.org.in/) is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).
>>>>>>> 64dca8adbdf64336b1a8203199b3791fa23434fa

