---
description: 'New release features, enhancements, and fixes'
---

# Release Notes

### Release Summary <a id="Release-Summary"></a>

<<<<<<< HEAD
DIGIT 2.4 is the latest release that has got new modules, a few functional changes, and non-functional changes.

* Functional: eChallan module, WhatsApp Bill Payment, Property Tax Citizen flow UI/UX revamp Arrears Breakup in Property Tax Due, and Send back to Citizen feature in Fire NOC.
* Non-functional: Platform Security Audit fixes, Hindi Localization, QA Automaton of APIs, and Technical improvements.
=======
DIGIT 2.5 is a release that has got new modules, a few functional changes, and non-functional changes.

* Functional: Property Tax Citizen Open search flow UI/UX revamp, Property Tax Employee flow UI/UX revamp, Property Tax Mutation flow UI/UX revamp, HRMS UI/UX revamp, mCollect v2 \(eChallan\) UI/UX revamp, Trade License Citizen & Employee UI/UX revamp, Receipt Cancellation UI/UX Revamp, WhatsApp v2 \(Pay and Enhanced PGR\), Workflow Auto Escalation with reference implementations in PGR, W&S Enhancements, FSM DSS, and Standardized Reports for FSM/PT/mCollect.
* Non-functional: QA Automaton of APIs for FSM & eChallan, Product Standard Ontologies, Technical improvements, Internal Data Mart, etc.
>>>>>>> 64dca8adbdf64336b1a8203199b3791fa23434fa

### New ‌Feature Additions <a id="New-&#x200C;Feature-Additions"></a>

<table>
  <thead>
    <tr>
<<<<<<< HEAD
      <th style="text-align:left"><b>S.No.</b>
=======
      <th style="text-align:left"><a href="http://s.no/"><b>S.No</b></a><b>.</b>
>>>>>>> 64dca8adbdf64336b1a8203199b3791fa23434fa
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
<<<<<<< HEAD
      <td style="text-align:left">eChallan module</td>
      <td style="text-align:left">
        <p></p>
        <ol>
          <li>Generate <b>e-challans / bill</b> for all miscellaneous / Adhoc services
            which citizens avail from ULBs</li>
          <li>Edit/Cancel e-challan/bill</li>
          <li>The ability for ULBs to Notify citizens about the outstanding payments
            - Online(email &amp; SMS) and offline.</li>
          <li>Enable Digital payments for citizens - QR code, payment link in notifications,
            etc.</li>
        </ol>
=======
      <td style="text-align:left">Property Tax UI/UX Revamp</td>
      <td style="text-align:left">
        <p><b>Citizen flow</b>
        </p>
        <ul>
          <li>Open Search and Payment</li>
        </ul>
        <p><b>Employee flow</b>
        </p>
        <ul>
          <li>Employee Inbox</li>
          <li>Create Property</li>
          <li>Search Property</li>
          <li>Transfer of Ownership</li>
          <li>Update Property</li>
          <li>Property Assessment</li>
        </ul>
>>>>>>> 64dca8adbdf64336b1a8203199b3791fa23434fa
      </td>
    </tr>
    <tr>
      <td style="text-align:left">2</td>
<<<<<<< HEAD
      <td style="text-align:left">WhatsApp Bill Payment and PGR v2 integration with redesigned Chatbot (xState)</td>
      <td
      style="text-align:left">
        <p></p>
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
          <li><b>Payment </b>
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
        <p></p>
        <p>Updated workflows and user interface changes in the following business
          cases -</p>
        <ul>
          <li>PT - Quick Pay</li>
          <li>Create Property</li>
          <li>My Properties</li>
          <li>My Applications</li>
