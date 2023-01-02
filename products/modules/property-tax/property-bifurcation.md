# Page 1

## Introduction&#x20;

**What does bifurcation of property mean?**

* A property is divided into two or more parts.&#x20;
* New properties which come into existence are called child properties.&#x20;
* The property that got bifurcated is known as parent property.&#x20;
* The owner(s) of the parent and child properties remain the same.&#x20;
* The relationship of child and parent properties is maintained to track the bifurcation.&#x20;
* Change in ownership of child properties is achieved through the Mutation (Title Transfer) process.&#x20;
* A building property can be divided into.&#x20;
  * Building + Building&#x20;
  * Building + Vacant Land&#x20;
* A vacant land property can be divided into vacant lands only.

**How is the bifurcation of property accomplished on the ground?**

The bifurcation is considered a service and the owner(s) has to apply for it. An application is submitted for a property bifurcation with the required supporting documents. There is no fee associated with the bifurcation of property application.

## Key Metrics&#x20;

Below are state-wise approximate figures of amalgamation applications received and processed in a year.

| State             | On the basis of                                       | No. of applications received/processed |
| ----------------- | ----------------------------------------------------- | -------------------------------------- |
| Andhra Pradesh    | On basis of data available in the property tax system | 1624                                   |
| Punjab            | On the basis of application received manually         |                                        |
| Uttarakhand       | On the basis of application received manually         |                                        |
| Cantonment Boards | On the basis of application received manually         |                                        |
| Orissa            | On the basis of application received manually         |                                        |

## Proposed Solution&#x20;

**How to achieve this with the DIGIT Platform?**

1. A new application type ‘BIFURCATION’ is created.&#x20;
2. The no. of properties resulting due to bifurcation is restricted to five which is configurable and can be changed according to the need of implementations.&#x20;
3. Application no. the format is defined and configured.&#x20;
4. Only one application is created and the record of the same is maintained and the new properties created as a result of bifurcation are linked to that application.&#x20;
5. The workflow component is integrated.&#x20;
6. The status of parent and child properties is maintained as ‘In Workflow’ while the application is in flow.&#x20;
7. On the approval of the application, bifurcation comes into effect and all the properties become active.&#x20;
8. Newly created properties are given a new property ID.&#x20;
9. Though there are no instances where the application fee is charged for bifurcation, the applicability of the application fee is to be made configurable.&#x20;
10. Bifurcation comes into effect from the date of approval of the application.&#x20;
11. No final document is generated as proof of bifurcation.&#x20;
12. Applicant(s) is/are intimated through SMS/ email notifications about the status and completion of the application.&#x20;

**Validations**&#x20;

1. The parent property should be an active property.&#x20;
2. Ownership of all the properties (parent + child) remains the same.&#x20;
3. The total land area of the parent property (before bifurcation) should be equal to the total land area of all the properties (parent + child).&#x20;
4. The total built-up area of the parent property (before bifurcation) should be equal to the total built-up area of all the properties (parent + child).&#x20;
5. All the child properties inherit the ownership from the parent property.&#x20;

## User Persona

| S.No. | As a | \<Role>                          | I want | \<What>                                              | so that | \<Why>                                                                               |
| ----- | ---- | -------------------------------- | ------ | ---------------------------------------------------- | ------- | ------------------------------------------------------------------------------------ |
| 1.    | As a | <p>Employee or</p><p>Citizen</p> | I want | Search a property by unique property ID              | so that | I can create an application for bifurcation of property.                             |
| 2.    | As a | <p>Employee or</p><p>Citizen</p> | I want | Search a property by owner’s mobile no.              | So that | I can create an application for bifurcation of property.                             |
| 3.    | As a | Employee or Citizen              | I want | Search a property by owner’s name or by door no.     | So that | I can create an application for bifurcation of property.                             |
| 3.    | As a | <p>Employee or</p><p>Citizen</p> | I want | Initiate new application for property bifurcation    | So that | I can create an application to bifurcate a property.                                 |
| 4.    | As a | Citizen                          | I want | Notification for my property bifurcation application | So that | I can keep track of my application (notification sent will be according to workflow) |
| 5.    | As a | Employee (Workflow)              | I want | Bifurcation application in my inbox                  | So that | I can take appropriate action on the application.                                    |
| 6.    | As a | Employee                         | I want | Search application                                   | So that | I can search and see the application details.                                        |
| 7.    | As a | Citizen                          | I want | My Applications                                      | So that | I can see the application details and keep track of the application.                 |

