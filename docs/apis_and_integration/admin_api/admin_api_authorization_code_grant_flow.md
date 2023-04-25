---
id: "admin_api_authorization_code_grant_flow"
---

# Authorization Code Grant Flow

# The Flow (Part One)

The client sends a POST request with following body parameters to the authorization server:

* response_type with the value code
* client_id with the client identifier
* redirect_uri with the client redirect URI. This parameter is optional, but if not send the user will be redirected to a pre-registered redirect URI.
* state with a CSRF token. This parameter is optional but highly recommended. You should store the value of the CSRF token in the user’s session to be validated when they return.
* iframe with true or false. This parameter will either perform a full redirect or return a redirectOutput
* identity_provider with the identity provider to use e.g trustly, gii-bankid-se.

All of these parameters will be validated by the authorization server.
The user will then be asked to login to the authorization server and approve the client.
If the user approves the client they will be redirected from the authorisation server back to the client (specifically to the redirect URI) with the following parameters in the query string:
* code with the authorization code
* state with the state parameter sent in the original request. You should compare this value with the value stored in the user’s session to ensure the authorization code obtained is in response to requests made by this client rather than another client application.

# Example Request

```curl
curl -X GET \
  'http://localhost:8080/paymentiq/oauth/authorize?identity_provider=trustly&iframe=true&mock_user=TEST_EUR&country=SE&response_type=code&state=1234213123&client_id=908d85e191d0486d97bd7751a754e128&scope=default&redirect_uri=https%3A%2F%2Fwww.getpostman.com%2Foauth2%2Fcallback' \
  -H 'Cache-Control: no-cache' \
  -H 'Postman-Token: 78a98323-a43c-4e37-83e6-855d659a727a'
```

# Example Response

```json
{
    "redirectOutput": {
        "html": null,
        "url": "https://test.trustly.com/_/orderclient.php?SessionID=23f6f3c9-66f5-4b7e-b250-395cc12d74c0&OrderID=3769297577&Locale=sv_SE",
        "method": "GET",
        "container": "iframe",
        "parameters": {},
        "height": 750,
        "width": 600
    },
    "messages": [],
    "links": {
        "statusUrl": "http://localhost:8080/paymentiq/api/signin/status?token=eyJhbGciOiJIUzI1NiJ9.eyJtZXJjaGFudElkIjoxMDAwLCJleHAiOjE1MjM1NDk1NzYsInRva2VuIjoiMTAwMEEyNTkzODAifQ.vDffOoxd3xY7XTnr9BOiP1bbCYL3uIPHR-oys0alBPM"
    },
    "success": true
}
```

# The Flow (Part Two)

The client will now send a POST request to the authorization server with the following parameters:
* grant_type with the value of authorization_code
* client_id with the client identifier
* client_secret with the client secret
* redirect_uri with the same redirect URI the user was redirect back to
* code with the authorization code from the query string

The authorization server will respond with a JSON object containing the following properties:
* token_type this will usually be the word “Bearer” (to indicate a bearer token)
* expires_in with an integer representing the TTL of the access token (i.e. when the token will expire)
* access_token the access token itself
* refresh_token a refresh token that can be used to acquire a new access token when the original expires

# Example Request

```curl
curl -X POST \
  'https://test-api.paymentiq.io/paymentiq/oauth/token?grant_type=authorization_code&code=dEd234&redirect_uri=https://www.getpostman.com/oauth2/callback&client_id=908d85e191d0486d97bd7751a754e128' \
  -H 'Authorization: Basic Y2E0YWNiODY5ZjYwNDU1NWFlNTdlYTkzM2FiZDZhNjU6NTFhYjRlNjdiZWNhNDVkYjgzZTE2YzM0NDdmNjFiOTY=' \
  -H 'Cache-Control: no-cache' \
  -H 'Postman-Token: 99acc480-31b7-4e76-9e91-5db5b38b4560' -i
```

# Example Response

