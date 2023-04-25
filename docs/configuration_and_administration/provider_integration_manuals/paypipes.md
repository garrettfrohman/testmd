--- 
id: "paypipes" 
title: "PayPipes"
hide_title: "true"
---
 
![](/img/providers/logos/paypipes_logo.png)

# PayPipes

## About
PayPipes is a service that allows you to securely store credit cards and use them to transact against any number of payment
gateways and third party APIs. It does this by simultaneously providing a card tokenization service as well as a gateway and
receiver integration service

| Provider Name                | PayPipes                                                                                                          |
|------------------------------|-------------------------------------------------------------------------------------------------------------------|
| Link                         | [https://www.paypipes.com/](https://www.paypipes.com/)                                                            |
| Classification               | Aggregator                                                                                                        |
| Regions                      | `International`                                                                                                   |
| Currencies                   | Please check directly with the provider regarding what currencies are supported                                   |
| Methods/PaymentTxTypes       | `CreditcardDeposit`<br/>`CreditcardWithdrawal`<br/> `WebRedirectDeposit`<br/> `Refund`<br/> `Void`<br/> `Capture` |
| PaymentIQ Configuration File | `PayPipesConfig`                                                                                                  |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.paypipes.PayPipesConfig>
  <enabled>true</enabled>
  <useViqProxy>true</useViqProxy>
  <testMode>false</testMode>
  <accounts>
    <entry>
      <string>wirecard</string>
      <account>
        <merchantId>??</merchantId> <!-- client_id-->
        <secretKey>??</secretKey> <!-- client_secret-->
        <accountID>??</accountID> <!-- api_id-->
        <use3Dsecure>true</use3Dsecure>
        <service>wirecard</service>
        <supportedCurrencies>EUR|USD</supportedCurrencies>
         <authType>AUTH_CAPTURE</authType>
           <!--
        <authType>AUTH_CAPTURE</authType>
        <authType>FINAL_AUTH</authType>
        <authType>PRE_AUTH</authType>
        -->
      </account>
    </entry>
    <entry>
      <string>webredirect</string>
      <account>
        <merchantId>??</merchantId> <!-- client_id-->
        <secretKey>??</secretKey> <!-- client_secret-->
        <accountID>??</accountID> <!-- api_id-->
        <supportedCurrencies>EUR|USD</supportedCurrencies>
      </account>
    </entry>
  </accounts>
  <services></services>
  <redirectUrl>${baseRedirectUrl}/api/paypipes/redirect/${ptx.txRefId}</redirectUrl>
  <defaultDescriptor>something</defaultDescriptor>
</com.devcode.paymentiq.integration.paypipes.PayPipesConfig>

```

</details>

### Attributes

| PaymentIQ Configuration | Description                                                                           |
|-------------------------|---------------------------------------------------------------------------------------|
| merchantId              | Corresponds to the `client_id` value from PayPipes used in authentication request     |
| secretKey               | Corresponds to the `client_secret` value from PayPipes used in authentication request |
| accessToken             | Corresponds to the `grant_type` value from PayPipes  used in authentication request   |
| accountID               | Corresponds to the `api_id` value from PayPipes used in the requests                  |
| service                 | Which creditcard "gateway" to use, eg. wirecard                                       |


- You have to create an accountconfig for each Creditcard gateway and set the service attribute to that gateway name

### Available service parameters

```cardpay```, ```astropay```, ```merbill```, ```wirecard```, ```paypal```, ```neteller```, ```paysafecard```, ```skrill```.

## Example Routing Rule
![](/img/providers/routing/PayPipes.png)

## Test Information

- Currency: EUR, USD

### CreditCard N3DS

| Card Brand | Account          | CVV | Expiry date |
|------------|------------------|-----|-------------|
| VISA       | 4012000300002001 | 003 | 01/23       |
| MASTERCARD | 5413330300002004 | 004 | 01/23       |

### CreditCard 3DS

| Card Brand | Account          | CVV | Expiry date | 3DS Code                             |
|------------|------------------|-----|-------------|--------------------------------------|
| VISA       | 4000000000000002 | 123 | 01/20       | will be CONFIRMED as 3DS transaction |
| MasterCard | 5555555555554444 | 123 | 01/20       | will be CONFIRMED as 3DS transaction |

### Skrill

| Email Address              | Password         |
|----------------------------|------------------|
| testcustomer987@skrill.com | 05v95bB0z0gcZuTs |

### Paysafecard

| PIN              | Value    | Currency |
|------------------|----------|----------|
| 8080867308687962 | 10000000 | EUR      |
| 6879873353139680 | 100      | USD      |

### Neteller

| Currency | Account ID   | Email Address                 | Secure ID |
|----------|--------------|-------------------------------|-----------|
| EUR      | 453501020503 | netellertest_EUR@neteller.com | 908379    |
| USD      | 454651018446 | netellertest_USD@neteller.com | 270955    |

### PayPal

| Email Address  | Password  |
|----------------|-----------|
| eur@devcode.se | gmsmotwlB |