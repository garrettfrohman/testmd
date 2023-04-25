--- 
id: "luxonpay" 
title: "Luxon"
hide_title: "true"
---
 
![](/img/providers/logos/luxon300px.png)

# Luxon

## About
Luxon is E-Wallet payment provider offering Deposit, Refund, Withdrawal and Status Check operations.

| Provider Name                | Luxon                                                                                                                 |
|------------------------------|-----------------------------------------------------------------------------------------------------------------------|
| Link                         | [https://luxon.com/](https://luxon.com/)                                                                              |
| Classification               | Wallet                                                                                                                |
| Regions                      | `International*`                                                                                                      |
| Currencies                   | `ARS`, `BRL`, `BYN`, `CAD`, `CHF`, `CLP`, `COP`, `EUR`, `GBP`, `HUF`, `KZT`, `NOK`, `PLN`, `RSD`, `RUB`, `SEK`, `USD` |
| Methods/PaymentTxTypes       | `LuxonPayWalletDeposit` <br/> `LuxonPayWalletWithdrawal` <br/> `Refund`                                               |
| PaymentIQ Configuration File | `LuxonConfig`                                                                                                         |

*Luxon does not operate in the following countries:

`Burundi`, `Central African Rep.`, `Congo, Dem. Rep.`, `Cuba`, `Eritrea`, `Guinea`, `Iran`, `Iraq`, `Israel`, `Lebanon`, `Libya`, `Maldives`, `Mali`, `Myanmar`, `North Korea`,  `Somalia`, `Sudan`, `Syria`, `Turkey`, `United States`, `Venezuela`, `Yemen`, `Zimbabwe`.

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.luxonpay.LuxonPayConfig>
  <enabled>true</enabled>
  <useViqProxy>false</useViqProxy>
  <accounts>
    <entry>
      <string>DEFAULT</string>
      <account>
        <merchantKeyId>??</merchantKeyId>
        <secretKey>??</secretKey>
        <shopName>??</shopName>
        <supportedCurrencies>EUR</supportedCurrencies>
      </account>
    </entry>
  </accounts>
  <testMode>true</testMode>
  <defaultDescriptor>??</defaultDescriptor>
</com.devcode.paymentiq.integration.luxonpay.LuxonPayConfig>
```

</details>

### Attributes

| Attribute              | Description                                                                                                                                                                            |
|------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| merchantKeyId          | Corresponds to the HMAC Key from Luxon. It is used to create a signature and set it to 'X-Signature' request header                                                                    |
| secretKey              | Corresponds to the HMAC Key Value from Luxon. It is used to create a signature and set it to 'X-Signature' request header                                                              |
| accountConfig.shopName | Optional. It will be send over to LuxonPay as a 'brand' parameter which can be used to send identifying information for the merchant to allow grouping transactions in LuxonPay system |

### Callback URL

Callback URLs are set by Luxon.

| Environment | URL                                                           |
|-------------|---------------------------------------------------------------|
| Test        | https://test-api.paymentiq.io/paymentiq/api/luxonpay/callback |
| Production  | https://api.paymentiq.io/paymentiq/api/luxonpay/callback      |

## Example Routing Rules
![](/img/providers/routing/luxonpay.png)

## Test Information

### Wallet Deposit
Please enter amount and press *Pay* button. You will be redirected to LuxonPay login dialog:

![](/img/providers/luxon_capture1.png)

Specify *Login* and *Password* and press *Continue* button in order to proceed with payment. You will be redirected to the confirmation page then:

![](/img/providers/luxon_capture2.png)

Press *Pay* button in order to confirm payment. After payment is completed, you will be redirected to result page:

![](/img/providers/luxon_capture3.png)

### Wallet Withdrawal
Withdrawals are made using a wallet ID, each successful deposit returns a wallet ID for the user that should be stored by the merchant and used to initiate a withdrawal in the API. Users are not able to access their wallet ID in the application and it is never presented to the user so in order to make a withdrawal a user must first have made a deposit and their wallet ID be stored by the merchant.<br/>
Saved accounts can also be user with a cashier integration to allow a user who has previously made a deposit to make a withdrawal.
