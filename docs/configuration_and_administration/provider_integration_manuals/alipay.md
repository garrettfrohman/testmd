--- 
id: "alipay" 
title: "Alipay"
hide_title: "true"
---
 
![](/img/providers/logos/alipay.png)

# Alipay

## About
The "Provider" Merchant Account gives you access to a globally renowned payment option, the ecoAccount, whilst at the time offering you an instant and cost effective means of taking payments from customers worldwide - even in countries that can be difficult to reach. "Provider" is a e-wallet where your customers can both do a deposit and withdrawal.

| Provider Name                | Alipay                                                                          |
|------------------------------|---------------------------------------------------------------------------------|
| Link                         | [https://intl.alipay.com/](https://intl.alipay.com/)                            |
| Classification               | Wallet                                                                          |
| Regions                      | `International`                                                                 |
| Currencies                   | Please check directly with the provider regarding what currencies are supported |
| Methods/PaymentTxTypes       | `AlipayDeposit`<br/> `Refund`                                                   |
| PaymentIQ Configuration File | `AlipayConfig`                                                                  |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.alipay.AlipayConfig>
  <enabled>true</enabled>
  <useViqProxy>false</useViqProxy>
  <accounts>
    <entry>
      <string>default</string>
      <account>
        <siteId>??</siteId>
        <secretKey>??</secretKey>
        <supportedCurrencies>USD|HKD|EUR|GBP|AUD|SGD|NZD|JPY|THB|KRW</supportedCurrencies>
      </account>
    </entry>
    <entry>
      <string>new</string>
      <account>
        <service>??</service>
        <version>??</version>
        <siteId>??</siteId>
        <secretKey>??</secretKey>
        <supportedCurrencies>USD|HKD|EUR|GBP|AUD|SGD|NZD|JPY|THB|KRW</supportedCurrencies>
      </account>
    </entry>
  </accounts>
  <testMode>false</testMode>
  <container>window</container> <!-- container should be window to avoid redirect issue -->
</com.devcode.paymentiq.integration.alipay.AlipayConfig>
```

</details>

### Attributes

| PaymentIQ Configuration | Provider Credential                                                                                                                                                                    |
|-------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| siteId                  | Site ID. Provided by Alipay.                                                                                                                                                           |
| secretKey               | Secret Key. Provided by Alipay.                                                                                                                                                        |
| version                 | If the agreement with Alipay is signed as "new cross_border payment solution" instead of "cross_border payment solution" this variable version must be added to the account in config. |
| service                 | Option to add wap, app or pc as service to choose the platform.                                                                                                                        |

## Transaction Flow
When user star the deposit s/he will presented with the following page:

![](/img/providers/alipay01.png)

Click on the blue button to open payment with email option.
Add email address, password and security check, as shown in the picture

![](/img/providers/alipay02.png)

You need to confirm the payment one more time by entering your password

![](/img/providers/alipay03.png)

Wait to see this page which mean payment is successful

![](/img/providers/alipay04.png)

## Example Routing Rule
![](/img/providers/routing/alipay.png)

## Test Information
Email address: douyufua@alitest.com
Password: 111111
