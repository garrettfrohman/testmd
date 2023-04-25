--- 
id: "trustspay" 
title: "TrustSPay"
hide_title: "true"
---
 
![](/img/providers/logos/trustspay.png)

# TrustSPay

## About
TrustSPay is online credit card payment service provider, which is specialized in processing Gaming merchants focused on processing miscode/unlicense transactions. Multi-currency transactions are supported from all over the world (only China is unavailable). TrustSPay is able to provide Visa/MC/Amex/Discover/JCB MID's.

:::warning

Please note that TrustSPay does not support 3DS2 transactions.

:::

| Provider Name                | TrustSPay                                                                       |
|------------------------------|---------------------------------------------------------------------------------|
| Link                         | not available                                                                   |
| Classification               | Debit/Credit Card Processor                                                     |
| Regions                      | ALL except China                                                                |
| Currencies                   | Please check directly with the provider regarding what currencies are supported |
| Methods/PaymentTxTypes       | `CreditcardDeposit`, `Refund`                                                   |
| PaymentIQ Configuration File | `TrustSPayConfig`                                                               |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.trustspay.TrustSPayConfig>
    <enabled>true</enabled>
    <useViqProxy>true</useViqProxy>
    <accounts>
        <entry>
            <string>TRUSTSPAY</string>
            <account>
                <use3Dsecure>true</use3Dsecure>
                <merchantId>??</merchantId>
                <secretKey>??</secretKey>
                <supportedCurrencies>EUR|USD</supportedCurrencies>
                <gatewayNo>??</gatewayNo>
            </account>
        </entry>
    </accounts>
    <testMode>false</testMode>
    <defaultDescriptor>DevCode payment</defaultDescriptor>
</com.devcode.paymentiq.integration.trustspay.TrustSPayConfig>
```

</details>

### Attributes

| Attribute                | Description                                                    |
|--------------------------|----------------------------------------------------------------|
| accountConfig.merchantId | Corresponds to the *merNo* from TrustSPay.                     |
| accountConfig.secretKey  | Key provided by TrustSPay used for creating SHA-256 signature. |
| accountConfig.gatewayNo  | Corresponds to the *gatewayNo* from TrustSPay.                 |

## Example Routing Rule

![](/img/providers/routing/trustspay.png)

## Test Information

| Card Number      | CVV | Expiry Date     |
|------------------|-----|-----------------|
| 5275331548947882 | Any | Any future date |
| 5393470277337555 | Any | Any future date |
| 5419256278398385 | Any | Any future date |

Note: these cards can be used on test non-3ds endpoint https://shoppingingstore.com/TestTPInterface. To use this endpoint `testMode` should be set as `true` and `use3DSecure` should be `false` in xml configuration. In all other cases REAL cards should be used.