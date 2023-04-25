--- 
id: "epay" 
title: "EPay"
hide_title: "true"
---
 
![](/img/providers/logos/epay.png)

# EPay

## About
EPay is a credit card processor offering Deposits, Refunds and Voids.

| Provider Name                | EPay                                                                                     |
|------------------------------|------------------------------------------------------------------------------------------|
| Link                         | [http://www.epay.eu/](http://www.epay.eu/)                                               |
| Classification               | Debit/Credit Card Processor                                                              |
| Regions                      | `Uganda`                                                                                 |
| Currencies                   | `SEK`, `EUR`                                                                             |
| Methods/PaymentTxTypes       | `CreditcardDeposit`<br/>  `MobilePayDeposit`<br/>  `Refund`<br/>  `Void`<br/>  `Capture` |
| PaymentIQ Configuration File | `EPayConfig`                                                                             |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>

<br/>

```xml
<com.devcode.paymentiq.integration.epay.EPayConfig>
  <enabled>true</enabled>
  <useViqProxy>true</useViqProxy>
  <accounts>
    <entry>
      <string>EPAY_N3DS</string>
      <account>
        <secretKey>??</secretKey>
        <useTokenId>false</useTokenId>
        <use3Dsecure>false</use3Dsecure>
        <supportedCurrencies>EUR|DKK</supportedCurrencies>
        <merchantNumber>??</merchantNumber>
        <apiKey>??</apiKey> <!-- NOTE: This equals the md5 key on ePays's end. NOT what they call apikey-->
        <accessToken>??</accessToken>
      </account>
    </entry>
    <entry>
      <string>EPAY_3DS</string>
      <account>
        <secretKey>??</secretKey>
        <auth>false</auth> <!-- Choose true for two-stage debits -->
        <use3Dsecure>true</use3Dsecure>
        <supportedCurrencies>EUR|DKK</supportedCurrencies>
        <merchantNumber>??</merchantNumber>
        <apiKey>??</apiKey> <!-- NOTE: This equals the md5 key on ePays's end. NOT what they call apikey-->
        <accessToken>??</accessToken>
      </account>
    </entry>
    <entry>
      <string>EPAY_3DS2</string>
      <account>
        <auth>false</auth>
        <use3Dsecure>true</use3Dsecure>
        <supportedCurrencies>EUR|DKK</supportedCurrencies>
        <secretKey>??</secretKey>
        <merchantNumber>??</merchantNumber>
        <apiKey>??</apiKey>
        <accessToken>??</accessToken>
        <acquirerMerchantId>??</acquirerMerchantId> <!-- NOTE: This is not the same as merchantNumber -->
        <mcc>????</mcc> 
        <merchantCountry>???</merchantCountry>
        <merchantUrl>https://???</merchantUrl>
        <merchantName>??</merchantName>
        <!-- For processing Dankort through SBN the below 2 settings are necessary -->
        <merchantThreeDSRequestorId>208727</merchantThreeDSRequestorId>
        <threeDSDirectoryServer>sbn</threeDSDirectoryServer> <!-- Required for the 3DServer to handle authentications as Dankort instead of Visa -->
        <!-- End of Dankort SBNv2 settings -->
      </account>
    </entry>
  </accounts>
  <liveServiceEndPoint>https://transaction-v1.api-eu.bambora.com</liveServiceEndPoint>
  <defaultDescriptor></defaultDescriptor>
  <authUrl>https://authorize-v1.api-eu.bambora.com</authUrl>
  <merchantUrl>https://merchant-v1.api-eu.bambora.com</merchantUrl>
</com.devcode.paymentiq.integration.epay.EPayConfig>
```

</details>

### Attributes

| PaymentIQ Configuration | Description                                                                                  |
|-------------------------|----------------------------------------------------------------------------------------------|
| secretKey               | Secret token (provided by EPay)                                                              |
| merchantNumber          | Id of merchant (provided by EPay)                                                            |
| apiKey                  | MD5 key (provided by EPay)                                                                   |
| accessToken             | Access token (provided by EPay)                                                              |
| createSubscription      | Set to false to send authorizations without the "create subscription" flag. Defaults to true |

### Generate MD5 Key

Instructions how to find the `MD5 key` can be found [here](https://developer.bambora.com/europe/checkout/getting-started/handle-responses#validate-accept-and-callback-url).

## Example Routing Rule
![](/img/providers/routing/epay.png)

## Test Information

### Test Cards

Use the cards in the table below to test different card type in your application. You can use the CVC code to alter the response of the transaction.
When CVC is 000 the transactions gets authorized, and all other CVC will result in a declined transaction.
The expiry date and month can be set to a arbitrary date in the future.

| Card   Brand | Card Type | Issuer Country | Card Number          |
|--------------|-----------|----------------|----------------------|
| DANKORT      | Debit     | DNK            | 5019 4500 0000 05    |
| VISA         | Credit    | DNK            | 4154 2100 0000 0001. |
| VISA,DANKORT | Debit     | DNK            | 4571 7400 0000 0002  |
| MASTERCARD   | Credit    | DNK            | 5156 2300 0000 0004  |
| VISA         | Debit     | SWE            | 4002 6200 0000 0005  |
| MASTERCARD   | Debit     | SWE            | 5125 8600 0000 0006  |
| VISA         | Debit     | NOR            | 4002 7700 0000 0008  |
| MASTERCARD   | Credit    | NOR            | 5206 8300 0000 0001  |
| VISA         | Debit     | DNK            | 4059 3400 0000 0002  |
| VISA,DANKORT | Debit     | DNK            | 4571 8000 0000 0004  |
| VISA,DANKORT | Debit     | DNK            | 4571 8000 0000 0012  |
| VISA,DANKORT | Debit     | DNK            | 4571 8000 0000 0020  |
| VISA,DANKORT | Debit     | DNK            | 4571 8000 0000 0038  |
