--- 
id: "perfectmoney" 
title: "Perfect Money"
hide_title: "true"
---
 
![](/img/providers/logos/perfectmoney.png)

# Perfect Money

## About
Perfect Money is a financial service allowing the users to make instant payments and to make money transfers securely throughout the Internet opening unique opportunities to Internet users and owners of the Internet businesses.
Perfect Money targets to bring the transactions on the Internet to the ideal level!

| Provider Name                | Perfect Money                                                                                  |
|------------------------------|------------------------------------------------------------------------------------------------|
| Link                         | [https://perfectmoney.is/](https://perfectmoney.is/)                                           |
| Classification               | E-wallet/ Voucher                                                                              |
| Regions                      | `Russia` , `Ukraine` , `UAE` , `Turkey` , `Moldova` , `UK` , `Azerbaijan` , `Georgia` , `Iran` |
| Currencies                   | `EUR` , `USD` , `BTC` , `GOLD`                                                                 |
| Methods/PaymentTxTypes       | `WebRedirectDeposit` <br/> `PerfectMoneyVoucherDeposit` <br/> `PerfectMoneyVoucherWithdrawal`  |
| PaymentIQ Configuration File | `PerfectMoneyConfig`                                                                           |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<<com.devcode.paymentiq.integration.perfectmoney.PerfectMoneyConfig>
  <enabled>true</enabled>
  <accounts>
    <entry>
     <string>default</string>
     <account>
        <sourceAccount>???</sourceAccount>
        <merchantName>???</merchantName>
        <secretKey>???</secretKey>  <!-- Passphrase -->
        <supportedCurrencies>EUR|USD</supportedCurrencies>
     </account>
    </entry>
    <entry>
     <string>voucher</string>
     <account>
       <accountID>???</accountID>
        <sourceAccount>???</sourceAccount>
        <secretKey>???</secretKey>  <!-- Passphrase -->
         <supportedCurrencies>EUR|USD</supportedCurrencies>
     </account>
    </entry>
  </accounts>
  <testMode>true</testMode>
</com.devcode.paymentiq.integration.perfectmoney.PerfectMoneyConfig>
```
</details>

### Attributes

| Attribute               | Description                                                                                 |
|-------------------------|---------------------------------------------------------------------------------------------|
| sourceAccount(E-Wallet) | The merchant’s Perfect Money account to which the payment is to be made                     |
| merchantName            | Merchant's name to be displayed as Payee on the Perfect Money payment form                  |
| secretKey (E-Wallet)    | Passphrase to set in perfect Money account before starting receiving payments confirmations |
| supportedCurrencies     | EUR, USD                                                                                    |
| accountID               | Perfect Money account login  (payer)                                                        |
| sourceAccount (Voucher) | Perfect Money account to activate e-Voucher to.                                             |
| secretKey (Voucher)     | Perfect Money account password                                                              |

   
## Example Routing Rule
![](/img/providers/routing/perfectmoneyrouting.png)

## Test Information

Perfect Money doesn't have any sandbox environment all the transactions has to go through their production environment.

One will have to create Perfect Money account to be able to make transactions.

For Perfect Money Voucher Withdrawal, no real transactions will be sent to Perfect Money as they don't have any voucher Withdrawal endpoint.
The merchant will do a manual withdrawal on their Perfect Money account and we will consider a withdrawal transaction as successful once the merchant approve it on PIQ backoffice.
