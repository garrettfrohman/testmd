--- 
id: "dreamspay" 
title: "DreamsPay"
hide_title: "true"
---
 
![](/img/providers/logos/dreamspay.png)

# DreamsPay

## About
DreamsPay is a credit card provider that offers deposits, refunds.

| Provider Name                | DreamsPay                                                                       |
|------------------------------|---------------------------------------------------------------------------------|
| Link                         | [http://dreamspay.com/](http://dreamspay.com/)                                  |
| Classification               | Debit/Credit Card Processor                                                     |
| Regions                      | `International`                                                                 |
| Currencies                   | Please check directly with the provider regarding what currencies are supported |
| Methods/PaymentTxTypes       | `CreditcardDeposit` <br/> `Refund`                                              |
| PaymentIQ Configuration File | `DreamsPayConfig`                                                               |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>

<br/>

```xml
<com.devcode.paymentiq.integration.dreamspay.DreamsPayConfig>
 <enabled>true</enabled>
 <useViqProxy>true</useViqProxy>
 <accounts>
   <entry>
     <string>default</string>
     <account>
       <merchantId>??</merchantId>
       <password>??</password>
       <language>en</language>
       <supportedCurrencies>EUR|USD|GBP|RUB|UAH</supportedCurrencies>
       <serviceEndpoint>https://api.dreamspay.com/api/</serviceEndpoint>
       <useTokenId>true</useTokenId>
     </account>
   </entry>
 </accounts>
</com.devcode.paymentiq.integration.dreamspay.DreamsPayConfig>
```

</details>

### Attributes

| PaymentIQ Configuration | Provider Credential                                                                                                   |
|-------------------------|-----------------------------------------------------------------------------------------------------------------------|
| merchantId              | API Username                                                                                                          |
| password                | Secret Key                                                                                                            |
| language                | The default is the english. It can be changed to ru (Russian, uk (Ukrainian), en (English), lv (Latvian), fr (French) |

## Example Routing Rule
![](/img/providers/routing/dreamspay.png)

## Test Information

### Test Accounts

- Supported currencies are EUR|USD|GBP|RUB|UAH

### 3DS

| Card Brand | Account          | CVV | Expiry date | Result   |
|------------|------------------|-----|-------------|----------|
| VISA       | 4444555566661111 | Any | Any         | APPROVED |
| VISA       | 4444111166665555 | Any | Any         | DECLINED |

### N3DS

| Card Brand | Account          | CVV | Expiry date | Result/Info |
|------------|------------------|-----|-------------|-------------|
| VISA       | 4444555511116666 | Any | Any         | APPROVED    |
| VISA       | 4444111155556666 | Any | Any         | DECLINED    |
