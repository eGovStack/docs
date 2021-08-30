# User Session Management In DIGIT

![](../../../../.gitbook/assets/user-session.png)

Whenever any user logs an authorization token and a refresh token is generated for him. Using the auth token the client can make rest API calls to the server to fetch data. The auth token has an expiry period. Once the auth token is expired it cannot be used to make API calls. The client will have to generate a new authorization token. This is done by authenticating the refresh token with the server which then generates and sends new authorization token to the client. The refresh token avoids the need for the client to again login whenever Auth token expires.

Refresh token also has an expiry period and once it gets expired it cannot be used to generate new authorization token and the user will have to login again to get a new pair of authorization token and refresh token. Generally, the duration before the expiry of the refresh token is much longer compared to that of auth token. If the user logs out of the account both Auth token and the refresh token will become invalid.

## Environment variables to configure expiry time <a id="Environment-variables-to-configure-expiry-time:"></a>

| **Param** | **Description** |
| :--- | :--- |
| access.token.validity.in.minutes | Duration in minutes for which the authorization token is valid |
| refresh.token.validity.in.minutes | Duration in minutes for which the refresh token is valid |

## API <a id="API:"></a>

| **API** | **Description** |
| :--- | :--- |
| /user/oauth/token | Used to start the session by generating Auth token and refresh token from username and password using grant\_type as password. The same API can be used to generate new auth token from refresh token by using grant\_type as refresh\_token and sending the refresh token with key refresh\_token |
| /user/\_logout | This API is used to end the session. The access token and refresh token will become invalid once this API is called. Auth token is sent as param in the API call |

\`

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation ](https://egov.org.in/)is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).

