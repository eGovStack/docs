# Stakeholder - Registration Flow

## **Objective** <a href="#objective" id="objective"></a>

This page provides details on the Stakeholder Registration workflow in the OBPAS module. Citizens have the option to submit the registration applications for various Stakeholders such as architects and construction companies.&#x20;

![BPA Home Card](<../../../../.gitbook/assets/Screenshot from 2021-09-30 10-20-48.png>)

## Apply For Stakeholder Application

Users can apply for stakeholder application by clicking on the “Register as a Stakeholder”, and while going through the workflow, can add all the information, according to the question asked, in the middle of the workflow after correspondence address Create API will be called, and at the end of the flow, a summary screen will be visible for the review of the answers and on clicking the submit button an Update API will be called which will change the status from Initiated to Applied and Registration Application will get updated.

### Registration Flow

The stakeholder Document Required screen is displayed after login, which helps the user to understand the necessary documents needed to complete the new registration for stakeholders. A citizen info card is also shown at the bottom of the page containing additional information such as the maximum size of the file that can be uploaded.

![Document Required Screen](<../../../../.gitbook/assets/Screenshot from 2021-09-30 10-41-39.png>)

### TimeLine Component

The TimeLine component is present on all pages. It informs the users about the steppers in completing the application for registration.

![TimeLine](<../../../../.gitbook/assets/Screenshot from 2021-10-07 22-28-57.png>)

### &#x20;Licensee Details&#x20;

In this step, users need to provide information about the License type and Licensee.

#### License Type

The system asks for the type of license that the user is registering for. If the user selects architecture, then a new field is displayed i.e. architecture number. For all other roles, no additional information user is required. All the roles are populated from the MDMS.

![License Type](<../../../../.gitbook/assets/Screenshot from 2021-10-07 22-26-32.png>)

#### Licensee Details

Here users have to provide the information of the person for whom the license application is being generated. By default, the name and mobile number field will be automatically pre-filled with the logged-in user data. Edits to this detail are disabled. Applicants must fill in the remaining information accordingly.

![Licensee Details](<../../../../.gitbook/assets/Screenshot from 2021-10-07 22-32-30.png>)

### Address Details

In this step, users have to enter their address details.

#### Permanent Address

Users have to provide a permanent address. This is mandatory information that the user needs to provide to move to proceed with the application.

![Permanent Adress](<../../../../.gitbook/assets/Screenshot from 2021-10-07 22-35-30.png>)

#### Correspondence Address

Here user gets the option to either pre-fill the form with the permanent address provided earlier or enter a different address. Users can also skip this step as it is non-mandatory.

![Correspondence Address](<../../../../.gitbook/assets/Screenshot from 2021-10-07 22-37-59.png>)

Clicking on the Next button calls the Create API. Further information is available in the technical Implementation details section.

### Document Details

#### Licensee Document Details

This screen displays a list of documents and their type (in dropdown format) from the MDMS. The document list displayed is as per the role selected by the user in license step. Users have to upload all the mandatory documents in order to proceed further.

![Document Details](<../../../../.gitbook/assets/Screenshot from 2021-10-07 22-42-20.png>)

### Summary Page and Acknowledgement Screen

Users can cross-verify the data entered throughout the flow on the Summary page. In case of any change or update required, the edit icon available adjacent to the section header allows the users to make the changes. It redirects users to the particular section page and the whole flow is repeated again in order to submit the application.

Along with the application details, the fee estimate for the corresponding application is also shown on the summary page.

![Fee Estimate](<../../../../.gitbook/assets/Screenshot from 2021-10-07 22-48-38.png>)

The Update API is called for the BPAREG Application update. Update API snippet given below:&#x20;

```
bpaRegUpdate: "/tl-services/v1/BPAREG/_update"
```

If the API response is successful, the Acknowledgement Screen is displayed. Else, the Failed Acknowledgement Screen is displayed.

![Summary Page](<../../../../.gitbook/assets/Screenshot from 2021-10-07 22-47-12.png>) ![Acknowledgement Page](<../../../../.gitbook/assets/Screenshot from 2021-10-07 22-49-38.png>)

Clicking on the Make Payment option to pay the registration fees is said in the summary screen.

## **Technical Implementation Details**

All the screen has been developed using the new-UI structure followed previously in FSM, PGR, PT and TL, few new components have been introduced such as TimeLine, Multi upload Document etc

The link for the Stakeholder Registration Main Index is given below, it can be used to understand the starting point of the flow:

