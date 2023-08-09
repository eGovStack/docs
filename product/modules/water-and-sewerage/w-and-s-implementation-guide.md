# W\&S Implementation Guide

## Section 1: Executive Summary

### Overview of the Product

Access to clean and safe water is one of the basic needs of citizens. Each Urban local body has been mandated with catering to the water and sanitation needs of its citizens. The computerized and automatic Water and Sewerage system offered by eGov enables citizens who seek to apply and pay for water and sewerage connections within any Urban Local Body with a transparent, speedy, hassle-free and user-friendly procedure. The ULB officials can now sanction connections, generate bills and collect payments for water and sewerage connections more efficiently. (For details on product features refer to Section-2)

### Implementation Methodology for W\&S

For the offered product, the implementation process can be divided into six major distinctive stages. Each stage has predefined entry and exit criteria, roles & responsibilities to assure objective monitoring and decision making for the overall success of the engagement. The whole implementation lifecycle is typical of 23-27 weeks for the State/UT keeping in mind the entry, and exit criteria defined at the beginning and end of each stage are met on time recommended.

![](https://lh6.googleusercontent.com/oTzTqSSRDKpFkpNzY9WL1gNp5X-I5LSRxIPs4LLZiyfp78EKyYJSDowUrkJC9X61ZlQ8UbbNr1r1mDHntUyxmMTfM9xd6P4Lmpm1hNQirB6lmWK-Vue6fHkDrx81jbgdUolVnYgx)

Stage Zero-program setup and onboarding is a pre-requisite for the initiative to kick-off and requires setup of the governance model, implementation team and decision regarding other significant elements of the initiative like funding and procurement process. Stage One of the initiative requires scoping of the initiative and decide on the priorities for implementation by the State/UT implementation Team. In Stage Two, the W\&S team is appointed and its processes are standardized. In Stage Three, the State/UT Team will work upon identifying and finding solutions to the significant gaps in the product offered w.r.t. to the need of the State/UT. Configuration and customization of the product offered in the primary objective of stage four. This involves working on various aspects of UT-specific needs and incorporating them into the product suite offered. In Stage Four and Five, post doing UAT and including all the necessary feedback on the product, the roll-out of the product is done at the State/UT level(Go Live) from a couple of ULBs to pan State/UT coverage. In Stage Six of sustenance and ongoing improvement, key activities are adoption and governance tracking with the planning of ongoing sustenance. (For details on implementation plan refer to Section-3).

### Critical Success Factors for implementation

Implementation of Water and Sewerage (W\&S) requires meticulous planning and close coordination between various stakeholders at the centre and State/UT level. The success of the initiative is dependent upon many factors like strong Program governance, availability of the trained resource, financial planning, targeted implementation Team onboarding, focus on last-mile capacity building and ensuring necessary support to the urban centre. Achievement of all these factors will provide the most effective and efficient roll-out and adoption of the Water and Sewerage Implementation System in the UT.

## Section 2: Water and Sewerage (W\&S) Product - Overview

The Water and Sewerage (W\&S) module provides a digital interface to apply for water and sewerage connections and pay the water and sewerage charges for connection/s. It can be used by the citizens, Urban Local Body (ULB) counter employees and field employees, and ULB Administrators to accomplish their specific tasks. It is available as a mobile and web-based application. The W\&S product features can be broadly classified as the following modules:

1. Registration, Login and Creation of User Profile
2. Application for new Water/Sewerage connection
3. Searching for a Connection
4. Modifications to a Connection
5. Entering meter reading of metered connections
6. Generate Demand
7. Payments collection and Receipts
8. Dashboards and Reports

### Module 1:  Registration, Login and Creation of User Profile

This module provides enables the following capabilities:

* OTP Based Login for Citizen via Web/Mobile App
* OTP Based Login for Employee via Web/Mobile App
*   Provision for language selection during first time registration for both Employee and

    citizens
* Provision of creating a personalized Profile for Citizens and employees on Web App
* Login Credentials for the various hierarchy of employees
* Role-based access for performing different actions relating to the W\&S module

### Module 2: Application for new Water & Sewerage connection

The system allows the Citizen / ULB user (with an appropriate role in the system) to apply for a New Water/Sewerage connection. The application goes through an approval workflow before it is available for various transactions in the system. The workflow to be followed for a new water/sewerage connection is configurable. In the workflow, the ULB official will generate the estimation notice. Once the payment is made, a work order will be generated.

Every time there is a change in the status of an application, the citizen will be intimated through in-app notifications, SMS and email. The citizen and employee can view the history of the various states that an application has been in and the comments added by the employee in each state of the application.

### Module 3: Searching for a Connection

Only employees from the W\&S department will be able to access the feature, to search for water and sewerage connections. They can search for any connection based on parameters such as:

* Consumer number
* Application number
* Owner mobile number
* Application status
* From date
* To date

The search result contains the Application number, Consumer number, Owner name, Status, Due amount and the Pay now option. The Employee can make payment for a connection on the citizen’s behalf using the ‘Pay Now’ option.

Citizens can also search for their connection in the portal. They can search using the Owners mobile number, Property ID, Consumer number etc. The search result yields, Owner’s Name, Address, Due amount and Pay option.

### Module 4: Modifications to a Connection

The system facilitates the title transfer of water tap connection from one person to the other person. Title transfer of water tap connection directly depends upon Property tax. If title transfer is done in the property tax module then at the time of final approval, the changes will reflect in the W\&S module automatically. After the title transfer has been completed successfully, subsequent bills will be generated with the details of the new owner/s.

Water tap change in usage happens when property type is changed from residential to Non-residential or from Non-residential to residential. Change in usage directly depends on the property tax module. If the property type is changed in the Property tax system then it will automatically reflect in the W\&S system. When there is a change in the usage type, the subsequent bills will reflect the rates as per the updated usage category. When there is a change in the usage category in the middle of the billing cycle, pro-rata charges will be applied in the next billing period.

The change in connection category from non-metered to metered and vice-versa is also possible in the W\&S system with the appropriate workflow configured to intimate all stakeholders of the change and collect any charges (if applicable) from the citizen.

### Module 5: Entering meter reading of metered connections

On the W\&S billing screen, there is a card called ‘Meter reading’. An employee can click on Meter reading which redirects the employee to the meter reading landing screen. The employee can search based on the following criteria:

* ULB
* Boundary Type
* Boundary Value
* Billing Year
* Billing Period
* Billing Period Value
* Consumer No.

This feature facilitates the employee to search for all results based on desired criteria. The search result yields the following values: consumer number, owner name, meter status, last reading, current reading, date and consumption.

The employee can edit meter status, current reading, date and consumption under certain conditions. Based on this information the employee can generate the bills for connections.

### Module 6: Generate Demand

In the system, there is a feature to generate demand under the billing section. Generate demand has a search feature in which the connections can be searched for which demand has been already generated. An employee can view, also edit those demands based on certain conditions.

The system has the capability to configure the demand generation as an automatic or a manual process. In the automatic process, the demand generation for non-metered connections is automatically done periodically. For metered connection as soon as the employee enters the meter reading and clicks on ‘SAVE’, the demand is generated.

Any success/ failure to generate demand triggers an automatic notification to the concerned ULB officials via email. Also, the demand generation cycle, demand generation date and officials who should receive the notifications can be configured.

### Module 7: Payments collection and Receipts

The citizen can pay for dues by searching his/her connection. In search results, the citizen can click on pay, which redirects to the summary page of the dues. After this, the citizen can pay for dues online. An employee can also collect the payment on the citizen’s behalf. After searching for the desired connection, clicking on pay will redirect the employee to the common payment page. The employee can print the receipt after the payment is successfully collected. The citizen is also notified and gets a download receipt link in the notification.

### Module 8: Closure of Water Connection

If the Water tap owner has got his own water source then the water tap owner can initiate for Water tap connection closure permanently. So, that tap will be closed permanently and demand would not be generated for the connection. Application for the closing of water tap connection is accepted only with the latest water charges receipt and clearing of old dues.

### Module 9: Dashboards and Reports

The state-level administrator can keep track of relevant metrics by using dashboards. Dashboards for W\&S can be accessed by a state-level user under login.

The dashboard has these components:

* Financial Indicators
  * W\&S Total collections YTD
  * Water Collection
  * Sewerage Collection
  * Water - Demand vs Collection (Monthly trend)
  * Sewerage - Demand vs Collection (Monthly trend)
* Municipal Adoption
  * W & S:  No. Of ULBs Live
  * W & S: Total Number of ULBs
  * Water Consumers by Connection Type
  * W & S Consumers by Usage Type
  * Total Collections by Source
  * Total Collections by Mode
  * W & S Adoption : ULB Wise
* Today’s Collections
  * W\&S Total collections: Today
  * Water Charges - Total collections: Today
  * Sewerage Charges - Total collections: Today
  * W\&S - Total No. of Receipts: Today
  * Water - Total No. of Receipts: Today
  * Sewerage - Total No. of Receipts: Today
  * Mode wise W\&S collections: Today
  * W\&S ULB wise collections: Today

## Water & Sewerage (W\&S) Implementation Methodology for the State of xxx

## Section 3 Water and Sewerage (W\&S) Implementation Methodology

This section provides an overview of the methodology for State-wide implementation of W\&S. The Implementation of W\&S is distributed across seven distinct stages. Each stage has predefined entry & exit criteria and roles & responsibilities. This is to ensure objective monitoring and decision making for the overall success of the program. Details of each stage are defined in this section.

![](https://lh4.googleusercontent.com/bN1Oeyb0rz8voxHH4pNMbAynq8W0uEBvQwtErV6ZvVaP5FfbNFoHrURdS8MYFfslR079BInVnPpWt10cAOJEh6fT\_diHc\_RUHu3YxlzFUPLggZ2AVwaAHsWvLNNCUWpryOuX8zbo)

{% hint style="info" %}
Note: This document is specific for States that have more than 30 ULBs.
{% endhint %}

W\&S implementation program is expected to be completed approximately between 38- 42 weeks with the resource deployment by the State and System Integrator (SI) Team (as defined below). However, it is critical that activities and exit criteria set for each stage are achieved to adhere to this timeline.

## Seven Stages of Implementation

### Stage 0 - Program Setup/Onboarding

There is a set of initial critical activities that are undertaken on receiving a letter of Enrollment from the State/Union Territory. Successful completion of these activities assures that the program is started with crucial personnel, System Integrator(SI) Teams and funds.

| Stage 0 - Program Setup/ On-Boarding |                                                                                                                                                                                                                                                                                                                                                                                                                  |
| ------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Duration                             | 4-6 weeks                                                                                                                                                                                                                                                                                                                                                                                                        |
| Entry Criteria                       | Acceptance Letter/MoU by State                                                                                                                                                                                                                                                                                                                                                                                   |
| Exit Criteria                        | <ul><li>Finalize Water and Sewerage Program Vision</li><li>Finalize funding for the program</li><li>Define State/Union Territory -specific procurement process</li><li><p>Water and Sewerage Cell appointment. Consisting of :</p><ul><li>Domain expert</li><li>Nodal officer (EO/ Commissioner/ Senior Official)</li><li>Program Head</li></ul></li><li>System Integrator(SI) Team sign-up/onboarding</li></ul> |

#### Vision:

* Define the value proposition of the programme  for the state &#x20;
* Define the  time frame within which the state needs to:
  * Go live
  * Scale pan-state
* Define Year-on-Year(YoY) Financial Targets

System Integrator(SI) Sign-up:

* System Integrator and state will agree on program scope, program timelines, and budgeting & resourcing.

### Stage 1 - Program Kick-Off

This stage envisages the in-person interaction of crucial State/UT officials and implementation System Integrator(SI) Teams to kick-start the program. This stage may require multiple interactions/meetings with different stakeholders. The principal objective of these interactions is to identify scope, plan strategies for phasing/rollout (in pilot ULBs/Pan State) and create an active collaboration & Governance approach and agree on a high-level timeline for the engagement.

| Stage 1 - Program kick-off |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| -------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Duration                   | 4-6 weeks                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| Entry Criteria             | <ul><li>Program setup (Stage 0) is complete</li><li>SI Team signed-up</li></ul>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| Key Activities             | <ul><li>Project kick-off meeting and stakeholders consultation</li><li>Identify &#x26; agree on scope and exclusions</li><li>Finalize the approach on obtaining the W&#x26;S Connection Legacy Data (At least from the Pilot ULBs)</li><li>Identify pilot ULBs</li><li>Product Walkthroughs</li><li>Define Project Steering Committee Structure and Project Governance process</li><li>Define phases of rollout/ deployment</li><li>State Baseline Data (As per the Module)</li><li>Pilot ULBs Specific Product Data Configuration</li><li>Agreement on Product Feature Priorities and high-level delivery timelines</li><li>Assessment of all on ground W&#x26;S process along (1) citizen services/channels around it (2) Integration with other Department process</li><li>Finalize Program Success Metrics for Rollout and Adoption and Governance adhering to the vision of the program</li><li>Internal Capacity Building, program logistics at State and ULBs, as per the current scenario</li></ul> |
| Exit Criteria              | <ul><li><p>Publish the program charter</p><ul><li>Implementation plan agreement with priority applications and broad timelines</li><li>Program Governance Model</li><li>Program Success Metrics</li><li>Capacity Building</li></ul></li><li>W&#x26;S Cell formation and appointment</li><li>Finalizing the strategy for W&#x26;S Connections Legacy Data</li><li>Master Data preparation/collection kickoff from Pilot ULBs</li><li>Cloud Infrastructure procured</li><li>Project Office Space allocated</li><li>Program Branding( Name, Logo, Tagline etc.)</li></ul>                                                                                                                                                                                                                                                                                                                                                                                                                                      |

{% hint style="info" %}
**Note**

1\) State Baseline Data (As per the Module): A Baseline Template is provided to collect certain vital information like no. of transactions, revenue collected in the last FYs, collection mode, budget data, etc. This data is vital for various analysis at the state level. This data must be collected pre-rollout. The baseline data collection templates will be provided to the state/SI Team.

2\) ULBs Specific Product Data Configuration: This Master data is required from the Product Perspective to go live. For eg: Connection Legacy Data, Boundary Data, List of Employees, Rates etc. Master Data Template will be provided for the collection of this particular data type.
{% endhint %}

