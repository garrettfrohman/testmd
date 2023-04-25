--- 
id: "impaya" 
title: "IMPAYA"
hide_title: "true"
---
 
![](/img/providers/logos/impaya.png)

# IMPAYA

## About
IMPAYA is a payment provider offering creditcard deposit (3DS and non 3DS, depending on card), withdrawal and full/partial refund.

| Provider Name                | IMPAYA                                                                                                                                                                                                           |
|------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Link                         | [https://www.impaya.com/](https://www.impaya.com/)                                                                                                                                                               |
| Classification               | Debit/Credit Card Processor                                                                                                                                                                                      |
| Regions                      | International                                                                                                                                                                                                    |
| Currencies                   | `AUD`, `BRL`, `GBP`, `CAD`, `CNY`, `HRK`, `CZK`, `DKK`, `EUR`, `HKD`, `HUF`, `INR`, `IDR`, `JPY`, `MYR`, `MXN`, `NOK`, `PHP`, `PLN`, `RON`, `RUB`, `ZAR`, `SEK`, `CHF`, `THB`, `TRY`, `UAH`, `AED`, `USD`, `VND` |
| Methods/PaymentTxTypes       | `CreditcardDeposit`<br/>`CreditcardWithdrawal`<br/>`Refund`                                                                                                                                                      |
| PaymentIQ Configuration File | `ImpayaConfig`                                                                                                                                                                                                   |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.impaya.ImpayaConfig>
  <enabled>true</enabled>
  <useViqProxy>true</useViqProxy>
  <accounts>
    <entry>
      <string>DEFAULT</string>
      <account>
        <merchantId>??</merchantId>
        <secretKey>??</secretKey>
        <supportedCurrencies>EUR|USD|RUB</supportedCurrencies>
      </account>
    </entry>
  </accounts>
  <container>window</container>
  <defaultDescriptor>Payment: ${ptx.txRefId}</defaultDescriptor>
</com.devcode.paymentiq.integration.impaya.ImpayaConfig>
```
</details>

### Attributes

| Attribute  | Description                                                                                        |
|------------|----------------------------------------------------------------------------------------------------|
| merchantId | Corresponds to *Merchant ID* from IMPAYA. It identifies a merchant at IMPAYA side.                 |
| secretKey  | Corresponds to *Merchant Secret* from IMPAYA. It is used to sign requests that are sent to IMPAYA. |

### Callback URL
Please ask IMPAYA to configure "redirect" and "callback" URLs:

#### TEST
https://test-api.paymentiq.io/paymentiq/api/impaya/redirect

https://test-api.paymentiq.io/paymentiq/api/impaya/callback

#### PRODUCTION
https://api.paymentiq.io/paymentiq/api/impaya/redirect

https://api.paymentiq.io/paymentiq/api/impaya/callback

### Refund Flow

Refund is initiated from PaymentIQ back office. Then IMPAYA will need to process it manually, and once it is done, "status" notification will be sent to PaymentIQ with actual tx status (status_id=5 -- successful refund).

## Example Routing Rule
![](/img/providers/routing/impaya.png)

## Test Information

IMPAYA doesn't have a TEST or SANDBOX environment and due to this testing should be done with PROD account settings and using real cards.

