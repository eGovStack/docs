# Fire Station Mapping

## Introduction <a id="Introduction"></a>

After we have created the fire station master, the next step would be to map the Districts, Sub-Districts, and ULBs with the fire stations. The two points that are very important to note here are:

1. All the ULBs in the state may not have a fire department.
2. Usually, only the larger ULBs in the state have a fire department that caters to that ULB at the same time to all the surrounding smaller ULBs and rural areas as well.

## Data Table <a id="Data-Table"></a>

### Urban Area - Fire station mapping <a id="Urban-Area---Fire-station-mapping"></a>

| Sr. No. | \*District code | \*ULB Code | \*Fire Station code | \*Fire Station Name |
| :--- | :--- | :--- | :--- | :--- |
| 1 | DC01 | ULB01 | FS02 | Amritsar |
| 2 | DC01 | ULB02 | FS02 | Amritsar |

### Rural Area - Fire station mapping <a id="Rural-Area---Fire-station-mapping"></a>

| Sr. No. | \*District code | \*Sub District code | \*Fire Station Code | \*Fire Station Name |
| :--- | :--- | :--- | :--- | :--- |
| 1 | DC02 | SDC01 | FS01 | Patiala |
| 2 | DC02 | SDC02 | FS01 | Patiala |

Note: Data given in the above table is sample data.

## Procedure <a id="Procedure"></a>

### Data Definitions <a id="Data-Definitions"></a>

Urban Area

| Sr. No. | Column Name | Data Type | Data Size | Mandatory | Description |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | District Code | Reference | 64 | Yes | The code given to each district in the [Area served masters](https://docs.digit.org/configure-digit/configuring-master-data-templates/module-setup/fire-noc-data/areas-served-master)​ |
| 2 | ULB Code | Reference | 64 | Yes | The code given to each district in the [Area served masters](https://docs.digit.org/configure-digit/configuring-master-data-templates/module-setup/fire-noc-data/areas-served-master)​ |
| 3 | Fire Station Code | Reference | 64 | Yes | The code given to each Fire station in the [Fire Station masters](https://docs.digit.org/configure-digit/configuring-master-data-templates/module-setup/fire-noc-data/fire-station-master)​ |
| 4 | Fire Station Name | Reference | 256 | Yes | The Fire Stations listed in the [Fire Station masters](https://docs.digit.org/configure-digit/configuring-master-data-templates/module-setup/fire-noc-data/fire-station-master)​ |

Rural Area

| Sr. No. | Column Name | Data Type | Data Size | Mandatory | Description |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | District Code | Reference | 64 | Yes | The code given to each district in the [Area served masters](https://docs.digit.org/configure-digit/configuring-master-data-templates/module-setup/fire-noc-data/areas-served-master)​ |
| 2 | Sub District Code | Reference | 64 | Yes | The code given to each sub-district in the [Area served masters](https://docs.digit.org/configure-digit/configuring-master-data-templates/module-setup/fire-noc-data/areas-served-master)​ |
| 3 | Fire Station Code | Reference | 64 | Yes | The code is given to each Fire station in the [Fire Station masters](https://docs.digit.org/configure-digit/configuring-master-data-templates/module-setup/fire-noc-data/fire-station-master)​ |
| 4 | Fire Station Name | Reference | 256 | Yes | The Fire Stations listed in the [Fire Station masters](https://docs.digit.org/configure-digit/configuring-master-data-templates/module-setup/fire-noc-data/fire-station-master)​ |

### How to fill data <a id="How-to-fill-data:"></a>

**Urban Area - Fire Mapping**

1. Download the data template attached to this page.
2. Get a good understanding of all the headers in the template sheet, their data type, size, and definitions by referring to the ‘Data Definition’ section of this document.
3. In case of any doubt, please reach out to the person who has shared this template with you to discuss and clear your doubts.
4. Enter the district codes of all the districts where fire services are provided, in the ‘District Code Column’.
5. Next, enter the ULB codes of all the ULBs within a particular district where the fire services are provided in the 'ULB Code Column'.
6. Identify the fire stations that are serving each District - ULB combination and enter their name in the Fire Station column along with its code in the Fire Station Code.
7. Verify the data once again by going through the checklist and making sure that each and every point mentioned in the checklist is covered.

**Rural Area - Fire Mapping**

1. Download the data template attached to this page.
2. Get a good understanding of all the headers in the template sheet, their data type, size, and definitions by referring to the ‘Data Definition’ section of this document.
3. In case of any doubt, please reach out to the person who has shared this template with you to discuss and clear your doubts.
4. Enter the district codes of all the districts where fire services are provided, in the ‘District Code Column’.
5. Next, enter the sub-district codes of all the sub-district within a particular district where the fire services are provided in the 'Sub District Code Column'.
6. Identify the fire stations that are serving each District - Sub District combination and enter their name in the Fire Station column along with its code in the Fire Station Code.
7. Verify the data once again by going through the checklist and making sure that each and every point mentioned in the checklist is covered.

## Checklist <a id="Common-Checklist"></a>

### Common Checklist <a id="common-checklist"></a>

This checklist covers all the activities which are common across the entities.

| Sr. No. | Checklist Parameter | Example |
| :--- | :--- | :--- |
| 1 | Make sure that each and every point in this reference list has been taken care of | ​[Checklist](https://docs.digit.org/configure-digit/configuring-master-data-templates/module-setup/common-config/checklist)​ |

### Entity Specific Checklist <a id="entity-specific-checklist"></a>

This checklist covers the activities which are specific to the entity.

| Sr. No. | Checklist Parameter | Example |
| :--- | :--- | :--- |
| 1 | District Codes, Sub-district Codes, and ULB codes have to be similar to the codes entered in the Area Master | ​[Areas Served Masters](https://docs.digit.org/configure-digit/configuring-master-data-templates/module-setup/fire-noc-data/areas-served-master)​ |
| 2 | The Fire Station Name and the Fire station Code should be similar to the name and codes entered in the Fire Station Master | ​[Fire Station Master](https://docs.digit.org/configure-digit/configuring-master-data-templates/module-setup/fire-noc-data/fire-station-master)​ |

## Attachments <a id="Attachments"></a>

[Configuration Data Templateconfiguration-data-fire-station-mapping.xlsx - 11KB](https://firebasestorage.googleapis.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-MERG_iQW5oN4ukgXP8K%2Fsync%2Fc38e67d370ac9a53df796a7339ab99cd7b372421.xlsx?generation=1602050608267201&alt=media)

[Sample Datasample-data-template-fire-station-mapping.xlsx - 11KB](https://firebasestorage.googleapis.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-MERG_iQW5oN4ukgXP8K%2Fsync%2Fd4b1486fd7a5db821aeffcee085bd19858208187.xlsx?generation=1602050608335216&alt=media)

<<<<<<< HEAD
[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation ](https://egov.org.in/)is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).
=======


 [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation ](https://egov.org.in/)is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).
>>>>>>> 64dca8adbdf64336b1a8203199b3791fa23434fa

