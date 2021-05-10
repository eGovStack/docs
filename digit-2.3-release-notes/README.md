---
description: 'New release features, enhancements, and fixes'
---

# Release Notes

## Release Summary <a id="Release-Summary"></a>

DIGIT 2.3 release offers new modules, few functional changes, and non-functional changes.

* Functional: Faecal Sludge Management module, Bill Amendment module, and Enhancements in HRMS.
* Non-functional: Security fixes.

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
      <td style="text-align:left">Faecal Sludge Management (FSM)</td>
      <td style="text-align:left">
        <p><b>Citizen</b>
        </p>
        <ul>
          <li>Apply for Emptying of Septic Tank / Pit</li>
          <li>My Applications and View Applications</li>
          <li>Make Online Payment for Emptying of Septic Tank / Pit Charges</li>
          <li>Download Application PDF and Receipt</li>
          <li>Rating the service</li>
        </ul>
        <p><b>Employee</b>
        </p>
        <ul>
          <li>Create a new Emptying of Septic Tank / Pit Application</li>
          <li>Search and View Applications</li>
          <li>Download Application PDF and Receipt</li>
          <li>Inbox</li>
          <li>Update Application/Demand</li>
          <li>Collect Payment</li>
          <li>Assign DSO</li>
          <li>Reassign DSO</li>
          <li>Complete Request on behalf of DSO</li>
        </ul>
        <p><b>Desludging operator</b>
        </p>
        <ul>
          <li>DSO Login</li>
          <li>Assign Vehicle</li>
          <li>Complete Request</li>
          <li>Decline Request</li>
          <li>Search and View Applications</li>
          <li>Inbox</li>
        </ul>
        <p><b>FSTP Operator</b>
        </p>
        <ul>
          <li>Inbox</li>
          <li>Update vehicle log</li>
        </ul>
        <p><b>Backend APIs</b>
        </p>
        <ul>
          <li>Create and Search Vendor/Desludging operator</li>
          <li>Create and Search Vehicle</li>
          <li>Create and Search Billing Slabs</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">2</td>
      <td style="text-align:left">Bill Amendment</td>
      <td style="text-align:left">
        <ul>
          <li>Application initiation</li>
          <li>Workflow-based application process</li>
          <li>Reference implementation for Water and Sewerage.</li>
          <li>Artefacts
            <ul>
              <li>Credit/ Debit note PDF</li>
              <li>Application Acknowledgement</li>
            </ul>
          </li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">3</td>
      <td style="text-align:left">HRMS Reports</td>
      <td style="text-align:left">Employee Report</td>
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
      <td style="text-align:left">HRMS Enhancements</td>
      <td style="text-align:left">Multi-Tenancy support while creating Employee</td>
    </tr>
    <tr>
      <td style="text-align:left">2</td>
      <td style="text-align:left">PGR Reports and Enhancements</td>
      <td style="text-align:left">
        <ul>
          <li>Support for PGR v2</li>
          <li>The Google map integration in Citizen Create complaint flow</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">3</td>
      <td style="text-align:left">Non-functional</td>
      <td style="text-align:left">
        <p>Few of the Security fixes:</p>
        <p><b>Backend</b>
        </p>
        <ul>
          <li>Sensitive Information in URL</li>
          <li>Standard pseudo-random number generators cannot withstand cryptographic
            attacks</li>
          <li>Improper Neutralization of CRLF Sequences in HTTP Headers (&apos;HTTP
            Response Splitting&apos;)</li>
          <li>Avoid Exception, Runtime Exception or Throwable in catch or Throw Statements(Merged
            only for municipal repo)</li>
          <li>Avoid sensitive information exposure through error messages(partially)</li>
          <li>Size Validations(partially)</li>
        </ul>
        <p><b>Frontend</b>
        </p>
        <ul>
          <li>Insecure Direct Object References (IDOR)</li>
          <li>Sensitive Information in URL</li>
          <li>Clickjacking</li>
          <li>It was observed that the application uses eval(code).</li>
          <li>Do not use dangerouslySetInnerHTML property in React components.</li>
          <li>Do not release debuggable apps</li>
          <li>Avoid post cross-document messages with an overly permissive target origin</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">4</td>
      <td style="text-align:left">Building plan approval system</td>
      <td style="text-align:left">
        <ul>
          <li>Scrutiny report download issue from UI screen fixed</li>
          <li>Fixed stakeholder registration issue for stakeholder like engineers, town
            planner etc.</li>
          <li>Added missing role actions in BPA for different stakeholders</li>
          <li>Security fix for vertical escalation issue for citizen/stakeholder</li>
          <li>Security fix for horizontal escalation issue for citizen/stakeholder</li>
          <li>Updated service code in the receipt search and download receipt</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">5</td>
      <td style="text-align:left">eDCR Enhancements</td>
      <td style="text-align:left">
        <ul>
          <li>Projections: Portico validation</li>
          <li>Glass Facade openings validation</li>
          <li>Information and Communication Technology landing point (ICT)</li>
          <li>Mezzanine At Room</li>
          <li>Amenities on Setback</li>
          <li>Enhanced chimney feature to accommodate multiple area and height</li>
          <li>Enhanced parapet feature to accommodate multiple area and height</li>
        </ul>
      </td>
    </tr>
  </tbody>
</table>

## ‌Document Resources and Links <a id="&#x200C;Document-Resources-and-Links"></a>

### UI Technical Documents

{% file src="../.gitbook/assets/bill-amendment.pdf" caption="Bill Amendment" %}

{% file src="../.gitbook/assets/bill-amendment-apply.pdf" caption="Bill Amendment Apply" %}

{% file src="../.gitbook/assets/create-employee.pdf" caption="Create Employee" %}

{% file src="../.gitbook/assets/apply-water-sewerage.pdf" caption="Apply Water & Sewerage" %}

{% file src="../.gitbook/assets/digit-ui-manual-r2.pdf" caption="DIGIT UI Manual" %}

{% file src="../.gitbook/assets/digit-ui-implementation.pdf" caption="DIGIT UI Implementation" %}

{% file src="../.gitbook/assets/fsm-ui-implementation.pdf" caption="FSM UI Implementation" %}

{% file src="../.gitbook/assets/pgr-ui-implementation.pdf" caption="PGR UI Implementation" %}

### Backend Service Documents

{% page-ref page="../modules/services-overview/business-services/bill-amendment.md" %}

{% page-ref page="../modules/faecal-sludge-management-fsm/fsm-service-configuration.md" %}

{% page-ref page="../modules/faecal-sludge-management-fsm/fsm-calculator-v1.0.md" %}

{% page-ref page="../modules/faecal-sludge-management-fsm/fsm-vendor-registry-v1.0.md" %}

{% page-ref page="../modules/faecal-sludge-management-fsm/fsm-vehicle-registry-v1.0.md" %}

{% file src="../.gitbook/assets/water-service-tech-doc.pdf" caption="Water Service Technical Document" %}

{% file src="../.gitbook/assets/sewerage-service-tech-doc.pdf" caption="Sewerage-Service Technical Document" %}

{% file src="../.gitbook/assets/egov-hrms.pdf" caption="egov-hrms" %}

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation ](https://egov.org.in/)is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).

