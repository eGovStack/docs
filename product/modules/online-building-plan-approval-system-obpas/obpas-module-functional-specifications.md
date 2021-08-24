---
description: Functional overview for stakeholders
---

# OBPAS Module Functional Specifications

## Introduction

This module enables Architects / Engineers / Supervisors /Town Planners etc. to register Online. Provision to migrate already registered Architects/ Engineers / Supervisors details in the system with current status and validity of registration. Provision to renew the registration.

1. Centralized Registration: Provide a single interface for the registration of all architects \(across the state\), who intend to do a transaction with the ULBs. 
2. Online Application for Registration: Identify the applicant with reference to a unique ID. Capture the following minimum information of the applicant with appropriate validations.
   1. Unique ID 
   2. Name 
   3. Address  
   4. Corporate Information  
   5. Certificate from Council of Architecture/ Other authorities 
   6. Educational Qualification
3. This module will also consist of the following:- 
   1. Facility for uploading of attachments as required by ULB for establishing identity and past experience etc.
   2. Enable online submission of registration fee.
   3. Assigning a unique application number to each applicant.
   4. Enable tracking the status of the application.

## Functional Scope

The OBPS product features can be broadly classified as the following modules:

1. Online registration of Architects/ Engineers / Supervisors etc.  
2. Online Real Time Scrutiny of Drawing/Plan  
3. Submission of Application and uploading Documents  
4. Application Process by the Department 
5. Online Payment 
6. Certificate 
7. Notice 
8. General requirements 
9. Module 1: Online registration of Architects/ Engineers / Supervisors etc. 
<<<<<<< HEAD
10. Approval of Applications: Enable the Competent Authority to approve/reject the applications for registration; based on a workflow system and business rules. Communication of successful registration/ rejection to the applicant through an e-mail alert & SMS. 
11. Renewal of Registrations: Enable the Competent Authority to renew the applications for registration according to workflow/business rules. Communication of successful renewal will be sent to the applicant through an e-mail alert & SMS. 
12. Search: Enable authorized officials to search the database for list of registered architects based on the ‘search’ criteria such as - line of business, turnover, past experience or as decided by ULB. 
13. Help: Provide an online handbook and user manual for registration. Provide FAQs on the registration process. ULB official will provide help desk assistance for resolving architects queries on registration process. 
14. Module 2: Online Real Time Scrutiny of Drawing/Plan
15. The Module enables the Architect/Engineer to submit the Drawing in Drawing Interchange Format\(DXF\) format from any Open Source CAD tools of their choice. The condition for the following are:
    1. The drawing should adhere to the Standards stipulated. 
    2. The Standards will be provided to the Architect in the native format \(DXF\) .
16. The Module enables the Architect/Engineer to submit the Application for various Services as listed above along with required supporting documents. Under the current provision, the document checklist will aid the Architect/Engineer. 
    1. The scrutiny process is online realtime and the Architect/Engineer will get the detailed Scrutiny report within minutes of submitting the Plan.
    2. Scrutiny reports will list the Bye-laws and sub-clauses with the approved values against the extracted values.
    3. Based on the extracted value range validation will be done by the system.
    4. Only on clearance of all the Rules Scrutinised the Report will reflect ACCEPTED.
    5. On Accepted Report a unique number of the Scrutiny will be generated
17. Scrutiny Parameters for all types of building meant for different usage; as per building bye laws and approved master plan will be taken into scrutiny. The major Plan provisions are as under : 
    1. Plot area / shape 
    2. Road width details 
    3. MOS \(Marginal open space\) 
    4. Ground coverage 
    5. FAR \(Floor area ratio\) 
    6. Building height 
    7. Use of building \(Floor wise including mixed use in floors\) 
    8. Parking provision 
    9. Amenities
    10. Components of building
    11. Services Evaluation 
    12. Firefighting requirement 
    13. Green building norms 
    14. Rain Water Harvesting 
    15. Water supply 
    16. Water treatment 
    17. Solid waste management provisions 
    18. NOC required on the basis of drawing details 
