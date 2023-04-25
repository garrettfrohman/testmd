--- 
id: "przelewy24" 
title: "Przelewy24"
hide_title: "true"
---
 
![](/img/providers/logos/przelewy24.png)

# Przelewy24

## About
Przelewy is a banking provider with support for Deposits and Refunds.

| Provider Name                | Przelewy24                                                                      |
|------------------------------|---------------------------------------------------------------------------------|
| Link                         | [https://www.przelewy24.pl/eng/](https://www.przelewy24.pl/eng/)                |
| Classification               | Online Banking                                                                  |
| Regions                      | `Poland`                                                                        |
| Currencies                   | Please check directly with the provider regarding what currencies are supported |
| Methods/PaymentTxTypes       | `Przelewy24Deposit` <br/> `Refund`                                              |
| PaymentIQ Configuration File | `Przelewy24Config`                                                              |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.przelewy24.Przelewy24Config>
  <enabled>true</enabled>
  <useViqProxy>true</useViqProxy>
  <accounts>
    <entry>
      <string>default</string>
      <account>
        <username>??</username>
        <password>??</password>
        <merchantId>??</merchantId>
        <secretKey>??</secretKey>
        <refundSecretKey>??</refundSecretKey>
        <use3Dsecure>false</use3Dsecure>
        <defaultCurrency>EUR</defaultCurrency>
        <supportedCurrencies>PLN|EUR|GBP|CZK</supportedCurrencies>
        <redirectUrl>${baseRedirectUrl}/api/przelewy24/deposit/redirect/${ptx.txRefId}</redirectUrl>
        <pspCodeToStatusCode/>
        <version>3.2</version>
      </account>
    </entry>
  </accounts>
  <container>window</container>
  <width>900</width>
  <height>800</height>
  <defaultDescriptor>PaymentIQ Descriptor</defaultDescriptor>
</com.devcode.paymentiq.integration.przelewy24.Przelewy24Config>
```

</details>

### Attributes

| Attribute       | Description            |
|-----------------|------------------------|
| username        | Provided by Przelewy24 |
| password        | Provided by Przelewy24 |
| merchantId      | Provided by Przelewy24 |
| secretKey       | Provided by Przelewy24 |
| refundSecretKey | Provided by Przelewy24 |

## Example Routing Rule
![](/img/providers/routing/przelewy24.png)

## Test Information

- Choose the Przelewy24 payment method
- Follow the steps on the sandbox site.
