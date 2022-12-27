# FSM Employee UI

## New Application  <a href="#new-application" id="new-application"></a>

Details of components added to the employee's new application screen are given below.

![](<../../../../../.gitbook/assets/image (16) (10).png>)

* **Payment Type:** Employees can select the mode of payment while creating a new application.

SelectPaymentType.js contains the component which is responsible to render the component.

File path: _DIGIT-Dev/frontend/micro-ui/web/micro-ui-internals/packages/modules/fsm/src/pageComponents/SelectPaymentType.js_

MDMS changes responsible to render payment type links and codes are given below:&#x20;

PaymentType.json -

[<img src="https://github.com/fluidicon.png" alt="" data-size="line">egov-mdms-data/PaymentType.json at DEV · egovernments/egov-mdms-data](https://github.com/egovernments/egov-mdms-data/blob/DEV/data/pb/FSM/PaymentType.json)

```
    "PaymentType": [
        {
            "name": "Pay Now",
            "code": "PRE_PAY",
            "active": true
        },
        {
            "name": "Pay on Service",
            "code": "POST_PAY",
            "active": true
        }
    ]
```

PreFieldsconfig.json -

[<img src="https://github.com/fluidicon.png" alt="" data-size="line">egov-mdms-data/PreFieldsConfig.json at DEV · egovernments/egov-mdms-data](https://github.com/egovernments/egov-mdms-data/blob/DEV/data/pb/FSM/PreFieldsConfig.json)

```
// Some  {
              "type": "component",
              "key": "paymentPreference",
              "withoutLabel": true,
              "component": "SelectPaymentType"
        }
```

master-config.json -

[<img src="https://github.com/fluidicon.png" alt="" data-size="line">egov-mdms-data/master-config.json at DEV · egovernments/egov-mdms-data](https://github.com/egovernments/egov-mdms-data/blob/DEV/master-config.json)

```
 "PaymentType": {
      "masterName": "PaymentType",
      "isStateLevel": true,
      "uniqueKeys": [
        "$.code"
      ]
    },
```

* **Gender Type:** Employees can choose the gender type of the applicants.

SelectName.js is responsible for rendering the component.

**File Path:** _DIGIT-Dev/frontend/micro-ui/web/micro-ui-internals/packages/modules/fsm/src/pageComponents/SelectName.js_

To render the gender type we have added the Object for gender in Inputs in selectName.js

```
{
      label: "COMMON_APPLICANT_GENDER",
      type: "dropdown",
      name: "applicantGender",
      options: genderTypes,
      isMandatory: false,
    }
```

## Vehicle Capacity And Number Of Trips <a href="#3.-vehicle-capacity-and-no-of-trips" id="3.-vehicle-capacity-and-no-of-trips"></a>

![](<../../../../../.gitbook/assets/image (347).png>)

Employees can select the vehicle capacity and the number of trips according to the need.

The number of trips is editable only if the payment type is selected as post-pay.

* **Schedule Action:** The **** Schedule Action option allows employees to schedule trips by entering the number of trips.

### Technical Implementation <a href="#technical-implementation" id="technical-implementation"></a>

Vehicle Type has been replaced by Vehicle Capacity and the vehicle capacity shown in the drop-down is filtered by the available DSOs. The unique value for capacity is shown in the drop-down.

![](<../../../../../.gitbook/assets/image (7) (1) (1).png>)

## Application Timeline <a href="#application-timeline" id="application-timeline"></a>

In the employee application timeline shown on the application details page, the vehicle timeline is also added with new statuses (Waiting for Disposal, Disposal in Progress and Disposed). These statuses are shown with the number of vehicle trips linked to individual applications.

![](<../../../../../.gitbook/assets/image (68).png>)\


### Technical Implementation  <a href="#technical-implementation-.1" id="technical-implementation-.1"></a>

For getting vehicle timeline /vehicle/trip/v1/\_search API is called for that particular application and based on the response Waiting for Disposal, Disposal in Progress and Disposed statuses are shown.

Code for handling vehicle trip timeline data available here: _frontend/micro-ui/web/micro-ui-internals/packages/libraries/src/services/elements/WorkFlow.js_

![](<../../../../../.gitbook/assets/image (8) (1).png>)

![](<../../../../../.gitbook/assets/image (14) (1).png>)
