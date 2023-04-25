---
id: "1click_api_token_retrieval"
---

# Token Retrieval

This method is called by the Operator Platform to PaymentIQ when end-user has been redirected back to the Operator redirect_url with the one-time authorization_code. As a result, an access_token will be returned which signifies that the end-user is now properly authenticated. 

This endpoint is protected by default and only allowed if the end-user has authenticated successfully at the identity provider. This endpoint uses basic authentication. If your library doesn’t support Basic authentication, you can manually add it by supplying the Authorization HTTP header with the string Basic followed by a space and a base64 encoded string containing your `client_id:client_secret` combination. 

:::info Example Authorization:

`Basic Y2E0YWNiODY5ZjYwNDU1NWFlNTdlYTkzM2FiZDZhNjU6NTFhYjRlNjdiZWNhNDVkYjgzZTE2YzM0NDdmNjFiOTY=`. 

Please note that this is an example authorization for PaymentIQs test client.
:::

`POST /oauth/token`

## Example Request

```curl
curl -X POST 'https://test-api.paymentiq.io/paymentiq/oauth/token?grant_type=authorization_code&code=dEd234&redirect_uri=https://www.getpostman.com/oauth2/callback&client_id=908d85e191d0486d97bd7751a754e128'  -H 'Authorization: Basic Y2E0YWNiODY5ZjYwNDU1NWFlNTdlYTkzM2FiZDZhNjU6NTFhYjRlNjdiZWNhNDVkYjgzZTE2YzM0NDdmNjFiOTY=' -i
```

## Request Parameters

| Name         | Located ln   | Description                                                            | Schema | Required |
|--------------|--------------|------------------------------------------------------------------------|--------|----------|
| code         | request body | The authorization code received from the initial authorize call.       | string | true     |
| grant_type   | request body | This must be authorization_code.                                       | string | true     |
| redirect_uri | request body | The URL must match exactly the redirect_uri passed to /oauth/authorize | string | false    |

## Example response

```json
{
  "access_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJsYXN0TmFtZSI6IkhhbnNzb24iLCJjb3VudHJ5IjoiU1dFIiwiY2l0eSI6Ik1hcmlhbm5lbHVuZCIsInVzZXJfbmFtZSI6IlRFU1RfRVVSIiwiaWRlbnRpdHlQcm92aWRlciI6IlRSVVNUTFkiLCJjbGllbnRfaWQiOiI5MDhkODVlMTkxZDA0ODZkOTdiZDc3NTFhNzU0ZTEyOCIsImJhbmsiOiJTd2VkYmFuayIsIm1lcmNoYW50SWQiOjEwMDAsImNsZWFyaW5naG91c2UiOiJTV0VERU4iLCJzdHJlZXQiOiJLbGludGEgOTQiLCJzY29wZSI6WyJkZWZhdWx0Il0sInBlcnNvbmlkIjoiU0UxOTkxMTAyODQ0NzkiLCJleHAiOjE1MjYxMzkwNjUsImp0aSI6IjhlYzY0Yzg1LTQxNDgtNDg0Yy1iY2E1LWYwNzNiYzMxODFiYiIsInppcCI6IjU3MCAzMCIsInR4UmVmSWQiOiIxMDAwQTI1OTM4MyIsImlwIjoiMTI3LjAuMC4xIiwibWFza2VkQWNjb3VudCI6IioqNjk4MzE2IiwidXNlcklkIjoiVEVTVF9FVVIiLCJhdXRob3JpdGllcyI6WyJST0xFX0lERU5USVRZX0FVVEgiXSwiZmlyc3ROYW1lIjoiQXJtYW4iLCJhdWQiOlsiYmFja29mZmljZV9hcGkiLCJpZGVudGl0eV9hcGkiXSwiZG9iIjoiMTk5MS0xMC0yOCIsIm5hbWUiOiJBcm1hbiBIYW5zc29uIiwiYXR0cmlidXRlcyI6eyJsYW5ndWFnZSI6ImVuIiwiYnJhbmRfaWQiOiJjYXNpbm9oZXJvZXMiLCJ0b2tlbiI6ImV5SmhiR2NpT2lKSVV6STFOaUo5LmV5SnRaWEpqYUdGdWRFbGtJam94TURBd0xDSmxlSEFpT2pFMU1qTTFORGszTlRFc0luUnZhMlZ1SWpvaU1UQXdNRUV5TlRrek9ETWlmUS5Xdy1Ja3F6SHliRlk0TXZwb3hKTlJNMHRZOC1ldFFIZ3BRQUswSTgxdXFBIn0sImxhc3RkaWdpdHMiOiI2OTgzMTYifQ.rW3b6YGRLCCRw340y-i31lHcI3q0RCMOCCXKGIXeh4c",
  "token_type": "bearer",
  "expires_in": 2591999,
  "scope": [
    "default"
  ],
  "userId": "123456",
  "merchantId": 1000,
  "clientId": "Example",
  "txRefId": "1000A258804",
  "name": "Arman Hansson",
  "firstName": "Arman",
  "lastName": "Hansson",
  "personid": "SE199110284479",
  "street": "Klinta 94",
  "city": "Mariannelund",
  "zip": "570 30",
  "country": "SWE",
  "dob": "1991-10-28",
  "ip": "127.0.0.1",
  "identityProvider": "trustly",
  "exp": 1525394791,
  "jti": "35d2fa6b-ae5b-4df6-8c9c-5bfc54d644a8",
  "aud": [
    "identity_api"
  ]
}
```

## Response Body Parameters

| Name             | Description                                                                                                   | Schema  | Required |
|------------------|---------------------------------------------------------------------------------------------------------------|---------|----------|
| access_token     | access token                                                                                                  | string  | true     |
| token_type       | Type of token used will always be set to bearer                                                               | string  | true     |
| expires_in       | How long the token is valid in seconds                                                                        | integer | true     |
| scope            | Allowed scopes for this client, currently is always returned as default                                       | array   | true     |
| userId           | Merchant's user id.                                                                                           | string  | true     |
| merchantId       | Merchant id.                                                                                                  | integer | true     |
| clientId         | Merchant API Client                                                                                           | string  | true     |
| txRefId          | Transaction reference id. Formatted as ##A## [merchantId A transaction id]                                    | string  | true     |
| name             | End user full name.                                                                                           | string  | true     |
| firstName        | End user first name                                                                                           | string  | true     |
| lastName         | End user last name                                                                                            | string  | true     |
| personid         | End user person id formatted as ## ########-##### two letter ISO country code + date of birth + last 4 digits | string  | true     |
| street           | End user address                                                                                              | string  | true     |
| city             | End user city                                                                                                 | string  | true     |
| zip              | End user zip code                                                                                             | string  | true     |
| country          | End user country code in 3 letter ISO code.                                                                   | string  | true     |
| dob              | End user date of birth formatted as ####-##-##                                                                | string  | true     |
| ip               | End user ip address                                                                                           | string  | true     |
| identityProvider | Identity provider used for the end user to authenticate                                                       | string  | true     |
| exp              | Expiration of the token                                                                                       | integer | true     |
| jti              | Unique identifier of the token, currently not used for anything.                                              | string  | true     |
| aud              | Resouces available for the API client                                                                         | array   | true     |