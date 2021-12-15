---
description: New release features, enhancements, and fixes
---

# Release Notes

### Release Summary <a href="#release-summary" id="release-summary"></a>

DIGIT 2.5 is a release that has got new modules, a few functional changes, and non-functional changes.

* Functional: Property Tax Citizen Open search flow UI/UX revamp, Property Tax Employee flow UI/UX revamp, Property Tax Mutation flow UI/UX revamp, HRMS UI/UX revamp, mCollect v2 (eChallan) UI/UX revamp, Trade License Citizen & Employee UI/UX revamp, Receipt Cancellation UI/UX Revamp, WhatsApp v2 (Pay and Enhanced PGR), Workflow Auto Escalation with reference implementations in PGR, W\&S Enhancements, FSM DSS, and Standardized Reports for FSM/PT/mCollect.
* Non-functional: QA Automaton of APIs for FSM & eChallan, Product Standard Ontologies, Technical improvements, Internal Data Mart, etc.

### New ‌Feature Additions <a href="#new-feature-additions" id="new-feature-additions"></a>

|                              |                                     |                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| ---------------------------- | ----------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [**S.No**](http://s.no)**.** | **Feature**                         | **Description**                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| 1                            | Property Tax UI/UX Revamp           | <p><strong>Citizen flow</strong></p><ul><li>Open Search and Payment</li></ul><p><strong>Employee flow</strong></p><ul><li>Employee Inbox</li><li>Create Property</li><li>Search Property</li><li>Transfer of Ownership</li><li>Update Property</li><li>Property Assessment</li></ul>                                                                                                                                                                             |
| 2                            | HRMS UI/UX Revamp                   | <ul><li>Create employee</li><li>Search employee</li><li>Edit Employee</li><li>Deactivate/re-activate employee</li></ul>                                                                                                                                                                                                                                                                                                                                          |
| 3                            | Trade License UX revamp             | <ul><li>Allow citizen to create Trade License application</li><li>Allow citizen to check application status and make payment, download artefacts</li><li>Allow Employee to create Trade License application on behalf of citizen</li><li>Application processing by employees</li><li>Allow citizen to renew the existing trade licenses which are due for renewal</li><li>Allow employee to renew the existing trade license which are due for renewal</li></ul> |
| 4                            | mCollect v2 (eChallan) UI/UX Revamp | <ul><li>Challan Generation</li><li>Challan Search Employee</li><li>Total Challan Count</li><li>My Challan - Citizen</li><li>Search and Pay - Citizen</li></ul>                                                                                                                                                                                                                                                                                                   |
| 5                            | Receipt Cancellation UI/UX Revamp   | Receipt Cancellation UI/UX Revamp                                                                                                                                                                                                                                                                                                                                                                                                                                |
| 6                            | FSM DSS                             | <ul><li>SLA Compliance</li><li>Average Collections</li><li>Performance by ULB and Districts</li><li>Performance by Desludging Operator</li><li>Plant Operating Efficiency</li><li>Drill downs for Desluding and Vehicle log report</li></ul>                                                                                                                                                                                                                     |
| 7                            | Workflow Auto Escalation            | <ul><li>Configure SLA at a workflow state level</li><li>Escalate the application to a role if there is a breach in SLA</li><li>Make the application status as deemed approved or reject on breach of an SLA</li><li>Escalate the application to the next logical step in the workflow ladder if there is a breach in SLA</li></ul>                                                                                                                               |
| 8                            | Product Standardized Reports        | <p><strong>FSM</strong></p><ul><li>Daily Collection Report</li><li>Desludging Request Report</li><li>Vehicle Log Report</li></ul><p><strong>PT</strong></p><ul><li>Defaulter Report</li><li>Collection Register Report</li><li>Receipt Register Report</li></ul><p><strong>mCollect</strong></p><ul><li>Challan Register Report</li><li>Daily Collection Report</li><li>Receipt Register Report</li></ul>                                                        |

### Enhancements <a href="#enhancements" id="enhancements"></a>

|                              |                                          |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| ---------------------------- | ---------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| [**S.No**](http://s.no)**.** | **Updated Feature**                      | **Description**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| 1                            | Water & Sewerage Enhancements            | <ul><li>Bill Cancellation of latest bill</li><li>Show Due Date in Arrears breakup</li><li>Water &#x26; Sewerage Combined PDF Changes</li><li>Water &#x26; Sewerage Due Validation on PT Title Transfer</li></ul>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| 2                            | WhatsApp v2 (Pay and PGR) Enhancements   | <ul><li><p><strong>Improvements in Public Grievance Redressal Module</strong></p><ul><li>Enhancements in messaging language.</li><li>NLP Inclusion (For City &#x26; Boundary Selection).</li></ul></li><li><p><strong>Improvements in Bill Payments</strong></p><ul><li><p>Enhancements in messaging language.</p><ul><li>Inclusion of call to action buttons (for certain messages).</li></ul></li><li><p>For Linked Mobile Numbers</p><ul><li>Single-click access to bills (for PT and W&#x26;S)</li></ul></li><li><p>For Non-Linked Mobile Numbers</p><ul><li>Provision of Search &#x26; Pay (If Property/Connection Details are known).</li><li>Inclusion of Open Search Links (If Property/ Connection Details are unknown).</li></ul></li></ul></li><li><p><strong>Improvements in Payment History</strong></p><ul><li><p>Enhancements in messaging language and flow.</p><ul><li>Inclusion of call to action buttons (for certain messages).</li></ul></li><li><p>For Linked Mobile Numbers</p><ul><li>Access to view the last three payments made (for PT &#x26; W&#x26;S)</li><li>Provision to download the last three payment receipts</li></ul></li><li><p>For Non-Linked Mobile Numbers</p><ul><li>Access control to view payments history only.</li></ul></li></ul></li></ul> |
| 3                            | Bill Amendment Enhancement               | <ul><li>Additional changes in Bill Amendment screen to display current Demand</li></ul>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| 4                            | PT Enhancements                          | PT Enhancements - Fuzzy search for Name, Door number, and old PT ID (old UI)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| 5                            | QA Automaton of APIs                     | <p>APIs automation for</p><ul><li>eChallan APIs including end to end APIs automation</li><li>Bill Amendment APIs</li><li>FSM Inbox API</li></ul>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| 6                            | Other Improvements and Tech Enhancements | <ul><li>Changes in Gender to introduce Transgender and Others.</li><li>Standardization of Product ontologies for Property Tax, Water &#x26; Sewerage, Fire NOC, mCollect (eChallan), PGR, and Online Building Plan Approval.</li><li>Inbox API to support module wise inbox for UI/UX revamp.</li></ul>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| 7                            | Internal Data mart                       | Internal Data mart for PT, TL, PGR, W\&S, FSM, eChallan, OBPS, and Fire NOC modules.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| 8                            | eDCR Enhancements                        | <ul><li>River Distance: Colour code used to identify different river types.</li><li>In the basement footprint layer, captured additional dimension to define the level of the basement under the ground.</li><li>In the stilt parking layer, captured height from floor to the bottom of a beam of the stilt floor.</li></ul>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |

### ‌Document Resources and Links <a href="#document-resources-and-links" id="document-resources-and-links"></a>

#### UI Technical Documents

**Trade License UI/UX Revamp**

**Citizen**

{% content-ref url="../product/modules/trade-license-tl/tl-apply-flow-ui-details/" %}
[tl-apply-flow-ui-details](../product/modules/trade-license-tl/tl-apply-flow-ui-details/)
{% endcontent-ref %}

{% content-ref url="../product/modules/trade-license-tl/tl-apply-flow-ui-details/my-applications-ui-flow.md" %}
[my-applications-ui-flow.md](../product/modules/trade-license-tl/tl-apply-flow-ui-details/my-applications-ui-flow.md)
{% endcontent-ref %}

{% content-ref url="../product/modules/trade-license-tl/tl-apply-flow-ui-details/send-back-edit-ui-flow.md" %}
[send-back-edit-ui-flow.md](../product/modules/trade-license-tl/tl-apply-flow-ui-details/send-back-edit-ui-flow.md)
{% endcontent-ref %}

{% content-ref url="../product/modules/trade-license-tl/tl-apply-flow-ui-details/trade-license-renewal-ui-flow.md" %}
[trade-license-renewal-ui-flow.md](../product/modules/trade-license-tl/tl-apply-flow-ui-details/trade-license-renewal-ui-flow.md)
{% endcontent-ref %}

**Employee**

{% content-ref url="../product/modules/property-tax/pt-create-property-ui-details/create-application-employee-ui-ux-revamp.md" %}
[create-application-employee-ui-ux-revamp.md](../product/modules/property-tax/pt-create-property-ui-details/create-application-employee-ui-ux-revamp.md)
{% endcontent-ref %}

{% content-ref url="../product/modules/property-tax/pt-create-property-ui-details/employee-inbox-and-application-details.md" %}
[employee-inbox-and-application-details.md](../product/modules/property-tax/pt-create-property-ui-details/employee-inbox-and-application-details.md)
{% endcontent-ref %}

{% content-ref url="../product/modules/trade-license-tl/tl-apply-flow-ui-details/employee-search-application-search-license-ui-flow.md" %}
[employee-search-application-search-license-ui-flow.md](../product/modules/trade-license-tl/tl-apply-flow-ui-details/employee-search-application-search-license-ui-flow.md)
{% endcontent-ref %}

{% content-ref url="../product/modules/trade-license-tl/tl-apply-flow-ui-details/new-trade-license-ui-flow.md" %}
[new-trade-license-ui-flow.md](../product/modules/trade-license-tl/tl-apply-flow-ui-details/new-trade-license-ui-flow.md)
{% endcontent-ref %}

{% content-ref url="../product/modules/trade-license-tl/tl-apply-flow-ui-details/application-details-trade-details-ui-flows.md" %}
[application-details-trade-details-ui-flows.md](../product/modules/trade-license-tl/tl-apply-flow-ui-details/application-details-trade-details-ui-flows.md)
{% endcontent-ref %}

{% content-ref url="../product/modules/trade-license-tl/tl-apply-flow-ui-details/renew-edit-application.md" %}
[renew-edit-application.md](../product/modules/trade-license-tl/tl-apply-flow-ui-details/renew-edit-application.md)
{% endcontent-ref %}

**HRMS UI/UX Revamp**

{% content-ref url="../product/modules/hrms/hrms-employee-create-edit-ui-flow.md" %}
[hrms-employee-create-edit-ui-flow.md](../product/modules/hrms/hrms-employee-create-edit-ui-flow.md)
{% endcontent-ref %}

{% content-ref url="../product/modules/hrms/employee-activation-deactivation-ui-flow.md" %}
[employee-activation-deactivation-ui-flow.md](../product/modules/hrms/employee-activation-deactivation-ui-flow.md)
{% endcontent-ref %}

{% content-ref url="../product/modules/hrms/employee-details-ui-flow.md" %}
[employee-details-ui-flow.md](../product/modules/hrms/employee-details-ui-flow.md)
{% endcontent-ref %}

{% content-ref url="../product/modules/hrms/search-employee-by-multiple-criteria-ui-flow.md" %}
[search-employee-by-multiple-criteria-ui-flow.md](../product/modules/hrms/search-employee-by-multiple-criteria-ui-flow.md)
{% endcontent-ref %}

{% content-ref url="../product/modules/hrms/employees-count-ui-flow.md" %}
[employees-count-ui-flow.md](../product/modules/hrms/employees-count-ui-flow.md)
{% endcontent-ref %}

**Receipt cancellation UI/UX Revamp**

{% content-ref url="../product/modules/receipt-cancellation-ui-flow/" %}
[receipt-cancellation-ui-flow](../product/modules/receipt-cancellation-ui-flow/)
{% endcontent-ref %}

{% content-ref url="../product/modules/receipt-cancellation-ui-flow/view-receipt-cancel-ui-flow.md" %}
[view-receipt-cancel-ui-flow.md](../product/modules/receipt-cancellation-ui-flow/view-receipt-cancel-ui-flow.md)
{% endcontent-ref %}

**Bill Cancellation**

{% content-ref url="../product/modules/current-bill-cancellation-ui-flow/" %}
[current-bill-cancellation-ui-flow](../product/modules/current-bill-cancellation-ui-flow/)
{% endcontent-ref %}

{% content-ref url="../product/modules/current-bill-cancellation-ui-flow/bill-details-ui-flow.md" %}
[bill-details-ui-flow.md](../product/modules/current-bill-cancellation-ui-flow/bill-details-ui-flow.md)
{% endcontent-ref %}

{% content-ref url="../product/modules/current-bill-cancellation-ui-flow/cancel-bill-ui-flow.md" %}
[cancel-bill-ui-flow.md](../product/modules/current-bill-cancellation-ui-flow/cancel-bill-ui-flow.md)
{% endcontent-ref %}

**mCollect v2 (eChallan) UI/UX Revamp**

{% content-ref url="../product/modules/mcollect-mcs/echallan-ui-details/mcollect-ui-flow.md" %}
[mcollect-ui-flow.md](../product/modules/mcollect-mcs/echallan-ui-details/mcollect-ui-flow.md)
{% endcontent-ref %}

{% content-ref url="../product/modules/mcollect-mcs/echallan-ui-details/update-cancel-challan-ui-flow.md" %}
[update-cancel-challan-ui-flow.md](../product/modules/mcollect-mcs/echallan-ui-details/update-cancel-challan-ui-flow.md)
{% endcontent-ref %}

{% content-ref url="../product/modules/mcollect-mcs/echallan-ui-details/search-and-pay-challan.md" %}
[search-and-pay-challan.md](../product/modules/mcollect-mcs/echallan-ui-details/search-and-pay-challan.md)
{% endcontent-ref %}

{% content-ref url="../product/modules/mcollect-mcs/echallan-ui-details/challan-creation.md" %}
[challan-creation.md](../product/modules/mcollect-mcs/echallan-ui-details/challan-creation.md)
{% endcontent-ref %}

**Workflow Auto Escalation**

{% content-ref url="../product/modules/auto-escalation-ui-flow.md" %}
[auto-escalation-ui-flow.md](../product/modules/auto-escalation-ui-flow.md)
{% endcontent-ref %}

**Property Tax UI/UX Revamp**

**Citizen**

{% content-ref url="../product/modules/property-tax/pt-create-property-ui-details/" %}
[pt-create-property-ui-details](../product/modules/property-tax/pt-create-property-ui-details/)
{% endcontent-ref %}

{% content-ref url="../product/modules/property-tax/pt-create-property-ui-details/edit-update-property.md" %}
[edit-update-property.md](../product/modules/property-tax/pt-create-property-ui-details/edit-update-property.md)
{% endcontent-ref %}

{% content-ref url="../product/modules/property-tax/pt-create-property-ui-details/property-tax-my-applications.md" %}
[property-tax-my-applications.md](../product/modules/property-tax/pt-create-property-ui-details/property-tax-my-applications.md)
{% endcontent-ref %}

{% content-ref url="../product/modules/property-tax/pt-create-property-ui-details/property-tax-my-properties.md" %}
[property-tax-my-properties.md](../product/modules/property-tax/pt-create-property-ui-details/property-tax-my-properties.md)
{% endcontent-ref %}

**Employee**

{% content-ref url="../product/modules/property-tax/pt-create-property-ui-details/employee-edit-application-flow.md" %}
[employee-edit-application-flow.md](../product/modules/property-tax/pt-create-property-ui-details/employee-edit-application-flow.md)
{% endcontent-ref %}

{% content-ref url="../product/modules/property-tax/pt-create-property-ui-details/create-application-employee-ui-ux-revamp.md" %}
[create-application-employee-ui-ux-revamp.md](../product/modules/property-tax/pt-create-property-ui-details/create-application-employee-ui-ux-revamp.md)
{% endcontent-ref %}

{% content-ref url="../product/modules/property-tax/pt-create-property-ui-details/employee-search-property-property-details-page-and-assessment.md" %}
[employee-search-property-property-details-page-and-assessment.md](../product/modules/property-tax/pt-create-property-ui-details/employee-search-property-property-details-page-and-assessment.md)
{% endcontent-ref %}

{% content-ref url="../product/modules/property-tax/pt-create-property-ui-details/employee-inbox-and-application-details.md" %}
[employee-inbox-and-application-details.md](../product/modules/property-tax/pt-create-property-ui-details/employee-inbox-and-application-details.md)
{% endcontent-ref %}

**Mutation**

{% content-ref url="../product/modules/property-tax/pt-create-property-ui-details/employee-mutation-ownership-transfer.md" %}
[employee-mutation-ownership-transfer.md](../product/modules/property-tax/pt-create-property-ui-details/employee-mutation-ownership-transfer.md)
{% endcontent-ref %}

{% content-ref url="../product/modules/property-tax/pt-create-property-ui-details/citizen-mutation-flow.md" %}
[citizen-mutation-flow.md](../product/modules/property-tax/pt-create-property-ui-details/citizen-mutation-flow.md)
{% endcontent-ref %}

**DSS**

{% content-ref url="../product/modules/dss-ui-flow.md" %}
[dss-ui-flow.md](../product/modules/dss-ui-flow.md)
{% endcontent-ref %}

{% content-ref url="../product/modules/faecal-sludge-management-fsm/fsm-service-configuration/fsm-implementation-configuration.md" %}
[fsm-implementation-configuration.md](../product/modules/faecal-sludge-management-fsm/fsm-service-configuration/fsm-implementation-configuration.md)
{% endcontent-ref %}

#### Backend Service Documents

{% file src="../.gitbook/assets/egov-hrms (1).pdf" %}
eGov HRMS
{% endfile %}

{% content-ref url="../product/modules/e-challan-service/" %}
[e-challan-service](../product/modules/e-challan-service/)
{% endcontent-ref %}

{% content-ref url="../configuration/configure-digit/configuring-digit-services/configuring-workflows/workflow-auto-escalation.md" %}
[workflow-auto-escalation.md](../configuration/configure-digit/configuring-digit-services/configuring-workflows/workflow-auto-escalation.md)
{% endcontent-ref %}

{% content-ref url="../configuration/configure-digit/services-overview/core-services/nlp-engine-service.md" %}
[nlp-engine-service.md](../configuration/configure-digit/services-overview/core-services/nlp-engine-service.md)
{% endcontent-ref %}

{% content-ref url="../configuration/configure-digit/services-overview/core-services/xstate-core-chatbot/" %}
[xstate-core-chatbot](../configuration/configure-digit/services-overview/core-services/xstate-core-chatbot/)
{% endcontent-ref %}

{% content-ref url="../configuration/configure-digit/services-overview/core-services/xstate-core-chatbot/xstate-chatbot-integration-document.md" %}
[xstate-chatbot-integration-document.md](../configuration/configure-digit/services-overview/core-services/xstate-core-chatbot/xstate-chatbot-integration-document.md)
{% endcontent-ref %}

{% content-ref url="../configuration/configure-digit/services-overview/core-services/xstate-core-chatbot/xstate-chatbot-message-localisation.md" %}
[xstate-chatbot-message-localisation.md](../configuration/configure-digit/services-overview/core-services/xstate-core-chatbot/xstate-chatbot-message-localisation.md)
{% endcontent-ref %}

{% content-ref url="../configuration/configure-digit/services-overview/business-services/collection-service/collection-service-v2.md" %}
[collection-service-v2.md](../configuration/configure-digit/services-overview/business-services/collection-service/collection-service-v2.md)
{% endcontent-ref %}

{% content-ref url="../product/modules/faecal-sludge-management-fsm/fsm-service-configuration/fsm-services.md" %}
[fsm-services.md](../product/modules/faecal-sludge-management-fsm/fsm-service-configuration/fsm-services.md)
{% endcontent-ref %}

{% content-ref url="../product/modules/faecal-sludge-management-fsm/fsm-service-configuration/fsm-vehicle-registry-v1.0.md" %}
[fsm-vehicle-registry-v1.0.md](../product/modules/faecal-sludge-management-fsm/fsm-service-configuration/fsm-vehicle-registry-v1.0.md)
{% endcontent-ref %}

{% content-ref url="../product/modules/faecal-sludge-management-fsm/fsm-service-configuration/fsm-vendor-registry-v1.0.md" %}
[fsm-vendor-registry-v1.0.md](../product/modules/faecal-sludge-management-fsm/fsm-service-configuration/fsm-vendor-registry-v1.0.md)
{% endcontent-ref %}

{% content-ref url="../product/modules/faecal-sludge-management-fsm/fsm-service-configuration/legacy-re-indexing-the-fsm-data.md" %}
[legacy-re-indexing-the-fsm-data.md](../product/modules/faecal-sludge-management-fsm/fsm-service-configuration/legacy-re-indexing-the-fsm-data.md)
{% endcontent-ref %}

{% content-ref url="../configuration/configure-digit/services-overview/municipal-services/turn-io-adapter.md" %}
[turn-io-adapter.md](../configuration/configure-digit/services-overview/municipal-services/turn-io-adapter.md)
{% endcontent-ref %}

{% content-ref url="../product/modules/property-tax/property-tax-service/fuzzy-search/" %}
[fuzzy-search](../product/modules/property-tax/property-tax-service/fuzzy-search/)
{% endcontent-ref %}

{% content-ref url="../product/modules/property-tax/property-tax-service/fuzzy-search/fuzzy-search-reindexing.md" %}
[fuzzy-search-reindexing.md](../product/modules/property-tax/property-tax-service/fuzzy-search/fuzzy-search-reindexing.md)
{% endcontent-ref %}

{% content-ref url="../product/modules/faecal-sludge-management-fsm/fsm-service-configuration/fsm-dss-technical-documentation.md" %}
[fsm-dss-technical-documentation.md](../product/modules/faecal-sludge-management-fsm/fsm-service-configuration/fsm-dss-technical-documentation.md)
{% endcontent-ref %}

{% content-ref url="../configuration/configure-digit/services-overview/municipal-services/inbox-service.md" %}
[inbox-service.md](../configuration/configure-digit/services-overview/municipal-services/inbox-service.md)
{% endcontent-ref %}

{% content-ref url="../configuration/configure-digit/configuring-digit-services/digit-internal-datamart-deployment-steps.md" %}
[digit-internal-datamart-deployment-steps.md](../configuration/configure-digit/configuring-digit-services/digit-internal-datamart-deployment-steps.md)
{% endcontent-ref %}

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)\_\_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_ ](https://egov.org.in)_is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
