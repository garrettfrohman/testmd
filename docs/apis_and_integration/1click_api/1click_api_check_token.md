---
id: "1click_api_check_token"
---

# Check Token

This method is called by the operator to verify the jwt token is valid. It can be used for a clustered environment where re-verification of the token is required. 

This endpoint is protected by default and only allowed if the end-user has authenticated successfully at the identity provider. Please note that if the operator uses Global Identity Integrator then they will do a call against SPAR that will be invoiced the operator. This endpoint uses basic authentication. 

If your library doesn’t support Basic authentication, you can manually add it by supplying the Authorization HTTP header with the string Basic followed by a space and a base64 encoded string containing your `client_id:client_secret` combination. 

:::info Example Authorization:

`Basic Y2E0YWNiODY5ZjYwNDU1NWFlNTdlYTkzM2FiZDZhNjU6NTFhYjRlNjdiZWNhNDVkYjgzZTE2YzM0NDdmNjFiOTY=` . 

Please note that this is an example authorization for PaymentIQs test client.
:::


`GET/oauth/check_token`

## Example Request

```curl
curl -X GET 'https://test-api.paymentiq.io/paymentiq/oauth/check_token?token=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJhZGRyZXNzIjoiS2xpbnRhIDk0IiwiY2l0eSI6Ik1hcmlhbm5lbHVuZCIsInVzZXJfbmFtZSI6IlRFU1RfRVVSIiwiZGVzY3JpcHRvciI6IioqNjk4MzE2IiwiYXV0aG9yaXRpZXMiOlsiUk9MRV9JREVOVElUWV9BVVRIIl0sImNsaWVudF9pZCI6IjkwOGQ4NWUxOTFkMDQ4NmQ5N2JkNzc1MWE3NTRlMTI4IiwiemlwY29kZSI6IjU3MCAzMCIsImF1ZCI6WyJiYWNrb2ZmaWNlX2FwaSIsImlkZW50aXR5X2FwaSJdLCJiYW5rIjoiU3dlZGJhbmsiLCJjbGVhcmluZ2hvdXNlIjoiU1dFREVOIiwic2NvcGUiOlsiZGVmYXVsdCJdLCJuYW1lIjoiQXJtYW4gSGFuc3NvbiIsInBlcnNvbmlkIjoiU0UxOTkxMTAyODQ0NzkiLCJleHAiOjE1MjI4MzM2MDksImxhc3RkaWdpdHMiOiI2OTgzMTYiLCJqdGkiOiI2MzdmMGFmYS0wZTgwLTQ4NmQtYjA2My1kMTM3NDhiMjg3M2YifQ.6w1MqK8df5mc7rQyVy8C4ImAOikX6U-AjeDQKMUJX6M' -H 'Authorization: Basic ZGZiMmVkNDVlZDhiNDY5ZjhiNGE5NTBlYzk2ZjM5NzY6NDYzMTU4MWE5OGEzNGFhNTg4ZDk5Y2JlMzE5NjM3ZGY='
```

## Request Parameters

| Name  | Located ln | Description                                              | Schema | Required |
|-------|------------|----------------------------------------------------------|--------|----------|
| token | query      | Access token returned from the token retrieval endpoint. | string | true     |

## Example response

```json
{
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
  ],
  "veriff_verification_false": "false",
  "veriff_verification_failed_reason": "empty"
}
```

## Response Body Parameters

| Name                              | Description                                                                                                                   | Schema  | Required |
|-----------------------------------|-------------------------------------------------------------------------------------------------------------------------------|---------|----------|
| scope                             | Allowed scopes for this client, currently is always returned as default                                                       | array   | true     |
| userId                            | Merchant's user id.                                                                                                           | string  | true     |
| merchantId                        | Merchant id.                                                                                                                  | integer | true     |
| clientId                          | Merchant API Client                                                                                                           | string  | true     |
| txRefId                           | Transaction reference id. Formatted as ##A## [merchantId A transaction id]                                                    | string  | true     |
| name                              | End user full name.                                                                                                           | string  | true     |
| firstName                         | End user first name                                                                                                           | string  | true     |
| lastName                          | End user last name                                                                                                            | string  | true     |
| personid                          | End user person id formatted as ## ########-##### two letter ISO country code + date of birth + last 4 digits                 | string  | true     |
| street                            | End user address                                                                                                              | string  | true     |
| city                              | End user city                                                                                                                 | string  | true     |
| zip                               | End user zip code                                                                                                             | string  | true     |
| country                           | End user country code in 3 letter ISO code.                                                                                   | string  | true     |
| dob                               | End user date of birth formatted as ####-##-##                                                                                | string  | true     |
| ip                                | End user ip address                                                                                                           | string  | true     |
| identityProvider                  | Identity provider used for the end user to authenticate                                                                       | string  | true     |
| exp                               | Expiration of the token, number of seconds                                                                                    | integer | true     |
| jti                               | Unique identifier of the token, currently not used for anything.                                                              | string  | true     |
| aud                               | Resources available for the API client                                                                                        | array   | true     |
| veriff_verification_false         | String that contains verification results from Veriff. Is set even if the user didnt use Veriff. Can be empty, true or false. | string  | true     |
| veriff_verification_failed_reason | String that contains failed reason from Veriff. Is set even if the user didnt use Veriff.                                     | string  | true     |