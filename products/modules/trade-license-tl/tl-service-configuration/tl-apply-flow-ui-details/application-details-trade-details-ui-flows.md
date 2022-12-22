# Application Details - Trade Details UI Flows

## **Objective**

Provide Employee purpose workflow actions.

The same screen is used for both application details and trade details.

Based on the conditions, we are showing the details here

example: If the application is not in an approved state and the business Service New TL, then we are showing application details otherwise we are showing trade details.

## **Application Details**

For workflow actions, please refer to the file below.

{% file src="../../../../../.gitbook/assets/apply-trade-license (1).pdf" %}
Apply Trade Licence
{% endfile %}

![](<../../../../../.gitbook/assets/image (234).png>)

File Path:[ <img src="https://github.com/fluidicon.png" alt="" data-size="line">digit-ui-internals/ApplicationDetails.js at main · egovernments/digit-ui-internals](https://github.com/egovernments/digit-ui-internals/blob/main/packages/modules/tl/src/pages/employee/ApplicationDetails.js)

## **Trade Details**

![](<../../../../../.gitbook/assets/image (130).png>)

### Timeline View

![](<../../../../../.gitbook/assets/image (176).png>)

It is common for all modules, find the path here:[ <img src="https://github.com/fluidicon.png" alt="" data-size="line">digit-ui-internals/ApplicationDetailsContent.js at main · egovernments/digit-ui-internals](https://github.com/egovernments/digit-ui-internals/blob/main/packages/modules/templates/ApplicationDetails/components/ApplicationDetailsContent.js)

The workflow is the same as Old UI only, please refer to the documentation link below.

{% file src="../../../../../.gitbook/assets/apply-trade-license (1).pdf" %}
Apply TradeLicence
{% endfile %}

## **Role Action Mapping**

|                          |                                             |                                                                       |               |
| ------------------------ | ------------------------------------------- | --------------------------------------------------------------------- | ------------- |
| [**S.NO**](http://s.no/) | **API**                                     | **ROLES**                                                             | **ACTION ID** |
| 1                        | `egov-mdms-service/v1/_search`              | `CR_PT`                                                               | `954`         |
| 2                        | `/tl-services/v1/_update`                   | `TL_APPROVER, TL_CEMP, EMPLOYEE, TL_DOC_VERIFIER, TL_FIELD_INSPECTOR` | `2029`        |
| 3                        | `/egov-workflow-v2/egov-wf/process/_search` | `EMPLOYEE`                                                            | `1730`        |
| 4                        | `/tl-services/v1/_search`                   | `EMPLOYEE`, `TL_APPROVER`, `TL_CEMP`                                  | `1687`        |
| 5                        | `/egov-hrms/employees/_search`              | `TL_APPROVER, TL_CEMP, EMPLOYEE, TL_DOC_VERIFIER, TL_FIELD_INSPECTOR` | `1752`        |
