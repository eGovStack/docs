---
description: DIGIT 2.0 Changes to the Water & Sewerage
---

# Water & Sewerage Release Notes

### Overview

Version 2.0 of 'Water & Sewerage' product allows the user to Apply for a New Water/Sewerage connection online. A citizen can apply for a new Water/ Sewerage connection Individually or in an Integrated manner. Citizen will receive a text and in-app notification on each step of the workflow. The Applications can be tracked online, in the 'My Applications' section provided to the citizen. Online application payment, send back to the citizen are some other features available for the citizen. Employees can search and process the application filed by the citizen. Some other features are workflow approval process, application payment collection etc.

### Release Highlights

1. W&S and Property integration, while applying for a New connection
2. Generation of artefacts at a desired stage of the application \(For eg. Generation of 'estimation notice' after the 'field inspector' approves the application\)
3. 'Send back' as a workflow step to facilitate employees to carry out, the desired correction in the application
4. Separate 'Search' for 'Connections' and 'Applications' on Employee side
5. Apply for an Integrated connection and track the applications individually \(Configurable workflow and calculation logic\)
6. The citizen can manage applications in the 'My Application' section also make payment for the application online.
7. Capture plumber information
8. Usage of Property ontology to cater to diverse use cases \(For eg. Water/Sewerage connections for Institutional, Commercial properties etc.\)

### Release Features

The W&S Version 2.0 release is equipped to allow citizens and employee to create an application for new water and sewerage connection online. The application is designed to facilitate the following affordance:

* Apply for water/sewerage connections including metered and non metered connection
* Addition of rebate/penalty on the employee side to cater use cases pertaining to the presence of any schemes
* Linkage of Property and W&S connection for a user
* Configurations available
  * Workflow actions and steps for application processing
  * Calculation logic for water and sewerage estimated demand
  * Estimation notice and sanction letter format

<table>
  <thead>
    <tr>
      <th style="text-align:left"><b>Key Features</b>
      </th>
      <th style="text-align:left"><b>Description</b>
      </th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Apply for new Water/Sewerage connection</td>
      <td style="text-align:left">
        <ol>
          <li>The user can apply for the connection individually or integrated</li>
          <li>For integrated connection, two separate applications are created. These
            applications are processed separately and can have a separate workflow,
            fee payment, SLAs, calculation logic etc.</li>
        </ol>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Role-Based Access for Employees</td>
      <td style="text-align:left">
        <ol>
          <li>Configurable role-action mapping</li>
          <li>Actors, actions and state can be configured as required</li>
          <li>Send back the application to the citizen</li>
        </ol>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Property Integration</td>
      <td style="text-align:left">
        <ol>
          <li>User can use his/her property ID to fetch property-related information
            and on the basis of that apply for a connection</li>
        </ol>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Capture Plumber details</td>
      <td style="text-align:left">
        <ol>
          <li>Plumber information ie. name, number, licence no. are captured in the
            system</li>
          <li>Better Communication and transparency, by bringing plumber info in the
            system</li>
        </ol>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">&apos;How it works&apos; section</td>
      <td style="text-align:left">
        <ol>
          <li>Videos can be uploaded about how to apply for a W&amp;S connection</li>
          <li>FAQs to handle common doubts</li>
        </ol>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">My Applications (Citizen)</td>
      <td style="text-align:left">
        <ol>
          <li>Applications filed by citizen are maintained in the &apos;My Application&apos;
            section</li>
          <li>The citizen can take required actions on the application ie. pay the fee,
            modify, track, submit, resubmit etc.</li>
        </ol>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Employee search screen</td>
      <td style="text-align:left">
        <ol>
          <li>Applications and connections can be searched using separate screens</li>
          <li>Different search parameters and search results, more flexibility</li>
          <li>Apply/Collect fee on behalf of citizen</li>
        </ol>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Pay application fee</td>
      <td style="text-align:left">
        <ol>
          <li>The citizen can pay the estimated connection charges online using the
            card</li>
          <li>Payment link in the application, mSeva notification, SMS notification</li>
          <li>The citizen can make payment at the counter using cash, DD, cheque</li>
        </ol>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Misc. features</td>
      <td style="text-align:left">
        <ol>
          <li>All artefacts formats ie. application form, estimation notice and sanction
            letter are configurable</li>
          <li>Citizens can maintain and download the artefacts</li>
          <li>Citizen gets notified at each workflow step</li>
          <li>Payment link in the SMS</li>
          <li>All the labels, legend names, etc. can be configured using localization
            service. It can support multiple languages</li>
          <li>For better usability and experience, the mobile view is optimized for
            each screen design</li>
        </ol>
      </td>
    </tr>
  </tbody>
