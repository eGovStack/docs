# OBPS Inbox

## Objective

Users can view all the applications assigned to them in the employee inbox. And it provides multiple filters and search options to filter the applications.

## Application Details

OBPS Inbox uses InboxComposer React HOC to create the Inbox through various child components, for both mobile and Desktop Components.

![](<../../../../../../.gitbook/assets/Desktop - 40.png>)

The API used to fetch applications in the inbox

```
curl 'https://qa.digit.org/inbox/v1/_search?_=1634785190890' \
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
  -H 'referer: https://qa.digit.org/digit-ui/employee/obps/inbox' \
  -H 'accept-language: en-GB,en-US;q=0.9,en;q=0.8' \
  -H 'cookie: amplitude_id_fef1e872c952688acd962d30aa545b9edigit.org=eyJkZXZpY2VJZCI6IjYxMDYxMWFjLTY5MjMtNDQ1Yi04ZWZlLTUxNGVkMmE5MzRjOFIiLCJ1c2VySWQiOm51bGwsIm9wdE91dCI6ZmFsc2UsInNlc3Npb25JZCI6MTYzMzA4NTYwNzE5MiwibGFzdEV2ZW50VGltZSI6MTYzMzA4NTYwNzk2OCwiZXZlbnRJZCI6MSwiaWRlbnRpZnlJZCI6MSwic2VxdWVuY2VOdW1iZXIiOjJ9; _ga=GA1.2.1811666557.1633085608' \
  --data-raw '{"inbox":{"tenantId":"pb.amritsar","processSearchCriteria":{"moduleName":"bpa-services","businessService":["BPA_LOW","BPA","BPA_OC"]},"moduleSearchCriteria":{"assignee":"ASSIGNED_TO_ALL","sortOrder":"DESC"},"sortBy":"","limit":10,"offset":0,"sortOrder":"DESC"},"RequestInfo":{"apiId":"Rainmaker","authToken":"c9fdcf78-37cd-44aa-af31-88278cf1dc75","userInfo":{"id":12588,"uuid":"a56bae11-e18b-4dd3-b70f-b29f2abb1edf","userName":"EMP-BPA","name":"SR DV FI","mobileNumber":"9999999445","emailId":null,"locale":null,"type":"EMPLOYEE","roles":[{"name":"Employee","code":"EMPLOYEE","tenantId":"pb.amritsar"},{"name":"BPAREG Employee","code":"BPAREG_EMPLOYEE","tenantId":"pb.amritsar"},{"name":"BPA Services verifier","code":"BPA_VERIFIER","tenantId":"pb.amritsar"},{"name":"QA Automation","code":"QA_AUTOMATION","tenantId":"pb.amritsar"},{"name":"State Administrator","code":"STADMIN","tenantId":"pb.amritsar"},{"name":"Super User","code":"SUPERUSER","tenantId":"pb.amritsar"},{"name":"BPAREG Approver","code":"BPAREG_APPROVER","tenantId":"pb.amritsar"},{"name":"BPAREG doc verifier","code":"BPAREG_DOC_VERIFIER","tenantId":"pb.amritsar"},{"name":"BPA NOC Verifier","code":"BPA_NOC_VERIFIER","tenantId":"pb.amritsar"}],"active":true,"tenantId":"pb.amritsar","permanentCity":null}}}' \
  --compressed
```

For viewing OBPS inbox these roles are necessary `"BPA_FIELD_INSPECTOR", "BPA_NOC_VERIFIER", "BPA_APPROVER", "BPA_VERIFIER", "CEMP"`

The MDMS links (blue text hyperlinks) are used while selecting OBPS [application type](https://github.com/egovernments/egov-mdms-data/blob/DEV/data/pb/BPA/ApplicationType.json), [service type](https://github.com/egovernments/egov-mdms-data/blob/DEV/data/pb/BPA/ServiceType.json), risk type with business service and status filters.&#x20;

Refer to the config below for risk type definition:-

```
    const configData = {
        BUILDING_PLAN_SCRUTINY: [{code: "BPA_LOW",i18nKey: "WF_BPA_LOW"}, {code: "BPA",i18nKey: "WF_BPA"}],
        BUILDING_OC_PLAN_SCRUTINY: [{code: "BPA_OC", i18nKey: "WF_BPA_OC"}],
    }
```



> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)_​_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in/) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
