---
description: New release features, enhancements, and fixes
---

# Release Notes

## Release Summary <a href="#release-summary" id="release-summary"></a>

DIGIT 2.4 is the latest release that has got new modules, a few functional changes, and non-functional changes.

* Functional: eChallan module, WhatsApp Bill Payment, Property Tax Citizen flow UI/UX revamp Arrears Breakup in Property Tax Due, and Send back to Citizen feature in Fire NOC.
* Non-functional: Platform Security Audit fixes, Hindi Localization, QA Automaton of APIs, and Technical improvements.

## New ‌Feature Additions <a href="#new-feature-additions" id="new-feature-additions"></a>

| **S.No.** | **Feature**                                                                   | **Description**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| --------- | ----------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 1         | eChallan module                                                               | <ol><li>Generate <strong>e-challans / bill</strong> for all miscellaneous / Adhoc services which citizens avail from ULBs</li><li>Edit/Cancel e-challan/bill</li><li>The ability for ULBs to Notify citizens about the outstanding payments - Online(email &#x26; SMS) and offline.</li><li>Enable Digital payments for citizens - QR code, payment link in notifications, etc.</li></ol>                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| 2         | WhatsApp Bill Payment and PGR v2 integration with redesigned Chatbot (xState) | <p><strong>Bill Payment:</strong></p><ol><li><p><strong>Search and View Bill `</strong></p><ol><li>View my Bills</li><li><p>Search Bills Based on</p><ol><li>Consumer Number</li><li>Application Number</li><li>Mobile Number etc</li></ol></li><li><p>View Bill</p><ol><li>Amount Due</li><li>Bill copy (PDF)</li></ol></li></ol></li><li><p><strong>Payment</strong></p><ol><li>Pay bills through quick payment links</li><li>Payment confirmation/failure notification</li><li>Payment receipt (PDF) on successful payment</li></ol></li><li><p><strong>Multi-Language Support</strong></p><ol><li>Hindi Localization (For Chats)</li></ol></li></ol><p><strong>PGR:</strong></p><ol><li>Geo-Location tagging</li><li>Two steps complaint category and type</li><li>Hindi Localization (For Chats)</li><li>PGR v1 &#x26; v2 support</li></ol> |
| 3         | Property Tax Citizen flow UI/UX revamp                                        | <p>Updated workflows and user interface changes in the following business cases -</p><ul><li>PT - Quick Pay</li><li>Create Property</li><li>My Properties</li><li>My Applications</li></ul>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |

## Enhancements <a href="#enhancements" id="enhancements"></a>

| **S.No.** | **Updated Feature**           | **Description**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| --------- | ----------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1         | Fire NOC Enhancements         | Send back to Citizen in Fire NOC                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| 2         | Property Tax Enhancements     | Arrears Breakup in Property Tax Due                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| 3         | Hindi Localization            | Hindi Localization of all labels, messages, notifications, and MDMS drop-down data of all the modules                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| 4         | QA Automaton of APIs          | <p>APIs automation for</p><ul><li>Core Services</li><li>Business Services</li><li><p>Municipal Services</p><ul><li>End to End APIs automation for Property Tax, Trade License, mCollect, Water &#x26; Sewerage, Fire NOC, Building Plan Approval, FSM, and PGR.</li></ul></li><li>Here is the <a href="qa-automation-release-notes.md">document</a> with the details of services automated and README documentation which details the detailed steps to execute the automation</li></ul>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| 5         | Platform Security Audit fixes | <p>Listed below are the security vulnerabilities identified as part of the security audit. Few of them are as per design and justification is provided for these. Others are fixed at the code level.</p><ol><li>Privilege Escalation</li><li>Failure to restrict URL Access</li><li>Insecure direct object references (IDOR)</li><li>Malicious file upload leads to Cross Site scripting</li><li>Improper Authentication</li><li>Missing Account Lockout</li><li>Request Throttling Attack</li><li>Weak Encoding Mechanism</li><li>Sensitive Information in URL</li><li>Lack of Automatic Session Expiration</li><li>Concurrent Session</li><li>Improper Error Handling</li><li>Improper Input Validation</li><li>Mail Command Injection</li><li>Use of hardcoded credentials</li><li>Use of sensitive information into configuration file</li><li>Exclude unsanitized user input from format strings</li><li>HTTP Parameter Pollution</li><li>Standard pseudo-random number generators cannot withstand cryptographic attacks</li><li>Weak cryptographic hash</li><li>Insecure SSL configuration</li><li>Improper Neutralization of CRLF Sequences in HTTP Header</li><li>Avoid Capturing Java.Lang Security Exception</li><li>Always normalize system inputs</li><li>Avoid the Command Throws within Finally</li><li>Close Input and Output resources in finally block</li><li>Cross Site Request Forgery</li><li>Cross Site Scripting - Stored</li><li>Insufficient Cookie Attributes</li><li>Code Injection</li><li>Exclude unsanitized user input from format strings</li><li>Avoid data submissions to non-editable fields</li><li>Potential Infinite Loops</li><li>Avoid dangerous J2EE API, use replacements from security-focused libraries (like OWASP ESAPI)</li><li>Do not allow external input to control resource identifiers</li><li>The setter method for an identifier property (id or composite-id) should be private</li></ol><p>Here are the security fixes guidelines as a <a href="../digit-support/security-guidelines-handbook.md">handbook</a> for best practices and guidelines.</p> |
| 6         | Technical Improvements        | <ul><li>PDF service refactoring for Localization API calls optimization</li><li>Timezone configuration support for all the services</li><li>Standard product Workflow bundling as part of the product</li></ul>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| 7         | eDCR Enhancements             | <ol><li>Enhanced Door, to support door widths with color code. The color code is used to identify the type of door</li><li>Fix of security audit issues</li><li>Cleanup unused code and database tables</li></ol>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| 8         | Finance                       | <ol><li>Hard coded sub domain formation logic changed, preparing dynamic sub domain url by reading env from the configuration</li><li>Fixed the security audit issues</li></ol>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |

## ‌Document Resources and Links <a href="#document-resources-and-links" id="document-resources-and-links"></a>

### UI Technical Documents

{% content-ref url="../product/modules/mcollect-mcs/echallan-ui-details/" %}
[echallan-ui-details](../product/modules/mcollect-mcs/echallan-ui-details/)
{% endcontent-ref %}

{% content-ref url="../product/modules/mcollect-mcs/echallan-ui-details/edit-cancel-challan.md" %}
[edit-cancel-challan.md](../product/modules/mcollect-mcs/echallan-ui-details/edit-cancel-challan.md)
{% endcontent-ref %}

{% content-ref url="../product/modules/mcollect-mcs/echallan-ui-details/search-and-pay-challan.md" %}
[search-and-pay-challan.md](../product/modules/mcollect-mcs/echallan-ui-details/search-and-pay-challan.md)
{% endcontent-ref %}

{% content-ref url="../product/modules/property-tax/property-tax-service/" %}
[property-tax-service](../product/modules/property-tax/property-tax-service/)
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

{% content-ref url="../product/modules/property-tax/pt-create-property-ui-details/property-tax-quick-pay-for-citizen.md" %}
[property-tax-quick-pay-for-citizen.md](../product/modules/property-tax/pt-create-property-ui-details/property-tax-quick-pay-for-citizen.md)
{% endcontent-ref %}

{% file src="../.gitbook/assets/common-pay-config (1).pdf" %}
Common Pay Configuration
{% endfile %}

{% file src="../.gitbook/assets/fire-noc-create.pdf" %}
Fire NOC Create
{% endfile %}

{% file src="../.gitbook/assets/digit-ui-manual (1).pdf" %}
DIGIT UI Manual
{% endfile %}

### Backend Service Documents

{% content-ref url="../configuration/configure-digit/services-overview/core-services/xstate-core-chatbot/" %}
[xstate-core-chatbot](../configuration/configure-digit/services-overview/core-services/xstate-core-chatbot/)
{% endcontent-ref %}

{% content-ref url="../configuration/configure-digit/services-overview/core-services/xstate-core-chatbot/xstate-chatbot-integration-document.md" %}
[xstate-chatbot-integration-document.md](../configuration/configure-digit/services-overview/core-services/xstate-core-chatbot/xstate-chatbot-integration-document.md)
{% endcontent-ref %}

{% content-ref url="../configuration/configure-digit/services-overview/core-services/xstate-core-chatbot/xstate-chatbot-message-localisation.md" %}
[xstate-chatbot-message-localisation.md](../configuration/configure-digit/services-overview/core-services/xstate-core-chatbot/xstate-chatbot-message-localisation.md)
{% endcontent-ref %}

{% content-ref url="../product/modules/e-challan-service/" %}
[e-challan-service](../product/modules/e-challan-service/)
{% endcontent-ref %}

{% content-ref url="../product/modules/e-challan-service/echallan-calculator-services.md" %}
[echallan-calculator-services.md](../product/modules/e-challan-service/echallan-calculator-services.md)
{% endcontent-ref %}

{% content-ref url="../product/modules/faecal-sludge-management-fsm/fsm-service-configuration/fsm-services.md" %}
[fsm-services.md](../product/modules/faecal-sludge-management-fsm/fsm-service-configuration/fsm-services.md)
{% endcontent-ref %}

### Tech Enablement Documents

{% content-ref url="../configuration/configure-digit/services-overview/business-services/appropriation-service.md" %}
[appropriation-service.md](../configuration/configure-digit/services-overview/business-services/appropriation-service.md)
{% endcontent-ref %}

{% content-ref url="../configuration/configure-digit/services-overview/business-services/billing-service/" %}
[billing-service](../configuration/configure-digit/services-overview/business-services/billing-service/)
{% endcontent-ref %}

{% content-ref url="../configuration/configure-digit/services-overview/business-services/billing-service/bill-amendment-service-configuration.md" %}
[bill-amendment-service-configuration.md](../configuration/configure-digit/services-overview/business-services/billing-service/bill-amendment-service-configuration.md)
{% endcontent-ref %}

{% content-ref url="../configuration/configure-digit/services-overview/business-services/collection-service/" %}
[collection-service](../configuration/configure-digit/services-overview/business-services/collection-service/)
{% endcontent-ref %}

{% content-ref url="../configuration/configure-digit/services-overview/business-services/billing-collection-integration.md" %}
[billing-collection-integration.md](../configuration/configure-digit/services-overview/business-services/billing-collection-integration.md)
{% endcontent-ref %}

{% content-ref url="../configuration/configure-digit/services-overview/business-services/dashboard-analytics-backend.md" %}
[dashboard-analytics-backend.md](../configuration/configure-digit/services-overview/business-services/dashboard-analytics-backend.md)
{% endcontent-ref %}

{% content-ref url="../configuration/configure-digit/services-overview/business-services/dss-technical-documentation.md" %}
[dss-technical-documentation.md](../configuration/configure-digit/services-overview/business-services/dss-technical-documentation.md)
{% endcontent-ref %}

{% content-ref url="../configuration/configure-digit/services-overview/business-services/dss-dashboard-technical-document-for-ui.md" %}
[dss-dashboard-technical-document-for-ui.md](../configuration/configure-digit/services-overview/business-services/dss-dashboard-technical-document-for-ui.md)
{% endcontent-ref %}

{% content-ref url="../configuration/configure-digit/services-overview/business-services/dss-features-enhancements.md" %}
[dss-features-enhancements.md](../configuration/configure-digit/services-overview/business-services/dss-features-enhancements.md)
{% endcontent-ref %}

{% content-ref url="../configuration/configure-digit/services-overview/business-services/technical-script-steps-for-migration-process.md" %}
[technical-script-steps-for-migration-process.md](../configuration/configure-digit/services-overview/business-services/technical-script-steps-for-migration-process.md)
{% endcontent-ref %}

{% content-ref url="../product/modules/property-tax/property-tax-service/" %}
[property-tax-service](../product/modules/property-tax/property-tax-service/)
{% endcontent-ref %}

{% content-ref url="../product/modules/water-and-sewerage/water-services/" %}
[water-services](../product/modules/water-and-sewerage/water-services/)
{% endcontent-ref %}

{% content-ref url="../product/modules/water-and-sewerage/water-services/water-calculator-service.md" %}
[water-calculator-service.md](../product/modules/water-and-sewerage/water-services/water-calculator-service.md)
{% endcontent-ref %}

{% content-ref url="../product/modules/water-and-sewerage/water-services/sewerage-service.md" %}
[sewerage-service.md](../product/modules/water-and-sewerage/water-services/sewerage-service.md)
{% endcontent-ref %}

{% content-ref url="../product/modules/water-and-sewerage/water-services/sewerage-calculator-service.md" %}
[sewerage-calculator-service.md](../product/modules/water-and-sewerage/water-services/sewerage-calculator-service.md)
{% endcontent-ref %}

{% content-ref url="../product/modules/fire-noc/fire-noc-service/" %}
[fire-noc-service](../product/modules/fire-noc/fire-noc-service/)
{% endcontent-ref %}

{% content-ref url="../product/modules/fire-noc/fire-noc-service/fire-noc-calculator-service.md" %}
[fire-noc-calculator-service.md](../product/modules/fire-noc/fire-noc-service/fire-noc-calculator-service.md)
{% endcontent-ref %}

{% content-ref url="../product/modules/trade-license-tl/tl-service-configuration/" %}
[tl-service-configuration](../product/modules/trade-license-tl/tl-service-configuration/)
{% endcontent-ref %}

{% content-ref url="../product/modules/trade-license-tl/tl-service-configuration/trade-license-calculator.md" %}
[trade-license-calculator.md](../product/modules/trade-license-tl/tl-service-configuration/trade-license-calculator.md)
{% endcontent-ref %}

{% content-ref url="../configuration/configure-digit/qa-automation/automation-framework-knowledge-base.md" %}
[automation-framework-knowledge-base.md](../configuration/configure-digit/qa-automation/automation-framework-knowledge-base.md)
{% endcontent-ref %}

{% content-ref url="../configuration/configure-digit/qa-automation/jenkins-setup-for-automation.md" %}
[jenkins-setup-for-automation.md](../configuration/configure-digit/qa-automation/jenkins-setup-for-automation.md)
{% endcontent-ref %}

{% content-ref url="../configuration/configure-digit/qa-automation/automation-test-tags.md" %}
[automation-test-tags.md](../configuration/configure-digit/qa-automation/automation-test-tags.md)
{% endcontent-ref %}

{% content-ref url="../configuration/configure-digit/qa-automation/automation-test-reporting.md" %}
[automation-test-reporting.md](../configuration/configure-digit/qa-automation/automation-test-reporting.md)
{% endcontent-ref %}

{% content-ref url="../digit-support/security-guidelines-handbook.md" %}
[security-guidelines-handbook.md](../digit-support/security-guidelines-handbook.md)
{% endcontent-ref %}

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)\_\_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_ ](https://egov.org.in/)_is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
