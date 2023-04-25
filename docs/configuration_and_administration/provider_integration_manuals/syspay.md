--- 
id: "syspay" 
title: "SysPay"
hide_title: "true"
---
 
![](/img/providers/logos/syspay.png)

# SysPay

## About
SysPay is a credit card provider that offers 3DS and N3DS deposit (sale, authorization + capture), void, refund and status check (no withdrawal).

| Provider Name                | SysPay                                                                                                                                                          |
|------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Link                         | [https://app.syspay.com/](https://app.syspay.com/)                                                                                                              |
| Classification               | Debit/Credit Card Processor                                                                                                                                     |
| Regions                      | International                                                                                                                                                   |
| Currencies                   | `ARS`, `AUD`, `BRL`, `GBP`, `BGN`, `CAD`, `CLP`, `COP`, `HRK`, `CZK`, `DKK`, `EUR`, `HUF`, `INR`, `LTL`, `MXN`, `NOK`, `PLN`, `RON`, `SEK`, `CHF`, `TRY`, `USD` |
| Methods/PaymentTxTypes       | `CreditcardDeposit`, `Refund`, `Capture`, `Void`                                                                                                                |
| PaymentIQ Configuration File | `SysPayConfig`                                                                                                                                                  |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.syspay.SysPayConfig>
  <enabled>true</enabled>
  <useViqProxy>true</useViqProxy>
  <accounts>
    <entry>
      <string>DEFAULT</string>
      <account>
        <secretKey>??</secretKey>
        <supportedCurrencies>EUR</supportedCurrencies>
        <apiKey>??</apiKey>
        <useTokenId>false</useTokenId>
        <authType>AUTH_CAPTURE</authType><!--AUTH_CAPTURE|FINAL_AUTH-->
      </account>
    </entry>
  </accounts>
  <testMode>true</testMode>
  <container>window</container>
  <defaultDescriptor>Bambora payment</defaultDescriptor>
</com.devcode.paymentiq.integration.syspay.SysPayConfig>
```
</details>

### Attributes

| Attribute               | Description                                                                                                    |
|-------------------------|----------------------------------------------------------------------------------------------------------------|
| accountConfig.apiKey    | Corresponds to the *API login* from SysPay                                                                     |
| accountConfig.secretKey | Corresponds to the *API passphrase* from SysPay to authorize request (it is used to build a request signature) |

## Example Routing Rules
![](/img/providers/routing/syspay.png)

## Test Information

#### Card Number

Any 16 digits card number starting with ‘4’ (VISA) or ‘5’ (Mastercard): 4111 1111 1111 1111, 5555 5555 5555 4444

#### Security Code

The validation follows the scheme of the card used, so any 3 digits for VISA/MC, or 4 digits for Amex

#### Expiration Date

- 01/2021
    - SUCCESS payment

- 02/2021
    - FAILED payment
    - INSUFFICIENT_FUNDS reason

- 03/2021
    - FAILED payment
    - SOFT_DECLINE reason

- 04/2021
    - FAILED payment
    - HARD_DECLINE reason

- 12/2021
    - ERROR mandate

- 01/2028
    - SUCCESS payment
    - With 3DS redirection (This should be tested when implementing the server-2-server flow)
    - **Note:** 3DS must be enabled on the API configuration for the test

- 02/2028
    - FAILED payment
    - With 3DS redirection (This should be tested when implementing the server-2-server flow)
    - **Note:** 3DS must be enabled on the API configuration for the test