18. Module 3: Submission and processing of Application  
19. The entire process from the time of submission of drawing to scrutiny completion is automatic without any human intervention and instantaneous.
    1. If the Scrutiny report REJECT the drawing the Report will have the details of the clauses in which it was rejected and also the values of the parameters. 
    2. The Architect/Engineer can correct the drawing and can resubmit the drawing till he gets the approval. 
    3. Only on approval the unique reference number for the Scrutiny Report will be generated. 
    4. Only with this number the Submission of Application can be initiated.
20. The OBPS handles the Plan Scrutiny in Online Real time mode and there is no need for any wait time, once the Plan is drawn. Scrutiny gets completed in less than a minute.. 
21. From the Plan submitted by the Architect the System will generate all the relevant plan in PDF format automatically. These are the set of Plans which will be issued to the end user with certification on successful completion of the Application Process. 
22. The Application can be filled and required documents can be uploaded by the Architect once he has the Plan Scrutiny Reference number. 
23. On Submission the Citizen need to validate and self certify the Application.
24. Module -4: Application Process by the Department 
25. Workflow is configurable as per the requirements and will be done during the Customisation phase of the Project
26. All approvals will be electronically signed \(e-sign\) with QR code 
27. The application captures all relevant details for all internal and external agencies; relevant data needs to be forwarded to corresponding agencies for issuing NOCs. 
28. SLA on NOC is also validated by the System. If the required date is passed without a reply from the NOC department the NOC will be taken as Deemed approved.
29. In addition a single window mechanism is also built into the system. This feature can be used by Departments which do not have the IT system for their process in full.
30. Provision for entering onsite inspection details and geo-tagged images \(document upload facility\) of the Site Inspection. 
31. The product has for the staff and the management for viewing the completed and pending tasks / works / applications. 
32. The product has features for Online single window system, and integrations with all internal and external agencies required to provide applicable NOCs/approvals \(Fire Services, Water and Sewerage Department, Discoms, AAI, NMA, Forest, Labour, Factory Directorate\)
33. A Statewide Dashboard is also available which can be used by State Administrators to see the flow of applications and the pendency or exceptions.
34. The product offers Security on User Authentication with Role based access 
35. The product will generate various MIS reports as per requirements of the Departments from time to time. MIS reports based on the payment received, dues position, plans passed, pending proposals, delayed approvals be generated as per Department requirement. 
36. The Product has well-defined inspection report format at various levels to guide the inspectors which is also configurable. 
37. The  Product incorporates digital signature \(e-sign\) for approval of application at different levels in the application system, Building permission letter, approved drawing, notices, letters, completion cum occupancy certificates etc. 
38. Product has well defined service levels and the escalation matrix to officials regarding time limit for processing an application automatically in the system. 
39. The  Product after the Citizen validates the application the system will schedule the Document Verification visit date. This date can be rescheduled by both the parties once. 
40. SMS/Email Alerts enabled in the  Product
=======



1. Approval of Applications: Enable the Competent Authority to approve/reject the applications for registration; based on a workflow system and business rules. Communication of successful registration/ rejection to the applicant through an e-mail alert & SMS. 
2. Renewal of Registrations: Enable the Competent Authority to renew the applications for registration according to workflow/business rules. Communication of successful renewal will be sent to the applicant through an e-mail alert & SMS. 
3. Search: Enable authorized officials to search the database for list of registered architects based on the ‘search’ criteria such as - line of business, turnover, past experience or as decided by ULB. 
4. Help: Provide an online handbook and user manual for registration. Provide FAQs on the registration process. ULB official will provide help desk assistance for resolving architects queries on registration process. 
5. Module 2: Online Real Time Scrutiny of Drawing/Plan
6. The Module enables the Architect/Engineer to submit the Drawing in Drawing Interchange Format\(DXF\) format from any Open Source CAD tools of their choice. The condition for the following are:
   1. The drawing should adhere to the Standards stipulated. 
   2. The Standards will be provided to the Architect in the native format \(DXF\) .
7. The Module enables the Architect/Engineer to submit the Application for various Services as listed above along with required supporting documents. Under the current provision, the document checklist will aid the Architect/Engineer. 
   1. The scrutiny process is online realtime and the Architect/Engineer will get the detailed Scrutiny report within minutes of submitting the Plan.
   2. Scrutiny reports will list the Bye-laws and sub-clauses with the approved values against the extracted values.
   3.  Based on the extracted value range validation will be done by the system.
   4. Only on clearance of all the Rules Scrutinised the Report will reflect ACCEPTED.
   5. On Accepted Report a unique number of the Scrutiny will be generated
