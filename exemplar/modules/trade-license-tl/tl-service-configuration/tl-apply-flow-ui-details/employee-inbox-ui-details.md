# Employee Inbox UI Details

Inbox page is constituted out of 4 react components:-

## ApplicationLinks

ApplicationLinks is a separate component that hold links to other pages of possible navigation from inbox. This component is common in both Mobile and Desktop view. Links are conditionally rendered according to the user roles

![](<../../../../../.gitbook/assets/image (127).png>)

## SearchApplication

Search Application component is a form based component, that controls the Table component and the search param for Inbox API, it uses FormComposer HOC to render fields.

Validation of these fields are achieved by using controlled component rules

![](<../../../../../.gitbook/assets/image (244).png>)

Any number of search fields can be added but by convention, only mobile numbers and appilication numbers are provided

## Filters

Filters contain input fields to filter the result of api, by sending search params to inbox api.

It contains 3 sections

1. Assigned to Me/ All - It is a radio component to send assignedToMe param as _true_ or _false_
2. Locality - Filter result according to the selected locality by sending locality code in moduleSearch params in inbox api
3. Status - Status filters are achieved by sending id received from inbox api response and mapping the name of businessService, status name and count

![](<../../../../../.gitbook/assets/image (118) (1).png>)

## Table

Table is a react component which uses React-Table plugin, used in multiple modules

![](<../../../../../.gitbook/assets/image (116).png>)

However in Mobile view are using cards to list all the applications without pagination support

## APIs

On Inbox page {env}[/inbox/v1/\_search?\_=1627374959930](https://qa.digit.org/inbox/v1/\_search?\_=1627374959930) is the only API that is called.

API CURL -

```
curl 'https://qa.digit.org/inbox/v1/_search?_=1627374959930' \
  -H 'authority: qa.digit.org' \
  -H 'sec-ch-ua: " Not;A Brand";v="99", "Google Chrome";v="91", "Chromium";v="91"' \
  -H 'accept: application/json, text/plain, */*' \
  -H 'dnt: 1' \
  -H 'sec-ch-ua-mobile: ?0' \
  -H 'user-agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/91.0.4472.114 Safari/537.36' \
  -H 'content-type: application/json;charset=UTF-8' \
  -H 'origin: https://qa.digit.org' \
  -H 'sec-fetch-site: same-origin' \
  -H 'sec-fetch-mode: cors' \
  -H 'sec-fetch-dest: empty' \
  -H 'referer: https://qa.digit.org/digit-ui/employee/tl/inbox' \
  -H 'accept-language: en-US,en;q=0.9,hi;q=0.8' \
  --data-raw '{"inbox":{"tenantId":"pb.amritsar","processSearchCriteria":{"moduleName":"tl-services","businessService":["NewTL","DIRECTRENEWAL","EDITRENEWAL"]},"moduleSearchCriteria":{"sortBy":"applicationDate","sortOrder":"ASC"},"limit":10,"offset":0},"RequestInfo":{"apiId":"Rainmaker","authToken":"18158d2b-0a50-4a60-baa3-a83c157e7aad","userInfo":{"id":12032,"uuid":"4dc1010d-4b31-4b31-a596-cec2986ac04c","userName":"QATLA","name":"Sham","mobileNumber":"9999999934","emailId":null,"locale":null,"type":"EMPLOYEE","roles":[{"name":"TL Approver","code":"TL_APPROVER","tenantId":"pb.amritsar"}],"active":true,"tenantId":"pb.amritsar","permanentCity":null}}}' \
  --compressed
```
