---
description: 'New release features, enhancements, and fixes'
---

# Release Notes DIGIT 2.2

### Release Summary

DIGIT 2.2 is a release that has got a few functional changes and few non-functional standardization changes.

* Functional: PGR v2 \(Revamped UI/UX, Revamped APIs, and Workflow integration\), Water & Sewerage Enhancements \(Public Domain Search, Open Payments, and PT Workflow Config Changes\), Property Enhancements, Search/Cancel Receipts Screen, and Enhancements in HRMS.
* Non-functional: Config Repo baselining \(Indexer and Persister configs sem version and baselining\).

### New ‌Feature Additions

<table>
  <thead>
    <tr>
      <th style="text-align:left"><b>Feature</b>
      </th>
      <th style="text-align:left"><b>Description</b>
      </th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">PGR v2 (UI/UX/API revamp and Workflow integration)</td>
      <td style="text-align:left">
        <p><b>Citizen</b>
        </p>
        <ul>
          <li>Create a Complaint</li>
          <li>My Complaints and View Complaints</li>
          <li>Rating and Reopening of the Complaint</li>
        </ul>
        <p><b>CSR</b>
        </p>
        <ul>
          <li>Create a Complaint</li>
          <li>View Complaints</li>
          <li>Reopen Complaints</li>
          <li>Inbox</li>
        </ul>
        <p><b>Grievance Routing Officer</b>
        </p>
        <ul>
          <li>View Complaints</li>
          <li>Assign Complaints</li>
          <li>Reject Complaints</li>
          <li>Inbox</li>
        </ul>
        <p><b>Last Mile Employee</b>
        </p>
        <ul>
          <li>View Complaints</li>
          <li>Assign Complaints</li>
          <li>ReAssign Complaints</li>
          <li>Inbox</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Water and Sewerage</td>
      <td style="text-align:left">
        <ul>
          <li>Public domain search for Water and Sewerage</li>
          <li>Open payment for Water and Sewerage</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Collection</td>
      <td style="text-align:left">
        <ul>
          <li>Search Receipt</li>
          <li>Receipt cancellation and its impact</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">HRMS</td>
      <td style="text-align:left">
        <ul>
          <li>Deactivate and activate employee</li>
        </ul>
      </td>
    </tr>
  </tbody>
</table>

### Enhancements

<table>
  <thead>
    <tr>
      <th style="text-align:left"><b>Updated Feature</b>
      </th>
      <th style="text-align:left"><b>Description</b>
      </th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Property Tax</td>
      <td style="text-align:left">
        <ul>
          <li>Payment Notification</li>
          <li>Payment Failure Scenario for Open payment</li>
          <li>Capturing data for better reporting and analysis</li>
          <li>Show the status of the receipt if the receipt is cancelled</li>
          <li>Mutation - Allow Guardian name to change</li>
          <li>Mutation - Multiple owners to single owner change and vice versa</li>
          <li>Tenant and date range wise re-indexing Utility</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Water and Sewerage Enhancements</td>
      <td style="text-align:left">
        <ul>
          <li>Property Workflow Config Changes for Water and Sewerage</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Collection Enhancements</td>
      <td style="text-align:left">
        <ul>
          <li>Tenant and date range wise re-indexing Utility</li>
          <li>Zero payment changes</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">HRMS Enhancements</td>
      <td style="text-align:left">
        <ul>
          <li>Employee Create and Search Enhancements</li>
          <li>Other minor enhancements and validations</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">UI and backend Enhancements</td>
      <td style="text-align:left">
        <ul>
          <li>Pagination on process instance search API</li>
          <li>Pagination in Employee Inbox</li>
          <li>Addition of spinners in all the UI screens</li>
          <li>DSS improvements to enable/disable module configs in MDMS and table headings
            Localization</li>
          <li>PGR migration from v1 to v2 including the workflow data and reindexing</li>
          <li>DSS config changes to support PGR v2</li>
          <li>SENDBACKTOCITIZEN send&#x2019;s application back to the user&#x2019;s
            with a registered Mobile Number</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Non-functional enhancements</td>
      <td style="text-align:left">
        <ul>
          <li>Config Repo baselining (Indexer and Persister configs sem version and
            baselining)
            <ul>
              <li>Improvement in Loading localization data in UI - module wise localization
                caching</li>
            </ul>
          </li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">eDCR Enhancements</td>
      <td style="text-align:left">
        <ul>
          <li>Road Reserve area captured</li>
          <li>Height of Room - The colour codes are used to identify the type of room</li>
          <li>Vehicle Ramp captured and slope auto calculated</li>
          <li>Floor Unit - Colour codes used to differentiate the different type of
            dwelling unit</li>
        </ul>
      </td>
    </tr>
  </tbody>
