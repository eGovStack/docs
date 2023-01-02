# Property Amalgamation

## Introduction

**What does amalgamation of properties mean?**

Two or more than two adjacent properties of an owner(s) are merged to form a single property. On merging of properties, merged properties are removed from the assessment registers while the retaining property is modified to add the merged property(ies) dimensions. The retaining and merged properties relationship is maintained for future reference. The combination of properties for which amalgamation can be done are given below.&#x20;

* Building + Building&#x20;
* Building + Vacant Land&#x20;
* Vacant Land + Vacant Land

**How is the amalgamation of properties accomplished on the ground?**

The amalgamation is considered a service and the owner(s) has to apply for it. A single application is created for the amalgamation of properties with details of all the properties and the required documents are produced in support of the application. There is no application/ processing fee associated with the amalgamation of properties.

## Key Metrics&#x20;

Below are state-wise approximate figures of amalgamation applications received and processed in a year.

|                   |                                                          |      |
| ----------------- | -------------------------------------------------------- | ---- |
| Andhra Pradesh    | \[On basis of data available in the property tax system] | 453  |
| Punjab            | \[On the basis of application received manually]         | 3000 |
| Uttarakhand       | \[On the basis of application received manually]         | 1500 |
| Cantonment Boards | \[On the basis of application received manually]         | 1000 |
| Odisha            | \[On the basis of application received manually]         | NA   |

## Proposed Solution&#x20;

**How to achieve this with the DIGIT Platform?**

1. A new application type ‘AMALGAMATION’ is created.&#x20;
2. Application no. format is defined.&#x20;
3. Only one application is created and the record of the same is maintained. All the properties involved in amalgamation are linked to that application.&#x20;
4. Workflow components are integrated and the wf status of retaining and merge properties are maintained as ‘In Workflow’ while the application is in flow.&#x20;
5. Though there are no instances observed where the application fee is charged for amalgamation, the applicability of the application fee is to be made configurable.&#x20;
6. The uniqueness of the owner (Individual) is identified based on the below-given attributes.&#x20;
   * Owner’s Name&#x20;
   * Owner’s Gender&#x20;
   * Owner’s Guardian Name&#x20;
   * Relationship with Guardian&#x20;
7. The uniqueness of the owner (Institutional) is identified based on the below-given attributes.&#x20;
   * Institute Name&#x20;
   * Institute Type&#x20;
   * Authorised Person Name&#x20;
8. No final document is generated as proof of amalgamation.&#x20;
9. Applicant(s) is/are intimated through SMS/ email notifications about the status and completion of the application.&#x20;
10. Any integration impact to be handled.&#x20;
    * Water and sewerage connection with merging properties to be moved to retaining property or to be brought to closure.&#x20;
    * Trade licenses associated with merging properties are to be moved to retaining property or to be brought to closure.&#x20;
11. Modules linked with property tax have to expose the API to check the status of applications in respective modules associated with a property.

## **Validations**

1. All the properties should be active properties, INACTIVE and WORKFLOW properties are not eligible for amalgamation.&#x20;
2. There should be any application in flow for other services as well linked with a merging property. E.g. Water Connection, Sewerage Connection, and Trade License.&#x20;
3. The owner (s) of the retaining property should always be a superset of the owner(s) of the merging property. It means there should not be a case where any owner of the merging property(ies) is not the one from the owners of the retaining property.&#x20;
4. There should not be any due on the properties which are to be merged while there is no such condition for retaining property.&#x20;
5. Dues related to water and sewerage charges for the connections associated with merging properties are not taken care here.&#x20;
6. The total land area of retaining property = Land area of retaining + Total land area of properties to be merged.&#x20;
7. The total built-up area of retaining property = Built-up area of retaining + Total built-up area of properties to be merged.&#x20;
8. Properties to be merged are deactivated on completion of the process while retaining property remains active.&#x20;
9. Amalgamation will be effective from the date of approval of the application.

