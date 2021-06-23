# Checklist

## Introduction

The checklist is the set of activities which are there to perform on completion of a task to ensure the fullness and quality of the task.

## Data Types

The data type is an attribute of data, is a particular kind of data item, as defined by the values it can take, the computer system used, or the operations that can be performed on it. In order to help to fill the right kind of data for a data field/ column in excel, the below-given table has different data types with its description.

| **Sr. No.** | **Data Type** | **Definition/ Description** |
| :--- | :--- | :--- |
| 1 | Alphanumeric | It contains alphabets and numbers. And generally used to define the code |
| 2 | Decimal | Floating point number with a fraction value up to 2 decimal places |
| 3 | Integer | Whole number without having a fraction part in it |
| 4 | Text | A string of alphabets, numbers, spaces, and symbols |
| 5 | Date | It represents a date and is captured in the format of ‘DD/MM/YYYY’ |
| 6 | Reference | It is a code of a record from the referred entity and having a related record in the prevailing entity |
| 7 | Document | It represents a document which is needed as an attachment with other relevant details in the template |

## Checklist

### **State Level: These activities are applicable to state-level entities only**

| Sr. No. | Activity | Example |
| :--- | :--- | :--- |
| 1 | The entity is to be decided to be defined at the state level and all the ULBs are agreed on the same. | NA |
| 2 | Data filled into templates should cater to the needs of each and every ULBs. | NA |

### **General: These activities are applicable to all the entities**

<table>
  <thead>
    <tr>
      <th style="text-align:left">Sr. No.</th>
      <th style="text-align:left">Activity</th>
      <th style="text-align:left">Example</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">3</td>
      <td style="text-align:left">Order of headers should remain unchanged in the template while filling
        the data.</td>
      <td style="text-align:left">NA</td>
    </tr>
    <tr>
      <td style="text-align:left">4</td>
      <td style="text-align:left">Value filled into the template doesn&#x2019;t exceed the given data size
        limit.</td>
      <td style="text-align:left">NA</td>
    </tr>
    <tr>
      <td style="text-align:left">5</td>
      <td style="text-align:left">Codes filled in the template for all the records are unique. It means
        no 2 records in the template share the same code.</td>
      <td style="text-align:left">
        <p>Below records in code, value pair is not acceptable.</p>
        <p>RES - Residential</p>
        <p>RES - Non-residential</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">6</td>
      <td style="text-align:left">All the columns marked with an asterisk must be filled with the values
        and not even a single record left without a value.</td>
      <td style="text-align:left">NA</td>
    </tr>
    <tr>
      <td style="text-align:left">7</td>
      <td style="text-align:left">Reference value in the template must also exist in the referred entity
        template. A value without being present in the referred entity template
        is invalid.</td>
      <td style="text-align:left">NA</td>
    </tr>
    <tr>
      <td style="text-align:left">8</td>
      <td style="text-align:left">None of the values filled in the template should have a character which
        is not allowed.</td>
      <td style="text-align:left">NA</td>
    </tr>
    <tr>
      <td style="text-align:left">9</td>
      <td style="text-align:left">Mobile Numbers filled into the template must be 10 digit valid mobile
        numbers without country code.</td>
      <td style="text-align:left">NA</td>
    </tr>
    <tr>
      <td style="text-align:left">10</td>
      <td style="text-align:left">Email id filled into template should be a valid email ID.</td>
      <td style="text-align:left">NA</td>
    </tr>
    <tr>
      <td style="text-align:left">11</td>
      <td style="text-align:left">Local language values should be Unicode charset only.</td>
      <td style="text-align:left">NA</td>
    </tr>
  </tbody>
</table>

### **Data Type Based: These activities are applicable to all entities**

<table>
  <thead>
    <tr>
      <th style="text-align:left">S.No.</th>
      <th style="text-align:left">Activity</th>
      <th style="text-align:left">Example</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">12</td>
      <td style="text-align:left">Values of data type alphanumeric consist of the alphabet and numeric values
        only. All the entity code should follow this.</td>
      <td style="text-align:left">
        <p>Allowed - ABC01</p>
        <p>Not allowed - ABC#01</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">13</td>
      <td style="text-align:left">Values of data type decimal must be a number having fraction part up to
        2 places of decimal.</td>
      <td style="text-align:left">
        <p>Allowed - 23.87</p>
        <p>Not allowed - 12.0982</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">14</td>
      <td style="text-align:left">Values of data type integer must be a number which is not a fraction but
        a whole number.</td>
      <td style="text-align:left">
        <p>Allowed - 15</p>
        <p>Not allowed - 12.01</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">15</td>
      <td style="text-align:left">Values of data type text must be a string of alphabets, numbers, special
        characters, and spaces.</td>
      <td style="text-align:left">NA</td>
    </tr>
    <tr>
      <td style="text-align:left">16</td>
      <td style="text-align:left">Values of data type date must be a date in the format &#x2018;DD/MM/YYYY&#x2019;.
        Here DD means day, MM means month and YYYY means years.</td>
      <td style="text-align:left">
        <p>Allowed - 31/12/2019</p>
        <p>Not allowed - 12/31/2019, 31/12/19, etc.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">17</td>
      <td style="text-align:left">Values of data type reference must be a reference to another entity referring
        to a value in that entity. Only the code of the referred record from the
        referred entity is provided as a value here.</td>
      <td style="text-align:left">NA</td>
    </tr>
    <tr>
      <td style="text-align:left">18</td>
      <td style="text-align:left">Value of the data type document must be a document which is to be provided
        separately as an attachment while submitting the data along with a filled
        data template.</td>
      <td style="text-align:left">NA</td>
    </tr>
  </tbody>
</table>

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)​](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation](https://egov.org.in/) is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).

