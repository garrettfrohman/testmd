--- 
id: "bitnetlab" 
title: "Bitnetlab"
hide_title: "true"
---
 
![](/img/providers/logos/bitnetlab.svg)

# Bitnetlab

## About
Bitnetlab is an payment provider that offers a solution for merchants to be paid in crypto currencies via credit cards.

| Provider Name                | Bitnetlab                                                                       |
|------------------------------|---------------------------------------------------------------------------------|
| Link                         | [https://bitnetlab.exchange/](https://bitnetlab.exchange/)                      |
| Classification               | Crypto currency / Creditcard                                                    |
| Regions                      | `International`                                                                 |
| Currencies                   | Please check directly with the provider regarding what currencies are supported |
| Methods/PaymentTxTypes       | `CryptoCurrencyDeposit`                                                         |
| PaymentIQ Configuration File | `BitnetlabConfig`                                                               |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.bitnetlab.BitnetlabConfig>
  <enabled>true</enabled>
  <accounts>
    <entry>
      <string>default</string>
      <account>
        <apiKey>??????</apiKey>
        <cryptoCurrency>XXX</cryptoCurrency>
        <supportedCurrencies>XXX|YYY</supportedCurrencies>
      </account>
    </entry>
  </accounts>
</com.devcode.paymentiq.integration.bitnetlab.BitnetlabConfig>
```
</details>

### Attributes

| Attribute      | Description                                                                                                                |
|----------------|----------------------------------------------------------------------------------------------------------------------------|
| apiKey         | API key provided by Bitnetlab                                                                                              |
| cryptoCurrency | Optional. Select which crypto currency to use. If not set Bitnetlab will use the default currency configured on their side |

## Example Routing Rules
![](/img/providers/routing/bitnetlab.png)

## Test Information
The whole flow can not be tested. There are no test cards to use on the credit card input page that the user is redirected to. To test the whole flow please contact Bitnetlab.

