---
description: Functional overview for stakeholders
---

# PGR Module Functional Specifications

## Introduction

The PGR module is an application that allows citizens to lodge complaints and track them. Employees track and address the grievances registered in the system to ensure speedy resolution. The platform is available for use in both mediums as a web and mobile app.

## Functional Scope

The list below summarizes the key features supported by the PGR module -

1. Registration, Login and Creation of User Profile
2. Lodging a Complaint
3. Assigning a Complaint
4. Resolving a Complaint
5. Manage Complaints
6. Track Complaints
7. Dashboards and Reports
8. General Features

### Registration, Login & Creation of User Profile

{% hint style="warning" %}
Key capabilities offered by this functional component -

* OTP Based Login for Citizen via Web/Mobile App
* OTP Based Login for Employee via Web/Mobile App
* Provision for language selection during first time registration for both Employee and citizens
* Provision of creating a personalized Profile for Citizens and employees on Web App
* Login Credentials for the various hierarchies of employees
* Role-based access for performing different actions relating to grievance redressal
{% endhint %}

### Lodging Complaint

The Citizen or Citizen Service Representative (CSR) on behalf of citizens can lodge, civic works related complaints in the PGR system. Users can also upload associated or relevant pictures with the complaint. For identifying the location of the complaint, the user can provide city, mohalla, house no. and other details or even select the location using maps. After filing the complaint a complaint number is generated.

{% hint style="warning" %}
Key capabilities offered by this functional component -

* Provision for Citizens to Lodge and Track Complaints via Mobile or Web App
* Provision for Employees to Assign, Reassign, Resolve complaints via Mobile or Web App
* The citizen can Upload Photographs
* The citizen can Select grievance from a list
* The citizen can Capture Address
* The citizen can Capture additional details about the complaint
* CSC Employee can File a complaint on behalf of the citizen.
* CSC Employee can Capture Complaint location, medium of complaint, complaint type and other details
* The system provides 2 levels of comprehensive grievance list
* Grievances mapped with departments
* The system generates a unique ticket number for each complaint based on complaint type and the same is communicated to the citizen by SMS, Whatsapp, and/or email.
{% endhint %}

### Assigning Complaint

The assigning officer has a dashboard with unassigned complaints. Any complaint can be selected to view details and expected closure timelines. The assigning officer can select and assign complaints to appropriate Employee from a department-wise list. A complaint can also be re-assigned if it is assigned incorrectly or for any other reason.

{% hint style="warning" %}
Key capabilities offered by this functional component -

* Assigning Officer can Assign grievance to employees
* Assigning Officer can Reject Complaints by providing the Reason for Rejection
* Assigning Officer: Re-assign complaints
{% endhint %}

### Resolving Complaint

The Employee can view the complaints assigned to him on the dashboard with functionality to mark them for closure. An employee can view details and closure timelines of the complaints from a list. After resolving the complaint the Employee can upload pictures as evidence and also enter comments. With the help of the Share feature, complaints details can be shared via Whatsapp, SMS, email etc to contractors. If the citizen finds the resolution to be unsatisfactory, the complaint can be reopened. Citizens can also provide feedback and rate the resolution.

{% hint style="warning" %}
Key capabilities offered by this functional component -

* Last Mile Employee can Add photograph and comments after the resolution
* Last Mile Employee can Request for re-assign of complaints
* Last Mile Employee can interact with assigning Officer over a Call
{% endhint %}

### Managing Complaint

The employee has access to the dashboard of open complaints from which he can select a complaint to view details and closure timelines. An employee can also request to reassign the complaint by selecting a reason from the list. In that case, the request goes to assigning officer and the complaint can be reassigned to a different Employee. The system has different interfaces for Assigning officer, Employee and CSR. The assigning officer can view tabs that contain unassigned and assigned complaints which are received from the citizens. The assigning officer can also view open/ closed complaints and access PGR reports for all grievances. Employee’s interface contains open and closed complaints which are assigned to him. CSR can view/ search the list of all the complaints filed on citizen’s behalf. The system has the provision to search, sort and refresh the list of grievances.

{% hint style="warning" %}
Key capabilities offered by this functional component -

* Assigning Officer can view Complaint Worklist (Inbox)
* Assigning Officer can View a list of all complaints
* Assigning Officer can view Auto prioritization of list based on SLA
* Assigning Officer can Review submitted complaints
* Last Mile Employee can View a list of all complaints
* Last Mile Employee can view Auto prioritization of list based on SLA
* Last Mile Employee can Review submitted complaints
* CSC can Search and view complaints based on complaint number, phone number, name of the complainant
* The citizen can reopen a complaint that has been resolved if he is not satisfied with the resolution
* The citizen can rate a complaint after its resolution
{% endhint %}

### Tracking Complaint

{% hint style="warning" %}
Key capabilities offered by this functional component -

* The citizen can View all complaints filed - pending and completed
* The citizen receives Notifications via App, SMS, email for complaint updates
* Citizens can View the complaint timeline in the app
* Citizens can Interact with the municipality (Call & Comments)
* Assigning Officer can Track Assigned Complaints with a timeline view
* Assigning Officer can Receive updates on complaints
* Assigning Officer can Interact with Last Mile Employee (Call)
{% endhint %}

### Dashboards & Reports

PGR Reports provide an operational bird’s eye view of the PGR system in the city. It enables city managers - commissioners, department heads, administrators at various levels to keep a track of the volume of complaints being received and the performance of the ULB and its employees in addressing them. Reports can be filtered based on date and also can be downloaded in pdf and xls formats.

{% hint style="warning" %}
* **Grievance key statistics:** View dashboards & reports to find Grievance filed, pending, completed and overdue- ULB wise, location wise details
* **SLA performance:** View dashboards & reports to get SLA performance and time taken for resolution details
* **State Dashboard:** Drilldown by Various Levels
* **Reports:** View Reports by State, ULB, Complaint Types, Department
{% endhint %}

### General Features

{% hint style="warning" %}
**Auto routing** - The system has the capability for Auto routing to assigning officer (city/department level) followed by assigning to the last mile employee.

**Auto escalation** - The system has the capability for escalation of non-resolved cases with a defined timeline to the ULB/Concerned head.

**Notifications** - The system has the capability to send notifications to citizens. These notifications can be sent for various steps like - complaint filing, change of status, complaint resolution. These notifications can be sent in the language chosen by the ULB through all channels - SMS, Whatsapp, Email.

**Configurable Masters** - The system provides the following masters that can be configured as per the State’s requirements:

* Assigning Officer: View, edit and update profile
* Assigning Officer: Department wise employee list
* Last Mile Employee: Employee Directory
* Configure assigning officer: Assigning officer can be at ULB / department level
{% endhint %}

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation ](https://egov.org.in/)is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).
