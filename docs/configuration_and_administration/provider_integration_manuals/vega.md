--- 
id: "vega"
title: "Vega (formerly VenusPoint)"
hide_title: "true"
---

![](/img/providers/logos/vega.png)

# Vega

## About
Vega is a Wallet provider.

| Provider Name                | Vega                                                                                     |
|------------------------------|------------------------------------------------------------------------------------------|
| Link                         | [https://vega-wallet.com/index.html?lang=en](https://vega-wallet.com/index.html?lang=en) |
| Classification               | Wallet                                                                                   |
| Regions                      | Please contact the provider directly                                                     |
| Currencies                   | Please check directly with the provider regarding what currencies are supported          |
| Methods/PaymentTxTypes       | `VegaDeposit`<br/> `VegaWithdrawal`                                                      |
| PaymentIQ Configuration File | `VegaConfig`                                                                             |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.vega.VegaConfig>
  <enabled>true</enabled>
  <useViqProxy>false</useViqProxy>
  <accounts>
    <entry>
      <string>default</string>
      <account>
        <username>??</username>
        <password>??</password>
        <supportedCurrencies>EUR</supportedCurrencies>
      </account>
    </entry>
  </accounts>
</com.devcode.paymentiq.integration.vega.VegaConfig>
```
</details>

### Attributes

| Attribute           | Description                         |
|---------------------|-------------------------------------|
| username            | Merchant's Vega Wallet User ID      |
| password            | Merchant's Vega Wallet API Password |
| supportedCurrencies |                                     |

## Example Routing Rule

![](/img/providers/routing/vega.png)

## Test Information

| Username | Password |
|----------|----------|
| U000095  | mv789    |
