---
id: "1click_api_authorization"
---

# Authorization

Used to initiate authentication of the end-user.

The authorization code flow begins with the client directing the user to the /authorize endpoint. In this request, the client indicates the permissions it needs to acquire from the user. Please note that PaymentIQ always return HTML when using Devcode Identity as identity provider. See more under each provider.

`GET/oauth/authorize`

## Example Request

```curl
curl -X GET 'https://test-api.paymentiq.io/paymentiq/oauth/authorize?client_id=changeme&identity_provider=[provider]&country=SE&redirect_uri=https://www.getpostman.com/oauth2/callback&locale=sv_SE&attributes[user_type]=beginner' -i -L
```

## Request Parameters

| Name                | Located ln | Description                                                                                                                                                                                                                                                                                                                                                                                  | Schema  | Required |
|---------------------|------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------|----------|
| client_id           | query      | Registered client id. You will probably only use one client_id per environment.                                                                                                                                                                                                                                                                                                              | string  | true     |
| redirect_uri        | query      | URL to redirect to when user has been authorized. The URL must match exactly the redirect_uri configured on the API client in PaymentIQ backoffice. NOTE! You should not URL encode this uri.                                                                                                                                                                                                | string  | true     |
| identity_provider   | query      | The identity provider to authenticate against. Valid values are gii-bankid-se, gii-bankid-no, gii-nemid, gii-yoti, gii-veriff, gii-sumsub, gii-eutellerid, gii-smartid, gii-verimi, trustly, zimpler                                                                                                                                                                                         | string  | true     |
| amount              | query      | Requested transaction amount, formatted in ##.## 100.50 (only digits and dot as decimal separator). Required if you want to use the 1-click deposit flow.                                                                                                                                                                                                                                    | string  | false    |
| currency            | query      | The currency of the end-user's account in the merchant's system. Example EUR and SEK.                                                                                                                                                                                                                                                                                                        | string  | false    |
| country             | query      | The ISO 3166-1-alpha-2 code of the end-user's country. This will be used for preselecting the correct country for the end-user in the iframe.                                                                                                                                                                                                                                                | string  | false    |
| ssn                 | query      | The end-user’s social security number. If a swedish personid is provided, it will be pre-filled when the user logs in to their bank. Will also be sent to Devcode Identity as part of claims query string.                                                                                                                                                                                   | string  | false    |
| enduser_id          | query      | ID, username, hash or anything uniquely identifying the end-user to be identified. If not provided PaymentIQ will random generate one. NOTE! this is required when using Devcode Identity Sum & substance. This information should not be anything sensitive since it could be sent in clear text. If you want to use a username or email address you need to hash it before.                | string  | false    |
| iframe              | query      | Set if you want to use iframe. Use false if you want to do full redirect where PaymentIQ will redirect to the Identity provider, use true if you want to handle the redirect. False will return HTML and true will return JSON. True is default. For Devcode Identity this value is ignored, instead you should use display=popup. We are always returning HTML when using Devcode Identity. | boolean | false    |
| locale              | query      | The end-user’s localization preference in the ISO 639-1 code and territory the ISO 3166-1-alpha-2 code.                                                                                                                                                                                                                                                                                      | string  | false    |
| display             | query      | Optional value of 'popup' if you want Devcode Identity to be used in an iframe, if the merchant are using an iframe he will need to implement handling for postmessages, see https://developer.gii.cloud/api/oauth2/#iframe                                                                                                                                                                  | string  | false    |
| ui_friendly         | query      | Optional value for a created UI configuration in Devcode Identity                                                                                                                                                                                                                                                                                                                            | string  | false    |
| ui_id               | query      | Optional value for Devcode Identity, ID of a created UI configuration. Used instead of ui_friendly                                                                                                                                                                                                                                                                                           | string  | false    |
| nonce               | query      | Optional value for Devcode Identity. Placed in the ID token when a login is complete. Can be used for user migration/matching.                                                                                                                                                                                                                                                               | string  | false    |
| attributes          | query      | Optional attributes to be included in the signin notification sent to merchant platform. Set this as an array for example attributes[user_type]=beginner or attributes[key]=value                                                                                                                                                                                                            | string  | false    |
| provider_attributes | query      | Optional provider attributes to be included in call sent to Identity provider. Set this as an array for example provider_attributes[user_type]=beginner or provider_attributes[key]=value, this is then sent to the Identity provider as &userType=beginner&key=Value. NOTE! works only for Devcode Identity.                                                                                | string  | false    |

## Example response

```json
{
  "success": "true",
  "redirectOutput": {
    "html": "",
    "url": "https://test.trustly.com/_/orderclient.php?SessionID=bcb3ab4c-daa4-42da-8f19-36f4b3e0c109&OrderID=1103124092&Locale=",
    "method": "GET",
    "container": "iframe",
    "parameters": "",
    "height": 750,
    "width": 600
  },
  "message": []
}
```

## Response Body Parameters

| Name           | Description                                                                                                                                                                                                         | Schema  | Required |
| -------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------- | -------- |
| success        | Flag if the transaction was successful or not. The the flag is false then the property errors is also populated.                                                                                                    | boolean | true     |
| redirectOutput | If this property is set then the user must be redirected to a page provided by the provider in order to complete the transaction, e.g. a credit card deposit with 3D secure. See below for how to redirect the user | object  | true     |
| message        | If success: true and the no redirect parameter is defined then the transaction was successfully completed. This property contains messages that can be displayed to the user.                                       | array   | true     |
| errors         | If success: false then transaction was not successfully completed. This property contains one or more error messages.                                                                                               | array   | true     |