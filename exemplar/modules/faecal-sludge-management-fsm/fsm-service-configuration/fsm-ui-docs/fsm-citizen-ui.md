# FSM Citizen UI

There are two new screens introduced in FSM v1.1 while creating a new application - the Payment Preference screen and the Gender Screen.

## **Payment Screen**

Users can select the preferred payment mode option on this screen.

![](<../../../../../.gitbook/assets/Screenshot from 2022-03-29 19-36-39 (1) (1).png>)

### Technical Implementation Details

**SelectPaymentPreference.js** is the file for rendering components based on the type of option.&#x20;

File path: _**DIGIT-Dev/frontend/micro-ui/web/micro-ui-internals/packages/modules/fsm/src/pageComponents/SelectPaymentPreference.js**_

### **MDMS Update**

Payment preference file: PaymentType.json

[<img src="https://github.com/fluidicon.png" alt="" data-size="line">egov-mdms-data/PaymentType.json at DEV · egovernments/egov-mdms-data](https://github.com/egovernments/egov-mdms-data/blob/DEV/data/pb/FSM/PaymentType.json)

```
{
    "tenantId": "pb",
    "moduleName": "FSM",
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
}
```

## **Gender Screen**

Users can select gender type on this screen.

![](<../../../../../.gitbook/assets/image (64).png>)\


### **Technical Implementation Details**

SelectGender.js is the file for rendering components based on the type of option.&#x20;

File path: **DIGIT-Dev/frontend/micro-ui/web/micro-ui-internals/packages/modules/fsm/src/pageComponents/SelectGender.js**

&#x20;Code snippet to fetch the gender type:

```
  const { data: GenderData, isLoading } = Digit.Hooks.fsm.useMDMS(stateId, "common-masters", "FSMGenderType");
```

