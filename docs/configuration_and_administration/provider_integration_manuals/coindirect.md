--- 
id: "coindirect" 
title: "Coindirect"
hide_title: "true"
---
 
![](/img/providers/logos/coindirect.png)

# Coindirect

## About
Coindirect is a way to buy and sell the world's most valuable digital currencies, with a single wallet, all in one place. Whether you're looking to spend or save, convert your coins or build out an investment portfolio, there's a currency waiting for you. 

| Provider Name                | Coindirect                                                                      |
|------------------------------|---------------------------------------------------------------------------------|
| Link                         | [https://coindirect.com/](https://coindirect.com/)                              |
| Classification               | Crypto Currency                                                                 |
| Regions                      | `International`                                                                 |
| Currencies                   | Please check directly with the provider regarding what currencies are supported |
| Methods/PaymentTxTypes       | `CryptoCurrencyDeposit`<br/>`CryptoCurrencyWithdrawal`                          |
| PaymentIQ Configuration File | `CoindirectConfig`                                                              |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.coindirect.deposit.CoindirectConfig>
  <enabled>true</enabled>
  <accounts>
    <entry>
     <string>default</string>
     <account>
       <merchantId>???</merchantId>
        <apiKey>???</apiKey>
        <secretKey>???</secretKey>
        <key1>???</key1>
       <supportedCurrencies>???</supportedCurrencies>
     </account>
    </entry>
  </accounts>
   <notifications>EMAIL</notifications>
  <testMode>false</testMode>
</com.devcode.paymentiq.integration.coindirect.deposit.CoindirectConfig>'
```
</details>

### Attributes

| Attribute                    | Description                                                                                                        |
|------------------------------|--------------------------------------------------------------------------------------------------------------------|
| merchantId                   | Generatated in your Coindirect Backoffice as MerchantID.                                                           |
| apiKey                       | Created in Coindirect Backoffice as ApiKey.                                                                        |
| secretKey                    | Generatated in Coindirect Backoffice at the same time with the Apikey.                                             |
| key1                         | Created in Coindirect Backoffice in the merchant details section as secret.                                        |
| supportedCurrencies          | Supported currencies (`USD`,`EUR`)                                                                                 |
| sleepBeforeStatusCheck       | true / false                                                                                                       |
| sleepBeforeStatusCheckMillis | Amount to wait before doing a status check, in miliseconds                                                         |
| notifications                | Notifications that will be sent, can be multiple separated by a "\|"<br/> Possible values: `EMAIL`, `NOTIFICATION` |

### Email template

If ```<notifications>EMAIL</notifications>``` then an email will be sent to the user on the email address that was provided in the verify user response.

A email template is required for sending out the withdrawal url to the user. Name it coindirect-withdrawal-email or set another name in the CoindirectConfig file and the ```<coindirectEmailTeplate></coindirectEmailTeplate>``` attribute.


<details>
<summary>Click to view example email template for withdrawals (coindirect-withdrawal-email)</summary>
<br/>

```html
<p>
    <b>Thank you for using Coindirect.</b>

    <br/>
     <br/>

    Please click on the following url to complete your Coindirect Withdrawal:
    
    <br/>
     <br/>
    
    <a href="${ptx.latestTxCmdMap.CoindirectWithdrawalTxRes.url}">${ptx.latestTxCmdMap.CoindirectWithdrawalTxRes.url}</a>

    <br/>
     <br/>
      <br/>
    
    Thank you!
<p>
```

</details>


## Example Routing Rule
![](/img/providers/routing/coindirectrouting.png)

### Provider Configuration

You will have to create credentials in your Coindirect back-office for both staging and production environment.
You will need also to add the Webhook URL in the Merchant Details section in your Coindirect back-office:
Test Webhook Url : https://test-api.paymentiq.io/paymentiq/api/coindirect/callback/
live Webhook Url : https://api.paymentiq.io/paymentiq/api/coindirect/callback/

## Test Information

To test deposit/withdrawal select Cryptocurrency payment option in PaymentIQ Cashier, fill in any amount and follow the instruction after being redirected. Use any value as wallet address for withdrawal

One needs a test wallet, and test Bitcoins as well from Coindirect to be able to test.

Make sure test user has email address populated.

