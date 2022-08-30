# OBPS BPA / OCBPA Citizen

## Objective

To provide the facility for the citizen user to view the application details, updating the BPA application state and make the payment.

![BPA Home Card](<../../../../../.gitbook/assets/Screenshot from 2021-09-30 10-20-48 (3).png>)

Users can review the list of applications and their status registered using their mobile number on the My Applications page. Each Application initially displays the Application Number, Application Type, Service Type, status, SLA with the View Details option.

## **View Application By Citizen**

Click on the View Applications by Citizen link routes users to the My Applications screen.\
The screen provides BPA, OC-BPA and stakeholder registration applications and details.\
The BPA search API and the Stakeholder Registration search APIs are called and the application cards are visible after getting the response from the APIs.

![](../../../../../.gitbook/assets/image-20211207-092617.png)

&#x20;File Path

{% embed url="https://github.com/egovernments/DIGIT-Dev/blob/develop/frontend/micro-ui/web/micro-ui-internals/packages/modules/obps/src/pages/citizen/MyApplication/index.js" %}

Click on the View Details button. It routes users to the application details screen.\
\
**1. BPA Application Details**

Clicking on the BPA/OC BPA application card routes users to the BPA application details page. The application details page displays the details of the application and also showcases all the actions that can be taken on the application.

![](../../../../../.gitbook/assets/image-20211207-092333.png) ![](../../../../../.gitbook/assets/image-20211207-092355.png) ![](../../../../../.gitbook/assets/image-20211207-092417.png)

&#x20;

Clicking on the Action button provides the citizen users with the actions list. Clicking on any one of the options opens a popup window. Users can enter the comments and upload documents. Clicking on the Submit or Forward button triggers the Update API call.

File Path

{% embed url="https://github.com/egovernments/DIGIT-Dev/blob/develop/frontend/micro-ui/web/micro-ui-internals/packages/modules/obps/src/pages/citizen/BpaApplicationDetail/index.js" %}

### **Send Back To Citizen**

When employees click on the Send Back to Citizen button, the applications are routed back to the My Applications list of the citizen. The Application Details screen allows users to make the required changes. The forward action button routes the citizen to the Summary screen. Users can attach the documents and submit the application.&#x20;

![
](../../../../../.gitbook/assets/image-20211207-095351.png)

![](../../../../../.gitbook/assets/image-20211207-095434.png)

File Path

{% embed url="https://github.com/egovernments/DIGIT-Dev/blob/develop/frontend/micro-ui/web/micro-ui-internals/packages/modules/obps/src/pages/citizen/BPASendBackToCitizen/index.js" %}

### **Download**&#x20;

Citizens can download the receipts which include Application Fee, Sanction Fee, Permit order, Revocation pdf, Comparison report etc based on the conditions.&#x20;

File Path

{% embed url="https://github.com/egovernments/DIGIT-Dev/blob/develop/frontend/micro-ui/web/micro-ui-internals/packages/modules/obps/src/pages/citizen/BpaApplicationDetail/index.js" %}

## **Stakeholder Registration Application Details**

Clicking on the Stakeholder Application card routes the user to the stakeholder application details. The application details page displays the details of the application and also showcases all the actions that can be taken on the application.

![](../../../../../.gitbook/assets/image-20211207-093009.png)

File Path

{% embed url="https://github.com/egovernments/DIGIT-Dev/blob/develop/frontend/micro-ui/web/micro-ui-internals/packages/modules/obps/src/pages/citizen/ApplicationDetail/index.js" %}

### **Timeline Component**

The Timeline component is present at the end of the application details and provides information on the current status.

![](../../../../../.gitbook/assets/image-20211209-054317.png)

## **Technical Implementation Details**

All the screens have been developed using the new-UI structure followed previously in FSM, PGR, PT and TL.\


**OBPS Hooks Details**

File Path&#x20;

{% embed url="https://github.com/egovernments/DIGIT-Dev/blob/develop/frontend/micro-ui/web/micro-ui-internals/packages/modules/obps/src/pages/citizen/BpaApplicationDetail/index.js" %}

OBPS Search API Hook

![](../../../../../.gitbook/assets/image-20211209-054939.png)

OBPS Update API Hook

![](../../../../../.gitbook/assets/image-20211209-055050.png)

OBPS WorkFlow API Hook

![](../../../../../.gitbook/assets/image-20211209-055128.png)

OBPS MDMS Hooks

![](../../../../../.gitbook/assets/image-20211209-055242.png)

Collection Services Hooks(For Receipts and Amount display)

![](../../../../../.gitbook/assets/image-20211209-055333.png)

**Stakeholder Hooks**\


File Path

{% embed url="https://github.com/egovernments/DIGIT-Dev/blob/develop/frontend/micro-ui/web/micro-ui-internals/packages/modules/obps/src/pages/citizen/ApplicationDetail/index.js" %}

Search Hook

![](../../../../../.gitbook/assets/image-20211209-055531.png)

MDMS Hook

![](../../../../../.gitbook/assets/image-20211209-055600.png)

Collection Service Hook(For Receipts and Amount display)

![](../../../../../.gitbook/assets/image-20211209-055622.png)

## **Localisation**

Localisation keys are added under the ‘_rainmaker-bpa_’ and ‘rainmaker-bpareg’ locale modules. In future, if any new labels are implemented in the OBPS - Architect (Citizen) they should also be pushed to the locale DB under '_rainmaker-bpa'_ locale module. Below is an example of a few locale labels.&#x20;

## **API Call Role Action Mapping**

| [**S.No**](http://s.no/)**.** | <p><strong>API</strong></p><p> </p>                       | **Action id** | **Roles** |
| ----------------------------- | --------------------------------------------------------- | ------------- | --------- |
| 1                             | `/egov-mdms-service/v1/_search`                           | `954`         | `CITIZEN` |
| 2                             | `/edcr/rest/dcr/scrutinydetails`                          |               | `CITIZEN` |
| 3                             | `/filestore/v1/files/url`                                 | `1528`        | `CITIZEN` |
| 4                             | `/billing-service/bill/v2/_fetchbill`                     | `1862`        | `CITIZEN` |
| 5                             | `collection-services/payments/{businessService}/_search/` | `1864`        | `CITIZEN` |
| 6                             | `/noc-services/v1/noc/_search`                            |               | `CITIZEN` |
| 7                             | `/localization/messages/v1/_search`                       | `1531`        | `CITIZEN` |
| 8                             | `/noc-services/v1/noc/_update`                            |               | `CITIZEN` |
| 9                             | `/bpa-services/v1/bpa/_update`                            |               | `CITIZEN` |
| 10                            | `/bpa-services/v1/bpa/_search`                            |               | `CITIZEN` |
| 11                            | `/egov-workflow-v2/egov-wf/process/_search`               |               | `CITIZEN` |
| 12                            | `/egov-workflow-v2/egov-wf/businessservice/_search`       |               | `CITIZEN` |
| 13                            | `/tl-services/v1/BPAREG/_search`                          |               | `CITIZEN` |

\


> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)_​_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in/) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
