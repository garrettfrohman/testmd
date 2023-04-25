---
id: "front_api_find_transactions"
---

# Find Transactions

`GET /api/user/transaction/{merchantId}/{userId}?sessionId={sessionId}`

## Example Request

```curl
curl -X GET -H 'Content-Type: application/json' https://api.paymentiq.io/paymentiq/api/user/transaction/1000/TEST_USER?sessionId=qwerty
```

## Request Parameters

| Name          | Located in | Description                                                                                                   | Data Type | Required |
|---------------|------------|---------------------------------------------------------------------------------------------------------------|-----------|----------|
| merchantId    | path       | PaymentIQ merchant which will process the payment. Assigned by PaymentIQ during onboarding.                   | integer   | true     |
| userId        | path       | User's unique id, which can be a number or a user name. It should not be changed during the user's life-time. | string    | true     |
| sessionId     | query      | User's session-id. Used by PaymentIQ to verify if user is authenticated.                                      | string    | true     |
| states        | query      | Array of payment states, e.g SUCCESSFUL,CANCELLED                                                             | string    | false    |
| txType        | query      | The transaction type, e.g CreditcardDeposit                                                                   | string    | false    |
| maxDate       | query      | Date format in case sending a value: “yyyy-MM-dd HH:mm:ss                                                     | string    | false    |
| minDate       | query      | Date format in case sending a value: “yyyy-MM-dd HH:mm:ss                                                     | string    | false    |
| transactionId | query      | User's withdrawal transaction-id.                                                                             | string    | false    |
| method        | query      | Method, Deposit or Withdrawal                                                                                 | string    | false    |

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

| Name         | Description             | Data Type | Required |
|--------------|-------------------------|-----------|----------|
| merchantId   | Merchant id             | integer   | true     |
| userId       | User id                 | string    | true     |
| success      | Result of the operation | boolean   | true     |
| transactions | Transactions            | array     | true     |