---
id: "payneteasy"
title: "Payneteasy"
hide_title: "true"
---

![](/img/providers/logos/payneteasy.png)

# Payneteasy

## About
Payneteasy is a payment gateway providing credit card operations, 3DS and N3DS deposit (sale, authorization + capture), void, refund, withdrawal confirmation and reversal as well as alternative payment methods (APMs).

| Provider Name                | Payneteasy                                                                                                                                                |
|------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------|
| Link                         | [https://payneteasy.com/](https://payneteasy.com/)                                                                                                        |
| Classification               | Debit/Credit Card Processor                                                                                                                               |
| Regions                      | `International`                                                                                                                                           |
| Currencies                   | Please check directly with the provider regarding what currencies are supported                                                                           |
| Methods/PaymentTxTypes       | `CreditcardDeposit`<br/>`WebRedirectDeposit`<br/>`Capture`<br/>`Void`<br/>`Refund`<br/>`CreditcardWithdrawal`<br/>`BankDomesticWithdrawal`<br/>`Reversal` |
| PaymentIQ Configuration File | `PayneteasyConfig`                                                                                                                                        |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.payneteasy.PayneteasyConfig>
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
</com.devcode.paymentiq.integration.payneteasy.PayneteasyConfig>
```

</details>

### Attributes

| Attribute         | Description                                                                                                                                                                                                                      |
|-------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| username          | Corresponds to the User Login from Payneteasy                                                                                                                                                                                    |
| secretKey         | Corresponds to the Merchant Control from Payneteasy. It is used to generate request signature                                                                                                                                    |
| groupID           | Corresponds to the End Point ID or Group ID from Payneteasy. It is an entry point for incoming Merchant’s transactions                                                                                                           |
| useTokenId        | To enable recurring please specify `useTokenId=true`                                                                                                                                                                             |
| use3Dsecure       | To enable 3DS please specify `use3Dsecure=true`                                                                                                                                                                                  |
| hasGroupId        | Should be set to `true` on account level (only set to false if End point ID is used instead of Group ID)                                                                                                                         |
| doDefaultRedirect | Set to true if redirect should not trigger a status check and instead wait for the callback. For `WebRedirectDeposit` methods (JPay) where the amount might change after initial redirect and needs to be set from the callback. |
| pspPrivateKey     | Corresponds to the private RSA key in the `PKCS#1` format that is used to authorize transactions                                                                                                                                 |

- Each operation 3DS, N3DS deposit or payout has its own "Endpoint ID / Endpoint GROUPID".<br/>
- You have to generate RSA public and private keys (see instruction below), then provide public key to Payneteasy and specify private key in `<pspPrivateKey>...</pspPrivateKey>` parameter.

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

Once it is done, please provide your public RSA key to the provider so they can register it in their system. Private RSA key **private_key_pkcs_1.pem** must be configured in the `PayneteasyConfig` using `account.pspPrivateKey` attribute.

## Example Routing Rule
![](/img/providers/routing/payneteasy.png)

## Test Information

Please check the below link for current test card data:

[https://doc.payneteasy.com/integration_helpers/test_card_data.html/](https://doc.solidpayments.com/integration_helpers/test_card_data.html)
