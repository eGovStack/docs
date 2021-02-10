---
description: DIGIT 2.0 changes to the Advance Payments
---

# Advance Payments Release Notes

### Overview

Advance payments feature helps citizens to make a payment more than the pending amount. The platform informs the citizen about the excess amount paid and the amount available as an advance in the bills and receipts.

### Release Highlights

1. Pay/ Adjust excess amount against the demand generated
2. Generate Receipt showing the excess payment
3. Generate Bill with advance amount adjustment

### Release Features

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
      <td style="text-align:left">Advance Carry Forward Tax head</td>
      <td style="text-align:left">
        <ol>
          <li>If excess amount present against the consumer no. is displayed on the
            UI under this Tax Head on Bill Summary Pages</li>
          <li>After the creation of new demand, this amount is adjusted against the
            other Tax heads and displayed on the UI</li>
        </ol>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Ability to pay more than Bill Amount</td>
      <td style="text-align:left">
        <ol>
          <li>Provision to make a payment under either &apos;Full amount&apos; or &apos;Custom
            amount&apos; options</li>
          <li>A citizen can enter the desired amount under &apos;Custom amount &apos;
            option</li>
          <li>Amount entered can be either less or more than the bill amount. So partial
            payment and advance payment both are possible.</li>
        </ol>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Changes in Receipt Format</td>
      <td style="text-align:left">
        <p>Two extra fields are provided in the Common Receipt Format</p>
        <ol>
          <li>Total Bill Amount: Includes arrears, taxes, demand, advance adjusted</li>
          <li>Advance available: Advance amount available against a particular consumer</li>
        </ol>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Changes in Bill Format</td>
      <td style="text-align:left">
        <p>Two extra fields are provided in the Common Bill Format</p>
        <ol>
          <li>Advance available: Advance amount available against a particular consumer</li>
          <li>Advance adjusted: Amount available under advance which is utilized against
            a particular demand</li>
        </ol>
      </td>
    </tr>
  </tbody>
</table>

### Known Issues

| **Issue** | **Description** |
| :--- | :--- |
| Bill amount incorrectly calculated | 'Due amount' miscalculation, if multiple meter readings are added without payment |
| Advance adjusted incorrectly calculated | 'Advance adjusted' miscalculated in the bill PDF |

### Upcoming Release Feature

<table>
  <thead>
    <tr>
      <th style="text-align:left">Key Feature</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Cap on the amount entered</td>
      <td style="text-align:left">
        <ol>
          <li>There is a check provided to inform the user about the amount entered
            when it crosses a certain limit.</li>
          <li>The user gets an alert message in the form of warning when a certain amount
            is entered which crosses the limit.</li>
          <li>Check is provided based on two conditions, any point of time it is the
            maximum of either
            <ol>
              <li>Fix amount, or</li>
              <li>10 x Bill amount</li>
            </ol>
          </li>
          <li>Note to be taken that, there is no restriction over the maximum amount
            that can be paid</li>
        </ol>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Changes in Bill PDF</td>
      <td style="text-align:left">
        <ol>
          <li>Tax heads must display &apos;unadjusted&apos; values on the bill PDF</li>
        </ol>
      </td>
    </tr>
  </tbody>
</table>

### Reference Doc Links

| **Doc Links** | **Description** |
| :--- | :--- |
|  |  |
|  |  |

