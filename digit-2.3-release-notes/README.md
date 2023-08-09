---
description: New release features, enhancements, and fixes
---

# Release Notes

## Release Summary <a href="#release-summary" id="release-summary"></a>

DIGIT 2.3 release offers new modules, few functional changes, and non-functional changes.

* Functional: Faecal Sludge Management module, Bill Amendment module, and Enhancements in HRMS.
* Non-functional: Security fixes.

## New ‌Feature Additions <a href="#new-feature-additions" id="new-feature-additions"></a>

| **S.No.** | **Feature**                    | **Description**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| --------- | ------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 1         | Faecal Sludge Management (FSM) | <p><strong>Citizen</strong></p><ul><li>Apply for Emptying of Septic Tank / Pit</li><li>My Applications and View Applications</li><li>Make Online Payment for Emptying of Septic Tank / Pit Charges</li><li>Download Application PDF and Receipt</li><li>Rating the service</li></ul><p><strong>Employee</strong></p><ul><li>Create a new Emptying of Septic Tank / Pit Application</li><li>Search and View Applications</li><li>Download Application PDF and Receipt</li><li>Inbox</li><li>Update Application/Demand</li><li>Collect Payment</li><li>Assign DSO</li><li>Reassign DSO</li><li>Complete Request on behalf of DSO</li></ul><p><strong>Desludging operator</strong></p><ul><li>DSO Login</li><li>Assign Vehicle</li><li>Complete Request</li><li>Decline Request</li><li>Search and View Applications</li><li>Inbox</li></ul><p><strong>FSTP Operator</strong></p><ul><li>Inbox</li><li>Update vehicle log</li></ul><p><strong>Backend APIs</strong></p><ul><li>Create and Search Vendor/Desludging operator</li><li>Create and Search Vehicle</li><li>Create and Search Billing Slabs</li></ul> |
| 2         | Bill Amendment                 | <ul><li>Application initiation</li><li>Workflow-based application process</li><li>Reference implementation for Water and Sewerage.</li><li><p>Artefacts</p><ul><li>Credit/ Debit note PDF</li><li>Application Acknowledgement</li></ul></li></ul>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| 3         | HRMS Reports                   | Employee Report                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |

## Enhancements <a href="#enhancements" id="enhancements"></a>

| **S.No.** | **Updated Feature**           | **Description**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| --------- | ----------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1         | HRMS Enhancements             | Multi-Tenancy support while creating Employee                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| 2         | PGR Reports and Enhancements  | <ul><li>Support for PGR v2</li><li>The Google map integration in Citizen Create complaint flow</li></ul>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| 3         | Non-functional                | <p>Few of the Security fixes:</p><p><strong>Backend</strong></p><ul><li>Sensitive Information in URL</li><li>Standard pseudo-random number generators cannot withstand cryptographic attacks</li><li>Improper Neutralization of CRLF Sequences in HTTP Headers ('HTTP Response Splitting')</li><li>Avoid Exception, Runtime Exception or Throwable in catch or Throw Statements(Merged only for municipal repo)</li><li>Avoid sensitive information exposure through error messages(partially)</li><li>Size Validations(partially)</li></ul><p><strong>Frontend</strong></p><ul><li>Insecure Direct Object References (IDOR)</li><li>Sensitive Information in URL</li><li>Clickjacking</li><li>It was observed that the application uses eval(code).</li><li>Do not use dangerouslySetInnerHTML property in React components.</li><li>Do not release debuggable apps</li><li>Avoid post cross-document messages with an overly permissive target origin</li></ul> |
| 4         | Building plan approval system | <ul><li>Scrutiny report download issue from UI screen fixed</li><li>Fixed stakeholder registration issue for stakeholder like engineers, town planner etc.</li><li>Added missing role actions in BPA for different stakeholders</li><li>Security fix for vertical escalation issue for citizen/stakeholder</li><li>Security fix for horizontal escalation issue for citizen/stakeholder</li><li>Updated service code in the receipt search and download receipt</li></ul>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| 5         | eDCR Enhancements             | <ul><li>Projections: Portico validation</li><li>Glass Facade openings validation</li><li>Information and Communication Technology landing point (ICT)</li><li>Mezzanine At Room</li><li>Amenities on Setback</li><li>Enhanced chimney feature to accommodate multiple area and height</li><li>Enhanced parapet feature to accommodate multiple area and height</li></ul>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |

## ‌Document Resources and Links <a href="#document-resources-and-links" id="document-resources-and-links"></a>

### UI Technical Documents

{% file src="../.gitbook/assets/bill-amendment.pdf" %}
Bill Amendment
{% endfile %}

{% file src="../.gitbook/assets/bill-amendment-apply.pdf" %}
Bill Amendment Apply
{% endfile %}

{% file src="../.gitbook/assets/create-employee.pdf" %}
Create Employee
{% endfile %}

{% file src="../.gitbook/assets/apply-water-sewerage.pdf" %}
Apply Water & Sewerage
{% endfile %}

{% file src="../.gitbook/assets/digit-ui-manual-r2.pdf" %}
DIGIT UI Manual
{% endfile %}

{% file src="../.gitbook/assets/digit-ui-implementation.pdf" %}
DIGIT UI Implementation
{% endfile %}

{% file src="../.gitbook/assets/fsm-ui-implementation.pdf" %}
FSM UI Implementation
{% endfile %}

{% file src="../.gitbook/assets/pgr-ui-implementation.pdf" %}
PGR UI Implementation
{% endfile %}

### Backend Service Documents

{% content-ref url="../modules/services-overview/business-services/bill-amendment.md" %}
[bill-amendment.md](../modules/services-overview/business-services/bill-amendment.md)
{% endcontent-ref %}

{% content-ref url="../modules/faecal-sludge-management-fsm/fsm-service-configuration.md" %}
[fsm-service-configuration.md](../modules/faecal-sludge-management-fsm/fsm-service-configuration.md)
{% endcontent-ref %}

{% content-ref url="../modules/faecal-sludge-management-fsm/fsm-calculator-v1.0.md" %}
[fsm-calculator-v1.0.md](../modules/faecal-sludge-management-fsm/fsm-calculator-v1.0.md)
{% endcontent-ref %}

{% content-ref url="../modules/faecal-sludge-management-fsm/fsm-vendor-registry-v1.0.md" %}
[fsm-vendor-registry-v1.0.md](../modules/faecal-sludge-management-fsm/fsm-vendor-registry-v1.0.md)
{% endcontent-ref %}

{% content-ref url="../modules/faecal-sludge-management-fsm/fsm-vehicle-registry-v1.0.md" %}
[fsm-vehicle-registry-v1.0.md](../modules/faecal-sludge-management-fsm/fsm-vehicle-registry-v1.0.md)
{% endcontent-ref %}

{% file src="../.gitbook/assets/water-service-tech-doc.pdf" %}
Water Service Technical Document
{% endfile %}

{% file src="../.gitbook/assets/sewerage-service-tech-doc.pdf" %}
Sewerage-Service Technical Document
{% endfile %}

{% file src="../.gitbook/assets/egov-hrms.pdf" %}
egov-hrms
{% endfile %}

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation ](https://egov.org.in/)is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).