## Integrations Impacts&#x20;

### Water and Sewerage

1. There should not be an application related to water connection linked with a merging property in the workflow.&#x20;
2. In the case of water and sewerage connections associated with merging property to be moved to retaining property, it has to be achieved in the WnS module itself by modifying the connection.&#x20;
3. In the case of water and sewerage connections associated with merging property to be closed, it has to be achieved in the WnS module itself by using closure connection activity.

### Trade Licenses

1. In the case of trade licenses associated with merging properties to be moved to retaining property, it has to be achieved in the TL module itself on renewal of trade.&#x20;
2. In the case of trade licenses associated with merging properties to be closed, it has to be achieved in the TL module itself by using the closure of trade features.

### Accounting and Finance&#x20;

Accounting entries are passed for these transactions in terms of demand modifications.

## **User Persona**

| As a \<Role>            | I want \<What>                                        | So that \<Why>                                                                       |
| ----------------------- | ----------------------------------------------------- | ------------------------------------------------------------------------------------ |
| **Employee/Citizen**    | Search a property by unique property ID               | I can create an application for amalgamation of property(ies)                        |
| **Employee/Citizen**    | Search a property by owner’s mobile no.               | I can create an application for amalgamation of property(ies)                        |
| **Employee/Citizen**    | Search a property by owner’s name or by door no.      | I can create an application for amalgamation of property(ies)                        |
| **Employee/Citizen**    | Initiate new application for properties amalgamation  | I can merge adjunct property(ies) into main property.                                |
| **Citizen**             | Notification for my property amalgamation application | I can keep track of my application (notification sent will be according to workflow) |
| **Employee (Workflow)** | Amalgamation application in my inbox                  | I can take appropriate action on the application.                                    |
| **Employee**            | Search application                                    | I can see the application details.                                                   |
| **Citizen**             | My Applications                                       | I can see the application details to keep track of the application.                  |

## Navigation&#x20;

**Employee**&#x20;

Login → Search Property → View Property Details → Select ‘Amalgamation’ Action

**Citizen**&#x20;

Login → Amalgamation Menu → Search Property → Search Result → Select Property.

**Application No. Format**&#x20;

Application No. should follow the given format. PT-\<running sequence>

**User Flow**

Citizen/ Counter Employee - Application is initiated by citizen/ counter employee.&#x20;

Document Verification - The application and documents attached to it are verified by a document verifier.&#x20;

Field Inspection - The field inspector performs the field visit for the physical verification of properties.&#x20;

Approval of Application - The application is approved by the approver and the changes requested in the application come into effect in case the application fee is not applicable.&#x20;

Payment of application fee - In the case the application fee is applicable, the changes related to amalgamation come into effect only after the payment of the application fee.

<figure><img src="https://lh3.googleusercontent.com/oy3TvG3p1PipSVIAN3iOiySNLfaNeVkP9BZqKDU1HYXc1NDIQN-frLrBm-cwh1HE_xiIz00LAJhCH2rggRmdGrQRIWDehZ1ZAjLj6YTKeLJeNSPhx9q4KIv5F1-tF1erJ3XvHpBtw22LGE9zORReMqyo0SgHervq3VTrV12QndPsq71AKXegg2AH" alt=""><figcaption></figcaption></figure>

### **Application Form**

