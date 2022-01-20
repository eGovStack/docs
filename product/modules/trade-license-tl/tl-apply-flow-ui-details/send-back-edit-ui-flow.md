# Send Back - Edit UI Flow

## **Edit Trade License**

This feature allows the user to edit the application already created under their mobile number. After verifying employee can send the application back to the citizen with remarks of any changes that are needed to be done, which can be edited by the user using this flow.

## **Edit Application**

On the Application details page, on the employee side, if the application is marked with “Send Back to Citizen”, the edit option will appear dynamically at the end of the application details page, which the user can navigate through my applications.

![](<../../../../.gitbook/assets/image (166).png>)

After this, On clicking the button, the user can edit the trade license details by going through the create flow again. First, it will land on the Summary page, where for each section “change” button is there. Clicking on the Change button, the user will be redirected to the particular content, the only exception here will be the values will be pre-populated from the License object received from Trade License Search API, on completing the flow, Update API will be called and License application will get successfully updated.

![Acknowledgement Screen](<../../../../.gitbook/assets/image (125).png>)

## **Technical Implementation Details**

Edit Trade License main index can be found in the link given below:

[https://github.com/egovernments/digit-ui-internals/blob/main/packages/modules/tl/src/pages/citizen/EditTrade/index.js](https://github.com/egovernments/digit-ui-internals/blob/main/packages/modules/tl/src/pages/citizen/EditTrade/index.js)

here the main code consists of the function which results in transforming the License object received in Search API to the object structure which is suitable for citizen Apply flow (owner details, units, accessories etc), as the user needs to go through Apply flow again with pre-populated details and update the value of any accordingly. it also consists of the routing for the pages in the Apply flow.

getTradeEditDetails() function is being used so that the License object which is received from the Trade Search API, is converted to the Apply flow relevant structure so that the values can be pre-populated for the user convenience, on completing the flow, the application is updated. The link for the same can be found below:

[![](https://github.com/fluidicon.png)digit-ui-internals/index.js at main · egovernments/digit-ui-internals](https://github.com/egovernments/digit-ui-internals/blob/main/packages/modules/tl/src/pages/citizen/EditTrade/index.js)

User can delete and add as many as accessory or units it needs but there should be at least one unit to complete the application, to add a new unit or accessory “Add” button is used which is located at the end of the page. A new array is formed with all the updated details or with the old unit/accessory, when the flow is completed, this new array is then compared with the old array of accessories and units, and a new resulting array object is formed for the request body, you can find the respective code in the following method : `gettradeupdateaccessories` & `gettradeupdateunits`. this can be found in the below link[ ![](https://github.com/fluidicon.png)digit-ui-internals/index.js at main · egovernments/digit-ui-internals](https://github.com/egovernments/digit-ui-internals/blob/main/packages/modules/tl/src/utils/index.js)

Similarly, for owners the method which is used to form the new request param array is `gettradeownerarray`

It is similar to Accessories and Units - the only difference is in UI. Users can’t select multiple owners and only add one owner, it needs to either add more than one owner or select a single owner as ownership category and proceed. After the successful update the application next action will be “Pending for document verification” as there is an update in the data.

On completing the flow, the same object structure which was being used earlier in the flow gets changed into the request body structure for the update API: `/tl-services/v1/_update`, for this, the method which gets used is declared inside the Utils folder. Method name: `convertToResubmitTrade` and it can be found in the below link:

[https://github.com/egovernments/digit-ui-internals/blob/main/packages/modules/tl/src/utils/index.js](https://github.com/egovernments/digit-ui-internals/blob/main/packages/modules/tl/src/utils/index.js)![](blob:https://digit-discuss.atlassian.net/4e2802b2-9a96-4ec6-9c98-8a460896386d#media-blob-url=true\&id=6d9d422b-f7ff-4999-b7ed-e014ddc2e590\&collection=contentId-1848672338\&contextId=1848672338\&mimeType=image%2Fpng\&name=Screenshot%20from%202021-07-28%2013-35-12.png\&size=61348\&width=525\&height=405)

## **MDMS**

MDMS data that is being used here is the same as the Apply flow only, as the flow structure used for edit trade is the same as the Apply for Trade License. Please refer to the link for detailed MDMS information.

[Trade License - Apply Flow](./)

## **Localization**

For Edit Trade also, the Localization keys are being added in the ‘_rainmaker-tl_’ locale module. To change, update or adding of any new localization key will be done in the same locale module only.