=======
      <td style="text-align:left">HRMS UI/UX Revamp</td>
      <td style="text-align:left">
        <ul>
          <li>Create employee</li>
          <li>Search employee</li>
          <li>Edit Employee</li>
          <li>Deactivate/re-activate employee</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">3</td>
      <td style="text-align:left">Trade License UX revamp</td>
      <td style="text-align:left">
        <ul>
          <li>Allow citizen to create Trade License application</li>
          <li>Allow citizen to check application status and make payment, download artefacts</li>
          <li>Allow Employee to create Trade License application on behalf of citizen</li>
          <li>Application processing by employees</li>
          <li>Allow citizen to renew the existing trade licenses which are due for renewal</li>
          <li>Allow employee to renew the existing trade license which are due for renewal</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">4</td>
      <td style="text-align:left">mCollect v2 (eChallan) UI/UX Revamp</td>
      <td style="text-align:left">
        <ul>
          <li>Challan Generation</li>
          <li>Challan Search Employee</li>
          <li>Total Challan Count</li>
          <li>My Challan - Citizen</li>
          <li>Search and Pay - Citizen</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">5</td>
      <td style="text-align:left">Receipt Cancellation UI/UX Revamp</td>
      <td style="text-align:left">Receipt Cancellation UI/UX Revamp</td>
    </tr>
    <tr>
      <td style="text-align:left">6</td>
      <td style="text-align:left">FSM DSS</td>
      <td style="text-align:left">
        <ul>
          <li>SLA Compliance</li>
          <li>Average Collections</li>
          <li>Performance by ULB and Districts</li>
          <li>Performance by Desludging Operator</li>
          <li>Plant Operating Efficiency</li>
          <li>Drill downs for Desluding and Vehicle log report</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">7</td>
      <td style="text-align:left">Workflow Auto Escalation</td>
      <td style="text-align:left">
        <ul>
          <li>Configure SLA at a workflow state level</li>
          <li>Escalate the application to a role if there is a breach in SLA</li>
          <li>Make the application status as deemed approved or reject on breach of
            an SLA</li>
          <li>Escalate the application to the next logical step in the workflow ladder
            if there is a breach in SLA</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">8</td>
      <td style="text-align:left">Product Standardized Reports</td>
      <td style="text-align:left">
        <p><b>FSM</b>
        </p>
        <ul>
          <li>Daily Collection Report</li>
          <li>Desludging Request Report</li>
          <li>Vehicle Log Report</li>
        </ul>
        <p><b>PT</b>
        </p>
        <ul>
          <li>Defaulter Report</li>
          <li>Collection Register Report</li>
          <li>Receipt Register Report</li>
        </ul>
        <p><b>mCollect</b>
        </p>
        <ul>
          <li>Challan Register Report</li>
          <li>Daily Collection Report</li>
          <li>Receipt Register Report</li>
>>>>>>> 64dca8adbdf64336b1a8203199b3791fa23434fa
        </ul>
      </td>
    </tr>
  </tbody>
</table>

### Enhancements <a id="Enhancements"></a>

<table>
  <thead>
    <tr>
<<<<<<< HEAD
      <th style="text-align:left"><b>S.No.</b>
=======
      <th style="text-align:left"><a href="http://s.no/"><b>S.No</b></a><b>.</b>
>>>>>>> 64dca8adbdf64336b1a8203199b3791fa23434fa
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
<<<<<<< HEAD
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
        <p></p>
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
          <li>Here is the <a href="qa-automation-release-notes.md">document </a>with
            the details of services automated and README documentation which details
            the detailed steps to execute the automation</li>