| Field Name                            | Data Type   | Is Mandatory? | Description                                                                               |
| ------------------------------------- | ----------- | ------------- | ----------------------------------------------------------------------------------------- |
| **Property Address**                  |             |               |                                                                                           |
| Pincode                               | Display     | Yes           | Pincode of area property is located.                                                      |
| City                                  | Display     | Yes           | City name of the property.                                                                |
| Locality/Mohalla                      | Display     | Yes           | Locality or mohalla name property is located.                                             |
| Street Name                           | Display     | Yes           | Street name property is located.                                                          |
| Door No./House No.                    | Display     | Yes           | House or door no. of the property.                                                        |
| **Ownership Details**                 |             |               |                                                                                           |
| Ownership Type                        | Display     | Yes           | Display of ownership type.                                                                |
| Institution Name                      | Display     | Yes           | It is applicable for the ownership type institution.                                      |
| Institution Type                      | Display     | Yes           | It is applicable for the ownership type institution.                                      |
| Name                                  | Display     | Yes           | Name of the owner of property or the authorised person in case of institutional property. |
| Guardian Name                         | Display     | Yes           | Name of guardian and applicable for single and multiple ownership type only.              |
| Gender                                | Display     | Yes           | Gender of owner/authorised person of the property.                                        |
| Landline No.                          | Display     | Yes           | Office landline no. in case of institutional ownership.                                   |
| Mobile No.                            | Display     | Yes           | Mobile no. of the owner/ authorised person.                                               |
| Designation                           | Display     | Yes           | Designation of the authorised person                                                      |
| Email                                 | Display     | Yes           | Email address of owner/ authorised person.                                                |
| Corresponding Address                 | Display     | Yes           | Corresponding address of the owner/ authorised person.                                    |
| **Merge Propertie(s)**                |             |               |                                                                                           |
| Property ID                           | Textbox     | Yes           | To search and add the property. A button with the label ‘Search and Add’.                 |
| Search Property                       | Hyperlink   | Yes           | To search the property by other params too and add it to the application.                 |
| **Property 1**                        |             |               |                                                                                           |
| Property ID                           | Display     | Yes           | Unique Property ID.                                                                       |
| Property Address                      | Display     | Yes           | Full address of property.                                                                 |
| Property Owners                       | Display     | Yes           | Comma separated list of property owners.                                                  |
| View Property Details/Remove Property | Hyperlink   | Yes           | To view the completed property details/ remove the added property.                        |
| **Assessment Details**                |             |               |                                                                                           |
| Property Type                         | Drop-down   | Yes           | Type of property                                                                          |
| Property Usage                        | Drop-down   | Yes           | Usage of property, residential, non-residential, or mixed.                                |
| Plot Size (In Sq Ft)                  | Textbox     | Yes           | Total area of land in square feet on which the property is constructed.                   |
| **Unit 1**                            |             |               |                                                                                           |
| Floor No.                             | Drop-down   | Yes           | Floor no. unit is located.                                                                |
| Usage                                 | Drop-down   | Yes           | Usage of unit, residential/ non-residential.                                              |
| Sub-Usage                             | Drop-down   | Yes           | Sub-usage of unit, mandatory in case of non-residential usage.                            |
| Occupancy                             | Drop-down   | Yes           | The type of occupancy of property.                                                        |
| Annual Rent                           | Textbox     | Yes           | Annual rent in INR, in case property is rented out.                                       |
| Built-up Area                         | Textbox     | Yes           | Built-up area of the unit in square feet.                                                 |
| Documents                             | File Picker | Yes           | The documents required to process the request.                                            |
| Timelines                             | Workflow    | Yes           | Display of workflow steps completed.                                                      |

### **Workflow**

| Action               | Role                       | From State                        | To State                          |
| -------------------- | -------------------------- | --------------------------------- | --------------------------------- |
| Initiate Application | Citizen/ Counter Employee  |                                   | Initiated                         |
| Submit Application   | Citizen/ Counter Employee  | Initiated                         | Pending for document verification |
| Verify and Forward   | Document Verifier          | Pending for document verification | Pending for field inspection      |
| Verify and Forward   | Field Inspector            | Pending for field inspection      | Pending approval for amalgamation |
| Send Back            | Document Verifier          | Pending for document verification | Pending for citizen action        |
| Send Back            | Field Inspector            | Pending for field inspection      | Pending for document verification |
| Send Back            | Approver                   | Pending approval for amalgamation | Pending for field inspection      |
| Send Back To Citizen | **\<roles having access>** | **\<Current Status>**             | Pending for citizen action        |
| Re-submit            | Citizen/ Counter Employee  | Pending for citizen action        | Pending for document verification |
| Re-submit            | Document Verifier          | Pending for document verification | Pending for field inspection      |
| Re-submit            | Field Inspector            | Pending for field inspection      | Pending approval for amalgamation |
| Approve              | Approver                   | Pending approval for amalgamation | Approved                          |
| Reject               | **\<roles having access>** | **\<Current Status>**             | Rejected                          |

