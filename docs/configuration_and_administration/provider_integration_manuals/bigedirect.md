--- 
id: "bigedirect" 
title: "BigeDirect"
hide_title: "true"
---
 
![](/img/providers/logos/bigedirect.png)

# BigeDirect

## About
The BigeDirect is a Luxembourg payment platform that offers credit card and bank deposits for international merchants.

| Provider Name                | BigeDirect                                                 |
|------------------------------|------------------------------------------------------------|
| Link                         | [https://www.bigedirect.com/](https://www.bigedirect.com/) |
| Classification               | Wallet                                                     |
| Regions                      | `International`                                            |
| Currencies                   | `USD`, `EUR`                                               |
| Methods/PaymentTxTypes       | `WebRedirectDeposit`                                       |
| PaymentIQ Configuration File | `BigeDirectConfig`                                         |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.bigedirect.BigeDirectConfig>
  <enabled>true</enabled>
  <useViqProxy>true</useViqProxy>
  <accounts>
    <entry>
      <string>DEFAULT</string>
      <account>
        <merchantId>??</merchantId>
        <secretKey>??</secretKey>
        <supportedCurrencies>EUR|USD</supportedCurrencies>
        <accessToken>??</accessToken>
      </account>
    </entry>
  </accounts>
  <testMode>true</testMode>
  <container>window</container>
  <defaultDescriptor>DevCode payment</defaultDescriptor>
</com.devcode.paymentiq.integration.bigedirect.BigeDirectConfig>
```

</details>

### Attributes

| Attribute   | Description                                                                                     |
|-------------|-------------------------------------------------------------------------------------------------|
| merchantId  | merchantId - provided by BigeDirect                                                             |
| secretKey   | secretKey - provided by BigeDirect                                                              |
| accessToken | accessToken - provided by PaymentIQ Technical Support and should be shared with BigeDirect team |

## Example Routing Rule

![](/img/providers/routing/bigedirect.png)

## Test Information

Testing could be done using real cards only and real transaction occurs. 