</table>

### Document Resources and Links

#### UI Technical Documents

{% file src="../../.gitbook/assets/employee-inbox.pdf" caption="Employee Inbox" %}

{% file src="../../.gitbook/assets/receipt-search.pdf" caption="Receipt Search & Cancellation" %}

{% file src="../../.gitbook/assets/hrms.pdf" caption="HRMS" %}

{% file src="../../.gitbook/assets/water-sewerage-public-domain-search.pdf" caption="W&S Public Domain Search and Open Payment" %}

{% file src="../../.gitbook/assets/search-create-property.pdf" caption="Search-Create Property" %}

{% file src="../../.gitbook/assets/universal-collection.pdf" caption="Universal Collection" %}

{% file src="../../.gitbook/assets/common-pay-config.pdf" caption="Common Pay Config" %}

{% file src="../../.gitbook/assets/view-property-details \(1\).pdf" caption="View Property Details" %}

{% file src="../../.gitbook/assets/digit-ui-frontend-design.pdf" caption="DIGIT UI - Frontend Architecture Design" %}

{% file src="../../.gitbook/assets/digit-ui-manual.pdf" caption="DIGIT UI Manual" %}

{% file src="../../.gitbook/assets/digit-ui-faq.pdf" caption="DIGIT UI: Implementation - Development Guidelines & FAQs" %}

{% file src="../../.gitbook/assets/digit-ui-internals-faq.pdf" caption="DIGIT UI Internals - Development Guidelines & FAQs" %}

#### Backend Service Documents

{% file src="../../.gitbook/assets/pgr-v2.pdf" caption="PGR V2.0" %}

{% file src="../../.gitbook/assets/pgr-migration.pdf" caption="PGR Migration" %}

{% file src="../../.gitbook/assets/steps-live-indexing.pdf" caption="Steps For Collection Live Indexing" %}

{% file src="../../.gitbook/assets/pgr-live-indexing-steps.pdf" caption="Steps For PGR Live Indexing" %}

{% file src="../../.gitbook/assets/indexer-persister-config.pdf" caption="Indexer And Persister Config Versioning and Baselining" %}

{% file src="../../.gitbook/assets/path-param-search-workflow.pdf" caption="Path Param Based Payment Search/Workflow \(Update\)" %}

{% file src="../../.gitbook/assets/property-service-reindexing.pdf" caption="Property Service Reindexing" %}

{% page-ref page="pgr-technical-release-notes.md" %}

#### Tech Enablement Documents

{% page-ref page="../services-overview/core-services/user-session-management.md" %}

{% page-ref page="../../configure-digit/persister-configuration.md" %}

{% page-ref page="../../configure-digit/indexer-configuration.md" %}

{% page-ref page="../../customizing-digit/digit-customization/enhancing-existing-service.md" %}

{% page-ref page="../services-overview/core-services/indexer-service.md" %}

{% page-ref page="../services-overview/core-services/pdf-generation-services.md" %}

{% page-ref page="../services-overview/core-services/url-shortening-service.md" %}

{% page-ref page="../services-overview/core-services/user-services.md" %}

{% page-ref page="../services-overview/core-services/workflow-services.md" %}

{% page-ref page="../../configure-digit/setting-up-edcr-service.md" %}



