### Stage 2 - Solution Design

During the Solution design stage, key State/UT officials and members, who are subject matter experts, are expected to share State/UT acts and policies and help interpret the same for the System Integrator (SI) Team. This stage baselines the State/UT-specific product features in the Product Configuration report.

| Stage 2 - Solution Design |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| ------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Duration                  | 4-6 weeks                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| Entry Criteria            | <ul><li>Program Charter</li><li>W&#x26;S Cell appointment</li></ul>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| Key Activities            | <ul><li>Standardization of all W&#x26;S processes, if needed</li><li>Initiate policy change and Process Re-engineering, if needed based on identified improvements</li><li>Conduct Product familiarization workshop</li><li>Initiate collection of Master Data (Legacy &#x26; Product Based) from pilot ULBs</li><li>Finalize data migration/collection/sync-up approach (State needs to provide a signoff)</li><li>Finalize data validation approach (State needs to provide a signoff)</li><li>Building capacity for basic understanding of resources and tools required to be used</li></ul> |
| Exit Criteria             | <ul><li>Publish the W&#x26;S processes, data template/workflows (State needs to provide a signoff)</li><li>Finalization of Roll-out plan(in different phases)</li><li>Solution agreement for required state/UT-specific customisations</li><li>Finalization of Initial Reporting and Design (State needs to provide a signoff)</li><li>Finalization of Dashboard KPIs (State needs to provide a signoff)</li><li>Sign-off on data approach( Data collection/migration/correction/sync-up/validation) from the state</li><li>Detailed project plan</li></ul>                                     |

