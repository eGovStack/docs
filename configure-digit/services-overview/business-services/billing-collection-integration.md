# Billing Collection Integration

## Overview <a href="#introduction" id="introduction"></a>

DIGIT is India's largest open-source platform for Urban Governance. It provides API-based access to government functions enabling the government to provide facilities via integration with relevant service players.\
This document provides the details of how system integrators enable bill collection facilities to customers using DIGIT as the governance platform. It outlines the integration approach with Billing and Collections services to enable fetching bill dues to citizens and recording their payments into the system.

![](../../../.gitbook/assets/108.png)

## Integration Approach <a href="#high-level-approach" id="high-level-approach"></a>

DIGIT is completely API driven and allows for data exchange with disparate systems using REST API calls. Most functional APIs are protected resources that can be accessed after proper authentication with the platform. The platform also checks for the right level of access for given credentials.\
A bill collection flow -

1. Authenticate with DIGIT
2. Get citizen bill using a service-specific query
3. Record the payment details against the bill
4. Optional - Get payment API to fetch the receipt details

The in-field team of the system integrator makes the calls to the integrator's own system (or a standard system like BBPS). Integration with DIGIT follows a server-to-server approach where the backend system of the integrator makes these calls to the DIGIT platform as per requirement. The diagram below depicts the high-level flow of calls between on-field devices like PoS to the integrator backend (Integrator System) and from the backend of the DIGIT integrator to DIGIT (DIGIT Platform).

{% hint style="info" %}
Note: The process of calling payment API results in a receipt creation.
{% endhint %}

## Integration Details <a href="#integration-details" id="integration-details"></a>

DIGIT uses Swagger 2.0 as its API standard and all its APIs are documented in Swagger. Wherever needed this document provides a link to our API documentation online. An example of typical request/response snippets necessary for integration is provided below in the respective sections.

DIGIT is a multi-tenanted system - hence all APIs in DIGIT except tenantid are passed either in the query param or RequestBody (Please refer to detailed API documentation as indicated in sections below). The tenantid represents the modular operating unit for the operation of an API, e.g. in a municipal governance use case. A tenantid represents one ULB. Your platform contact will help you access the configured list for your use case.

Authentication API also expects tenantid (your platform contact will help you identify the one to use). Based on the role as an integrator the OAUTH token in response can be used for unit/ULB level tenants in subsequent API calls (meaning you may not need one authentication per unit/ULB level tenant).

1. **Authentication**

To ensure data privacy and security, transactional APIs in DIGIT are protected under authentication. System integrators are requested to contact the respective state authority to get the necessary OAUTH tokens required to access the APIs. &#x20;

{% hint style="info" %}
**Note:** Apart from the userid/password, the system may enforce IP-based access control in which case the integrator may be required to share the IP or range of IPs from which the request will originate.
{% endhint %}

Use the API below to generate the access token based on the credentials provided.\
Given below is an example of the request and response. The OAuth token to be used from the response is highlighted in bold.

**Request Snippet**

```
curl -X POST \
    https://egov-micro-dev.egovernments.org/user/oauth/token \
    -H 'Authorization: Basic {Authorization Token}' \
    -H 'Content-Type: application/x-www-form-urlencoded' \
    -H 'Postman-Token: 81c87b4c-f69d-464a-8c9a-990e698391ec' \
    -H 'cache-control: no-cache' \
    -d 'grant_type=password&scope=read&username={username}&password={Password}&tenantId={TenantId}&userType=Employee'
```

**Response Snippet**

```
{
"access_token": "6cf92021-8433-4da3-9a1e-8bc511983b2f",
"token_type": "bearer",
"refresh_token": "1f3097f3-39ab-4fd1-91a9-2ce48ac5b6bc",
"expires_in": 604799,
"scope": "read"
}
```

**2. Fetching Bill**

DIGIT allows the integrators to fetch the bills for citizens using the consumer number of the respective service (e.g. Water charges, Property Service, Trade License).&#x20;

{% hint style="info" %}
**Note:** Different services may have different notions of consumer number, e.g. for Water Charges consumer number signifies the "Connection number" while for Property it is the "Property Id".
{% endhint %}

For some services, DIGIT also provides the facility to fetch bills by mobile number.&#x20;

{% hint style="info" %}
**Note:** A bill search by mobile number may return multiple bills across services and may not return bills from services that do not support mobile-number-based search.
{% endhint %}

To support the partial payment use case each bill in the response of the fetch bill API indicates whether it allows partial payment and if yes, the minimum amount to be paid.

To fetch a bill from DIGIT, make sure that the OAuth token is generated as per the Authentication section above. Post that use the following API to fetch the bill -

* [https://www.getpostman.com/collections/900d99a85d083fb2d377](https://www.getpostman.com/collections/900d99a85d083fb2d377)
* [https://raw.githubusercontent.com/egovernments/business-services/master/Docs/billingservice/V-2.0.yml](https://raw.githubusercontent.com/egovernments/business-services/master/Docs/billingservice/V-2.0.yml)
* Choose Billing Service from the dropdown.
* Go to the Bill section of BillingService.
* Go to the Bill tab.

**3. Make Payment**

Once the bill is fetched from the DIGIT system, the system integrator is expected to relay it back to the Field Device. The integrator is expected to Initiate and collect the payment based on government preference indicated in the bill (can it be partially paid and if so the minimum amount etc.) and citizen's preference of payment instrument etc.

Once the payment is successfully done in the integrator's system, the integrator is expected to register the payment in DIGIT using the Payment Create API.&#x20;

{% hint style="info" %}
Note: A bill is considered unpaid/partially paid by DIGIT till appropriate receipts are created using this API - which means that a subsequent fetch of the bill, till this API is called, returns the original bill
{% endhint %}

DIGIT expects a receipt (result of calling payment API) to be created against the bill number returned in the fetch bill API.&#x20;

{% hint style="info" %}
Note: A receipt needs to be created for each bill. Therefore, if a total payment represents multiple bills - one receipt creation per bill is expected (DIGIT supports multiple receipt creation in a single call).
{% endhint %}

To create a receipt in DIGIT, make sure that the OAuth token is generated as per the Authentication section above. Post that use the following API to create the receipt -

* [https://www.getpostman.com/collections/824d6b50b728bccd86d4](https://www.getpostman.com/collections/824d6b50b728bccd86d4)
* [https://raw.githubusercontent.com/egovernments/business-services/master/Docs/collection-services/V-2-0.yml](https://raw.githubusercontent.com/egovernments/business-services/master/Docs/collection-services/V-2-0.yml)
* Choose Collection Service from the dropdown.
* Go to Payment.
* Go to Make Payment.



> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)\_\_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_ ](https://egov.org.in/)_is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
