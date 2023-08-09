# PT Implementation Guide

## Executive Summary

### Overview of the Product

The computerized and automatic Property Tax system offered by eGov, facilitates citizens who seek to pay their Property Tax within any Urban Local Body with a transparent, speedy, hassle-free and user-friendly procedure. Property Tax (PT) is one of the components of a smart city that has the capability of providing the highest revenue of a state. Keeping in mind the benefits associated with the product offered, the proposed system is about to be implemented in 500+ ULBs across the country in 15 states. (For details on product features refer to Section-2)

### Implementation Methodology for PT

For the offered product, the implementation process can be divided into seven major distinctive stages. Each stage has a predefined entry and exit criteria, roles & responsibilities to assure objective monitoring and decision making for the overall success of the engagement. The whole implementation lifecycle is typical of 38-42 weeks for the State, keeping in mind the entry, and exit criteria defined at the beginning and end of each stage are met on time recommended.

![Exhibit 1: Phases of Implementation.](https://lh4.googleusercontent.com/YbdylRaOH65fQXr1Rx9jOLbo4RCaoCdiKyjDGXVp0LsXILVc0-SA-UBFL--XMm2\_MHs0LOKVee2zzTq2ctMzH2F0ewG9y7MQJmXv8CSwnur9EfHaUTiqC5tEYfbCNGWkaOZU-aI)

Stage Zero-program setup and onboarding is a pre-requisite for the initiative to kick-off and requires setup of the governance model, implementation Team and decision regarding other significant elements of the initiative like funding and procurement process. Stage One requires scoping of the initiative and decisions on the priorities for implementation by the State Implementation Team. In stage two, the State Team will work upon identifying and finding solutions to the significant gaps in the product offered with respect to the need of the State. Configuration and customization of the product offered is the primary objective of stage four. This involves working on various aspects of State-specific needs and incorporating them into the product offered. In stage five, post doing UAT and including all the necessary feedback on the product, the roll-out of the product is done at the State level (Go Live) from a couple of ULBs to pan State coverage in batches. Finally, in stage 6 sustenance and ongoing improvements are worked upon while the product is already functioning in the State. (For details on implementation plan refer to Section-3)

### Critical Success Factors for implementation

Implementation of Property Tax (PT) requires meticulous planning and close coordination between various stakeholders at the center and State level. The success of the initiative is dependent upon many factors like strong Program governance, availability of the trained resource, financial planning, targeted Implementation Team onboarding, focus on last-mile capacity building and ensuring necessary support to Urban center. Achievement of all these factors will provide the most effective and efficient roll-out and adoption of the Property Tax System in the State.

## Property Tax (PT) Product - Overview

The Property Tax System(PT) provides a digital interface to make property assessments, pay property tax, generate payment receipts and monitor tax collection. It can be used by the citizens, Urban Local Body (ULB) counter and field employees, and ULB Administrators to accomplish their specific tasks. It is available as a mobile and web-based application. The PT product features can be broadly classified as the following modules:

1. Registration, Login and Creation of User Profile
2. Filling an Assessment for a Property
3. Searching for a Property
4. Modifications to a Property
5. Generate Demand Notice
6. Payments collection and Receipts
7. Dashboards and Reports
8. General Features

### Module 1:  Registration, Login and Creation of User Profile

This module provides enables the following capabilities

* OTP Based Login for Citizen via Web/Mobile App
* OTP Based Login for Employee via Web/Mobile App
* Provision for language selection during first time registration for both  Employee and citizens
* Provision of creating a personalized Profile for Citizens and employees on Web App
* Login Credentials for various hierarchy of employees
* Role based access for performing different actions relating to property tax modules

### Module 2:   Filing an Assessment for a Property

With this feature, a citizen and employee can perform self assessment of a new property for a financial year. This feature helps in registering the property in the system. The details of the property can be entered online and can be assessed for calculation of the taxes. The PT Product is designed in a user friendly manner and reduces chances of error. System calculates the tax automatically and creates the demand. If a user wants to reassess his property due to any reason (for eg, incorrect data, change in property etc), it can be done by editing details of last assessment. Employee can edit the details of the last assessment, on behalf of the citizen based on owner’s input. Citizen can track down the status of his incomplete assessment. Any incomplete assessment can be searched and completed.

This module provides enables the following capabilities:

* Citizen/CSC can Assess New Property (By Different Financial Years).
* Citizen/CSC can Capture Address, Assessment Info, Owner Info.for all types of properties like residential houses, flats and commercial buildings.
  * Sample Details captured:
* Door Number,&#x20;
* Mutation number,&#x20;
* Number of floors,
* Area covered,&#x20;
* Owner and co-owner,&#x20;
* Mailing & permanent address,&#x20;
* Built year
* Individual room measurements
* The system computes the property taxes automatically as per process and rules of the state.&#x20;
* The system has a facility to make entry in system by inspector after site visit and assessment of the same by the superintendent.
* The system supports dynamic calculation for late fees, interest, rebates, etc. as on the day of demand generation.
* The system fetches the data of previous year property data while e-filing for current year so that all the dues are calculated.
* The system assigns a unique property ID based on the process defined in the ULBs.
* Citizen/CSC : View/Print Summary of Filled Form
  * Assessment Form
  * Assessment Form is also sent by email to citizen
* Upload Documents
  * Ownership/Title related
  * ID Proof
  * Any other statutory documents

### Module 3:   Searching for a Property

Citizen or Employee can track down the status of his incomplete assessment. Any incomplete assessment can be searched and completed.

This module provides the following capabilities:

* Citizen/CSC can search for Property by&#x20;
  * Mobile No,
  * City,&#x20;
  * Property Tax Unique ID
* Citizen/ CSC can view Incomplete Assessments
* Citizen/CSC can reassess Searched Property
* View Property details and pending dues

### Module 4:  Modifications to a Property

The PT system provides the ability to capture mutation and transfer of ownership. It reduces interfaces between the user and the State and thus promote greater transparency. It also helps in reducing the time taken for mutation after registration. The system provides the ability for alteration of assessment after verification and inspection. Any structural changes like addition/extension/reduction of existing built up area or construction type OR utility changes like usage or occupancy have an impact on the increase/decrease in property tax demand. These changes can be handled by the ‘Additional/Alteration of Assessment’ feature. The System provides the ability for bifurcation/ amalgamation of property. The property bifurcation/ amalgamation undergoes an approval process. The parent property needs to be modified accordingly, which can be done in the system.

This module provides the following capabilities:

* Mutation of property and change of ownership details
* Capture Extension/ Addition and Alteration and reassessment based on changed property details
* Bifurcation of property&#x20;
* Amalgamation of property

### Module 5:  Generate Demand Notice

System has the capability to automatically generate demand notice for a financial year based on set triggers like time-based roll over on completion of a financial year. The system notifies the citizens about the demand through SMS/Email. The generated Bills can also be grouped and printed for physical distribution by the ULB employees. The system provides the capability to Employees to merge and download bills based on given parameters to plan their distribution drives.

This module provides the following capabilities:

* Generate Demand Notice based on periodic basis
* Group Demand Notices
* Print Demand Notices
* Cancel Demand Notices
* Send notifications to citizens on demand generation- SMS, Whatsapp, Email, Physical bill

### Module 6: Payments collection and Receipts

The citizen/ employee can view payment status of previous assessments from Assessment History section. Payment for any assessment with full or partially paid amount can be completed. Receipts for assessment can be downloaded in Assessment history section after searching for the property details.

This module provides the following capabilities:

* Payment of Property Tax -Online, Cheque, Cash, DD, during assessment
* Partial Payment of Property Tax -Online, Cheque, Cash, DD, during assessment
* The system allows a citizen to pay for anyone's property without changing the demand
* The system can also be integrated with PoS machines to enable doorstep collection of property tax and issue of receipt.

### Module 7:  Reports and Dashboards

PT reports provides facility to access receipt register, cancelled receipt register, account receipt register, ULB wise PT collection report, DCB Register. All reports can be downloaded in PDF/XLS format. State level administrator can monitor property tax collections, assessments and other information at a state level through dashboards.

This module provides the following capabilities:

* State Dashboard : View Reports for Total Collections, Properties Assessed, ULBs on Prod, Usage Type, Payment Distribution
* State Dashboard : PT Collection Timeline (Monthly,Weekly)
* State Dashboard : ULB Wise (Collection, Assessments)
* Cancelled Receipt Register Report
* PT Collection Report (ULB/Date Wise)

### Module 8:  General Features

#### Notifications

The system has the capability to send notifications to citizens. These notifications can be sent for various steps like - assessment completion, payment reminder, payment confirmation. These notifications can be sent in the language chosen by the ULB through all channels - SMS, Whatsapp, Email.

#### Legacy Data Migration

The system has the capability to migrate Demand and Collection. In most states, the preliminary step would be to migrate Legacy data of existing properties/connections along with the Demand and Collection details. This would ensure that subsequent demand generation happens through the system.

#### Configurable Masters

The system provides the following masters that can be configured as per the State’s requirements:

* Charges & Calculation : Calculation Engine, Rebate, Penalty,&#x20;
* Rate Master
* State Masters : Property Ontology, Documents List, Employee Data Mapping, Boundary Data Mapping

| Reform No. | Reform Area                                           | Weightage (score) | Recommendation                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         | Remarks                                                                                                                                                                  |
| ---------- | ----------------------------------------------------- | ----------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 7          | Land administration and Transfer of Land and Property | 3                 | <p>Digitize land transaction deeds of last 10 years at all sub-registrar offices and make the same available on an online system to check for ownership details and history. The metadata should be searchable for each record and a soft copy of the registered deed should be available. The searchable metadata available should be:</p><p>i. Name of buyer</p><p>ii. Name of seller</p><p>iii. Survey no.</p><p>iv. Registration number</p><p>v. Registration date</p>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             | The feature of ‘Property Registry’ in the product will enable this recommendation                                                                                        |
| 8          | Land administration and Transfer of Land and Property | 3                 | <p>Digitize and publish the updated Record of Rights (ROR) at all Revenue department offices online in public domain for all areas of the State/UT. The searchable metadata available should be:</p><p>i. Name of buyer</p><p>ii. Name of seller</p><p>iii. Date of mutation</p><p>iv. Survey no.</p>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  | The Property tax system enables this capability                                                                                                                          |
| 9          | Land administration and Transfer of Land and Property | 2                 | <p>Digitize and publish data of Property Tax payment dues online in public domain for all the Urban Local Bodies (ULBs) in the State/UT. The searchable metadata available should be:</p><p>i. Name of the Property Tax payer</p><p>ii. Property Tax dues</p><p>iii. Survey no. of land / Unique Identification no. of property</p>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    | This feature is enabled by the citizens itself                                                                                                                           |
| 10         | Land administration and Transfer of Land and Property | 2                 | Digitize cadastral maps of all rural areas in the State/UT and make them available in public domain                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    | This can be enabled and worked on by the state team                                                                                                                      |
| 11         | Land administration and Transfer of Land and Property | 5                 | <p>Integrate the below-mentioned records on one website:</p><p>i. Data of land transaction deeds for last 10 years at all sub-registrar offices (Name of buyer, Name of seller, Registration number, Registration date, Survey no.),</p><p>ii. Updated Record of Rights at all Revenue department offices (Date of mutation), and</p><p>iii. Data of Property Tax payment dues at all urban areas of the State/UT (Name of the Property Tax payer, Property Tax dues)</p><p>iv. Revenue Court case data (Court case number, Name of parties involved, Date of filing of court case, Status of case [Ongoing/Resolved])</p><p>v. Civil Court case data (Court case number, Name of parties involved, Date of filing of court case, Status of case [Ongoing/Resolved])</p><p>The website should be publicly accessible. It will help in establishing property ownership and identify tax encumbrances. The integration should be done for all areas of the State/UT.</p> | The integration with external portals and systems of other departments can be enabled by state teams who can enhance the offered product to cater to this recommendation |
| 12         | Land administration and Transfer of Land and Property | 2                 | <p>Implement an online application system having the following features</p><p>i. Mandatory Online application submission including submission of draft deed and other documents</p><p>ii. Provision of online payment of Stamp duty and Registration fee</p><p>iii. Auto generation of appointment date and time on making the payment of Stamp duty and Registration fee</p>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          | The system will provide these capabilities which can be customized as per the state specific rules and regulations                                                       |
| 13         | Land administration and Transfer of Land and Property | 1                 | Provide model deed templates for sale, gift, lease, mortgage and rent in downloadable and editable format along with instructions to use them                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          | This provision is made available through the ULB portal to make these features accessible to the citizens                                                                |
| 14         | Land administration and Transfer of Land and Property | 2                 | <p>Integrate the mutation process with the registration process and mandate initiation of mutation process (Revenue department and/ or ULB) as soon as the deed is registered. Ensure that:</p><p>i. Information to mutation authority to be automatically shared on completion of transaction (registration). This should be considered as initiation of mutation process.</p><p>ii. No separate application from transferee to be required.</p><p>iii. SMS/email should be sent to transferee/ transferor to inform about the initiation of mutation</p>                                                                                                                                                                                                                                                                                                                                                                                                             | The integration with external portals and systems of other departments can be enabled by state teams who can enhance the offered product to cater to this recommendation |

## Property Tax (PT) Implementation Methodology

This section provides an overview of the methodology for State-wide implementation of PT. The Implementation of PT is distributed across seven distinct stages. Each stage has a predefined entry & exit criteria and roles & responsibilities. This is to ensure objective monitoring and decision making for the overall success of the program. Details of each stage are defined in this section.

![](https://lh4.googleusercontent.com/ghE5J\_YGs1X1DSgwTdwh-j0meXtcHsvY2TEXy7875jmmRzZlZolKJi6\_airBN5zN2yAn067iIFi0yZTyxtC4xm-S4ytmWmZFwqJocm8TFKGryqMBorHnVrxokgImW-zff02qLR8)

Note: This document is specific for States that have more than 30 ULBs

PT implementation program is expected to be completed approximately between 38- 42 weeks depending on the variety in Processes, Integration and the Disparate legacy data systems involved. This is done with the resource deployment by the State and System Integrator (SI) Team. However, it is critical that activities and exit criteria set for each stage are achieved to adhere to this timeline.

### Seven Stages of Implementation

### Stage 0 - Program Setup/Onboarding

This is a set of initial critical activities undertaken on receiving a letter of Enrollment or MOU from the State. Successful completion of these activities assures that the program is started with crucial personnel, System Integrator(SI) Teams, and funds.

| **Stage 0 - Program Setup/ On-Boarding** |                                                                                                                                                                                                                                                                                                                                                                                          |
| ---------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Duration**                             | 4-6 weeks                                                                                                                                                                                                                                                                                                                                                                                |
| **Entry Criteria**                       | Acceptance Letter/MoU by State                                                                                                                                                                                                                                                                                                                                                           |
| **Exit Criteria**                        | <ul><li>Finalize Property Tax Program Vision</li><li>Finalize funding for the program</li><li>Define State- specific procurement process</li><li><p>Property Tax Cell appointment (*). Consisting of :</p><ul><li>Domain expert</li><li>Nodal officer (EO/ Commissioner/ Senior Official)</li><li>Program Head</li></ul></li><li>System Integrator(SI) Team sign-up/onboarding</li></ul> |

\*Details of PT cell is mentioned in section 4 of the handbook

### System Integrator(SI) Sign-up

* System Integrator and state will agree on program scope, program timelines, and budgeting & resourcing.

### Stage 1 - Program Kick-Off

This stage envisages in-person interaction of crucial State officials and implementation System Integrator(SI) Teams to kick-start the program. This stage may require multiple interactions/meetings with different interest groups. The principal objective of these interactions is to identify and agree on the scope and exclusions of Pilot ULBs, create an active collaboration & Governance approach and agree on a high-level timeline for the engagement.

| Stage 1 - Program kick-off |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| -------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Duration**               | 4-6 weeks                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| **Entry Criteria**         | <ul><li>Program setup (Stage 0) is complete</li><li>SI Team onboarded</li></ul>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| **Key Activities**         | <ul><li>Identify &#x26; agree on scope and exclusions</li><li>Identify pilot ULBs</li><li>Project Kickoff - Implementation Methodology Presentation</li><li>Product Walkthroughs</li><li>Define Project Steering Committee Structure and Project Governance process</li><li>Define phases of rollout/ deployment</li><li>Agreement on Deployment Priorities and high-level delivery timelines</li><li>Assessment of all current PT processes along</li></ul><p>(1) Citizen services/channels around it</p><p>(2) Integration with other Department process</p><ul><li>Finalise Program Success Metrics for Rollout, Adoption and Governance, adhering to the vision of the program</li><li>Internal Capacity Building, program logistics at State and ULBs, as per the current scenario</li><li>Collection of baseline data to measure endline target for the product (Revenue generated, total properties in ULBs etc.)</li></ul> |
| **Exit Criteria**          | <ul><li><p>Publish the program charter</p><ul><li>Implementation plan agreement with priority applications and broad timelines</li><li>Program Governance Model and processes</li><li>Program Success Metrics</li><li>Capacity Building</li></ul></li><li>PT Cell formation and appointment (*)</li><li>Data preparation/collection kickoff from Pilot ULBs</li><li>Cloud Infrastructure procured</li><li>Project Office Space allocated</li><li>Program Branding (name, logo, tagline etc.)</li></ul>                                                                                                                                                                                                                                                                                                                                                                                                                             |

\*Details of PT cell is mentioned in section 4 of the handbook

### Stage 2 - Solution Design

During the Solution design stage, key State officials and members, who are subject matter experts, are expected to share their inputs, discuss the process and help understand how to bring in compliance around the system design for the System Integrator(SI) Team. This stage baselines the State-specific product features in the Product Configuration report.

| **Stage 2 - Solution Design** |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| ----------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Duration**                  | 4-6 weeks                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| Entry Criteria                | <ul><li>Program Charter</li><li>PT Cell appointment</li></ul>                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| **Key Activities**            | <ul><li>Standardisation of all PT processes</li><li>Initiate policy change if needed, based on the Processes defined</li><li>Conduct Product familiarisation workshop</li><li>Initiate collection of master data from pilot ULBs</li><li>Finalise data migration/collection/sync-up approach</li><li>Finalise data validation approach</li><li>Capacity Building for making state team aware about basic usage of tools like MS Office, mails etc.</li><li>Dashboard design finalisation for Program Tracking</li></ul> |
| **Exit Criteria**             | <ul><li>Publish the PT processes, data template/workflows</li><li>Finalisation of Roll-out plan (in different phases)</li><li>Solution agreement for required State- specific customisations</li><li>Program tracking mechanism (Dashboard design finalisation)</li><li>Sign-off on approach to work with legacy or manual data (Data collection/migration/correction/ sync-up/validation)</li><li>Detailed project plan</li></ul>                                                                                      |

### Stage 3 - Configuration & Customization

This stage consists of a series of developments in accordance with the detailed project plan to ensure smooth functioning of the customised product. Master Data Collection & Environment Setup will be achieved in this phase. Further monitoring and maintenance strategies are put in place.

| **Stage 3 – Configuration & Customization** |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| ------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Duration**                                | 6-8 weeks                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| **Entry Criteria**                          | <ul><li>Product Configuration Report has been signed off by the state</li><li>Detailed Project Plan set up in accordance with master data collection and environment setup</li></ul>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| **Key Activities**                          | <ul><li>Setting up development environments</li><li>Development/customisation of reports and dashboards</li><li>Development/ integration of portal</li><li>Third-Party integrations (payment gateway, handheld/pos device)</li><li>Updation of user manuals and other key documents</li><li>Preparation &#x26; execution of Test Cases</li><li>Setup monitoring, support &#x26; maintenance processes, tools and dashboards</li><li>PT legacy data collection from Pilot ULBs(at least). No historical transaction will be considered. Only outstanding and property details shall be migrated</li><li><p>Capacity Building for making state team aware about basic usage of tools like MS Office, mails etc.</p><ul><li>Identify ULB level Nodal officers for day to day support</li></ul></li><li>Migration and verification of Pilot ULB data</li></ul> |
| **Exit Criteria**                           | <ul><li>Configured/Customized product that is ready for UAT</li><li><p>Monitoring, support &#x26; maintenance of Dashboards</p><ul><li>Finalization of Initial Reporting and Dashboard KPIs</li></ul></li><li>Identification of participants for UAT session</li><li>Training for System Content related Capacity Building finalised</li></ul>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |

### Stage 4 - UAT & Go Live

During this stage, demonstration of the product followed by a hands on session is conducted for the ULB officials. Necessary training of ULB officials and resources required for UAT is conducted and identified respectively. The establishment of the State support Team and required processes are initiated in this stage.

| **Stage 4 – UAT & Go Live** |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| --------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Duration**                | 2-3 weeks                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| **Entry Criteria**          | <ul><li>Configured/Customized product ready for UAT</li><li>Pilot ULB Officials associated with TL are available for UAT &#x26; Training</li></ul>                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| **Key Activities**          | <ul><li>UAT Environment Setup</li><li>Regression UAT and sign off from Pilot ULBs/ State</li><li>Issues/bug resolution</li><li>Setting up the Production environment</li><li>Setting up Support Center &#x26; processes (Help Desk)</li><li><p>Training (Users, trainer)</p><ul><li>master trainers identified from ground for simultaneous training</li></ul></li><li>Training the support resources</li><li>Marketing &#x26; promotion activities</li><li>Go Live &#x26; launch event</li><li><p>Setup of review and monitoring cadence/team</p><ul><li>Usage/review/Dashboard/Field Visits</li></ul></li></ul> |
| **Exit Criteria**           | <ul><li>UAT Sign-off &#x26; Go Live for Pilot ULBs</li><li>Setup of review and monitoring cadence</li></ul>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |

### Stage 5 – Rollout

On successful Go-Live in the Pilot ULBs, and further fine tuning to stabilize the product, the solution will be rolled out to the rest of the ULBs in phases. Guidance and support from the State Team will be required to create the rollout plans and assure the necessary infrastructure for training and deployment is available at each ULB.

Note: The rollout phase needs to be detailed out for iterative activities of onboarding ULBs in batches.

| **Stage 5 – Rollout** |                                                                                                                                                                                                                                                                                                                                                                                   |
| --------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Duration**          | 5-6 weeks                                                                                                                                                                                                                                                                                                                                                                         |
| **Entry Criteria**    | <ul><li><p>Pilot has been successful in the State</p><ul><li>there are less than 3 open critical incidents (issues) with respect to product, implementation and data</li></ul></li></ul>                                                                                                                                                                                          |
| **Key Activities**    | <ul><li>ULB configurations phase wise as per the Project Plan</li><li>Migration and verification of ULB data</li><li>Logistics planning for training</li><li>Establishment of bug ticketing tool for resolving ground level issues by the state team</li><li>Training the Users at the district level</li><li>Pan State Roll Out - Phase wise</li><li>Stabilise product</li></ul> |
| **Exit Criteria**     | <p>State-wide Rollout in batches:</p><ul><li>Adoption tracking &#x26; Review Cadence operational</li><li>Help Desk Effectiveness assured</li><li>Critical Bugs fixed</li><li>Program Success Metrics Tracking Kick-started</li></ul>                                                                                                                                              |

Note: Only once all the stages are complete in one batch of rollout of around 30 ULBs, the next batch begins. There are multiple phases of rollout. The second batch begins after the first batch has successfully fulfilled all the criteria of the Rollout Phase. Typical timeline for closure of rollout in each batch is 5-6 weeks (in a batch of 30 ULBs)

### Stage 6 – Sustenance and Ongoing Improvement

The final stage consists of strategies to ensure the sustenance of the program in the State. Systems are put in place to ensure the continuous tracking of data and provisions are made to improve the product if new data suggests.

| **Stage 6- Sustenance and Ongoing Improvement** |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| ----------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Duration**                                    | Ongoing process                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| **Entry Criteria**                              | <ul><li>Rollout Phase 1 (First set of 30 ULBs where rollout will happen after all ULBs are live)</li></ul>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| **Key Ongoing Activities**                      | <ul><li>Adoption Review Meetings as per the vision defined for the program</li><li><p>Plans for Execution of Core Team to ensure Sustenance of the initiative in the areas of:</p><ul><li>Funding</li><li>IT support (infra, helpdesk, ongoing enhancements)</li><li>Process Effectiveness and Improvements</li></ul></li><li><p>PT Cell Focuses on Using data for:</p><ul><li>tracking field issues and performance data to identify improvements</li><li>identify additional Integrations around PT to make processes more robust towards enhancing PT revenues (e.g Upstream and downstream Processes)</li></ul></li></ul> |

## Roles and Responsibilities

### PT Cell, eGov Team & System Integrator(SI)Team

This section outlines the activities involved in each stage of the implementation along with responsibility and accountability of critical stakeholders - State, eGov Team and System Integrator Team onboard.

**PT Cell:** PT Cell is the government-appointed body chaired by the Principal Secretary/Secretary, Urban Development Department with members from Urban Development Department etc.

Resource requirements for the PT cell required to be formed by the State

| Resource Name          | No. Of Resources                                          |
| ---------------------- | --------------------------------------------------------- |
| Project Head           | 1                                                         |
| Domain Expert          | 1 Representation from Corporations/Council/Panchayat etc. |
| District Nodal Officer | 1 per district                                            |
| MIS Expert             | 1 per district                                            |

Note:

* Designations mentioned above are in accordance with those already driving PT implementation at the State level.&#x20;
* The description of each designation is explained below.&#x20;
* Project Head: Is the Head of the PT Cell who will drive the project from the State’s Side
* Domain Expert: Person who is well aware of the on ground scenario, well versed with the act, GOs passed, Prevalent Business processes, Deviations from the acts, PT Rates/ slabs applicable. In addition, provisions may be made to include External Domain Consultants/Advisors.&#x20;
* Nodal officer (EO/Commissioner/ Senior Official): the product coordinator to drive the project centrally. Monitor usage post Go Live- point of escalation for Implementation Team, Seasoned and worked in Multiple ULBs on various modules and has a good understanding of PT, Facilitate and Track data collection Post Go Live, Monitors and facilitates adoption of application. Point of contact for Management team, SI and at the HQ level.
* MIS Expert: Data Preparation for ULBs,Day to day tracking of the data specific to ULBs, data collection/validation for correctness and comprehesiness, reporting and review to senior officials

**eGOv Team:** eGov Team is the technical partner of the project which will provide all necessary support to the State/UT concerning the implementation, Program Designing etc.

**System Integrator (SI)Team:** SI Team will be responsible for consulting, program management and the implementation of the state specific customized and configured products in the ULBs in close collaboration with the PT cell, technical partner (eGov) and various other stakeholders.

#### Guidelines to read the tables below:

**Execute** - One who owns the accountability to complete the activity

**Consult** - One who may initiate, guide and in the process, handhold the execution of the activity

| Stage 0 - Program Setup/ On-Boarding          |         |                  |
| --------------------------------------------- | ------- | ---------------- |
| Task/Activity                                 | eGov    | State Leadership |
| Appoint PT Cell                               | Consult | Execute          |
| Finalise funding for the program              | Consult | Execute          |
| Define state -specific procurement process    | Consult | Execute          |
| System Integrator(SI) Team sign-up/onboarding | Consult | Execute          |
| Finalise Property Tax Program Vision          | Consult | Execute          |

Note: Stage 0 is where the PT cell and SI team is formed, hence there are only two entities playing a role which is that of eGov and the state leadership. Once the PT cell and SI team is finalised, their role begins in the following stages.

| Stage 1 - Program kick-off                                                                                                                  |         |         |         |
| ------------------------------------------------------------------------------------------------------------------------------------------- | ------- | ------- | ------- |
| Task/Activity                                                                                                                               | eGov    | PT Cell | SI Team |
| Identify & agree on scope and exclusions                                                                                                    | Consult | Consult | Execute |
| Identify pilot ULBs                                                                                                                         |         | Execute | Consult |
| Project Kickoff - Implementation Methodology Presentation                                                                                   | Consult | Consult | Execute |
| Product Walkthroughs                                                                                                                        | Consult |         | Execute |
| Define Project Steering Committee structure and Project Governance process                                                                  | Consult | Consult | Execute |
| Define phases of deployment/ rollout                                                                                                        |         | Consult | Execute |
| Agreement on Deployment Priorities and high-level delivery timelines                                                                        |         | Consult | Execute |
| <p>Assessment of all PT process along</p><p>(1) citizen services/channels around it</p><p>(2) Integration with other department process</p> |         | Consult | Execute |
| Finalize Program Success Metrics for Adoption and Governance adhering to the vision of the program                                          | Consult | Consult | Execute |
| Internal Capacity Building, program logistics at State and ULBs, as per the current scenario                                                |         | Execute | Consult |
| Collection of baseline data to measure endline target for the product (Revenue generated, total properties in ULBs etc.)                    | Consult | Execute | Consult |

| Stage 2 - Solution Design                                                                           |         |         |         |
| --------------------------------------------------------------------------------------------------- | ------- | ------- | ------- |
| Task/Activity                                                                                       | eGov    | PT Cell | SI Team |
| Standardisation of all PT processes, if needed                                                      |         | Consult | Execute |
| Initiate policy change, if needed based on identified improvements                                  | Consult | Execute | Consult |
| Conduct Product familiarisation workshop                                                            |         | Consult | Execute |
| Initiate collection of master data from pilot ULBs                                                  |         | Consult | Execute |
| Finalise data migration/collection/sync-up approach                                                 |         | Consult | Execute |
| Finalise data validation approach                                                                   |         | Execute | Consult |
| Capacity Building for making state team aware about basic usage of tools like MS Office, mails etc. |         | Execute | Consult |

| Stage 3 – Configuration & Customization                                                             |      |         |         |
| --------------------------------------------------------------------------------------------------- | ---- | ------- | ------- |
| Task/Activity                                                                                       | eGov | PT Cell | SI Team |
| Setting up development environments                                                                 |      | Consult | Execute |
| Development/customisation of reports and dashboards                                                 |      | Consult | Execute |
| Development/Integration of portal                                                                   |      | Consult | Execute |
| Third-Party Integrations (Payment gateway, Handheld/pos device)                                     |      | Consult | Execute |
| Updation of user manuals and other key documents                                                    |      | Consult | Execute |
| Preparation & execution of Test Cases                                                               |      | Consult | Execute |
| Setup monitoring, support & maintenance processes, tools and dashboards                             |      | Consult | Execute |
| PT legacy data collection from Pilot ULBs(at least)                                                 |      | Consult | Execute |
| Capacity Building for making state team aware about basic usage of tools like MS Office, mails etc. |      | Execute | Consult |
| Migration and verification of Pilot ULB data                                                        |      | Consult | Execute |

| Stage 4 – UAT & Go Live                            |         |         |         |
| -------------------------------------------------- | ------- | ------- | ------- |
| Task/Activity                                      | eGov    | PT Cell | SI Team |
| UAT Environment Setup                              | Consult | Consult | Execute |
| Identification of participants for UAT session     |         | Consult | Execute |
| Issues/bug resolution                              |         | Consult | Execute |
| Regression UAT and sign off from Pilot ULBs/ State |         | Execute | Consult |
| Setting up the Production environment              |         | Consult | Execute |
| Setting up Support Center & processes (Help Desk)  |         | Execute | Consult |
| Training user                                      |         | Execute | Consult |
| Training Trainer                                   |         | Consult | Execute |
| Training the Support Resources                     |         | Consult | Execute |
| Marketing & promotion activities                   |         | Execute | Consult |
| Go Live & launch event                             | Consult | Execute | Execute |
| Setup of review and monitoring cadence/team        |         | Execute | Consult |

| Stage 5: Rollout                                                                        |         |         |         |
| --------------------------------------------------------------------------------------- | ------- | ------- | ------- |
| Task/Activity                                                                           | eGov    | PT Cell | SI Team |
| ULB configurations phase wise as per the Project Plan                                   |         | Consult | Execute |
| Migration and verification of ULB data                                                  |         | Execute | Consult |
| Logistics planning for training                                                         |         | Execute | Consult |
| Establishment of bug ticketing tool for resolving ground level issues by the state team |         | Consult | Execute |
| Training the Users at the district level                                                |         | Execute | Consult |
| Pan State Roll Out - All Locations                                                      | Consult | Execute | Execute |
| Stabilise product                                                                       |         | Consult | Execute |

| Stage 6- Sustenance and Ongoing Improvement                                                                                                                                                                                                                                           |         |         |         |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------- | ------- | ------- |
| Task/Activity                                                                                                                                                                                                                                                                         | eGov    | PT Cell | SI Team |
| Adoption Review Meetings as per the vision defined for the program                                                                                                                                                                                                                    | Consult | Execute | Consult |
| <p>PT Cell Focuses on Using data for:</p><ul><li>tracking field issues and performance data to identify improvements</li><li>identify additional Integrations around PT to make processes more robust towards enhancing PT revenues (e.g Upstream and downstream Processes)</li></ul> |         | Execute | Consult |
| <p>Plans of ongoing Sustenance in Place with respect to :</p><ul><li>Funding</li><li>IT support (infra, helpdesk, ongoing enhancements)</li><li>Process Effectiveness and Improvements</li></ul>                                                                                      | Consult | Execute | Consult |

## Overall Program Assumptions

| Areas          | Assumptions                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| -------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Infrastructure | <ul><li>The actual Infra will be provided based on the questionnaire inputs received from the state</li><li>The state will take care of providing necessary project infrastructure and office facilities during the program for all on-site project Team members, which will be confirmed during the initiation phase. This includes workspace, office equipment (e.g., telephone with STD, fax machine, photocopy machine, etc.), stationery, PC/workstation, project LAN and internet access, etc.</li><li>The state will provide the necessary administrative support staff to carry out day-to-day project administration tasks, e.g., meeting rooms, Videoconferencing, etc.</li><li>The state should provide a Project Office and at least one conference room with speakerphone throughout the Project Duration.</li></ul> |
| Project Scope  | <ul><li>Any new requirements received from State during the implementation phase will be handled through a change management process</li></ul>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| State Team     | <ul><li>The state will nominate a reasonably sized multifunctional Team from various departments of the State to be responsible for the implementation. The state Team would be required for information, validation, and execution through the implementation cycle and the Team members should be reasonably empowered to take decisions. Any delay in the decision-making process and the non-availability of the State Team may have an impact on the schedule.</li><li>The participants from State are expected to have a thorough understanding of the State’s internal processes.</li><li>The state will engage internal and external stakeholders required for this engagement and ensure their availability whenever needed.</li></ul>                                                                                   |
| Documentation  | <ul><li><p>The Tech Implementation Partner will ensure provision of the following:</p><ul><li>User education and training documentation delivery as per the default product documentation of the identified product versions.</li><li>Product manuals are expected to be shared with the State as part of the user manual.</li><li>All documentation in English and the language requirement of the state.</li></ul></li></ul>                                                                                                                                                                                                                                                                                                                                                                                                    |
| Training       | <ul><li>Training to the end-users will be driven by the state Team.</li><li>The state will be responsible for providing the necessary infrastructure required for the Training, which includes the following readiness.</li><li>Training Rooms (Parallel Training Sessions) with Projector, White Board, Markers, Internet Connection, sufficient seating capacity, Desktop/Laptop for each participant and availability of Network for Trainees to connect to the server.</li></ul>                                                                                                                                                                                                                                                                                                                                              |
| Implementation | <ul><li>The scope of the implementation will be limited to the services mentioned in Section 2.</li><li>State Team will have an identified SPOC for handling the first level of eGov communication with the client unless discussed and agreed.</li><li>eGov Team will not be involved in defining the test cases or executing the test cases.</li><li>Necessary signoff would be provided by the state upon completion of the defined milestones.</li></ul>                                                                                                                                                                                                                                                                                                                                                                      |

## Glossary

| **PROGRAM** |
| ----------- |

Vision:

Defining the time frame to go live, the time frame to scale it pan state, the value proposition of the programme for the state and year-on-year financial targets and adoption targets

Project Plan:

A detailed plan of Program schedule/timelines, implementation phases, team structure and ongoing support and maintenance required.

System Integrator:

The Entity/Company which collates all the subsystem required for the project and integrates them to achieve the program objective

Program Charter:

Outline of implementation plan agreement with priority applications and broad timelines, program governance model, program success metrics and capacity building.

Acceptance Letter/MOU:

Formal Acceptance/Sign Off of the Client State with a clear mandate of the Program

Program Success Metrics:

Defining the parameters (which are measurable) prior to the program, on which the success of the program is to be measured on the completion of the program

Project steering committee:

The key body within the governance structure which is responsible for the business issues associated with the project that are essential in ensuring the delivery of the project outputs and the attainment of project outcomes.

Project governance:

Set of policies, regulations, functions, processes, procedures and responsibilities that define the establishment, management and control of projects, programmes and portfolios.

| IMPLEMENTATION |
| -------------- |

Scoping:

List of activities measured against time taken to complete them in accordance with the project goals

Baseline data:

Set of information that serves as a foundation to compare other data acquired afterwards

Project Kick off meeting:

Meeting with the project team and the client of the project. This meeting would follow definition of the base elements for the project and other project planning activities

Fitment Study:

GAP Study of the Existing/Required Field Process Vs Product

Data migration:

Existing Records of the functional activities need to be moved into the Database of the newly released Application

Data collection:

Required data for the roll-out of the applications, which needs to be collected from the existing functional process

Data validation approach:

This approach enables the sanctity of the Data with built-in validation by Design

Data synchronization:

The process of establishing consistency among data from a source to a target data storage and vice versa and the continuous harmonization of the data over time.

Pilot Implementation:

Any new process is tested out as pilot in one or two instances before pan implementation

Pilot ULB:

The ULB's Selected for the pilot implementation are called pilot ULB’s.

Roll out:

On successful clearance of the Pilot, the Process/Application/Services are implemented across all Offices/ULB's

Deployment:

Deployment defines the complete package of Software components set up in a particular environment

| PRODUCT |
| ------- |

Customisation:

Details of changes to be made in the Product to comply with the needed field process

Configuration:

Defining existing content such as Options and Variables based on the requirements on the ground

Product walkthrough:

Explaining the users step-by-step through a set of actions that they need to take to achieve a specific outcome

> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_ ](https://egov.org.in/)_is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
