---
id: "cezam"
title: "Cezam"
hide_title: "true"
---

![](/img/providers/logos/cezam.png)

# CashLib Cezam

## About
Cezam is a payment provider offering voucher (barcode) payments.
Cezam project permits a customer to make a direct deposit on his Merchant's account at a Distributor (SAF) Point of Sale (POS).

| Provider Name                | CashLib/Cezam                                                                                                                                              |
|------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Link                         | [https://backoffice-test.cashlib.com/documentation/cezam/merchant/index.html](https://backoffice-test.cashlib.com/documentation/cezam/merchant/index.html) |
| Classification               | Voucher                                                                                                                                                    |
| Supported Countries          | European Union member states                                                                                                                               |
| Currencies                   | `EUR`                                                                                                                                                      |
| Methods/PaymentTxTypes       | `WebredirectDeposit`<br/> `CezamVoucherDeposit` <br/> `Reversal`                                                                                           |
| PaymentIQ Configuration File | `CezamConfig`                                                                                                                                              |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.emp.cezam.CezamConfig>
    <enabled>true</enabled>
    <testMode>true</testMode>
    <apiKey>{apiKey}</apiKey>
    <maxTxCount>{maxTxCount}</maxTxCount>
    <maxTxAmount>{maxTxAmount}</maxTxAmount>
    <accounts>
        <entry>
            <string>DEFAULT</string>
            <account>
                <merchantId>{account.merchantId}</merchantId>
                <apiKey>{account.apiKey}</apiKey>
                <supportedCurrencies>EUR</supportedCurrencies>
                <container>window</container>
            </account>
        </entry>
    </accounts>
</com.devcode.paymentiq.integration.emp.cezam.CezamConfig>
```
</details>

### Attributes

| Attribute                | Description                                                                                                                                                                                                     |
|--------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| apiKey                   | Corresponds to the "API key" provided by Cezam.                                                                                                                                                                 |
| maxTxCount               | It can be used to set maximum count of transactions customer can make. Optional.                                                                                                                                |
| maxTxAmount              | It can be used to set maximum transaction amount customer can make. Optional.                                                                                                                                   |
| validCallbackIpAddresses | It is used to specify IPs where Cezam will send requests to PaymentIQ from. Please clarify such IPs with Cezam and ask PaymentIQ technical support to whitelist them.                                           |
| account.merchantId       | Corresponds to the "MID" parameter provided by Cezam.                                                                                                                                                           |
| account.apiKey           | Corresponds to the "API key" provided by Cezam. It is used to authenticate incoming request (same as "apiKey"). The difference is that specific `account.apiKey` will be used for a specific account. Optional. |

### Request URLs

To initiate or cancel payment you will need to ask Cezam to configure request URLs as shown below. It is required in order to receive a corresponding requests from Cezam.

### Test environment
```
https://test-api.paymentiq.io/paymentiq/api/cezam/validate/{merchantId}?account={pspAccount} - predeposit (validate if deposit can be made)
https://test-api.paymentiq.io/paymentiq/api/cezam/process/{merchantId}?account={pspAccount} - deposit (make a deposit)
https://test-api.paymentiq.io/paymentiq/api/cezam/cancel/{merchantId}?account={pspAccount} - cancel (cancel/reverse deposit)
```

### Production environment
```
https://api.paymentiq.io/paymentiq/api/cezam/validate/{merchantId}?account={pspAccount} - predeposit (validate if deposit can be made)
https://api.paymentiq.io/paymentiq/api/cezam/process/{merchantId}?account={pspAccount} - deposit (make a deposit)
https://api.paymentiq.io/paymentiq/api/cezam/cancel/{merchantId}?account={pspAccount} - cancel (cancel/reverse deposit)
```

Where<br/>
`merchantId` - is a merchant ID in PaymentIQ;<br/>
`account` - is an optional parameter, that can define PSP account name in CezamConfig. That PSP account can have `apiKey` defined, which can be used for authentication validation (more info in table above).

You can also use a simplified request URLs without `account` parameter:

```
https://{DOMAIN}/paymentiq/api/cezam/{OPERATION}/{merchantId}
```

In that case PSP account from the CezamConfig will not be used (PaymentIQ will use a config-level `apiKey` instead of account-level `apiKey` for validation).

## Operations Overview

### Predeposit and deposit

#### Request Parameters

| Name         | Description                                                                                                                                                      |
|--------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| request_id   | Unique request ID that identifies payment at CASHlib, containing no more than 64 digits <br/> e.g. `"12345678901234567890"`                                      |
| request_date | Request date in format `yyyy-MM-dd hh:mm:ss` <br/> e.g. `"2023-12-31 23:59:59"`                                                                                  |
| test         | Indicates if it is test (`Y`) or real (`N`) request. <br/> Possible values are `Y` - TEST and `N` - LIVE                                                         |
| customer_id  | Merchant Customer Id from barcode in format `xxx123456789`, where `xxx` represents merchant in Cezam system and `123456789` is numeric representation of user id |
| amount       | Amount in cents e.g. `1000` for `10.00 EUR`                                                                                                                      |
| currency     | Currency in ISO3 format e.g. `EUR`                                                                                                                               |

#### Request Example

```json
{
  "request_id": "12345678901234567890",
  "request_date": "2023-12-31 23:59:59",
  "test": "N",
  "customer_id": "1234567890000",
  "amount": 1000,
  "currency": "EUR"
}
```

### Cancel

#### Request Parameters

| Name              | Description                                                                                                                 |
|-------------------|-----------------------------------------------------------------------------------------------------------------------------|
| request_id        | Unique request ID that identifies payment at CASHlib, containing no more than 64 digits <br/> e.g. `"12345678901234567890"` |
| request_date      | Request date in format `yyyy-MM-dd hh:mm:ss` <br/> e.g. `"2023-12-31 23:59:59"`                                             |
| test              | Indicates if it is test (`Y`) or real (`N`) request. <br/> Possible values are `Y` - TEST and `N` - LIVE                    |
| request_id_cancel | Request ID of the payment you want to cancel/revert, containing no more than 64 digits <br/> e.g. `"12345678901234567890"`  |

#### Example

```json
{
  "request_id": "98765432109876543210",
  "request_date": "2023-12-31 23:59:59",
  "test": "N",
  "request_id_cancel": "12345678901234567890"
}
```

## Error Status Codes

| Name                      | Code | Message                                                            |
|---------------------------|------|--------------------------------------------------------------------|
| InvalidRequest            | 1    | The JSON payload is malformed                                      |
| MissingApiKey             | 2    | No API Key in request                                              |
| InvalidApiKey             | 3    | The API Key does not match                                         |
| NoApiKeyConfigured        | 4    | API Key is not configured                                          |
| NonWhitelistedIP          | 5    | Received request from untrusted IP                                 |
| ConfigNotFound            | 7    | Cezam configuration is missing                                     |
| MissingCustomerId         | 8    | No customer_id in request                                          |
| InvalidCustomerId         | 9    | Invalid customer_id                                                |
| TransactionFailed         | 10   | The transaction failed for some reason                             |
| DuplicatePaymentTx        | 11   | We already have a transaction with the same transaction identifier |
| MissingTx                 | 12   | Missing transaction                                                |
| MissingBarCodeTx          | 13   | Missing transaction with barcode                                   |
| MissingTransactionId      | 14   | No transaction id in request                                       |
| CanceledAlready           | 15   | Transaction canceled already                                       |
| ConnectionIssue           | 16   | Issue connecting to external system                                |
| Fraud                     | 17   | Fraud or suspicious activity                                       |
| UserBlocked               | 18   | This user is blocked                                               |
| MerchantNotFound          | 19   | The merchant was not found                                         |
| AmountAboveLimit          | 20   | Amount above limit                                                 |
| NoFunds                   | 22   | No funds                                                           |
| Exception                 | 23   | An unexpected error occurred                                       |
| SystemError               | 24   | System error                                                       |
| UserNotFound              | 25   | User not found                                                     |
| FraudMaxTxAmountOverdrawn | 26   | Maximum tx amount reached                                          |
| FraudMaxNrOfTxOverdrawn   | 27   | Maximum number of transactions reached                             |
| InvalidRequestId          | 28   | Invalid request_id                                                 |

## Example Routing Rule

Routing rules for making deposit related operations and requesting a new bar code.

![](/img/providers/routing/cezam.png)

## Payment Flow

Each merchant will have a unique number (three digits number) assigned by Cezam so that they can identify them during payments at the point of sale (POS).<br/>
Each merchant's customer will also have a unique number (ten digits number) at Cezam.<br/>
`123XXXXXXXXXX` represents a bar code (generated by the provider), whose `X` represents the customer identifiers and `123` the merchant identifier.

Customer goes to the POS with the barcode and pays the amount he wants to deposit.<br/>
The distributor communicates this `13` digits bar code to Cezam with the amount, then Cezam calls the corresponding partner with the first `3` digits and then calls PaymentIQ to initiate a deposit.

A deposit can be made only once for the amount chosen at the point of sale. A bar code itself can be used without limit in number of deposits and also in time.

There are two possible flows:

### Predeposit and deposit

When the predeposit is configured, it lets Cezam know if they can make a deposit with regards to the `customer_id`, but it doesn't make the deposit. If Cezam gets a positive answer from PaymentIQ, they announce to the distributor that the deposit will be made.<br/>
At this point, Cezam waits 5 minutes, the time for which the distributor can cancel, and if there is no request from the distributor, Cezam makes a deposit. There will be no cancellation request from the distributor after this time.

#### Possible scenarios

Scenario 1:<br/>
- Distributor said payment is done
- Cezam calls "predeposit" and replies "OK" to the distributor
- After 5 minutes Cezam calls "deposit"

Scenario 2:<br/>
- Distributor said payment is done
- Cezam calls "predeposit" and replies "OK" to the distributor
- Distributor "cancel" (before 5 minutes)
- Cezam doesn't call "deposit"

### Deposit and cancel

Cezam call PaymentIQ for a deposit directly after the distributor's call, and the distributor can call Cezam to cancel within 5 minutes, in this case Cezam call PaymentIQ to make the cancel.<br/>
The distributor can cancel a deposit within a maximum of 5 minutes after a deposit has been made (these are the cases where they would have had a problem on their side).<br/>
If the distributor calls Cezam after 5 minutes, they do not call the PaymentIQ.

#### Possible scenarios

Scenario 1:<br/>
- Distributor said payment is done
- Cezam calls "deposit" and replies "OK" to the distributor

Scenario 2:<br/>
- Distributor said payment is done
- Cezam calls "deposit" and replies "OK" to the distributor
- Distributor "cancel" (before 5 minutes)
- Cezam calls "cancel" and answers to the distributor

Scenario 3:<br/>
- Distributor said payment is done
- Cezam calls "deposit" and replies "OK" to the distributor
- Distributor "cancel" (after 5 minutes) and Cezam answers NOK to the distributor

More details about whole flows in Cezam documentation. See [Cezam-Flow](https://backoffice-test.cashlib.com/documentation/cezam/merchant/index.html#section/Cezam-Flow).

### Generate bar code

Merchant can generate a bar code by using API endpoint provided by the Cezam

https://api.cashlib.com/api/merchant/cezam/barcode
https://backoffice-test.cashlib.com/api/merchant/cezam/barcode

with `apiKey` header and request:

```json
{
  "mid": "{mid}",
  "customer_id": "{userId}",
  "count": "{maxTxCount}",
  "amount": "{maxTxAmount}"
}
```
As a response you will receive:

```json
{
"status": 0,
"barcode": "1234567890128",
"barcode_image": "iVBORw0KGgoAAAA..."
}
```
For more info please check Cezam documentation [here](https://backoffice-test.cashlib.com/documentation/cezam/merchant/index.html#tag/API/paths/~1api~1merchant~1cezam~1barcode/post).

Also, you can generate a barcode via PaymentIQ by sending a corresponding deposit request with `WebRedirectDeposit` transaction type and `0` (zero) amount.

## Test Information

### Deposit
To simulate deposit, you can execute below cURL command (please replace apiKey, mid, barcode and amount fields with respective values).

```
curl --header "Content-Type: application/json" \
  --header "accept: application/json" \
  --header "apikey: {accoint.apiKey}" \
  --request POST \
  --data '{"mid": "{accoint.merchantId}", "barcode": "{barcode}", "amount": 1000}' \
  https://backoffice-test.cashlib.com/api/merchant/cezam/simulate-deposit
```
In case of successful operation you will receive response containing `deposit_id` parameter (it will be used to cance deposit (see below)):

```json
{"status":0,"result":"Deposit Success","deposit_id":"62d7a720c99c2-62d7a720c99c3"}
```

### Cancel
To cancel a deposit, you can execute below cURL command (please replace apiKey, mid, barcode and amount fields with respective values).

```
curl --header "Content-Type: application/json" \
  --header "accept: application/json" \
  --header "apikey: {account.apiKey}" \
  --request POST \
  --data '{"mid": "{accoint.merchantId}", "deposit_id": "{deposit_id}"}' \
  https://backoffice-test.cashlib.com/api/merchant/cezam/simulate-cancel
```
In case of successful operation you will receive response:

```json
{"status":0,"result":"Cancel Success"}
```

### Note
You can check transaction status at Cezam side by accessing their back office at [https://backoffice-test.cashlib.com/transaction/](https://backoffice-test.cashlib.com/transaction/). You will need to have active account to do so.