=======
      <td style="text-align:left">Water &amp; Sewerage Enhancements</td>
      <td style="text-align:left">
        <ul>
          <li>Bill Cancellation of latest bill</li>
          <li>Show Due Date in Arrears breakup</li>
          <li>Water &amp; Sewerage Combined PDF Changes</li>
          <li>Water &amp; Sewerage Due Validation on PT Title Transfer</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">2</td>
      <td style="text-align:left">WhatsApp v2 (Pay and PGR) Enhancements</td>
      <td style="text-align:left">
        <ul>
          <li><b>Improvements in Public Grievance Redressal Module</b>
            <ul>
              <li>Enhancements in messaging language.</li>
              <li>NLP Inclusion (For City &amp; Boundary Selection).</li>
            </ul>
          </li>
          <li><b>Improvements in Bill Payments</b>
            <ul>
              <li>Enhancements in messaging language.
                <ul>
                  <li>Inclusion of call to action buttons (for certain messages).</li>
                </ul>
              </li>
              <li>For Linked Mobile Numbers
                <ul>
                  <li>Single-click access to bills (for PT and W&amp;S)</li>
                </ul>
              </li>
              <li>For Non-Linked Mobile Numbers
                <ul>
                  <li>Provision of Search &amp; Pay (If Property/Connection Details are known).</li>
                  <li>Inclusion of Open Search Links (If Property/ Connection Details are unknown).</li>
                </ul>
              </li>
            </ul>
          </li>
          <li><b>Improvements in Payment History</b>
            <ul>
              <li>Enhancements in messaging language and flow.
                <ul>
                  <li>Inclusion of call to action buttons (for certain messages).</li>
                </ul>
              </li>
              <li>For Linked Mobile Numbers
                <ul>
                  <li>Access to view the last three payments made (for PT &amp; W&amp;S)</li>
                  <li>Provision to download the last three payment receipts</li>
                </ul>
              </li>
              <li>For Non-Linked Mobile Numbers
                <ul>
                  <li>Access control to view payments history only.</li>
                </ul>
              </li>
            </ul>
          </li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">3</td>
      <td style="text-align:left">Bill Amendment Enhancement</td>
      <td style="text-align:left">
        <ul>
          <li>Additional changes in Bill Amendment screen to display current Demand</li>
>>>>>>> 64dca8adbdf64336b1a8203199b3791fa23434fa
        </ul>
      </td>
    </tr>
    <tr>
<<<<<<< HEAD
      <td style="text-align:left">5</td>
      <td style="text-align:left">Platform Security Audit fixes</td>
      <td style="text-align:left">
        <p></p>
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
        <p>Here are the security fixes guidelines as a<a href="../digit-support/security-guidelines-handbook.md"> handbook </a>for
          best practices and guidelines.</p>
=======
      <td style="text-align:left">4</td>
      <td style="text-align:left">PT Enhancements</td>
      <td style="text-align:left">PT Enhancements - Fuzzy search for Name, Door number, and old PT ID (old
        UI)</td>
    </tr>
    <tr>
      <td style="text-align:left">5</td>
      <td style="text-align:left">QA Automaton of APIs</td>
      <td style="text-align:left">
        <p>APIs automation for</p>
        <ul>
          <li>eChallan APIs including end to end APIs automation</li>
          <li>Bill Amendment APIs</li>
          <li>FSM Inbox API</li>
        </ul>
>>>>>>> 64dca8adbdf64336b1a8203199b3791fa23434fa
      </td>
    </tr>
    <tr>
      <td style="text-align:left">6</td>
<<<<<<< HEAD
      <td style="text-align:left">Technical Improvements</td>
      <td style="text-align:left">
        <p></p>
        <ul>
          <li>PDF service refactoring for Localization API calls optimization</li>
          <li>Timezone configuration support for all the services</li>
          <li>Standard product Workflow bundling as part of the product</li>
=======
      <td style="text-align:left">Other Improvements and Tech Enhancements</td>
      <td style="text-align:left">
        <ul>
          <li>Changes in Gender to introduce Transgender and Others.</li>
          <li>Standardization of Product ontologies for Property Tax, Water &amp; Sewerage,
            Fire NOC, mCollect (eChallan), PGR, and Online Building Plan Approval.</li>
          <li>Inbox API to support module wise inbox for UI/UX revamp.</li>
>>>>>>> 64dca8adbdf64336b1a8203199b3791fa23434fa
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">7</td>
<<<<<<< HEAD
      <td style="text-align:left">eDCR Enhancements</td>
      <td style="text-align:left">
        <p></p>
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
        <p></p>
        <ol>
          <li>Hard coded sub domain formation logic changed, preparing dynamic sub domain
            url by reading env from the configuration</li>
          <li>Fixed the security audit issues</li>
        </ol>
