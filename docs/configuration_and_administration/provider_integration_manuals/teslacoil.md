--- 
id: "teslacoil" 
title: "TeslaCoil"
hide_title: "true"
---
 
![](/img/providers/logos/teslacoil.png)

# TeslaCoil

## About
TeslaCoil enables companies to easily accept Bitcoin and Bitcoin Lightning payments, without being cryptocurrency experts. 

TeslaCoil features integrations with exchange partners. This enables the customers to hedge out the incoming bitcoin in real time and receive settlement in their desired fiat currency. 

| Provider Name                | TeslaCoil                                                                                                       |
|------------------------------|-----------------------------------------------------------------------------------------------------------------|
| Link                         | [https://teslacoil.io/](https://teslacoil.io/)                                                                  |
| Classification               | Crypto Currency                                                                                                 |
| Regions                      | `International`                                                                                                 |
| Currencies                   | `EUR`,`USD`,`GBP`,`NOK`                                                                                         |
| Methods/PaymentTxTypes       | `CryptoCurrencyDeposit` <br/> `WebRedirectDeposit` <br/> `CryptoCurrencyWithdrawal` <br/> `TeslaCoilWithdrawal` |
| PaymentIQ Configuration File | `TeslaCoilConfig`                                                                                               |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.teslacoil.TeslaCoilConfig>
  <enabled>true</enabled>
  <accounts>
    <entry>
     <string>default</string>
     <account>
        <apiKey>???</apiKey>
        <supportedCurrencies>EUR|USD|GBP|NOK</supportedCurrencies>
        <cryptoCurrency>BTC</cryptoCurrency>
        <defaultDescriptor>DevCode_Payment</defaultDescriptor>
     </account>
    </entry>
  </accounts>
  <testMode>true</testMode>
  <baseRedirectUrl>https://testnet.teslacoil.io/teslapay?id=</baseRedirectUrl>
  <customerCompany>???</customerCompany>
  <targetConfirmation>???</targetConfirmation>
  <notifications>EMAIL</notifications>
</com.devcode.paymentiq.integration.teslacoil.TeslaCoilConfig>'
```

</details>

### Attributes

| Attribute           | Description                                                                                                                                              |
|---------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------|
| apiKey              | Generated in your TeslaCoil account, (Settings -> Api-Keys -> New Key)                                                                                   |
| supportedCurrencies | Supported currencies (`USD`,`EUR`,`GBP`,`NOK`)                                                                                                           |
| customerCompany     | Merchant company name to be shown on the TeslaCoil redirect page                                                                                         |
| defaultDescriptor   | description to associate with the invoice, this will be displayed on TeslaCoil redirect page                                                             |
| targetConfirmation  | Applies for Withdrawal transactions. A lower value would make your transaction confirm quicker, but it would be more expensive. possible values : 1-1008 |
| notifications       | Notifications that will be sent, can be multiple separated by a \|                                                                                       |

### Notes

- TeslaCoil requires you to create credentials in your TeslaCoil back-office for both staging and production environment.

### Email template

For Lightning withdrawals, If ```<notifications>EMAIL</notifications>``` then an email will be sent to the user on the email address that was provided in the verify user response.

A email template is required for sending out the withdrawal url to the user. Name it teslacoil-withdrawal-email or set another name in the TeslaCoilConfig file and the ```<TeslaCoilEmailTemplate></TeslaCoilEmailTemplate>``` attribute.

<details>
<summary>Click to view example email template for withdrawals (coindirect-withdrawal-email)</summary>
<br/>

```html
<p>
    <b>Thank you for using TeslaCoil.</b>

    <br/>
     <br/>

    Please click on the following url to complete your TeslaCoil Withdrawal:
    
    <br/>
     <br/>
    
    <a href="${ptx.latestTxCmdMap.TeslaCoilLightningWithdrawalTxRes.url}">${ptx.latestTxCmdMap.TeslaCoilLightningWithdrawalTxRes.url}</a>

    <br/>
     <br/>
      <br/>
    
    Thank you!
<p>
```

</details>

## Example Routing Rule

![](/img/providers/routing/teslacoilrouting2.png)

## Test Information

### Deposit

To test deposit select Cryptocurrency or WebRedirect payment option in PaymentIQ Cashier, fill in any amount and once on redirect page, choose either Onchain or Lightning payment.

#### Onchain payment
1. Copy the onchain address and the Bitcoin amount on the redirect page 
2. Open your crypto test wallet app or any web Bitcoin test environment, “https://testnet-faucet.mempool.co/” for example 
3. Paste the address and the amount in the App/ Bitcoin test environment and send the payment.

#### Lightning payment
1. Copy the lightning request on the redirect page.
2. Initiate a new transaction in the Teslacoil Backoffice Trasaction -> New Transaction
3. Paste the Lightning request and follow the instructions to finish the transaction.

### Withdrawal

To test withdrawal select Teslacoil payment option in PaymentIQ Cashier, fill in any amount, choose either you want to make an Onchain or Lightning Withdrawal, fill in a valid Bitcoin address then press withrawal button.

If you selected Lightning as withdrawal method, an email should be sent to the user email, follow the link in the email to finalise the payment. After being redirected to the  Lightning withdrawal page, open your crypto wallet app, Wallet of Satoshi “https://www.walletofsatoshi.com/” for example (recommended by TeslaCoil) scan the Qr code and receive the payment.

Note that Lightning Withdrawal can only be tested in production.
