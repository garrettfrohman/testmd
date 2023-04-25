---
id: "notification"
---

# notification

This method is used by PaymentIQ to notify merchants of events related to transactions. This is optional to implement. Events including Notification (970), DisputeFiled (971) and DisputeResolved (972). It is only used by a limited set of providers such as Cryptopay, Coindirect, EasyPay, PayPal. If it is available for a provider you can find more information in the integration manual.

`POST/paymentiq/notification`

## Example Request

```json
{
  "txTypeId": "101",
  "txName": "CreditcardDeposit",
  "txRefId": "25A0324"
}
```

## Request Parameters

| Name             | Located In | Description                                                                                                                                                                                                                                                                                                      | Schema | Required |
|------------------|------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------|----------|
| txTypeId         | body       | Transaction type, e.g 971 = DisputeFiled<br/>_Example:_ `"101"`                                                                                                                                                                                                                                                  | string | Yes      |
| txName           | body       | Transaction name, e.g DisputeFiled<br/>_Example:_ `"CreditcardDeposit"`                                                                                                                                                                                                                                          | string | Yes      |
| txRefId          | body       | Transaction reference id sent to provider. It contains the PaymentIQ merchant-id and transaction-id separated by 'A', e.g. 100019999A26720<br/>_Example:_ `"25A0324"`                                                                                                                                            | string | Yes      |
| provider         | body       | Provider that processed the transaction, e.g. Neteller<br/>_Example:_ `"Neteller"`                                                                                                                                                                                                                               | string | No       |
| originTxId       | body       | Optional reference to the origin PaymentIQ transaction. This field is only populated when there is an origin transaction, e.g. when receiving dispute notification this field will refer to the transaction that is subject of dispute or when a kyc information have been verified.<br/>_Example:_ `"12321312"` | string | No       |
| userId           | body       | User's unique id, which can be a number or a username. Max 50 char.<br/>_Example:_ `"user_123"`                                                                                                                                                                                                                  | string | No       |
| pspRefId         | body       | The reference ID used by the Provider for the transaction.<br/>_Example:_ `"111111"`                                                                                                                                                                                                                             | string | No       |
| pspStatusMessage | body       | The status message returned from the PSP provider.<br/>_Example:_ `"Success"`                                                                                                                                                                                                                                    | string | No       |
| accountId        | body       | Optional ref to PaymentIQ account-id. The account-id is used for repeat payments.<br/>_Example:_ `"dd14cb2d-623f-46a9-9210-beb8d1f033c9."`                                                                                                                                                                       | string | No       |
| accountHolder    | body       | Optional name of the credit card holder or bank account holder<br/>_Example:_ `"John"`                                                                                                                                                                                                                           | string | No       |
| maskedAccount    | body       | Optional masked account<br/>_Example:_ `"411812******2410"`                                                                                                                                                                                                                                                      | string | No       |
| attributes       | body       | Echoing back the optional parameter sent in the payment request by merchant, or optional extraAttributes configured in MerchantConfig.<br/>_Example:_ `{"allow_manual_payout":"true"}`                                                                                                                           | string | No       |

## Example Response

```json
{
  "success": true,
  "errCode": "111111",
  "errMsg": "Transfer failed"
}
```

## Response Parameters

| Name    | Description                                                                                      | Schema  | Required |
| ------- | ------------------------------------------------------------------------------------------------ | ------- | -------- |
| success | True or false. If false then only the two last parameters will be appended<br/>_Example:_ `true` | boolean | Yes      |
| errCode | If success false: Custom error code<br/>_Example:_ `"111111"`                                    | number  | No       |
| errMsg  | If success false: Custom error message<br/>_Example:_ `"Transfer failed"`                        | string  | No       |