=======
      <td style="text-align:left">Internal Data mart</td>
      <td style="text-align:left">Internal Data mart for PT, TL, PGR, W&amp;S, FSM, eChallan, OBPS, and
        Fire NOC modules.</td>
    </tr>
    <tr>
      <td style="text-align:left">8</td>
      <td style="text-align:left">eDCR Enhancements</td>
      <td style="text-align:left">
        <p></p>
        <ul>
          <li>River Distance: Colour code used to identify different river types.</li>
          <li>In the basement footprint layer, captured additional dimension to define
            the level of the basement under the ground.</li>
          <li>In the stilt parking layer, captured height from floor to the bottom of
            a beam of the stilt floor.</li>
        </ul>
>>>>>>> 64dca8adbdf64336b1a8203199b3791fa23434fa
      </td>
    </tr>
  </tbody>
</table>

### ‌Document Resources and Links <a id="&#x200C;Document-Resources-and-Links"></a>

#### UI Technical Documents

<<<<<<< HEAD
{% page-ref page="../product/modules/mcollect-mcs/echallan-ui-details/" %}

{% page-ref page="../product/modules/mcollect-mcs/echallan-ui-details/edit-cancel-challan.md" %}

{% page-ref page="../product/modules/mcollect-mcs/echallan-ui-details/search-and-pay-challan.md" %}

{% page-ref page="../product/modules/property-tax/property-tax-service/" %}
=======
 **Trade License UI/UX Revamp**

 **Citizen**

{% page-ref page="../product/modules/trade-license-tl/tl-apply-flow-ui-details/" %}

{% page-ref page="../product/modules/trade-license-tl/tl-apply-flow-ui-details/my-applications-ui-flow.md" %}

{% page-ref page="../product/modules/trade-license-tl/tl-apply-flow-ui-details/send-back-edit-ui-flow.md" %}

{% page-ref page="../product/modules/trade-license-tl/tl-apply-flow-ui-details/trade-license-renewal-ui-flow.md" %}

 **Employee**

{% page-ref page="../product/modules/property-tax/pt-create-property-ui-details/create-application-employee-ui-ux-revamp.md" %}

{% page-ref page="../product/modules/property-tax/pt-create-property-ui-details/employee-inbox-and-application-details.md" %}

{% page-ref page="../product/modules/trade-license-tl/tl-apply-flow-ui-details/employee-search-application-search-license-ui-flow.md" %}

{% page-ref page="../product/modules/trade-license-tl/tl-apply-flow-ui-details/new-trade-license-ui-flow.md" %}

{% page-ref page="../product/modules/trade-license-tl/tl-apply-flow-ui-details/application-details-trade-details-ui-flows.md" %}

{% page-ref page="../product/modules/trade-license-tl/tl-apply-flow-ui-details/renew-edit-application.md" %}

 **HRMS UI/UX Revamp**

{% page-ref page="../product/modules/hrms/hrms-employee-create-edit-ui-flow.md" %}

{% page-ref page="../product/modules/hrms/employee-activation-deactivation-ui-flow.md" %}

{% page-ref page="../product/modules/hrms/employee-details-ui-flow.md" %}

{% page-ref page="../product/modules/hrms/search-employee-by-multiple-criteria-ui-flow.md" %}

{% page-ref page="../product/modules/hrms/employees-count-ui-flow.md" %}

 **Receipt cancellation UI/UX Revamp**

{% page-ref page="../product/modules/receipt-cancellation-ui-flow/" %}

{% page-ref page="../product/modules/receipt-cancellation-ui-flow/view-receipt-cancel-ui-flow.md" %}

 **Bill Cancellation**

{% page-ref page="../product/modules/current-bill-cancellation-ui-flow/" %}

{% page-ref page="../product/modules/current-bill-cancellation-ui-flow/bill-details-ui-flow.md" %}

{% page-ref page="../product/modules/current-bill-cancellation-ui-flow/cancel-bill-ui-flow.md" %}

 **mCollect v2 \(eChallan\) UI/UX Revamp**

{% page-ref page="../product/modules/mcollect-mcs/echallan-ui-details/mcollect-ui-flow.md" %}

{% page-ref page="../product/modules/mcollect-mcs/echallan-ui-details/update-cancel-challan-ui-flow.md" %}

