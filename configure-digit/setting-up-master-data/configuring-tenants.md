# Configuring Tenants

## Overview

Tenant represents a body in a system. In the municipal system, a state and its ULBs \(Urban local bodies\) are tenants. ULB represents a city or a town in a state. Tenant configuration is done in MDMS.

## Pre-requisites

Before proceeding with the configuration, the following pre-requisites are met -

* Knowledge of json and how to write a json is required.
* Knowledge of MDMS is required.
* User with permissions to edit the git repository where MDMS data is configured.

## Key Functionalities

* For login page city name selection is required. Tenant added in MDMS shows in city drop-down of the login page.
* In reports or in the employee inbox page the details related to ULB is displayed from the fetched ULB data which is added in MDMS.
* Modules i.e., TL, PT, MCS can be enabled based on the requirement for the tenant.

## Deployment Details

After adding the new tenant, the MDMS service needs to be restarted to read the newly added data.

## Configuration Details

Tenant is added in tenant.json.  
In MDMS, file **tenant.json**, under **tenant** folder holds the details of state and ULBs to be added in that state.

```text
{
  "tenantId": "uk",  //<ReplaceWithDesiredTenantId>
  "moduleName": "tenant",
  "tenants": [ {
      "code": "uk.citya", //<state.ulbname>
      "name": "City A",  //<name of the ulb>
      "description": "City A", //<ulb description>
      "logoId": "https://s3.ap-south-1.amazonaws.com/uk-egov-assets/uk.citya/logo.png",  //<ulb logo path - To display ulb logo on login>
      "imageId": null,
      "domainUrl": "", //<ulb website url>
      "type": "CITY",
      "twitterUrl": null,
      "facebookUrl": null,
      "emailId": "complaints.citya@gmail.com",  //<ulb email id>
      "OfficeTimings": {
        "Mon - Sat": "10.00 AM - 5.00 PM"
      },
"city": {
"name": "City A",
"localName": null,
"districtCode": "CITYA",
"districtName": null,
"regionName": null,
"ulbGrade": "Municipal Corporation",
"longitude": 78.0322,
"latitude": 30.3165,
"shapeFileLocation": null,
"captcha": null,
"code": "248430"
},
"address": "City A Municipal Cornoration Address",
"contactNumber": "91 (135) 2653572"
}]}
```

{% hint style="info" %}
To enable tenant the above data should be pushed in tenant.json file. Here "ULB Grade" and City "Code" are important fields. **ULB Grade** can have a set of allowed values that determines the ULB type, \([Municipal corporation \(Nagar Nigam\)](https://en.wikipedia.org/wiki/Municipal_Corporations_in_India), Municipality \(municipal council, municipal board, municipal committee\) \(Nagar Parishad\), etc\). City "**Code**" has to be unique to each tenant. This city-specific code is used in all transactions. Not permissible to change the code. If changed we will lose the data of the previous transactions done.
{% endhint %}

{% hint style="info" %}
Naming Convention for **Tenants Code**

**“Code”:“uk.citya”** is **StateTenantId.ULBTenantName"**
{% endhint %}

{% hint style="info" %}
**"logoId": "**[**https://s3.ap-south-1.amazonaws.com/uk-egov-assets/uk.citya/logo.png**](https://s3.ap-south-1.amazonaws.com/pb-egov-assets/pb.citya/logo.png)**",** Here the last section of the path should be "/&lt;tenantId&gt;/logo.png". If we use anything else, logo will not be displayed on the UI. **&lt;tenantId&gt;** is the tenant code ie **“uk.citya”.**
{% endhint %}

Localization should be pushed for ULB grade and ULB name. The format is given below.

**Localization for ULB Grade**

```text
{
     "code": "ULBGRADE_MUNICIPAL_CORPORATION",
     "message": "MUNICIPAL CORPORATION",
     "module": "rainmaker-common",
     "locale": "en_IN"
  }
```

**Localization for ULB Name**

```text
{
     "code": "TENANT_TENANTS_UK_HALDWANI",    
     "message": "Haldwani",
     "module": "rainmaker-tl",
     "locale": "en_IN"
}
```

**Format of localization code for tenant name** &lt;**MDMS\_State\_Tenant\_Folder\_Name**&gt;\_&lt;**Tenants\_Fille\_Name**&gt;\_&lt;**Tenant\_Code**&gt; \(replace dot with underscore\)

Boundary data should be added for the new tenant.

## Reference Docs

### Doc Links

| **Title** | **Link** |
| :--- | :--- |
| tenant json file | [![](https://github.githubassets.com/favicon.ico)tenants.json](https://github.com/egovernments/ukd-mdms-data/blob/master/data/uk/tenant/tenants.json) |
| content | [MDMS Configuration:](https://digit-discuss.atlassian.net/wiki/spaces/DOPS/pages/110952456) |

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation ](https://egov.org.in/)is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).

