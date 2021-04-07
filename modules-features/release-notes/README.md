---
description: 'New release features, enhancements, and fixes'
---

# Release Notes DIGIT 2.1

## Release Summary

DIGIT 2.1 is a release that has got a few functional changes and few non-functional standardization changes.

* Functional: Introducing Water and Sewerage edit connection and Connection holder feature, DSS enhancements, Edit \(send back to Citizen\) property enhancements, and PGR APIs redesign along with workflow integration and reports.
* Non-functional: Baselining Actions, Role action mapping, and English Localization data.

## New ‌Feature Additions

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
      <td style="text-align:left">Water and Sewerage edit connection and Connection holder feature</td>
      <td
      style="text-align:left">
        <ul>
          <li>Edit existing water or sewerage connection information using a workflow
            approval process.</li>
          <li>Associate a non-owner (connection holder) of the property to any connection.</li>
        </ul>
        </td>
    </tr>
    <tr>
      <td style="text-align:left">PGR API Contracts and APIs redesign</td>
      <td style="text-align:left">
        <ul>
          <li>PGR APIs redesign along with workflow integration.</li>
          <li>New reports
            <ul>
              <li>ULB Report</li>
              <li>Description Report</li>
              <li>LME Performance Report</li>
              <li>GRO Performance Report</li>
            </ul>
          </li>
        </ul>
      </td>
    </tr>
  </tbody>
</table>

## Enhancements

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
      <td style="text-align:left">DSS v1.2 Enhancements</td>
      <td style="text-align:left">
        <ul>
          <li>Graphs</li>
          <li>Pie Charts</li>
          <li>Typography</li>
          <li>Time Filter</li>
          <li>Comparison Indicators in Tables</li>
          <li>Breadcrumbs</li>
          <li>Event Duration Graphs</li>
          <li>Drilldown and Drillthroughs</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Property Enhancements</td>
      <td style="text-align:left">
        <ul>
          <li>Edit (Send Back to citizen) in Property Create, Update, and Mutation workflow</li>
          <li>Workflow configuration to support Data Entry and Data migration in Property
            Service</li>
          <li>Payer information on citizen side in open payments</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">UI and backend Enhancements</td>
      <td style="text-align:left">
        <ul>
          <li>Searcher Ignore case for user input fields</li>
          <li>DOB range Validation in HRMS and Trade License</li>
          <li>Create a user for an unregistered mobile number as part of the Billing
            service</li>
          <li>Added Deserialization Error Handler in Persister</li>
          <li>Localization caching in the application (module wise - within the module)</li>
          <li>Addition of spinner in all PT, TL, and Common pay screens</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Non-functional enhancements</td>
      <td style="text-align:left">
        <ul>
          <li>Actions and Roleaction mapping - Product baseline</li>
          <li>Baseline English Localisation data</li>
          <li>Readme and Localsetup documentations for all the services</li>
          <li>Technical Enablement and other Tech documentations</li>
        </ul>
      </td>
    </tr>
  </tbody>
</table>

## Document Resources and Links

### UI Technical Documents

{% file src="../../.gitbook/assets/dss-features-enhancements-v2-technical-document-for-ui.pdf" caption="DSS Feature Enhancements" %}

{% file src="../../.gitbook/assets/search-property-tax.pdf" caption="Search Property Tax" %}

{% file src="../../.gitbook/assets/view-property-details.pdf" caption="View Property Details" %}

{% file src="../../.gitbook/assets/property-and-mutation-workflow.pdf" caption="Property & Mutation Workflow" %}

{% file src="../../.gitbook/assets/property-tax.pdf" caption="Property Tax - Add New Property" %}

{% file src="../../.gitbook/assets/update-existing-property.pdf" caption="Update Existing Property" %}

{% file src="../../.gitbook/assets/transfer-ownership.pdf" caption="Transfer Of Ownership" %}

{% file src="../../.gitbook/assets/connection-holder-details.pdf" caption="Connection Holder" %}

{% file src="../../.gitbook/assets/edit-connection-flow.pdf" caption="Edit Connection Flow" %}

### Backend Service Documents

