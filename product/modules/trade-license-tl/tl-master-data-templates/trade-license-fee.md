# Trade License Fee

## Introduction <a href="#introduction" id="introduction"></a>

Once the Trade Ontology is defined, the next step is to allocate the license fee associated with the Trades.

Dependent on the Trade Classification Level ([Types](trade-type.md)/ [Subtypes](trade-sub-type.md)), the fee allocated might be the same across the Sate or could vary from ULB to ULB. There could be a distinct fee(s) for two different types of applications (new and renewal).

Following are the key tasks to be executed :

* Allocate the License Fee according to Trade Classification Level (Types/Subtypes).
* Map the License fee with the respective Trade Classification Level.

## Data Table <a href="#data-table" id="data-table"></a>

| Sr. No | Trade Sub Type Code\* | Trade Sub Type Name (In English) | New License Fee\* | Renewal License Fee\* | UOM     | UOM From | UOM To |
| ------ | --------------------- | -------------------------------- | ----------------- | --------------------- | ------- | -------- | ------ |
| 1      | TRADE\_SMALL\_BAKERY  | Small Bakery                     | 2500              | 2000                  | Workers | 1        | 20     |
| 2      | TRADE\_SMALL\_BAKERY  | Small Bakery                     | 3000              | 2500                  | Workers | 21       | 30     |
| 2      | TRADE\_MED\_BAKERY    | Medium Bakery                    | 5000              | 4500                  | Workers | 1        | 30     |

The table above contains sample data.

## Procedure <a href="#procedure" id="procedure"></a>

| Sr. No. | Column Name                      | Data Type | Data Size | Is Mandatory? | Description                                                                                                    |
| ------- | -------------------------------- | --------- | --------- | ------------- | -------------------------------------------------------------------------------------------------------------- |
| 1       | Trade Sub Type Code              | Reference | 64        | Yes           | The Code assigned to the [Trade Sub Type](trade-sub-type.md). Eg: TRADE\_SMALL\_BAKERY is assigned to Bakery   |
| 2       | Trade Sub Type Name (In English) | Text      | 256       | Yes           | Name of the Trade Sub Type in English. Eg: Small Bakery                                                        |
| 3       | New License Fee                  | Decimal   | (6,2)     | Yes           | The fee charged when the license applied for the respective trade for the first time.                          |
| 4       | Renewal License Fee              | Decimal   | (6,2)     | Yes           | The fee charged when the license applied for the respective trade for the renewal.                             |
| 5       | UOM                              | Text      | 64        | No            | The Units of Measurement” associated with the Trade. Eg: Workers is the UOM associated with the trade “Bakery” |
| 6       | UOM From                         | Integer   | 6         | No            | Initial Range from which the “Units of Measurement” is applicable for a Trade                                  |
| 7       | UOM To                           | Integer   | 6         | No            | Final Range to which the “Units of Measurement” is applicable to a Trade                                       |

### How to fill data <a href="#how-to-fill-data" id="how-to-fill-data"></a>

1. Download the data template attached to this page.
2. Get a good understanding of all the headers in the template sheet, their data type, size, and definitions by referring to the ‘Data Definition’ section of this document.
3. Identify the “[Trade Sub Types](trade-sub-type.md)” that exists at a ULB/ State level.
4. Collect the above information and feed it below the “Trade Sub Type Name” column accordingly. The Description of Trade Sub Type Name must be provided as per the language specified in the respective column.
5. Add the “Trade Sub Type Code” respectively against the identified trade type(s).
6. Fill in the New License Fee & New Renewal Fee accordingly. The New License Fee & Renewal Fee can be the same as well as distinct, depending on the by-laws/ mandate followed by the State/ULB.
7. Fill in the fields related to Units of Measurement (UOM Unit, From/To) for the available trades only.

## Checklist <a href="#checklist" id="checklist"></a>

The checklist is a set of activities to be performed once the data is filled into a template to ensure data type, size, and format of data is as per the expectation. These activities have been divided into 2 groups as given below.

### Common Checklist <a href="#common-checklist" id="common-checklist"></a>

This checklist covers all the activities which are common across the entities.

| Sr. No. | Checklist Parameter                                                               | Example                                                                                                                      |
| ------- | --------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| 1       | Make sure that each and every point in this reference list has been taken care of | ​[Checklist](https://docs.digit.org/configure-digit/configuring-master-data-templates/module-setup/common-config/checklist)​ |

### Entity Specific Checklist <a href="#entity-specific-checklist" id="entity-specific-checklist"></a>

This checklist covers the activities which are specific to the entity.

| Sr. No. | Checklist Parameter                                                            | Example                                                             |
| ------- | ------------------------------------------------------------------------------ | ------------------------------------------------------------------- |
| 1       | Trade Type Name (In either Language) should not contain any special characters | <p>Small Bakery: [Allowed]</p><p>#Small_Bakery! : [Not allowed]</p> |

## Attachments <a href="#attachments" id="attachments"></a>

[Configuration Data Templateconfiguration-data-template-trade-master-4-.xlsx - 23KB](https://firebasestorage.googleapis.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-MERG\_iQW5oN4ukgXP8K%2Fsync%2F70e034155e217212b5dd14ee4f5f69ff5155e8f9.xlsx?generation=1602050607472075\&alt=media)

[Sample Data Templatesample-configuration-data-template-trade-master-filled-4- (1).xlsx - 24KB](https://firebasestorage.googleapis.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-MERG\_iQW5oN4ukgXP8K%2Fsync%2F4454370e4d6a6d658d27c9c0085b345b8f2e070c.xlsx?generation=1602050607766814\&alt=media)

> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_ ](https://egov.org.in)_is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