[https://github.com/egovernments/DIGIT-Dev/blob/develop/frontend/micro-ui/web/micro-ui-internals/packages/modules/obps/src/pages/citizen/StakeholderRegistration/index.js](https://github.com/egovernments/DIGIT-Dev/blob/develop/frontend/micro-ui/web/micro-ui-internals/packages/modules/obps/src/pages/citizen/StakeholderRegistration/index.js)

The OBPAS module is segregated into a specified structure. The screen configuration details are available in the PageComponent folder and the configuration for routing of the pages are available in the config folder which is common for both citizens as well as employees. New components like TimeLine is defined in the component folder. Below is the snippet for folder structure and routing configuration.

![](<../../../../.gitbook/assets/Screenshot from 2021-10-07 22-55-13.png>)

The Stakeholder config responsible for the routing of the pages is defined under config folder. Click on the link below to access the code.

{% embed url="https://github.com/egovernments/DIGIT-Dev/blob/develop/frontend/micro-ui/web/micro-ui-internals/packages/modules/obps/src/config/stakeholderConfig.js" %}

```
 {
      head: "ES_NEW_APPLICATION_PROPERTY_ASSESSMENT",
      body: [
        {
          route: "stakeholder-docs-required",
          component: "StakeholderDocsRequired",
          key: "data",
          nextStep: "provide-license-type"
        },
        {
          type: "component",
          route: "provide-license-type",
          isMandatory: true,
          component: "LicenseType",
          texts: {
            headerCaption: "BPA_LICENSE_DET_CAPTION",
            header: "BPA_LICENSE_TYPE_LABEL",
            cardText: "BPA_LICENSE_TYPE_TEXT",
            submitBarLabel: "CS_COMMON_NEXT",
          },
          nextStep: "license-details",
          key: "LicneseType",
          withoutLabel: true,
          hideInEmployee: true,
        },
```

The Pages folder contains the high-level configuration for controlling the whole flow for citizens and employees. The flows for citizens include Apply flows, Send Back flows, Application details etc. These carry the index (the main starting point of the whole flow).

The main difference of Stakeholder registration flow from the apply flow in other modules is that the Create API is called in between the flow and at the end, the Update API is called.

The code for Create API request object generation is found inside the correspondence address component. This API call is triggered when the user clicks on the Next button on the correspondence address page.

The hook used for this API call is `Digit.OBPSService.BPAREGCreate(payload, tenantId)` and payload can be found inside the gonext() method in the following file:

Code reference:

[https://github.com/egovernments/DIGIT-Dev/blob/develop/frontend/micro-ui/web/micro-ui-internals/packages/modules/obps/src/pageComponents/CorrospondenceAddress.js](https://github.com/egovernments/DIGIT-Dev/blob/develop/frontend/micro-ui/web/micro-ui-internals/packages/modules/obps/src/pageComponents/CorrospondenceAddress.js)

The Utils folder basically contains all the methods that are used throughout the OBPAS module, and if any common method needs to be declared here, which in turn can be imported in other files.&#x20;

For updating an application the Update API from BPAREG is called using the React hooks, which has been declared under hooks/elements/obps as OBPSService.

The response object from the Create API is used for the request object of Update API, with the addition of document details which the user has entered. This marks the status of the Application as Applied instead of initiated.

Below is the hook used for fetching the update API call.

```
const mutation = Digit.Hooks.obps.useStakeholderAPI(
    data?.address?.city ? data.address?.city?.code : tenantId,
    true
  );
```

This API is called in the Stakeholder Acknowledgement code, using the useEffect Hook.

Code reference:

{% embed url="https://github.com/egovernments/DIGIT-Dev/blob/develop/frontend/micro-ui/web/micro-ui-internals/packages/modules/obps/src/pages/citizen/StakeholderRegistration/StakeholderAcknowledgement.js" %}

### **MDMS Data**

Throughout the flow, a few of the page data is imported from MDMS. Following are the list of pages that use MDMS data. These pages .js files can be found under page components.

| PageComponent           | MDMS Detail                                 | Module Details Name        | Master Detail Name         |
| ----------------------- | ------------------------------------------- | -------------------------- | -------------------------- |
| StakeholderDocsRequired | List of documents required for registration | `StakeholderRegistraition` | `StakeholderRegistraition` |
| LicenseType             | License role options                        | `StakeholderRegistraition` | `StakeholderRegistraition` |
| LicenseDetails          | Gender                                      | `common-masters`           | `GenderType`               |
| StakeholderDocsRequired | Documents and its drop downs                | `StakeholderRegistraition` | `StakeholderRegistraition` |

For calling the MDMS data, React Hooks are used, so that it could be shared throughout the modules. Below is the little code snippet for the MDMS call.

```
const { data, isLoading } = Digit.Hooks.obps.useMDMS(state, "StakeholderRegistraition", "TradeTypetoRoleMapping");
```

### **Localization**

Localization keys are added in the ‘_rainmaker-bpareg_’ locale module. In future, if any new labels are implemented in the OBPS - Stakeholder (Citizen) they should be pushed in the locale DB under _rainmaker-bpareg_ locale module. Below is an example of a few locale labels.

**API Call Role Action Mapping**

| [**S.No**](http://s.no)**.** | <p><strong>API</strong></p><p> </p>   | **Action id** | **Roles** |
| ---------------------------- | ------------------------------------- | ------------- | --------- |
| 1                            | `/egov-mdms-service/v1/_search`       | `954`         | `CITIZEN` |
| 2                            | `/tl-services/v1/BPAREG/_create`      |               | `CITIZEN` |
| 3                            | `/filestore/v1/files/url`             | `1528`        | `CITIZEN` |
| 4                            | `/billing-service/bill/v2/_fetchbill` | `1862`        | `CITIZEN` |
| 5                            | `/tl-calculator/billingslab/_search`  | `1684`        | `CITIZEN` |
| 6                            | `/tl-services/v1/BPAREG/_update`      |               | `CITIZEN` |
| 7                            | `/localization/messages/v1/_search`   | `1531`        | `CITIZEN` |
| 8                            | `/tl-calculator/v1/BPAREG/_getbill`   |               | `CITIZEN` |



> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)_​_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
