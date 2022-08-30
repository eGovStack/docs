# Challan Creation

## **Create Challan**

### **Objective**

Provide Employee to create Challan, by selecting the service category, entering all consumer information and tax head details.

**MCollect - Create Challan**![](blob:https://digit-discuss.atlassian.net/ca892647-2509-462c-8aa4-126430b699df#media-blob-url=true\&id=36779bf0-e155-456d-84d3-20d0a3c5e4db\&collection=contentId-1845297183\&contextId=1845297183\&mimeType=image%2Fpng\&name=image-20210601-050414.png\&size=44228\&width=1180\&height=598)

File Path:[ ![](https://github.com/fluidicon.png)digit-ui-internals/CreateChallan.js at main · egovernments/digit-ui-internals](https://github.com/egovernments/digit-ui-internals/blob/main/packages/modules/mCollect/src/pages/employee/CreateChallan.js)

### **MDMS Details**

Created hooks for MDMS in mCollect, by using hooks will get the response by passing on the details in the method.

`Digit.MDMSService.getPaymentRules(tenantId, "[?(@.type=='Adhoc')]");` which is present in the below file:[ ![](https://github.com/fluidicon.png)digit-ui-internals/CreateChallan.js at main · egovernments/digit-ui-internals](https://github.com/egovernments/digit-ui-internals/blob/main/packages/modules/mCollect/src/pages/employee/CreateChallan.js)

MDMS File path:[ ![](https://github.com/fluidicon.png)digit-ui-internals/MDMS.js at main · egovernments/digit-ui-internals](https://github.com/egovernments/digit-ui-internals/blob/main/packages/libraries/src/services/elements/MDMS.js)

### **Service Type and Service Category Dropdown Formation**

Based on the response, Service Type and Service category Dropdowns are Loaded.\
For eg: Refer to the response object

```
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

Based on that `"businessService": "WaterCharges.Metered"`

The service Category will be `"WaterCharges"`

The service Type will be `"Metered"`

### **Tax Head Dropdown Formation**

Based on the MDMS response `TaxHeadMaster` are formed by selection service type dropdown.

Filter the initial Taxhead master with selected service type with `service` the attributes in each Taxheads.

**Other Validations and Create challan** can be referred in[ ![](https://github.com/fluidicon.png)digit-ui-internals/CreateChallan.js at main · egovernments/digit-ui-internals](https://github.com/egovernments/digit-ui-internals/blob/main/packages/modules/mCollect/src/pages/employee/CreateChallan.js)

`createChallan` the method is used to create challan.

`/echallan-services/eChallan/v1/_create` API is used to create a challan.

Once Challan is created successfully, you will be able to see Challan Acknowledgement.

Actions available:

1. Print Challan
2. Go to home
3. Proceed to Payment

![](<../../../../../.gitbook/assets/image (266).png>)

File Path:[ ![](https://github.com/fluidicon.png)digit-ui-internals/EmployeeChallanAcknowledgement.js at main · egovernments/digit-ui-internals](https://github.com/egovernments/digit-ui-internals/blob/main/packages/modules/mCollect/src/pages/employee/EmployeeChallanAcknowledgement.js)

**Print Challan:** Click on Print Challan, Challan will be downloaded using `egov-pdf/download/UC/mcollect-challan` API.

**Go to home:** Click on Go TO Home, will route to the home screen.

**Proceed To Payment:** On clicking this, will route the common pay screen and it is common for all modules and also refer to [Update / Cancel Challan](update-cancel-challan-ui-flow.md).

## **Localisation Module**

`rainmaker-uc`

## **API Used**

1. `egov-mdms-service/v1/_search`
2. `echallan-services/eChallan/v1/_update`
3. `egov-pdf/download/UC/mcollect-challan`
4. `collection-services/payments/ADVT.Gas_Balloon_Advertisement/_search` **we need to pass the businessService** (`collection-services/payments/{businessService}/_search` ).
5. `collection-services/payments/_create`
6. `billing-service/bill/v2/_fetchbill`
7. `pdf-service/v1/_create`

## **Role Action Mapping**

|                          |                                                                       |            |               |
| ------------------------ | --------------------------------------------------------------------- | ---------- | ------------- |
| [**S.NO**](http://s.no/) | **API**                                                               | **ROLES**  | **ACTION ID** |
| 1                        | `egov-mdms-service/v1/_search`                                        |            | `954`         |
| 2                        | `/echallan-services/eChallan/v1/_create`                              | `UC_EMP`   | `2112`        |
| 3                        | `egov-pdf/download/UC/mcollect-challan`                               | `UC_EMP`   | `2115`        |
| 4                        | `collection-services/payments/ADVT.Gas_Balloon_Advertisement/_search` | `UC_EMP`   | `2138`        |
| 5                        | `collection-services/payments/_create`                                | `UC_EMP`   | `1862`        |
| 6                        | `pdf-service/v1/_create`                                              | `UC_EMP`   | `1834`        |
| 7                        | `billing-service/bill/v2/_fetchbill`                                  | `EMPLOYEE` | `1862`        |

## **Related Links**

|                                |                                                             |
| ------------------------------ | ----------------------------------------------------------- |
| **Related Title**              | **Documentation**                                           |
| MCollect Search                | [mCollect - Technical Documentation](mcollect-ui-flow.md)   |
| MCollect Update/Cancel Challan | [Update / Cancel Challan](update-cancel-challan-ui-flow.md) |
