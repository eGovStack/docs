# Employee Flow - Messages

## Screen Flow

![Employee Inbox](../../../.gitbook/assets/image-20211213-042511.png)

![Create Messages](../../../.gitbook/assets/image-20211213-042553.png)

![Application Details With Actions](../../../.gitbook/assets/image-20211213-042901.png)

![Edit Message](../../../.gitbook/assets/image-20211213-042934.png)

## User Permissions  <a href="#user-permissions" id="user-permissions"></a>

Employee users with user roles including “`EMPLOYEE ADMIN`" or “`EMPLOYEE`" have access to the event actions.

## Events API cURLs  <a href="#events-api-curls" id="events-api-curls"></a>

### Search Inbox API

```
curl 'https://qa.digit.org/egov-user-event/v1/events/_search?tenantId=pb.amritsar&status=ACTIVE,INACTIVE&eventTypes=BROADCAST&limit=10&offset=0&_=1639369326123' \
  -H 'Connection: keep-alive' \
  -H 'sec-ch-ua: " Not A;Brand";v="99", "Chromium";v="96", "Google Chrome";v="96"' \
  -H 'Accept: application/json, text/plain, */*' \
  -H 'DNT: 1' \
  -H 'Content-Type: application/json;charset=UTF-8' \
  -H 'sec-ch-ua-mobile: ?0' \
  -H 'User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/96.0.4664.93 Safari/537.36' \
  -H 'sec-ch-ua-platform: "Windows"' \
  -H 'Origin: https://qa.digit.org' \
  -H 'Sec-Fetch-Site: same-origin' \
  -H 'Sec-Fetch-Mode: cors' \
  -H 'Sec-Fetch-Dest: empty' \
  -H 'Referer: https://qa.digit.org/digit-ui/employee/engagement/messages/inbox' \
  -H 'Accept-Language: en-US,en;q=0.9,hi;q=0.8' \
  --data-raw '{"RequestInfo":{"apiId":"Rainmaker"}}' \
  --compressed
```

### Create API

```
curl 'https://qa.digit.org/egov-user-event/v1/events/_create?_=1639369667873' \
  -H 'Connection: keep-alive' \
  -H 'sec-ch-ua: " Not A;Brand";v="99", "Chromium";v="96", "Google Chrome";v="96"' \
  -H 'Accept: application/json, text/plain, */*' \
  -H 'DNT: 1' \
  -H 'Content-Type: application/json;charset=UTF-8' \
  -H 'sec-ch-ua-mobile: ?0' \
  -H 'User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/96.0.4664.93 Safari/537.36' \
  -H 'sec-ch-ua-platform: "Windows"' \
  -H 'Origin: https://qa.digit.org' \
  -H 'Sec-Fetch-Site: same-origin' \
  -H 'Sec-Fetch-Mode: cors' \
  -H 'Sec-Fetch-Dest: empty' \
  -H 'Referer: https://qa.digit.org/digit-ui/employee/engagement/messages/response' \
  -H 'Accept-Language: en-US,en;q=0.9,hi;q=0.8' \
  --data-raw '{"events":[{"recepient":null,"source":"WEBAPP","eventType":"BROADCAST","tenantId":"pb.amritsar","description":"contect","name":"Message","eventDetails":{"documents":[],"fromDate":1639506540000,"toDate":1640284140000}}],"RequestInfo":{"apiId":"Rainmaker","authToken":"df875063-9b4e-4fc7-bad6-f80844a6b4ed"}}' \
  --compressed
```

### Update API

```
curl 'https://qa.digit.org/egov-user-event/v1/events/_update?_=1639369794800' \
  -H 'Connection: keep-alive' \
  -H 'sec-ch-ua: " Not A;Brand";v="99", "Chromium";v="96", "Google Chrome";v="96"' \
  -H 'Accept: application/json, text/plain, */*' \
  -H 'DNT: 1' \
  -H 'Content-Type: application/json;charset=UTF-8' \
  -H 'sec-ch-ua-mobile: ?0' \
  -H 'User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/96.0.4664.93 Safari/537.36' \
  -H 'sec-ch-ua-platform: "Windows"' \
  -H 'Origin: https://qa.digit.org' \
  -H 'Sec-Fetch-Site: same-origin' \
  -H 'Sec-Fetch-Mode: cors' \
  -H 'Sec-Fetch-Dest: empty' \
  -H 'Referer: https://qa.digit.org/digit-ui/employee/engagement/messages/response?update=true' \
  -H 'Accept-Language: en-US,en;q=0.9,hi;q=0.8' \
  --data-raw '{"events":[{"tenantId":"pb.amritsar","id":"4d888e56-be4d-45a0-b05c-f7939f544213","referenceId":null,"eventType":"BROADCAST","eventCategory":null,"name":"Message","description":"content","status":"ACTIVE","source":"WEBAPP","postedBy":"d0710c4c-728a-446d-bc7e-d4614efe1463","recepient":null,"actions":null,"eventDetails":{"documents":[],"fromDate":1639440000000,"toDate":1640217600000},"auditDetails":{"createdBy":"d0710c4c-728a-446d-bc7e-d4614efe1463","createdTime":1639369670687,"lastModifiedBy":"d0710c4c-728a-446d-bc7e-d4614efe1463","lastModifiedTime":1639369670687},"recepientEventMap":null,"generateCounterEvent":null,"internallyUpdted":null,"user":{"id":12074,"userName":"QAADMIN","salutation":null,"name":"FSM Admin","gender":"MALE","mobileNumber":"9966999999","emailId":null,"altContactNumber":null,"pan":null,"aadhaarNumber":null,"permanentAddress":null,"permanentCity":null,"permanentPinCode":null,"correspondenceAddress":null,"correspondenceCity":null,"correspondencePinCode":null,"alternatemobilenumber":null,"active":true,"locale":null,"type":"EMPLOYEE","accountLocked":false,"accountLockedDate":0,"fatherOrHusbandName":"Test","relationship":"FATHER","signature":null,"bloodGroup":null,"photo":null,"identificationMark":null,"createdBy":12011,"lastModifiedBy":1,"tenantId":"pb.amritsar","roles":[{"code":"FSM_VIEW_EMP","name":"FSM Employee Application Viewer","tenantId":"pb.amritsar"},{"code":"FSM_ADMIN","name":"FSM Administrator","tenantId":"pb.amritsar"},{"code":"EMPLOYEE","name":"Employee","tenantId":"pb.amritsar"},{"code":"FSM_REPORT_VIEWER","name":"FSM Employee Report Viewer","tenantId":"pb.amritsar"},{"code":"STADMIN","name":"State Administrator","tenantId":"pb.amritsar"},{"code":"EMPLOYEE ADMIN","name":null,"tenantId":"pb.amritsar"},{"code":"FSM_DASHBOARD_VIEWER","name":"FSM Employee Dashboard Viewer","tenantId":"pb.amritsar"}],"uuid":"d0710c4c-728a-446d-bc7e-d4614efe1463","createdDate":"15-02-2021 14:41:32","lastModifiedDate":"06-04-2021 14:58:43","dob":"1990-09-09","pwdExpiryDate":"16-05-2021 14:41:32"}}],"RequestInfo":{"apiId":"Rainmaker","authToken":"df875063-9b4e-4fc7-bad6-f80844a6b4ed"}}' \
  --compressed
```



> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)_​_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
