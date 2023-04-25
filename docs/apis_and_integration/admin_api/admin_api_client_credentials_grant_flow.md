---
id: "admin_api_client_credentials_grant_flow"
---

# Client Credentials Grant Flow

The authentication in the Admin API is done with OAuth 2.0 and Client Credentials grant flow. Detailed information on this flow can be found in the [auth0 documentation](https://auth0.com/docs/get-started/authentication-and-authorization-flow/client-credentials-flow).

The client sends a POST request with the Authorization header with the base64 encoded `[clientId:clientSecret]`

The authorization server will respond with a JSON object containing the following properties:

* token_type with the value Bearer
* expires_in with an integer representing the TTL of the access token
* access_token the access token itself

# Example Request

```curl
curl -X POST \
  'https://test-api.paymentiq.io/paymentiq/oauth/token?grant_type=client_credentials' \
  -H 'Authorization: Basic Y2E0YWNiODY5ZjYwNDU1NWFlNTdlYTkzM2FiZDZhNjU6NTFhYjRlNjdiZWNhNDVkYjgzZTE2YzM0NDdmNjFiOTY=' \
  -H 'Cache-Control: no-cache' \
  -H 'Postman-Token: 99acc480-31b7-4e76-9e91-5db5b38b4560' -i
```

# Example Response

```json
{
  "access_token" : "REDACTED",
  "expires_in" : 7200,
  "refresh_expires_in" : 3900,
  "refresh_token" : "REDACTED",
  "token_type" : "bearer",
  "not-before-policy" : 1623240044,
  "session_state" : "33f303f5-c0f4-43b4-a2e3-d24c22b1063b",
  "scope" : "email address profile paymentiq phone"
}
```