### Stage 3 - Configuration & Customization

This stage consists of a series of developments in accordance with the detailed project plan to ensure the smooth functioning of the customised product. Preparation for the testing and data collection of the product UAT is complete. Further monitoring and maintenance strategies are put in place.

| Stage 3 – Configuration & Customization |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| --------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Duration                                | 6-8 weeks                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| Entry Criteria                          | <ul><li>Product Configuration Report has been Signed Off by the State/UT</li><li>Detailed Project Plan set up in accordance with master data collection and environment setup</li></ul>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| Key Activities                          | <ul><li>Setting up development environments</li><li>Development/customization of reports and dashboards</li><li>Development/Integration of portal</li><li>Third-Party Integrations (Payment gateway, Handheld/pos device)</li><li>Updation of user manuals and other key documents</li><li>Preparation &#x26; execution of Test Cases</li><li>Setup monitoring, support &#x26; maintenance processes and tools</li><li>W&#x26;S and Legacy data collection from Pilot ULBs (at least)</li><li><p>Training for basic understanding of resources and tools required to be used (system-related)</p><ul><li>identify ULB level nodal officers for day to day support</li></ul></li><li><p>Legacy Data Validation signoff from the state on Data Validation</p><ul><li>Post this migration exercise will be taken up for water/sewerage connections</li><li>Migration and verification of Pilot ULB data as per data provided by the State</li></ul></li></ul> |
| Exit Criteria                           | <ul><li>Data Validation Signoff by the state, post which the Legacy Data will be uploaded to UAT</li><li>Configured/Customized product that is ready for UAT</li><li><p>Monitoring, support &#x26; maintenance of Dashboards</p><ul><li>finalization of Initial Reporting and Dashboard KPIs</li></ul></li></ul>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |

### Stage 4 - UAT & Go Live

During this stage, a demonstration of the product followed by a hand on session is conducted for the ULB officials. Necessary training of ULB officials and resources required for UAT is conducted and identified respectively. The establishment of the State/UT support Team and required processes are initiated in this stage.

| Stage 4 – UAT & Go Live |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| ----------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Duration                | 2-3 weeks                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| Entry Criteria          | <ul><li>Configured/Customized product ready for UAT</li><li>Pilot ULB Officials (Associated with W&#x26;S) are available for UAT &#x26; Training</li></ul>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| Key Activities          | <ul><li>UAT Environment Setup</li><li>Sign off from Pilot ULBs on the Migrated Connection Legacy Data during UAT</li><li>Issues/bug identification and resolution</li><li>Regression UAT and Sign off from Pilot ULBs/ State</li><li>Setting up the Production environment</li><li>Setting up Support Center &#x26; processes (Help Desk)</li><li><p>Training (Users, trainer)</p><ul><li>master trainers identified from the ground for simultaneous training</li></ul></li><li>Training the Support Resources</li><li>Marketing &#x26; promotion activities</li><li>Go Live &#x26; launch event</li><li><p>Setup of review and monitoring cadence/team</p><ul><li>Usage/review/Dashboard/Field Visits</li></ul></li></ul> |
| Exit Criteria           | <ul><li>UAT Sign-off &#x26; Go Live for Pilot ULBs</li><li>Setup of review and monitoring cadence</li></ul>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |

### Stage 5 – Rollout

On successful Go-Live in the Pilot ULBs, after further configurations to stabilize the product, the solution will be rolled out to the rest of the ULBs in multiple phases. Guidance and support from the State/UT Team will be required to create the rollout plans and assure the necessary infrastructure for training and deployment is available at each ULB.

{% hint style="info" %}
Note: The rollout phase needs to be detailed out for iterative activities of onboarding ULBs in batches.
{% endhint %}

| Stage 5 – Rollout |                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| ----------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Duration          | 5-6 weeks                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| Entry Criteria    | <ul><li><p>The pilot has been successful in the State/UT</p><ul><li>there are less than 3 open critical incidents (issues) with respect to product, implementation and data</li></ul></li></ul>                                                                                                                                                                                                                                                         |
| Key Activities    | <ul><li>ULB configurations phase-wise as per the Project Plan</li><li>Phase wise migration and verification of ULB data (as per the Data Agreement signoff, provided by the State)</li><li>Logistics planning for training</li><li>Establishment of bug ticketing tool for resolving ground-level issues by the state team</li><li>Training the Users at the district level</li><li>Pan State Roll-Out - Phase wise</li><li>Stabilise product</li></ul> |
| Exit Criteria     | <p>State/UT wide Rollout in batches:</p><ul><li>Adoption tracking &#x26; Review Cadence operational</li><li>Help Desk Effectiveness assured</li><li>Critical Bugs fixed</li><li>Program Success Metrics Tracking Kick-started</li></ul>                                                                                                                                                                                                                 |

{% hint style="info" %}
Note: Only once all the stages are complete in one batch of the rollout of around 30 ULBs, the next batch begins. There are multiple phases of rollout. The second batch begins after the first batch has successfully fulfilled all the criteria of the Rollout Phase. Typical timelines for closure of rollout in each batch is 5-6 weeks (in a batch of 30 ULBs).
{% endhint %}

### Stage 6 – Sustenance and Ongoing Improvement

The final stage consists of strategies to ensure the sustenance of the product in the State/UT. Systems are put in place to ensure the continuous tracking of data and provisions are made to improve the product if new data suggest.

| Stage 6- Sustenance and Ongoing Improvement |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| ------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Duration                                    | Ongoing process                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| Entry Criteria                              | <ul><li>Rollout Phase 1( First set of 30 ULBs where rollout will happen after Pilot)</li></ul>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| Key Ongoing Activities                      | <ul><li>Adoption Review Meetings as per the vision defined for the program</li><li>W&#x26;S Cell Focuses on Using data for:</li><li>tracking field issues and performance data to identify improvements</li><li>identify additional Integrations around W&#x26;S to make processes more robust towards enhancing W&#x26;S revenues (e.g Upstream and downstream Processes)</li><li><p>Conduct Weekly Review Meeting between ULBs, State Team for feedback on the system, which must be chaired by the Program Head</p><ul><li><p>Plans of ongoing Sustenance in Place with respect to :</p><ul><li>Funding</li><li>IT support (infra, helpdesk, ongoing enhancements)</li><li>Process Effectiveness and Improvements</li></ul></li></ul></li></ul> |

## Section 4: Roles and Responsibilities – W\&S Cell, NUS Team & System Integrator (SI)Team

This section outlines the activities involved in each stage of the implementation along with the responsibility and accountability of critical stakeholders - UT, NUS Team and System Integrator Team onboard.

W\&S Cell: W\&S Cell is the government-appointed body chaired by the Principal Secretary/Secretary, Urban Development Department with members from Urban Development Department etc.

Resource requirements for the W\&S cell required to be formed by the UT

| Resource Name | No. Of Resources |
| ------------- | ---------------- |
| Project Head  | 1                |
| Domain Expert | 2                |
| Nodal Officer | 2                |
| MIS Expert    | 4                |

{% hint style="info" %}
Note: Designation mentioned above are as per designations known driving W\&S implementation at the State/UT level as explained below. (These are the preferred figures in the case of Domain Expert, 2 people are subject to availability)
{% endhint %}

* Project Head: Is the Head of the W\&S Cell who will drive the project from the State/UT Side
* Domain Expert: Person who is well aware of the on-ground scenario, well versed with the act, GOs passed, Prevalent Business processes, Deviations from the acts,  Rates/ slabs applicable&#x20;
* Nodal officer (EO/Commissioner/ Senior Official): the product coordinator to drive the project centrally. Monitor usage post Go Live- point of escalation for Implementation Team, Seasoned and worked in Multiple ULBs on various modules and has a good understanding of W\&S, Facilitate and Track data collection Post Go Live, Monitors and facilitates the adoption of the application. point of contact for eGov, SI and at the HQ level.
* MIS Expert: Day to day tracking of the program, data entry, reporting and review to senior officials

eGov Team: eGov Team is the technical partner of the project which will provide all necessary support to the State/UT concerning the implementation, Program Designing etc.

System Integrator (SI) Team: SI Team will be responsible for the rollout of the initiative in the UT, providing end to end support to the State/UT w.r.t. The implementation of the products in the ULBs.

Guidelines to read the table are mentioned on the next page:

* Execute - One who owns the accountability to complete the activity
* Consult - One who may initiate, guide and in the process, handhold the execution of the activity

| Stage 0 - Program Setup/ On-Boarding          |          |                      |
| --------------------------------------------- | -------- | -------------------- |
| **Task/Activity**                             | **eGov** | **State Leadership** |
| Appoint W\&S Cell                             | Consult  | Execute              |
| Finalize funding for the program              | Consult  | Execute              |
| Define state/UT-specific procurement process  | Consult  | Execute              |
| System Integrator(SI) Team sign-up/onboarding | Consult  | Execute              |
| Finalize Water and Sewerage Program Vision    | Consult  | Execute              |

Note: Stage 0 is where the W\&S cell and SI team are formed, hence there are only two entities playing a role which is that of eGov and the state leadership. Once the W\&S cell and SI team are finalized, their role begins in the following stages.

| Stage 1 - Program kick-off                                                                                                                              |          |               |             |
| ------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | ------------- | ----------- |
| **Task/Activity**                                                                                                                                       | **eGov** | **W\&S Cell** | **SI Team** |
| Identify & agree on scope and exclusions                                                                                                                | Consult  | Consult       | Consult     |
| Identify pilot ULBs                                                                                                                                     |          | Execute       | Consult     |
| Project kick-off meeting and stakeholders consultation                                                                                                  |          | Execute       | Consult     |
| Product Walkthroughs                                                                                                                                    | Consult  |               | Execute     |
| Define Project Steering Committee structure and Project Governance process                                                                              | Consult  | Consult       | Execute     |
| Define phases of deployment/ rollout                                                                                                                    | Consult  | Consult       | Execute     |
| Agreement on Product Feature Priorities and high-level delivery timelines                                                                               |          | Consult       | Execute     |
| <p>Assessment of all W&#x26;S process along</p><p>(1) citizen services/channels around it</p><p>(2) Integration with other department processes<br></p> |          | Consult       | Execute     |
| <p>Finalize Program Success Metrics for Adoption and Governance adhering to the vision of the program<br></p>                                           |          | Consult       | Execute     |
| Internal Capacity Building, program logistics at State and ULBs, as per the current scenario                                                            |          | Execute       | Consult     |

| Stage 2 - Solution Design                                                                     |          |               |             |
| --------------------------------------------------------------------------------------------- | -------- | ------------- | ----------- |
| **Task/Activity**                                                                             | **eGov** | **W\&S Cell** | **SI Team** |
| Standardisation of all W\&S processes, if needed                                              |          | Consult       | Execute     |
| Initiate policy change and Process Re-engineering, if needed based on identified improvements | Consult  | Execute       | Consult     |
| Conduct Product familiarization workshop                                                      | Consult  | Consult       | Execute     |
| Initiate collection of master data from pilot ULBs                                            |          | Consult       | Execute     |
| Finalize data migration/collection/sync-up approach                                           |          | Consult       | Execute     |
| Finalize data validation approach                                                             |          | Execute       | Consult     |
| Building capacity for basic understanding of resources and tools required to be used          |          | Execute       | Consult     |

| Stage 3 – Configuration & Customization                                                      |          |               |             |
| -------------------------------------------------------------------------------------------- | -------- | ------------- | ----------- |
| **Task/Activity**                                                                            | **eGov** | **W\&S Cell** | **SI Team** |
| Setting up development environments                                                          |          | Consult       | Execute     |
| Development/customization of reports and dashboards                                          |          | Consult       | Execute     |
| Development/Integration of portal                                                            |          | Consult       | Execute     |
| Third-Party Integrations (Payment gateway, Handheld/pos device)                              |          | Consult       | Execute     |
| Updation of user manuals and other key documents                                             |          | Consult       | Execute     |
| Preparation & execution of Test Cases                                                        |          | Consult       | Execute     |
| Setup monitoring, support & maintenance processes, tools and dashboards                      |          | Consult       | Execute     |
| Data Migration for Pilot ULBs(at least)                                                      |          | Consult       | Execute     |
| Training for basic understanding of resources and tools required to be used (system-related) |          | Execute       | Consult     |
| Legacy Data Validation signoff from the state on Data Validation                             |          | Execute       | Consult     |

| Stage 4 – UAT & Go Live                                                          |          |               |             |
| -------------------------------------------------------------------------------- | -------- | ------------- | ----------- |
| **Task/Activity**                                                                | **eGov** | **W\&S Cell** | **SI Team** |
| UAT Environment Setup                                                            | Consult  | Consult       | Execute     |
| UAT Testing                                                                      |          | Consult       | Execute     |
| Issues/bug resolution                                                            |          | Consult       | Execute     |
| UAT Sign off from Pilot ULBs                                                     |          | Execute       | Consult     |
| Setting up the Production environment                                            |          | Consult       | Execute     |
| Setting up Support Center & processes (Help Desk)                                |          | Execute       | Consult     |
| Training (Users, trainer)                                                        |          | Execute       | Consult     |
| Training the Support Resources                                                   |          | Consult       | Execute     |
| Marketing & promotion activities                                                 |          | Execute       | Consult     |
| Go Live & launch event                                                           |          | Execute       | Consult     |
| Setup of review and monitoring cadence/team Usage/ review/Dashboard/Field Visits |          | Execute       | Consult     |

| Stage 5: Rollout                                  |          |               |             |
| ------------------------------------------------- | -------- | ------------- | ----------- |
| **Task/Activity**                                 | **eGov** | **W\&S Cell** | **SI Team** |
| ULB configurations                                |          | Consult       | Execute     |
| Phase wise Migration and verification of ULB data |          | Execute       | Consult     |
| Logistics planning for training                   |          | Execute       | Consult     |
| Training the Users at the district level          |          | Execute       | Consult     |
| Roll Out - All Locations                          | Consult  | Execute       | Execute     |
| Stabilize product                                 |          | Consult       | Execute     |

| Stage 6- Sustenance and Ongoing Improvement                                                                                                                                                                                                                                                             |          |               |             |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | ------------- | ----------- |
| **Task/Activity**                                                                                                                                                                                                                                                                                       | **eGov** | **W\&S Cell** | **SI Team** |
| Adoption Review Meetings as per the vision defined for the program                                                                                                                                                                                                                                      | Consult  | Execute       | Consult     |
| <p>W&#x26;S Cell Focuses on Using data for:</p><ul><li>tracking field issues and performance data to identify improvements</li><li>identify additional Integrations around W&#x26;S to make processes more robust towards enhancing W&#x26;S revenues (e.g Upstream and downstream Processes)</li></ul> |          | Execute       | Consult     |
| Conduct Weekly Review Meeting between ULBs, State Team for feedback on the system, which must be chaired by the Program Head                                                                                                                                                                            |          | Execute       | Consult     |
| <p>Plans of ongoing Sustenance in Place with respect to :</p><ul><li>Funding</li><li>IT support</li><li>Process Effectiveness and Improvements</li></ul>                                                                                                                                                | Consult  | Execute       | Consult     |

## Section 5: Overall Program Assumptions

| Areas          | Assumptions                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| -------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Infrastructure | <ul><li>The actual Infra will be provided based on the questionnaire inputs received from the state</li><li>The state will take care of providing necessary project infrastructure and office facilities during the program for all on-site project Team members, which will be confirmed during the initiation phase. This includes workspace, office equipment (e.g., telephone with STD, fax machine, photocopy machine, etc.), stationery, PC/workstation, project LAN and internet access, etc.</li><li>The state will provide the necessary administrative support staff to carry out day-to-day project administration tasks, e.g., meeting rooms, Videoconferencing, etc.</li><li>The state should provide a Project Office and at least one conference room with a speaker phone throughout the Project Duration.</li></ul> |
| Project Scope  | <ul><li>Any new requirements received from the State during the implementation phase will be handled through a change management process</li></ul>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| State Team     | <ul><li>The state will nominate a reasonably sized multifunctional Team from various departments of the State to be responsible for the implementation. The state Team would be required for information, validation, and execution through the implementation cycle and the Team members should be reasonably empowered to take decisions. Any delay in the decision-making process and the non-availability of the State Team may have an impact on the schedule.</li><li>The participants from State are expected to have a thorough understanding of the State’s internal processes.</li><li>The state will engage internal and external stakeholders required for this engagement and ensure their availability whenever needed.</li></ul>                                                                                      |
| Documentation  | <ul><li>User education and training documentation will be delivered as per the default product documentation of the identified product versions.</li><li>The product manuals are expected to be shared with the State as part of the user manual.</li><li>All documentation would be in English only.</li></ul>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| Training       | <ul><li>Training to the end-users will be driven by the state Team.</li><li>The state will be responsible for providing the necessary infrastructure required for the Training, which includes the following readiness.</li><li>Training Rooms (Parallel Training Sessions) with Projector, White Board, Markers, Internet Connection, sufficient seating capacity, Desktop/Laptop for each participant and availability of Network for Trainees to connect to the server.</li></ul>                                                                                                                                                                                                                                                                                                                                                 |
| Implementation | <ul><li>The scope of the implementation will be limited to the services mentioned in Section 2.</li><li>eGov Team will have an identified SPOC for handling the first level of communication with the client unless discussed and agreed upon.</li><li>eGov Team will not be involved in defining the test cases or executing the test cases.</li><li>Necessary signoff would be provided by the state upon completion of the defined milestones.</li></ul>                                                                                                                                                                                                                                                                                                                                                                          |

## Glossary

| PROGRAM |
| ------- |

Vision: Defining the time frame to go live, the time frame to scale it pan state, the value proposition of the programme for the state and year-on-year financial targets and adoption targets

Project Plan: A detailed plan of Program schedule/timelines, implementation phases, team structure and ongoing support and maintenance required.

System Integrator: The Entity/Company which collates all the subsystem required for the project and integrates them to achieve the program objective

Program Charter: Outline of implementation plan agreement with priority applications and broad timelines, program governance model, program success metrics and capacity building.

Acceptance Letter/MOU: Formal Acceptance/Sign Off of the Client State with a clear mandate of the Program

Program Success Metrics: Defining the parameters (which are measurable) prior to the program, on which the success of the program is to be measured on the completion of the program

Project steering committee: The key body within the governance structure which is responsible for the business issues associated with the project that are essential in ensuring the delivery of the project outputs and the attainment of project outcomes.

Project governance: Set of policies, regulations, functions, processes, procedures and responsibilities that define the establishment, management and control of projects, programmes and portfolios.

| IMPLEMENTATION |
| -------------- |

Scoping: List of activities measured against the time taken to complete them in accordance with the project goals

Baseline data: Set of information that serves as a foundation to compare other data acquired afterwards

Project Kick-off meeting: Meeting with the project team and the client of the project. This meeting would follow the definition of the base elements for the project and other project planning activities

Fitment Study: GAP Study of the Existing/Required Field Process Vs Product

Data migration: Existing Records of the functional activities need to be moved into the Database of the newly released Application

Data collection: Required data for the roll-out of the applications, which needs to be collected from the existing functional process

Data validation approach: This approach enables the sanctity of the Data with built-in validation by Design

Data synchronization: The process of establishing consistency among data from a source to a target data storage and vice versa and the continuous harmonization of the data over time.

Pilot Implementation: Any new process is tested out as a pilot in one or two instances before pan implementation

Pilot ULB: The ULBs selected for the pilot implementation are called pilot ULB.

Roll out: On successful clearance of the Pilot, the Process/Application/Services are implemented across all Offices/ULB's

Deployment: Deployment defines the complete package of Software components set up in a particular environment

| PRODUCT |
| ------- |

Customisation: Details of changes to be made in the Product to comply with the needed field process

Configuration: Defining existing content such as Options and Variables based on the requirements on the ground

Product walkthrough: Explaining the users step-by-step through a set of actions that they need to take to achieve a specific outcome

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)​](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation](https://egov.org.in/) is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).
