---
id: "1click_api_error_responses"
---

# Error Responses

If the request fails due to a missing, invalid, or mismatching redirection URI, or if the client identifier is missing or invalid, the authorization server SHOULD inform the resource owner of the error and MUST NOT automatically redirect the user-agent to the invalid redirection URI.

If the resource owner denies the access request or if the request fails for reasons other than a missing or invalid redirection URI, the authorization server informs the client by adding the following parameters to the query component of the redirection URI using the "application/x-www-form-urlencoded" format, per Appendix B:

| JSON params       | Type   | M/O | Description                                                                                                                                                     |
|-------------------|--------|-----|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| error             | String | M   | Error code. See all available codes below "List of available error code"                                                                                        |
| error_description | String | O   | Transaction status code. See all available codes at [States and Status Codes](../../configuration_and_administration/system_configuration/statesandstatuscodes) |
| tx_state          | String | O   | Transaction state. See all available state at [States and Status Codes](../../configuration_and_administration/system_configuration/statesandstatuscodes)       |
| state             | String | O   | If a "state" parameter was present in the client authorization request.  The exact value received from the client.                                              |
| errMsg            | String | O   | The exact same errMsg sent from sign in response by merchant, if available.                                                                                     |
| errCode           | String | O   | The exact same errCode sent from merchant, if available                                                                                                         |


## Example JSON Responses

```json
  {
    "error": "access_denied",
    "error_description": "err_not_authenticated"
  }
```

```json
 {
   "error": "access_denied",
   "error_description": "err_user_account_blocked",
   "errorMsg": "User has self excluded himself",
   "errCode": "1001"
 }
```

## Example Redirect HTTP Response

For example, the authorization server redirects the user-agent by
sending the following HTTP response:

```curl
HTTP/1.1 302 Found
Location: https://client.example.com/cb?error=access_denied&state=xyz
```


## List of available error code

| Code                      | Description                                                                                                                                                                                                                                                            |
|---------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| access_denied             | The resource owner or authorization server denied the                                                                                                                                                                                                                  |
| invalid_request           | The request is missing a required parameter, includes an invalid parameter value, includes a parameter more than once, or is otherwise malformed.                                                                                                                      |
| unauthorized_client       | The client is not authorized to request an authorization code using this method.                                                                                                                                                                                       |
| unsupported_response_type | The authorization server does not support obtaining an authorization code using this method.                                                                                                                                                                           |
| invalid_scope             | The requested scope is invalid, unknown, or malformed.                                                                                                                                                                                                                 |
| server_error              | The authorization server encountered an unexpected condition that prevented it from fulfilling the request. (This error code is needed because a 500 Internal Server Error HTTP status code cannot be returned to the client via an HTTP redirect.)                    |
| temporarily_unavailable   | The authorization server is currently unable to handle the request due to a temporary overloading or maintenance of the server.  (This error code is needed because a 503 Service Unavailable HTTP status code cannot be returned to the client via an HTTP redirect.) |