# New Trade License UI Flow

## **Objective**

The trade license 'apply' is the major feature in TL Module. It allows Citizens or Counter Employees to create TL Applications for the current financial year.

Every application is a part of the workflow. Once the user login with `TL_CEMP` role, then the User will get the option for creating a New TL Application in the TL card as well as in the inbox.

![](<../../../../../.gitbook/assets/image (123) (1).png>)

![](<../../../../../.gitbook/assets/image (138).png>)

File path:[ <img src="https://github.com/fluidicon.png" alt="" data-size="line">digit-ui-internals/TLCard.js at main · egovernments/digit-ui-internals](https://github.com/egovernments/digit-ui-internals/blob/main/packages/modules/tl/src/components/TLCard.js) and[ <img src="https://github.com/fluidicon.png" alt="" data-size="line">digit-ui-internals/DesktopInbox.js at main · egovernments/digit-ui-internals](https://github.com/egovernments/digit-ui-internals/blob/main/packages/modules/tl/src/components/inbox/DesktopInbox.js)

Clicking on New Application navigates to the New Trade License Application screen.

Route:[ ![](https://cdn.jsdelivr.net/npm/@egovernments/digit-ui-css/img/browser-icon.png)mSeva](https://qa.digit.org/digit-ui/employee/tl/new-application)

![](<../../../../../.gitbook/assets/image (152).png>)

File Path:[ <img src="https://github.com/fluidicon.png" alt="" data-size="line">digit-ui-internals/index.js at main · egovernments/digit-ui-internals](https://github.com/egovernments/digit-ui-internals/blob/main/packages/modules/tl/src/pages/employee/NewApplication/index.js)

## **Technical Implementation Details**

Initial MDMS call is being made on page load like old UI.

## **MDMS Data**

Structure Type and Sub Structure Type field data is fetched from[ <img src="https://github.com/fluidicon.png" alt="" data-size="line">egov-mdms-data/StructureType.json at master · egovernments/egov-mdms-data](https://github.com/egovernments/egov-mdms-data/blob/master/data/pb/common-masters/StructureType.json)

Trade Category, Trade Type, Trade Sub Type field data is fetched from[ <img src="https://github.com/fluidicon.png" alt="" data-size="line">egov-mdms-data/TradeType.json at master · egovernments/egov-mdms-data](https://github.com/egovernments/egov-mdms-data/blob/master/data/pb/TradeLicense/TradeType.json)

Mohalla Data -[ <img src="https://github.com/fluidicon.png" alt="" data-size="line">egov-mdms-data/boundary-data.json at master · egovernments/egov-mdms-data](https://github.com/egovernments/egov-mdms-data/blob/master/data/pb/amritsar/egov-location/boundary-data.json) (For Amritsar)

Accessories -[ <img src="https://github.com/fluidicon.png" alt="" data-size="line">egov-mdms-data/AccessoriesCategory.json at master · egovernments/egov-mdms-data](https://github.com/egovernments/egov-mdms-data/blob/master/data/pb/TradeLicense/AccessoriesCategory.json)

Type of Ownership and Type of Sub ownership -[ <img src="https://github.com/fluidicon.png" alt="" data-size="line">egov-mdms-data/OwnerShipCategory.json at master · egovernments/egov-mdms-data](https://github.com/egovernments/egov-mdms-data/blob/master/data/pb/common-masters/OwnerShipCategory.json)[ <img src="https://github.com/fluidicon.png" alt="" data-size="line">egov-mdms-data/OwnerType.json at master · egovernments/egov-mdms-data](https://github.com/egovernments/egov-mdms-data/blob/master/data/pb/common-masters/OwnerType.json)

documents:[ <img src="https://github.com/fluidicon.png" alt="" data-size="line">egov-mdms-data/documentObj.json at master · egovernments/egov-mdms-data](https://github.com/egovernments/egov-mdms-data/blob/master/data/pb/TradeLicense/documentObj.json)

**Data fetch, load and render**

* Clicking on Submit button, `tl-services/v1/_create` api is called and create the application, after getting success response, we are calling update API `tl-services/v1/_update`.
* On loading the page, `/tl-calculator/billingslab/_search` api is called for showing the licence type (File Path:[ <img src="https://github.com/fluidicon.png" alt="" data-size="line">digit-ui-internals/TLTradeDetailsEmployee.js at main · egovernments/digit-ui-internals](https://github.com/egovernments/digit-ui-internals/blob/main/packages/modules/tl/src/pageComponents/TLTradeDetailsEmployee.js) ) and accessories options (File Path:[ <img src="https://github.com/fluidicon.png" alt="" data-size="line">digit-ui-internals/TLAccessoriesEmployee.js at main · egovernments/digit-ui-internals](https://github.com/egovernments/digit-ui-internals/blob/main/packages/modules/tl/src/pageComponents/TLAccessoriesEmployee.js) ).

**Acknowledgement Screen**

![](<../../../../../.gitbook/assets/image (132).png>)

After the success of creating and updating calls will route to the \*\*\*\*acknowledgement screen.

File Path:[ <img src="https://github.com/fluidicon.png" alt="" data-size="line">digit-ui-internals/getTLAcknowledgementData.js at main · egovernments/digit-ui-internals](https://github.com/egovernments/digit-ui-internals/blob/main/packages/modules/tl/src/utils/getTLAcknowledgementData.js)

## **Role Action Mapping**

| S.No. | API                                  | Roles     | Action ID |
| ----- | ------------------------------------ | --------- | --------- |
| 1     | `/egov-mdms-service/v1/_search`      | `TL_CEMP` | `954`     |
| 2     | `/tl-services/v1/_create`            | `TL_CEMP` | `1685`    |
| 3     | `/tl-services/v1/_update`            | `TL_CEMP` | `1686`    |
| 4     | `/tl-calculator/billingslab/_search` | `TL_CEMP` | `1684`    |