### Wireframes&#x20;

Please click here to see the wireframes in Figma.&#x20;

Screenshots are attached below.&#x20;

### Citizen (Mobile First)

Apply for amalgamation

<figure><img src="https://lh3.googleusercontent.com/0jzNmIFgc7FVp2nsj9Q9x1l0oGf4v69Dq-KXi8E1kUPSHBgJ_F__WDk-Vwkq2U8xD0bqnBU_JNgzG4-atOUwWC-xXytceIcvflTm5ksgiFOPknRFy1oULk4FjT5A4vSN04HFtwdSBxKqNWX-gbiMUZmtjvcz1ad4eDjnOXehL-OWDqEU9H_fzww3" alt=""><figcaption></figcaption></figure>

Login into the account (If not already logged in)

<figure><img src="https://lh6.googleusercontent.com/QV1L39b9GfaVS4WtrhhDwMVWUCrevzlmcy8nX0URJiZGKS0uFLUn5f30FTw7qJtyyLV2ayGeePJfg_EsAeym-7-oqYNxPeJZ-aOFrK5cKCeVp9ovTN7ukpmbEfXGvbhvaOTkZSCZB8PDvTANZRNsdFGUlPU13rH6wKuq62SAxs4ICBClXGnGmYFK" alt=""><figcaption></figcaption></figure>

Select retaining the property for amalgamation&#x20;

The user will be displayed all the properties currently linked with the logged-in account and allowed to select one of them as retaining property.

<figure><img src="https://lh6.googleusercontent.com/riDcvqtsOTeabYcx-wKrEhAAdo0J5jZEEf7eOxtk0m3u8aoeK2CIo7_tj_qvlVBDoFGfw8OPy1g4fMVdK8-MQSEkivwWJBM4LOpDTHqR5wq15SBlmu873c3InUiceVH2gWD6MOxleLyne6NCzqBOMHQwfjVddAI8kCd2njec_7xC082lq3E4oSbJ" alt=""><figcaption></figcaption></figure>

The retaining property address and ownership details is displayed on apply

<figure><img src="https://lh6.googleusercontent.com/jn1fjeBY9OSHFGhpO9zNarbf6n747qME_N7sqDEKbnh9PkycgdD2Nu27v3W3uYrzXUY9cf_Vf2H5b0tYZJ8BMjxfseoIvL9DNX1uD9Zww8vlRqyx7msVt1GFCzbf4MxPPo0zsDvuwpvdFOBR-mf5rE5362gpBOeMVvE9TfdTl96GQhEY51fQnnP6" alt=""><figcaption></figcaption></figure>

Select a property to merge&#x20;

The user will be displayed a list of all those properties which are owned by him/ her as a single owner or joint owner and allowed to select a property based on below conditions.&#x20;

* Owner(s) of the merging property should be a subset of the owner(s) of the retaining property.&#x20;
* There should not be any dues on the property.&#x20;
* The property should be active property, **also there should not be any application in flow for an integrated module associated with the property.**&#x20;
* The property should belong to the same locality as the retaining property.

<figure><img src="https://lh4.googleusercontent.com/OAWQsdV70mi2ysrhrfbkPwTyi0KGsd3T2a5mSYMQr4lp3IMEkfKxo1j-sPZvsIrVj_-GU52SRn0s3NUdJ7opt1HpkcgDyO217bfdDYQyYRGuKlaeMAMb3VnEkU4s5IedMTsraV3nf4RxtbTmkMNU5x6Qizv7x5bXQzKiv2PGdE_MZWwe6exJFQ8h" alt=""><figcaption></figcaption></figure>

