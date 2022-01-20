# OBPAS Demo Script

## Objective

Welcome to the OBPAS product demo script. The key objective of the demo script is to walk users through the OBPAS module and highlight module capabilities and functions.

## Module Overview

The Online Building Permission and Approval System or the OBPAS module offers a comprehensive platform that automates the entire building plan approval process. The OBPAS module along with the eDCR scrutiny application streamlines the entire process right from the point of uploading plans for approval to fetching no-objection certificates from concerned authorities and final issue of approvals or permits.

### Key Challenges Addressed

The module aims to address key challenges that include -

* Any construction in the city requires prior approval from the local body authorities. Architects and building owners submit a plan diagram that is validated as per the state/city bylaws.
* Most of the building plan applications and drawing plans are submitted manually in paper format since there is a high cost involved for the AUTOCAD license and the absence of cost-effective plan scrutiny solutions.
* The major drawback of the manual permit application process is that it takes more than 45 days to get one permit.
* Iterative plan corrections complicate the process.
* Lack of transparency is another major setback for all stakeholders.

### User Benefits

Key benefits of using the OBPAS application -

* Scrutiny is real-time which reduces the time taken for diagram scrutiny. The module routes the uploaded plans through defined workflows for required inspections and approvals.
* It provides access to all authorized stakeholders including department staff, Architects/Consultants, Building owners and Senior Management team based on their role entitlement.
* Being an online system, DIGIT BPA is available anywhere, any place and on any device to the various stakeholders mentioned above. The intuitiveness of the DIGIT-BPA system becomes apparent when even a layman is able to track the status of their submission easily.

Consolidated OBPAS application help ULBs -

* Plan city infrastructure (roads, culverts, drains, streetlights, garbage bins) details better resulting in effective decisions depending upon the type of buildings and their occupancies
* Since capital infra is the second highest expenditure category for any ULB, it is important to know where to invest the funds and resources
* Ensure buildings are not constructed in restricted areas zones (AAI / Water bodies /Monuments)
* Generate revenue and facilitate prompt services to the citizen

## Functional Demo

### eDCR Scrutiny & Application Submit

The eDCR Scrutiny application digitises the building plan approval. The application features a rules engine required to evaluate the drawing against the existing building by-laws, the scrutiny of the application, configure the internal workflow - inspection, NOCs and finally issuance of approval.

* A stakeholder can be an Architect/Licensed business engineer/town planner who is registered within the ULB. Only a registered stakeholder (architect) can create an application on behalf of the citizen.
* eDCR (development control rules) - which is a rules engine that basically validates the uploaded diagram with that of the by-laws of the state and provides an O/P.
  * UNique reference eDCR number is generated only if it is successful.
  * In case of a failure - the errors are marked in the diagram which can be corrected by the architect and submitted again. This can be iteratively done till scrutiny is successfully completed.
* Using the successfully scrutinized plan diagram parameters, an application is created. Any value which is populated from the plan diagram cannot be modified. There is no manual intervention allowed.
* Discuss the EODB guideline which discusses getting all the application info from citizens in one shot.
  * Here showcase one application from OBPS is getting forked into 3 applications (one for the department to process the permit, one for airport NOC and one for FIRE NOC)
  * Discuss application is smart enough to figure out the list of NOCs required based on the location info gathered from the diagram.
  * The Architect on the creation of an application forwards it to get it concurred from the citizen. If there are any changes, the citizen requests an architect to make those changes or else can inform the architect to submit the application.
  * After getting approval from the citizen, the architect submits the application. On submit, the application fee is auto-generated based on configured payment details. Once the payment is made, the application is forwarded to the department.
    * Application fee can be either paid by the citizen or architect or the citizen can walk into any ULB designated collection counter and make the payment.

### Application Processing by Employees

* Submitted applications are available in the ULB clerk inbox for the required processing. Actions by the ULB clerk or counter employee include -
  * Scrutinize the application and documents submitted and check for correctness.
  * Request for additional documents from the applicant
  * Or Upload documents on behalf of the applicant
  * Or Reject the application citing the reason for a rejection
  * Or if the application and documents are in order, the clerk forwards the application for field inspection.
* The Town planning overseer/Engineer does the field inspection of an application. Actions by the Field inspector include -
  * Schedule a meeting with the applicant offline after receiving the request and visit the actual location on the day of field inspection
  * The entire application is designed in a mobile-first approach which will enable the field inspector to use the application on the ground on a mobile phone
  * The field inspection report is designed as a series of checklists with yes and no options to make the process easier for a field inspector.
  * Also, the FI can take photographs of the site and tag them to the application.
    * If no violations are found - FI forwards the application for NOC verification
    * If due to some practical reasons, field inspection is not completed in a single visit - FI does multiple field inspections; the application supports the entry of multiple field inspection details.
    * If some violations are identified, the FI rejects the application.
* NOC Verification - NOC verification responsibility lies with the superintendent of the department.
  * Refer back to the Forking of applications during the application created by Architect
  * Now showcase the status of all 3 applications at the NOC level where you can see the NOC applications are of status in progress.
  * Now login as a FIRENOC department user - process the NOC application and approve it.
  * Now login as Superintendent - showcase the status change from in progress to approved and discuss 3 use cases of NOC integration.
    * One API integration
    * Allowing NOC department users to log in to DIGIT and process the application
    * Completely manual where either the NOC is provided by citizens during application creation or by the Department employee by discussing with the NOC department user.
  * Now approve the NOC step of the application and recommend for approval.
* Executive Engineer/Superintendent engineer can approve the application by entering the permit conditions.
  * There is a calculation logic that runs in the background to calculate the Permit fee using the built-up area and floor area.
  * Also, discuss the importance of permit conditions.
  * Now approve the file.
* The next step is for the Architect or the Citizen to make payment for the permit fee and generate the permit order online.
  * Discuss the info in the permit order
  * QR code info
  * Payment info
  * Approver info

## Demo Use Case Scenarios

Possible use case scenarios for the demo -

1. Architect to do eDCR scrutiny
2. Architect to apply for permit application
3. Architect to apply for OC application
4. Citizen to approve/validate the application created by architect
5. Architect and citizen can make payment for application
6. The employee does document scrutiny - can add additional documents if needed
7. The employee does field inspection - update field inspection report- attach photographs of the site if needed
8. The employee does NOC verification - update NOC documents on behalf of NOC department user or citizen if needed.
9. NOC department user to update the NOC details
10. The employee can update the permit conditions
11. Citizens and architects can download the permit order/Occupancy certificate/comparison report, revocation permit PDF and other payment artefacts.
12. The Architect can generate permit orders on create of applications for low-risk applications.

Refer to the [OBPAS User Manual](obpas-user-manual/) for step-by-step instructions on these demo scenarios.

> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)_​_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
