# Challan Creation

## **Overview**

Provide employees with the option to create Challan, by selecting the service category, and entering all consumer information and tax head details.

## Workflow Details

### **MCollect - Create Challan**

<figure><img src="../../../../../.gitbook/assets/image (17).png" alt=""><figcaption></figcaption></figure>

File Path:[ <img src="https://github.com/fluidicon.png" alt="" data-size="line">digit-ui-internals/CreateChallan.js at main · egovernments/digit-ui-internals](https://github.com/egovernments/digit-ui-internals/blob/main/packages/modules/mCollect/src/pages/employee/CreateChallan.js)

### **MDMS Details**

Created hooks for MDMS in mCollect, by using hooks will get the response by passing on the details in the method.

`Digit.MDMSService.getPaymentRules(tenantId, "[?(@.type=='Adhoc')]");` which is present in the below file:[ <img src="https://github.com/fluidicon.png" alt="" data-size="line">digit-ui-internals/CreateChallan.js at main · egovernments/digit-ui-internals](https://github.com/egovernments/digit-ui-internals/blob/main/packages/modules/mCollect/src/pages/employee/CreateChallan.js)

MDMS File path:[ <img src="https://github.com/fluidicon.png" alt="" data-size="line">digit-ui-internals/MDMS.js at main · egovernments/digit-ui-internals](https://github.com/egovernments/digit-ui-internals/blob/main/packages/libraries/src/services/elements/MDMS.js)

## **Technical Implementation Details**

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

Based on the MDMS response `TaxHeadMaster` are formed by the selected service type dropdown. Filter the initial Taxhead master with the selected service type with `service` the attributes in each Taxheads.

**Other Validations and Create challan** can be referred in[ <img src="https://github.com/fluidicon.png" alt="" data-size="line">digit-ui-internals/CreateChallan.js at main · egovernments/digit-ui-internals](https://github.com/egovernments/digit-ui-internals/blob/main/packages/modules/mCollect/src/pages/employee/CreateChallan.js)

`createChallan` the method is used to create challan.

`/echallan-services/eChallan/v1/_create` API is used to create a challan.

Once Challan is created successfully, you will be able to see the Challan Acknowledgement.

Actions available:

1. Print Challan
2. Go to home
3. Proceed to Payment

![](<../../../../../.gitbook/assets/image (266).png>)

File Path:[ <img src="https://github.com/fluidicon.png" alt="" data-size="line">digit-ui-internals/EmployeeChallanAcknowledgement.js at main · egovernments/digit-ui-internals](https://github.com/egovernments/digit-ui-internals/blob/main/packages/modules/mCollect/src/pages/employee/EmployeeChallanAcknowledgement.js)

**Print Challan:** Click on Print Challan, Challan will be downloaded using `egov-pdf/download/UC/mcollect-challan` API.

**Go to home:** Click on Go TO Home routes users to the home screen.

**Proceed To Payment:** Clicking on this routes users to the common pay screen and it is common for all modules also refer to [Update / Cancel Challan](update-cancel-challan-ui-flow.md).

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

| API                                                                   | Roles      | Action ID |
| --------------------------------------------------------------------- | ---------- | --------- |
| `egov-mdms-service/v1/_search`                                        |            | `954`     |
| `/echallan-services/eChallan/v1/_create`                              | `UC_EMP`   | `2112`    |
| `egov-pdf/download/UC/mcollect-challan`                               | `UC_EMP`   | `2115`    |
| `collection-services/payments/ADVT.Gas_Balloon_Advertisement/_search` | `UC_EMP`   | `2138`    |
| `collection-services/payments/_create`                                | `UC_EMP`   | `1862`    |
| `pdf-service/v1/_create`                                              | `UC_EMP`   | `1834`    |
| `billing-service/bill/v2/_fetchbill`                                  | `EMPLOYEE` | `1862`    |

## **Related Links**

| Related Title                  | Documenation                                                |
| ------------------------------ | ----------------------------------------------------------- |
| MCollect Search                | [mCollect - Technical Documentation](mcollect-ui-flow.md)   |
| MCollect Update/Cancel Challan | [Update / Cancel Challan](update-cancel-challan-ui-flow.md) |