Modify the assessment details of retaining property&#x20;

* Property Type&#x20;
* Plot Size

<figure><img src="https://lh6.googleusercontent.com/jmU6XVNmdWpt53B1Niacl0C3ubU-YW3pkqgszlt_6GqXF1dajI6NhmMqATuJ9Cen8yLjGnWgwgnhbYQdcQUHVDsDPtwo46safSZftoFi_F5ZdUwd5kKxW2QbTou5_eh999HpgmytFTaCLJkdeMLXla_vhuSZwlAMTw4sJY9eeC1sl44mcpmFmBrz" alt=""><figcaption></figcaption></figure>

* Number of basements&#x20;
* Number of floors

<figure><img src="https://lh5.googleusercontent.com/VMmYj11kDyd3yy5DtJ8wzR-fKM835CuUWK7RctjcekJmjXTyaA700noc3XW06QeLwm2V40OqLhMogyl_PJ5-Zcz7Dv3PQMl0oNPjJe3Mx7PHdi3JoInXlDwwOaMCBRxPCgo4sjcvDrrwLW_u-Wd4VoEc5zxsgthxD6skgDzktmbWwPd9p6FYYIjp" alt=""><figcaption></figcaption></figure>

* Unit details&#x20;
  * Usage&#x20;
  * Sub-usage&#x20;
  * Occupancy&#x20;
  * Built-up Area&#x20;
  * Annual Rental

<figure><img src="https://lh6.googleusercontent.com/PY2mnrg0nIEZXi2gLcmw1wCTZR9WF5XxVXI04Y0cfGI2D2xuOFpmRyvbO9a9koWtM9VTZBleqUxXquXLU7xtqXKOot41jU1d6f3u6zxc81sIh9DnmzeMY9M4hgYaPXLvzdMo6MzbbJNSTfuTccz8eFm98X_iSu73dvHwIlVykWuhsrhvNoQ3YU7N" alt=""><figcaption></figcaption></figure>

In case the property type is ‘Flat’, flat details are modified.

<figure><img src="https://lh4.googleusercontent.com/_RrYR_PGqHZ2mX7QESl60WWkSvFZzQtq7mVzGk2wF2wDsQ2tgqg65HPE_efhAcsQXt0tfOEFznvKFVhWbd86GGwFbW0ND-JzczNNrbZz8ATxLRIfNWyuFXbOacF5eF7Qldxpq-lhh7oGTCtc4NhcaOw9at-DJZ6Vny51jpnBJBjYA_zKgghMWuP1" alt=""><figcaption></figcaption></figure>

In the case property type is vacant land, vacant land details are modified.

<figure><img src="https://lh4.googleusercontent.com/drLwE5wx93-H50p5FJZL8JiPBWugfi2BMPaXWAe4kZwdRLx_qUxyx8mA9z2nKve6bgI-irsjd1Gz0wXOL161Pe9ESW_gqharBIdrff-KiAHpMlbGf8Je_gRDUVy3Qwdmes1xnaoFNrL3nSbKvXqkyivOsumYD9hHZ4Rh8nkQHNVVUNarDhfU4pNO" alt=""><figcaption></figcaption></figure>

Documents attachment and summary of the application

<figure><img src="https://lh6.googleusercontent.com/FzYpT4agDDCHYz6kEkSKBgNZhbr4RcEWHqOOyPUA_lnRIGjxlywNFG-vruOy72SERphC7O2ZYfWLg8-xhYSjvt5c20b4GJ62CV09Pz8a6HULDfmz1WSEOlVFVWJqgxsV6_53N02DsJW-35zkXbrFbzVNe3T7CyX1GN-0pmSzGbhRUk5msbfycY22" alt=""><figcaption></figcaption></figure>

