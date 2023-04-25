---
id: "admin_api_authentication"
---

# Authentication

The authentication in the Admin API is done with OAuth 2.0 and Client Credentials grant flow. The Client Credentials flow is described in more detail in the [next chapter](./admin_api_client_credentials_grant_flow).

To get started you need to register an API client under ```Admin > API clients``` in the PaymentIQ back office. Chapter [Create API Client](./create_api_client) describes this in more detail. Only back office users with merchant admin role are allowed to setup clients. A registered client is assigned an unique ```Client Id``` and ```Client Secret``` which will be used in the OAuth 2.0 flow. The client secret should not be shared.

To request an access token, provide a base64 encoded ```[clientId:clientSecret]``` in the authorization header.

```curl
curl -X POST 'https://test-bo.paymentiq.io/paymentiq/oauth/token?grant_type=client_credentials' -H 'authorization: Basic YzU3YTNlOTlkODAzNDE4Njh' -H 'content-type: application/x-www-form-urlencoded'
```

To make an API request provide your bearer token in the authorization header.

```curl
curl -X GET 'https://test-bo.paymentiq.io/paymentiq/admin/v1/payments?merchantId=100101999&limit=10' -H 'authorization: Bearer xxxx.xxxx.xxxxx' -H 'content-type: application/json' \ -d '{ "limit": 10 }'
```

To issue a new ```access_token``` if expired, provide your ```refresh_token```.

```curl
curl -X POST 'https://test-bo.paymentiq.io/paymentiq/oauth/token?grant_type=refresh_token&refresh_token=xxx.xxxx.xxxx' -H 'authorization: Basic RDBHNlpLSFVHSjJWV0'
```
