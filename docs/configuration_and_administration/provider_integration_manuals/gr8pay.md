--- 
id: "gr8pay"
title: "GR8Pay"
hide_title: "true"
---

![](/img/providers/logos/gr8pay.png)

# GR8Pay

## About
GR8Pay is a payment platform offering credit card payments. Credit card payments supports Deposit, Refund, Void, Auth and Capture.

| Provider Name                | GR8Pay                                                          |
|------------------------------|-----------------------------------------------------------------|
| Link                         | [https://gr8pay.com/](https://gr8pay.com/)                      |
| Classification               | Aggregator provider                                             |
| Currencies                   | `USD/EUR/GBP`                                                   |
| Methods/PaymentTxTypes       | `CreditcardDeposit` <br/> `Void` <br/> `Refund` <br/> `Capture` |
| PaymentIQ Configuration File | `GR8Pay`                                                        |


## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.gr8pay.GR8PayConfig>
  <enabled>true</enabled>
  <testMode>true</testMode>
  <useViqProxy>true</useViqProxy>
  <accounts>
    <entry>
      <string>default</string>
      <account>
        <merchantId>???</merchantId> <!-- Provided by GR8Pay. "Merchant number" -->
        <secretKey>???</secretKey> <!-- Provided by GR8Pay. "Personal Hash Key" -->
        <merchantName>???</merchantName>
        <!--<authType>FINAL_AUTH</authType> Set this to make an authorization request-->
        <!--<supportedCurrencies>EUR|USD</supportedCurrencies> Optional-->
        <!--<container>window</container> Optional, defaults to iframe if not set-->
      </account>
    </entry>
  </accounts>
</com.devcode.paymentiq.integration.gr8pay.GR8PayConfig>
```
</details>

### Attributes

| Attribute            | Description                                                    |
|----------------------|----------------------------------------------------------------|
| account.merchantId   | Corresponds to the merchant number provided by GR8Pay.         |
| account.secretKey    | Corresponds to hash key provided by GR8Pay                     |
| account.merchantName | Corresponds to the merchant name provided by GR8Pay (optional) |

### GR8Pay merchant account
To setup GR8Pay in PaymentIQ the merchant first needs to obtain the following from GR8Pay:
* The Merchant number.
* Credentials for the merchant panel.
* The personal Hash Key.

## Example Routing Rules
![](/img/providers/routing/gr8pay.png)

## Test Information
### Credit Card:
- Any expiry date in the near future may be used and any 3-digit CVV code (4 digits for American Express).
- Use the following amounts to cause either approval or various declines:
    - 55.3 3D secure flow.
    - 0.04 Error 1001: Soft Decline.
    - 0.05 Error 1002: Insufficient Funds.
    - 0.91 Approved with 10 second delay.
    - 0.99 Approved with 90 second delay.

| Credit   Card Number | Issuer                |
|----------------------|-----------------------|
| 4387751111111111     | VISA (US)             |
| 5442987111111111     | MasterCard (US)       |
| 371000911111111      | American Express (US) |
| 4056850111111111     | Visa (FR)             |
| 5130113111111111     | MasterCard (FR)       |
| 36005131111111       | Diners Club (GB)      |
| 3535111111111111     | JCB (JP)              |
| 6221701111111111     | LivaKash (JP)         |
| 4580000000000000     | VISA (IL)             |
| 5326140000000000     | MasterCard (IL)       |
| 91000000             | IsraCard (IL)         |
