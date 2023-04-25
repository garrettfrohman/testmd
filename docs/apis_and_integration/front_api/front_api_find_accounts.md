---
id: "front_api_find_accounts"
---

# Find Accounts

`GET /api/user/account/{merchantId}/{userId}?sessionId={sessionId}`

## Example Request

```curl
curl -X GET -H 'Content-Type: application/json' https://api.paymentiq.io/paymentiq/api/user/account/1000/TEST_USER?sessionId=qwerty
```

## Request Parameters

| Name        | Located in | Description                                                                                                   | Data Type | Required |
|-------------|------------|---------------------------------------------------------------------------------------------------------------|-----------|----------|
| merchantId  | path       | PaymentIQ merchant which will process the payment. Assigned by PaymentIQ during onboarding.                   | integer   | true     |
| userId      | path       | User's unique id, which can be a number or a user name. It should not be changed during the user's life-time. | string    | true     |
| sessionId   | query      | User's session-id. Used by PaymentIQ to verify if user is authenticated.                                      | string    | true     |
| type        | query      | Type of account, e.g creditcard                                                                               | string    | false    |
| showExpired | query      | Toggle if expired accounts should be shown                                                                    | boolean   | false    |
| showNew     | query      | Toggle if accounts with state NEW should be shown                                                             | boolean   | false    |

## Example Response

```json
{
  "merchantId": 1000,
  "userId": "TEST_USER",
  "success": true,
  "accounts": [
    {
      "type": "creditcard",
      "accountId": "e2989c66-cc01-4ee5-8252-527a72c56782",
      "maskedAccount": "417666******1015",
      "lastUsed": "2021-01-21 12:01:28",
      "lastSuccess": "2021-01-21 11:54:43",
      "description": null,
      "expired": false,
      "status": "ACTIVE",
      "cardType": "Visa",
      "cardHolder": "test holder",
      "startDate": null,
      "expiryDate": "2021-02",
      "storedInVaultIQ": true
    },
    {
      "type": "banklocal",
      "accountId": "590b4343-fe56-417f-984e-227768da772d",
      "maskedAccount": "123456-12345678",
      "lastUsed": "2020-11-08 10:47:14",
      "lastSuccess": null,
      "visible": true,
      "description": null,
      "expired": false,
      "status": "ACTIVE",
      "service": "TRUSTLY"
    }
  ]
}
```

## Response Parameters

| Name       | Description                | Data Type | Required |
|------------|----------------------------|-----------|----------|
| merchantId | Merchant id                | integer   | true     |
| userId     | User id                    | string    | true     |
| success    | Result of the operation    | boolean   | true     |
| accounts   | List of available accounts | array     | true     |

