---
id: "1click_api_luxonpay"
---

# LuxonPay Flow And Configuration

## Requirements
The merchant must have an account activated in the LuxonPay platform. The credentials should be added in LuxonPayConfig via PaymentIQ backoffice.

## Configuration
Only one account is needed and can be used for both sign in and sign up with deposit.

```xml
<com.devcode.paymentiq.integration.luxonpay.LuxonPayConfig>
  <enabled>true</enabled>
  <useViqProxy>false</useViqProxy>
  <accounts>
    <entry>
      <string>DEFAULT</string>
      <account>
       <merchantKeyId>?</merchantKeyId> <!-- HMAC Key ID-->
       <secretKey>?</secretKey> <!-- HMAC Key Value-->
       <supportedCurrencies>EUR</supportedCurrencies>
      </account>
    </entry>
  </accounts>
  <testMode>true</testMode>
  <container>window</container>
  <defaultDescriptor>Bambora TEST Payment</defaultDescriptor>
</com.devcode.paymentiq.integration.luxonpay.LuxonPayConfig>
```

## Presentation Layer

For LuxonPay two steps transactions flow, PaymentIQ can either return a JSON containing an URL or do a 303 Redirect to the same URL. 
JSON is returned when `iframe=true`, a redirect is performed when `iframe=false`, see [Authorization Endpoint](1click_api_authorization).

Example JSON response:

```json
{
    "redirectOutput": {
        "html": null,
        "url": "https://merchants.int.luxon.com/#/payment-details/1e86ad98-31f1-40f4-aa78-a9c1525ed2e4",
        "method": "POST",
        "container": "window",
        "parameters": {},
        "height": 600,
        "width": 600,
        "sizeUnit": null
    },
    "messages": [],
    "links": {
        "statusUrl": "https://test-api.paymentiq.io/paymentiq/identity/api/signin/status?token=eyJhbGciOiJIUzI1NiJ9.eyJtZXJjaGFudElkIjoyMTEyLCJleHAiOjE2Njk2MzM5ODYsInRva2VuIjoiMjExMkExMDE0MjA4NTcyIn0.dridSKnEiVnuvDDiUghVQGijkT7PL2-WFLCo-fcafiQ"
    },
    "success": true
}
```


## KYC Data
| Field        | Type   | Example                                          | Description                                          |
|--------------|--------|--------------------------------------------------|------------------------------------------------------|
| firstName    | string | John                                             | The first name of the user making the deposit.       |
| lastName     | string | Doe                                              | The last name of the user making the deposit.        |
| dateOfBirth  | string | 1990-01-01                                       | The date of birth of the user in ISO8601 format.     |
| phone        | string | +46701701701                                     | The mobile phone number of the user.                 |
| email        | string | example@gmail.com                                | The email address of the user.                       |
| address      | string | Somestreet, Stockholm, Stockholm, Sweden, 111 11 | The registered address of the user.                  |
| country      | string | SWE                                              | The 3-letter country of the user in ISO 3166 format. |


## User Sign Up & Deposit Flow

1. The first step is for the user to specify the login then enter the phone number or email and password.

![](/img/1clickapi/luxon_1.png)

2. The user is redirected to the confirmation page then press Pay button in order to confirm payment.

![](/img/1clickapi/luxon_2.png)

3. The user is redirected to the result page after the payment is completed

![](/img/1clickapi/luxon_3.png)

