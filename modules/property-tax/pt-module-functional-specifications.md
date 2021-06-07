---
description: Functional overview for stakeholders
---

# PT Module Functional Specifications

## Introduction

The Property Tax System\(PT\) provides a digital interface to make property assessments, pay property tax, generate payment receipts and monitor tax collection. It can be used by the citizens, Urban Local Body \(ULB\) counter and field employees and ULB Administrators to accomplish their specific tasks. It is available as a mobile and web-based application.

## Functional Scope

The PT product features can be broadly classified as the following modules:

1. Registration, Login and Creation of User Profile
2. Filling an Assessment for a Property
3. Searching for a Property
4. Modifications to a Property
5. Generate Demand Notice
6. Payments collection and Receipts
7. Dashboards and Reports
8. General Features

### Registration, Login and Creation of User Profile

{% hint style="warning" %}
* OTP Based Login for Citizen via Web/Mobile App
* OTP Based Login for Employee via Web/Mobile App
* Provision for language selection during first time registration for both  Employee and citizens
* Provision of creating a personalized Profile for Citizens and employees on Web App
* Login Credentials for the various hierarchy of employees
* Role-based access for performing different actions relating to property tax modules
{% endhint %}

### Filing For Property Assessment

With this feature, a citizen and employee can perform a self-assessment of a new property for a financial year. This feature helps in registering the property in the system. The details of the property can be entered online and can be assessed for the calculation of the taxes.

The PT Product is designed in a user friendly manner and reduces chances of error. System calculates the tax automatically and creates the demand. If a user wants to reassess his property due to any reason \(for eg, incorrect data, change in property etc\), it can be done by editing details of the last assessment.

An employee can edit the details of the last assessment, on behalf of the citizen-based on the owner’s input. Citizen can track down the status of his incomplete assessment. Any incomplete assessment can be searched and completed.

{% hint style="warning" %}
* Citizen/CSC can Assess New Property \(By Different Financial Years\).
* Citizen/CSC can Capture Address, Assessment Info, Owner Info.for all types of properties like residential houses, flats and commercial buildings.

o Sample Details captured:

* Door Number, 
* Mutation number, 
* Number of floors,
* Area covered, 
* Owner and co-owner, 
* Mailing & permanent address, 
* Built year
* Individual room measurements
* The system computes the property taxes automatically as per process and rules of the state. 
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
{% endhint %}

### Searching for a Property

Citizen or Employee can track down the status of his incomplete assessment. Any incomplete assessment can be searched and completed.

{% hint style="warning" %}
* Citizen/CSC can search for Property by 
  * Mobile No,
  * City, 
  * Property Tax Unique ID
* Citizen/ CSC can view Incomplete Assessments
* Citizen/CSC can reassess Searched Property
* View Property details and pending dues
{% endhint %}

### Modifications to a Property

The PT system provides the ability to capture mutation and transfer of ownership. It reduces interfaces between the user and the State and thus promote greater transparency. It also helps in reducing the time taken for mutation after registration. The system provides the ability for alteration of assessment after verification and inspection. Any structural changes like addition/extension/reduction of existing built up area or construction type OR utility changes like usage or occupancy have an impact on the increase/decrease in property tax demand. These changes can be handled by the ‘Additional/Alteration of Assessment’ feature.

The System provides the ability for bifurcation/ amalgamation of property. The property bifurcation/ amalgamation undergoes an approval process. The parent property needs to be modified accordingly, which can be done in the system.

{% hint style="warning" %}
* Mutation of property and change of ownership details
* Capture Extension/ Addition and Alteration and reassessment based on changed property details
* Bifurcation of property 
* Amalgamation of property
{% endhint %}

### Generate Demand Notice

System has the capability to automatically generate demand notice for a financial year based on set triggers like time-based roll over on completion of a financial year. The system notifies the citizens about the demand through SMS/Email. The generated Bills can also be grouped and printed for physical distribution by the ULB employees. The system provides the capability to Employees to merge and download bills based on given parameters to plan their distribution drives.

{% hint style="warning" %}
* Generate Demand Notice based on periodic basis
* Group Demand Notices
* Print Demand Notices
* Cancel Demand Notices
* Send notifications to citizens on demand generation- SMS, Whatsapp, Email, Physical bil
{% endhint %}

### Payments collection and Receipts

The citizen/ employee can view payment status of previous assessments from Assessment History section. Payment for any assessment with full or partially paid amount can be completed. Receipts for assessment can be downloaded in Assessment history section after searching for the property details.

{% hint style="warning" %}
* Payment of Property Tax -Online, Cheque, Cash, DD, during assessment
* Partial Payment of Property Tax -Online, Cheque, Cash, DD, during assessment
* The system allows a citizen to pay for anyone's property without changing the demand
* The system can also be integrated with PoS machines to enable doorstep collection of property tax and issual of receipt
{% endhint %}

### Reports and Dashboards

PT reports provides facility to access receipt register, cancelled receipt register, account receipt register, ULB wise PT collection report, DCB Register. All reports can be downloaded in PDF/XLS format.State level administrator can monitor property tax collections, assessments and other information at a state level through dashboards.

