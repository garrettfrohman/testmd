--- 
id: "onetopay" 
title: "OneToPay"
hide_title: "true"
---
 
![](/img/providers/logos/onetopay.png)

# OneToPay

## About

| Provider Name                | OneToPay                                                                        |
|------------------------------|---------------------------------------------------------------------------------|
| Link                         | not available                                                                   |
| Classification               | Debit/Credit Card Processor                                                     |
| Regions                      | ALL except China                                                                |
| Currencies                   | Please check directly with the provider regarding what currencies are supported |
| Methods/PaymentTxTypes       | `CreditcardDeposit`, `Refund`                                                   |
| PaymentIQ Configuration File | `OneToPayConfig`                                                                |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.onetopay.OneToPayConfig>
    <enabled>true</enabled>
    <useViqProxy>true</useViqProxy>
    <accounts>
        <entry>
            <string>DEFAULT</string>
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
</com.devcode.paymentiq.integration.onetopay.OneToPayConfig>
```

</details>

### Attributes

| Attribute                | Description                                                   |
|--------------------------|---------------------------------------------------------------|
| accountConfig.merchantId | Corresponds to the *merNo* from OneToPay.                     |
| accountConfig.secretKey  | Key provided by OneToPay used for creating SHA-256 signature. |
| accountConfig.gatewayNo  | Corresponds to the *gatewayNo* from OneToPay.                 |

## Provider Configuration

1. The above XML template (OneToPayConfig) will need to be added via backoffice Admin -> Configuration.
2. Routing needs to be added for CreditcardDeposit in Routing -> Routing.

## Example Routing Rule

![](/img/providers/routing/onetopay.png)

## Transaction Flow

1. The end user enters the transaction amount and relevant credit card information.
2. PaymentIQ sends the deposit request to OneToPay.
3. OneToPay responds with an initial status (for 3DS also with redirectUrl) acknowledging they have received the PaymentIQ request and begin processing.
4. After the payment is complete, OneToPay sends back a callback notification once the transaction status has changed.

## Test Information
| Card Number      | CVV | Expiry Date     |
|------------------|-----|-----------------|
| 5275331548947882 | Any | Any future date |
| 5393470277337555 | Any | Any future date |
| 5419256278398385 | Any | Any future date |

Note: these cards can be used on test non-3ds and 3ds endpoints.

N3DS: https://pay.onetopay.net/interface/WSTestTPInterface
3DS: https://pay.onetopay.net/interface/WSTestDirectInterface

To use these endpoints `testMode` should be set as `true`. For N3DS, `use3DSecure` should be `false` in xml configuration. For 3DS, it should be `true`. In all other cases REAL cards should be used.