---
id: "cancel"
---

# cancel

This method is called by PaymentIQ after a failed transaction to cancel the previous authorize request, i.e. the Operator should release any reserved money from the user's account.

`POST/paymentiq/cancel`

## Example Request

```json
{
  "userId": "user_123",
  "authCode": "1238712937821",
  "txAmount": "100.50",
  "txAmountCy": "SEK",
  "txId": "26720",
  "txTypeId": "101",
  "txName": "CreditcardDeposit",
  "provider": "Neteller"
}
```

## Request Parameters

| Name             | Located In | Description                                                                                                                                                                                                                                                                                                     | Schema | Required |
|------------------|------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------|----------|
| userId           | body       | User's unique id, which can be a number or a username. Max 50 char.<br/>_Example:_ `"user_123"`                                                                                                                                                                                                                 | string | Yes      |
| authCode         | body       | Authorization code from authorize response.<br/>_Example:_ `"1238712937821"`                                                                                                                                                                                                                                    | string | Yes      |
| txAmount         | body       | Amount credited or debited user's account, formatted like 100.50. Negative amount must decrease the user's account balance, i.e. the user is withdrawing money. Positive amount must increase the user's account balance. Note: This amount might differ from the amount in authorize<br/>_Example:_ `"100.50"` | string | Yes      |
| txAmountCy       | body       | 'txAmount' currency, 3-letter code according to ISO standard, e.g SEK. <br/>_Example:_ `"SEK"`                                                                                                                                                                                                                  | string | Yes      |
| txId             | body       | PaymentIQ unique transaction-id<br/>_Example:_ `"26720"`                                                                                                                                                                                                                                                      | string | Yes      |
| txTypeId         | body       | Transaction type, e.g 101 = CreditcardDeposit<br/>_Example:_ `"101"`                                                                                                                                                                                                                                            | string | Yes      |
| txName           | body       | Transaction name, e.g CreditcardDeposit<br/>_Example:_ `"CreditcardDeposit"`                                                                                                                                                                                                                                    | string | Yes      |
| provider         | body       | Provider that processed the transaction, e.g. Neteller<br/>_Example:_ `"Neteller"`                                                                                                                                                                                                                              | string | Yes      |
| originTxId       | body       | Optional reference to the origin PaymentIQ transaction. This field is only populated when there is an origin transaction, e.g when doing a refund this field will refer to the transaction which was refunded. <br/>_Example:_ `"12321312"`                                                                     | string | No       |
| accountId        | body       | Optional ref to PaymentIQ account-id. The account-id is used for repeat payments.<br/>_Example:_ `"dd14cb2d-623f-46a9-9210-beb8d1f033c9."`                                                                                                                                                                      | string | No       |
| accountHolder    | body       | Optional name of the credit card holder or bank account holder<br/>_Example:_ `"John"`                                                                                                                                                                                                                          | string | No       |
| maskedAccount    | body       | Optional masked account<br/>_Example:_ `"411812******2410"`                                                                                                                                                                                                                                                     | string | No       |
| statusCode       | body       | Optional PaymentIQ specific status code. List of status codes can be provided on request.<br/>_Example:_ `"1111"`                                                                                                                                                                                               | string | No       |
| pspStatusCode    | body       | Optional PSP specific status code, e.g. Neteller status code 1010 is 'You have requested an amount higher than the balance available in your NETELLER account.'<br/>_Example:_ `"123"`                                                                                                                          | string | No       |
| pspFee           | body       | Expected fee from the provider. Calculated by PaymentIQ provider Fee rules. <br/>_Example:_ `"123"`                                                                                                                                                                                                             | string | No       |
| pspFeeCy         | body       | PSP fee currency. 3-letter code according to ISO standard, e.g SEK. <br/>_Example:_ `"SEK"`                                                                                                                                                                                                                     | string | No       |
| pspFeeBase       | body       | Expected fee from the provider in the base currency. Calculated by PaymentIQ provider Fee rules. <br/>_Example:_ `"20"`                                                                                                                                                                                         | string | No       |
| pspFeeBaseCy     | body       | Currency for the fee in the base currency. 3-letter code according to ISO standard, e.g SEK.<br/>_Example:_ `"SEK"`                                                                                                                                                                                             | string | No       |
| pspRefId         | body       | The reference ID used by the Provider for the transaction.<br/>_Example:_ `"111111"`                                                                                                                                                                                                                            | string | No       |
| pspStatusMessage | body       | The status message returned from the PSP provider.<br/>_Example:_ `"Success"`                                                                                                                                                                                                                                   | string | No       |
| attributes       | body       | Echoing back the optional parameter sent in the payment request by merchant, or optional extraAttributes configured in MerchantConfig.<br/>_Example:_ `{"allow_manual_payout":"true"}`                                                                                                                          | string | No       |

## Example Response

```json
{
  "userId": "user_123",
  "success": true,
  "errCode": "111111",
  "errMsg": "Transfer failed"
}

```

## Response Parameters

| Name    | Description                                                                                      | Schema  | Required |
|---------|--------------------------------------------------------------------------------------------------|---------|----------|
| userId  | User's unique id, which can be a number or a username. Max 50 char.<br/>_Example:_ `"user_123"`  | string  | Yes      |
| success | True or false. If false then only the two last parameters will be appended<br/>_Example:_ `true` | boolean | Yes      |
| errCode | If success false: Custom error code<br/>_Example:_ `"111111"`                                    | number  | No       |
| errMsg  | If success false: Custom error message<br/>_Example:_ `"Transfer failed"`                        | string  | No       |
