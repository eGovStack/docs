---
description: Functional overview for stakeholders
---

# W&S Module Functional Specifications

## Introduction

The Water and Sewerage \(W&S\) module provides a digital interface to apply for water and sewerage connections and, pay the water and sewerage charges for connection/s. It can be used by the citizens, Urban Local Body \(ULB\) counter employees and field employees, and ULB Administrators to accomplish their specific tasks. It is available as a mobile and web-based application.

## Functional Scope

The Water and Sewerage product features can be broadly classified as the following modules:

1. Registration, Login and Creation of User Profile
2. Applying for a new Water/Sewerage connection
3. Searching for a Connection
4. Modifications to a Connection
5. Entering meter reading of metered connections
6. Generate Demand
7. Payment collection and Receipts
8. Closure of water connection
9. Dashboards and Reports

### Registration, Login and Creation of User Profile

{% hint style="warning" %}
This module provides enables the following capabilities

* OTP Based Login for Citizen via Web/Mobile App
* OTP Based Login for Employee via Web/Mobile App
* Provision for language selection during first time registration for both Employee and citizens
* Provision of creating a personalized Profile for Citizens and employees on Web App
* Login Credentials for the various hierarchy of employees
* Role-based access for performing different actions relating to the W&S module
{% endhint %}

### Application for new Water/Sewerage connection

The system allows the Citizen / ULB user \(with an appropriate role in the system\) to apply for a New Water/Sewerage connection. The application goes through an approval workflow before it is available for various transactions in the system. The workflow to be followed for a new water/sewerage connection is configurable. In the workflow, the ULB official will generate the estimation notice. Once the payment is made, a work order will be generated.

Every time there is a change in the status of an application, the citizen will be intimated through in-app notifications, SMS and email. The citizen and employee can view the history of the various states that an application has been in and the comments added by the employee in each state of the application.

### Searching for a Connection

The employee from the W&S department will be able to access the feature, to search for water and sewerage connections. They can search for any connection based on parameters such as:

* Consumer number
* Application number
* Owner mobile number
* Application status
* From date
* To date

The search result contains, Application number, Consumer number, Owner name, Status, Due amount and Pay now option. The Employee can make payment for a connection on the citizen’s behalf using the ‘Pay Now’ option.

Citizens can also search for their connection in the portal. They can search using the Owners mobile number, Property ID, Consumer number etc. The search result yields, Owner’s Name, Address, Due amount and Pay option.

### Modifications to a Connection

The system facilitates the title transfer of water tap connection from one person to the other person. Title transfer of water tap connection directly depends upon Property tax. If title transfer is done in the property tax module then at the time of final approval, the changes will reflect in the W&S module automatically. After the title transfer has been completed successfully, subsequent bills will be generated with the details of the new owner/s.

Water tap change in usage happens when property type is changed from residential to Non-residential or from Non-residential to residential. Change in usage directly depends on the property tax module. If the property type is changed in the Property tax system then it will automatically reflect in the W&S system. When there is a change in the usage type, the subsequent bills will reflect the rates as per the updated usage category. When there is a change in the usage category in the middle of the billing cycle, pro-rata charges will be applied in the next billing period.

The change in connection category from non-metered to metered and vice-versa is also possible in the W&S system with the appropriate workflow configured to intimate all stakeholders of the change and collect any charges \(if applicable\) from the citizen.

### Entering meter reading of metered connections

On the W&S billing screen, there is a card called ‘Meter reading’. An employee can click on ‘Meter reading’ which redirects the employee to the meter reading landing screen. The employee can search based on the following criteria:

* ULB
* Boundary Type
* Boundary Value
* Billing Year
* Billing Period
* Billing Period Value
* Consumer No.

This feature facilitates the employee to search for all results based on desired criteria. The search result yields the following values: consumer number, owner name, meter status, last reading, current reading, date and consumption.

The employee can edit meter status, current reading, date and consumption under certain conditions. Based on this information the employee can generate the bills for connections.

### Generate Demand

