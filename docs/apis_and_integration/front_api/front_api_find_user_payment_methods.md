---
id: "front_api_find_user_payment_methods"
---

# Find User Payment Methods

`GET /api/user/payment/method/{merchantId}/{userId}?sessionId={sessionId}&method={method}`

## Example Request

```curl
curl -X GET -H 'Content-Type: application/json' https://api.paymentiq.io/paymentiq/api/user/payment/method/99/TEST_USER?sessionId=qwerty&method=deposit
```

## Request Parameters

| Name                     | Located in | Description                                                                                                                                                                                    | Data Type | Required |
|--------------------------|------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------|----------|
| merchantId               | path       | PaymentIQ merchant which will process the payment. Assigned by PaymentIQ during onboarding.                                                                                                    | integer   | true     |
| userId                   | path       | User's unique id, which can be a number or a user name. It should not be changed during the user's life-time.                                                                                  | string    | true     |
| sessionId                | query      | User's session-id. Used by PaymentIQ to verify if user is authenticated.                                                                                                                       | string    | true     |
| method                   | query      | Method, Deposit or Withdrawal                                                                                                                                                                  | string    | true     |
| channelId                | query      | Channel id used for method                                                                                                                                                                     | string    | false    |
| showExpired              | query      | Toggle if expired accounts should be shown                                                                                                                                                     | boolean   | false    |
| showNew                  | query      | Toggle if accounts with state NEW should be shown                                                                                                                                              | boolean   | false    |
| locale                   | query      | Locale used for payment method                                                                                                                                                                 | string    | false    |
| attributes.attributeName | path       | Option to send attributes.attributeName as a parameter. For example attributes.site=siteName which can then be matched up with the Payment Methods Condition 'Check Payment Methods Attribute' | string    | false    |



## Example Response

```json
{
  "merchantId": 1000,
  "userId": "TEST_USER",
  "success": true,
  "methods": [
    {
      "toUserCurrencyBuyRate": 0,
      "txType": "CreditcardDeposit",
      "accountSettings": null,
      "accounts": [
        {
          "accountId": "59e2768b-1340-4fc9-96a6-4d695e07ce31",
          "description": null,
          "lastSuccess": "2020-05-03 00:00:00",
          "lastUsed": "2020-05-03 00:00:00",
          "maskedAccount": "4234********3323",
          "type": "creditcard",
          "visible": true,
          "expired": false,
          "status": "ACTIVE",
          "cardType": "Visa",
          "cardHolder": "test",
          "expiryDate": "2022-02",
          "service": "EMP",
          "assets": [
            {
              "data": "iVBORw0KGgoAAAANSUhEUgAABgAAAAPJCAYAAAD....SUVORK5CYII=",
              "mediaType": "image/png",
              "type": "digitalCardArt"
            }
          ]
        }
      ],
      "limit": {
        "max": "10.00",
        "min": "1.00",
        "fixed": [
          "5.00",
          "3.00",
          "2.00"
        ]
      },
      "fees": [
        {
          "fixedFee": "3.00",
          "percentageFee": "0.1",
          "fixedFeeMin": "1.00",
          "fixedFeeMax": "2.00",
          "mode": "add",
          "billTo": "USER"
        }
      ],
      "pspToUserCurrencyBuyRate": 0,
      "providerType": "CREDITCARD",
      "service": null,
      "pspCurrency": "",
      "canAddAccount": true,
      "maintenanceInfo": {
        "maintenance": false,
        "from": "2020-04-03 00:00:00",
        "to": "2020-08-03 00:00:00",
        "message": "Not available"
      }
    },
    {
      "txType": "BankDeposit",
      "accountSettings": null,
      "accounts": [],
      "limit": {
        "max": "10.00",
        "min": "2.00",
        "fixed": [
          "1.00"
        ]
      },
      "fees": [
        {
          "fixedFee": "2.00",
          "percentageFee": "0.1",
          "fixedFeeMin": "1.00",
          "fixedFeeMax": "10.00",
          "mode": "ADD",
          "billTo": "USER"
        }
      ],
      "pspToUserCurrencyBuyRate": 0,
      "providerType": "BANK",
      "service": null,
      "pspCurrency": "",
      "canAddAccount": true,
      "maintenanceInfo": {
        "maintenance": false
      },
      "toUserCurrencyBuyRate": 0
    }
  ],
  "feeInfo": {
    "nextFreeDate": "2021-02-11T18:59:22.150Z"
  }
}
```

## Response Parameters

| Name       | Description                                                                                                                                        | Data Type | Required |
|------------|----------------------------------------------------------------------------------------------------------------------------------------------------|-----------|----------|
| merchantId | Merchant Id                                                                                                                                        | integer   | true     |
| userId     | User Id                                                                                                                                            | string    | true     |
| success    | Result of the operation                                                                                                                            | boolean   | true     |
| methods    | The available payment methods for this user, including potentially saved accounts                                                                  | array     | true     |
| feeInfo    | Info about when next free withdrawal is allowed. This is only present if action Next free withdrawal is set in the fee rules, otherwise it's null. | object    | true     |