## Navigation&#x20;

### Employee&#x20;

Login → Search Property → View Property Details → Select ‘Bifurcate Property’ Action.&#x20;

### Citizen&#x20;

Login → Bifurcate Property → Search Property → Search Result → Select Property.

### Application No. Format&#x20;

Application no. should follow the given format - PT-\<runningsequence>

## User Flow&#x20;

1. Citizen/ Counter Employee - Application is initiated by citizen/ counter employee.&#x20;
2. Document Verification - The application and documents attached to it are verified by a document verifier.&#x20;
3. Field Inspection - The field inspector performs the field visit for the physical verification of properties.&#x20;
4. Approval of application - In the case no application fee is applicable, the application is approved and bifurcation comes into effect with approval.&#x20;
5. Payment of application fee - In the case the application fee is applicable, bifurcation comes into effect only after the payment of the application fee.

<figure><img src="https://lh6.googleusercontent.com/07Nq7dil2cLOgHlD09KYvna-9YtmgFW4T5N8OUksTQXoITaBrXrrUgnA9qy5W_8jElDItoB8ccOzLWaQZqF4GhVvG60Yn_M1cuhXgIYdb6PIKT1foyc3HbmQVZ10AsHR-Adv6nT3_mG5J52mjbrfLXW_XVf9JzbFt5HQNSZm4Zhq7YJzjcpQ8Ng-V7o7" alt=""><figcaption></figcaption></figure>

### Application Form

| Field Name                             | Data Type   | Is Mandatory? | Description                                                                               |
| -------------------------------------- | ----------- | ------------- | ----------------------------------------------------------------------------------------- |
| **Property Address**                   | <p><br></p> | <p><br></p>   | <p><br></p>                                                                               |
| Pincode                                | Display     | Yes           | Pincode of area property is located.                                                      |
| City                                   | Display     | Yes           | City name of the property.                                                                |
| Locality/ Mohalla                      | Display     | Yes           | Locality or mohalla name property is located.                                             |
| Street Name                            | Display     | Yes           | Street name property is located.                                                          |
| Door No./ House No.                    | Display     | Yes           | House or door no. of the property.                                                        |
| **Ownership Details**                  | <p><br></p> | <p><br></p>   | <p><br></p>                                                                               |
| Ownership Type                         | Display     | Yes           | Display of ownership type.                                                                |
| Institution Name                       | Display     | Yes           | It is applicable for the ownership type institution.                                      |
| Institution Type                       | Display     | Yes           | It is applicable for the ownership type institution.                                      |
| Name                                   | Display     | Yes           | Name of the owner of property or the authorized person in case of institutional property. |
| Guardian Name                          | Display     | Yes           | Name of guardian and applicable for single and multiple ownership type only.              |
| Gender                                 | Display     | Yes           | Gender of owner/authorized person of the property.                                        |
| Landline No.                           | Display     | Yes           | Office landline no. in case of institutional ownership.                                   |
| Mobile No.                             | Display     | Yes           | Mobile no. of the owner/ authorized person.                                               |
| Designation                            | Display     | Yes           | Designation of the authorized person                                                      |
| Email                                  | Display     | Yes           | Email address of owner/ authorized person.                                                |
| Corresponding Address                  | Display     | Yes           | Corresponding address of the owner/ authorized person.                                    |
| **Assessment Details**                 | <p><br></p> | <p><br></p>   | <p><br></p>                                                                               |
| Property Type                          | Drop-down   | Yes           | Type of property                                                                          |
| Property Usage                         | Drop-down   | Yes           | Usage of property, residential, non-residential, or mixed.                                |
| Plot Size (In Sq. Ft.)                 | Textbox     | Yes           | Total area of land in square feet on which the property is constructed.                   |
| Unit 1                                 | <p><br></p> | <p><br></p>   | <p><br></p>                                                                               |
| Floor No.                              | Drop-down   | Yes           | Floor no. unit is located.                                                                |
| Usage                                  | Drop-down   | Yes           | Usage of unit, residential/ non-residential.                                              |
| Sub-usage                              | Drop-down   | Yes           | Sub-usage of unit, mandatory in case of non-residential usage.                            |
| Occupancy                              | Drop-down   | Yes           | The type of occupancy of property.                                                        |
| Annual Rent                            | Textbox     | Yes           | Annual rent in INR, in case property is rented out.                                       |
| Built-up Area                          | Textbox     | Yes           | Built-up area of the unit in square feet.                                                 |
| Child Propertie(s)                     | <p><br></p> | <p><br></p>   | <p><br></p>                                                                               |
| Add Child Property                     | Icon        | Yes           | To add child property.                                                                    |
| Property 1                             | <p><br></p> | <p><br></p>   | <p><br></p>                                                                               |
| Property ID                            | Display     | Yes           | Unique Property ID.                                                                       |
| Door/ House No.                        | Display     | Yes           | House no./ Door no. of newly created child property.                                      |
| Property Type                          | Display     | Yes           | Type of property of child property.                                                       |
| Property Usage                         | Display     | Yes           | Usage of child property, residential, non-residential, or mixed.                          |
| Plot Size (In Sq. Ft.)                 | Display     | Yes           | Total area of land in square feet on which the child property is constructed.             |
| No. of floors                          | Display     | Yes           | No. of floors child property is having.                                                   |
| Total Builtup Area (Sq. Ft.)           | Display     | <p><br></p>   | Total built-up area of the child property across all the floors.                          |
| Property 2                             | <p><br></p> | <p><br></p>   | <p><br></p>                                                                               |
| Property ID                            | Display     | Yes           | Unique Property ID.                                                                       |
| Door/ House No.                        | Display     | Yes           | House no./ Door no. of newly created child property.                                      |
| Property Type                          | Display     | Yes           | Type of property of child property.                                                       |
| Property Usage                         | Display     | Yes           | Usage of child property, residential, non-residential, or mixed.                          |
| Plot Size (In Sq. Ft.)                 | Display     | Yes           | Total area of land in square feet on which the child property is constructed.             |
| No. of floors                          | Display     | Yes           | No. of floors child property is having.                                                   |
| Total Builtup Area (Sq. Ft.)           | Display     | <p><br></p>   | Total built-up area of the child property across all the floors.                          |
| View Property Details/ Remove Property | Hyperlink   | Yes           | To view the completed property details/ remove the added property.                        |
| Documents                              | File Picker | Yes           | The documents required to process the request.                                            |
| Timelines                              | Workflow    | Yes           | Display of workflow steps completed.                                                      |

