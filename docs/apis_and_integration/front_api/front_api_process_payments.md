---
id: "front_api_process_payments"
---

# Process Payments

Please notee that depending on provider integration you will have to provide additional request body parameters, please refer to the provider specific parameters section for more information.

`POST /api/{provider}/{type}/{method}`

## Example Request

```curl
curl -X POST -H 'Content-Type: application/json' -d '{"sessionId":"1234567","userId":"TEST_USER","merchantId":"1000","amount":"1","attributes": {}}' https://api.paymentiq.io/paymentiq/api/neteller/deposit/process
```

## Request Parameters

| Name       | Located in   | Description                                                                                                                                                                                                                                                                                                                            | Data Type | Required |
|------------|--------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------|----------|
| provider   | path         | Provider specific type. See the "Provider Specific Params" chapter of this documentation for their full endpoint. Example: skrill                                                                                                                                                                                                      | string    | true     |
| type       | path         | Type of method. Possible values: deposit, withdrawal                                                                                                                                                                                                                                                                                   | string    | true     |
| method     | path         | Method to execute. You can either process a payment or validate a payment which is a server-side validation. Possible values: process, validate                                                                                                                                                                                        | string    | true     |
| sessionId  | request body | User's session-id. Used by PaymentIQ to verify if user is authenticated.                                                                                                                                                                                                                                                               | string    | true     |
| userId     | request body | User's unique id, which can be a number or a user name. It should not be changed during the user's life-time.                                                                                                                                                                                                                          | string    | true     |
| merchantId | request body | PaymentIQ merchant which will process the payment. Assigned by PaymentIQ during onboarding.                                                                                                                                                                                                                                            | string    | true     |
| amount     | request body | Amount of the transaction.                                                                                                                                                                                                                                                                                                             | string    | true     |
| accountId  | request body | Reference to optional account UUID, i.e a saved account in PIQ                                                                                                                                                                                                                                                                         | string    | false    |
| attributes | request body | Map of optional parameters which are merchant specific and is not related to the payment request, e.g.bonus code, channel, and request specific success and failure URLs. These will be reflected back to merchant in the authorize and transfer requests in the Integration API. **Note: Some properties are reserved by PaymentIQ.** | object    | false    |

## Example Response

```json
{
  "txState": "SUCCESSFUL",
  "txRefId": "4712A27023107",
  "txId": "27023107",
  "statusCode": "SUCCESS",
  "maskedAccount": "417666******1015",
  "success": true,
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
  ]
}
```

## Response Parameters

| Name           | Description                                                                                                                                                                                                         | Data Type | Required |
|----------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------|----------|
| txState        | Transaction state                                                                                                                                                                                                   | string    | true     |
| txRefId        | Reference Id of the transaction                                                                                                                                                                                     | string    | true     |
| txId           | Id of the transaction                                                                                                                                                                                               | integer   | true     |
| statusCode     | Transaction status                                                                                                                                                                                                  | string    | true     |
| maskedAccount  | Masked user account                                                                                                                                                                                                 | string    | true     |
| success        | Flag if the transaction was successful or not. The the flag is false then the property errors is also populated.                                                                                                    | boolean   | true     |
| redirectOutput | If this property is set then the user must be redirected to a page provided by the provider in order to complete the transaction, e.g. a credit card deposit with 3D secure. See below for how to redirect the user | object    | true     |
| messages       | If success: true and the no redirect parameter is defined then the transaction was successfully completed. This property contains messages that can be displayed to the user.                                       | array     | true     |
| errors         | If success: false then transaction was not successfully completed. This property contains one or more error messages.                                                                                               | array     | true     |
