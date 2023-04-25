---
id: "transfer"
---

# transfer

This method is called by PaymentIQ after a successfully processed transaction to credit (increase) or debit (decrease) a user's account balance. Note: The Operator Platform must always accept a transfer request, even if it results in a negative user balance because the payment transaction has already been processed by the payment provider.

`POST/paymentiq/transfer`

## Example Request

```json
{
  "userId": "user_123",
  "txAmount": "100.50",
  "txAmountCy": "SEK",
  "txPspAmount": "12.50",
  "txPspAmountCy": "EUR",
  "fee": "0.50",
  "feeCy": "SEK",
  "txId": "26720",
  "txTypeId": "101",
  "txName": "CreditcardDeposit",
  "provider": "Neteller",
  "txRefId": "100019999A26720"
}
```

## Request Parameters

| Name             | Located In | Description                                                                                                                                                                                                                                                                                                     | Schema | Required |
|------------------|------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------|----------|
| userId           | body       | User's unique id, which can be a number or a username. Max 50 char.<br/>_Example:_ `"user_123"`                                                                                                                                                                                                                 | string | Yes      |
| authCode         | body       | Authorization code from authorize response.<br/>_Example:_ `"1238712937821"`                                                                                                                                                                                                                                    | string | No       |
| txAmount         | body       | Amount credited or debited user's account, formatted like 100.50. Negative amount must decrease the user's account balance, i.e. the user is withdrawing money. Positive amount must increase the user's account balance. Note: This amount might differ from the amount in authorize<br/>_Example:_ `"100.50"` | string | Yes      |
| txAmountCy       | body       | 'txAmount' currency, 3-letter code according to ISO standard, e.g SEK. <br/>_Example:_ `"SEK"`                                                                                                                                                                                                                  | string | Yes      |
| txPspAmount      | body       | Amount sent to PSP, formatted like 12.50. Positive amount is deposit and negative amount is withdrawal. The 'txPspAmount' is 'txAmount' + 'fee' converted to 'txPspAmountCy currency.<br/>_Example:_ `"12.50"`                                                                                                  | string | Yes      |
| txPspAmountCy    | body       | 'txPspAmount' currency, 3-letter code according to ISO standard, e.g EUR.<br/>_Example:_ `"EUR"`                                                                                                                                                                                                                | string | Yes      |
| fee              | body       | Fee charged user, formatted like 0.50<br/>_Example:_ `"0.50"`                                                                                                                                                                                                                                                   | string | Yes      |
| feeCy            | body       | 'fee' currency, 3-letter code according to ISO standard, e.g SEK. It will be the same currency as 'txAmountCy'.<br/>_Example:_ `"SEK"`                                                                                                                                                                          | string | Yes      |
| feeMode          | body       | Indicates if the fee is deducted 'D' from the 'txPspAmount' or if the fee is added 'A' to the 'txAmount'. NOTE: The 'txPspAmount' can be converted to another currency<br/>_Example:_ `"D"`                                                                                                                     | string | No       |
| txId             | body       | PaymentIQ unique transaction-id<br/>_Example:_ `"26720"`                                                                                                                                                                                                                                                      | string | Yes      |
| txTypeId         | body       | Transaction type, e.g 101 = CreditcardDeposit<br/>_Example:_ `"101"`                                                                                                                                                                                                                                            | string | Yes      |
| txName           | body       | Transaction name, e.g CreditcardDeposit<br/>_Example:_ `"CreditcardDeposit"`                                                                                                                                                                                                                                    | string | Yes      |
| provider         | body       | Provider that processed the transaction, e.g. Neteller<br/>_Example:_ `"Neteller"`                                                                                                                                                                                                                              | string | Yes      |
| pspService       | body       | Optional payment service used when an aggregating provider has several underlaying services. E.g. provider='Envoy' and pspService='IDEAL'<br/>_Example:_ `"IDEAL"`                                                                                                                                              | string | No       |
| txRefId          | body       | Transaction reference id sent to provider. It contains the PaymentIQ merchant-id and transaction-id separated by 'A', e.g 100019999A26720<br/>_Example:_ `"100019999A26720"`                                                                                                                                    | string | Yes      |
| originTxId       | body       | Optional reference to the origin PaymentIQ transaction. This field is only populated when there is an origin transaction, e.g when doing a refund this field will refer to the transaction which was refunded. <br/>_Example:_ `"12321312"`                                                                     | string | No       |
| accountId        | body       | Optional ref to PaymentIQ account-id. The account-id is used for repeat payments.<br/>_Example:_ `"dd14cb2d-623f-46a9-9210-beb8d1f033c9."`                                                                                                                                                                      | string | No       |
| accountHolder    | body       | Optional name of the credit card holder or bank account holder<br/>_Example:_ `"John"`                                                                                                                                                                                                                          | string | No       |
| maskedAccount    | body       | Optional masked account<br/>_Example:_ `"411812******2410"`                                                                                                                                                                                                                                                     | string | No       |
| pspFee           | body       | Expected fee from the provider. Calculated by PaymentIQ provider Fee rules. <br/>_Example:_ `"123"`                                                                                                                                                                                                             | string | No       |
| pspFeeCy         | body       | PSP fee currency. 3-letter code according to ISO standard, e.g SEK. <br/>_Example:_ `"SEK"`                                                                                                                                                                                                                     | string | No       |
| pspFeeBase       | body       | Expected fee from the provider in the base currency. Calculated by PaymentIQ provider Fee rules. <br/>_Example:_ `"20"`                                                                                                                                                                                         | string | No       |
| pspFeeBaseCy     | body       | Currency for the fee in the base currency. 3-letter code according to ISO standard, e.g SEK.<br/>_Example:_ `"SEK"`                                                                                                                                                                                             | string | No       |
| pspRefId         | body       | The reference ID used by the Provider for the transaction.<br/>_Example:_ `"111111"`                                                                                                                                                                                                                            | string | No       |
| pspStatusMessage | body       | The status message returned from the PSP provider.<br/>_Example:_ `"Success"`                                                                                                                                                                                                                                   | string | No       |
| expiryYear       | body       | The card expiration year.<br/>_Example:_ `"2020"`                                                                                                                                                                                                                                                               | string | No       |
| expiryMonth      | body       | The card expiration month.<br/>_Example:_ `"05"`                                                                                                                                                                                                                                                                | string | No       |
| attributes       | body       | Echoing back the optional parameter sent in the payment request by merchant, or optional extraAttributes configured in MerchantConfig.<br/>_Example:_ `{"allow_manual_payout":"true"}`                                                                                                                          | string | No       |




## Example Response

```json
{
  "userId": "user_123",
  "success": true,
  "txId": "26720",
  "merchantTxId": "111111111",
  "errCode": "111111",
  "errMsg": "Transfer failed"
}
```

## Response Parameters

| Name         | Description                                                                                      | Schema  | Required |
|--------------|--------------------------------------------------------------------------------------------------|---------|----------|
| userId       | User's unique id, which can be a number or a username. Max 50 char.<br/>_Example:_ `"user_123"`  | string  | Yes      |
| success      | True or false. If false then only the two last parameters will be appended<br/>_Example:_ `true` | boolean | Yes      |
| txId         | PaymentIQ unique transaction-id<br/>_Example:_ `"26720"`                                       | string  | Yes      |
| merchantTxId | Merchant's unique transaction-id<br/>_Example:_ `"111111111"`                                    | number  | Yes      |
| errCode      | If success false: Custom error code<br/>_Example:_ `"111111"`                                    | number  | No       |
| errMsg       | If success false: Custom error message<br/>_Example:_ `"Transfer failed"`                        | string  | No       |

