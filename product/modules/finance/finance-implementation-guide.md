# Finance Implementation Guide

## Executive Summary

### Overview of the Product

The eGov Financial Management System is an integrated fund-based double-entry accounting system that manages the financial accounting and reporting, budgeting and Asset Management for a ULB (Urban Local Body). The system is based on simple, easy to use screens and is fully web-enabled which will make it possible to deploy the system in multiple ULBs from a central data center. Transition to a fully online accounting system will ensure that the data is captured in the system at the point of creation and is immediately available for real time reporting and effective decision making. Perhaps most importantly, the system is fully integrated into the ULB’s various Revenue and Expenditure sources which will enable the administration to generate easy-to-understand reports summarizing the ULB’s key financial indicators on real time.

### Implementation Methodology for Finance and Accounting System

For the offered product, the implementation process can be divided into seven major distinctive stages. Each stage has a predefined entry and exit criteria, roles & responsibilities to assure objective monitoring and decision making for the overall success of the engagement. The whole implementation lifecycle is typical of 28-30 weeks keeping in mind the entry, and exit criteria defined at the beginning and end of each stage are met on time recommended.

![](https://lh5.googleusercontent.com/noAONyvwA6200w0nJHURXAbld1-lrAUFqgETKsklCvFaeLkpduWwWIJO\_FQwrm6RHAtsgCPLGHGp9m8J2InVfBFpBROp2Wjg\_3MTGAVzTCAomPQorRt4Qs3ZInEVCQAv1kxVM3cv)

Exhibit 1: Various stages of implementation

Stage Zero-program setup and onboarding is a pre-requisite for the initiative to kick-off and requires setup of the governance model, implementation Team and decision regarding other significant elements of the initiative like funding and procurement process. Stage one of this initiative requires scoping of the initiative and decide on the priorities for implementation by the state/UT implementation Team. Stage two consists of requirement analysis and configuring & customising the product as per the needs of the state/UT. In stage three, the state/UT Team will work upon identifying and finding solutions to the significant gaps in the product offered w.r.t. to the need of the state/UT. Pilot and UAT (User Acceptance Testing) of the product is the primary objective of stage four. This involves working on various aspects of state/UT-specific needs and incorporating them into the product suite offered. In stage five, post doing UAT and including all the necessary feedback on the product, end user training for the Phase 1 ULBs is provided which included data loading. Stage 5 involves Go live where the product is rolled out in phases. Stage 6 involves monitoring and sustenance where plans for ongoing activities post roll out are made.

### Critical Success Factors for Implementation

Implementation of Accrual based Finance accounting system requires meticulous planning and close coordination between various stakeholders at the centre and state/UT level. The success of the initiative is dependent upon many factors like strong Program governance, availability of the trained resource, financial planning, targeted implementation Team onboarding, focus on last-mile capacity building and ensuring necessary support to urban centre. Achievement of all these factors will provide the most effective and efficient roll-out and adoption of the Finance Accounting System in the state/UT.

## Finance & Accounting System Product-Overview

The objective of this section is to give an overview of the features and functionalities available in the Finance and Accounting product.

As part of the implementation, easy rules can be incorporated to configure the work flows and transaction based validations which are specific to ULB processes. This is expected to greatly reduce data entry errors and improve productivity. The system provides for all the necessary management controls like voucher approval before G/L posting, security with role-based access control and approval workflows. A fully integrated Budgeting module has the potential to improve the budgeting process by supporting the creation and approval of detail budgets by department and function with a ward and then aggregating these budgets into the overall ULB budget. Once approved, budgetary controls can be enforced on all transactions. The Asset Management module allows for the creation and tracking of assets throughout their lifecycle, automatic depreciation calculation, asset revaluation and disposal.

eGov Financials is fully integrated to eGov Works, Assets, eGov Purchasing/Inventory, Pension, Payroll, Property Tax, Trade License, Land and estates, Professional Tax, Company Tax and other eGov Modules and can also be integrated with other existing ULB eGovernance applications. This would enable the automatic capture of the financial accounting impact of all transactions in these systems. Further, eGov Financials can also be integrated to eGov GIS to provide GIS based reports.

#### Generic Features :

• Fully National Municipal Accounts Manual (NMAM) Compliant

• User Friendly, Simple and easy to use screens

• Fully internet enabled

• Supports fund-based double-entry accounting

• Multi-level approval workflows

• Exhaustive management controls like voucher approval before G/L posting controlled

environment for entries to avoid accounting errors.

• Extensive data management

• Supports accounting of all types of accounting transactions – automatic remittance, Receipts

• Robust in-built budgeting system with controls

• Exhaustive reporting infrastructure

• Key Security features of ERP system

• Systematic Bank reconciliation and integrated Remittance processing.

• User defined Unique Transaction code for every entry – Financial Transaction code can be customized by Fund, Year/Month, Voucher type, etc.,

#### Benefits :

• Visibility into key financial indicators of the Municipality.

• Prepare and publish balance sheets and income & expenditure accounts on time.

• Accounting of transactions as per preconfigured rules and guidelines of the National Municipal

Accounting Manual

• Traceability and accountability for utilization of funds

• Automated budgetary controls help Financial management of ULB operations

• Integration with expenditure management modules provides visibility into utilization of funds

and ensures better planning of funds

### Masters

All master data defined at the state level will be uploaded as part of the system set up. Any add-ons or changes at ULB level will be controlled using the create and modify feature of the respective master.

1.1 Chart of Accounts

Chart of Account master data will be finalized at state level and the same will be loaded as part of the system set up. Master screen will be provided to add detailed level code. Also modify option allows the users to update the properties of the account code like - adding subledger mapping, enable/disable budget check option, update the purpose and so on.

1.2 Bank

Standard banks that are published by RBI to be loaded as part of system set up and any new banks to be added using the bank master option.

1.3 Bank account

Bank accounts needs will be created for a bank and branch using the bank account master. Multiple accounts can be created for a bank and branch where each account used for various purposes like -receipts and payments.

1.4 Fund

```
   Fund master data can be added and updated using this master. Fund will be of multiple levels.
```

1.5 Function

```
   Any new functions that are to be added apart from the standard ones listed in NMAM will be done from this master screen. Function is of 3 levels as per NMAM and any modifications can be managed using this master.
```

1.6 Scheme and sub scheme

Any schemes and sub schemes defined by the state or centre government will be associated with a fund and will be for a time period. Sub scheme are defined under a scheme.

1.7 Financial Year and Fiscal period

Any financial year can be added in the system using this master. A year can be defined into multiple fiscal periods based on the date range. If a year is open for posting vouchers or not will be configured using this master.

1.8 Cheque

All bank accounts from which payments are made needs to have cheque master data defined against it. Each cheque book will have a range of cheque leaves and system will have the facility to denote which all cheque leaves are used, and which are available for use.

1.9 Vendor (Contractor/Supplier)

Vendor master consists of both supplier and contractor. System will capture all the relevant information of the supplier and contractor like Permanent Account Number (PAN), Tax deduction and Collection Account Number (TAN), Bank account details and so on. Vendor status will be maintained to know if they are active or blocked at any point of time. Blocking/Blacklisting of vendors will be taken care.

1.10 Recovery Codes

All deductions that are mandated by the centre/state/ULB will be defined here with details of the deduction percentage and account code. Some deductions can be flat rate as well.

1.11 Accounting entities and User defined masters

System will be configured with standard accounting entities like- Employee, Contractor and Supplier for which the master data will come from the employee, contractor and supplier master respectively. At any point a new subledger can be added in the system using the accounting entities master. Master data pertaining to these entities can be added from the User defined masters.

1.12 Ledger Opening Balance

Opening balances for any GL codes (Assets and Liabilities) for any financial year can be added into the system using this screen. GL code balances will be taken sub ledger wise in case the code is marked as a control code. Any change made to the opening balance will be reflected in the corresponding year Trial balance immediately.

1.13 Service to Bank Account mapping

Any collections made in the system will be associated with a specific source. This can be property tax, Advertisement tax and so on. Any revenue earned under these sources needs to be accounted under the specific bank account. This master will be used to capture the mapping of services to bank accounts.

### Expenditure Accounting

Financials module can be used as a standalone system when Inventory and Works modules are not in place, wherein all supplier and contractor bills will be raised in the Financials system against a purchase order or work order. Payments can be made to a party for all approved bills raised in the system. Payments may be done even without bill in certain cases.

2.1 Creation and approval of expense bill

Any contingent expenses, administrative expenses and indirect expenses against a work will be accounted using the expense bill option. System should be able to accommodate bills for any kind of sub ledgers here. System should allow to select any debit and credit and net payable code here. Bills can be sent through an approval cycle based on the system set up, it may as well be created in approved state. Here the net payable can be any party - contractor, supplier, employee or any random person.

2.2 Create voucher from bill

Any bills created from the Financials system as well as from the third-party systems should be available for voucher creation. For these bills the voucher will be created based on the GL codes available in the bill. Budgetary controls will be applied based on the system configuration. A voucher will be generated against a bill once it passed all levels of validation. Voucher can go through an approval cycle based on the system set up or it will be approved on create.

2.3 Payment of Bills

All bills for which vouchers are generated should be available for payment to the concerned party. System should be configured to take the mode of payment (Cash, Cheque, RTGS) according to the bill type. Partial or complete payment of the bills to be allowed and multiple bills should be allowed to be paid using a single payment. Payment voucher may be taken to approval cycle and bank balance checking based on the system configuration. We should promote the user to move away from the Cash and Cheque mode of payments and move to RTGS payments.

2.4 Direct bank payment

Any expenses for which bills are not present should be paid using the direct bank payment option. Budgetary controls will be applied based on the GL accounts debited and credited.

2.5 Cancel Bill

Any bills for which vouchers are not created should be allowed for cancellation. Cancelled bills should not be available for voucher create.

2.6 Cheque Assignment

All payments that are made with mode of payment “cheque” and “consolidated Cheque” will need to be processed for cheque assignment. System will have the facility to automatically or manually assign a cheque party wise for the selected payments.

2.7 RTGS Assignment

All payments that are made with mode of payment “RTGS” will need to be processed for RTGS assignment. System will have the facility to automatically or manually assign a single RTGS number for all the parties linked to the selected payments.

2.8 Surrender and reassign cheques

In cases where cheques are spoiled or wrongly written, one has to surrender this cheque and reassign a new one. System will allow the user to surrender cheques and give option to reassign a new cheque if needed.

2.9 Surrender and reassign RTGS

If the RTGS assignment done was wrong, the system provides the facility to surrender this RTGS. At this point all the payments associated with the surrendered RTGS will be listed again for RTGS assignment and system can assign a new RTGS number to these payments.

### Revenue Accounting

All receipts created in the system should be accounted using the receipt vouchers. System should create one receipt voucher for each of the receipt and any modification or cancellation of receipt made will be accommodated by passing a reversal or cancellation voucher. All receipts collected for the day should be remitted to the bank on the same day.

3.1 Creation and approval of receipt voucher

Receipt voucher will be generated for the receipts created in the system online or offline mode. Receipt vouchers will use the debit and credit GL codes based on the revenue heads for which the receipts are made. These vouchers may be approved on create or can be sent for approval.

3.2 Creation of day end remittance vouchers

All the collection done on a day should be submitted to the bank based on the mode of collection- cash, cheque, DD, online by the end of the same day. On remittance a pay in slip contra voucher will be generated after which this amount will be reflected in the Bank book.

3.3 Miscellaneous receipts

Any revenues coming from revenue systems will be accounted using the appropriate module like property tax and water charges systems. There are one of cases where revenues are coming from other sources like deposits from vendors or grants received from funding agencies and so on. These receipts will be created in the system using the miscellaneous receipt option. Deductions are applicable in case service taxes. Receipt voucher may be created automatically on approval of receipt based on system configuration.

### Journal Voucher

Journal vouchers are used to make ledger entries for various categories of transactions using voucher sub types. Voucher subtypes are mainly classified as - Purchase, Works, Salary, Pension and General. Each of these subtypes should be turned on and off based on the availability of the source module in the ERP. Vouchers will be sent for approval based on the system configuration.

4.1 Book adjustment entries

Any book adjustments like assetization and depreciation entries will be of type General Journal voucher. System should be enabled to accommodate GL codes of any type of sub ledgers here.

4.2 Creation and approval of Vouchers of type -Works,Purchase

System will generate different voucher number formats for each of the voucher subtypes. Various types of vouchers like works, fixed assets and purchase can be configured.

### General Transaction

5.1 Cancel Voucher

Any voucher (bill voucher, payment voucher, receipt voucher) created in the system should be allowed for cancellation either by the creator of the voucher or by the administrator. Once the vouchers are cancelled all accounting impact will be nullified and these records will not show in the general ledger accounts and Trial balance. System should take care of dependencies like, bill voucher cannot be cancelled if payment is already done for this and so on.

5.2 View Voucher

Provide a facility to view any type of vouchers created in the system for the selected filter parameters like - date range, fund, department and so on.

### Reports

6.1 Accounting Reports

6.1.1 General Ledger

For the selected GL code and other parameters system should list all the vouchers with opening and closing balances.

6.1.2 Trial Balance

Trial balance shows GL code wise debit and credit balances along with the opening balance and closing balances for the selected date range and other parameters with drill down facility to General ledger report.

6.1.3 Bank book

For the selected Bank account system will list all the receipts, payment and adjustment entries along with opening and closing balance.

6.1.4 Day book

For the selected day all the transactions happened will be listed account head wise in this report.

6.1.5 Journal book

All the Journal vouchers of various types that are posted for the selected period will be listed in this report.

6.1.6 Opening balance

This report will show the GL code that has got opening balance for the selected financial year and other parameters. Opening balances will be uploaded into the system before the go live.

6.2 Collection Reports

6.2.1 Receipt Register

All the receipts made for the selected date and other parameters will be listed here with details of the mode of collection and service.

6.3 MIS Reports

6.3.1 Bills and Payments

This report will show the list of bills along with the payments made against it and the cheque number or RTGS number associated with it. Any bills that are unpaid will have payment details empty and paid amount as zero.

6.3.2 Cheque Issue Register

This report will show the list of cheques that are issued out to vendors, employees and others from the selected bank account. Cheque details like the cheque number, pay to, amount and so on will be listed here along with the payment voucher details.

6.3.3 RTGS Advice

Every RTGS needs to be supported by an RTGS Advice that will be handed over to the bank for transferring the amount to respective accounts. This advice will have details like party name, PAN number, bank account number and amount information.

### Configuration data

Configuration data consist of master data and system set up data that are required for the basic functioning of the application.

7.1 Master data upload

Masters like -Fund, Function, GL Codes, Bank, scheme, sub- scheme, Bank account, Financial year and fiscal periods will be loaded into the system based on the data provided by the client. Master screens will be provided only for GL Codes, Function, Bank and Bank account.

## Finance and Accounting System Implementation Methodology for the State/UT

This section provides an overview of the methodology for state/UT-wide implementation Finance and Accounting System. Implementation of this system is distributed across seven distinct stages. Each stage has a predefined entry and exit criteria, roles & responsibilities to assure objective monitoring and decision making for the overall success of the engagement. Details of each stage are defined in this section.

![](https://lh3.googleusercontent.com/Me0LK-PoV6raaNQDgXes9L73\_qglMY2rpa9H5McSA1fduZYRo3UmDbe\_eqre\_cEHT12x0M54AqDuCSZ\_2UBLMP1jNh8KllMPIaD9\_mCJRmiVqYfRHvq6ttz7wIowxYdAIfzX3Kpv)

Exhibit 2: Various stages of implementation

Finance and Accounting System implementation program is expected to be completed within approximately 24-30 weeks with the resource deployment by the State/UT and System Integrator (SI) Team (as defined below). However, it is critical that activities and exit criteria set for each stage are achieved to adhere to this timeline.

### Seven Stages of Implementation

| Stage 0 - Program Setup/Onboarding |                                                                                                                                                                                                                                                                        |
| ---------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Duration                           | 3-4 weeks                                                                                                                                                                                                                                                              |
| Entry Criteria                     | <ul><li>Acceptance Letter/MoU signed by the State</li></ul>                                                                                                                                                                                                            |
| Exit Criteria                      | <ul><li>Finance &#x26; Accounting Function Cell Appointment</li><li>Finalise funding for the program</li><li>Define State/Union Territory -specific procurement process</li><li>Finalise Finance &#x26; Accounting Program vision</li><li>SI team onboarding</li></ul> |

Set of initial critical activities that are undertaken on receiving a letter of Enrollment from the state/UT. Successful completion of these activities assures that the program is started with crucial personnel, System Integrator (SI) Teams and funds.

This stage envisages the in-person interaction of crucial State/UT officials and implementation System Integrator (SI) Teams to kick-start the program. This stage may require multiple interactions/meetings with different interest groups. The principal objective of these interactions is to identify Pilot ULBs, create an active collaboration & Governance approach and agree on a high-level timeline for the engagement.

| Stage 1- Initiation |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| ------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Duration            | 3-4 weeks                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| Entry Criteria      | <ul><li>Program set up (Stage0) is completed</li><li>SI Team signed up</li></ul>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| Key Activities      | <ul><li>Identify &#x26; agree on scope and exclusions</li><li>Identify pilot ULBs</li><li>Project Kickoff - Implementation Methodology Presentation</li><li>Define Project Steering Committee Structure and Project Governance process</li><li>Define phases of rollout/ deployment</li><li>Agreement on Deployment Priorities and high-level delivery timelines</li><li>Finalise Program Success Metrics for Rollout, Adoption and Governance, adhering to the vision of the program</li><li>Internal Capacity Building, program logistics at State and ULBs, as per the current scenario</li><li>Collection of baseline data to measure endline target for the product (no. of vouchers generated etc)</li></ul> |
| Exit Criteria       | <ul><li>Publish Project Charter</li><li>Cloud Infrastructure procured</li><li>Finance and Accounting cell formation and appointment</li><li>Project office space allocated</li><li>Program Branding (Name,logo,tagline etc)</li><li>Pilot ULBs Identified &#x26; ULB team On-boarded</li><li>Finalized Chart of Accounts for the State</li><li>Accounting Process gaps Identified for Introduction / rectification</li><li>Kickstart</li></ul><p>•Pilot ULB Preparations</p><p>•Finalization of State Level Master Data</p><p>•Data Preparation Efforts for Budget, Assets, Masters, Opening Balance</p>                                                                                                           |

During the Program design stage key state/UT officials and members, who are subject matter experts, are expected to share state/UT specific manuals and also help interpret these manuals for the System Integrator (SI) Team. This stage baselines the State/UT-specific product features in the Product Configuration report.

| Stage 2 -Program Design |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| ----------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Duration                | 7-8 weeks                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| Entry Criteria          | <ul><li>Define Chart of Accounts</li><li>Formation of Domain Team / Pilot ULB teams</li></ul>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| Key Activities          | <ul><li>Standardisation of all Finance processes</li><li>Initiate policy change if needed, based on the Processes defined</li><li>Conduct Product familiarisation workshop</li><li>Initiate collection of master data from pilot ULBs</li><li>Finalise data migration/collection/sync-up approach/data migration approach</li><li>Building capacity for basic understanding of resources and tools required to be used</li><li>Finalisation of Dashboard design for Program rollout Tracking</li></ul>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| Exit Criteria           | <ul><li>Accounting Processes Reengineered and Finalized – for Implementation on the ground</li><li>Scope of Pilot stage and Success Criteria defined</li><li>State level Policy Changes, if needed, taken up</li><li>Finalized Review mechanism / Cadence for Implementation Tracking, Adoption and Finance related Governance Metrics</li><li>Capacity Building Team Formed and Capacity Building Program Designed</li><li>Finalisation of Roll-out plan (in different phases)</li><li>Product Configuration / customization Report</li><li>Publish finalized - Accounting Processes, Workflows, Data Preparation Templates</li><li>Ensure Synching up the Data Preparation Strategy</li><li>Key Integrations with Finance mainly focused on primary Revenue and Expenditure buckets.</li><li>Solution agreement for required State/UT-specific customisations</li><li>Sign-off on data approach (Data collection/migration/ correction/sync-up/validation)</li><li>Detailed project plan published</li></ul> |

Configuration & customisation stage, spread across 12 weeks, envisages configuration of the product as per the baselined Product Configuration report and identified state/UT-specific customisations. Active involvement of domain experts from the state/UT Team is required in this stage to validate the implementation of state/UT accounting manuals.

| Stage 3 - Configuration & Customization |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| --------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Duration                                | 9-10 weeks                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| Entry Criteria                          | <ul><li>Product Configuration/ Customization Reports signed off</li><li>Detailed Project plan set up in accordance with master data collection and environment set up</li><li>Capacity Building Plans finalized</li><li>Pilot ULB team formed</li><li>Tracking Mechanisms finalized</li></ul>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| Key Activities                          | <ul><li>Setting up development environments</li><li>Development/customisation of reports and dashboards</li><li>Development/ integration of portal</li><li>Third-Party integrations (payment gateway, handheld/pos device)</li><li>Updation of user manuals and other key documents</li><li>Preparation &#x26; execution of Test Cases</li><li>Setup monitoring, support &#x26; maintenance processes, tools and dashboards</li><li>Capacity Building for making state team aware about basic usage of tools like MS Office, mails etc.</li><li>Identify ULB level Nodal officers for day to day support</li><li>Migration and verification of Pilot ULB data</li><li>Training (Users, trainer)</li></ul><p>-master trainers identified from ground for simultaneous training</p><ul><li>Training the support resources</li></ul> |
| Exit Criteria                           | <ul><li>Implementation &#x26; Data Preparation Team formed and Primed up</li><li>Configured/Customized product that is ready for UAT</li><li>Pilot ULB data Preparation Completed</li><li>Capacity Building Well underway for Non-Software (Finance Processes and Change Management interventions)</li><li>ULBs instructed to start implementing Missing Ground Level Processes and for data preparation</li><li>Product readied for UAT</li><li>Training Material – Ready for Capacity Building on Finance Product</li><li>Monitoring, support &#x26;amp; maintenance of Dashboards</li><li>Finalization of Initial Reporting and Dashboard KPIs</li></ul>                                                                                                                                                                       |

During this stage, the active involvement of Pilot ULB officials is expected for thorough testing of the configured product. Training of the key ULB officials will also be undertaken during this stage, along with the promotion of the solution. The establishment of the State/UT support Team and required processes are initiated in this stage.

| Stage 4 - Pilot and UAT |                                                                                                                                                                                                                                                                                                                                                                                                                             |
| ----------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Duration                | 3-4 weeks                                                                                                                                                                                                                                                                                                                                                                                                                   |
| Entry Criteria          | <ul><li>Pilot ULB Team Clear on Scope, Processes and Product</li><li>Full Product Configured / readied as per Configuration / Customization report</li><li>Implementation tracking Mechanisms finalized</li><li>Kick-off of Data Preparation efforts</li></ul>                                                                                                                                                              |
| Key Activities          | <ul><li>UAT Environment Setup</li><li>Identification of participants for UAT session</li><li>Regression UAT and sign off from Pilot ULBs/ State</li><li>Issues/bug resolution</li><li>Setting up the Production environment</li><li>Setting up Support Center &#x26; processes (Help Desk)</li><li>Marketing &#x26; promotion activities</li><li>Go Live &#x26; launch event</li></ul>                                      |
| Exit Criteria           | <ul><li>Pilot Success as per Pilot Scope</li><li>Product UAT Completed &#x26; Signed off</li><li>Go LIVE Schedule Announced (Max 3 or 4 phases) and readiness sought</li><li>Implementation Tracking Dashboard &#x26; Finance Dashboard are readied for Reviews on Adoption/ Outcomes</li><li>Capacity Building Well underway for Non-Software</li><li>Capacity Building for UP Specific Finance Product Underway</li></ul> |

On successful rollout in the Pilot ULBs, the solution will be rolled out to the rest of the ULBs in batches. Guidance and support from the State/UT Team will be required to create the rollout plans and assure the necessary infrastructure for training and deployment is available at each ULB.

Note: The rollout phase needs to be detailed out for iterative activities of onboarding ULBs in batches.

| Stage 5- Go live |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| ---------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Duration         | 14-16 weeks                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| Entry Criteria   | <ul><li>UAT Completion</li><li>Correct Data Loads</li><li>Capacity Building for ULBs on State Finance Product Completed</li><li>Capacity Building Well underway for Non-Software</li></ul>                                                                                                                                                                                                                                                                                                             |
| Key Activities   | <ul><li>ULB configurations phase wise as per the Project Plan</li><li>Migration and verification of ULB data</li><li>Logistics planning for training</li><li>Establishment of bug ticketing tool for resolving ground level issues by the state team</li><li>Training of master trainers for training the end users of all ULB’s</li><li>Pan State Roll Out - Phase wise</li><li>Stabilise product</li><li>Setup of review and monitoring cadence( Field Visit Plan, Review Dashboards etc.)</li></ul> |

| Stage 6: Monitoring and Sustenance |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| ---------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Duration                           | NA                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| Entry Criteria                     | <ul><li>ULBs Live &#x26; Finance Team empowered to handle all operations</li></ul>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| Key Activities                     | <ul><li>Adoption Review Meetings as per the vision defined for the program</li><li>The team focuses on Using data for:</li><li>Tracking field issues and performance data to identify improvements</li><li>Identify additional Integrations around Finance to make processes more robust towards enhancing accounting functionalities (e.g. Upstream and downstream Processes)</li><li>Plans of ongoing sustenance in Place with respect to:</li><li>Funding</li><li>IT support (infra, helpdesk, ongoing enhancements)</li><li>Process Effectiveness and Improvements</li></ul> |
| Ongoing Criteria                   | <ul><li>Adoption and Performance Measurements being monitored</li><li>Clear Mechanisms for Capturing from Field – Issues / Suggestions</li><li>Focus on using data to identify Process Improvements and additional Integration for ensuring movement towards target</li><li>Team ramped down to Monitoring and Sustenance levels</li><li>Plans for Ongoing Sustenance in place</li><li>Funding</li><li>Resource availability</li><li>Project enhancement</li></ul>                                                                                                               |

Stage 5 – Rollout

## Roles and Responsibilities - Finance and Accounting Cell, eGov Team & System Integrator(SI)Team

This section outlines the activities involved in each stage of the implementation along with responsibility and accountability of critical stakeholders - State, eGov Team and System Integrator Team onboard.

Finance and Accounting Cell: Finance and Accounting Cell is the government-appointed body chaired by the Principal Secretary/Secretary, Urban Development Department with members from Urban Development Department etc.

Resource requirements for the Finance & Accounting Cell required to be formed by the State

| Resource Name          | No. Of Resources                                          |
| ---------------------- | --------------------------------------------------------- |
| Project Head           | 1                                                         |
| Domain Expert          | 1 Representation from Corporations/Council/Panchayat etc. |
| District Nodal Officer | 1 per district                                            |
| MIS Expert             | 1 per district                                            |

{% hint style="info" %}
Note:

* Designation mentioned above are as per designations already driving Finance and Accounting implementation at the State level.
* The description of each designation is explained below.
* Project Head: Is the Head of the Finance and Accounting Cell who will drive the project from the State’s Side
* Domain Expert: Person who is well aware of the on ground scenario, well versed with the act, GOs passed, Prevalent Business processes, Deviations from the acts.
* Nodal officer (EO/Commissioner/ Senior Official): The product coordinator to drive the project centrally. Monitor usage post Go Live- point of escalation for Implementation Team, Seasoned and worked in Multiple ULBs on various modules and has a good understanding of Finance, facilitate and track data collection post Go Live, monitors and facilitates adoption of application. Point of contact for Management team, SI at the HQ level.
* MIS Expert: Day to day tracking of the data specific to ULBs, data collection/validation for correctness and comprehensiveness, reporting and review to senior officials
{% endhint %}

eGOv Team: eGov Team is the technical partner of the project which will provide all necessary support to the State/UT concerning the implementation, Program Designing etc.

System Integrator (SI)Team: SI Team will be responsible for consulting, program management and the implementation of products in the ULBs in close collaboration with the Finance and Accounting cell, technical partner (eGov) and various other stakeholders.

{% hint style="info" %}
Guidelines to read the tables below:

Execute - One who owns the accountability to complete the activity

Consult - One who may initiate, guide and in the process, handhold the execution of the activity
{% endhint %}

| Stage 0 - Program Setup/ On-Boarding          |         |                  |
| --------------------------------------------- | ------- | ---------------- |
| Task/Activity                                 | eGov    | State Leadership |
| Appoint Finance and Accounting Cell           | Consult | Execute          |
| Finalise funding for the program              | Consult | Execute          |
| Define state -specific procurement process    | Consult | Execute          |
| System Integrator(SI) Team sign-up/onboarding | Consult | Execute          |
| Finalise Finance Impel Program Vision         | Consult | Execute          |

| Stage 1 - Program kick-off                                                                                                                                      |         |                           |         |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------- | ------------------------- | ------- |
| Task/Activity                                                                                                                                                   | eGov    | Finance & Accounting Cell | SI Team |
| Identify & agree on scope and exclusions                                                                                                                        | Consult | Consult                   | Execute |
| Identify pilot ULBs                                                                                                                                             |         | Execute                   | Consult |
| Project Kickoff - Implementation Methodology Presentation                                                                                                       | Consult | Consult                   | Execute |
| Product Walkthroughs                                                                                                                                            | Consult |                           | Execute |
| Define Project Steering Committee structure and Project Governance process                                                                                      | Consult | Consult                   | Execute |
| Define phases of deployment/ rollout                                                                                                                            |         | Consult                   | Execute |
| Agreement on Deployment Priorities and high-level delivery timelines                                                                                            |         | Consult                   | Execute |
| <p>Assessment of all Finance and Accounting process along</p><p>(1) citizen services/channels around it</p><p>(2) Integration with other department process</p> |         | Consult                   | Execute |
| Finalize Program Success Metrics for Adoption and Governance adhering to the vision of the program                                                              | Consult | Consult                   | Execute |
| Internal Capacity Building, program logistics at State and ULBs, as per the current scenario                                                                    |         | Execute                   | Consult |
| Collection of baseline data to measure endline target for the product (Revenue generated, total properties in ULBs etc.)                                        | Consult | Execute                   | Consult |

| Stage 2 - Solution Design                                                                           |         |                           |         |
| --------------------------------------------------------------------------------------------------- | ------- | ------------------------- | ------- |
| Task/Activity                                                                                       | eGov    | Finance & Accounting Cell | SI Team |
| Standardisation of all Finance processes, if needed                                                 |         | Consult                   | Execute |
| Initiate policy change, if needed based on identified improvements                                  | Consult | Execute                   | Consult |
| Conduct Product familiarisation workshop                                                            |         | Consult                   | Execute |
| Initiate collection of master data from pilot ULBs                                                  |         | Consult                   | Execute |
| Finalise data migration/collection/sync-up approach                                                 |         | Consult                   | Execute |
| Finalise data validation approach                                                                   |         | Execute                   | Consult |
| Capacity Building for making state team aware about basic usage of tools like MS Office, mails etc. |         | Execute                   | Consult |

| Stage 3 – Configuration & Customization                                                             |      |                           |         |
| --------------------------------------------------------------------------------------------------- | ---- | ------------------------- | ------- |
| Task/Activity                                                                                       | eGov | Finance & Accounting Cell | SI Team |
| Setting up development environments                                                                 |      | Consult                   | Execute |
| Development/customisation of reports and dashboards                                                 |      | Consult                   | Execute |
| Development/Integration of portal                                                                   |      | Consult                   | Execute |
| Third-Party Integrations (Payment gateway, Handheld/pos device)                                     |      | Consult                   | Execute |
| Updation of user manuals and other key documents                                                    |      | Consult                   | Execute |
| Preparation & execution of Test Cases                                                               |      | Consult                   | Execute |
| Setup monitoring, support & maintenance processes, tools and dashboards                             |      | Consult                   | Execute |
| Finance legacy data collection from Pilot ULBs(at least)                                            |      | Consult                   | Execute |
| Capacity Building for making state team aware about basic usage of tools like MS Office, mails etc. |      | Execute                   | Consult |
| Migration and verification of Pilot ULB data                                                        |      | Consult                   | Execute |

| Stage 4 – UAT & Go Live                            |         |                           |         |
| -------------------------------------------------- | ------- | ------------------------- | ------- |
| Task/Activity                                      | eGov    | Finance & Accounting Cell | SI Team |
| UAT Environment Setup                              | Consult | Consult                   | Execute |
| Identification of participants for UAT session     |         | Consult                   | Execute |
| Issues/bug resolution                              |         | Consult                   | Execute |
| Regression UAT and sign off from Pilot ULBs/ State |         | Execute                   | Consult |
| Setting up the Production environment              |         | Consult                   | Execute |
| Setting up Support Center & processes (Help Desk)  |         | Execute                   | Consult |
| Training user                                      |         | Execute                   | Consult |
| Training Trainer                                   |         | Consult                   | Execute |
| Training the Support Resources                     |         | Consult                   | Execute |
| Marketing & promotion activities                   |         | Execute                   | Consult |
| Go Live & launch event                             | Consult | Execute                   | Execute |
| Setup of review and monitoring cadence/team        |         | Execute                   | Consult |

| Stage 5: Rollout                                                                        |         |                           |         |
| --------------------------------------------------------------------------------------- | ------- | ------------------------- | ------- |
| Task/Activity                                                                           | eGov    | Finance & Accounting Cell | SI Team |
| ULB configurations phase wise as per the Project Plan                                   |         | Consult                   | Execute |
| Migration and verification of ULB data                                                  |         | Execute                   | Consult |
| Logistics planning for training                                                         |         | Execute                   | Consult |
| Establishment of bug ticketing tool for resolving ground level issues by the state team |         | Consult                   | Execute |
| Training the Users at the district level                                                |         | Execute                   | Consult |
| Pan State Roll Out - All Locations                                                      | Consult | Execute                   | Execute |
| Stabilise product                                                                       |         | Consult                   | Execute |

| Stage 6- Sustenance and Ongoing Improvement                                                                                                                                                      |         |                           |         |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------- | ------------------------- | ------- |
| Task/Activity                                                                                                                                                                                    | eGov    | Finance & Accounting Cell | SI Team |
| Adoption Review Meetings as per the vision defined for the program                                                                                                                               | Consult | Execute                   | Consult |
| <p>Finance Cell Focuses on Using data for:</p><ul><li>tracking field issues and performance data to identify improvements</li><li>identify additional Integrations around Finance</li></ul>      |         | Execute                   | Consult |
| <p>Plans of ongoing Sustenance in Place with respect to :</p><ul><li>Funding</li><li>IT support (infra, helpdesk, ongoing enhancements)</li><li>Process Effectiveness and Improvements</li></ul> | Consult | Execute                   | Consult |

## Overall Program Assumptions

| Areas          | Assumptions                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| -------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Infrastructure | <ul><li>The actual Infra will be provided based on the questionnaire inputs received from the state</li><li>The state will take care of providing necessary project infrastructure and office facilities during the program for all on-site project Team members, which will be confirmed during the initiation phase. This includes workspace, office equipment (e.g., telephone with STD, fax machine, photocopy machine, etc.), stationery, PC/workstation, project LAN and internet access, etc.</li><li>The state will provide the necessary administrative support staff to carry out day-to-day project administration tasks, e.g., meeting rooms, Videoconferencing, etc.</li><li>The state should provide a Project Office and at least one conference room with speakerphone throughout the Project Duration.</li></ul> |
| Project Scope  | <ul><li>Any new requirements received from State during the implementation phase will be handled through a change management process</li></ul>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| State Team     | <ul><li>The state will nominate a reasonably sized multifunctional Team from various departments of the State to be responsible for the implementation. The state Team would be required for information, validation, and execution through the implementation cycle and the Team members should be reasonably empowered to take decisions. Any delay in the decision-making process and the non-availability of the State Team may have an impact on the schedule.</li><li>The participants from State are expected to have a thorough understanding of the State’s internal processes.</li><li>The state will engage internal and external stakeholders required for this engagement and ensure their availability whenever needed.</li></ul>                                                                                   |
| Documentation  | <ul><li><p>The Tech Implementation Partner will ensure provision of the following:</p><ul><li>User education and training documentation delivery as per the default product documentation of the identified product versions.</li><li>Product manuals are expected to be shared with the State as part of the user manual.</li><li>All documentation in English and the language requirement of the state.</li></ul></li></ul>                                                                                                                                                                                                                                                                                                                                                                                                    |
| Training       | <ul><li>Training to the end-users will be driven by the state Team.</li><li>The state will be responsible for providing the necessary infrastructure required for the Training, which includes the following readiness.</li><li>Training Rooms (Parallel Training Sessions) with Projector, White Board, Markers, Internet Connection, sufficient seating capacity, Desktop/Laptop for each participant and availability of Network for Trainees to connect to the server.</li></ul>                                                                                                                                                                                                                                                                                                                                              |
| Implementation | <ul><li>The scope of the implementation will be limited to the services mentioned in Section 2.</li><li>State Team will have an identified SPOC for handling the first level of eGov communication with the client unless discussed and agreed.</li><li>eGov Team will not be involved in defining the test cases or executing the test cases.</li><li>Necessary signoff would be provided by the state upon completion of the defined milestones.</li></ul>                                                                                                                                                                                                                                                                                                                                                                      |

## GLOSSARY

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

Customisation:

Details of changes to be made in the Product to comply with the needed field process

Configuration:

Defining existing content such as Options and Variables based on the requirements on the ground

Product walkthrough:

Explaining the users step-by-step through a set of actions that they need to take to achieve a specific outcome

Terminologies specific to Finance Delivery Handbook

Accrual Based Finance Accounting:

Method of recording accounting transactions for revenue when earned and expenses when incurred. The income or expense is recognised even through the related receivable/payable has a future date.

Double-entry Accounting:

The system of accounting or bookkeeping which ensures that for every business transaction, amounts must be recorded in a minimum of two accounts. The double-entry system also requires that for all transactions, the amounts entered as debits must be equal to the amounts entered as credits.

Asset Management:

Asset management is the process of inventory, valuation, use, strategic portfolio reviews, reporting and auditing of municipal assets as part of the decision making process of local governments.

Voucher approval:

Reviewing the transaction for compliance with policies and process.

G/L posting:

General Ledger posting is the process of posting the Payroll results to the appropriate GL accounts including the cost centres.

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation ](https://egov.org.in/)is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).