</table>

**Notifications format**

<table>
  <thead>
    <tr>
      <th style="text-align:left"><b>Code</b>
      </th>
      <th style="text-align:left"><b>Type of Notification</b>
      </th>
      <th style="text-align:left"><b>Flow</b>
      </th>
      <th style="text-align:left"><b>Trigger Point</b>
      </th>
      <th style="text-align:left"><b>Receivers</b>
      </th>
      <th style="text-align:left"><b>SMS Message</b>
      </th>
      <th style="text-align:left"><b>In-app notification</b>
      </th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">NC-1</td>
      <td style="text-align:left">Event-based</td>
      <td style="text-align:left">Application submitted</td>
      <td style="text-align:left">Application Submission</td>
      <td style="text-align:left">All Owners + Applicant</td>
      <td style="text-align:left">Dear &lt;Owner Name&gt;, You have successfully submitted your application
        for a New &lt;Service&gt; Connection. Your Application No. is &lt;Application
        number&gt;. Click here to download your application &lt;Application download
        link&gt;. For more information, please log in to &lt;mseva URL&gt; or download
        &lt;mseva app link&gt;.</td>
      <td style="text-align:left">
        <p>Dear &lt;Owner Name&gt;, You have successfully submitted your application
          for a New &lt;Service&gt; Connection. Your Application No. is &lt;Application
          number&gt;.</p>
        <p>Action Button: Download Application</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">NC-2</td>
      <td style="text-align:left">Event-based</td>
      <td style="text-align:left">Application rejected</td>
      <td style="text-align:left">DV/JE/AP Rejects Application</td>
      <td style="text-align:left">All Owners + Applicant</td>
      <td style="text-align:left">Dear &lt;Owner Name&gt;, Your Application &lt;Application number&gt; for
        a New &lt;Service&gt; Connection has been rejected. For more details, please
        log in to &lt;mseva URL&gt; or download &lt;mseva app link&gt;.</td>
      <td
      style="text-align:left">Dear &lt;Owner Name&gt;, Your Application &lt;Application number&gt; for
        a New &lt;Service&gt; Connection has been rejected. Click here for more
        details &lt;View History Link&gt;</td>
    </tr>
    <tr>
      <td style="text-align:left">NC-3</td>
      <td style="text-align:left">Event-based</td>
      <td style="text-align:left">Application sent back</td>
      <td style="text-align:left">DV/JE/AP sends back Application</td>
      <td style="text-align:left">All Owners + Applicant</td>
      <td style="text-align:left">Dear &lt;Owner Name&gt;, Your Application &lt;Application number&gt; for
        a New &lt;Service&gt; Connection has been sent back. For more details,
        please log in to &lt;mseva URL&gt; or download &lt;mseva app link&gt;.</td>
      <td
      style="text-align:left">Dear &lt;Owner Name&gt;, Your Application &lt;Application number&gt; for
        a New &lt;Service&gt; Connection has been sent back. Click here for more
        details &lt;View History Link&gt;</td>
    </tr>
    <tr>
      <td style="text-align:left">NC-4</td>
      <td style="text-align:left">Event-based</td>
      <td style="text-align:left">DV : Application forwarded</td>
      <td style="text-align:left">DV forwards Application</td>
      <td style="text-align:left">All Owners + Applicant</td>
      <td style="text-align:left">Dear &lt;Owner Name&gt;, Status of your application &lt;Application number&gt;
        for a New &lt;Service&gt; Connection has changed to &#x2018;Pending for
        field inspection&apos; from &apos;Pending for document verification&#x2019;.
        For more details, please log in to &lt;mseva URL&gt; or download &lt;mseva
        app link&gt;.</td>
      <td style="text-align:left">Dear &lt;Owner Name&gt;, Status of your application &lt;Application number&gt;
        for a New &lt;Service&gt; Connection has changed to &#x2018;Pending for
        field inspection&apos; from &apos;Pending for document verification&#x2019;.
        To track your application, click on &lt;View History Link&gt;</td>
    </tr>
    <tr>
      <td style="text-align:left">NC-5</td>
      <td style="text-align:left">Event-based</td>
      <td style="text-align:left">JE : Application forwarded</td>
      <td style="text-align:left">JE forwards Application</td>
      <td style="text-align:left">All Owners + Applicant</td>
      <td style="text-align:left">Dear &lt;Owner Name&gt;, Status of your application &lt;Application number&gt;
        for a New &lt;Service&gt; Connection has changed to &#x2018;Pending : Approval
        for connection&apos; from &apos;Pending for field inspection&#x2019;. For
        more details, please log in to &lt;mseva URL&gt; or download &lt;mseva
        app link&gt;.</td>
      <td style="text-align:left">Dear &lt;Owner Name&gt;, Status of your application &lt;Application number&gt;
        for a New &lt;Service&gt; Connection has changed to &#x2018;Pending: Approval
        for connection&apos; from &apos;Pending for field inspection&#x2019;. To
        track your application, click on &lt;View History Link&gt;</td>
    </tr>
    <tr>
      <td style="text-align:left">NC-6</td>
      <td style="text-align:left">Event-based</td>
      <td style="text-align:left">AP: Application approves for connection</td>
      <td style="text-align:left">Approver approves for Connection</td>
      <td style="text-align:left">All Owners + Applicant</td>
      <td style="text-align:left">Dear &lt;Owner Name&gt;, Your New &lt;Service&gt; connection against the
        application &lt;Application number&gt; has been approved. To make payment
        against your application, please click on &lt;payment link&gt; . Log in
        to &lt;mseva URL&gt; or download &lt;mseva app link&gt; for more details.</td>
      <td
      style="text-align:left">
        <p>Dear &lt;Owner Name&gt;, Your New &lt;Service&gt; connection against the
          application &lt;Application number&gt; has been approved. To make payment
          against your application, please click on PAY NOW.</p>
        <p>Action button: PAY NOW</p>
        </td>
    </tr>
    <tr>
      <td style="text-align:left">NC-7</td>
      <td style="text-align:left">Event-based</td>
      <td style="text-align:left">Make Payment</td>
      <td style="text-align:left">Citizen/CEMP makes payment</td>
      <td style="text-align:left">All Owners + Applicant</td>
      <td style="text-align:left">Dear &lt;Owner Name&gt; , Your payment for New &lt;Service&gt; connection
        against the application &lt;Application number&gt; has been been successfully
        recorded. You can download your receipt using this link &lt;receipt download
        link&gt;. For more details, please log in to &lt;mseva URL&gt; or download
        &lt;mseva app link&gt;.</td>
      <td style="text-align:left">
        <p>Dear &lt;Owner Name&gt; , Your payment for New &lt;Service&gt; connection
          against the application &lt;Application number&gt; has been been successfully
          recorded. You can download the receipt by clicking DOWNLOAD RECEIPT</p>
        <p>Action button: DOWNLOAD RECEIPT</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">NC-8</td>
      <td style="text-align:left">Event-based</td>
      <td style="text-align:left">Connection activation</td>
      <td style="text-align:left">CL activates connection</td>
      <td style="text-align:left">All Owners + Applicant</td>
      <td style="text-align:left">Dear &lt;Owner Name&gt;, Your New &lt;Service&gt; connection against the
        application &lt;Application number&gt; has been activated. To check your
        connection details, please log in to &lt;mseva URL&gt; or download &lt;mseva
        app link&gt;.</td>
      <td style="text-align:left">Dear &lt;Owner Name&gt;, Your New &lt;Service&gt; connection against the
        application &lt;Application number&gt; has been activated. To check your
        connection details, click here &lt;connection details page&gt;.</td>
    </tr>
    <tr>
      <td style="text-align:left">NC-9</td>
      <td style="text-align:left">Event-based</td>
      <td style="text-align:left">Application edited</td>
      <td style="text-align:left">DV/JE/AP Edits the Application</td>
      <td style="text-align:left">All Owners + Applicant</td>
      <td style="text-align:left">Dear &lt;Owner Name&gt;, Your Application &lt;Application number&gt; for
        a New &lt;Service&gt; Connection has been edited. For more details, please
        log in to &lt;mseva URL&gt; or download &lt;mseva app link&gt;.</td>
      <td
      style="text-align:left">Dear &lt;Owner Name&gt;, Your Application &lt;Application number&gt; for
        a New &lt;Service&gt; Connection has been edited. Click here for more details
        &lt;View History Link&gt;</td>
    </tr>
  </tbody>