8. Scrutiny Parameters for all types of building meant for different usage; as per building bye laws and approved master plan will be taken into scrutiny. The major Plan provisions are as under : 
   1. Plot area / shape 
   2. Road width details 
   3. MOS \(Marginal open space\) 
   4. Ground coverage 
   5. FAR \(Floor area ratio\) 
   6. Building height 
   7. Use of building \(Floor wise including mixed use in floors\) 
   8. Parking provision 
   9. Amenities
   10. Components of building
   11. Services Evaluation 
   12. Firefighting requirement 
   13. Green building norms 
   14. Rain Water Harvesting 
   15. Water supply 
   16. Water treatment 
   17. Solid waste management provisions 
   18. NOC required on the basis of drawing details 
9. Module 3: Submission and processing of Application  
10. The entire process from the time of submission of drawing to scrutiny completion is automatic without any human intervention and instantaneous.
    1.  If the Scrutiny report REJECT the drawing the Report will have the details of the clauses in which it was rejected and also the values of the parameters. 
    2. The Architect/Engineer can correct the drawing and can resubmit the drawing till he gets the approval. 
    3. Only on approval the unique reference number for the Scrutiny Report will be generated. 
    4. Only with this number the Submission of Application can be initiated.
11. The OBPS handles the Plan Scrutiny in Online Real time mode and there is no need for any wait time, once the Plan is drawn. Scrutiny gets completed in less than a minute.. 
12. From the Plan submitted by the Architect the System will generate all the relevant plan in PDF format automatically. These are the set of Plans which will be issued to the end user with certification on successful completion of the Application Process. 
13. The Application can be filled and required documents can be uploaded by the Architect once he has the Plan Scrutiny Reference number. 
14. On Submission the Citizen need to validate and self certify the Application.
15. Module -4: Application Process by the Department 
16. Workflow is configurable as per the requirements and will be done during the Customisation phase of the Project
17. All approvals will be electronically signed \(e-sign\) with QR code 
18. The application captures all relevant details for all internal and external agencies; relevant data needs to be forwarded to corresponding agencies for issuing NOCs. 
19. SLA on NOC is also validated by the System. If the required date is passed without a reply from the NOC department the NOC will be taken as Deemed approved.
20. In addition a single window mechanism is also built into the system. This feature can be used by Departments which do not have the IT system for their process in full.
21. Provision for entering onsite inspection details and geo-tagged images \(document upload facility\) of the Site Inspection. 
22. The product has for the staff and the management for viewing the completed and pending tasks / works / applications. 
23. The product has features for Online single window system, and integrations with all internal and external agencies required to provide applicable NOCs/approvals \(Fire Services, Water and Sewerage Department, Discoms, AAI, NMA, Forest, Labour, Factory Directorate\)
24. A Statewide Dashboard is also available which can be used by State Administrators to see the flow of applications and the pendency or exceptions.
25. The product offers Security on User Authentication with Role based access 
26. The product will generate various MIS reports as per requirements of the Departments from time to time. MIS reports based on the payment received, dues position, plans passed, pending proposals, delayed approvals be generated as per Department requirement. 
27. The Product has well-defined inspection report format at various levels to guide the inspectors which is also configurable. 
28. The  Product incorporates digital signature \(e-sign\) for approval of application at different levels in the application system, Building permission letter, approved drawing, notices, letters, completion cum occupancy certificates etc. 
29.  Product has well defined service levels and the escalation matrix to officials regarding time limit for processing an application automatically in the system. 
30. The  Product after the Citizen validates the application the system will schedule the Document Verification visit date. This date can be rescheduled by both the parties once. 
31. SMS/Email Alerts enabled in the  Product
>>>>>>> 64dca8adbdf64336b1a8203199b3791fa23434fa
    1. Document Verification Meeting
    2. Field Verification
    3. Fee Computed and Demand Generated
    4. Plan Permit Approved and Digitally Signed
