--- 
id: "icarddirect" 
title: "ICardDirect"
hide_title: "true"
---
 
![](/img/providers/logos/icarddirect.png)

# ICardDirect

## About
ICardDirect is a credit card provider that offers deposit, refund and withdrawal.

| Provider Name                | ICardDirect                                             |
|------------------------------|---------------------------------------------------------|
| Link                         | [https://icard.com/](https://icard.com/)                |
| Classification               | Debit/Credit Card Processor                             |
| Regions                      | International                                           |
| Currencies                   | `USD`, `EUR`, `BGN`, `GBP`, `RON`, `CHF`                |
| Methods/PaymentTxTypes       | `ICardDirectDeposit`, `Refund`, `ICardDirectWithdrawal` |
| PaymentIQ Configuration File | `ICardDirectConfig`                                     |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.icarddirect.ICardDirectConfig>
  <enabled>true</enabled>
  <testMode>true</testMode>
   <width>400</width>
  <height>40</height>
  <container>window</container>
  <accounts>
    <entry>
     <string>EUR</string>
     <account>
        <useTokenId>??</useTokenId>
        <gatewayNo>??</gatewayNo>
        <merchantKeyId>1</merchantKeyId>
        <version>3.3</version>
        <language>EN</language>
        <merchantId>??</merchantId>
        <merchantName>??</merchantName>
        <supportedCurrencies>USD|EUR|BGN|GBP|RON|CHF</supportedCurrencies>
        <productCategory>??</productCategory>
        <key1>1</key1>
        <secretKey>??</secretKey>
        <pspPublicKey>??</pspPublicKey>
     </account>
    </entry>
  </accounts>
<paymentProgram>0</paymentProgram> 
</com.devcode.paymentiq.integration.icarddirect.ICardDirectConfig>
```

</details>

### Attributes

| Attribute       | Description                                                                                                                                                                                                                                                                                                                                             |
|-----------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| container       | If set to window, the window flow will be used,where the user will be transfered to IPG page to complete the payment. If it is set to iframe,the widget flow will be used, where an embedded widget is used to complete the payment(mini-application that is used to collect payment data and process transaction).                                     |
| useTokenId      | Boolean value to determine if purchase with card token is going to be used. If set to true, the first time the user does a purchase he/she need to enter his/her card info, then the following times the user makes a purchase he only need to choose a previous saved account and only enter the amount. Note: for gambling it should be set to false. |
| gatewayNo       | MID provided by ICard. It is different for every currency.                                                                                                                                                                                                                                                                                              |
| merchantKeyId   | The keyIndex of the RSA key used to sign the request. The merchant can generate more than a key to be used in the communication,a key index is assigned to every key, starting from 1 to MAXINT.                                                                                                                                                        |
| version         | IPGVersion provided by ICard.                                                                                                                                                                                                                                                                                                                           |
| language        | ISO 2-character code for the desired language on the payment page.                                                                                                                                                                                                                                                                                      |
| merchantId      | Originator provided by ICard. It is a value that uniquely identifies the merchant company.                                                                                                                                                                                                                                                              |
| merchantName    | User friendly name of the merchant web shop. The cardholder will see this name on some notices in the payment page.The merchant can choose a proper name of choice.                                                                                                                                                                                     |
| productCategory | ProductName: product name/service name the merchant provides to the customer.ProductName is going to  be displayed on payment page. The merchant can choose a proper name of choice.                                                                                                                                                                    |
| key1            | BannerIndex :Index specified in ICard Side for every banner provided by the Merchant. The Merchant need to provide one or more banner to ICard. The merchant May choose to select  proper banner for every payment to be displayed on the payment page.                                                                                                 |
| paymentProgram  | Used in withdrawal. Defines the payment program : 0 = GamblingRepay  1 = BusinessToCustomer.                                                                                                                                                                                                                                                            |
| pspPublicKey    | The RSA public Key that the Merchant will recieve from the provider.                                                                                                                                                                                                                                                                                    |
| secretKey       | The RSA Private key that the Merchant need to generate. The merchant can generate more than a key to be used in the communication,a key index  is assigned to every key, starting from 1 to MAXINT.                                                                                                                                                     |

## Example Routing Rules

![](/img/providers/routing/icarddirect.png)

## Test Information

The merchant need to generate RSA keyPair using the website: https://ipg.icard.com/test_keys/generate
and paste the private key into 'secretKey' attribute in ICardDirectSystemConfig, and send the generated public key to ICard technical team . 
ICard technical team in turn need to send their public key to the merchant. The recieved public key should be pasted into 'pspPublicKey' attribute in ICardDirectSystemConfig.
If the merchant choose to generate and use only one RSA key pair for all the communications then the attribute 'merchantKeyId' will take the value one, while if 
the merchant choose to genertate and use different keys for different methods in this case the merchant need to set index for every key and send the public key
with an index for each to ICard technical team, in this case the value of the attribute 'merchantKeyId' should be the index of the key pair used. 
 
### Deposits

After initiating a deposit transaction, the user will be either redirected to the IPG page (if container attribute in config is set to window) or a IPG widget will be displayed in an iframe (if container attribute in config is set to window) then the user needs to enter his/her card information.
you need to use one of the cards below with any valid expiry date and (000) for cvv to test different responses: 
if useTokenId is sett to true in config, then you will be redirected to enter the card data only the first time you do deposit 
the subsequent deposits will be done using token.

| CardNumber        | Response |
|-------------------|----------|
| 5326100000000004  | Approved |
| 4006090000000007  | Approved |
| 4002880000000005  | Approved |
| 4877000000000002  | Decline  |
| 67032000000000001 | Decline  |

### Withdrawal

To test withdrawal, You need to choose a saved account and then fill the amount .
Important: Withdrawals are only possible with existing accounts.






