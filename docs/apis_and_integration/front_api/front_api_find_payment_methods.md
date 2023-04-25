---
id: "front_api_find_payment_methods"
---

# Find Payment Methods (by locale)

Get available payment methods based on the locale value which is required, and the locale condition is also needed in the 'Payment methods' rule.

`GET /api/user/payment/method/{merchantId}?locale={locale}`

## Example Request

```curl
curl -X GET -H 'Content-Type: application/json' https://api.paymentiq.io/paymentiq/api/user/payment/method/1000?locale=en_GB
```

## Request Parameters

| Name       | Located in | Description                                                                                 | Data Type | Required |
|------------|------------|---------------------------------------------------------------------------------------------|-----------|----------|
| merchantId | path       | PaymentIQ merchant which will process the payment. Assigned by PaymentIQ during onboarding. | integer   | true     |
| locale     | query      | The desired locale.                                                                         | string    | true     |
| channelId  | query      | The channel id used for the payment methods                                                 | string    | false    |


## Example Response

```json
{
  "merchantId": 1000,
  "success": true,
  "methods": [
    {
      "txType": "",
      "accountSettings": null,
      "accounts": [],
      "limit": null,
      "fees": [],
      "pspToUserCurrencyBuyRate": 0,
      "providerType": "CREDITCARD",
      "service": null,
      "pspCurrency": "",
      "canAddAccount": null,
      "maintenanceInfo": {
        "maintenance": false
      },
      "toUserCurrencyBuyRate": 0
    }
  ]
}
```

## Response Parameters

| Name       | Description                                   | Data Type | Required |
|------------|-----------------------------------------------|-----------|----------|
| merchantId | Merchant Id                                   | integer   | true     |
| success    | Result of the operation                       | boolean   | true     |
| methods    | The available payment methods for this locale | array     | true     |
