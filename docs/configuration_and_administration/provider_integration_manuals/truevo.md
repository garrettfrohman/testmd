--- 
id: "truevo" 
title: "Truevo"
hide_title: "true"
---
 
![](/img/providers/logos/truevo.png)

# Truevo

## About
Truevo is a credit card provider that offers 3DS and N3DS deposit (sale, authorization + capture), recurring, void, refund, withdrawal and status check.

| Provider Name                | Truevo                                                                                   |
|------------------------------|------------------------------------------------------------------------------------------|
| Link                         | [https://truevo.com/](https://truevo.com/)                                               |
| Classification               | Debit/Credit Card Processor                                                              |
| Regions                      | `International`                                                                          |
| Currencies                   | `EUR`, `GBP`, `USD` \*                                                                   |
| Methods/PaymentTxTypes       | `CreditcardDeposit`<br/> `CreditcardWithdrawal`<br/> `Refund`<br/> `Capture`<br/> `Void` |
| PaymentIQ Configuration File | `TruevoConfig`                                                                           |

\* Other currencies can be requested

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.truevo.TruevoConfig>
  <enabled>true</enabled>
  <useViqProxy>true</useViqProxy>
  <accounts>
    <entry>
      <string>DEFAULT</string>
      <account>
        <merchantId>??</merchantId><!--entityId-->
        <useTokenId>true</useTokenId>
        <use3Dsecure>false</use3Dsecure>
        <authType>AUTH_CAPTURE</authType>
        <supportedCurrencies>EUR</supportedCurrencies>
        <accessToken>??</accessToken>
      </account>
    </entry>
  </accounts>
  <testMode>true</testMode>
  <container>iframe</container>
  <decryptKey>??</decryptKey>
  <cardMapping>VISA-&gt;VISA,ELECTRON-&gt;ELECTRON,MASTERCARD-&gt;MASTERCARD,MAESTRO-&gt;MAESTRO,DINERS-&gt;DINERS</cardMapping>
</com.devcode.paymentiq.integration.truevo.TruevoConfig>
```

</details>

### Attributes

| Attribute                 | Description                                                                                   |
|---------------------------|-----------------------------------------------------------------------------------------------|
| accountConfig.accessToken | Provided by the Truevo in order to authorize request (to build *Bearer* authorization header) |
| accountConfig.merchantId  | Corresponds to the *entityId* from Truevo.                                                    |
| config.decryptKey         | Provided by the Truevo in order to decrypt callback notification                              |

### Notes

- Please ask Truevo to configure one `decryptKey` for all your accounts mentioned in TruevoConfig XML.

### Callback URL

Callback URL is set by Truevo. Each PaymentIQ merchant ID should have its own Truevo `entityId`, and each Truevo `entityId` should have its own callback URL (each PaymentIQ merchant ID should have its own callback URL):
- TEST: https://test-api.paymentiq.io/paymentiq/api/truevo/callback/{mid}
- PRODUCTION: https://api.paymentiq.io/paymentiq/api/truevo/callback/{mid}

where "mid" -- merchant ID on TEST or PRODUCTION.

## Example Routing Rules

![](/img/providers/routing/truevo.png)

## Test Information

- Testing must be done with currency `EUR`

### Creditcards

|      | Card type  | Number           | CVV          | Expiry |
|------|------------|------------------|--------------|--------|
| N3DS | Visa       | 4200000000000000 | Any 3 digits | Any    |
| 3DS  | Visa       | 4711100000000000 | Any 3 digits | Any    |
| N3DS | MasterCard | 5454545454545454 | Any 3 digits | Any    |
| 3DS  | MasterCard | 5212345678901234 | Any 3 digits | Any    |
