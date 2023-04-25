--- 
id: "yuupay" 
title: "YuuPay"
hide_title: "true"
---
 
![](/img/providers/logos/yuupay.png)

# YuuPay

## About
YuuPay is a creditcard processor with support for Deposits and Refunds.

| Provider Name                | YuuPay                                                                          |
|------------------------------|---------------------------------------------------------------------------------|
| Link                         | [https://www.yuupay.com/](https://www.yuupay.com/)                              |
| Classification               | Debit/Credit Card Processor                                                     |
| Regions                      | `International`                                                                 |
| Currencies                   | Please check directly with the provider regarding what currencies are supported |
| Methods/PaymentTxTypes       | `CreditcardDeposit`<br/> `YuuCollectDeposit`<br/> `Refund`                      |
| PaymentIQ Configuration File | `YuuPayConfig`                                                                  |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.yuupay.YuuPayConfig>
  <enabled>true</enabled>
<useViqProxy>true</useViqProxy>
<notificationUrl>https://api.paymentiq.io/paymentiq/yuupay/callback</notificationUrl>
<accounts>
    <entry>
      <string>N3DS</string>
      <account>
        <secretKey>??</secretKey>
        <use3Dsecure>false</use3Dsecure>
        <serviceEndpoint>https://pay.yuupay.net/secure/txHandler.php</serviceEndpoint>
        <merchantCode>??</merchantCode>
      </account>
    </entry>
  </accounts>
</com.devcode.paymentiq.integration.yuupay.YuuPayConfig>
```
</details>

### Attributes

| Attribute    | Description                  |
|--------------|------------------------------|
| secretKey    |                              |
| use3Dsecure  | Can be either true or false. |
| merchantCode |                              |

## Example Routing Rule

![](/img/providers/routing/yuupay.png)

## Test Information

No test information available. Please contact the provider directly.
