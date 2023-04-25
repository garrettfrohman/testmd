---
id: "admin_api_introduction"
---

# Admin API  Introduction

The Admin API is used to administrate and perform actions surrounding transactions and user account actions.

To get started there are certain steps that needs to be taken. First you need to register an API Client which is described in the [authentication section](./admin_api_authentication). This client is used for the OAuth 2.0 authentication of the Admin API.

The Admin API is organized around REST and uses JSON, http://en.wikipedia.org/wiki/JSON, for all data interchange. It is language independent and supported for virtually all programming languages. The API expects all requests and responses to be UTF-8 encoded. Localization is controlled by the request header ```i18n```.

The API parameters are organized using following JSON structure:

```json
{
  "param1": "value1",
  "param2": "value2",
  "param3": {
    "param4": "value3",
    "param5": true
  }
}
```

For example:

```json
{
  "merchantId": "1",
  "sessionId": "HT04D1QAAAAABQDGPM5QAAA",
  "userId": "123456",
  "attributes": {
    "bonusCode": "A123",
    "channelId": "mobile"
  }
}
```