In the system, there is a feature to generate demand under the billing section. Generate demand has a search feature in which, the connections can be searched for which demand has been already generated. An employee can view, also edit those demands based on certain conditions.

The system has the capability to configure the demand generation as an automatic or a manual process. In the automatic process, the demand generation for non-metered connections is automatically done periodically. For metered connection as soon as the employee enters the meter reading and clicks on ‘SAVE’, the demand is generated.

Any success/ failure to generate demand triggers an automatic notification to the concerned ULB officials via email. Also, the demand generation cycle, demand generation date and officials who should receive the notifications can be configured.

### Payments collection and Receipts

The citizen can pay for dues by searching his/her connection. In search results, the citizen can click on pay, which redirects to the summary page of the dues. After this, the citizen can pay for dues online. An employee can also collect the payment on the citizen’s behalf. After searching for the desired connection, clicking on pay will redirect the employee to the common payment page. The employee can print the receipt after the payment is successfully collected. The citizen is also notified and gets a download receipt link in the notification.

### Closure of Water Connection

If the Water tap owner has got his own water source then the water tap owner can initiate for Water tap connection closure permanently. So, that tap will be closed permanently and demand would not be generated for the connection. Application for the closing of water tap connection is accepted only with the latest water charges receipt and clearing of old dues.

### Dashboards and Reports

The state-level administrator can keep track of relevant metrics by using dashboards. Dashboards for W&S can be accessed by a state-level user under login. The dashboard has these components:

* Financial Indicators
  * W&S Total collections YTD
  * Water Collection
  * Sewerage Collection
  * Water - Demand vs Collection \(Monthly trend\)
  * Sewerage - Demand vs Collection \(Monthly trend\)
* Municipal Adoption
  * W & S : No. Of ULBs Live
  * W & S: Total Number of ULBs
  * Water Consumers by Connection Type
  * W & S Consumers by Usage Type
  * Total Collections by Source
  * Total Collections by Mode
  * W & S Adoption : ULB Wise
* Today’s Collections
  * W&S Total collections: Today
  * Water Charges - Total collections: Today
  * Sewerage Charges - Total collections: Today
  * W&S - Total No. of Receipts: Today
  * Water - Total No. of Receipts: Today
  * Sewerage - Total No. of Receipts: Today
  * Mode wise W&S collections: Today
  * W&S ULB wise collections: Today

The table below lists the functionalities supported by the offered product as per the recommendations under the guidelines mentioned under the Ease of Doing Business \(EODB\) guidelines of 2019.

<table>
  <thead>
    <tr>
      <th style="text-align:left">Reform Area</th>
      <th style="text-align:left">Weightage (score)</th>
      <th style="text-align:left">Recommendation</th>
      <th style="text-align:left">Remarks</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Obtaining Utility Permits</td>
      <td style="text-align:left">1</td>
      <td style="text-align:left">Obtaining Water Connection</td>
      <td style="text-align:left">
        <p>Implement an online application system with the following features:</p>
        <p>i. Online submission of application without the need to submit a physical
          copy of the application</p>
        <p>ii. Eliminate physical touchpoint for document submission</p>
        <p>iii. Allow the option of online payment of application fee</p>
        <p>iv. Allow the applicant to track the status of the application online</p>
        <p>( Available in DIGIT Platform)</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Obtaining Utility Permits</td>
      <td style="text-align:left">1</td>
      <td style="text-align:left">Obtaining Water Connection</td>
      <td style="text-align:left">
        <p>Display information on tariffs (in Rs. per kL) and notify customers of
          the change in tariff ahead of the billing cycle (for commercial and industrial
          users)</p>
        <p>( Available in DIGIT Platform)</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Obtaining Utility Permits</td>
      <td style="text-align:left">1</td>
      <td style="text-align:left">Obtaining Water Connection</td>
      <td style="text-align:left">
        <p>Allow users to pay water bills online</p>
        <p>( Available in DIGIT Platform)</p>
      </td>
    </tr>
  </tbody>
</table>

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation ](https://egov.org.in/)is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).