{% hint style="warning" %}
* State Dashboard : View Reports for Total Collections, Properties Assessed, ULBs on Prod, Usage Type, Payment Distribution
* State Dashboard : PT Collection Timeline \(Monthly,Weekly\)
* State Dashboard : ULB Wise \(Collection, Assessments\)
* Cancelled Receipt Register Report
* PT Collection Report \(ULB/Date Wise\)
{% endhint %}

### General Features

{% hint style="warning" %}
**Notifications -** The system has the capability to send notifications to citizens. These notifications can be sent for various steps like - assessment completion, payment reminder, payment confirmation. These notifications can be sent in the language chosen by the ULB through all channels - SMS, Whatsapp, Email.

**Legacy Data Migration -** The system has the capability to migrate Demand and Collection. In most states, the preliminary step would be to migrate Legacy data of existing properties/connections along with the Demand and Collection details. This would ensure that subsequent demand generation happens through the system.

**Configurable Masters** - The system provides the following masters that can be configured as per the State’s

**Requirements -**

* Charges & Calculation : Calculation Engine, Rebate, Penalty, 
* Rate Master
* State Masters : Property Ontology, Documents List, Employee Data Mapping, Boundary Data Mapping
{% endhint %}

System specification in compliance with the Ease of Doing Business \(EODB\) BRAP 2019

<table>
  <thead>
    <tr>
      <th style="text-align:left">Reform No.</th>
      <th style="text-align:left">Reform Area</th>
      <th style="text-align:left">Weightage (score)</th>
      <th style="text-align:left">Recommendation</th>
      <th style="text-align:left">Remarks</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">7</td>
      <td style="text-align:left">Land administration and Transfer of Land and Property</td>
      <td style="text-align:left">3</td>
      <td style="text-align:left">
        <p>Digitize land transaction deeds of last 10 years at all sub-registrar
          offices and make the same available on an online system to check for ownership
          details and history. The metadata should be searchable for each record
          and a soft copy of the registered deed should be available. The searchable
          metadata available should be:</p>
        <p>i. Name of buyer</p>
        <p>ii. Name of seller</p>
        <p>iii. Survey no.</p>
        <p>iv. Registration number</p>
        <p>v. Registration date</p>
      </td>
      <td style="text-align:left">The feature of &#x2018;Property Registry&#x2019; in the product will enable
        this recommendation</td>
    </tr>
    <tr>
      <td style="text-align:left">8</td>
      <td style="text-align:left">Land administration and Transfer of Land and Property</td>
      <td style="text-align:left">3</td>
      <td style="text-align:left">
        <p>Digitize and publish the updated Record of Rights (ROR) at all Revenue
          department offices online in public domain for all areas of the State/UT.
          The searchable metadata available should be:</p>
        <p>i. Name of buyer</p>
        <p>ii. Name of seller</p>
        <p>iii. Date of mutation</p>
        <p>iv. Survey no.</p>
      </td>
      <td style="text-align:left">The Property tax system enables this capability</td>
    </tr>
    <tr>
      <td style="text-align:left">9</td>
      <td style="text-align:left">Land administration and Transfer of Land and Property</td>
      <td style="text-align:left">2</td>
      <td style="text-align:left">
        <p>Digitize and publish data of Property Tax payment dues online in public
          domain for all the Urban Local Bodies (ULBs) in the State/UT. The searchable
          metadata available should be:</p>
        <p>i. Name of the Property Tax payer</p>
        <p>ii. Property Tax dues</p>
        <p>iii. Survey no. of land / Unique Identification no. of property</p>
      </td>
      <td style="text-align:left">This feature is enabled by the citizens itself</td>
    </tr>
    <tr>
      <td style="text-align:left">10</td>
      <td style="text-align:left">Land administration and Transfer of Land and Property</td>
      <td style="text-align:left">2</td>
      <td style="text-align:left">Digitize cadastral maps of all rural areas in the State/UT and make them
        available in public domain</td>
      <td style="text-align:left">This can be enabled and worked on by the state team</td>
    </tr>
    <tr>
      <td style="text-align:left">11</td>
      <td style="text-align:left">Land administration and Transfer of Land and Property</td>
      <td style="text-align:left">5</td>
      <td style="text-align:left">
        <p>Integrate the below-mentioned records on one website:</p>
        <p>i. Data of land transaction deeds for last 10 years at all sub-registrar
          offices (Name of buyer, Name of seller, Registration number, Registration
          date, Survey no.),</p>
        <p>ii. Updated Record of Rights at all Revenue department offices (Date of
          mutation), and</p>
        <p>iii. Data of Property Tax payment dues at all urban areas of the State/UT
          (Name of the Property Tax payer, Property Tax dues)</p>
        <p>iv. Revenue Court case data (Court case number, Name of parties involved,
          Date of filing of court case, Status of case [Ongoing/Resolved])</p>
        <p>v. Civil Court case data (Court case number, Name of parties involved,
          Date of filing of court case, Status of case [Ongoing/Resolved])
          <br />
        </p>
        <p>The website should be publicly accessible. It will help in establishing
          property ownership and identify tax encumbrances. The integration should
          be done for all areas of the State/UT.</p>
      </td>
      <td style="text-align:left">The integration with external portals and systems of other departments
        can be enabled by state teams who can enhance the offered product to cater
        to this recommendation</td>
    </tr>
    <tr>
      <td style="text-align:left">12</td>
      <td style="text-align:left">Land administration and Transfer of Land and Property</td>
      <td style="text-align:left">2</td>
      <td style="text-align:left">
        <p>Implement an online application system having the following features</p>
        <p>i. Mandatory Online application submission including submission of draft
          deed and other documents</p>
        <p>ii. Provision of online payment of Stamp duty and Registration fee</p>
        <p>iii. Auto generation of appointment date and time on making the payment
          of Stamp duty and Registration fee</p>
      </td>
      <td style="text-align:left">The system will provide these capabilities which can be customised as
        per the state specific rules and regulations</td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">13</td>
      <td style="text-align:left">Land administration and Transfer of Land and Property</td>
      <td style="text-align:left">1</td>
      <td style="text-align:left">Provide model deed templates for sale, gift, lease, mortgage and rent
        in downloadable and editable format along with instructions to use them</td>
      <td
      style="text-align:left">This provision is made available through the ULB portal to make these
        features accessible to the citizens</td>
    </tr>
    <tr>
      <td style="text-align:left">14</td>
      <td style="text-align:left">Land administration and Transfer of Land and Property</td>
      <td style="text-align:left">2</td>
      <td style="text-align:left">
        <p>Integrate the mutation process with the registration process and mandate
          initiation of mutation process (Revenue department and/ or ULB) as soon
          as the deed is registered. Ensure that:</p>
        <p>i. Information to mutation authority to be automatically shared on completion
          of transaction (registration). This should be considered as initiation
          of mutation process.</p>
        <p>ii. No separate application from transferee to be required.</p>
        <p>iii. SMS/email should be sent to transferee/ transferor to inform about
          the initiation of mutation</p>
      </td>
      <td style="text-align:left">The integration with external portals and systems of other departments
        can be enabled by state teams who can enhance the offered product to cater
        to this recommendation</td>
    </tr>
  </tbody>
