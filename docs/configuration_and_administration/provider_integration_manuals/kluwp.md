--- 
id: "kluwp" 
title: "Kluwp"
hide_title: "true"
---
 
![](/img/providers/logos/kluwp.png)

# Kluwp

## About
Kluwp hosted payment page provides a secure yet simple means of authorizing transactions instant bank transfer, eWallets and prepaid card schemes from your online portal.

Kluwp provides a straightforward payment interface for the customer, and handles the complete process for the online transaction.

### Kluwp Gateway

Kluwp gateway provides a different kind of payment methods that are integrated under one payment page. Some of these payment methods are forceable through a configurable parameter in PaymentIQs system in order facilitate the payment process.
If you provide one of at the below variable, your customer by pass the payment method select screen

* VISA (by Voucher)
* GIFTCARD
* CUP
* INSTANTBANKTRANSFER

| Provider Name                | Kluwp                                                                                                                                                                                                     |
|------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Link                         | [https://www.kluwp.com/](https://www.kluwp.com/)                                                                                                                                                          |
| Classification               | PrePaid Card / Voucher                                                                                                                                                                                    |
| Regions                      | `International*`                                                                                                                                                                                          |
| Currencies                   | Please check directly with the provider regarding what currencies are supported                                                                                                                           |
| Methods/PaymentTxTypes       | `KluwpDeposit`<br/> `ChinaUnionPayDeposit`<br/> `VisaVoucherDeposit`<br/> `WebRedirectDeposit`<br/> `BankDeposit`<br/> `GiftcardDeposit`<br/> `BankIBANWithdrawal`<br/> `CreditcardDeposit`<br/> `Refund` |
| PaymentIQ Configuration File | `KluwpConfig`                                                                                                                                                                                             |

### Countries supported for Instantbanktransfer
Australia, Austria, Latvia, Belgium, Lithuania, Canada, Czech Republic, Denmark, Estonia, Poland, Finland, Portugal, France, Germany, Slovakia, Spain, Hungary, Sweden, Ireland, United Kingdom and Italy.

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.kluwp.KluwpConfig>
<enabled>true</enabled>
<useViqProxy>true</useViqProxy>
<container>window</container> <!-- window is needed when using the cashier due to restrictions on the provider's end. Using iframe will cause the cashier not to be able to redirect to receipt page -->
<accounts>
    <entry>
     <string>default</string>
     <account>
       <merchantId>??</merchantId>
       <merchantName>??</merchantName>
       <apiKey>??7</apiKey>
       <secretKey>??</secretKey>
       <useTokenId>false</useTokenId> <!-- true = enables the use of stored card token -->
       <!-- <supportedCurrencies>EUR</supportedCurrencies> -->
     </account>
    </entry>
    <entry>
     <string>INSTANTBANKTRANSFER</string>
     <account>
       <merchantId>??</merchantId>
       <merchantName>??</merchantName>
       <apiKey>??</apiKey>
       <secretKey>??</secretKey>
       <forcePayment>INSTANTBANKTRANSFER</forcePayment>
       <!-- <supportedCurrencies>EUR</supportedCurrencies> -->
     </account>
    </entry>
  </accounts>
  <defaultDescriptor>??</defaultDescriptor>
</com.devcode.paymentiq.integration.kluwp.KluwpConfig>
```
</details>

### Attributes

| Attribute    | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
|--------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| merchantId   | MerchantID. Provided by Kluwp.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| merchantName | Merchant Name. Provided by Kluwp.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| apiKey       | API Key. Provided by Kluwp.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| secretKey    | Secret Key. Provided by Kluwp.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| useTokenId   | Flag the transaction to use Kluwp's store card functionality, which means PIQ will save a token for future re-occurring transactions                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| forcePayment | Kluwp payment services can be accessed using a configuration tag inside an account root called ```<forcePayment>INSTANTBANKTRANSFER</forcePayment>```, for example using the PIQ bank deposit API you will need to use this tag in order to route to a specific bank solution.<br/>The force payment tag will directly connect filtering incoming transaction with a wished payment method making very flexible from PIQ to set condition for every transaction (In this way if you are already integrated to PIQ no further integration will be needed for most payment methods). |

### Notification/Callback
Callback/Notification need to be set by Kluwp technical support.
For PIQ Hosted test example will be:

https://test-api.paymentiq.io/paymentiq/api/kluwp/callback/

## Example Routing Rule
![](/img/providers/routing/kluwp.png)
![](/img/providers/routing/kluwp2.png)
![](/img/providers/routing/kluwp3.png)

## Test Information

### Visavoucher
- Mock user: KLUWP_EUR

| Card Brand | Account          | CVV | Expiry date | Result/Info  |
|------------|------------------|-----|-------------|--------------|
| VISA       | 4012888888881881 | 123 | 10/2025     | APPROVED     |
| VISA       | 4242424242424242 | 123 | 10/2025     | DECLINED     |
| VISA       | 4900000000000086 | 123 | 10/2025     | NOT ENROLLED |

### GiftCard

| Card Brand | Account          | CVV | Expiry date | Result/Info |
|------------|------------------|-----|-------------|-------------|
| MASTERCARD | 5500000000000004 | 123 | 10/2025     | APPROVED    |
| MASTERCARD | 5200000000000007 | 123 | 10/2025     | DECLINED    |

### Instantbanktransfer
- Mock user: KLUWP_EUR					

Choose swedbank Login with:

Username: devcode

Password : Welcome_12 					

### CHINA UNION PAY
- Mock user: KLUWP_CNY

### Creditcard
- Mock user: KLUWP_EUR

| Card Brand | Account          | CVV | Expiry date | Result/Info  |
|------------|------------------|-----|-------------|--------------|
| VISA       | 4012888888881881 | 123 | 10/2025     | APPROVED     |
| VISA       | 4242424242424242 | 123 | 10/2025     | DECLINED     |
| VISA       | 4900000000000086 | 123 | 10/2025     | NOT ENROLLED |
