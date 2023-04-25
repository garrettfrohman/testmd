--- 
id: "onlineips" 
title: "OnlineIPS"
hide_title: "true"
---
 
![](/img/providers/logos/onlineips.png)

# OnlineIPS

## About
At Online IPS, our entire focus is on delivering reliable and secure payment solutions. By serving as a single source for payment processing worldwide, IPS sets new standards in convenience, reliability and innovation.

| Provider Name                | OnlineIPS                                                                               |
|------------------------------|-----------------------------------------------------------------------------------------|
| Link                         | [https://onlineips.net/](https://onlineips.net/)                                        |
| Classification               | Debit/Credit Card Processor                                                             |
| Regions                      | `Worldwide`, `Brazil`, `Columbia`, `Peru`                                               |
| Currencies                   | `BRL`, `EUR`, `GBP`, `COP`, `PEN`                                                       |
| Methods/PaymentTxTypes       | `CreditcardDeposit`, `Capture`, `Void`, `Refund`, `BoletoBancarioDeposit`, `PixDeposit` |
| PaymentIQ Configuration File | `OnlineIPSConfig`                                                                       |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.onlineips.OnlineIPSConfig>
  <enabled>true</enabled>
  <useViqProxy>true</useViqProxy>
  <accounts>
    <entry>
      <string>default</string>
      <account>
        <merchantId>???</merchantId>
        <siteId>???</siteId>
        <username>???</username>
        <password>???</password>
        <productId>???</productId>
      </account>
    </entry>
    <entry>
      <string>boleto</string>
      <account>
        <redirectMethod>GET</redirectMethod>
        <container>window</container>
        <merchantId>???</merchantId>
        <siteId>???</siteId>
        <username>???</username>
        <password>???</password>
        <productId>???</productId>
      </account>
    </entry>
    <entry>
      <string>pix</string>
      <account>
        <redirectMethod>GET</redirectMethod>
        <container>window</container>
        <merchantId>???</merchantId>
        <siteId>???</siteId>
        <username>???</username>
        <password>???</password>
        <productId>???</productId>
      </account>
    </entry>
  </accounts>
</com.devcode.paymentiq.integration.onlineips.OnlineIPSConfig>
```

</details>

### Attributes

| Attribute  | Description                                                |
|------------|------------------------------------------------------------|
| merchantId | account config level: `Client ID` provided by OnlineIPS    |
| siteId     | account config level: `Site ID` provided by OnlineIPS      |
| productId  | account config level: `li_prod_id_1` provided by OnlineIPS |
| username   | account config level: `REQ_Username` provided by OnlineIPS |
| password   | account config level: `REQ_Password` provided by OnlineIPS |

### Boleto and PIX
To use Boleto and PIX, merchant's user should have valid Brazilian address, including zip, city, street, district (for PIX), state and country code.<br/>
Using Boleto, merchant's user is redirected to boleto receipt that should be paid in bank.<br/>
Using PIX, merchant's user is redirected to webpage with QR code that should be paid in bank or banking app.<br/>
If merchant uses PaymentIQ Cashier, by default, transaction status will be shown as ```cancelled``` immediately after tab with boleto receipt / PIX QR code will be closed.
To prevent this ```"allowWindowClose": "boleto"``` / ```"allowWindowClose": "pix"``` is recommended to be added to ```MerchantCashierConfig``` as shown below, and query parameter ```fetchConfig=true``` should be used in PaymentIQ Cashier URL 

<details>
<summary>Click to view example of MerchantCashierConfig</summary>
<br/>

```xml
<com.devcode.paymentiq.service.cashier.MerchantCashierConfig>
  <enabled>true</enabled>
  <configs>
    <entry>
      <string>default</string>
      <cashierConfigEntry>
        <config>
          {
            "allowWindowClose": "boleto, pix"
          }
        </config>
      </cashierConfigEntry>
    </entry>
  </configs>
</com.devcode.paymentiq.service.cashier.MerchantCashierConfig>
```
</details>

## Example Routing Rule

![](/img/providers/routing/onlineips_cc.png)

![](/img/providers/routing/onlineips_boleto.png)

![](/img/providers/routing/onlineips_pix.png)



## Test Information

| Type            | Number           | CVV              | Expiry Date     |
|-----------------|------------------|------------------|-----------------|
| VISA 3DS2       | 4035874000424977 | Any three digits | Any future date |
| MASTERCARD 3DS2 | 5426064000424979 | Any three digits | Any future date |
| VISA 3DS1       | 4122857790340234 | Any three digits | Any future date |
| VISA N3DS       | 4111111111111111 | Any three digits | Any future date |