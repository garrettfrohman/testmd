--- 
id: "decta" 
title: "Decta"
hide_title: "true"
---
 
![](/img/providers/logos/Decta.png)

# Decta

## About
DECTA is a global processing company that provides integrated services for payment processing, online acquiring and card issuing.

| Provider Name                | DECTA                                                         |
|------------------------------|---------------------------------------------------------------|
| Link                         | [https://decta.com/](https://decta.com/)                      |
| Classification               | Debit/Credit Card Processor                                   |
| Regions                      | `International`                                               |
| Currencies                   | `EUR`, `USD`, `JPY`, `RUB`, `CZK`, `NOK`, `PLN`, `SEK`        |
| Methods/PaymentTxTypes       | `CreditcardDeposit`<br/> `Refund` <br/> `Void`<br/> `Capture` |
| PaymentIQ Configuration File | `DectaConfig`                                                 |


## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.decta.DectaConfig>
  <enabled>true</enabled>
  <useViqProxy>true</useViqProxy>
  <accounts>
    <entry>
      <string>default</string>
      <account>
        <secretKey>???</secretKey>
         <email>???</email>
        <supportedCurrencies>RUB|USD|EUR|JPY|CZK|NOK|PLN|SEK</supportedCurrencies>
        <serviceEndpoint>https://gate.decta.com/api/v0.6/orders/</serviceEndpoint>
        <productName>test</productName>
       <mcc>7995</mcc>
      <merchantCountry>SWE</merchantCountry>
     <merchantUrl>http://www.example.com</merchantUrl>
      <merchantName>Test merchant</merchantName>
       <authType>PRE_AUTH</authType>
         <!--
         <authType>AUTH_CAPTURE</authType>
        <authType>PRE_AUTH</authType>
        <authType>FINAL_AUTH</authType>
        -->
      </account>
    </entry>
  </accounts>
  <saveCard>false</saveCard>
  <testMode>false</testMode>
</com.devcode.paymentiq.integration.decta.DectaConfig>
```

</details>

### Attributes

| Attribute | Description                                                                                  |
|-----------|----------------------------------------------------------------------------------------------|
| email     | Corresponds to the email of the Client                                                       |
| secretKey | Corresponds to the Api key from Decta                                                        |
| saveCard  | Corresponds to the variable we send to Decta to specify if they should save card data or not |

## Example Routing Rule
![](/img/providers/routing/DectaRouting.png)

## Provider Configuration

Merchants have to create credentials (Keys sets) in their Decta back-office in the E-commerce & API section for both staging and production environment.
They will also need to add the Webhook URL in the E-commerce & API section :

| environment | Webhook URL                                                 |
|-------------|-------------------------------------------------------------|
| Test        | https://test-api.paymentiq.io/paymentiq/api/decta/callback/ |
| live        | https://api.paymentiq.io/paymentiq/api/decta/callback/      |


![](/img/providers/Decta.png)

## Test Information

It is not possible to test N3DS and 3DS2 in test environment. Live API key and real Debit/Credit cards are needed.
Merchant needs to inform Decta that they will be using PaymentIQ/Devcode in order to be granted with all required permissions.



