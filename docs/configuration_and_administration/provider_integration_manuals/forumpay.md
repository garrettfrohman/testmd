--- 
id: "forumpay" 
title: "ForumPay"
hide_title: "true"
---
 
![](/img/providers/logos/forumpay.png)

# ForumPay

## About
ForumPay provides empowers consumers to pay using their preferred crypto currency with their preferred wallet.

| Provider Name          | ForumPay                                               |
|------------------------|--------------------------------------------------------|
| Link                   | [https://www.forumpay.com/](https://www.forumpay.com/) |
| Classification         | Crypto Currency                                        |
| Regions                | `International`                                        |
| Currencies             | `EUR`,`USD`                                            |
| Methods/PaymentTxTypes | `CryptoCurrencyDeposit` <br/> `WebRedirectDeposit`     |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.forumpay.ForumPayConfig>
  <enabled>true</enabled>
  <accounts>
    <entry>
     <string>default</string>
     <account>
        <merchantCode>???</merchantCode> <!-- Key -->
        <apiKey>???</apiKey> <!-- apiKey -->
        <secretKey>???</secretKey>  <!-- apiSecret -->
        <supportedCurrencies>EUR|USD</supportedCurrencies>
        <cryptoCurrency>LTC</cryptoCurrency>
     </account>
    </entry>
  </accounts>
  <testMode>true</testMode>
  <acceptZeroConfirmations>false</acceptZeroConfirmations>
</com.devcode.paymentiq.integration.forumpay.ForumPayConfig>
```
</details>

### Attributes

| Attribute               | Description                                                                                          |
|-------------------------|------------------------------------------------------------------------------------------------------|
| merchantCode            | Internal merchant reference for the point of service. The merchant can decide what to write here     |
| apiKey                  | Generated in your ForumPay account, (MY ACCOUNT -> PROFILE -> Payment Gateway API Key) as API user   |
| secretKey               | Generated in your ForumPay account, (MY ACCOUNT -> PROFILE -> Payment Gateway API Key) as API secret |
| acceptZeroConfirmations | Confirms small payment on zero confirmations. Should be set to false                                 |


## Example Routing Rule
![](/img/providers/routing/forumpay.png)

### Provider Configuration

You need to set the Webhook URL and Redirect URL in the Profile section in your ForumPay account: <br/>
Test Webhook Url : https://test-api.paymentiq.io/paymentiq/api/forumpay/callback/ <br/>
Live Webhook Url : https://api.paymentiq.io/paymentiq/api/forumpay/callback/ <br/>
Test redirect Url : https://test-api.paymentiq.io/paymentiq/api/forumpay/redirect/ <br/>
Live redirect Url : https://api.paymentiq.io/paymentiq/api/forumpay/redirect/

## Test Information
ForumPay doesn't have any sandbox environment, instead you will need to test directly in the production environment. Select Cryptocurrency payment or Webredirect payment option in PaymentIQ Cashier, 
fill in any amount (Limit amount per payment can be set in your ForumPay account under Payment settings) and follow the instruction after being redirected.

You will need to have a real Crypto wallet to test ForumPay. The recommended app from ForumPay is Trust Wallet.
