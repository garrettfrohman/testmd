---
id: "front_api_cancel_transaction"
---

# Cancel Transaction

`DELETE /api/user/transaction/{merchantId}/{userId}/{transactionId}?sessionId={sessionId}`

## Example Request

```curl
curl -X DELETE -H 'Content-Type: application/json' https://api.paymentiq.io/paymentiq/api/user/transaction/1000/TEST_USER/27023106?sessionId=qwerty
```

## Request Parameters

| Name          | Located in | Description                                                                                                   | Data Type | Required |
|---------------|------------|---------------------------------------------------------------------------------------------------------------|-----------|----------|
| merchantId    | path       | PaymentIQ merchant which will process the payment. Assigned by PaymentIQ during onboarding.                   | integer   | true     |
| userId        | path       | User's unique id, which can be a number or a user name. It should not be changed during the user's life-time. | string    | true     |
| transactionId | path       | User's withdrawal transaction-id.                                                                             | string    | true     |
| sessionId     | query      | User's session-id. Used by PaymentIQ to verify if user is authenticated.                                      | string    | true     |

## Example Response

```json
{
  "merchantId": 1000,
  "userId": "TEST_USER",
  "transactionId": "27023106",
  "success": true
}
```

## Response Parameters

| Name          | Description             | Data Type | Required |
|---------------|-------------------------|-----------|----------|
| merchantId    | Merchant id             | integer   | true     |
| userId        | User id                 | string    | true     |
| transactionId | Transaction-id          | string    | true     |
| success       | Result of the operation | boolean   | true     |