</table>

### Known Issues

* 'Property Type' localization value missing
* Owner details, in case of multiple owners, need to refresh for getting other names
* Not able to find Jalandhar property, Not working for Nawashahr as well \(For both citizen and employee\)
  * PB-PT-2020-04-04-004623 \(Nawashahr\)
  * PB-PT-2020-03-23-004500 \(Jalandhar\)
* Displaying random value in case of multiple owners
* Connection details missing from the Application summary page
* Incorrect names and random DOB value in Application summary page
* Application-based on the same property has different values for "Rainwater harvesting": Sewerage application: SW\_AP/1013/2020-21/062956 Water application: WS\_AP/1013/2020-21/062955
* Application forms PDFs for the applications mentioned above have incorrect values for mentioned fields
  * No. of floors \(It is not captured as a part of the property in case of Flat/part of a building, so this value is random\)
  * Property Sub Usage type
* After submission of the application by the counter employee,
  * Downloaded application PDF did not have meter installation date value, which was not also filled in the first place,
  * Task details page of Doc verifier is displaying a random date for the meter installation date
  * Downloaded application PDF by doc verifier still doesn't have the meter installation date
* No download/Print option to DV, FI, AP after submission \(Artifacts are needed to be downloaded\)
* Metered connection getting executed without initial meter reading

