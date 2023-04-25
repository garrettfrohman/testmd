---
id: "front_api_delete_accounts"
---

# Delete Account

`DELETE /api/user/account/{merchantId}/{userId}/{accountId}?sessionId={sessionId}`

## Example Request

```curl
curl -X DELETE -H 'Content-Type: application/json' https://api.paymentiq.io/paymentiq/api/user/account/1000/TEST_USER/faafb9ec-a8c1-4c4c-aa65-ba67e556f204?sessionId=qwerty
```

## Request Parameters

| Name       | Located in | Description                                                                                                   | Data Type | Required |
|------------|------------|---------------------------------------------------------------------------------------------------------------|-----------|----------|
| merchantId | path       | PaymentIQ merchant which will process the payment. Assigned by PaymentIQ during onboarding.                   | integer   | true     |
| userId     | path       | User's unique id, which can be a number or a user name. It should not be changed during the user's life-time. | string    | true     |
| accountId  | path       | User's account id                                                                                             | string    | true     |
| sessionId  | query      | User's session-id. Used by PaymentIQ to verify if user is authenticated.                                      | string    | true     |

## Example Response

```json
{
  "merchantId": 1000,
  "userId": "TEST_USER",
  "success": true,
  "accountId": "faafb9ec-a8c1-4c4c-aa65-ba67e556f204"
}
```

## Response Parameters

| Name       | Description             | Data Type | Required |
| ---------- | ----------------------- | --------- | -------- |
| merchantId | Merchant id             | integer   | true     |
| userId     | User id                 | string    | true     |
| success    | Result of the operation | boolean   | true     |
| accountId  | The deleted account     | string    | true     |