### Child Property Form

| Field Name             | Data Type   | Is Mandatory? | Description                                                             |
| ---------------------- | ----------- | ------------- | ----------------------------------------------------------------------- |
| Property ID            | Display     | Yes           | Unique Property ID.                                                     |
| Door/ House No.        | Display     | Yes           | Full address of property.                                               |
| Assessment Details     | <p><br></p> | <p><br></p>   | <p><br></p>                                                             |
| Property Type          | Drop-down   | Yes           | Type of property                                                        |
| Property Usage         | Drop-down   | Yes           | Usage of property, residential, non-residential, or mixed.              |
| Plot Size (In Sq. Ft.) | Textbox     | Yes           | Total area of land in square feet on which the property is constructed. |
| Unit 1                 | <p><br></p> | <p><br></p>   | <p><br></p>                                                             |
| Floor No.              | Drop-down   | Yes           | Floor no. unit is located.                                              |
| Usage                  | Drop-down   | Yes           | Usage of unit, residential/ non-residential.                            |
| Sub-usage              | Drop-down   | Yes           | Sub-usage of unit, mandatory in case of non-residential usage.          |
| Occupancy              | Drop-down   | Yes           | The type of occupancy of property.                                      |
| Annual Rent            | Textbox     | Yes           | Annual rent in INR, in case property is rented out.                     |
| Built-up Area          | Textbox     | Yes           | Built-up area of the unit in square feet.                               |

### Workflow

