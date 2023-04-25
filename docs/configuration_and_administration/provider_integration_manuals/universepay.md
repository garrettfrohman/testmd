--- 
id: "universepay" 
title: "UniversePay"
hide_title: "true"
---
 
![](/img/providers/logos/universepay.png)

# UniversePay

## About
UniversePay is a credit card provider that offers deposit (debit, Auth/Capture), refund and void.

| Provider Name                | UniversePay                                                                      |
|------------------------------|----------------------------------------------------------------------------------|
| Product                      | WebPay                                                                           |
| Link                         | [https://client.universepay.eu/mportal/](https://client.universepay.eu/mportal/) |
| Classification               | Debit/Credit Card Processor                                                      |
| Regions                      | `International`                                                                  |
| Currencies                   | `UAH`, `RUB`, `USD`,`GBP`,`EUR`                                                  |
| Methods/PaymentTxTypes       | `CreditcardDeposit`, `Refund`, `Void`, `Capture`                                 |
| PaymentIQ Configuration File | `UniversePayConfig`                                                              |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.universepay.UniversePayConfig>
  <enabled>true</enabled>
  <useViqProxy>true</useViqProxy>
  <width>800</width>
  <height>850</height>
  <accounts>
    <entry>
      <string>default</string>
      <account>
        <merchantKeyId>??</merchantKeyId>
        <useTokenId>true</useTokenId>
        <secretKey>??</secretKey>
        <supportedCurrencies>UAH|RUB|USD|EUR|GBP|CZK</supportedCurrencies>
        <version>1.0</version>
        <authType>FINAL_AUTH</authType>
           <!--
        <authType>AUTH_CAPTURE</authType>
        <authType>FINAL_AUTH</authType>
        <authType>PRE_AUTH</authType>
        -->
      </account>
    </entry>
   </accounts>
  <defaultDescriptor>My order</defaultDescriptor>
  <testServiceEndPoint>https://api.universepay.eu/api/</testServiceEndPoint>
  <redirectUrl>${baseRedirectUrl}/api/universepay/redirect/${ptx.txRefId}</redirectUrl>
  <callbackUrl>${baseRedirectUrl}/api/universepay/callback/${ptx.txRefId}</callbackUrl>
</com.devcode.paymentiq.integration.universepay.UniversePayConfig>
```
</details>

### Attributes

| Attribute     | Description                                                                                                                                                                         |
|---------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| merchantKeyId | Corresponds to the `merchant Id` used in all the requests.                                                                                                                          |
| useTokenId    | Corresponds to the `required_rectoken`.`required_rectoken` is a flag which indicate whether Universepay must return card token to access card funds without cardholder interaction. |
| secretKey     | Corresponds to the `transaction password for purchase, verification` used for encryption.                                                                                           |
| authType      | Used to configure auth/capture settings. If it is set to `PRE_AUTH` or `FINAL_AUTH` the deposit will be auth. And if it is set to `AUTH_CAPTURE` the deposit will be direct debit.  |

## Example Routing Rule
![](/img/providers/routing/universepay.png)

## Test Information

### Test Cards 3DS

| Card Brand | Account          | CVV | Expiry date | Respnonse type |
|------------|------------------|-----|-------------|----------------|
| VISA       | 4444555566661111 | Any | Any         | Approved       |
| VISA       | 4444111166665555 | Any | Any         | Decline        |

### Test Cards N3DS

| Card Brand | Account          | CVV | Expiry date | Response type |
|------------|------------------|-----|-------------|---------------|
| VISA       | 4444555511116666 | Any | Any         | Approved      |
| VISA       | 4444111155556666 | Any | Any         | Decline       |
