---
description: Migrating legacy data
---

# PT Data Migration

## Overview

This section covers the principles eGov will be following for migrating legacy property registry along with demand and collection balances to the DIGIT system \(currently in Uttarakhand but can be used for other clients in future\). eGov has been successful in implementing property tax applications in states of Andhra Pradesh, Punjab and various other Municipal Corporations like Greater Chennai, Nagpur and so on using best practices defined here.

## Entry Criteria

The state team is supposed to take care of the below activities before property data is shared to eGov for data migration:

1. State team to share all master data and its localization that are part of the property tax. For example masters like - city, boundary, usage type, property type and so on
2. State team to do the data gathering and prepare the property tax data in the predefined template shared by eGov
3. Data prepared needs to be scrutinised by the data owner from the State’s team. Following data validations to be considered in particular:
   1. Validate if all sheets have accurate records \(owner details, property details and DCB details, Floor details\) in terms of what is expected
   2. DCB details can be more than the number of records in the property sheet
   3. There can be multiple owners for a single property. But there needs to be an owner and DCB for each of the properties
   4. Have a check on all mandatory data present
   5. All sheets to be aligned with the unique id field
4. The state has to share the complete set of property data for a city in a single go. They can also give one set for residential properties and another for commercial properties, but cannot give multiple sets for the same.
5. Data owner to give a sign off on data before handing over to eGov team
6. State team to be aware of assumptions and default values that will be applied as part of the data migration process. This will be shared by the eGov team
7. UAT and production environment where the data is to be loaded to be provisioned and set up

## Principles

![](../../../.gitbook/assets/image%20%2898%29.png)

### Step 1 - Data cleansing

1. Data received from the State team will be cleansed by eGov with default values
   1. Mandatory fields that have no financial impact on citizens can be filled with default values in the absence of values specified by the State team. Few examples are listed below -
      1. Covered areas can be updated as 0
      2. Road type as 12 meters
      3. The number of floors can be updated as 1
   2. Certain fields that have a financial impact can also have default values like tax amount in the absence of values specified by the State team. \(It can be updated as Rs.1\)
   3. If the mobile number is blank, a dummy mobile number will be updated. Care will be taken to ensure that this is not an actual mobile number and this number will be removed from notifications. Dummy numbers can be something like 99999xxxxx where the first few dummy numbers in a state will be 9999900001, 9999900002, 9999900003 so on.
2. Follow the below assumptions to do data cleaning
   1. If the mobile number and user name combinations are duplicating we will consider these properties belong to the same owner. This means one user will be created in the system which will have a link to two properties.
   2. Have a marker if any assumptions and default values are applied on a record
   3. Certain data are currently not assumed or defaulted. Below listed are a few cases -
      1. Owner details completely not available for a property - If complete owner details are missing, these records to be kept in the not to be migrated list.
      2. If DCB is not there or given for a range of years - since there are a lot of use cases here, we can keep this record in the not to be migrated list
      3. Duplicate old property id - leave the data as it is and then edit it later using the data entry screen
      4. If boundary data is not present or data not aligned with the master data shared - update to a default mohalla which the state agrees to
      5. Door number is not present - update the value as “door number”
      6. Owner Name blank in the owner details sheet - update the value as “owner”.

### Step 2 - Data Load on UAT

1. Load the records using property migration kit to UAT server
2. Prepare a list of all passed and failed property records and share them back with the State team. Passed records along with values defaulted will be shared.
3. If the State team wants eGov to retry all failed records they are expected to come back with the revised data within one week.
4. Repeat Step 1 for revised records received from the State team.
5. The final status of the data load will be shared with the State team.

### Step 3 - Move data to Production

1. State team to verify data loaded on UAT server and provide a sign off for each of the ULBs within 1 week
2. On getting sign-off of UAT data, eGov will load that data to production using the migration kit used for loading to UAT instances. This can be done only if the production infrastructure is ready.
3. Get sign off on the production data before the application can be made live.

## References

<table>
  <thead>
    <tr>
      <th style="text-align:left">ULB</th>
      <th style="text-align:left">Total Records</th>
      <th style="text-align:left">Duplicate/Wrong data</th>
      <th style="text-align:left">% of data loadable after imposing assumptions</th>
      <th style="text-align:left">% of incorrect data</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Roorkee</td>
      <td style="text-align:left">16363</td>
      <td style="text-align:left">500</td>
      <td style="text-align:left">97%</td>
      <td style="text-align:left">3%</td>
    </tr>
    <tr>
      <td style="text-align:left">Rishikesh</td>
      <td style="text-align:left">2877</td>
      <td style="text-align:left">
        <p>356 in the first sheet</p>
        <p>261 in the second pass</p>
      </td>
      <td style="text-align:left">
        <p>88%</p>
        <p>91%</p>
      </td>
      <td style="text-align:left">
        <p>12%</p>
        <p>9%</p>
      </td>
    </tr>
  </tbody>
</table>

## Communication Mechanism

Communication for data migration exercise can be split into the following stages:

There will be a SPOC from the State team who is the data owner who will share data with the eGov team. Excel sheet data will be put on google drive and shared with the project manager from eGov. Similarly, all communications from the eGov side to State will be routed through the project manager.

1. Pre-migration
   1. A demo of how PT module works - State + ULBs
   2. Product fitment discussion, configurable data finalization and sign off - State
   3. An overview of how data migration works - State + ULBs
   4. Sharing the template \(along with checklists and FAQs\) in which we will collect data and type of data required against each field along with training - State + ULBs
   5. Sharing assumptions which will be followed while migrating data - State + ULBs
2. During migration
   1. Data inconsistencies observed in Data cleaning stage - State
   2. Gaps needed to complete data migration \(like mohalla mapping\) - State
   3. List of records which will be migrated as-is and the ones which will be migrated with assumptions - State
3. Post-migration
   1. List of properties migrated without error - State
   2. List of properties migrated with error for ULBs manual entry - State
   3. UAT Sign-off document - State + ULB
   4. Final confirmation post migration on Production - State + ULB

## Way Forward

1. All failed records from the second pass will be manually entered into the system using data entry screens
2. The state has to make a mandate to collect property tax only using DIGIT. 
3. All records with assumption markers or incorrect data can be updated by counter employees when citizens come for payment. Maybe this option can be given to the citizen when coming for online payment.
4. When a citizen is coming for making his payment, the counter operator can check if their property exists in the system using propertyid or mobile number. If it is found to be missing, it can be captured afresh in the system using the data entry option. All required information can be obtained from the citizen, either from previous year receipts that they carry or directly asking them.
5. With this approach, a ULB can go live with 90% of property data within a short time.

## Data Mapping Template

{% file src="../../../.gitbook/assets/propertytaxdata-masters-mapping.xlsx" caption="Property Tax Master Data Mapping Template" %}

{% hint style="warning" %}
**Data Migration Checklist**

1. Data provided in the standard template attached only will be accepted for further analysis and process.
2. Data provided into the template is loaded into staging tables and then validation and data clean-up is done.
   1. Properties with current Tax 0. \(2020-21\)
   2. Properties with advance collection
   3. Properties with current tax partially payment
   4. Properties with Mohalla not configured in master
   5. Masters mapping with the configured masters data in the system.
3. All the findings of data are reported to the onsite team and sought clarification.
4. Once all the queries/ findings are cleared/addressed data is moved into UAT.
5. Data is verified into UAT with sampling by the state team. Go ahead.
6. Preparing some basic checkpoints before moving into production.
7. Move the data into production and verify the checkpoints. 
{% endhint %}





> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_ ](https://egov.org.in/)_is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._