```json
{
  "access_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJsYXN0TmFtZSI6IkhhbnNzb24iLCJjb3VudHJ5IjoiU1dFIiwiY2l0eSI6Ik1hcmlhbm5lbHVuZCIsInVzZXJfbmFtZSI6IlRFU1RfRVVSIiwiaWRlbnRpdHlQcm92aWRlciI6IlRSVVNUTFkiLCJjbGllbnRfaWQiOiI5MDhkODVlMTkxZDA0ODZkOTdiZDc3NTFhNzU0ZTEyOCIsImJhbmsiOiJTd2VkYmFuayIsIm1lcmNoYW50SWQiOjEwMDAsImNsZWFyaW5naG91c2UiOiJTV0VERU4iLCJzdHJlZXQiOiJLbGludGEgOTQiLCJzY29wZSI6WyJkZWZhdWx0Il0sInBlcnNvbmlkIjoiU0UxOTkxMTAyODQ0NzkiLCJleHAiOjE1MjYxMzkwNjUsImp0aSI6IjhlYzY0Yzg1LTQxNDgtNDg0Yy1iY2E1LWYwNzNiYzMxODFiYiIsInppcCI6IjU3MCAzMCIsInR4UmVmSWQiOiIxMDAwQTI1OTM4MyIsImlwIjoiMTI3LjAuMC4xIiwibWFza2VkQWNjb3VudCI6IioqNjk4MzE2IiwidXNlcklkIjoiVEVTVF9FVVIiLCJhdXRob3JpdGllcyI6WyJST0xFX0lERU5USVRZX0FVVEgiXSwiZmlyc3ROYW1lIjoiQXJtYW4iLCJhdWQiOlsiYmFja29mZmljZV9hcGkiLCJpZGVudGl0eV9hcGkiXSwiZG9iIjoiMTk5MS0xMC0yOCIsIm5hbWUiOiJBcm1hbiBIYW5zc29uIiwiYXR0cmlidXRlcyI6eyJsYW5ndWFnZSI6ImVuIiwiYnJhbmRfaWQiOiJjYXNpbm9oZXJvZXMiLCJ0b2tlbiI6ImV5SmhiR2NpT2lKSVV6STFOaUo5LmV5SnRaWEpqYUdGdWRFbGtJam94TURBd0xDSmxlSEFpT2pFMU1qTTFORGszTlRFc0luUnZhMlZ1SWpvaU1UQXdNRUV5TlRrek9ETWlmUS5Xdy1Ja3F6SHliRlk0TXZwb3hKTlJNMHRZOC1ldFFIZ3BRQUswSTgxdXFBIn0sImxhc3RkaWdpdHMiOiI2OTgzMTYifQ.rW3b6YGRLCCRw340y-i31lHcI3q0RCMOCCXKGIXeh4c",
  "token_type":"bearer",
  "expires_in": "2591999",
  "scope":"default",
  "userId": "TEST_EUR",
  "merchantId": 1000,
  "clientId": "908d85e191d0486d97bd7751a754e128",
  "txRefId": "1000A258804",
  "authorities": [
    "ROLE_IDENTITY_AUTH"
  ],
  "name": "Arman Hansson",
  "firstName": "Arman",
  "lastName": "Hansson",
  "personid": "SE199110284479",
  "street": "Klinta 94",
  "city": "Mariannelund",
  "zip": "570 30",
  "country": "SWE",
  "dob": "1991-10-28",
  "clearinghouse": "SWEDEN",
  "bank": "Swedbank",
  "maskedAccount": "**698316",
  "lastdigits": "698316",
  "ip": "127.0.0.1",
  "identityProvider": "TRUSTLY",
  "attributes": {
    "test2": "test3",
    "test": "test2"
  },
  "scope": [
    "default"
  ],
  "exp": 1525394791,
  "jti": "35d2fa6b-ae5b-4df6-8c9c-5bfc54d644a8",
  "aud": [
    "identity_api"
  ]
}
```