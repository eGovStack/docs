# Google Map Configuration

## Introduction

At times in the different modules, there is a need to capture the address of the user’s place of residence or where the person is doing a trade, for which the user has to enter his/her full address which creates a task. In order to simplify the process, we can have google map geolocation service in place which would help us get the exact coordinates of the place on the map and help us identify the place.

This service is paid and the client has to purchase the below items:

{% hint style="info" %}
**Google Map API's**

[https://developers.google.com/maps/documentation/javascript/get-api-key](https://developers.google.com/maps/documentation/javascript/get-api-key)  
"Maps Javascript API", "Places API" and "Geolocation API" are needed and first 200$ usages are free, once it exceeds, the price per 1000 requests as given below.

1. **Maps JavaScript API \(web-client\)** Return the location and accuracy radius of a device, based on Wi-Fi or cell towers. $5
2. **Geolocation API** Return the location and accuracy radius of a device, based on Wi-Fi or cell towers. $5
3. **Places API for Web \(web-server\)** Turn a phone number, address, or name into a place, and provide its name and address. $17
{% endhint %}

## Data Table

<table>
  <thead>
    <tr>
      <th style="text-align:left">Sr. No</th>
      <th style="text-align:left">Google API URL*</th>
      <th style="text-align:left">API Key*</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">
        <ol>
          <li></li>
        </ol>
      </td>
      <td style="text-align:left"><a href="http://www.google.apiurls.com/">www.google.apiurls.com</a>
      </td>
      <td style="text-align:left">1458-ASD785-987722</td>
    </tr>
  </tbody>
</table>

Note:

## Procedure

### Data Definition

<table>
  <thead>
    <tr>
      <th style="text-align:left">Sr. No.</th>
      <th style="text-align:left">Column Name</th>
      <th style="text-align:left">Data Type</th>
      <th style="text-align:left">Data Size</th>
      <th style="text-align:left">Is Mandatory?</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">
        <ol>
          <li></li>
        </ol>
      </td>
      <td style="text-align:left">Google API URL</td>
      <td style="text-align:left">Alphanumeric</td>
      <td style="text-align:left">64</td>
      <td style="text-align:left">Yes</td>
      <td style="text-align:left">The URL of the API that is being purchased</td>
    </tr>
    <tr>
      <td style="text-align:left">2.</td>
      <td style="text-align:left">API Key</td>
      <td style="text-align:left">Alphanumeric</td>
      <td style="text-align:left">64</td>
      <td style="text-align:left">Yes</td>
      <td style="text-align:left">The key which the google would provide after the purchase for the API
        has been done</td>
    </tr>
  </tbody>
</table>

{% hint style="info" %}
The data provided is sample data
{% endhint %}

### Steps to fill the data

1. Download the data template attached to this page.
2. Get a good understanding of all the headers in the template sheet, their data type, size, and definitions by referring to the ‘Data Definition’ section of this document.
3. In case of any doubt, please reach out to the person who has shared this template with you to discuss and clear your doubts.
4. Ask the clients to purchase the above-mentioned APIs in the Introduction section.
5. Get the details for the API URL and key from the client.
6. Verify the data once again by going through the checklist and making sure that each and every point mentioned in the checklist is covered.

## Checklist

The checklist is a set of activities to be performed one the data is filled into a template to ensure data type, size, and format of data is as per the expectation. These activities have been divided into 2 groups as given below.

### Common Checklist

This checklist covers all the activities which are common across the entities.

| Sr. No. | Checklist Parameter | Example |
| :--- | :--- | :--- |
| 1 | Make sure that each and every point in this reference list has been taken care of | [Checklist](../../module-setup/common-config/checklist.md) |

### Entity Specific Checklist

Not Applicable

## Attachments

{% file src="../../../../.gitbook/assets/configurable-data-template-google-map-account-configuration-v1.xlsx" caption="Configuration Data Template" %}

{% file src="../../../../.gitbook/assets/configurable-sample-data-google-map-account-configuration-v1.xlsx" caption="Sample Data Template" %}

