--- 
id: "wirecapital" 
title: "Wirecapital"
hide_title: "true"
---
 
![](/img/providers/logos/wirecapital.png)

# Wirecapital

## About
Wirecapital is a payment provider offering 3DS/N3DS creditcard deposit, withdrawal, OCT withdrawal and full/partial refund.

| Provider Name                | Wirecapital                                                 |
|------------------------------|-------------------------------------------------------------|
| Link                         | [https://wire.capital/](https://wire.capital/)              |
| Classification               | Debit/Credit Card Processor                                 |
| Regions                      | International                                               |
| Currencies                   | `EUR`, `USD`, `RUB`                                         |
| Methods/PaymentTxTypes       | `CreditcardDeposit`<br/>`CreditcardWithdrawal`<br/>`Refund` |
| PaymentIQ Configuration File | `WirecapitalConfig`                                         |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.wirecapital.WirecapitalConfig>
  <enabled>true</enabled>
  <testMode>true</testMode>
  <useViqProxy>true</useViqProxy>
  <accounts>
    <entry>
      <string>DEFAULT</string>
      <account>
        <secretKey>??</secretKey><!--Private Key-->
        <accessToken>??</accessToken><!--Token-->
        <productName>SKI Pass</productName><!--can be left blank-->
        <!--use useTokenId=true and withdrawalType=OCT to enable OCT payout-->
        <useTokenId>false</useTokenId>
        <withdrawalType>OCT</withdrawalType>
        <supportedCurrencies>EUR|USD|RUB</supportedCurrencies>
      </account>
    </entry>
  </accounts>
  <container>window</container>
</com.devcode.paymentiq.integration.wirecapital.WirecapitalConfig>
```
</details>

### Attributes

| Attribute   | Description                                                                                                         |
|-------------|---------------------------------------------------------------------------------------------------------------------|
| secretKey   | Corresponds to **Private Key** from Wirecapital. It is used to authorize each request that is sent to the provider. |
| accessToken | Corresponds to **Payment Token** from Wirecapital. It uniquely identifies a payment transaction at provider side.   |

Above attributes can be found at Wirecapital back office, at **Profile** section and **Merchant** tab.

## Example Routing Rule
![](/img/providers/routing/wirecapital.png)

## Test Information

You can use the following PAN for tests:

| Card Number      | Description                             |
|------------------|-----------------------------------------|
| 4617611794313933 | CONFIRMED as 3-D Secure transaction     |
| 4626233193837898 | DECLINED as 3-D Secure transaction      |
| 4392963203551251 | CONFIRMED as non 3-D Secure transaction |
| 4730198364688516 | DECLINED as non 3-D Secure transaction  |
| 4271619466080208 | CONFIRMED as payout card                |
| 4811437417740292 | DECLINED as payout card                 |

You can use any cardholder name and CVV2/CVC2 with these PAN.

You can use even amount in refund request to emulate success refund and odd amount for emulate false refund.
