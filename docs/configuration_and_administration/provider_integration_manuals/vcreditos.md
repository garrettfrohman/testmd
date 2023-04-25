--- 
id: "vcreditos" 
title: "VCreditos"
hide_title: "true"
---
 
![](/img/providers/logos/vcreditos.png)

# VCreditos

## About
VCreditos is an e-wallet focused on the Brazilian online gambling market providing easy and secure payment integration.

### VSI
The communication between servers always starts on VCreditos side, and the PaymentIQ API will give the response according to the request. Hence the VSI integration can not be used using the Cashier API but instead has to be integrated directly in the merchant’s own cashier interface using the Front End API request specified below. The different basic methods are needed: Deposit, Withdraw and Verification.

### Non VSI
With VCreditos API, merchants can integrate VCreditos to accept deposits and withdrawals from customers by requesting their VCreditos User ID and Secure ID. Unlike VSI, Non VSI can be used with the Cashier API

| Provider Name                | VCreditos                                                                                                                    |
|------------------------------|------------------------------------------------------------------------------------------------------------------------------|
| Link                         | [https://www.vcreditos.com/](https://www.vcreditos.com/)                                                                     |
| Classification               | Wallet                                                                                                                       |
| Regions                      | `Brazil`                                                                                                                     |
| Currencies                   | `BRL`, `USD`                                                                                                                 |
| Methods/PaymentTxTypes       | VSI (`VCreditosDeposit`, `VCreditosWithdrawal`),<br/> API or non VSI (`VCreditosWalletDeposit`, `VCreditosWalletWithdrawal`) |
| PaymentIQ Configuration File | `VCreditosConfig`                                                                                                            |

## Limits

### Non VSI Deposit
For BRL min are 10.00 and max 150,000.00
For USD min are 10.00 and max 50,000.00

### Non VSI Withdrawal
For BRL min are 10.00 and max 40,000.00
For USD min are 10.00 and max 10,000.00

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.vcreditos.VCreditosConfig>
  <enabled>true</enabled>
  <useViqProxy>false</useViqProxy>
  <accounts>
    <entry>
      <string>VSI</string>
      <account>
        <secretKey>??</secretKey>
        <supportedCurrencies>BRL|USD</supportedCurrencies>
      </account>
    </entry>
    <entry>
      <string>NON_VSI</string>
      <account>
        <pspPublicKey>??</pspPublicKey>
        <secretKey>??</secretKey>
        <supportedCurrencies>BRL|USD</supportedCurrencies>
      </account>
    </entry>
  </accounts>
  <testMode>true</testMode>
</com.devcode.paymentiq.integration.vcreditos.VCreditosConfig>
```

</details>

### Attributes

#### VSI

| Attribute | Description                                        |
|-----------|----------------------------------------------------|
| secretKey | Secret Key that is used to generate hash parameter |

#### NON VSI (API)

| Attribute    | Description                                                                                                                 |
|--------------|-----------------------------------------------------------------------------------------------------------------------------|
| pspPublicKey | Corresponds to the Pre-shared public key from VCreditos. It is used as an 'Authorization' request header for each operation |
| secretKey    | Corresponds to the signing key from VCreditos. It is used to create JWT token                                               |

## Example Routing Rules
![](/img/providers/routing/vcreditos.png)

## Test Information

### VSI

#### Request URL

| Environment | Base Request URL                           |
|-------------|--------------------------------------------|
| TEST        | https://test-bo.paymentiq.io/paymentiq/api |
| PROD        | https://api.paymentiq.io/paymentiq/api     |

#### Request Parameters

| Attribute      | Mandatory | Type    | Description                                                                                                                                                  |
|----------------|-----------|---------|--------------------------------------------------------------------------------------------------------------------------------------------------------------|
| transfer_id    | Yes       | String  | Unique transaction ID in Merchant system                                                                                                                     |
| related_id     | Yes       | String  | Unique transaction ID in PaymentIQ (is used in verification request)                                                                                         |
| psp_user_id    | Yes       | String  | Payment method account identifier (like Skrill email, Neteller ID)                                                                                           |
| user_id        | Yes       | String  | User ID in Merchant system                                                                                                                                   |
| user_name      | Yes       | String  | User name                                                                                                                                                    |
| user_birthdate | Yes       | String  | User date of birth in format YYYY-MM-DD                                                                                                                      |
| user_ip        | Yes       | String  | User IP                                                                                                                                                      |
| amount         | Yes       | String  | Payment amount in format ##.## (e.g. 10.00)                                                                                                                  |
| currency       | Yes       | String  | Case sensitive currency (e.g. BRL or USD)                                                                                                                    |
| merchant_id    | Yes       | Numeric | Merchant identifier in PaymentIQ system                                                                                                                      |
| hash           | Yes       | String  | Generated hash (see details below)                                                                                                                           |
| session_id     | Yes       | String  | Session ID from the Merchant system that will be used to authorize user's payments (it is the same session ID that is present for each payment in PaymentIQ) |
| is_user_agent  | Yes       | Boolean | Identifies AGENT accounts (true or false) in merchant system that can be used for close loop validations                                                     |

#### Response Parameters

| Attribute  | Type    | Description                                   |
|------------|---------|-----------------------------------------------|
| status     | String  | Payment status (e.g. success, pending, error) |
| related_id | String  | Unique transaction ID on Merchant site        |
| error_code | Numeric | Error code in case of error response          |
| message    | String  | Error description in case of error response   |

#### Response statuses

| Status  | Description                                                          |
|---------|----------------------------------------------------------------------|
| SUCCESS | Payment operation is successful                                      |
| PENDING | Payment is in progress e.g. must be approved at PaymentIQ backoffice |
| ERROR   | Payment operation failed                                             |

#### Response error codes

| Code | Description                                           |
|------|-------------------------------------------------------|
| 00   | Success                                               |
| 01   | Date format is invalid                                |
| 02   | Date is invalid                                       |
| 03   | The transaction failed to succeed                     |
| 04   | Something went wrong while processing the transaction |
| 05   | Transaction status is invalid                         |
| 06   | Invalid hash                                          |
| 07   | Currency not supported                                |
| 08   | Request currency is not the same as user currency     |
| 09   | Request body is missing or empty                      |
| 10   | Transaction id was already used                       |
| 11   | Invalid transaction id                                |
| 12   | Transaction wasn't created                            |
| 13   | Validation failed. Transaction is invalid             |

#### Deposit

To initiate a deposit please send a corresponding request to `{base.request.url}/vcreditos/vsi/deposit/process` as shown below:

```json
curl -i -X POST \
   -H "Content-Type:application/x-www-form-urlencoded" \
   -d "transfer_id={uniqueTxId}" \
   -d "user_id={userId}" \
   -d "user_name=Bill" \
   -d "user_birthdate=1980-01-01" \
   -d "user_ip=54.215.9.11" \
   -d "amount=12.55" \
   -d "currency=BRL" \
   -d "merchant_id={piqMid}" \
   -d "hash={hash}" \
   -d "session_id={sessionId}" \
   -d "is_user_agent=true" \
   -d "psp_user_id={pspUserId}" \
 'https://test-bo.paymentiq.io/paymentiq/api/vcreditos/vsi/deposit/process'
```

In case of failed operation you could receive

```json
{
  "status": "ERROR",
  "error_code": "06",
  "message": "Invalid hash"
}
```

#### Withdrawal

To initiate a withdrawal please send a corresponding request to `{base.request.url}/vcreditos/vsi/withdrawal/process` as shown below:

```json
curl -i -X POST \
   -H "Content-Type:application/x-www-form-urlencoded" \
   -d "transfer_id={uniqueTxId}" \
   -d "user_id={userId}" \
   -d "user_name=Bill" \
   -d "user_birthdate=1980-01-01" \
   -d "user_ip=54.215.9.11" \
   -d "amount=12.55" \
   -d "currency=BRL" \
   -d "merchant_id={piqMid}" \
   -d "hash={hash}" \
   -d "session_id={sessionId}" \
   -d "is_user_agent=true" \
   -d "psp_user_id={pspUserId}" \
 'https://test-bo.paymentiq.io/paymentiq/api/vcreditos/vsi/withdrawal/process'
```

In case of successful operation you could receive

```json
{
  "status": "SUCCESS",
  "related_id": "1024A1447762"
}
```

**NOTE:** deposit and withdrawal are one time request examples and for each new request you will have to set unique `transfer_id` and generate a new `hash`.

#### Verification

To verify payment please send a corresponding request to `{base.request.url}/vcreditos/vsi/verification` as shown below:

```json
curl -i -X POST \
   -H "Content-Type:application/x-www-form-urlencoded" \
   -d "related_id=1024A1447762" \
   -d "transfer_id=74410" \
 'https://test-bo.paymentiq.io/paymentiq/api/vcreditos/vsi/verification'
```

In case of successful operation you could receive

```json
{
  "status": "SUCCESS",
  "related_id": "1024A1447762"
}
```

#### Hash generation

Please take a look to the example below to see how hash is generated. Please use below input to generate hash

`transfer_id + "+" + user_id + "+" + user_name + "+" + user_birthdate + "+" + psp_user_id + "+" + user_ip + "+" + amount + "+" + currency + "+" + merchant_id + "+" + secretKey`

`secretKey` -- provided by VCreditos/PIQ to generate hash.

Example

`sha512Hex("974+USD+Alan Walker+1980-11-11+207946+128.29.15.46+10.00+USD+4712+oeFG2hYY9zhbxn5cIoQMuZ7cm1yCMNKSxgN9PdmC") = 73f24b48eafb916f2997037429e3c40f079df075b6793d4c0c26ab8e229bdfa9243260a4e788a2dde3302d4cfcad8669636bfb00c6bff247da71de9e326ac10d`

Please note, generated hash must be lowercased.

### API (non VSI)

#### Deposit

The Deposit method is used to transfer funds from the user’s VCreditos account to his player account on the Merchant.

To initiate Deposit the user must specify:

_user_id_ - this is user VCreditos identifier, a numeric value
_user_secure_id_ - this is a generated PIN on VCreditos (when user wants to use VCreditos from outside of VCreditos)


#### Withdrawal

To initiate a withdrawal the user must specify:

_user_id_ - this is user VCreditos identifier, a numeric value
