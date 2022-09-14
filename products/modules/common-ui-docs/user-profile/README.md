# User Profile

**Objective:** The User Profile page is used to view or update user details like name, gender, email, phone number, and profile pic.&#x20;

A user profile is created when the user registers into the application for the first time.&#x20;

## Types of User Profiles <a href="#types-of-user-profiles" id="types-of-user-profiles"></a>

* **Citizen:** A citizen is a basic user who uses the application to perform basic tasks including
  * creating applications, properties, etc
  * viewing all applications, properties, etc
  * payments
* **Employee:** An employee is a user linked to the organization and is more privileged than the citizen and can perform the following tasks
  * creating applications, properties, etc
  * viewing all applications, properties, etc
  * payments
  * and many more

## **Technical Implementations**

Technical Implementations of the user profile code link: [https://github.com/egovernments/DIGIT-Dev/blob/master/frontend/micro-ui/web/micro-ui-internals/packages/modules/core/src/pages/citizen/Home/UserProfile.js](https://github.com/egovernments/DIGIT-Dev/blob/master/frontend/micro-ui/web/micro-ui-internals/packages/modules/core/src/pages/citizen/Home/UserProfile.js)

## **API Call Role Action Mapping**

| **API**                 | **ACTION ID** | **ROLES**            |
| ----------------------- | ------------- | -------------------- |
| `/filestore/v1/files`   |               | `PTCEMP, CITIZEN`    |
| `/user/profile/_update` |               | `PTCEMP, CITIZEN`    |
| `user/password/_update` |               | `ObOPTCEMP, CITIZEN` |

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_ ](https://egov.org.in/)_is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
