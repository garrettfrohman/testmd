--- 
id: "xpate" 
title: "Xpate"
hide_title: "true"
---
 
![](/img/providers/logos/xpate.png)

# Xpate

## About
Xpate is a credit card provider that offers 3DS and N3DS deposit (both direct sale, and auth + capture), void, refund, withdrawal and status check.

| Provider Name                | Xpate                                                                                                    |
|------------------------------|----------------------------------------------------------------------------------------------------------|
| Link                         | [https://www.xpate.com/](https://www.xpate.com/)                                                         |
| Classification               | Debit/Credit Card Processor                                                                              |
| Regions                      | `International`                                                                                          |
| Currencies                   | `EUR`, `USD`, `RUB`, `KZT`,`UAH`                                                                         |
| Methods/PaymentTxTypes       | `CreditcardDeposit`<br/> `CreditcardWithdrawal`<br/> `Refund`<br/> `Capture`<br/> `Void`<br/> `Reversal` |
| PaymentIQ Configuration File | `XpateConfig`                                                                                            |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.xpate.XpateConfig>
  <enabled>true</enabled>
  <useViqProxy>true</useViqProxy>
  <accounts>
    <entry>
      <string>DEFAULT</string>
      <account>
        <secretKey>??</secretKey><!--Auth token-->
        <accessToken>??</accessToken><!--S2S token-->
        <productId>Product Name</productId>
        <brandId>??</brandId>
        <supportedCurrencies>EUR|USD|RUB</supportedCurrencies>
        <authType>AUTH_CAPTURE</authType><!--AUTH_CAPTURE|FINAL_AUTH-->
      </account>
    </entry>
    <entry>
      <string>payout</string>
      <account>
        <username>??</username>
        <secretKey>??</secretKey><!--Private key-->
        <supportedCurrencies>EUR|USD</supportedCurrencies>
      </account>
    </entry>
  </accounts>
  <testMode>true</testMode>
  <defaultDescriptor>Bambora payment</defaultDescriptor>
</com.devcode.paymentiq.integration.xpate.XpateConfig>
```

</details>

### Attributes

| Attribute           | Description                                                                                                  |
|---------------------|--------------------------------------------------------------------------------------------------------------|
| account.secretKey   | Corresponds to the *Auth Token* from Xpate to authorize request (to build *Bearer* authorization header)     |
| account.accessToken | Corresponds to the *S2S Token* from Xpate to authorize S2S request  (to build *Bearer* authorization header) |
| account.brandId     | Corresponds to the *Brand ID* from Xpate. It can be found in API section at Xpate backoffice                 |
| account.username    | Corresponds to the *Username* from Xpate.                                                                    |
| account.secretKey   | Corresponds to the *Private key* generated to sign Oauth signature.                                          |


### Callback URL

A callback URL has to be configured by the merchant at the Xpate merchant back-office at https://m.xpate.com/.

Please select Live or Test mode at company name section and then go to API > Webhook (see below).

![](/img/providers/xpate01.png)

| Environment | Callback URL                                               |
|-------------|------------------------------------------------------------|
| Test        | https://test-api.paymentiq.io/paymentiq/api/xpate/callback |
| Live        | https://api.paymentiq.io/paymentiq/api/xpate/callback      |

## Payout keys generation

For payout pair of public and private keys should be generated. 
Public key should be shared with XPate to register it in the system.
Please use following commands to generate the keys

```
openssl genpkey -algorithm RSA -out private_key_pkcs_8.pem -pkeyopt rsa_keygen_bits:4096
openssl rsa -pubout -in private_key_pkcs_8.pem -out public_key.pem
openssl rsa -in private_key_pkcs_8.pem -out private_key_pkcs_1.pem
```

Private key should be added to config as secret key


## Example Routing Rules

![](/img/providers/routing/xpate.png)

## Example Routing Rules for v4 payout

![](/img/providers/routing/xpate_v4.png)

## Test Information

### Credit cards

|      | Card type  | Number              | CVV | Expiry |
|------|------------|---------------------|-----|--------|
| N3DS | Visa       | 4444 3333 2222 1111 | 123 | Any    |
| 3DS  | MasterCard | 5555 5555 5555 4444 | 123 | Any    |

:::note

CVC = 123 to test a successful payment and any other values for these fields to test payment failure.

:::