<<<<<<< HEAD
41. The Checklist for the Document Verification will be filled up by the officials on the Document Verification meeting. In the system the the Checklist is configurable.
42. The  Product offers provision to incorporate the changes of building by-laws as intimated by the department in the application within time frame. 
    1. Product has the feature to capture the history of changes and based on the original application submission date the relevant rules will be taken into account for scrutiny.
43. The  Product has the feature of provisioning ther Revoking/Cancelling of Building Permission. 
44. On completion of the Document Verification the applicable NOC Departments will be addressed by the System for NOC.
45. Field Verification Schedule will be assigned by the System with reschedule option for both the parties once.
46. The officials can do the Field Verification, update the report in a checklist format and forward for approval
47. Module-5: Online Fee Payments 
48. The solution is  integrated with the payment gateway for Online Payments and facilitate for Fee collection, Fee calculation, refund calculation and generate online fee receipts based on the submitted Building plan. 
49. Upon approval of the report and NOC clearances the Fees are computed automatically by the system. 
50. The Fee computation uses the Plan Parameters and the applicable laws and rules of the State which are configurable.
51. The Plans in PDF will be generated by the System with QR Code without any manual intervention.
52. Citizen/Architect can pay the Fees Online
53. Upon payment of Fees Plan Permit Approval process will be initiated and approved with Digital Signature. The Permit has been incorporated with QR Code.
54. The Fees can be collected under various heads of accounts and the Reports for the collections against the Heads of Accounts will be generated. This will enable the user to account the collections accordingly. 
55. Module-6: Certificate\(s\) 
56. The product has provision to generate certificates with e-Sign/ digital signature and QR code which can be downloaded by the applicant.
57. Module-7: Notice\(s\) 
58. The notices, acknowledgment letters, approval letters, deviation or the rejection letters will be system generated with e-sign. 
59. Every communication sent/received from/by an applicant will be received online only and reflected in the case as well as in the reports which can be used in court cases & for any other purpose. 
60. Module-8: General requirements 
61. The software tracks delays in approval steps and maintain an audit log of the approval process steps. 
    1. System generates an alert against each application when it nears the time limit for disposing it. 
62. The solution allows extraction of system logs to excel/pdf formats for internal analysis of cases.
63. The product have provisions where in providing basic parameters like certificate no., name, area etc. would generate basic information about approved certificate and hence would enable easy third party verification. 
64. The Checklist, FAQ, User guide with video should be provided for end users. 
65. The product provision to get month wise approved/ rejected/ pending application and status of pending approval.
=======
32. The Checklist for the Document Verification will be filled up by the officials on the Document Verification meeting. In the system the the Checklist is configurable.
33. The  Product offers provision to incorporate the changes of building by-laws as intimated by the department in the application within time frame. 
    1.  Product has the feature to capture the history of changes and based on the original application submission date the relevant rules will be taken into account for scrutiny.
34. The  Product has the feature of provisioning ther Revoking/Cancelling of Building Permission. 
35. On completion of the Document Verification the applicable NOC Departments will be addressed by the System for NOC.
36. Field Verification Schedule will be assigned by the System with reschedule option for both the parties once.
37. The officials can do the Field Verification, update the report in a checklist format and forward for approval
38. Module-5: Online Fee Payments 
39. The solution is  integrated with the payment gateway for Online Payments and facilitate for Fee collection, Fee calculation, refund calculation and generate online fee receipts based on the submitted Building plan. 
40. Upon approval of the report and NOC clearances the Fees are computed automatically by the system. 
41. The Fee computation uses the Plan Parameters and the applicable laws and rules of the State which are configurable.
42. The Plans in PDF will be generated by the System with QR Code without any manual intervention.
43. Citizen/Architect can pay the Fees Online
44. Upon payment of Fees Plan Permit Approval process will be initiated and approved with Digital Signature. The Permit has been incorporated with QR Code.
45. The Fees can be collected under various heads of accounts and the Reports for the collections against the Heads of Accounts will be generated. This will enable the user to account the collections accordingly. 
46. Module-6: Certificate\(s\) 
47. The product has provision to generate certificates with e-Sign/ digital signature and QR code which can be downloaded by the applicant.
48. Module-7: Notice\(s\) 
49. The notices, acknowledgment letters, approval letters, deviation or the rejection letters will be system generated with e-sign. 
50. Every communication sent/received from/by an applicant will be received online only and reflected in the case as well as in the reports which can be used in court cases & for any other purpose. 
51. Module-8: General requirements 
52. The software tracks delays in approval steps and maintain an audit log of the approval process steps. 
    1. System generates an alert against each application when it nears the time limit for disposing it. 
