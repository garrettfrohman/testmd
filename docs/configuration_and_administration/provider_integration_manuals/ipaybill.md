--- 
id: "ipaybill" 
title: "iPaybill"
hide_title: "true"
---
 
![](/img/providers/logos/ipaybill.png)

# iPaybill

## About

| Provider Name                | iPaybill                                                                                                                                                                    |
|------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Link                         | not available                                                                                                                                                               |
| Classification               | Debit/Credit Card Processor                                                                                                                                                 |
| Regions                      | ALL except: China, Ghana, Nigeria, Singapore, South Africa, Turkey, Vietnam, Germany, Canada, Russia                                                                        |
| Currencies                   | `USD`, `HKD`, `GBP`, `JPY`, `EUR`, `AUD`, `CAD`, `SGD`, `NZD`, `TWD`, `KRW`, `DKK`, `TRY`, `MYR`, `THB` <br/> `INR`, `PHP`, `CHF`, `SEK`, `ILS`, `ZAR`, `RUB`, `NOK`, `AED` |
| Methods/PaymentTxTypes       | `CreditcardDeposit`, `Refund`                                                                                                                                               |
| PaymentIQ Configuration File | `iPaybillConfig`                                                                                                                                                            |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.ipaybill.IPaybillConfig>
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
                <siteId>https://example.com</siteId>
            </account>
        </entry>
    </accounts>
    <testMode>false</testMode>
    <defaultDescriptor>DevCode payment</defaultDescriptor>
</com.devcode.paymentiq.integration.ipaybill.IPaybillConfig>
```

</details>

### Attributes

| Attribute                | Description                                                                                                                                                                                                     |
|--------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| accountConfig.merchantId | Corresponds to the *merNo* from iPaybill.                                                                                                                                                                       |
| accountConfig.secretKey  | Key provided by iPaybill used for creating SHA-256 signature.                                                                                                                                                   |
| accountConfig.gatewayNo  | Corresponds to the *gatewayNo* from iPaybill.                                                                                                                                                                   |
| accountConfig.siteId     | It represents the online store where the order comes from, and the format is as follows: example.com, www.example.com, http://example.com, http://www.example.com, https://example.com, https://www.example.com |

## Provider Configuration

1. The above XML template (iPaybill) will need to be added via backoffice Admin -> Configuration.
2.  Routing needs to be added for CreditcardDeposit in Routing -> Routing.
    For 3DS, additional routing needs to be added in Routing -> 3DS2 Routing

## Example Routing Rule

![](/img/providers/routing/ipaybill.png)
![](/img/providers/routing/ipaybill_3ds2.png)

## Transaction Flow

1. The end user enters the transaction amount and relevant credit card information.
2. PaymentIQ sends the deposit request to iPaybill.
3.  - For N3DS, iPaybill responds with final status (failure or success). 
    - For 3DS, iPaybill responds with an initial status acknowledging they have received the PaymentIQ request and a redirectUrl to which the user is redirected for 3DS verification.
4. After the verification is successfully done, the payment processing continues. 
5. After the payment is complete, iPaybill sends back a callback notification once the transaction status has changed.

## Test Information

### N3DS                                                
| Card Number      | CVV | Expiry Date     |
|------------------|-----|-----------------|
| 5275331548947882 | Any | Any future date |
| 5393470277337555 | Any | Any future date |
| 5419256278398385 | Any | Any future date |

### 3DS
| Card Number      | CVV | Expiry Date     |
|------------------|-----|-----------------|
| 5436031030606378 | Any | Any future date |

Testing URL: https://secure.ipaybill.com/TestTPInterface

To use this endpoint `testMode` should be set as `true`. For N3DS, `use3DSecure` should be `false` in xml configuration. For 3DS, it should be `true`. In all other cases REAL cards should be used.