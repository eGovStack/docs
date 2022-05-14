# TL Apply Flow UI Details

## **Objective**

To provide the facility for the user to create trade license application for the current year by citizen or counter employee.![](blob:https://digit-discuss.atlassian.net/45b2ca9f-5acb-4679-82aa-2619bd7d185d#media-blob-url=true\&id=0ba070ea-7d63-4210-b678-07606a42e7fb\&collection=contentId-1847754759\&contextId=1847754759\&mimeType=image%2Fpng\&name=Screenshot%20from%202021-07-27%2014-17-00.png\&size=6402\&width=256\&height=122)

![TL Home Card](<../../../../.gitbook/assets/image (198).png>)

## **Apply for Trade License**

Users can apply for trade license application by clicking on the Apply for Trade License button, and while going through the workflow, can add all the information, according to the question asked, at the end of the flow a summary screen will be visible for the review of the answers and on clicking the submit button an Application Trade License will be created for current Financial Year.

**Apply Flow** - The Trade License Registration screen will be displayed after login, which helps the user to understand the necessary documents needed to complete the new registration for Trade License. A Citizen Info card is also shown at the bottom of the page for any additional information, in here it’s about the maximum size of the file that can be uploaded.

![Information Screen](<../../../../.gitbook/assets/image (207) (6).png>)

**Trade License Details/Assessment Flow -** In this flow, the user needs to provide specific information about the trade being registered in order to get the license. Following are the steppers user needs to go through in this flow.

Trade Name - The user needs to give the name of the trade and on this page, only an info card is shown at the bottom which tells about the current financial year the trade application will be created, this financial year value is retrieved from MDMS.

![](<../../../../.gitbook/assets/image (263).png>)

Structure Type - here users need to select yes or no based on whether the trade has mobility or not, if they select Yes, then it will move to vehicle type and if they select No then it will move to the Building type page.

![](<../../../../.gitbook/assets/image (238) (6).png>)

Vehicle Type / Building Type - The options for vehicle and building type are coming from the MDMS structure. Building type contains an information card about the options Pucca or kuccha.![](blob:https://digit-discuss.atlassian.net/6d2f1073-d1fe-4791-9ebc-29fcfaa46748#media-blob-url=true\&id=a236e4ce-2ba2-4304-988a-b999bfa23b31\&collection=contentId-1847754759\&contextId=1847754759\&mimeType=image%2Fpng\&name=Screenshot%20from%202021-07-27%2014-52-57.png\&size=13987\&width=287\&height=243)

![Vehicle Type](<../../../../.gitbook/assets/image (193) (6).png>)

![Building Type](<../../../../.gitbook/assets/image (243).png>)

Commencement Date - It defines the date at which the trade had started or will start in the future.

![](<../../../../.gitbook/assets/image (202).png>)

Trade Units - User can enter about the trade category whether its goods or services, according to the option selected, Trade Type will load from MDMS as a drop-down and according to the trade type selected trade sub-type options will load in the trade sub type drop-down. The unit of measure and UOM value cannot be entered by the user, it will get pre-populated according to the options selected above that too from MDMS.

Users need to enter at least one unit to move forward and if needed to enter more, add more unit option can be clicked to do so, and to remove any unit, delete option on the top right of each unit card can be clicked.

![](<../../../../.gitbook/assets/image (175).png>)

![](<../../../../.gitbook/assets/image (155).png>)

Accessories - The Accessory page inquires if there are any accessories required for the business or not. Accessories may not be compulsory for all trades. If yes, it will move to the accessory details page. If no, it will skip it altogether and move to the start of the address flow.

![](<../../../../.gitbook/assets/image (182) (6).png>)

Accessory details - The options for accessories are retrieved from MDMS. According to the option selected Unit of Measure or UOM gets pre-populated, which is non-editable by the user. The users can edit the UOM value and the accessory count or it may get pre-populated from MDMS. Click on Add More Trade Accessory button to add multiple accessories.![](blob:https://digit-discuss.atlassian.net/747713d2-9198-45d2-8d7f-c4fddd8d4ee2#media-blob-url=true\&id=67bc938b-e45d-41d0-944c-2b77bbef12ab\&collection=contentId-1847754759\&contextId=1847754759\&mimeType=image%2Fpng\&name=Screenshot%20from%202021-07-27%2015-14-11.png\&size=19635\&width=281\&height=457)

![](<../../../../.gitbook/assets/image (161).png>)

**Address Details Flow -** After entering the details about the Trade, users will need to enter the address of the Trade, where it is located. The flow is straightforward, without any conditional routing.

![](<../../../../.gitbook/assets/image (117) (6).png>)

![](<../../../../.gitbook/assets/image (203) (6).png>)

Users can pinpoint the location in the Geo-location map, according to which pin code and city, as well as locality, will be automatically filled.

**Owner Details Flow -** At the end, users need to enter the details, about the Trade owner. Ownership can be Single or Multiple Owners. According to which the details will be filled.

In the case of a single/Multiple Owner following screen will be displayed, rest flow will remain the same.

Users can add multiple owners by clicking on the add owner button, the same functionality as Trade units and accessories. Add Owner button is not visible if the user selects a single owner on the previous page.

![](<../../../../.gitbook/assets/image (223).png>)

The rest of the flow will contain the owner primary address and three documents mainly regarding address proof, owner identity and owner photograph.

![](<../../../../.gitbook/assets/image (250).png>)

**Check Page and Acknowledgement Screen -** Users can cross-verify the data entered throughout the flow in the Check page and also if needed to change/update any data, can do that by clicking on the change option just mentioned in front of the data, it will credit them to the said page which data needs to be changed and then the whole flow needs to be repeated again in order to submit the application.

For Applying of Trade License Create API is being called, following is the snippet of the Create API being used:`1create: "/tl-services/v1/_create"`

If the API response is successful, then the Acknowledgement Screen will be displayed, otherwise Failed Acknowledgement Screen will be displayed.

![](<../../../../.gitbook/assets/image (186).png>)

![](<../../../../.gitbook/assets/image (205) (6).png>)

On clicking on the Download Acknowledgement Form, A PDF will be downloaded.

![](<../../../../.gitbook/assets/image (247).png>)

## **Technical Implementation Details**

All the screen has been developed using the new-UI structure followed previously in FSM, PGR and PT, except for multi-component.

The link for the Apply Trade License Main Index is given below, it can be used to understand the starting point of the flow:

[https://github.com/egovernments/digit-ui-internals/blob/main/packages/modules/tl/src/pages/citizen/Create/index.js](https://github.com/egovernments/digit-ui-internals/blob/main/packages/modules/tl/src/pages/citizen/Create/index.js)

TL (Trade License) Module has been segregated into a specified structure, All the screen configuration is inside PageComponent Folder, and the configuration for routing of the pages are mentioned under config folder which is common for both Citizen as well as Employee. Below is the snippet for folder structure and routing configuration.

![](<../../../../.gitbook/assets/image (265).png>)

```
export const newConfig = [
  {
    head: "",
    body: [
      {
        type: "component",
        component: "TLInfoLabel",
        key: "tradedetils1",
        withoutLabel: true,
        hideInCitizen: true,
      }
    ]
  },
```

Pages Folder is where the high-level configuration for controlling the whole flow is mentioned, for citizens and employees. Citizen includes Create, EditTrade, Renewal, Applications and Search Trade. Which inside carry the index (the main starting point of the whole flow).

In the Accessory-details page, Billing slab search API `"/tl-calculator/billingslab/_search"` is being called, which returns the array list of all the accessories for which the billing slab has been configured, from that object only a list of accessories has been formed, if the response came out to be an empty array then the options are curated from the MDMS API mentioned in the MDMS data section.

After completing the flow the user can download the acknowledgement PDF form of the License created and the config for the PDF generation can be found in the link given below:

[https://github.com/egovernments/digit-ui-internals/blob/main/packages/modules/tl/src/utils/getTLAcknowledgementData.js](https://github.com/egovernments/digit-ui-internals/blob/main/packages/modules/tl/src/utils/getTLAcknowledgementData.js)

Utils Folder basically contains all the methods which are being used throughout the TL module, and if any common method needs to be declared here, which in turn can be imported in other files.

For creating an Application the Create API from Trade License is being called using the React hooks, which has been declared under hooks/elements/TL as TLService.

## **MDMS Data**

Throughout the flow, a few of the page data are being imported from MDMS, Following is the list of pages that are using MDMS data, These pages .js files can be found under page components.

| PageComponent            | MDMS Detail                                                    | Module Details Name | Master-Detail Name    |
| ------------------------ | -------------------------------------------------------------- | ------------------- | --------------------- |
| TradeLicense             | List of documents required for registration                    | `TradeLicense`      | `Documents`           |
| SelectTradeName          | Current Financial Year                                         | `egf-master`        | `FinancialYear`       |
| SelectVehicleType        | Type of mobility trade                                         | `common-masters`    | `StructureType`       |
| SelectBuildingType       | Type of Steady Trade                                           | `common-masters`    | `StructureType`       |
| SelectTradeUnits         | List of trade category and its corresponding type and sub-type | `TradeLicense`      | `TradeType`           |
| SelectAccessoriesDetails | Lit of Accessory and its Unit of measure and UOM value         | `TradeLicense`      | `AccessoriesCategory` |
| TLSelectAddress          | List of cities and its corresponding localities                | `TradeLicense`      | `tenants`             |
| SelectOwnerShipDetails   | categories imported are single and multiple owner.             | `common-masters`    | `OwnerShipCategory`   |
| SelectOwnerDetails       | List of Gender options.                                        | `common-masters`    | `GenderType`          |

For calling of MDMS data React Hooks has been used, so that it could be shared throughout the modules. Below is the little code snippet for the call used for MDMS.

```
const { isLoading, data: Documentsob = {} } = Digit.Hooks.tl.useTradeLicenseMDMS(stateId, "TradeLicense", "TLDocuments");
```

## **Localization**

Localization keys are added under the ‘_rainmaker-tl_’ locale module. In future, if any new labels are implemented in the Trade License (Citizen) that should also be pushed in the locale DB under _rainmaker-tl_ locale module. Below is an example of few locale labels.

![](<../../../../.gitbook/assets/image (158).png>)

## **API Call Role Action Mapping**

|                               |                                       |               |           |
| ----------------------------- | ------------------------------------- | ------------- | --------- |
| [**S.No**](http://s.no/)**.** | **API**                               | **Action id** | **Roles** |
| 1                             | `/egov-mdms-service/v1/_search`       | `954`         | `CITIZEN` |
| 2                             | `/tl-services/v1/_create`             | `1685`        | `CITIZEN` |
| 3                             | `/filestore/v1/files/url`             | `1528`        | `CITIZEN` |
| 4                             | `/billing-service/bill/v2/_fetchbill` | `1862`        | `CITIZEN` |
| 5                             | `/tl-calculator/billingslab/_search`  | `1684`        | `CITIZEN` |
| 6                             | `/tl-services/v1/_update`             | `1686`        | `CITIZEN` |
| 7                             | `/localization/messages/v1/_search`   | `1531`        | `CITIZEN` |
