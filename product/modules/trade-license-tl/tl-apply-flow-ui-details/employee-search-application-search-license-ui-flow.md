# Employee Search Application Search License UI Flow

Search Application and Search License pages are used for searching any application/ license that may or may not be relevant to the workflow action of the logged-in users.

Search Application has 2 components.

## Search Fields

Search field component is a form which takes inputs and pass it into tl-search api params. It utilizes SearchForm and SearchField component to create and arrange the form.

![](../../../../.gitbook/assets/image%20%28242%29.png)

## Result Table

Result Table uses Table react component and the result from api is adapted to the table config using a custom hook inside common parent wrapper and passing the response to individual components

![](../../../../.gitbook/assets/image%20%28184%29.png)

Search License has fixed param where the status of the application is _“APPROVED”_, other than differences in table config

## APIs

API end point for searching trade licenses is `{env}/tl-services/v1/_search`

API CURL -

```text
curl 'https://qa.digit.org/tl-services/v1/_search?tenantId=pb.amritsar&fromDate=1625077800000&toDate=1627410599000&limit=10&sortBy=commencementDate&sortOrder=DESC&status=APPROVED&_=1627375567840' \
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
  -H 'referer: https://qa.digit.org/digit-ui/employee/tl/search/license' \
  -H 'accept-language: en-US,en;q=0.9,hi;q=0.8' \
  --data-raw '{"RequestInfo":{"apiId":"Rainmaker","authToken":"18158d2b-0a50-4a60-baa3-a83c157e7aad"}}' \
  --compressed
```



