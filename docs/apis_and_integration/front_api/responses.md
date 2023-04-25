---
id: "responses"
---

# API Response

The response has following JSON structure:

| JSON params    | Type    | M/O | Description                                                                                                                                                                                                          |
|----------------|---------|-----|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| success        | Boolean | M   | Flag if the transaction was successful or not. If the flag is false then the property ```errors``` is also populated.                                                                                                     |
| txState        | String  | M   | Transaction state.                                                                                                     |
| txRefId        | String  | M   | Reference Id of the transaction.                                                                                                     |
| txId           | Integer | M   | Id of the transaction.                                                                                                     |
| statusCode     | String  | M   | Transaction status.                                                                                                     |
| maskedAccount  | String  | O   | Masked user account.                                                                                                     |
| redirectOutput | Object  | O   | If this property is set then the user must be redirected to a page provided by the provider in order to complete the transaction, e.g. a credit card deposit with 3D secure. See [Generic Redirect](./redirect) for more. |
| message        | Array   | O   | If property ```success``` is ```true``` and no redirect parameter is defined then the transaction was successfully completed. This property contains messages that can be displayed to the end user.                                      |
| errors         | Array   | O   | If property ```success``` is ```false``` the transaction was not successfully completed. This property will contain one or more error messages.                                                                                              |

Example response of a successful transaction with no redirect:

```json
{
  "txState": "SUCCESSFUL",
  "messages": [{
    "label": "Account",
    "keys": ["creditcarddeposit.receiptDepositAccountToCharge", "receiptDepositAccountToCharge"],
    "value": "400000******0002"
  }, {
    "label": "Amount deposited to player account",
    "keys": ["creditcarddeposit.receiptDepositAmount", "receiptDepositAmount"],
    "value": "10.00 EUR"
  }, {
    "label": "Deposit fee",
    "keys": ["creditcarddeposit.receiptDepositFee", "receiptDepositFee"],
    "value": "0.00 EUR"
  }, {
    "label": "Amount withdrawn from PSP account",
    "keys": ["creditcarddeposit.receiptDepositTxAmount", "receiptDepositTxAmount"],
    "value": "10.00 EUR"
  }, {
    "label": "Payment reference",
    "keys": ["creditcarddeposit.receiptDepositPspRefId", "receiptDepositPspRefId"],
    "value": "94748057"
  }],
  "txRefId": "1000A597345",
  "txId": 597345,
  "statusCode": "SUCCESS",
  "maskedAccount": "400000******0002",
  "success": true
}
```

Example response of a failed transaction with errors:

```json
{
  "txState": "FAILED",
  "errors": [{
    "field": null,
    "keys": [
      "creditcarddeposit.pspcode.1000",
      "creditcarddeposit.status.err_declined_other_reason",
      "creditcarddeposit.state.failed",
      "status.err_declined_other_reason",
      "state.failed"],
    "msg": "Invalid CVV"
  }],
  "messages": [],
  "txRefId": "1000A597352",
  "txId": 597345,
  "statusCode": "ERR_DECLINED_OTHER_REASON",
  "maskedAccount": "400000******0002",
  "success": false
}
```