### Upcoming Release Feature

<table>
  <thead>
    <tr>
      <th style="text-align:left"><b>Features</b>
      </th>
      <th style="text-align:left"><b>Capability</b>
      </th>
      <th style="text-align:left"><b>Priority</b>
      </th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Misc features</td>
      <td style="text-align:left">
        <p>Keep the same consumer no.</p>
        <p>Enhance flow(Restrict actions)</p>
      </td>
      <td style="text-align:left">P2</td>
    </tr>
    <tr>
      <td style="text-align:left">Legacy Data Upload and Management</td>
      <td style="text-align:left">Facilitate legacy data upload including connection details and DCB details.
        Provision to correct connection details and accounts due to error while
        uploading data.</td>
      <td style="text-align:left">P1</td>
    </tr>
    <tr>
      <td style="text-align:left">Integrated Bill</td>
      <td style="text-align:left">
        <p>Group connections against Property ID</p>
        <p>Remittance in Different bank accounts</p>
        <p>Generate integrated bills</p>
      </td>
      <td style="text-align:left">P1</td>
    </tr>
    <tr>
      <td style="text-align:left">Handling advance payment</td>
      <td style="text-align:left">Accepting advance payment</td>
      <td style="text-align:left">P1</td>
    </tr>
    <tr>
      <td style="text-align:left">Door-step billing and collection</td>
      <td style="text-align:left">Edit meter reading. Ability to enable a door to door collection and generating
        bills on the spot once meter reading is updated in the system</td>
      <td style="text-align:left">P1</td>
    </tr>
    <tr>
      <td style="text-align:left">Connection against non-owner</td>
      <td style="text-align:left">
        <p>Title transfer</p>
        <ul>
          <li>Transfer of connection</li>
          <li>Mutation</li>
        </ul>
      </td>
      <td style="text-align:left">P2</td>
    </tr>
    <tr>
      <td style="text-align:left">Block-level due date on bills</td>
      <td style="text-align:left">Ability to Define different Due dates at Ward level (within the ULB)</td>
      <td
      style="text-align:left">P1</td>
    </tr>
    <tr>
      <td style="text-align:left">Apply flows</td>
      <td style="text-align:left">
        <p>Change of usage</p>
        <p>Non metered to metered</p>
        <p>Regularizing connection</p>
      </td>
      <td style="text-align:left">P2</td>
    </tr>
  </tbody>
</table>

### Reference Doc Links

<table>
  <thead>
    <tr>
      <th style="text-align:left"><b>Doc Link</b>
      </th>
      <th style="text-align:left"><b>Description</b>
      </th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">
        <ul>
          <li> <a href="https://digit-discuss.atlassian.net/wiki/spaces/EPE/pages/328925216/Water+Service+-+Technical+Document">Water Charges Service</a>
          </li>
          <li><a href="https://digit-discuss.atlassian.net/wiki/spaces/EPE/pages/329252923/Water+Calculator+Service+-+Technical+Document">Water Charges Calculator</a>
          </li>
          <li><a href="https://digit-discuss.atlassian.net/wiki/spaces/EPE/pages/328892444/Sewerage+Service+-+Technical+Document">Sewerage Charges Service</a>
          </li>
          <li><a href="https://digit-discuss.atlassian.net/wiki/spaces/EPE/pages/328892534/Sewerage+Calculator+Service+-+Technical+Document">Sewerage Charges Calculator</a>
          </li>
        </ul>
      </td>
      <td style="text-align:left">Apply for a new Water/Sewerage connection</td>
    </tr>
  </tbody>
</table>

