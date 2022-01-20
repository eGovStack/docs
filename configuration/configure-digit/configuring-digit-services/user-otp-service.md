# User OTP Service

## Overview <a href="#overview" id="overview"></a>

User-OTP service handles the OTP for user registration, user login and password reset for a particular user.

## Pre-requisites <a href="#pre-requisites" id="pre-requisites"></a>

Before you proceed with the documentation, make sure the following pre-requisites are met -

* _Java 8_
* egov-user service is running
* egov-localization service is running
* egov-otp service is running

## Key Functionalities <a href="#key-functionalities" id="key-functionalities"></a>

The user-otp service sends the OTP to the user on login requests, on password change requests and during new user registration.

## Deployment Details <a href="#deployment-details" id="deployment-details"></a>

1. Deploy the latest version of user-otp.
2. Make sure egov-otp is running.
3. Add Role-Action mapping for APIs.

## Integration <a href="#integration" id="integration"></a>

### Integration Scope <a href="#integration-scope" id="integration-scope"></a>

User-OTP service handles the OTP for user registration, user log in and password reset for a particular user.

### Integration Benefits <a href="#integration-benefits" id="integration-benefits"></a>

* Can perform user registration, login, password reset.
* In the future, if we want to expose the application to citizens then it can be done easily.

### Steps to Integration <a href="#steps-to-integration" id="steps-to-integration"></a>

1. To integrate, a host of user-otp modules should be overwritten in the helm chart.
2. `/user-otp/v1/_send` __ should be added as the endpoint for sending OTP to the user via sms or email

## Reference Docs <a href="#reference-docs" id="reference-docs"></a>

### Doc Links <a href="#doc-links" id="doc-links"></a>

| **Title**              | **Link**                                                                          |
| ---------------------- | --------------------------------------------------------------------------------- |
| API Postman Collection | [Postman Collection](https://www.getpostman.com/collections/5a7475c3ec5ad9b06927) |

### API Details <a href="#api-details" id="api-details"></a>

`BasePath` /user-otp/v1/\[API endpoint]

#### **Method**

a) `POST /_send`

This method sends the OTP to the user via SMS or email based on the below parameters:

| Input Field | Description | Mandatory | Data Type |
| ----------- | ----------- | --------- | --------- |

| Input Field    | Description                                | Mandatory | Data Type |
| -------------- | ------------------------------------------ | --------- | --------- |
| `tenantId`     | Unique id for a tenant.                    | Yes       | String    |
| `mobileNumber` | Mobile number of the user                  | Yes       | String    |
| `type`         | OTP type ex: login/register/password reset | Yes       | String    |
| `userType`     | Type of user ex: Citizen/Employee          | No        | String    |

#### Producers <a href="#producers" id="producers"></a>

*   Following are the Producer topic.

    * `egov.core.notification.sms.otp` :- This topic is used to send OTP to the user mobile number.
    * `org.egov.core.notification.email` :- This topic is used to send OTP to the user email id.



> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)_​_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