{% page-ref page="../product/modules/mcollect-mcs/echallan-ui-details/search-and-pay-challan.md" %}

{% page-ref page="../product/modules/mcollect-mcs/echallan-ui-details/challan-creation.md" %}

 **Workflow Auto Escalation**

{% page-ref page="../product/modules/auto-escalation-ui-flow.md" %}

 **Property Tax UI/UX Revamp**

 **Citizen**

{% page-ref page="../product/modules/property-tax/pt-create-property-ui-details/" %}
>>>>>>> 64dca8adbdf64336b1a8203199b3791fa23434fa

{% page-ref page="../product/modules/property-tax/pt-create-property-ui-details/edit-update-property.md" %}

{% page-ref page="../product/modules/property-tax/pt-create-property-ui-details/property-tax-my-applications.md" %}

{% page-ref page="../product/modules/property-tax/pt-create-property-ui-details/property-tax-my-properties.md" %}

<<<<<<< HEAD
{% page-ref page="../product/modules/property-tax/pt-create-property-ui-details/property-tax-quick-pay-for-citizen.md" %}

{% file src="../.gitbook/assets/common-pay-config \(1\).pdf" caption="Common Pay Configuration" %}

{% file src="../.gitbook/assets/fire-noc-create.pdf" caption="Fire NOC Create" %}

{% file src="../.gitbook/assets/digit-ui-manual \(1\).pdf" caption="DIGIT UI Manual" %}

#### Backend Service Documents

{% page-ref page="../configuration/configure-digit/services-overview/core-services/xstate-core-chatbot/" %}

{% page-ref page="../configuration/configure-digit/services-overview/core-services/xstate-core-chatbot/xstate-chatbot-integration-document.md" %}

{% page-ref page="../configuration/configure-digit/services-overview/core-services/xstate-core-chatbot/xstate-chatbot-message-localisation.md" %}

{% page-ref page="../product/modules/e-challan-service/" %}

{% page-ref page="../product/modules/e-challan-service/echallan-calculator-services.md" %}

{% page-ref page="../product/modules/faecal-sludge-management-fsm/fsm-service-configuration/fsm-services.md" %}

#### Tech Enablement Documents

{% page-ref page="../configuration/configure-digit/services-overview/business-services/appropriation-service.md" %}

{% page-ref page="../configuration/configure-digit/services-overview/business-services/billing-service/" %}

{% page-ref page="../configuration/configure-digit/services-overview/business-services/billing-service/bill-amendment-service-configuration.md" %}

{% page-ref page="../configuration/configure-digit/services-overview/business-services/collection-service/" %}

{% page-ref page="../configuration/configure-digit/services-overview/business-services/billing-collection-integration.md" %}

{% page-ref page="../configuration/configure-digit/services-overview/business-services/dashboard-analytics-backend.md" %}

{% page-ref page="../configuration/configure-digit/services-overview/business-services/dss-technical-documentation.md" %}

{% page-ref page="../configuration/configure-digit/services-overview/business-services/dss-dashboard-technical-document-for-ui.md" %}

{% page-ref page="../configuration/configure-digit/services-overview/business-services/dss-features-enhancements.md" %}

{% page-ref page="../configuration/configure-digit/services-overview/business-services/technical-script-steps-for-migration-process.md" %}

{% page-ref page="../product/modules/property-tax/property-tax-service/" %}

{% page-ref page="../product/modules/water-and-sewerage/water-services/" %}

{% page-ref page="../product/modules/water-and-sewerage/water-services/water-calculator-service.md" %}

{% page-ref page="../product/modules/water-and-sewerage/water-services/sewerage-service.md" %}

{% page-ref page="../product/modules/water-and-sewerage/water-services/sewerage-calculator-service.md" %}

{% page-ref page="../product/modules/fire-noc/fire-noc-service/" %}

{% page-ref page="../product/modules/fire-noc/fire-noc-service/fire-noc-calculator-service.md" %}

{% page-ref page="../product/modules/trade-license-tl/tl-service-configuration/" %}

