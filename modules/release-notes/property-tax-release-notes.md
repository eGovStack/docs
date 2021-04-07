---
description: DIGIT 2.2 Changes in the Property Tax Module
---

# Property Tax 2.2 Release Notes

## Overview <a id="Overview"></a>

The latest release version of the Property Tax module focuses on enhancing application usability, handling instances of payment failure, and the capability to capture data for better reporting & dashboards. Also, employees can now cancel the receipts from the UI to promote efficient service delivery.

## Release Highlights <a id="Release-Highlights"></a>

1. Search API enhancements
2. UI for cancel receipt
3. Capturing transactional data for reporting
4. Transfer of ownership 'Transferee details' validations

## Release Features <a id="Release-Features"></a>

<table>
  <thead>
    <tr>
      <th style="text-align:left"><b>Key Feature</b>
      </th>
      <th style="text-align:left"><b>Description</b>
      </th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Payment Notification</td>
      <td style="text-align:left">
        <p>The enhancement defines the notification content and triggers the notification
          to different stakeholders.</p>
        <p>User story - <a href="https://digit-discuss.atlassian.net/browse/RAIN-1137"><img src="https://digit-discuss.atlassian.net/secure/viewavatar?size=medium&amp;avatarId=10318&amp;avatarType=issuetype" alt/>RAIN-1137: Payment NotificationQA SIGNOFF</a>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Payment Failure Scenario - Open payment</td>
      <td style="text-align:left">
        <p>For open payments, the property owners will not receive any notification
          in the event of a payment failure. Only the payer will receive the notification.
          The feature details out the scenario and content of the notification.</p>
        <p>User story - <a href="https://digit-discuss.atlassian.net/browse/RAIN-1138"><img src="https://digit-discuss.atlassian.net/secure/viewavatar?size=medium&amp;avatarId=10318&amp;avatarType=issuetype" alt/>RAIN-1138: Payment Failure Scenario - Open paymentQA SIGNOFF</a>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Capturing data for better reporting and analysis</td>
      <td style="text-align:left">
        <p>This is backend enhancement concerning the transactional data. The system
          offers the scope to generate reports on various transactional data such
          as type, device, task creator information, legacy entry, etc. This enables
          users to track product usage and understand the adoption patterns of the
          product.</p>
        <p>User story - <a href="https://digit-discuss.atlassian.net/browse/RAIN-1140"><img src="https://digit-discuss.atlassian.net/secure/viewavatar?size=medium&amp;avatarId=10318&amp;avatarType=issuetype" alt/>RAIN-1140: Capturing data for better reporting and analysisQA SIGNOFF</a>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">PT:: Show the status of the receipt if the receipt is cancelled</td>
      <td
      style="text-align:left">In case the receipt is cancelled, the system displays the receipt status
        in red to avoid any confusion to the users.</td>
    </tr>
    <tr>
      <td style="text-align:left">Search receipt</td>
      <td style="text-align:left">
        <p>Enhance user access control for the search API. Search data access is
          now restricted to the user-specific role. Earlier, a user had search access
          to search application, receipt, etc. for all products.</p>
        <p>User story -<a href="https://digit-discuss.atlassian.net/browse/RAIN-1756"><img src="https://digit-discuss.atlassian.net/secure/viewavatar?size=medium&amp;avatarId=10318&amp;avatarType=issuetype" alt/>RAIN-1756: Search ReceiptQA SIGNOFF</a>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Cancel receipt</td>
      <td style="text-align:left">
        <p>Employees can cancel the receipts at the counter in case of any discrepancy
          in the receipt. This feature aims to improve the service delivery of the
          ULBs. Employees will be able to capture the reason for cancelling the receipt
          and add penalties to the bills, if applicable.</p>
        <p>User story - <a href="https://digit-discuss.atlassian.net/browse/RAIN-1757"><img src="https://digit-discuss.atlassian.net/secure/viewavatar?size=medium&amp;avatarId=10318&amp;avatarType=issuetype" alt/>RAIN-1757: Cancel ReceiptQA SIGNOFF</a>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Transfer of ownership - All use cases</td>
      <td style="text-align:left">
        <p>This enhancement covers all the combinations and possible values in the
          transferee details. Now, the user can change a single owner to multiple
          owners or private owner to institutional and so on. The user story covers
          all the corner cases in the mutation process.</p>
        <p>User Story - <a href="https://digit-discuss.atlassian.net/browse/RAIN-1820"><img src="https://digit-discuss.atlassian.net/secure/viewavatar?size=medium&amp;avatarId=10310&amp;avatarType=issuetype" alt/>RAIN-1820: PT Mutation - Allow the following changes in the mutation application QA SIGNOFF</a>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Zero payment changes</td>
      <td style="text-align:left">
        <p>This enhancement in the billing service will solve the reporting problem
          in case of consolidated bill generation by excluding the demands that are
          already consumed.</p>
        <p>User story - <a href="https://digit-discuss.atlassian.net/browse/RAIN-1893"><img src="https://digit-discuss.atlassian.net/secure/viewavatar?size=medium&amp;avatarId=10318&amp;avatarType=issuetype" alt/>RAIN-1893: Backend: Zero payment changesQA SIGNOFF</a>
        </p>
      </td>
    </tr>
  </tbody>
</table>

## Known Issues <a id="Known-Issues"></a>

None

## Upcoming Release Features <a id="Upcoming-Release-Features"></a>

None

## Reference Doc Links <a id="Reference-Doc-Links"></a>

| **Doc Links** | **Description** |
| :--- | :--- |
|  |  |

