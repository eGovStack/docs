---
description: UI details for eChallan feature in mCollect module
---

# eChallan UI Details

## Overview

<<<<<<< HEAD
This page offers a detailed insight into the user interface features, screens, and navigation available for the eChallan service in the mCollect module. Browse through this document to find the eChallan service details, MDMS and localization details.
=======
This page offers a detailed insight into the user interface features, screens, and navigation available for the eChallan service in the mCollect module. Browse through this document to find the eChallan service details, MDMS and localization details. 
>>>>>>> 64dca8adbdf64336b1a8203199b3791fa23434fa

## Objective

1. Generate **e-challans / bill** for all miscellaneous / Adhoc services which citizens avail from ULBs
2. The ability for ULBs to Notify citizens about the outstanding payments - Online and offline
3. Enable Digital payments for citizens - QR code, payment link in notifications, etc.

Employees will be able to Create Challan, by selecting the service category, entering all consumer information and tax head details.

## **mCollect - Create Challan**

![](../../../../.gitbook/assets/image-20210514-092513.png)

<<<<<<< HEAD
Click here to find the [create new challan file changes](https://github.com/egovernments/frontend/blob/39ffbeb4f5446bbb08729e9ce6cf0d519f2f748c/web/rainmaker/dev-packages/egov-uc-dev/src/ui-config/screens/specs/uc/newCollection.js).

=======
Click here to find the [create new challan file changes](https://github.com/egovernments/frontend/blob/39ffbeb4f5446bbb08729e9ce6cf0d519f2f748c/web/rainmaker/dev-packages/egov-uc-dev/src/ui-config/screens/specs/uc/newCollection.js).   
  
>>>>>>> 64dca8adbdf64336b1a8203199b3791fa23434fa
Selecting City is disabled as UC Employee of City A should be able to access/create only City A related challans.

## **MDMS Details**

```text
{
  "tenantId": "pb.amritsar",
  "moduleDetails": [
    {
      "moduleName": "BillingService",
      "masterDetails": [
        {
          "name": "BusinessService",
          "filter": "[?(@.type=='Adhoc')]"
        },
        {
        "name":"TaxPeriod"
        }
      ]
    },
    {
      "moduleName": "common-masters",
      "masterDetails": [
        {
          "name": "uiCommonPay"
        }
      ]
    }
  ]
}
```

### **Service Type and Service Category Dropdown Formation**

Based on the response, Service Type and Service category Dropdowns are Loaded.  
For eg: Refer to the response object

```text
{
  "businessService": "WaterCharges.Metered",
  "code": "WaterCharges.Metered",
  "collectionModesNotAllowed": [
    "DD"
  ],
  "partPaymentAllowed": false,
  "isAdvanceAllowed": true,
  "demandUpdateTime": 86400000,
  "isVoucherCreationEnabled": false,
  "type": "Adhoc"
}
```

<<<<<<< HEAD
Based on that `"businessService": "WaterCharges.Metered"`

The service Category is `"WaterCharges"` and the service Type is `"Metered"`  
The conversion of business Service utils is `setServiceCategory` method present in \`\`[https://github.com/egovernments/frontend/blob/39ffbeb4f5446bbb08729e9ce6cf0d519f2f748c/web/rainmaker/dev-packages/egov-uc-dev/src/ui-config/screens/specs/utils/index.js](https://github.com/egovernments/frontend/blob/39ffbeb4f5446bbb08729e9ce6cf0d519f2f748c/web/rainmaker/dev-packages/egov-uc-dev/src/ui-config/screens/specs/utils/index.js)
=======
Based on that `"businessService": "WaterCharges.Metered"` 

The service Category is `"WaterCharges"` and the service Type is `"Metered"`  
The conversion of business Service utils is `setServiceCategory` method present in ``[https://github.com/egovernments/frontend/blob/39ffbeb4f5446bbb08729e9ce6cf0d519f2f748c/web/rainmaker/dev-packages/egov-uc-dev/src/ui-config/screens/specs/utils/index.js](https://github.com/egovernments/frontend/blob/39ffbeb4f5446bbb08729e9ce6cf0d519f2f748c/web/rainmaker/dev-packages/egov-uc-dev/src/ui-config/screens/specs/utils/index.js)
>>>>>>> 64dca8adbdf64336b1a8203199b3791fa23434fa

### **Tax Head Dropdown Formation**

Based on the MDMS response `TaxHeadMaster` are formed by selection service type dropdown.

Filter the initial Taxhead master with selected service type with `service` attribute in each Taxheads.

**Other Validations and Create challan** can be refered in [https://github.com/egovernments/frontend/blob/39ffbeb4f5446bbb08729e9ce6cf0d519f2f748c/web/rainmaker/dev-packages/egov-uc-dev/src/ui-config/screens/specs/uc/newCollectionResource/newCollectionFooter.js](https://github.com/egovernments/frontend/blob/39ffbeb4f5446bbb08729e9ce6cf0d519f2f748c/web/rainmaker/dev-packages/egov-uc-dev/src/ui-config/screens/specs/uc/newCollectionResource/newCollectionFooter.js)

`createChallan` method is used to create challan.

`/echallan-services/eChallan/v1/_create` API is used to create a challan.

Users will be able to see the Challan Acknowledgement once the Challan is created successfully,

Actions available:

<<<<<<< HEAD
1. Proceed to Payment
=======
1.  Proceed to Payment
>>>>>>> 64dca8adbdf64336b1a8203199b3791fa23434fa
2. Download/print Challan
3. Navigate back to Home page

![](../../../../.gitbook/assets/image-20210514-100011.png)

<<<<<<< HEAD
Challan’s can be downloaded through this API `egov-pdf/download/UC/mcollect-challan?challanNo=`
=======
Challan’s can be downloaded through this API `egov-pdf/download/UC/mcollect-challan?challanNo=` 
>>>>>>> 64dca8adbdf64336b1a8203199b3791fa23434fa

## **Localisation Module**

`rainmaker-uc`

<<<<<<< HEAD
**API Used**
=======
**API Used** 
>>>>>>> 64dca8adbdf64336b1a8203199b3791fa23434fa

1. `egov-mdms-service/v1/_search`
2. `echallan-services/eChallan/v1/_create`
3. `egov-pdf/download/UC/mcollect-challan`

## **Role Action Mapping**

| [**S.NO**](http://s.no/) | **API** | **ROLES** | **ACTION ID** |
| :--- | :--- | :--- | :--- |
<<<<<<< HEAD
| 1 | `egov-mdms-service/v1/_search` |  | 954 |
| 2 | `echallan-services/eChallan/v1/_create` | UC\_EMP | 2112 |
| 3 | `egov-pdf/download/UC/mcollect-challan` | UC\_EMP | 2115 |

## **Document Resources and Links**
=======
| 1 | `egov-mdms-service/v1/_search` |   | 954 |
| 2 | `echallan-services/eChallan/v1/_create` | UC\_EMP | 2112 |
| 3 | `egov-pdf/download/UC/mcollect-challan` | UC\_EMP | 2115 |

## **Document Resources and Links** 
>>>>>>> 64dca8adbdf64336b1a8203199b3791fa23434fa

| **Related Title** | **Documentation** |
| :--- | :--- |
| MCollect Search Challan | [Search Challan and Pay Challan](search-and-pay-challan.md) |
| MCollect Pay Challan | [BillGenie](https://digit-discuss.atlassian.net/wiki/spaces/EGR/pages/436502610/BillGenie) |
| MCollect Edit / Update Challan | [Edit/Cancel Challan](edit-cancel-challan.md) |

<<<<<<< HEAD
[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)​](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation](https://egov.org.in/) is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).
=======


 [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)​](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation](https://egov.org.in/) is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).
>>>>>>> 64dca8adbdf64336b1a8203199b3791fa23434fa

