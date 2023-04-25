---
id: "front_api_check_transaction_status"
---

# Check Transaction Status

`GET /api/user/transaction/{merchantId}/{userId}/{transactionId}/status?sessionId={sessionId}`

## Example Request

```curl
curl -X GET -H 'Content-Type: application/json' https://api.paymentiq.io/paymentiq/api/user/transaction/1000/TEST_USER/27023106/status?sessionId=qwerty
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
  "txState": "SUCCESSFUL",
  "messages": [
    {
      "label": "creditcarddeposit.receiptDepositAccountToCharge",
      "keys": [
        "creditcarddeposit.receiptDepositAccountToCharge",
        "receiptDepositAccountToCharge"
      ],
      "value": "491730******0000"
    },
    {
      "label": "creditcarddeposit.receiptDepositAmount",
      "keys": [
        "creditcarddeposit.receiptDepositAmount",
        "receiptDepositAmount"
      ],
      "value": "5.00 EUR"
    },
    {
      "label": "creditcarddeposit.receiptDepositFee",
      "keys": [
        "creditcarddeposit.receiptDepositFee",
        "receiptDepositFee"
      ],
      "value": "0.00 EUR"
    },
    {
      "label": "creditcarddeposit.receiptDepositTxAmount",
      "keys": [
        "creditcarddeposit.receiptDepositTxAmount",
        "receiptDepositTxAmount"
      ],
      "value": "5.00 EUR"
    },
    {
      "label": "creditcarddeposit.receiptDepositPspRefId",
      "keys": [
        "creditcarddeposit.receiptDepositPspRefId",
        "receiptDepositPspRefId"
      ],
      "value": "4712A27023102"
    },
    {
      "label": "creditcarddeposit.receiptDepositTxId",
      "keys": [
        "creditcarddeposit.receiptDepositTxId",
        "receiptDepositTxId"
      ],
      "value": "27023102"
    },
    {
      "label": "creditcarddeposit.receiptDepositBankName",
      "keys": [
        "creditcarddeposit.receiptDepositBankName",
        "receiptDepositBankName"
      ],
      "value": ""
    },
    {
      "label": "creditcarddeposit.receiptDepositInProgressExtraMsg",
      "keys": [
        "creditcarddeposit.receiptDepositInProgressExtraMsg",
        "receiptDepositInProgressExtraMsg"
      ],
      "value": ""
    }
  ],
  "txRefId": "4712A27023107",
  "statusCode": "SUCCESS",
  "pspStatusCode": "PENDING",
  "psp": "Neteller",
  "pspAccount": "3DS",
  "pspService": "250EAO",
  "merchantTxId": "c15eef34-1f37-43a4-a19b-473dbef541ed",
  "success": true
}
```

## Response Parameters

| Name          | Description                                                                                                           | Data Type | Required |
|---------------|-----------------------------------------------------------------------------------------------------------------------|-----------|----------|
| txState       | Transaction state                                                                                                     | string    | true     |
| errors        | If success: false then transaction was not successfully completed. This property contains one or more error messages. | array     | true     |
| messages      | Receipt information about the transaction                                                                             | array     | true     |
| txRefId       | Reference Id of the transaction                                                                                       | string    | true     |
| statusCode    | Status code                                                                                                           | string    | true     |
| pspStatusCode | Provider specific status code                                                                                         | string    | true     |
| psp           | Representation of provider who has processed the transaction, e.g. Skrill, Neteller or PayPoint                       | string    | true     |
| pspAccount    | Provider account used in the transaction                                                                              | string    | true     |
| pspService    | Representation of provider's sub service which will be used to do a payment                                           | string    | true     |
| merchantTxId  | Merchant's tx id.                                                                                                     | string    | true     |
| success       | Result of the operation                                                                                               | boolean   | true     |