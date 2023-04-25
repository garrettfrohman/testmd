---
id: "gumballpay"
title: "GumBallPay"
hide_title: "true"
---

![](/img/providers/logos/gumballpay.png)

# GumBallPay

## About
GumBallPay is a payment gateway providing credit card operations, 3DS and N3DS deposit (sale, authorization + capture), void, refund, withdrawal confirmation and reversal as well as alternative payment methods (APMs).

| Provider Name                | GumBallPay                                                                                                                                                |
|------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------|
| Link                         | [https://gumballpay.com/](https://gumballpay.com/)                                                                                                        |
| Classification               | Debit/Credit Card Processor                                                                                                                               |
| Regions                      | `International`                                                                                                                                           |
| Currencies                   | Please check directly with the provider regarding what currencies are supported                                                                           |
| Methods/PaymentTxTypes       | `CreditcardDeposit`<br/>`WebRedirectDeposit`<br/>`Capture`<br/>`Void`<br/>`Refund`<br/>`CreditcardWithdrawal`<br/>`BankDomesticWithdrawal`<br/>`Reversal` |
| PaymentIQ Configuration File | `GumBallPayConfig`                                                                                                                                        |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.gumballpay.GumBallPayConfig>
<enabled>true</enabled>
<useViqProxy>true</useViqProxy>
<accounts>
    <entry>
     <string>N3DS</string>
     <account>
       <username>???</username>                                     <!-- login-->
       <groupId>???</groupId>                                       <!-- Group Id/Endpoint Id -->
       <secretKey>XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX</secretKey>  <!-- Merchant Control -->
       <use3Dsecure>false</use3Dsecure>
       <useTokenId>true</useTokenId>
       <authType>AUTH_CAPTURE</authType>
       <hasGroupId>true</hasGroupId>
       <supportedCurrencies>USD|EUR</supportedCurrencies>
     </account>
    </entry>
    <entry>
     <string>3DS</string>
     <account>
       <username>???</username>                                     <!-- login-->
       <groupId>???</groupId>                                       <!-- Group Id/Endpoint Id -->
       <secretKey>XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX</secretKey>  <!-- Merchant Control -->
       <use3Dsecure>true</use3Dsecure>
       <useTokenId>true</useTokenId>
       <authType>AUTH_CAPTURE</authType>
       <hasGroupId>true</hasGroupId>
       <supportedCurrencies>USD|EUR</supportedCurrencies>
     </account>
    </entry>
    <entry>
      <string>WEBREDIRECT</string>
      <account>
        <container>window</container>
        <username>???</username>                                     <!-- login-->
        <groupId>???</groupId>                                       <!-- Group Id/Endpoint Id -->
        <secretKey>XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX</secretKey>  <!-- Merchant Control -->
        <supportedCurrencies>EUR</supportedCurrencies>
        <hasGroupId>true</hasGroupId>
      </account>
    </entry>
    <entry>
      <string>PAYOUT</string>
      <account>
        <username>???</username>                                     <!-- login-->
        <groupId>???</groupId>                                       <!-- Group Id/Endpoint Id -->
        <secretKey>XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX</secretKey>  <!-- Merchant Control -->
        <version>v4</version>
        <useTokenId>false</useTokenId>
        <!--RSA Private Key (required for transfer v4 operations)-->
        <pspPrivateKey>-----BEGIN RSA PRIVATE KEY-----
MIIJJwIBAAKCAgEA6zqar2 ... usbt4EK1oA7ukAP69uBE8vTeH3oIsew==
-----END RSA PRIVATE KEY-----</pspPrivateKey>
        <supportedCurrencies>USD|EUR</supportedCurrencies>
        <hasGroupId>true</hasGroupId>
      </account>
    </entry>
  </accounts>
  <testMode>false</testMode>
</com.devcode.paymentiq.integration.gumballpay.GumBallPayConfig>
```

</details>

### Attributes

| Attribute         | Description                                                                                                                                                                                                                      |
|-------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| username          | Corresponds to the User Login from GumBallPay                                                                                                                                                                                    |
| secretKey         | Corresponds to the Merchant Control from GumBallPay. It is used to generate request signature                                                                                                                                    |
| groupID           | Corresponds to the End Point ID or Group ID from GumBallPay. It is an entry point for incoming Merchant’s transactions                                                                                                           |
| useTokenId        | To enable recurring please specify `useTokenId=true`                                                                                                                                                                             |
| use3Dsecure       | To enable 3DS please specify `use3Dsecure=true`                                                                                                                                                                                  |
| hasGroupId        | Should be set to `true` on account level (only set to false if End point ID is used instead of Group ID)                                                                                                                         |
| doDefaultRedirect | Set to true if redirect should not trigger a status check and instead wait for the callback. For `WebRedirectDeposit` methods (JPay) where the amount might change after initial redirect and needs to be set from the callback. |
| pspPrivateKey     | Corresponds to the private RSA key in the `PKCS#1` format that is used to authorize transactions                                                                                                                                 |


1). Merchant should specify all the parameters marked with "??". `secretKey` should be also specified.<br/>
2). Each operation 3DS, N3DS deposit or payout has its own "Endpoint ID / Endpoint GROUPID".<br/>
3). You have to generate RSA public and private keys (see instruction below), then provide public key to GumBallPay and specify private key in `<pspPrivateKey>...</pspPrivateKey>` parameter.

