---
id: "front_api_introduction"
---

# Front API Introduction

The PaymentIQ Front-End API is organized around REST and uses JSON, [http://en.wikipedia.org/wiki/JSON](http://en.wikipedia.org/wiki/JSON) for all data interchange. It is language independent and supported for virtually all programming languages. The API expects all requests and responses to be UTF-8 encoded.

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