</table>

**List of Features- Property Tax**

| List of Functionalities | Corresponding Features |
| :--- | :--- |
| Registration, Login, Creation of User Profile | Provision for Language Selection during first time registration via Mobile/ Web App. |
| OTP Based Login for Citizen/ Employee via Mobile/ Web App |  |
| Login Credentials for various hierarchy of employees. |  |
| Provision of Personalized Profile for Citizen/ Employee on Web App |  |
| Filing an assessment for a property | Citizen/CSC : Assess New Property \(By Different Financial Years\). |
| Citizen/CSC : Capture Address, Assessment Info, Owner Info. |  |
| Citizen/CSC : View/Print Summary of Filled Form |  |
| Searching for a property | Citizen/CSC : Search Property \(By Mobile No,City, Property Tax Unique ID, Existing ID\). |
| Citizen/CSC : View the Searched Property |  |
| Citizen : View My Properties |  |
| Citizen : View Incomplete Assessments |  |
| Citizen/CSC : Edit the Searched Property |  |
| Citizen/CSC : Reassess Searched Property |  |
| Generate demand notice | Generate Demand Notice based on periodic basis |
| Group/ Print/ Cancel Demand Notices |  |
| Send notifications to citizens on demand generation- SMS, Whatsapp, Email, Physical bill |  |
| Modifications to a property | Mutation of property and change of ownership details |
| Capture Extension/ Addition and Alteration and reassessment based on changed property details |  |
| Bifurcation/ Amalgamation of property |  |
| Payment collection and receipts | Payment of TAX \(Online,Cheque,Cash,DD\) : During Assessment |
| Payment of TAX \(Online,Cheque,Cash,DD\) : Partial Payment |  |
| Citizen/CSC : Download Receipts for payments |  |
| Dashboards and reports | State Dashboard : View Reports for Total Collections, Properties Assessed, ULBs on Prod, Usage Type, Payment Distribution |
| State Dashboard : PT Collection Timeline \(Monthly,Weekly\) |  |
| State Dashboard : ULB Wise \(Collection, Assessments\) |  |
| Cancelled Receipt Register Report |  |
| PT Collection Report \(ULB/Date Wise\) |  |
| General features | Notification |
| Legacy data migration |  |
| System assigns a unique property ID based on the Process defined in the ULBs. |  |
| System has the facility to classify the property based on its type. |  |
| System allows changing the type of property. |  |
| Configuration masters | Configurable Rate Master \(ULB Specific\) : Fire Cess/ Building Height |
| Charges & Calculation : Calculation Engine, Rebate, Penalty |  |
| State Masters : Property Ontology, Documents List, Employee Data Mapping, Boundary Data Mapping |  |

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation ](https://egov.org.in/)is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).

