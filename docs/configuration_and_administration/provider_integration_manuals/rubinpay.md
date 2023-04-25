--- 
id: "rubinpay"
title: "RubinPay"
hide_title: "true"
---

![](/img/providers/logos/rubinpay.png)

# RubinPay

## About
RubinPay is a payment provider offering WebRedirect deposit.

| Provider Name                | RubinPay                          |
|------------------------------|-----------------------------------|
| Link                         | N/A                               |
| Classification               | Debit/Credit Card Processor       |
| Regions                      | `International`                   |
| Currencies                   | `CAD`, `USD`, `EUR`, `JPY`, `NOK` |
| Methods/PaymentTxTypes       | `WebRedirectDeposit`              |
| PaymentIQ Configuration File | `RubinPayConfig`                  |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.rubinpay.RubinPayConfig>
    <enabled>true</enabled>
    <testMode>true</testMode>
    <accounts>
        <entry>
            <string>DEFAULT</string>
            <account>
                <merchantId>{account.merchantId}</merchantId>
                <supportedCurrencies>EUR|USD|CAD|JPY|NOK</supportedCurrencies>
                <container>window</container>
            </account>
        </entry>
    </accounts>
</com.devcode.paymentiq.integration.rubinpay.RubinPayConfig>
```
</details>

### Attributes
| Attribute          | Description                              |
|--------------------|------------------------------------------|
| account.merchantId | Unique merchant ID provided by provider. |

### Callback URL

Please ask RubinPay to configure "callback" URLs:

TEST<br/>
https://test-api.paymentiq.io/paymentiq/api/rubinpay/callback

PRODUCTION<br/>
https://api.paymentiq.io/paymentiq/api/rubinpay/callback

## Example Routing Rule
![](/img/providers/routing/rubinpay.png)

## Transaction Flow

### Deposits
1. User enters an amount in the cashier and clicks on "Deposit".
2. PaymentIQ sends a POST request to the PSP. An url is received in response, to which the user is redirected
   and where he fills in the info for completing transaction.
3. PaymentIQ receives a callback from the PSP and send back response with HTTP status 200.
   Provider uses callback to confirm transaction.
4. PaymentIQ pulls transaction status from RubinPay to verify and update transaction accordingly.

## Test Information

### BankID
Personal ID number:
- go to https://ra-preprod.bankidnorge.no/#/generate and press "Generate"
- fill in first name, last name, friendly name and press "Order"
- use the account number to log in (usually valid for a few days)<br/>
  One-time password (Engangskode): `otp`<br/>Personal password: `qwer1234`
  
NOTE: For this scenario user should have `countryCode` - `NOR`

### Test cards

| Card Number      | CVV          | Expiry Date     |
|------------------|--------------|-----------------|
| 4242424242424242 | Any 3 digits | Any future date |
| 5555555555554444 | Any 3 digits | Any future date |