| S.No. | Action               | Role                      | From State                        | To State                          |
| ----- | -------------------- | ------------------------- | --------------------------------- | --------------------------------- |
| 1     | Initiate Application | Citizen/ Counter Employee |                                   | Initiated                         |
| 2     | Submit Application   | Citizen/ Counter Employee | Initiated                         | Pending for document verification |
| 3     | Verify and Forward   | Document Verifier         | Pending for document verification | Pending for field inspection      |
| 4     | Verify and Forward   | Field Inspector           | Pending for field inspection      | Pending approval for bifurcation  |
| 5     | Send Back            | Document Verifier         | Pending for document verification | Pending for citizen action        |
| 6     | Send Back            | Field Inspector           | Pending for Field inspection      | Pending for document verification |
| 7     | Send Back            | Approver                  | Pending approval for bifurcation  | Pending for field inspection      |
| 8     | Send Back To Citizen | \<roles having access>    | \<Current Status>                 | Pending for citizen action        |
| 9     | Re-submit            | Citizen/ Counter Employee | Pending for citizen action        | Pending for document verification |
| 10    | Re-submit            | Document Verifier         | Pending for document verification | Pending for field inspection      |
| 11    | Re-submit            | Field Inspector           | Pending for field inspection      | Pending approval for bifurcation  |
| 12    | Approve              | Approver                  | Pending approval for bifurcation  | Approved                          |
| 13    | Reject               | \<roles having access>    | \<Current Status>                 | Rejected                          |

### Wireframes