53. The solution allows extraction of system logs to excel/pdf formats for internal analysis of cases.
54. The product have provisions where in providing basic parameters like certificate no., name, area etc. would generate basic information about approved certificate and hence would enable easy third party verification. 
55. The Checklist, FAQ, User guide with video should be provided for end users. 
56. The product provision to get month wise approved/ rejected/ pending application and status of pending approval.
>>>>>>> 64dca8adbdf64336b1a8203199b3791fa23434fa

Below mentioned table mention the functionality of the offered product as per the recommendations under the guidelines mentioned under the Ease of Doing Business\(EODB\) guidelines of 2019.

<table>
  <thead>
    <tr>
      <th style="text-align:left">Sr. No</th>
      <th style="text-align:left">Reform</th>
      <th style="text-align:left">Recommendation</th>
      <th style="text-align:left">Remarks</th>
      <th style="text-align:left"></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">1</td>
      <td style="text-align:left">Uniform Building Code</td>
      <td style="text-align:left">Enact a comprehensive uniform building code/building by-law with the following
        features:</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">&#x25CF; Prepare a uniform building code. The State may have separate
        sections within the uniform building code/ building by-law which apply
        to specific geographic areas or are under the administrative control of
        different agencies/ bodies</td>
      <td style="text-align:left">&#x25CF; OBPS Product offers these features: It has the functionality
        uniform building code, and the by-laws for the state can be configured.</td>
      <td
      style="text-align:left"></td>
        <td style="text-align:left"></td>
        <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">&#x25CF; Applicable to all urban areas and industrial estates/parks in
        the State</td>
      <td style="text-align:left">&#x25CF; Bylaws can be configured by based on Usage.</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">&#x25CF; Provisions for risk-based classification of buildings</td>
      <td
      style="text-align:left">&#x25CF; Risk can be classified in the application.</td>
        <td style="text-align:left"></td>
        <td style="text-align:left"></td>
        <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">&#x25CF; Accreditation programs and clear responsibilities for professionals
        including architects and engineers engaged in the construction process
        along with qualifications for accreditation under the program</td>
      <td style="text-align:left">&#x25CF; State Team&apos;s support is needed on this recommendation.</td>
      <td
      style="text-align:left"></td>
        <td style="text-align:left"></td>
        <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">2</td>
      <td style="text-align:left">Master Plans</td>
      <td style="text-align:left">Develop Master plans/ Zonal plans/ land use plans with legal sanction
        for all urban areas and make it available online in public domain</td>
      <td
      style="text-align:left">&#x25CF; State Team&apos;s support is needed on this recommendation.</td>
        <td
        style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">3</td>
      <td style="text-align:left">Construction Permit Approval</td>
      <td style="text-align:left">
        <p>Mandate timelines such that the following approvals/ NOCs are provided
          within 45 days:</p>
        <p>&#x25CF; Building Plan approval is granted within 30 days</p>
        <p>&#x25CF; Plinth Inspection is done within seven days of intimation</p>
        <p>&#x25CF; Final Completion/Occupancy Certificate is provided within eight
          days ( 7 days for inspection + 1 day for issuing the certificate)</p>
      </td>
      <td style="text-align:left">OBPS Product offered has this functionality - it can be configured from
        state to state</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">4</td>
      <td style="text-align:left">Construction Permit Approval</td>
      <td style="text-align:left">Design and develop an online single window system for granting construction
        permits with following functionalities:</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">&#x25CF; A common integrated application provided on the online unique
        window system, for all internal and external agencies required to provide
        applicable NOCs/approvals (Fire Services, Water and Sewerage Department,
        Discoms, AAI, NMA, Forest, Labor, Factory Directorate)</td>
      <td style="text-align:left">&#x25CF; OBPS Product offered has this functionality: Integrated application
        - one window portal for all stakeholders are available</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">&#x25CF; Provision for making an online application with integrated payment
        without the need for a physical touchpoint for document submission and
        verification</td>
      <td style="text-align:left">&#x25CF; Online payment interface is present is OBPS Product offered</td>
      <td
      style="text-align:left"></td>
        <td style="text-align:left"></td>
        <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">&#x25CF; The system should allow auto scrutiny of building plans from
        the compliance perspective according to the uniform Building Codes/Building
        By-law using AutoDCR (or similar) software</td>
      <td style="text-align:left">&#x25CF; Auto e-DCR scrutiny is available in the product offered based
        on the bylaws defined in the system</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">&#x25CF; Provision for e-intimation of commencement of construction</td>
      <td
      style="text-align:left">&#x25CF; OBPS Product offered has this functionality</td>
        <td style="text-align:left"></td>
        <td style="text-align:left"></td>
        <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">&#x25CF; Provision for e-intimation of plinth level completion</td>
      <td
      style="text-align:left">&#x25CF; OBPS Product offered has this functionality</td>
        <td style="text-align:left"></td>
        <td style="text-align:left"></td>
        <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">&#x25CF; Provision for online form for Completion/ Occupancy Certificate
        application with online payment of a fee</td>
      <td style="text-align:left">&#x25CF; OBPS Product offered has this functionality</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">&#x25CF; Provision for online issuance of the certificate of inspections</td>
      <td
      style="text-align:left">&#x25CF; OBPS Product offered has this functionality</td>
        <td style="text-align:left"></td>
        <td style="text-align:left"></td>
        <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">&#x25CF; Provision for online issuance of digitally signed Completion/
        Occupancy Certificate to the applicant</td>
      <td style="text-align:left">&#x25CF; OBPS Product offered has this functionality</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">5</td>
      <td style="text-align:left">Construction Permit Approval</td>
      <td style="text-align:left">Mandate that a single, joint site inspection will be carried out by all
        concerned authorities such as Fire, Water and Sewerage, Electricity, Labor
        (such as Factory license) Department and other internal Departments responsible
        for granting construction permits in urban areas and IDCs</td>
      <td style="text-align:left">&#x25CF; OBPS Product offered has this functionality</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">6</td>
      <td style="text-align:left">Construction Permit Approval</td>
      <td style="text-align:left">Implement a system which allows the grant of approval to Low-Risk buildings
        based on third party certification (during building plan approval and/or
        construction and/or completion stage) of structural design and architectural
        drawings across all urban areas and IDCs</td>
      <td style="text-align:left">&#x25CF; Grant of approval for the low-risk building is available in the
        product offered. Third-party certification is not necessary</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">7</td>
      <td style="text-align:left">Inspection by Building Proposal Office/ relevant agency as part of Building
        Plan Approval Process, Plinth Level Inspection and obtaining completion/
        occupancy certificate</td>
      <td style="text-align:left">Publish a well-defined inspection procedure, a checklist on the Department&#x2019;s
        web site and mandate that inspections (except in case of complaint-based
        inspection) shall be limited to the checklist</td>
      <td style="text-align:left">State Team&apos;s support is needed on this recommendation.</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">8</td>
      <td style="text-align:left">Inspection by Building Proposal Office/ relevant agency as part of Building
        Plan Approval Process, Plinth Level Inspection and obtaining completion/
        occupancy certificate</td>
      <td style="text-align:left">Design and implement a computerised system which is capable of:</td>
      <td
      style="text-align:left">Yes, the product offered has this functionality</td>
        <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">&#x25CF; Identifying buildings/areas that need to be inspected based on
        risk assessment</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">&#x25CF; Computerised allocation of inspectors</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">9</td>
      <td style="text-align:left">Inspection by Building Proposal Office/ relevant agency as part of Building
        Plan Approval Process, Plinth Level Inspection and obtaining completion/
        occupancy certificate</td>
      <td style="text-align:left">Mandate online submission of the inspection report within 48 hours to
        the Department</td>
      <td style="text-align:left">&#x25CF; OBPS Product offered has this functionality</td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>

<<<<<<< HEAD
[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation ](https://egov.org.in/)is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).
=======


 [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation ](https://egov.org.in/)is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).
>>>>>>> 64dca8adbdf64336b1a8203199b3791fa23434fa

