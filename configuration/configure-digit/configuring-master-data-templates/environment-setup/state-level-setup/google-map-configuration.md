# Google Map Configuration

### Introduction

At times in the different modules, there is a need to capture the address of the user’s place of residence or where the person is doing a trade, for which the user has to enter his/her full address which creates a task. In order to simplify the process, we can have google map geolocation service in place which would help us get the exact coordinates of the place on the map and help us identify the place.

This service is paid and the client has to purchase the below items:

{% hint style="info" %}
**Google Map API's**

[https://developers.google.com/maps/documentation/javascript/get-api-key](https://developers.google.com/maps/documentation/javascript/get-api-key)\
"Maps Javascript API", "Places API" and "Geolocation API" are needed and first 200$ usages are free, once it exceeds, the price per 1000 requests as given below.

1. **Maps JavaScript API (web-client)** Return the location and accuracy radius of a device, based on Wi-Fi or cell towers. $5
2. **Geolocation API** Return the location and accuracy radius of a device, based on Wi-Fi or cell towers. $5
3. **Places API for Web (web-server)** Turn a phone number, address, or name into a place, and provide its name and address. $17
{% endhint %}

### Data Table

| Sr. No             | Google API URL\*                                         | API Key\*          |
| ------------------ | -------------------------------------------------------- | ------------------ |
| <ol><li></li></ol> | [www.google.apiurls.com](http://www.google.apiurls.com/) | 1458-ASD785-987722 |

Note:

### Procedure

#### Data Definition

| Sr. No.            | Column Name    | Data Type    | Data Size | Is Mandatory? | Description                                                                         |
| ------------------ | -------------- | ------------ | --------- | ------------- | ----------------------------------------------------------------------------------- |
| <ol><li></li></ol> | Google API URL | Alphanumeric | 64        | Yes           | The URL of the API that is being purchased                                          |
| 2.                 | API Key        | Alphanumeric | 64        | Yes           | The key which the google would provide after the purchase for the API has been done |

{% hint style="info" %}
The data provided is sample data
{% endhint %}

#### Steps to fill the data

1. Download the data template attached to this page.
2. Get a good understanding of all the headers in the template sheet, their data type, size, and definitions by referring to the ‘Data Definition’ section of this document.
3. In case of any doubt, please reach out to the person who has shared this template with you to discuss and clear your doubts.
4. Ask the clients to purchase the above-mentioned APIs in the Introduction section.
5. Get the details for the API URL and key from the client.
6. Verify the data once again by going through the checklist and making sure that each and every point mentioned in the checklist is covered.

### Checklist

The checklist is a set of activities to be performed one the data is filled into a template to ensure data type, size, and format of data is as per the expectation. These activities have been divided into 2 groups as given below.

#### Common Checklist

This checklist covers all the activities which are common across the entities.

| Sr. No. | Checklist Parameter                                                               | Example                                                    |
| ------- | --------------------------------------------------------------------------------- | ---------------------------------------------------------- |
| 1       | Make sure that each and every point in this reference list has been taken care of | [Checklist](../../module-setup/common-config/checklist.md) |

#### Entity Specific Checklist

Not Applicable

### Attachments

{% file src="../../../../../.gitbook/assets/configurable-data-template-google-map-account-configuration-v1.xlsx" %}
Configuration Data Template
{% endfile %}

{% file src="../../../../../.gitbook/assets/configurable-sample-data-google-map-account-configuration-v1.xlsx" %}
Sample Data Template
{% endfile %}

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)​](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation](https://egov.org.in/) is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).
