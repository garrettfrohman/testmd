--- 
id: "borica" 
title: "Borica"
hide_title: "true"
---
 
![](/img/providers/logos/borica.png)

# Borica

## About
Borica is a credit card provider that offers secure payments through a redirect solution. Supported features are deposits using 3DS, void/capture flow and refunds.

| Provider Name                | Borica                                                                          |
|------------------------------|---------------------------------------------------------------------------------|
| Link                         | [https://www.borica.bg/en](https://www.borica.bg/en)                            |
| Classification               | Debit/Credit Card Processor                                                     |
| Regions                      | `Bulgaria`                                                                      |
| Currencies                   | Please check directly with the provider regarding what currencies are supported |
| Methods/PaymentTxTypes       | `WebRedirectDeposit` <br/> `Void` <br/> `Capture` <br/> `Refund`                |
| PaymentIQ Configuration File | `BoricaConfig`                                                                  |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.borica.BoricaConfig>
  <enabled>true</enabled>
  <accounts>
    <entry>
      <string>default</string>
      <account>
        <merchantId>???</merchantId>
        <terminal>???</terminal>
        <pspPublicKey>???</pspPublicKey>
        <pspPrivateKey>???</pspPrivateKey>
        <merchantName>???</merchantName>
        <supportedCurrencies>XXX|YYY</supportedCurrencies>
      </account>
    </entry>
  </accounts>
</com.devcode.paymentiq.integration.borica.BoricaConfig>
```

</details>

### Attributes
| Attribute         | Description                                                                       |
|-------------------|-----------------------------------------------------------------------------------|
| merchantId        | Provided by Borica                                                                |
| terminal          | Provided by Borica                                                                |
| pspPublicKey      | Provided by Borica                                                                |
| pspPrivateKey     | Created by PaymentIQ. Please contact support                                      |
| merchantName      | Used to display information to the cardholder on payment page                     |
| merchantUrl       | Optional. Merchant's primary web site URL                                         |
| email             | Optional. Used to send notifications about transaction results                    |
| defaultDescriptor | Optional. Descriptor must be set either in MerchantConfig or using this attribute |

### Transaction Descriptor
Borica requires that a transaction descriptor is sent with every payment. The merchant needs to configure a descriptor either in MerchantConfig property `<defaultTransactionDescriptor>` or directly in BoricaConfig with the setting `<defaultDescriptor>`

## Example Routing Rule
![](/img/providers/routing/borica.png)

## Transaction Flow
The user will be redirected to the providers payment page where they will enter their credit card details. If 3DS is to be used there will be another redirect to the issuer challenge page.

![](/img/providers/borica.png)

## Test Information

Please check directly with the provider.