# Update Number & Invalid Number

**Objective:** To facilitate users update invalid or inactive mobile numbers in the owner records.

## Update Mobile Number <a href="#update-mobile-number-feature-provides-following" id="update-mobile-number-feature-provides-following"></a>

1. Reminds ULB users about the invalid mobile numbers existing in the owner's record and facilitates updating those in an easy way.
2. Enables ULB users to update the mobile numbers in a request from the property owner(s).
3. Enables property owner(s) to update the mobile number in their record by way of login into the system.

Users can update the mobile number from the application details page by clicking on the assign button at the workflow level.

![](<../../../.gitbook/assets/Screenshot from 2022-03-11 16-54-45.png>)

This opens a pop-up window where users can enter the respective details required to update the mobile number.

![](<../../../.gitbook/assets/Screenshot from 2022-03-11 16-56-24.png>)

Click on the Update button once the details are entered.

Following actions take place on successful updates -&#x20;

1. Mobile number is updated in the owner’s record and a success message is displayed.
2. View Property page is refreshed to reflect the updated mobile number.
3. SMS is sent to both (old and new) mobile numbers intimating about the change in the mobile number in the owner’s record.

The following actions take place on failure to update -

1. Failure message is displayed.
2. User remains on the View Property page.

## **Invalid Mobile Number**

Property is searched to collect the tax and the search result is displayed.

Clicking on the Collect Tax button displays an alert dialogue box communicating the following details:

1. Mobile number associated with owner(s) detail is incorrect. Update the correct mobile number to receive future notifications. - Text message.
2. Continue to Collect- **a**ction button
3. Update Mobile Number - action button

![](<../../../.gitbook/assets/Screenshot from 2022-03-11 17-04-41.png>)

Continue to Collect - The user is taken to the collection page and the collection process is completed.

Update Mobile Number - Users must provide the below details to update the mobile number:

1. **Owner’s name** - displays the owner name.
2. **Current mobile number** - displays the existing mobile number of the owner.
3. **New mobile number** - a text box to enter the new mobile number. The mobile number validations are applicable as per the DIGIT standard mobile number validation.
4. Documents required - provision to upload necessary documents as attachments. This is optional and includes -
   * Duly Signed Change Request Form
   * Identity Proof (Aadhar Card, Voter ID)
     * Document Name - Drop-down with the list of documents considered as identity proof.
     * Choose File - File picker to upload the file.
5. **Update** - action button to update the mobile no.

![](<../../../.gitbook/assets/Screenshot from 2022-03-11 17-05-23.png>)

The remaining process is the same as in the application details edit page.

## **Technical Implementation Details**

Update and invalid mobile number code link: [https://github.com/egovernments/DIGIT-Dev/blob/develop/frontend/micro-ui/web/micro-ui-internals/packages/modules/pt/src/components/search/PropertySearchResults.js](https://github.com/egovernments/DIGIT-Dev/blob/develop/frontend/micro-ui/web/micro-ui-internals/packages/modules/pt/src/components/search/PropertySearchResults.js)

Popup component code link: [https://github.com/egovernments/DIGIT-Dev/blob/develop/frontend/micro-ui/web/micro-ui-internals/packages/modules/pt/src/pages/citizen/MyProperties/updateNumber.js](https://github.com/egovernments/DIGIT-Dev/blob/develop/frontend/micro-ui/web/micro-ui-internals/packages/modules/pt/src/pages/citizen/MyProperties/updateNumber.js)&#x20;

Assignment code:&#x20;

```
const UpdatePropertyNumberComponent = Digit?.ComponentRegistryService?.getComponent("EmployeeUpdateOwnerNumber");
```

A mobile number is invalid if it doesn't match the pattern defined in the MDMS config file or if the number of digits is invalid.

MDMS Config

```
 "MdmsCriteria": {
        "tenantId": "pb",
        "moduleDetails": [
            {
                "moduleName": "PropertyTax",
                "masterDetails": [
                    {
                        "name": "UpdateNumber"
                    }
                ]
            }
        ]
    }

```

Response:

```
invalidNumber: "9999999999"
invalidPattern: "^[6789][0-9]{9}$"
skipEnabled: true
warningEnabled: true
documents:[]
```

**MDMS**

The MDMS is used to check any invalid number. This data is present in the technical implementation part.

## **Localization**

The localization keys for the update mobile number and invalid number are added to the ‘_rainmaker-pt_’ locale module. Any changes, updates or addition of any new localization key is done in the same locale module.

## **Role Actions Mapping**

| **Url**                                             | **Roles**   | **Action Id** |
| --------------------------------------------------- | ----------- | ------------- |
| `egov-workflow-v2/egov-wf/process/_search`          | `All Roles` | `1730`        |
| `/property-services/property/_search`               | `All Roles` | `1897`        |
| `/egov-workflow-v2/egov-wf/businessservice/_search` | `All Roles` | `1743`        |
| `/filestore/v1/files/url`                           | `All Roles` | `1528`        |
| `property-services/property/_update`                | `All Roles` | `1896`        |

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_ ](https://egov.org.in/)_is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
