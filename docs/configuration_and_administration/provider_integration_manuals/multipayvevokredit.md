--- 
id: "multipayvevokredit" 
title: "MultiPay VevoKredit"
hide_title: "true"
---
 
![](/img/providers/logos/multipay.png)

# MultiPay VevoKredit

## About
MultiPay VevoKredit is a credit card processor with support for Deposits and status check.

| Provider Name                | MultiPay                                       |
|------------------------------|------------------------------------------------|
| Link                         | [https://multipay.vip/](https://multipay.vip/) |
| Classification               | Credit Card Processor                          |
| Regions                      | `International`                                |
| Currencies                   | `TRY`                                          |
| Methods/PaymentTxTypes       | `CreditcardDeposit`                            |
| PaymentIQ Configuration File | `MultiPayConfig`                               |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.multipay.MultiPayConfig>
  <enabled>true</enabled>
  <useViqProxy>true</useViqProxy>
  <accounts>
    <entry>
     <string>default</string>
     <account>
        <apiToken>???</apiToken> <!-- API Token -->
        <secretKey>???</secretKey> <!-- Api Key -->
        <supportedCurrencies>USD|EUR|NOK|TRY</supportedCurrencies>
     </account>
    </entry>
  </accounts>
  <testMode>false</testMode>
</com.devcode.paymentiq.integration.multipay.MultiPayConfig>
```
</details>

### Attributes

| Attribute               | Description                                                                          |
|-------------------------|--------------------------------------------------------------------------------------|
| accountConfig.apiToken  | Provided by Multipay as Api Token. Used for authenticating all API requests          |
| accountConfig.secretKey | Provided by Multipay as Api Key. Used for calculating the signature for the requests |

### Callback URL

Before testing, merchant needs to ask MultiPay team to set callback URLS

#### TEST
https://test-api.paymentiq.io/paymentiq/api/multipay/callback

#### PRODUCTION
https://api.paymentiq.io/paymentiq/api/multipay/callback

## Example Routing Rules

![](/img/providers/routing/multipay.png)

## Test Information

The transaction is initiated from the cashier as VevoKredit payment method.

The user enters the amount and the essential credit card parameters - number, holder name, CVV code and expiry date `(MM/YYYY)`.

After that the user gets redirected to another page where entering an OTP code is required. 

Then PaymentIQ receives a callback with the transaction's result and verifies its status with the provider's endpoint.

### Credit cards

One needs to contact MultiPay support team for test credit cards and OTP code when testing the Api.