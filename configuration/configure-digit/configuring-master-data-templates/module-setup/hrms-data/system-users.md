# System Users

## Introduction

A system user is a person who uses the application service. A user often has a user account and is identified to the system by a username. A user is a person who accesses a particular application to perform a set of actions.

Each user has a certain number of set tasks, the user would be allowed to perform a task by assigning particular roles which are Super Admin, Trade License Approver, Data Entry Admin and Trade License document verifier etc.

## Data Table

| Sl No. | Name\* | Mobile No\* | Father/Husband's Name \* | Gender \* | Date of Birth\* | Email | Correspondence Address \* | ULB\* | Role\* | Employment Type \* | Current Assignment | Status \* | Hierarchy \* | Boundary Type \* | Boundary \* | Assigned from Date\* | Department\* | Designation\* |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | Pooja | 9999999999 | Mr.Bala Chandra | FEMALE | 22/01/1987 | [poojachandra914@gmail.com](mailto:poojachandra914@gmail.com) | Nagar Nigam Haldwani-PIN CODE-263139 | Haldwani | Super User | PERMANENT | Yes | EMPLOYED | REVENUE | City | Haldwani | 05/10/2019 | Revenue | Tax Inspector |
| 2 | M.C. Joshi | 9999999999 | Late Jai Dutt Joshi | MALE | 04/08/1965 | [haldwaninagarnigam@gmail.com](mailto:haldwaninagarnigam@gmail.com) | Nagar Nigam Haldwani | Haridwar | TL Counter Employee | PERMANENT | Yes | EMPLOYED | REVENUE | City | Haldwani | 30/10/2019 | Revenue | Tax Collector |

{% hint style="info" %}
Data given in the table is sample data for reference.
{% endhint %}

## Procedure

### Data Definition

| Sr No | Column Name | Data Type | Data Size | Is Mandatory? | Definition/ Description |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | Name | Text | 256 | Yes | The Name of his/her to whom the access to the system is provided, so he/she can use the application to perform the role function assigned |
| 2 | Mobile Number | Alphanumeric | 10 | Yes | The Mobile number of his/her to whom the access to an application provided. The mobile number is relevant so in an emergency case the person can be contacted |
| 3 | Father/Husband's Name | Text | 256 | Yes | The Name of the Father/Husband of his/her to whom the access to an application provided. This information is for internal records |
| 4 | Gender | Text | 64 | Yes | The Gender of the individual person. This information is for internal records |
| 5 | Date of Birth | Date | 10 | Yes | The Date of birth of the individual person. This information is for internal records |
| 6 | Email | Alphanumeric | 256 | No | The email id of his/her, this email id is linked to receiving all the official communication from the customers and other counterparts |
| 7 | Correspondence Address | Text | 256 | Yes | The address of his/her, this information is saved for internal records |
| 8 | ULB | Text | 256 | Yes | A ULB to be assigned against the individual employee, So that the assigned role can perform his/her duty within that assigned ULB |
| 9 | Role | Text | 256 | Yes | A Role is a permission for users to perform a group of tasks, a role is assigned to the user to perform a function within the application. A user can be assigned multiple roles. Click [User Roles](user-roles.md) for the Role master Data |
| 10 | Employment Type | Text | 256 | Yes | The employment types indicate the type of contract which he/she hold with the organization. This indicates whether he/she is a permanent employee or a contract employee for short period. The employment type “Permanent”, “Temporary”, “DailyWages” and “Contract” either one should be selected |
| 11 | Current Assignment | Text | 64 | Yes | The current assignment type to indicate whether the employee is currently assigned to a particular department and designation. A user can be also be assigned multiple assignments to perform his/her function |
| 12 | Status | Text | 256 | Yes | The Status indicates the type of status which he/she hold, whether employed or not within the organization |
| 13 | Hierarchy | Text | 256 | Yes | The hierarchy indicates the hierarchy type for the Boundary to which he/she is assigned |
| 14 | Boundary Type | Text | 256 | Yes | The boundary type indicates assigning a city to his/her role within the organization. A user can be assigned multiple Boundary Type to perform in different function. \(Example: City, Zone, Block and Locality\) |
| 15 | Boundary | Text | 256 | Yes | The boundary indicates assigning a particular city to his/her role wherein they perform role function of the application for the particular city. A user can be assigned multiple Boundary to perform in a different location \(Example: City Name and Tenant Zone\) |
| 16 | Assigned from Date | Date | 10 | Yes | The assigned from date indicates the date from which his/her role is assigned to perform the role function assigned |
| 17 | Department | Text | 256 | Yes | The Department indicates the particular department to which his/her role is assigned |
| 18 | Designation | Text | 256 | Yes | The designation indicates a particular designation is assigned to his/her role |

### Steps to fill data

1. Download the data template attached to this page.
2. Have it open and go through all the headers and understand the meaning of them by referring 'Data Definition' section.
3. Make sure all the headers, its data type, field size and its definition/ description is understood properly. In case of any doubt, please reach out to the person who has shared this document with you to discuss the same and clear out the doubts.
4. Start filling the data starting from serial no. and complete a record at once. repeat this exercise until the entire data is filled into a template.
5. Verify the data once again by going through the checklist and taking care of each and every point mentioned in the checklist.

## Checklist

The checklist is a set of activities to be performed once the data is filled into a template to ensure data type, size, and format of data is as per the expectation. These activities have been divided into 2 groups as given below.

### Common Checklist

This checklist covers all the activities which are common across the entities.

| Sr. No | Checklist Parameter | Example |
| :--- | :--- | :--- |
| 1 | Make sure that each and every point in this reference list has been taken care of | [Checklist](https://digit-discuss.atlassian.net/wiki/spaces/DO/pages/502203140/Checklist) |

### Entity Specific Checklist

This checklist covers the activities which are specific to the entity.

<table>
  <thead>
    <tr>
      <th style="text-align:left">Sr. No.</th>
      <th style="text-align:left">Activity</th>
      <th style="text-align:left">Example</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">1</td>
      <td style="text-align:left">The Name should not have any special character</td>
      <td style="text-align:left">
        <p>Pooja : [Allowed]</p>
        <p>#Pooja! : [Not allowed]</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">2</td>
      <td style="text-align:left">The date should be in DD/MM/YYYY format</td>
      <td style="text-align:left">
        <p>DD/MM/YYYY : [Allowed]</p>
        <p>YYYY/DD/MM : [Not allowed]</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">3</td>
      <td style="text-align:left">The Email ID should be valid Id, email Id should contain the Company/Firm
        name or an individual personal name before the &#x201C;@&#x201D; and the
        &#x201C;<a href="http://xxxxx.com/">XXXXX.com</a>&#x201D; after the &#x201C;@&#x201D;</td>
      <td
      style="text-align:left"><a href="mailto:ABCLtd@xeror.com">ABCLtd@xeror.com</a>
        </td>
    </tr>
  </tbody>
</table>

## Attachments

{% file src="../../../../../.gitbook/assets/configuration-data-template-system-user.xlsx" caption="Configuration Data Template " %}

{% file src="../../../../../.gitbook/assets/sample-confugration-data-system-user.xlsx" caption="Sample Data " %}

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)​](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation](https://egov.org.in/) is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).

