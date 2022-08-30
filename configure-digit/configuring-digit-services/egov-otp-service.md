# eGov OTP Service

## Overview <a href="#overview" id="overview"></a>

OTP Service is a core service that is available on the DIGIT platform. The service is used to authenticate the users on the platform. The functionality is exposed via REST API.

## Pre-requisites <a href="#pre-requisites" id="pre-requisites"></a>

Before you proceed with the documentation, make sure the following pre-requisites are met -

* _Java 8_

## Key Functionalities <a href="#key-functionalities" id="key-functionalities"></a>

egov-otp is called internally by the user-otp service which fetches the mobileNumber and feeds it to egov-otp to generate 'n' digit OTP.

## Deployment Details <a href="#deployment-details" id="deployment-details"></a>

1. Deploy the latest version of egov-otp service.
2. Add Role-Action mapping for APIs.

## Configuration Details <a href="#configuration" id="configuration"></a>

Below properties define the OTP configurations

a) `egov.otp.length` : Number of digits in the OTP

b) `egov.otp.ttl` : Controls the validity time frame of the OTP. The default value is 900 seconds. Another OTP generated within this time frame is also allowed.

c) `egov.otp.encrypt` : Controls if the OTP is encrypted and stored in the table.

## Integration Details <a href="#integration" id="integration"></a>

### Integration Scope <a href="#integration-scope" id="integration-scope"></a>

The egov-otp service is used to authenticate the user in the platform.

### Integration Benefits <a href="#integration-benefits" id="integration-benefits"></a>

* Can perform user authentication without impacting the other module.
* In the future, this application can be used in a standalone manner in any other platform that requires a user authentication system.

### Steps to Integration <a href="#steps-to-integration" id="steps-to-integration"></a>

1. To integrate, a host of egov-otp modules should be overwritten in the helm chart.
2. `/otp/v1/_create` __ should be added as the create endpoint. Create OTP Configuration this API is an internal call from v1/\_send endpoint. This endpoint is present in the user-otp service and hence explicit calls are not needed.
3. `/otp/v1/_validate` should be added as the validate endpoint. OTP Configuration this endpoint validates the OTP with respect to the mobile number.
4. `/otp/v1/_search` should be added as the search endpoint. This API searches the mobile number and OTP using the uuid. The uuid nothing but the OTP reference number.

## Reference Docs <a href="#reference-docs" id="reference-docs"></a>

### Doc Links <a href="#doc-links" id="doc-links"></a>

| **Title**                 | **Link**                                                                                                                                                              |
| ------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| API Swagger Documentation | [Swagger Documentation](https://editor.swagger.io/?url=https://raw.githubusercontent.com/egovernments/DIGIT-OSS/doc-patch/core-services/docs/egov-otp-contract.yml#!) |

### API Details <a href="#api-details" id="api-details"></a>

`BasePath` /egov-otp/v1

Egov-otp service APIs - contains create, validate and search endpoint

a) `POST /otp/v1/_create` - create OTP Configuration this API is an internal call from v1/\_send endpoint. This endpoint is present in the user-otp service and hence there is no need for any explicit calls.

b) `POST /otp/v1/_validate` - validate OTP Configuration this endpoint is to validate the OTP with respect to the mobile number.

c) `POST /otp/v1/_search` - search the mobile number and OTP using uuid. The uuid is the OTP reference number.





> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)_​_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in/) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