{% file src="../../.gitbook/assets/water-service-technical-doc.pdf" caption="Water Service Technical Document" %}

{% file src="../../.gitbook/assets/sewerage-service.pdf" caption="Sewerage Service Technical Document" %}

{% file src="../../.gitbook/assets/water-calculator-service.pdf" caption="Water Calculator Service Technical Document" %}

{% file src="../../.gitbook/assets/sewerage-calculator-service.pdf" caption="Sewerage Calculator Service Technical Document" %}

{% file src="../../.gitbook/assets/w-and-s-promotion.pdf" caption="W&S Promotion Doc v2.2" %}

{% file src="../../.gitbook/assets/dss-backend-configuration-manual.pdf" caption="DSS Backend Configuration Manual" %}

{% file src="../../.gitbook/assets/property-registry-migration.pdf" caption="Property Registry Migration" %}

{% file src="../../.gitbook/assets/chatbot-service.pdf" caption="Chatbot Service" %}

{% file src="../../.gitbook/assets/promotion-doc-whatsapp.pdf" caption="Promotion Doc Whatsapp PGR Chatbot" %}

{% file src="../../.gitbook/assets/kafka.pdf" caption="Kafka-Connect Commands for DSS and Collection Live Indexing" %}

{% file src="../../.gitbook/assets/noc-promotion-document.pdf" caption="NOC Promotion Document" %}

### Infra/Deployment Documents

* [MDMS \(Master Data Management Service\)](https://docs.digit.org/modules-features/technical-documentation/core-service/mdms-master-data-management-service)
* [Setting Up Workflows](https://app.gitbook.com/@egov-digit/s/home/install-digit/configuring-workflows/setting-up-workflow)
* [Configuring Workflows For New Product/Entity](https://app.gitbook.com/@egov-digit/s/home/v/v2.1/install-digit/configuring-workflows/configuring-workflow-for-an-entity)
* [PDF Generation Service](https://app.gitbook.com/@egov-digit/s/home/v/v2.1/modules-features/technical-documentation/core-service/pdf-generation-service)
* [Customizing PDF Receipts & Certificates](https://app.gitbook.com/@egov-digit/s/home/v/v2.1/install-digit/configuring-digit-services/customizing-pdf-notices-and-certificates/customizing-pdf-receipts-and-certificates)
* [Integration of PDF in UI for download and print PDF](https://app.gitbook.com/@egov-digit/s/home/v/v2.1/install-digit/configuring-digit-services/customizing-pdf-notices-and-certificates/integration-of-pdf-in-ui-for-download-and-print-pdf)
* [API Do's and Don'ts](https://app.gitbook.com/@egov-digit/s/home/v/v2.1/install-digit/configuring-digit-services/api-dos-and-donts)
* [Writing a new Consumer](https://app.gitbook.com/@egov-digit/s/home/v/v2.1/customizing-digit/digit-customization/writing-a-new-customer)
* [Workflow Service](https://app.gitbook.com/@egov-digit/s/home/v/v2.1/modules-features/technical-documentation/core-service/workflow-service)
* [User Service](../technical-documentation/core-service/user-service.md)
* [Access Control Service](https://app.gitbook.com/@egov-digit/s/home/v/v2.1/modules-features/technical-documentation/core-service/access-control-service)
* [Payment Gateway Service](https://app.gitbook.com/@egov-digit/s/home/v/v2.1/modules-features/technical-documentation/core-service/payment-gateway-service)
* [Location Service](https://app.gitbook.com/@egov-digit/s/home/v/v2.1/modules-features/technical-documentation/core-service/location-service)
* [Trade License Service](https://app.gitbook.com/@egov-digit/s/home/v/v2.1/modules-features/technical-documentation/municipal-service/trade-license-service)
* [PGR Services v2.0](https://app.gitbook.com/@egov-digit/s/home/v/v2.1/modules-features/technical-documentation/municipal-service/pgr-services)

{% file src="../../.gitbook/assets/bpa-service.pdf" caption="BPA Service" %}

{% file src="../../.gitbook/assets/noc-services.pdf" caption="NOC Services" %}

