# Property Tax - My Payments

**Objective:** Provide users with the payment details for properties registered to the given mobile number and facilitating payments.

## **My Payments**

Users can view the list of payments for properties registered to their mobile number in My Payments tab. The initial view displays the Amount Paid, Property Id, Owner Name, Receipt Date and Receipt Number, and the Download Receipt options. Clicking on the Download Receipt button offers a payment receipt details.&#x20;

![](<../../../../../.gitbook/assets/Screenshot from 2022-03-11 12-59-07.png>)

Clicking on the Download Receipt button downloads the payment receipt.

![](<../../../../../.gitbook/assets/Screenshot from 2022-03-11 13-32-31.png>)

## **Technical Implementation Details**

My Payments common index file link: [https://github.com/egovernments/DIGIT-Dev/blob/develop/frontend/micro-ui/web/micro-ui-internals/packages/modules/pt/src/pages/citizen/MyPayments/index.js](https://github.com/egovernments/DIGIT-Dev/blob/develop/frontend/micro-ui/web/micro-ui-internals/packages/modules/pt/src/pages/citizen/MyPayments/index.js)

Static screen file link: [https://github.com/egovernments/DIGIT-Dev/blob/develop/frontend/micro-ui/web/micro-ui-internals/packages/modules/pt/src/pages/citizen/MyPayments/PTPayments.js](https://github.com/egovernments/DIGIT-Dev/blob/develop/frontend/micro-ui/web/micro-ui-internals/packages/modules/pt/src/pages/citizen/MyPayments/PTPayments.js)

The property search API is called in order to get all the properties linked to the mobile number -`https://qa.digit.org/property-services/property/_search?_=1646986118830`

Next the payments search API is called to retrieve the payments for each property -&#x20;

```
curl 'https://qa.digit.org/collection-services/payments/PT/_search?tenantId=pb&consumerCodes=PB-PT-2022-03-10-027523,PB-PT-2022-03-10-027520,PB-PT-2022-03-09-027519,PB-PT-2022-03-09-027518,PB-PT-2022-03-09-027516,PB-PT-2022-02-23-025202,PB-PT-2022-03-08-027515,PB-PT-2022-03-08-027514,PB-PT-2022-03-08-027513,PB-PT-2022-03-08-027512,PB-PT-2022-03-08-027511,PB-PT-2022-03-08-027510,PB-PT-2022-03-07-027482,PB-PT-2022-03-07-027481,PB-PT-2022-03-07-027472,PB-PT-2022-03-07-027471,PB-PT-2022-03-07-027470,PB-PT-2022-03-07-027469,PB-PT-2022-03-07-027467,PB-PT-2022-03-07-027466,PB-PT-2022-03-07-027465,PB-PT-2022-03-04-027440,PB-PT-2022-03-04-027436,PB-PT-2022-03-04-027435,PB-PT-2022-03-04-027432,PB-PT-2022-03-04-027408,PB-PT-2022-03-04-027406,PB-PT-2022-03-04-027324,PB-PT-2022-03-02-026743,PB-PT-2022-03-02-026680,PB-PT-2022-03-02-026678,PB-PT-2022-03-02-026677,PB-PT-2022-03-02-026676,PB-PT-2022-03-02-026589,PB-PT-2022-03-02-026576,PB-PT-2022-03-02-026586,PB-PT-2022-03-02-026575,PB-PT-2022-02-24-026519,PB-PT-2022-02-24-025642,PB-PT-2022-02-24-025994,PB-PT-2022-02-23-025198,PB-PT-2022-02-23-025014,PB-PT-2022-02-23-024972,PB-PT-2022-02-23-024968,PB-PT-2022-02-23-024969,PB-PT-2022-02-22-024965,PB-PT-2022-02-22-024963,PB-PT-2022-02-22-024962,PB-PT-2022-02-22-024957,PB-PT-2022-02-22-024955&_=1646986124015' \
  -H 'authority: qa.digit.org' \
  -H 'accept: application/json, text/plain, */*' \
  -H 'user-agent: Mozilla/5.0 (Linux; Android 8.0.0; SM-G955U Build/R16NW) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/87.0.4280.141 Mobile Safari/537.36' \
  -H 'content-type: application/json;charset=UTF-8' \
  -H 'origin: https://qa.digit.org' \
  -H 'sec-fetch-site: same-origin' \
  -H 'sec-fetch-mode: cors' \
  -H 'sec-fetch-dest: empty' \
  -H 'referer: https://qa.digit.org/digit-ui/citizen/pt/property/my-payments' \
  -H 'accept-language: en-GB,en;q=0.9' \
  --data-raw '{"RequestInfo":{"apiId":"Rainmaker","authToken":"03434b7d-66d1-47ae-a196-eaf7f4f33f73","userInfo":{"id":16490,"uuid":"7d82122e-1e91-4f34-893f-d16963af217a","userName":"7979797979","name":"Lata","mobileNumber":"7979797979","emailId":"lata@gmail.com","locale":null,"type":"CITIZEN","roles":[{"name":"Citizen","code":"CITIZEN","tenantId":"pb"}],"active":true,"tenantId":"pb","permanentCity":"pb.amritsar"},"msgId":"1646986124015|en_IN"}}' \
  --compressed
```

API Hooks used to call APIs are in the index file of My Payments

```
const result = Digit.Hooks.pt.usePropertySearch({});
const consumerCode = result?.data?.Properties?.map((a) => a.propertyId).join(",");

const {data, isLoading, error} = Digit.Hooks.pt.useMyPropertyPayments({tenantId : tenantId,filters: {consumerCodes:consumerCode}},{enabled:result?.data?.Properties.length>0?true:false, propertyData:result?.data?.Properties});
```

## **MDMS**

No MDMS data is used here. All data is loaded from the Search API.

## &#x20;**Localization**&#x20;

For My Payments the Localization keys are added to the ‘_rainmaker-pt_’ locale module. Any changes, updates or addition of new localization keys is done in the same locale module.

## **Role Action Mapping**

| **Url**                                             | **Roles**               | **Action Id**                         |
| --------------------------------------------------- | ----------------------- | ------------------------------------- |
| `egov-workflow-v2/egov-wf/process/_search`          | `PTCEMP,FI,APPROVER,DV` | `1730`                                |
| `/property-services/property/_search`               | `PTCEMP,FI,APPROVER,DV` | `1897`                                |
| `/egov-workflow-v2/egov-wf/businessservice/_search` | `PTCEMP,FI,APPROVER,DV` | `1743`                                |
| `/filestore/v1/files/url`                           | `PTCEMP,FI,APPROVER,DV` | `1528`                                |
| `/egov-mdms-service/v1/_search?`                    | `PTCEMP,FI,APPROVER,DV` | <p></p><p></p><p></p><p></p><p>O </p> |

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation ](https://egov.org.in/)is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).
