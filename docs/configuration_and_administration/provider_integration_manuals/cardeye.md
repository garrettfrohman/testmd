--- 
id: "cardeye"
title: "CardEye"
hide_title: "true"
---

![](/img/providers/logos/cardeye.png)

# CardEye

## About

| Provider Name                | CardEye                                                                         |
|------------------------------|---------------------------------------------------------------------------------|
| Link                         | https://cardeye.tech/                                                           |
| Classification               | Debit/Credit Card Processor                                                     |
| Regions                      | `International`                                                                 |
| Currencies                   | Please check directly with the provider regarding what currencies are supported |
| Methods/PaymentTxTypes       | `CreditcardDeposit`                                                             |
| PaymentIQ Configuration File | `CardEyeConfig`                                                                 |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>


```xml
<com.devcode.paymentiq.integration.cardeye.CardEyeConfig>
  <enabled>true</enabled>
  <testMode>true</testMode>
  <useViqProxy>true</useViqProxy>
  <container>window</container>
  <accounts>
    <entry>
      <string>???</string>
      <account> 
        <secretKey>???</secretKey>
        <supportedCurrencies>???</supportedCurrencies>
      </account>
    </entry>
  </accounts>
</com.devcode.paymentiq.integration.cardeye.CardEyeConfig>


```

</details>

### Attributes

| Attribute           | Description                                                                      |
|---------------------|----------------------------------------------------------------------------------|
| supportedCurrencies | CardEye supported currencies                                                     |
| secretKey           | Authorization key provided to the merchant by CardEye needed for authentication. |


## Provider Configuration
1. The above XML template (CardEyeConfig) will need to be added via backoffice Admin -> Configuration.
2. Routing needs to be added for Creditcard Deposit in Routing -> Routing.

## Example Routing Rule
![](/img/providers/routing/cardeye.png)

## Transaction Flow
1. The end user enters the card number, the name on card, the transaction amount and card's CVV.
2. PaymentIQ sends the deposit request to CardEye.
3. CardEye validates the request and responds with an html form to which the end user is redirected:
    - for the 3DS flow, the end user performs the in-browser verification step
    - for the N3DS flow, the end user does not have to perform any verification 
4. After the payment is processed, CardEye sends back a callback notification once the transaction status has changed.

## Test Information

### Creditcard Deposit

| Card number      | Brand | Expiry date     | Scenario                                   |
|------------------|-------|-----------------|--------------------------------------------|
| 4111111111111111 | Visa  | any future date | 3DS Challenge                              |
| 5500000000000004 | MC    | any future date | 3DS Challenge                              |
| 4111111111111111 | Visa  | any future date | N3DS (only if sent with amount 200.01 EUR) |
| 5500000000000004 | MC    | any future date | N3DS (only if sent with amount 200.01 EUR) |
