# Fire Station Mapping

### Introduction <a id="Introduction"></a>

After we have created the fire station master, the next step would be to map the Districts, Sub-Districts, and ULBs with the fire stations. The two points that are very important to note here are:

1. All the ULBs in the state may not have a fire department.
2. Usually, only the larger ULBs in the state have a fire department that caters to that ULB at the same time to all the surrounding smaller ULBs and rural areas as well.

### Data Table <a id="Data-Table"></a>

#### Urban Area - Fire station mapping <a id="Urban-Area---Fire-station-mapping"></a>

| Sr. No. | \*District code | \*ULB Code | \*Fire Station code | \*Fire Station Name |
| :--- | :--- | :--- | :--- | :--- |
| 1 | DC01 | ULB01 | FS02 | Amritsar |
| 2 | DC01 | ULB02 | FS02 | Amritsar |

#### Rural Area - Fire station mapping <a id="Rural-Area---Fire-station-mapping"></a>

| Sr. No. | \*District code | \*Sub District code | \*Fire Station Code | \*Fire Station Name |
| :--- | :--- | :--- | :--- | :--- |
| 1 | DC02 | SDC01 | FS01 | Patiala |
| 2 | DC02 | SDC02 | FS01 | Patiala |

Note: Data given in the above table is a sample data.

### Procedure <a id="Procedure"></a>

#### Data Definitions <a id="Data-Definitions"></a>

Urban Area

| Sr. No. | Column Name | Data Type | Data Size | Mandatory | Description |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | District Code | Reference | 64  | Yes | The code given to each district in the [Area served masters](areas-served-master.md) |
| 2 | ULB Code | Reference | 64  | Yes | The code given to each district in the [Area served masters](areas-served-master.md) |
| 3 | Fire Station Code | Reference | 64  | Yes | The code given to each Fire station in the [Fire Station masters](fire-station-master.md) |
| 4 | Fire Station Name | Reference | 256 | Yes | The Fire Stations listed in the[ Fire Station masters](fire-station-master.md) |

Rural Area

| Sr. No. | Column Name | Data Type | Data Size | Mandatory | Description |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | District Code | Reference |  64 | Yes | The code given to each district in the[ Area served masters](areas-served-master.md) |
| 2 | Sub District Code | Reference | 64  | Yes | The code given to each sub-district in the [Area served masters](areas-served-master.md) |
| 3 | Fire Station Code | Reference | 64  | Yes | The code is given to each Fire station in the [Fire Station masters](fire-station-master.md) |
| 4 | Fire Station Name | Reference | 256 | Yes | The Fire Stations listed in the [Fire Station masters](fire-station-master.md) |

#### How to fill data <a id="How-to-fill-data:"></a>

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

### Checklist <a id="Common-Checklist"></a>

#### Common Checklist

This checklist covers all the activities which are common across the entities.

| Sr. No. | Checklist Parameter | Example |
| :--- | :--- | :--- |
| 1 | Make sure that each and every point in this reference list has been taken care of | [Checklist](../untitled-1/checklist.md) |

#### Entity Specific Checklist

This checklist covers the activities which are specific to the entity.

| Sr. No. | Checklist Parameter | Example |
| :--- | :--- | :--- |
| 1 | District Codes, Sub-district Codes, and ULB codes have to be similar to the codes entered in the Area Master | [Areas Served Masters](areas-served-master.md) |
| 2 | The Fire Station Name and the Fire station Code should be similar to the name and codes entered in the Fire Station Master | [Fire Station Master](fire-station-master.md) |

### Attachments <a id="Attachments"></a>

{% file src="../../../../.gitbook/assets/configuration-data-fire-station-mapping.xlsx" caption="Configuration Data Template" %}

{% file src="../../../../.gitbook/assets/sample-data-template-fire-station-mapping.xlsx" caption="Sample Data" %}

