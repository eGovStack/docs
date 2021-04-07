---
description: DIGIT 2.2 Changes to the Water & Sewerage Module
---

# Water & Sewerage 2.2 Release Notes

### Overview <a id="Overview"></a>

The latest Water & Sewerage \(W&S\) release version features two distinct product enhancements. One leverages the ‘open’ search and payment capability of the DIGIT platform. The second enhancement feature relates to the availability of configuration options within W&S to help adoption.

### Release Highlights <a id="Release-Highlights"></a>

1. Open search and payment for W&S recurring bill payments
2. W&S and Property Tax module configuration options for processing new applications

### Release Features <a id="Release-Features"></a>

<table>
  <thead>
    <tr>
      <th style="text-align:left"><b>Key Feature</b>
      </th>
      <th style="text-align:left"><b>Description</b>
      </th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Open search and payment</td>
      <td style="text-align:left">
        <p>Changes in SMS notification:</p>
        <ol>
          <li>Payment link and a Receipt download link is sent to Owner for Bill payment
            and Receipt download. This is an open link that does not require authentication.</li>
        </ol>
        <p>W&amp;S Connection search in Public Domain:</p>
        <ol>
          <li>Open search and payment page can be integrated on the ULB portal where
            Citizens would be able to search and pay for bills without logging in.</li>
          <li>The citizen can search using Property ID, Locality, Consumer ID.</li>
        </ol>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">W&amp;S and PT Config</td>
      <td style="text-align:left">
        <p>The latest W&amp;S module version now has two configuration options and
          they can switch between them according to the state&#x2019;s requirement:</p>
        <ol>
          <li>Implementation of DIGIT W&amp;S individually without Property Tax
            <ol>
              <li>Property registry would be created from W&amp;S and Unique Property ID
                would be allocated to users.</li>
              <li>W&amp;S connection would be allotted over that Property ID.</li>
              <li>Independent from property module, property approval workflows, and property
                department actors.</li>
            </ol>
          </li>
          <li>Implementation of DIGIT W&amp;S along with PT
            <ol>
              <li>Property registry would be created from W&amp;S and Unique Property ID
                will be allocated.</li>
              <li>Property department will process property application created from W&amp;S
                department.</li>
              <li>W&amp;S connection can be either allotted over the Property ID newly created
                from W&amp;S or they can choose an existing property registered in the
                system.</li>
            </ol>
          </li>
        </ol>
      </td>
    </tr>
  </tbody>
</table>

### Known Issues <a id="Known-Issues"></a>

1. [![](https://digit-discuss.atlassian.net/secure/viewavatar?size=medium&avatarId=10310&avatarType=issuetype)RAIN-2119: W&S:: In Workflow selection is not happening in property searched result.REOPENED](https://digit-discuss.atlassian.net/browse/RAIN-2119)

### Upcoming Release Features <a id="Upcoming-Release-Features"></a>

1. Extending this config to W&S modify the connection.
2. Enhancing validations and UI put in place for property creation

### Reference Doc Links <a id="Reference-Doc-Links"></a>

| **Doc Links** | **Description** |
| :--- | :--- |
|  |  |