Figma Link - [https://www.figma.com/file/AXXM9veAvX5IRazkhwbvqF/Digit-Design-System?node-id=38193%3A82388](https://www.figma.com/file/AXXM9veAvX5IRazkhwbvqF/Digit-Design-System?node-id=38193%3A82388)

### Screenshots

<table data-view="cards"><thead><tr><th></th><th></th><th></th></tr></thead><tbody><tr><td>My properties and selecting a property for bifurcation. The property should not be inactive or in the workflow.</td><td><img src="https://lh5.googleusercontent.com/aLDKyE7NUobm08L2X7PQZEWY_ToAGKt_NLUJtG1mhzn25yg39VA4ARmvXBtijW1rOutntp2hKoK16l8bY53RCuwV1pkMm3gO7aVbi-3kNzIdJBD7yyk7Pz8HFiUyqMgWhzc5TrNHRpEvt2EkMC5JyuvUsSX_PqHO4u9nZarZFKPPgP0vfgudyEAKPsatyQ" alt=""></td><td></td></tr><tr><td>Parent property address and ownership details are displayed.</td><td><img src="https://lh3.googleusercontent.com/pG7ZFSxGqDQxQIR12TY-zrrMmffF9dpjlSMxTCi91m2iqLx15SQIf5J5m9BvxyAACCtxsRKg9FGvyXPH2NkCrF40E7Giamsm4iAhd665oXtzUOY7i6qrvM9aWsyNVxCBpvSfqRQtfULZsv7IwAgTHSA8qgyRWteMRcSPdP_kMPqq8dx1im_utRs3PeJLwQ" alt=""></td><td></td></tr><tr><td><p>Parent property assessment details are edited and the flow of screens is according to the property type of the parent property.</p><ol><li>Property Type: Individual Building</li></ol></td><td><img src="https://lh5.googleusercontent.com/HQAIvoLIx7gLlzw1qC7jQD6xDmR1Un4E-TgQYXp2DksurlnUsUL6ia0aHUs7Mh8l7kSfCDi1mAAT3pFrjUeUVJ4tvVzVaPVjg1tj2xNMDLFqE1l9Rq5n4LGTFzbfDGV0yoCGyc2rUoMlI8_jYqoAzX6dp6ZCVIAqsfvcFWrpYB04YyjNZ2SW2zFB1D5GFA" alt=""></td><td><img src="https://lh5.googleusercontent.com/DAM7CcnVndvS7SSeFW6aWoiPAMJ7STv7I7HV0IACGDnY84F234o1wzvY5GPbjGDkP7kGZQv5oHrQyrwad_VRcni1MQ6DpqaelNKfVhNGUc7MpcuDhkiJwp-nSFVbg8s18azFVZ_W7VF1WF7dEEDNN2nkzYxCu9FEikPE7desYhLwyDsuQZBAWpfQSU-jng" alt=""></td></tr><tr><td>Property Type: Flat/ Part of building</td><td><img src="https://lh4.googleusercontent.com/VQIITuo8rNC63jqFMhapyU7Q07H8NVYFzd6BsnEXnUh5ODVjZ3_T1B3mMYGbLnHSZI6DOCQaBA9ZPRx96h-mp2AKI0MaqbfQgUhTO4F2mQBOWB99-8pdS5Z_u2FhjnobZPN3zx8SH2buLUkutk28PyBpeR_Bjh_nrxaH8dfsgPIsSXRwkf8y2GcvIcEgMQ" alt=""></td><td></td></tr><tr><td>Property Type: Vacant Land</td><td><img src="https://lh6.googleusercontent.com/YhhVXf5vyknojiNGIIVwizKQzK3t81I-47vdUV8gPdb-V1DEG_fz0-7Vb3mIGfydTXaeTTCj6UOddGcLWOVfrgFVcKgLlh8uR-sDUqLsfI0gxIYKsZ9fX2a8WTkS3pweuI9Rgp5ttrX1iVsfHSWvNmpIFDkX1XHYZW1R0ESlQ5Npf8DdNHN5pP0zZZ2t8Q" alt=""></td><td></td></tr><tr><td><p>Child property (ies) is/are added to the application. To add the child property, the flow of property registration is used with the below-given limitations.</p><ol><li>Pincode, City, Locality and Street Name is inherited from parent property and are not allowed to edit. The House/ Door No. is entered newly. </li><li>Ownership and owner details are also inherited from parent property and are not allowed to edit.</li><li>The assessment details are entered afresh following the validations about the parent and child properties.</li></ol></td><td><img src="https://lh4.googleusercontent.com/9W8YzGl1lwbdsCqDSuXGCdCUVItpAmPKOBgj97AeyNngNUZ4ywIWV0obAgAHBUrIOYACO7d18vpRc8tKhKGBMM1hqf8Xfjw14gRYSIPr24DaBdzJOdlMmV5uYmJ0OKiLEsNAf8okJbj7DpfiR9TeqpXG_aDmrARs0TxCCrUIgyiUSVia2veD1FSjfIUGlg" alt=""></td><td></td></tr><tr><td>Documents and application summary page are displayed.</td><td><img src="https://lh4.googleusercontent.com/SgkRDH4Ud0G69MkPDjn09GaHCqaEaZItVddi0C8HDf9be5qyX77SLpEETdKhYUQ21PFXghYiRbY2JUl2J1HL_QaGdyQEpitPUYH__YItGecsdr-a0ogBzrDFKqGCzHjjRwwMjH9QO_1qVOevz1st4RSwfB0-r1z9a6TBrQ63GuHEvzzt8VBZPJ9WQn3b1Q" alt=""></td><td></td></tr></tbody></table>

## Use Case Scenarios

#### UC1: There is property ‘A’ which has to be divided into 2 properties of the same usage and in the name of the same owner(s).

1. One new property ‘B’ record is created keeping the address and owner(s) details the same as property ‘A’.&#x20;
2. New door no. is provided to property ‘B’.
3. Assessment detail is added to newly created property ‘B’ keeping usage the same as ‘A’.
4. Property ‘A’ is modified to change the assessment details while the change in address and owner’s detail is now allowed.

#### UC2: There is property ‘A’ which has to be divided into 2 properties of different usage and in the same of the same owner(s).

1. One new property ‘B’ record is created keeping the address and owner(s) details the same as property ‘A’.&#x20;
2. New door no. is provided to property ‘B’.
3. Assessment detail is added to the newly created property ‘B’.
4. Property ‘A’ is modified to change the assessment details while the change in address and owner’s detail is now allowed.

#### UC3: There is property ‘A’ which has to be divided into 2 properties and for the second property owner(s) to be changed.

1. Property ‘A’ is modified to change the assessment details while the change in address and owner’s detail is now allowed.
2. One new property ‘B’ record is created keeping the address and owner(s) details the same as property ‘A’.&#x20;
3. New door no. is provided to property ‘B’.
4. Assessment detail is added to the newly created property ‘B’.
5. Once the bifurcation application is closed, a mutation application seeking change in the owner(s) is applied either for newly created property ‘B’ or existing property ‘A’ based on the need.

**UC4: There is property ‘A’ which has to be divided into 2 properties and for both properties' owner(s) to be changed.**

1. Property ‘A’ is modified to change the assessment details while a change in address and owner’s detail is now allowed.
2. One new property ‘B’ record is created keeping the address and owner(s) details the same as property ‘A’.&#x20;
3. New door no. is provided to property ‘B’.
4. Assessment detail is added to the newly created property ‘B’.
5. Once the bifurcation application is closed, mutation applications seeking change in the owner(s) are applied for newly created property ‘B’ and existing property ‘A’.

\
