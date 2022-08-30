# Common PT

**Objective**: Common PT is used as a plugin for other modules to search or create a lightweight property data on the go and tag it to the requesting module.

![](<../../../../.gitbook/assets/1 (3).png>)

## **Search Property** <a href="#seach-property" id="seach-property"></a>

CommonPT module provides two ways to search for a property. Users can search for a property either by **Property Id** or by **Door Number.**

**Search By Property ID**

* The search by Property ID requires certain parameters to filter out required properties.
  * City Name (Drop Down)
  * Owner Mobile Number (Input Field)
  * Property Id (Input Field)
  * Old Property Id (Input Field)
* where City Name is mandatory and at least one more parameter like Mobile Number, Property Id or Old Property Id must be provided to find properties.

![](<../../../../.gitbook/assets/image (92).png>)

**Search By Door Number**

* The search by Door Number form requires certain parameters to filter out required properties
  * City Name (Drop Down)
  * Locality (Drop Down)
  * Door Number (Input Field)
  * Consumer Name(Input Field)
* Where City Name and Locality are mandatory at least one more parameter like Door Number or Consumer Name is required to find properties.

![](<../../../../.gitbook/assets/image (318).png>)

Once the user enters all required details, the form redirects the user to the list of all properties registered with the property id or as per the search parameters entered by the user

![](<../../../../.gitbook/assets/image (302).png>)

Clicking on the Select button redirects users to the OTP verification page. Users must enter the OTP sent on their mobile number to proceed further.

![](<../../../../.gitbook/assets/image (196).png>)

Users are redirected to the Property Details pages where the user can create new property using the existing property ID.

![](<../../../../.gitbook/assets/image (214).png>)

Clicking on Create New Property button, redirects users to create a new property page form. Users can enter the property details to be registered.

![](<../../../../.gitbook/assets/image (71).png>)

After filling in all details users can submit.  The Acknowledgment page displays the application status as either Success or Failed along with the application number.

![](<../../../../.gitbook/assets/image (326).png>)![](<../../../../.gitbook/assets/image (121).png>)

## Common PT Integration With TL

Common PT search and create feature is integrated with the TL (Trade License) module. The two flows of common PT allow users to:

1. Select the desired property using property search facility. The user can select the property from the search results.
2. Create a new lightweight property during the trade license application process. Once the acknowledgement page is displayed, the Proceed button is enabled to move forward with the flow.

![](<../../../../.gitbook/assets/Screenshot from 2022-05-20 17-47-34.png>)![](<../../../../.gitbook/assets/Screenshot from 2022-05-20 17-48-25.png>)

Once the property is selected/created, property details is available on the next page Property Details.

![](<../../../../.gitbook/assets/Screenshot from 2022-05-20 17-48-36.png>)

Clicking on the View More Details button redirects users to the view property page that offers an overview detail of the attached property.

![](<../../../../.gitbook/assets/Screenshot from 2022-05-20 17-51-17.png>)

## &#x20;**Technical Implementation**

Common PT implementation code link:

{% embed url="https://github.com/egovernments/DIGIT-Dev/blob/develop/frontend/micro-ui/web/micro-ui-internals/packages/modules/commonPt/src/pages/citizen/index.js" %}

## Role Action Mapping

| **API**                               | **ACTION ID** | **ROLES** |
| ------------------------------------- | ------------- | --------- |
| `/property-services/property/_search` |               |           |
| `/billing-service/bill/v2/_fetchbill` | `1862`        |           |
| `/property-services/property/_create` |               |           |
| `/egov-mdms-service/v1/_search`       | `954`         |           |
| `/localization/messages/v1/_search`   | `1531`        |           |

&#x20;[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_ ](https://egov.org.in/)_is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