{% page-ref page="../product/modules/trade-license-tl/tl-service-configuration/trade-license-calculator.md" %}

{% page-ref page="../configuration/configure-digit/qa-automation/automation-framework-knowledge-base.md" %}

{% page-ref page="../configuration/configure-digit/qa-automation/jenkins-setup-for-automation.md" %}

{% page-ref page="../configuration/configure-digit/qa-automation/automation-test-tags.md" %}

{% page-ref page="../configuration/configure-digit/qa-automation/automation-test-reporting.md" %}

{% page-ref page="../digit-support/security-guidelines-handbook.md" %}
=======
 **Employee**

{% page-ref page="../product/modules/property-tax/pt-create-property-ui-details/employee-edit-application-flow.md" %}

{% page-ref page="../product/modules/property-tax/pt-create-property-ui-details/create-application-employee-ui-ux-revamp.md" %}

{% page-ref page="../product/modules/property-tax/pt-create-property-ui-details/employee-search-property-property-details-page-and-assessment.md" %}

{% page-ref page="../product/modules/property-tax/pt-create-property-ui-details/employee-inbox-and-application-details.md" %}

 **Mutation**

{% page-ref page="../product/modules/property-tax/pt-create-property-ui-details/employee-mutation-ownership-transfer.md" %}

{% page-ref page="../product/modules/property-tax/pt-create-property-ui-details/citizen-mutation-flow.md" %}

 **DSS**

{% page-ref page="../product/modules/dss-ui-flow.md" %}

{% page-ref page="../product/modules/faecal-sludge-management-fsm/fsm-service-configuration/fsm-implementation-configuration.md" %}

#### Backend Service Documents

{% file src="../.gitbook/assets/egov-hrms \(1\).pdf" caption="eGov HRMS" %}

{% page-ref page="../product/modules/e-challan-service/" %}

{% page-ref page="../configuration/configure-digit/configuring-digit-services/configuring-workflows/workflow-auto-escalation.md" %}

{% page-ref page="../configuration/configure-digit/services-overview/core-services/nlp-engine-service.md" %}

{% page-ref page="../configuration/configure-digit/services-overview/core-services/xstate-core-chatbot/" %}

{% page-ref page="../configuration/configure-digit/services-overview/core-services/xstate-core-chatbot/xstate-chatbot-integration-document.md" %}

{% page-ref page="../configuration/configure-digit/services-overview/core-services/xstate-core-chatbot/xstate-chatbot-message-localisation.md" %}

#### 

#### 

{% page-ref page="../configuration/configure-digit/services-overview/business-services/collection-service/collection-service-v2.md" %}

{% page-ref page="../product/modules/faecal-sludge-management-fsm/fsm-service-configuration/fsm-services.md" %}

{% page-ref page="../product/modules/faecal-sludge-management-fsm/fsm-service-configuration/fsm-vehicle-registry-v1.0.md" %}

{% page-ref page="../product/modules/faecal-sludge-management-fsm/fsm-service-configuration/fsm-vendor-registry-v1.0.md" %}

{% page-ref page="../product/modules/faecal-sludge-management-fsm/fsm-service-configuration/legacy-re-indexing-the-fsm-data.md" %}

{% page-ref page="../configuration/configure-digit/services-overview/municipal-services/turn-io-adapter.md" %}

{% page-ref page="../product/modules/property-tax/property-tax-service/fuzzy-search/" %}

{% page-ref page="../product/modules/property-tax/property-tax-service/fuzzy-search/fuzzy-search-reindexing.md" %}

{% page-ref page="../product/modules/faecal-sludge-management-fsm/fsm-service-configuration/fsm-dss-technical-documentation.md" %}

{% page-ref page="../configuration/configure-digit/services-overview/municipal-services/inbox-service.md" %}

{% page-ref page="../configuration/configure-digit/configuring-digit-services/digit-internal-datamart-deployment-steps.md" %}

#### Tech Enablement Documents






>>>>>>> 64dca8adbdf64336b1a8203199b3791fa23434fa





 [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)\_\_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_ ](https://egov.org.in/)_is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._