### Generate Public and Private key pair

You will need to use [OpenSSL](https://www.openssl.org/) to generate private and public keys.

1). Generate RSA private key - **private_key_pkcs_8.pem** file in PKCS#8 format:

```
openssl genpkey -algorithm RSA -out private_key_pkcs_8.pem -pkeyopt rsa_keygen_bits:4096
```

2). Generate RSA public key - **public_key.pem** file:

```
openssl rsa -pubout -in private_key_pkcs_8.pem -out public_key.pem
```

3). Convert RSA private key to PKCS#1 format:

```
openssl rsa -in private_key_pkcs_8.pem -out private_key_pkcs_1.pem
```

e.g. you should have something like

```
-----BEGIN RSA PRIVATE KEY-----
MIIJJwIBAAKCAgEA6zqar2j62mSHTWWpiHEUcPFCUTbXgSzFWc7w0+AerEu1n8Vn
. . .
m0jhQ5wP67ow50DR+KNF009lRwRusbt4EK1oD7ukAO69uBE8vTeH2oIeew==
-----END RSA PRIVATE KEY-----
```

Once it is done, please provide your public RSA key to the provider so they can register it in their system. Private RSA key **private_key_pkcs_1.pem** must be configured in the `GumBallPayConfig` using `account.pspPrivateKey` attribute.

### Automatically send whitelist information to GumballPay

GumballPay requires merchants to send customer information when they make their first-time deposit, in order to whitelist the customer.

This can be done automatically in PaymentIQ using rules and email templates.

1. A routing rule can be used to separate out first deposits by using the condition "first deposit = true/false" and route accordingly.
2. Then you need a notification rule that triggers if the transaction is a successful first time deposit using GumballPay. That rule can look something like this:
   ![](/img/providers/gumballpay_whitelist.png)
3. Finally you need to create the email template "GumballPayCustomerWhitelist" that will be sent to GumballPay when the notification rule is triggered. You do this under **Admin > Templates > Email Templates**. The template can look something like this:
 
```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <title></title>
  </head>
  <body>
    <h1 style="padding-left: 0; text-align: left;"><strong>Creditcard to be whitelisted</strong></h1>
    <h2>Transaction Details</h2>
    <table style="border-collapse: collapse; height: 129px;" border="1">
      <tbody>
        <tr style="height: 17px;">
          <td style="width: 200px; height: 17px;"><strong>Payment Account</strong></td>
          <td style="width: 300px; height: 17px;">${ptx.maskedUserAccount}</td>
          <td style="width: 200px;"><strong>User ID</strong></td>
          <td style="width: 300px;">${ptx.merchantUser.userId}</td>
        </tr>
      </tbody>
    </table>
  </body>
</html>
```
In this example html template `${ptx.maskedUserAccount}` will fetch the masked PAN from the transaction and `${ptx.merchantUser.userId}` will fetch the userId of the user.

## Example Routing Rule
![](/img/providers/routing/gumballpay.png)

## Test Information

Please check the below link for current test card data:

[https://doc.gumballpay.com/integration_helpers/test_card_data.html](https://doc.gumballpay.com/integration_helpers/test_card_data.html)
