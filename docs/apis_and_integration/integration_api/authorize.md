---
id: "authorize"
---

# authorize

This method is called by PaymentIQ so the Operator Platform can authorize a payment before it is getting processed. The Operator Platform should verify that the user is allowed to process and also reserve amount for future debit and check that the user account will not be over debited. If the Operator Platform response is success, then PaymentIQ will continue with processing of the payment transaction. If not, then PaymentIQ will decline the transaction with the status code returned by the Operator Platform.

`POST/paymentiq/authorize`

## Example Request

```json
{
  "userId": "user_123",
  "txAmount": "100.50",
  "txAmountCy": "SEK",
  "txId": "12345",
  "txTypeId": 108,
  "txName": "CreditcardDeposit",
  "provider": "BamboraGa"
}
```

## Request Parameters

| Name          | Located In | Description                                                                                                                                                                                                                                                                                                                                     | Schema | Required |
|---------------|------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------|----------|
| userId        | body       | User's unique id, which can be a number or a username. Max 50 char.<br/>_Example:_ `"user_123"`                                                                                                                                                                                                                                                 | string | Yes      |
| txAmount      | body       | Requested transaction amount, formatted like 100.50 (only digits and dot as decimal separator). A negative amount will decrease the account balance and must therefore be reserved until captured or canceled by PaymentIQ. Note: This amount should not be trusted because the final amount in transfer might differ<br/>_Example:_ `"100.50"` | string | Yes      |
| txAmountCy    | body       | Transaction currency. 3-letter code according to ISO standard, e.g SEK. If currency is not the same as player's registered currency then the merchant has to do a currency exchange or decline the transaction.<br/>_Example:_ `"SEK"`                                                                                                          | string | Yes      |
| txId          | body       | PaymentIQ unique transaction-id<br/>_Example:_ `"12345"`                                                                                                                                                                                                                                                                                        | string | Yes      |
| txTypeId      | body       | Transaction type, e.g 101 = Neteller deposit<br/>_Example:_ `108`                                                                                                                                                                                                                                                                               | string | Yes      |
| txName        | body       | Transaction name, e.g NetellerDeposit<br/>_Example:_ `"CreditcardDeposit"`                                                                                                                                                                                                                                                                      | string | Yes      |
| provider      | body       | Provider that processed the transaction<br/>_Example:_ `"BamboraGa"`                                                                                                                                                                                                                                                                            | string | Yes      |
| pspService    | body       | Optional payment service used when an aggregating provider has several underlaying services. E.g. provider='Envoy' and pspService='IDEAL'<br/>_Example:_ `"IDEAL"`                                                                                                                                                                              | string | No       |
| originTxId    | body       | Transaction id that is origin to this transaction<br/>_Example:_ `"123456789"`                                                                                                                                                                                                                                                                  | string | No       |
| accountId     | body       | Optional ref to PaymentIQ account-id. The account-id is used for repeat payments.<br/>_Example:_ `"dd14cb2d-623f-46a9-9210-beb8d1f033c9"`                                                                                                                                                                                                       | string | No       |
| accountHolder | body       | Optional name of the credit card holder or bank account holder<br/>_Example:_ `"John"`                                                                                                                                                                                                                                                          | string | No       |
| maskedAccount | body       | Optional masked account<br/>_Example:_ `"411812******2410"`                                                                                                                                                                                                                                                                                     | string | No       |
| pspFee        | body       | Expected fee from the provider. Calculated by PaymentIQ provider Fee rules. <br/>_Example:_ `"123"`                                                                                                                                                                                                                                             | string | No       |
| pspFeeCy      | body       | PSP fee currency. 3-letter code according to ISO standard, e.g SEK. <br/>_Example:_ `"SEK"`                                                                                                                                                                                                                                                     | string | No       |
| pspFeeBase    | body       | Expected fee from the provider in the base currency. Calculated by PaymentIQ provider Fee rules. <br/>_Example:_ `"20"`                                                                                                                                                                                                                         | string | No       |
| pspFeeBaseCy  | body       | Currency for the fee in the base currency. 3-letter code according to ISO standard, e.g SEK.<br/>_Example:_ `"SEK"`                                                                                                                                                                                                                             | string | No       |
| attributes    | body       | Echoing back the optional parameter sent in the payment request by merchant, or optional extraAttributes configured in MerchantConfig.<br/>_Example:_ `{"allow_manual_payout":"true"}`                                                                                                                                                          | string | No       |

## Example Response

```json
{
  "userId": "user_123",
  "success": true,
  "merchantTxId": "111111111",
  "authCode": "550e8400-e29b-41d4-a716-446655440000",
  "errCode": "10001",
  "errMsg": "Authorize failed",
  "updatedUser": {
    "kycStatus": "Approved"
  }
}
```

## Response Parameters

| Name         | Description                                                                                                                                                         | Schema  | Required |
|--------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------|----------|
| userId       | Player user-id. Should be unique for a player. It will be the same as the request parameter userId.<br/>_Example:_ `"user_123"`                                     | string  | Yes      |
| success      | True or false. If false then only the two last parameters will be appended<br/>_Example:_ `true`                                                                    | boolean | Yes      |
| merchantTxId | Merchant's unique transaction-id<br/>_Example:_ `"111111111"`                                                                                                       | number  | No       |
| authCode     | Unique authorization code. It is recommended to use a UUID<br/>_Example:_ `"550e8400-e29b-41d4-a716-446655440000"`                                                  | string  | Yes      |
| errCode      | If success false: Custom error code<br/>_Example:_ `"10001"`                                                                                                        | number  | No       |
| errMsg       | If success false: Custom error message<br/>_Example:_ `"Authorize failed"`                                                                                          | string  | No       |
| updatedUser  | Can be used to update any user fields. The parameter structure for this object is the same as in the VerifyUser response.<br/>_Example:_ `{"kycStatus":"Approved"}` | string  | No       |



