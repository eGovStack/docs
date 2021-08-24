# Renew Edit Application

All the fields in this flow are the same as the New TL Application. The difference here is that max fields are having pre-populated data \(On Loading the page, search is made for that particular application\).

Will get the Renew Trade License option, when the application is in an approved state and the same financial year application is not present in the workflow.

File path:[ ![](https://github.com/fluidicon.png)digit-ui-internals/ApplicationDetails.js at main · egovernments/digit-ui-internals](https://github.com/egovernments/digit-ui-internals/blob/main/packages/modules/tl/src/pages/employee/ApplicationDetails.js) 

![](../../../../.gitbook/assets/image%20%28269%29.png)

When we click on the Renew Trade License application, it will route to Renew screen 

File Path:[ ![](https://github.com/fluidicon.png)digit-ui-internals/ApplicationDetails.js at main · egovernments/digit-ui-internals](https://github.com/egovernments/digit-ui-internals/blob/main/packages/modules/tl/src/pages/employee/ApplicationDetails.js)

![](../../../../.gitbook/assets/image%20%28232%29.png)

File Path:[ ![](https://github.com/fluidicon.png)digit-ui-internals/index.js at main · egovernments/digit-ui-internals](https://github.com/egovernments/digit-ui-internals/blob/main/packages/modules/tl/src/pages/employee/ReNewApplication/index.js)

**Direct Renewal:** There is no change in any fields and directly clicks on submit application, update API call is made for the respective application wit respective to Direct Renewal \(`applicationType`: `RENEWAL`, `workflowCode`: `DIRECTRENEWAL,` \)and it will go into direct renewal flow.

**Edit Renewal:** If there is any change in any fields and clicks on submit application, update API call is made with respect to edit renewal \(`applicationType`: `RENEWAL`,`workflowCode`: `EDITRENEWAL` \)and update the application and it will go into edit renewal flow.

**Units, Accessories, Owners and documents details in case of Edit/Renewal flow**

1. Employee can edit units in both cases, employee can add and delete multiple units, please find the file below reg all use cases:[ ![](https://github.com/fluidicon.png)digit-ui-internals/TLTradeUnitsEmployee.js at main · egovernments/digit-ui-internals](https://github.com/egovernments/digit-ui-internals/blob/main/packages/modules/tl/src/pageComponents/TLTradeUnitsEmployee.js)
2. Employee cannot edit accessories in both cases, the employee can not add and delete multiple units and all fields are in disable state, please find the file below reg all use cases:[ ![](https://github.com/fluidicon.png)digit-ui-internals/TLAccessoriesEmployee.js at main · egovernments/digit-ui-internals](https://github.com/egovernments/digit-ui-internals/blob/main/packages/modules/tl/src/pageComponents/TLAccessoriesEmployee.js)
3. Employee can edit in both cases, expect ownership details, ownership details field is in disable state in both cases. please find the file below reg all use cases:[ ![](https://github.com/fluidicon.png)digit-ui-internals/TLTradeUnitsEmployee.js at main · egovernments/digit-ui-internals](https://github.com/egovernments/digit-ui-internals/blob/main/packages/modules/tl/src/pageComponents/TLTradeUnitsEmployee.js)
4. Employee can edit the documents in both cases, please find the file below reg all use cases:[ ![](https://github.com/fluidicon.png)digit-ui-internals/TLDocumentsEmployee.js at main · egovernments/digit-ui-internals](https://github.com/egovernments/digit-ui-internals/blob/main/packages/modules/tl/src/pageComponents/TLDocumentsEmployee.js)

**Acknowledgement Screen**

After a successful update call, the user is routed to the acknowledgement screen.

File Path:[ ![](https://github.com/fluidicon.png)digit-ui-internals/getTLAcknowledgementData.js at main · egovernments/digit-ui-internals](https://github.com/egovernments/digit-ui-internals/blob/main/packages/modules/tl/src/utils/getTLAcknowledgementData.js)

**EDIT Flow:** It is also the same as renewal flow only, but we are passing the action `action`: `RESUBMIT` on the update call with all the changes.

**Application/ Trade Details:** [Application Details/Trade Details](application-details-trade-details-ui-flows.md)

**TL Create New Application:**[ New Trade License Application](new-trade-license-ui-flow.md)

## **Role Action Mapping**

| [**S.NO**](http://s.no/) | **API** | **ROLES** | **ACTION ID** |
| :--- | :--- | :--- | :--- |
| 1 | `/egov-mdms-service/v1/_search` | `TL_CEMP` | `954` |
| 2 | `/tl-services/v1/_create` | `TL_CEMP` | `1685` |
| 3 | `/tl-services/v1/_update` | `TL_CEMP` | `1686` |
| 4 | `/tl-calculator/billingslab/_search` | `TL_CEMP` | `1684` |





