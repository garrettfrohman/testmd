--- 
id: "sirpaga"
title: "Sirpaga"
hide_title: "true"
---

![](/img/providers/logos/sirpaga.png)

# Sirpaga

## About
Sirpaga is an aggregator provider offering Credit Card and several alternative payment methods using their hosted payment page. Credit Card payments supports Deposit, Withdrawal, Refund and also they have WebRedirectDeposit and WebRedirectWithdrawal methods.
Please check with the provider for more details.

| Provider Name                | Sirpaga                                                                                              |
|------------------------------|------------------------------------------------------------------------------------------------------|
| Link                         | [https://docs.sirpaga.com](https://docs.sirpaga.com)                                                 |
| Classification               | Debit/Credit Card Processor                                                                          |
| Regions                      | `Internatioal`                                                                                       |
| Currencies                   | `CNY` `EUR` `USD` `JPY`                                                                              |
| Methods/PaymentTxTypes       | `CreditcardDeposit`, `CreditcardWithdrawal`, `Refund`, `WebRedirectDeposit`, `WebRedirectWithdrawal` |
| PaymentIQ Configuration File | `SirpagaConfig`                                                                                      |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>


```xml   
<com.devcode.paymentiq.integration.sirpaga.SirpagaConfig>
  <enabled>true</enabled>
  <useViqProxy>true</useViqProxy>
  <testMode>true</testMode>
  <accounts>
    <entry>
     <string>default</string>
     <account>
       <secretKey??</secretKey>
       <productName>digitalProduct</productName>
       <supportedCurrencies>CNY|EUR|USD|JPY</supportedCurrencies>
     </account>
    </entry>
  </accounts>
  <services>
   <entry>
     <string>WEBMONEY</string>
      <string>webmoney</string>
    </entry>
    <entry>
      <string>BANKCARD</string>
      <string>bank_card</string>
    </entry>
        <entry>
      <string>QIWI</string>
      <string>qiwi_wallet</string>
    </entry>
        <entry>
      <string>SKRILL</string>
      <string>skrill_wallet</string>
    </entry>
   </services>
</com.devcode.paymentiq.integration.sirpaga.SirpagaConfig>

```

</details>

### Attributes

| Attribute   | Description                                                                                               |
|-------------|-----------------------------------------------------------------------------------------------------------|
| secretKey   | merchant_private_key provided by Sirpaga to be used in authentication                                     |
| productName | product name (Service description) to be send in deposit request. (example: 'iPhone', between 5-255 char) |
| service     | used to map PaymentIQ service to corresponding Sirpaga payment method                                     |

### Example Routing Rules

![](/img/providers/routing/sirpaga.png)

## Test Information

### Testing Creditcard

Use the following cards with any cvv and expiry date to test creditcard deposits and withdrawals.

| 3DS/N3DS | Card Number      | Result/Info     |
|----------|------------------|-----------------|
| 3DS      | 4617611794313933 | CONFIRMED       |
| 3DS      | 4626233193837898 | DECLINED        |
| N3DS     | 4392963203551251 | CONFIRMED       |
| N3DS     | 4730198364688516 | DECLINED        |
| -        | 4627342642639018 | APPROVED PAYOUT |
| -        | 4968357931420422 | DECLINED PAYOUT |
