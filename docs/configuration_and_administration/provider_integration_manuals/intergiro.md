--- 
id: "intergiro" 
title: "Intergiro"
hide_title: "true"
---

![](/img/providers/logos/intergiro.png)

# Intergiro

## About
Intergiro is an electronic money institution focused on providing current accounts and payment cards. 
Intergiro offers business account with IBAN, corporate payment cards to business entities.

| Provider Name                | Intergiro                                                                       |
|------------------------------|---------------------------------------------------------------------------------|
| Link                         | [https://intergiro.com/](https://intergiro.com/)                                |
| Classification               | `Debit/Credit Card Processor`                                                   |
| Regions                      | `EU`                                                                            |
| Currencies                   | Please check directly with the provider regarding what currencies are supported |
| Methods/PaymentTxTypes       | `CreditcardDeposit` <br/> `Capture` <br/> `Void` <br/> `Refund`                 |
| PaymentIQ Configuration File | `IntergiroConfig`                                                               |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.intergiro.IntergiroConfig>
    <enabled>true</enabled>
    <useViqProxy>true</useViqProxy>
    <accounts>
        <entry>
            <string>DEFAULT</string>
            <account>
                <pspPrivateKey>??</pspPrivateKey>
                <pspPublicKey>??</pspPublicKey>
                <supportedCurrencies>USD|EUR</supportedCurrencies>
                <authType>??</authType>
                <cardOnFileType>INITIAL_RECURRING</cardOnFileType>
                <useTokenId>true</useTokenId>
                <merchantName>???</merchantName>
                <scaExemption>???</scaExemption>
            </account>
        </entry>
    </accounts>
    <testMode>true</testMode>
    <defaultDescriptor>DevCode payment</defaultDescriptor>
</com.devcode.paymentiq.integration.intergiro.IntergiroConfig>
```

</details>

### Attributes

| Attribute                        | Description                                                                                                                                  |
|----------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------|
| accountConfig.pspPrivateKey      | Merchant's account private key provided by Intergiro                                                                                         |
| accountConfig.pspPublicKey       | Merchant's account public key provided by Intergiro                                                                                          |
| accountConfig.authType           | Can be either AUTH_CAPTURE for sales (auth + capture) or FINAL_AUTH for auth only. CreditcardAccountVerifications must be of type FINAL_AUTH |
| accountConfig.cardOnFileType     | Should be set to INITIAL_RECURRING for CIT/MIT transaction. Should not be configured at all for one-time-payments.                           |
| accountConfig.scaExemption       | SCA Excemption can be one of: LOW_VALUE_PAYMENT, TRANSACTION_RISK_ANALYSIS or  SECURE_CORPORATE_PAYMENT                                      |
| accountConfig.useTokenId         | Must be true if cardOnFileType is defined, otherwise tx will fail                                                                            |

:::note 
3DS1 and 3DS2 are handled on PaymentIQ side. If 3DS is desired to be used, corresponding configurations should be made. On how to configure 3DS, see more [here](https://docs.paymentiq.io/europe/3ds2/general/generalguidelines). The example of 3DS routing rule can be seen below.
:::

## Example Routing Rule
![](/img/providers/routing/intergiro.png)

## Example 3DS Routing Rule
![](/img/providers/routing/intergiro-3ds.png)

## Test Information

| Card Number      | Type  |
|------------------|-------|
| 4122857790340234 | 3DSv1 |
| 4111111111111111 | N3DS  |
