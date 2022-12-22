# Trade License Renewal UI Flow

## **Renewal Flow**

This feature allows the user to renew any trade license applications, which either has been expired or had to be renewed for current financial year (Approved and Paid), it also had integration with the payment component, in order to complete the flow all together for renewal.

Renewal can be two types:

* DIRECT RENEWAL
* EDIT RENEWAL

### **Renewal List**

Once the user click on Renew Trade License button at the home page, it will redirect to the renewal list page which will display all the application eligible for the renewal corresponding to the mobile number on which the user has logged in. It will show the Trade name, License Number, Owner Name and status whether active or expired.![](blob:https://digit-discuss.atlassian.net/0330bfe3-4d76-473b-8177-c2a888c1a862#media-blob-url=true\&id=64447843-1df7-4f77-b485-97a1d5dc41b2\&collection=contentId-1849000004\&contextId=1849000004\&mimeType=image%2Fpng\&name=Screenshot%20from%202021-07-28%2014-18-45.png\&size=25937\&width=273\&height=393)

Once the user click on Renew Button, it will redirect the user on the summary page just like in edit Trade license, with all the values pre-populated from the search API. Info card will be declared so that user will understand how to proceed with either direct renewal or edit renewal.

![](<../../../../../.gitbook/assets/image (9).png>)

### **Direct Renewal**

If the user just want to renew the same application without updating any data, it will cross-verify all the values in the summary page and then click on submit button directly at the end of the page, this will lead the application with the next status as pending for payment and user can go through payment flow from the acknowledgement screen also, by clicking on the Make Payment button.

![](../../../../../.gitbook/assets/image.png)

### **Edit Renewal**

If the user before renewal need to update the application, they can do so by clicking on the change button on the summary screen, this will tell that the flow has been changed from direct to edit renewal, and user will need to follow the same apply flow in order to complete the edit part of it. the values from the application will be pre-populated in the respective screens, to get the details about the edit flow,one can refer this link. [Send Back Flow - Edit](send-back-edit-ui-flow.md).

Once the user click on submit button it will change the current action of the application to pending for document verification as the data has been updated.

## **Technical Implementation Details**

Renewal Trade main index can be found in the below given link:

[https://github.com/egovernments/digit-ui-internals/blob/main/packages/modules/tl/src/pages/citizen/Renewal/index.js](https://github.com/egovernments/digit-ui-internals/blob/main/packages/modules/tl/src/pages/citizen/Renewal/index.js)

in this we are calling the trade license search API, In order to get all the application, through which the sorting is happened to classify which application are eligible for renewal for the current financial year.

the hook which has been used for the API is:

```
const { isLoading, isError, error, data } = Digit.Hooks.tl.useTradeLicenseSearch({ filters: filter1 }, {});
  if (isLoading) {
    return <Loader />;
  }
```

The data from here then are sorted into application which doesn’t have any open renewal application for current financial year or which has a status of approved or expired. the significant method to get the renewal list of application is mentioned below:

```
applicationsList.filter((response)=>response.licenseNumber).map((ob)=>{
    if(applications[ob.licenseNumber]){
    if(applications[ob.licenseNumber].applicationDate<ob.applicationDate)
    applications[ob.licenseNumber]=ob
    }
    else
    applications[ob.licenseNumber]=ob;    
    })
```

From here the Trade License List Component has been called which displays the list of the renewal application.

[https://github.com/egovernments/digit-ui-internals/blob/main/packages/modules/tl/src/pages/citizen/Renewal/TradeLicenseList.js](https://github.com/egovernments/digit-ui-internals/blob/main/packages/modules/tl/src/pages/citizen/Renewal/TradeLicenseList.js)

The main functionality of converting the License Object received from the API to the object structure for formdata for apply flow , following is done at the similar way as the edit trade, and the same method is being used to convert the response object, to know more details please refer to[ Send Back Flow - Edit](send-back-edit-ui-flow.md)

Once the user has completed the flow as required or clicked the submit button directly, the method `convertToEditTrade` is being called, which re arranges the data for the request body for the update API `/tl-services/v1/_update`.

If its a direct renewal only one update API is being called which updates the financial year only.

but if its a edit renewal, two updated API is called after the first API successful call the application status gets changed to Initiated but after the second API call its changed to applied. with next action as pending for document verification.

the code for these can be found in utils folder index please refer the below link for the same:

[https://github.com/egovernments/digit-ui-internals/blob/main/packages/modules/tl/src/utils/index.js](https://github.com/egovernments/digit-ui-internals/blob/main/packages/modules/tl/src/utils/index.js)

## **MDMS**

MDMS data which is being used here is same as the Apply flow only, as the flow structure used for edit renew trade is same as the Apply for Trade License. Please refer the link for detailed MDMS information.

[Trade License - Apply Flow](./)

## **Localization**

For Renew Trade also, the Localization keys are being added in the ‘_rainmaker-tl_’ locale module. To change, update or adding of any new localization key will be done in the same locale module only.