![](https://lh6.googleusercontent.com/pW6c55ZOZphNIbGkcwVgGohSmlUw\_HgD\_oaG9g-MJvJExrweSHzEujw9e9tB8buTvpNe-ty-jpJbHXbqhvu\_piEyKdbT2zITXGdmf7p6LzOS7XUKn3FGzj3WkiVORB5wI8G2GD0vcJ\_IbCXpwwu97L2E3cnhRq4iCmnSpxtFYWHAuLb0Ey42GnwD)![](https://lh4.googleusercontent.com/4Q0N7HEQ9Dg6WOp7G2U56B9btpYvcenHyjlto6ZS2T-5taVxtuSKaWtgz8kX-RVJAtTzt1tkknAi8TrCweZuIPaGX6g4FVkZeU\_FaZpcscifW6xpO5ElPqsvWoYgiPNONK-UwXtYoyrNnYZ9xpBPzZf-cjsNf8eenWI6ZiR7Fiqz7tnb0JHlBcbj)

### Employee&#x20;

**Apply for amalgamation**

Property is searched and property details are viewed.

<figure><img src="https://lh3.googleusercontent.com/cqYFVeFPfPnYyKJ0-TLymhtugjmMFp-S4DN4isYr_Ropx4dSKCAV53YQlQrg3xSfjqXE3Ii5M10zwudsH0j1tEAEywcAJfRBMXnxnXBVQA2k70ePRkwymN_-VeEVcynLYsVJoohive2PZG94648rmPVso1hkV3qfwwCQdfTAmoawYiievmuobRh5" alt=""><figcaption></figcaption></figure>

<figure><img src="https://lh4.googleusercontent.com/wGfKSUJD1PAdJ_CatU1Kbfv0P6pQ5hyj_76oM_A1GdV49wrea0q1ZjNG2AlY6B9rGASG4yDzG2nvMrd-6lFRUT9oP6abDX1r6fEU4O9F--pAE8fsgu75dNVtC8s6QmxFPUmVTBck34RwwUT1EhLIagO5P6c2_787CLx09yZEZcHuaYqeanXvkcSb" alt=""><figcaption></figcaption></figure>

Select the action ‘Amalgamate Property’ from the action list.

<figure><img src="https://lh4.googleusercontent.com/CDOUMjUpBmnWU18L0XW9udd1em52-4BGo8bEqRfGDkrxIKrkXufDJTWHjfF7PQ_BS5y1g9rwsDQK0_rSf1yzFOm_M9-x7lzQf5jqvioBCb4r-7QMKiU3YUiddTEkCqcYETI5DQTjOpxeKa8hWLYaeO7QmcbXRn1gM7l8rUts-n_PmX2KEmIyLs-K" alt=""><figcaption></figcaption></figure>

<figure><img src="https://lh6.googleusercontent.com/iWb2kx1AkttTGYBlA6wESavAhty3w_TYZutrla7mQ_WUZTzZKZvV2d0xGt9vTMoRl5_KEcevE2TK6OJSNxNxWn_wKJ3ynBbYe1PYQ8q1qEb4trPZTCYLEm4AfxPfOgfi6Kw6YQQ5qtiU-AJz0O5oohTXZ1YXs7WjtCfqfIEBR9AptXAa6Urk9ihQ" alt=""><figcaption></figcaption></figure>

<figure><img src="https://lh3.googleusercontent.com/Z_-TKQjz57mezu6HB9hre6roENG5ZEyVp-AMMethYCp17HykMN-urk8We5Y85_OaAs5XMBDV9nTprJHxQ0FDvM7JJ-cc0mBXk-w_7xLteduHZtPpsbA7u18TWQvbKoLw3V7ybID-67SLB0dX5LNOLJtOixGrGC2uI2mp2fZfdbMwKRbRLc715F4W" alt=""><figcaption></figcaption></figure>

<figure><img src="https://lh5.googleusercontent.com/Amr8AgNZIdFbCfE9TeuzJ5Ld0NI2zUMRyEBE5d0nwhXKSE5bgySPvAfwFm5kE04GeU6jF4GyTvxRiAwjm4xjeJIavQBvw1CUf0XITmjHDUgao4etQNYfDes-HHxQAhp7FqjiQ0wYyZXHGFHGQN8EBZbbLuMERSrXS2X4aJNn-5BmFmcNXcsOlyEd" alt=""><figcaption></figcaption></figure>

<figure><img src="https://lh4.googleusercontent.com/RQzGiXVdVqu1NTdFnZlt7Yim6YkiKYKATMOTB0uBJfkQgsYm-sO50pR6cL59USfIyX7x6W5SjhqL0Q1m2CXHrO6Cx7WcBrGDpk2dgWJslOJ5MCbb0WQgXb6pEhx1uwjO4GP8nFa7wFkHtUYiirczmzlREtq3aywRbyyutFxG9c7p0MGo7_H7BD1O" alt=""><figcaption></figcaption></figure>

## Use Case Scenarios&#x20;

**UC 1 - Same Owner’s Residential Properties**

There are two properties A and B, both are residential in nature and belong to the same owner “xyz”.&#x20;

Illustration: Suppose A is the retaining property while B has to be merged with A.&#x20;

* Property A address remains unchanged.&#x20;
* Property A ownership details remain unchanged.

So assessment details of property A are modified according to the assessment details of B. Below given are the activities which can be performed to modify the assessment detail of property A.&#x20;

* The land area of A is increased to include B into A.&#x20;
* One more UNIT is added to A representing B.&#x20;
* An additional floor is added to A representing B.&#x20;
* The existing UNIT area of A is increased.&#x20;
* The existing UNIT rental value of A is increased.&#x20;
* The remaining attributes would remain unchanged. Like Usage, Sub Usage, and Occupancy. Though these also can be edited if required.

Property B is linked with the application which is deactivated on completion.

**UC 2 - Same Owner’s Mixed Properties**

There are two properties A and B, A is residential while B is non-residential and belongs to the same owner “xyz”.

Illustration: Suppose A is the retaining property while B has to be merged with A.

* Property A address remains unchanged.&#x20;
* Property A ownership details remain unchanged.&#x20;
* So assessment details of property A are modified according to the assessment details of B. Below given are the activities which can be performed to modify the assessment detail of property A.
  * The land area of A is increased to include B into A.&#x20;
  * Property usage is changed to Mixed.&#x20;
  * One more UNIT is added to A representing B and UNIT usage and sub-usage is kept according to property B, commercial in this case.&#x20;
  * An additional floor is added to A representing B.&#x20;
  * The existing UNIT area of A is increased.&#x20;
  * The existing UNIT rental value of A is increased.
* Property B is linked with the application which is deactivated on completion.

**UC 3 - Solo Owner Of One Property And Joint Of Others**

There are two properties A and B, “xyz” is the only owner of property A while he/she is the joint owner of property B.&#x20;

Illustration:

* In case, property B is the retaining property, property A is merged according to usage cases #1 and #2.&#x20;
* In case, property A is the retaining property, property B is first mutated in the name of the owners of property A using the mutation process.

**UC 4 - Properties Of Two Different Owners**

There are two properties A and B, the owner of property A is “xyz” while the owner of property B is “def”.&#x20;

Illustration:&#x20;

* In case A is going to be retaining property, property B is to be first mutated in the name of “xyz” using the mutation process.&#x20;
* In case B is going to be retaining property, property A to be first mutated in the name of “def” using the mutation process.&#x20;

There are two properties A and B, the owner of property A is “xyz” which is institutional ownership while the owner of property B is “def” which is individual ownership.&#x20;

* It is a similar case to #4, and the property is to be mutated first to initiate amalgamation.
