---
description: 'New release features, enhancements, and fixes'
---

# Release Notes

## Release Summary <a id="Release-Summary"></a>

DIGIT 2.4 is a release that has got new modules, a few functional changes, and non-functional changes.

* Functional: eChallan module, WhatsApp Bill Payment, Property Tax Citizen flow UI/UX revamp Arrears Breakup in Property Tax Due, and Send back to Citizen feature in Fire NOC.
* Non-functional: Platform Security Audit fixes, Hindi Localization, QA Automaton of APIs, and Technical improvements.

## New ‌Feature Additions <a id="New-&#x200C;Feature-Additions"></a>

<table>
  <thead>
    <tr>
      <th style="text-align:left"><b>S.No.</b>
      </th>
      <th style="text-align:left"><b>Feature</b>
      </th>
      <th style="text-align:left"><b>Description</b>
      </th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">1</td>
      <td style="text-align:left">eChallan module</td>
      <td style="text-align:left">
        <ol>
          <li>Generate <b>e-challans / bill</b> for all miscellaneous / Adhoc services
            which citizens avail from ULBs</li>
          <li>Edit/Cancel e-challan/bill</li>
          <li>The ability for ULBs to Notify citizens about the outstanding payments
            - Online(email &amp; SMS) and offline.</li>
          <li>Enable Digital payments for citizens - QR code, payment link in notifications,
            etc.</li>
        </ol>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">2</td>
      <td style="text-align:left">WhatsApp Bill Payment and PGR v2 integration with redesigned Chatbot (xState)</td>
      <td
      style="text-align:left">
        <p><b>Bill Payment:</b>
        </p>
        <ol>
          <li><b>Search and View Bill `</b>
            <ol>
              <li>View my Bills</li>
              <li>Search Bills Based on
                <ol>
                  <li>Consumer Number</li>
                  <li>Application Number</li>
                  <li>Mobile Number etc</li>
                </ol>
              </li>
              <li>View Bill
                <ol>
                  <li>Amount Due</li>
                  <li>Bill copy (PDF)</li>
                </ol>
              </li>
            </ol>
          </li>
          <li><b>Payment</b>
            <ol>
              <li>Pay bills through quick payment links</li>
              <li>Payment confirmation/failure notification</li>
              <li>Payment receipt (PDF) on successful payment</li>
            </ol>
          </li>
          <li><b>Multi-Language Support</b>
            <ol>
              <li>Hindi Localization (For Chats)</li>
            </ol>
          </li>
        </ol>
        <p><b>PGR:</b>
        </p>
        <ol>
          <li>Geo-Location tagging</li>
          <li>Two steps complaint category and type</li>
          <li>Hindi Localization (For Chats)</li>
          <li>PGR v1 &amp; v2 support</li>
        </ol>
        </td>
    </tr>
    <tr>
      <td style="text-align:left">3</td>
      <td style="text-align:left">Property Tax Citizen flow UI/UX revamp</td>
      <td style="text-align:left">
        <p>Updated workflows and user interface changes in the following business
          cases -</p>
        <ul>
          <li>PT - Quick Pay</li>
          <li>Create Property</li>
          <li>My Properties</li>
          <li>My Applications</li>
        </ul>
      </td>
    </tr>
  </tbody>
</table>

## Enhancements <a id="Enhancements"></a>

<table>
  <thead>
    <tr>
      <th style="text-align:left"><b>S.No.</b>
      </th>
      <th style="text-align:left"><b>Updated Feature</b>
      </th>
      <th style="text-align:left"><b>Description</b>
      </th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">1</td>
      <td style="text-align:left">Fire NOC Enhancements</td>
      <td style="text-align:left">Send back to Citizen in Fire NOC</td>
    </tr>
    <tr>
      <td style="text-align:left">2</td>
      <td style="text-align:left">Property Tax Enhancements</td>
      <td style="text-align:left">Arrears Breakup in Property Tax Due</td>
    </tr>
    <tr>
      <td style="text-align:left">3</td>
      <td style="text-align:left">Hindi Localization</td>
      <td style="text-align:left">Hindi Localization of all labels, messages, notifications, and MDMS drop-down
        data of all the modules</td>
    </tr>
    <tr>
      <td style="text-align:left">4</td>
      <td style="text-align:left">QA Automaton of APIs</td>
      <td style="text-align:left">
        <p>APIs automation for</p>
        <ul>
          <li>Core Services</li>
          <li>Business Services</li>
          <li>Municipal Services
            <ul>
              <li>End to End APIs automation for Property Tax, Trade License, mCollect,
                Water &amp; Sewerage, Fire NOC, Building Plan Approval, FSM, and PGR.</li>
            </ul>
          </li>
          <li>Here is the<a href="qa-automation-release-notes.md"> document </a>with
            the details of services automated and README documentation which details
            the detailed steps to execute the automation</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">5</td>
      <td style="text-align:left">Platform Security Audit fixes</td>
      <td style="text-align:left">
        <p>Listed below are the security vulnerabilities identified as part of the
          security audit. Few of them are as per design and justification is provided
          for these. Others are fixed at the code level.</p>
        <ol>
          <li>Privilege Escalation</li>
          <li>Failure to restrict URL Access</li>
          <li>Insecure direct object references (IDOR)</li>
          <li>Malicious file upload leads to Cross Site scripting</li>
          <li>Improper Authentication</li>
          <li>Missing Account Lockout</li>
          <li>Request Throttling Attack</li>
          <li>Weak Encoding Mechanism</li>
          <li>Sensitive Information in URL</li>
          <li>Lack of Automatic Session Expiration</li>
          <li>Concurrent Session</li>
          <li>Improper Error Handling</li>
          <li>Improper Input Validation</li>
          <li>Mail Command Injection</li>
          <li>Use of hardcoded credentials</li>
          <li>Use of sensitive information into configuration file</li>
          <li>Exclude unsanitized user input from format strings</li>
          <li>HTTP Parameter Pollution</li>
          <li>Standard pseudo-random number generators cannot withstand cryptographic
            attacks</li>
          <li>Weak cryptographic hash</li>
          <li>Insecure SSL configuration</li>
          <li>Improper Neutralization of CRLF Sequences in HTTP Header</li>
          <li>Avoid Capturing Java.Lang Security Exception</li>
          <li>Always normalize system inputs</li>
          <li>Avoid the Command Throws within Finally</li>
          <li>Close Input and Output resources in finally block</li>
          <li>Cross Site Request Forgery</li>
          <li>Cross Site Scripting - Stored</li>
          <li>Insufficient Cookie Attributes</li>
          <li>Code Injection</li>
          <li>Exclude unsanitized user input from format strings</li>
          <li>Avoid data submissions to non-editable fields</li>
          <li>Potential Infinite Loops</li>
          <li>Avoid dangerous J2EE API, use replacements from security-focused libraries
            (like OWASP ESAPI)</li>
          <li>Do not allow external input to control resource identifiers</li>
          <li>The setter method for an identifier property (id or composite-id) should
            be private</li>
        </ol>
        <p>Here are the security fixes guidelines as a <a href="../digit-support/security-guidelines-handbook.md">handbook</a> for
          best practices and guidelines.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">6</td>
      <td style="text-align:left">Technical Improvements</td>
      <td style="text-align:left">
        <ul>
          <li>PDF service refactoring for Localization API calls optimization</li>
          <li>Timezone configuration support for all the services</li>
          <li>Standard product Workflow bundling as part of the product</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">7</td>
      <td style="text-align:left">eDCR Enhancements</td>
      <td style="text-align:left">
        <ol>
          <li>Enhanced Door, to support door widths with color code. The color code
            is used to identify the type of door</li>
          <li>Fix of security audit issues</li>
          <li>Cleanup unused code and database tables</li>
        </ol>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">8</td>
      <td style="text-align:left">Finance</td>
      <td style="text-align:left">
        <ol>
          <li>Hard coded sub domain formation logic changed, preparing dynamic sub domain
            url by reading env from the configuration</li>
          <li>Fixed the security audit issues</li>
        </ol>
      </td>
    </tr>
  </tbody>
</table>

## ‌Document Resources and Links <a id="&#x200C;Document-Resources-and-Links"></a>

### UI Technical Documents

{% page-ref page="../modules/mcollect-mcs/echallan-ui-details/" %}

{% page-ref page="../modules/mcollect-mcs/echallan-ui-details/edit-cancel-challan.md" %}

{% page-ref page="../modules/mcollect-mcs/echallan-ui-details/search-and-pay-challan.md" %}

{% page-ref page="../modules/property-tax/property-tax-service/" %}

{% page-ref page="../modules/property-tax/pt-create-property-ui-details/edit-update-property.md" %}

{% page-ref page="../modules/property-tax/pt-create-property-ui-details/property-tax-my-applications.md" %}

{% page-ref page="../modules/property-tax/pt-create-property-ui-details/property-tax-my-properties.md" %}

{% page-ref page="../modules/property-tax/pt-create-property-ui-details/property-tax-quick-pay-for-citizen.md" %}

{% file src="../.gitbook/assets/common-pay-config \(1\).pdf" caption="Common Pay Configuration" %}

{% file src="../.gitbook/assets/fire-noc-create.pdf" caption="Fire NOC Create" %}

{% file src="../.gitbook/assets/digit-ui-manual \(1\).pdf" caption="DIGIT UI Manual" %}

### Backend Service Documents

{% page-ref page="../configure-digit/services-overview/core-services/xstate-core-chatbot/" %}

{% page-ref page="../configure-digit/services-overview/core-services/xstate-core-chatbot/xstate-chatbot-integration-document.md" %}

{% page-ref page="../configure-digit/services-overview/core-services/xstate-core-chatbot/xstate-chatbot-message-localisation.md" %}

{% page-ref page="../modules/e-challan-service/" %}

{% page-ref page="../modules/e-challan-service/echallan-calculator-services.md" %}

{% page-ref page="../modules/faecal-sludge-management-fsm/fsm-service-configuration/fsm-services.md" %}

### Tech Enablement Documents

{% page-ref page="../configure-digit/services-overview/business-services/appropriation-service.md" %}

{% page-ref page="../configure-digit/services-overview/business-services/billing-service/" %}

{% page-ref page="../configure-digit/services-overview/business-services/billing-service/bill-amendment-service-configuration.md" %}

{% page-ref page="../configure-digit/services-overview/business-services/collection-service/" %}

{% page-ref page="../configure-digit/services-overview/business-services/billing-collection-integration.md" %}

{% page-ref page="../configure-digit/services-overview/business-services/dashboard-analytics-backend.md" %}

{% page-ref page="../configure-digit/services-overview/business-services/dss-technical-documentation.md" %}

{% page-ref page="../configure-digit/services-overview/business-services/dss-dashboard-technical-document-for-ui.md" %}

{% page-ref page="../configure-digit/services-overview/business-services/dss-features-enhancements.md" %}

{% page-ref page="../configure-digit/services-overview/business-services/technical-script-steps-for-migration-process.md" %}

{% page-ref page="../modules/property-tax/property-tax-service/" %}

{% page-ref page="../modules/water-and-sewerage/water-services/" %}

{% page-ref page="../modules/water-and-sewerage/water-services/water-calculator-service.md" %}

{% page-ref page="../modules/water-and-sewerage/water-services/sewerage-service.md" %}

{% page-ref page="../modules/water-and-sewerage/water-services/sewerage-calculator-service.md" %}

{% page-ref page="../modules/fire-noc/fire-noc-service/" %}

{% page-ref page="../modules/fire-noc/fire-noc-service/fire-noc-calculator-service.md" %}

{% page-ref page="../modules/trade-license-tl/tl-service-configuration/" %}

{% page-ref page="../modules/trade-license-tl/tl-service-configuration/trade-license-calculator.md" %}

{% page-ref page="../configure-digit/qa-automation/automation-framework-knowledge-base.md" %}

{% page-ref page="../configure-digit/qa-automation/jenkins-setup-for-automation.md" %}

{% page-ref page="../configure-digit/qa-automation/automation-test-tags.md" %}

{% page-ref page="../configure-digit/qa-automation/automation-test-reporting.md" %}

{% page-ref page="../digit-support/security-guidelines-handbook.md" %}

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)\_\_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_ ](https://egov.org.in/)_is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._

