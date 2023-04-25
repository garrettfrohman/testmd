--- 
id: "tinkbit" 
title: "Tinkbit"
hide_title: "true"
---
 
![](/img/providers/logos/tinkbitlogo.png)

# Tinkbit

## About
Tinkbit provides a platform for its merchants to collect payments from their customers through cryptocurrency. Through this platform you may avoid the frauds and wrong claims(roll back of money), secure transaction etc. You can generate your transaction reports. You may see all your customers through your back-office.

| Provider Name                | Tinkbit                                      |
|------------------------------|----------------------------------------------|
| Link                         | [https://tinkbit.com/](https://tinkbit.com/) |
| Classification               | Crypto Currency                              |
| Regions                      | `International`                              |
| Currencies                   | `EUR` `USD`                                  |
| Methods/PaymentTxTypes       | `CryptoCurrencyDeposit` `WebRedirectDeposit` |
| PaymentIQ Configuration File | `TinkbitConfig`                              |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.tinkbit.TinkbitConfig>
  <enabled>true</enabled>
  <accounts>
    <entry>
     <string>default</string>
     <account>
        <apiKey>???</apiKey>
        <secretKey>???</secretKey>
        <supportedCurrencies>EUR|USD</supportedCurrencies>
     </account>
    </entry>
  </accounts>
  <testMode>true</testMode>
</com.devcode.paymentiq.integration.tinkbit.TinkbitConfig>
```

</details>

### Attributes

| Attribute | Description                        |
|-----------|------------------------------------|
| apiKey    | Provided by Tinkbit as API Key.    |
| secretKey | Provided by Tinkbit as Secret Key. |

## Example Routing Rules

![](/img/providers/routing/tinkbitrouting.png)

## Test Information

To test Tinkbit deposit select Cryptocurrency payment option in PaymentIQ Cashier, 
fill in any amount and follow the instruction after being redirected.

Use the following credit card on Tinkbit redirect page for test:

| Card Brand | Account          | CVV | Expiry date |
|------------|------------------|-----|-------------|
| VISA       | 4111111111111111 | 123 | 12/23       |


