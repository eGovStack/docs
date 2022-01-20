# OBPS-BPA/OC-BPA Employee Flow

## Objective <a href="#objective" id="objective"></a>

To provide the facility for the employee users to update the BPA application state.

## Localization <a href="#localization" id="localization"></a>

The localization module used across the OBPS module was rainmaker-bpa and rainmaker-common, out of which we initialized rainmaker-bpa with module initialization.

![](<../../../../../.gitbook/assets/image-20211207-124358 (1).png>)

## Application Details <a href="#application-details" id="application-details"></a>

The application details page is used to display the details of the application and also showcase all the actions that can be taken on the application.

![](<../../../../../.gitbook/assets/Desktop - 50.png>)

The various step for the application:

#### Document Verification

In this step, the user can upload multiple documents and/or approve the already uploaded documents.

#### NOC Verification

The user approves the uploaded NOC documents.

#### Inspection Report

The user fills in the inspection details (date, time, question, remarks) and submits.

#### Permit Condition

Here the user approves the required permit conditions and can also add new conditions.

### UI Implementation <a href="#ui-implementation" id="ui-implementation"></a>

All the screens are developed using the new-UI structure followed previously in FSM, PGR, PT, and TL. Certain new components have been introduced such as Multi-Document Upload, Approval Checks, etc.

### MDMS Data <a href="#mdms-data" id="mdms-data"></a>

Throughout the flow, some data is imported from the MDMS. Following are the list of MDMS data:

1. CheckList
2. RiskTypeComputation

Below is the MDMS config used to fetch MDMS data:

```
curl 'https://qa.digit.org/egov-mdms-service/v1/_search?tenantId=pb' \
  -H 'authority: qa.digit.org' \
  -H 'sec-ch-ua: "Chromium";v="94", "Google Chrome";v="94", ";Not A Brand";v="99"' \
  -H 'accept: application/json, text/plain, */*' \
  -H 'content-type: application/json;charset=UTF-8' \
  -H 'sec-ch-ua-mobile: ?0' \
  -H 'user-agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/94.0.4606.81 Safari/537.36' \
  -H 'sec-ch-ua-platform: "Linux"' \
  -H 'origin: https://qa.digit.org' \
  -H 'sec-fetch-site: same-origin' \
  -H 'sec-fetch-mode: cors' \
  -H 'sec-fetch-dest: empty' \
  -H 'referer: https://qa.digit.org/digit-ui/employee/obps/bpa/PB-BP-2021-10-19-002931' \
  -H 'accept-language: en-GB,en-US;q=0.9,en;q=0.8' \
  -H 'cookie: amplitude_id_fef1e872c952688acd962d30aa545b9edigit.org=eyJkZXZpY2VJZCI6IjYxMDYxMWFjLTY5MjMtNDQ1Yi04ZWZlLTUxNGVkMmE5MzRjOFIiLCJ1c2VySWQiOm51bGwsIm9wdE91dCI6ZmFsc2UsInNlc3Npb25JZCI6MTYzMzA4NTYwNzE5MiwibGFzdEV2ZW50VGltZSI6MTYzMzA4NTYwNzk2OCwiZXZlbnRJZCI6MSwiaWRlbnRpZnlJZCI6MSwic2VxdWVuY2VOdW1iZXIiOjJ9; _ga=GA1.2.1811666557.1633085608' \
  --data-raw '{"MdmsCriteria":{"tenantId":"pb","moduleDetails":[{"moduleName":"BPA","masterDetails":[{"name":"RiskTypeComputation"}]}]},"RequestInfo":{"apiId":"Rainmaker"}}' \
  --compressed
```



>
