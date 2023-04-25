--- 
id: "payclub" 
title: "PayClub"
hide_title: "true"
---
 
![](/img/providers/logos/payclub.png)

# PayClub

## About
PayClub is a creditcard payment provider that offers 3DS/N3DS deposit, refund and status check.

| Provider Name                | PayClub                                                                                                                                                                                                                                                                                                                                                                                                       |
|------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Link                         | [https://www.payclub.co](https://www.payclub.co)                                                                                                                                                                                                                                                                                                                                                              |
| Classification               | Debit/Credit Card Processor                                                                                                                                                                                                                                                                                                                                                                                   |
| Regions                      | `International`                                                                                                                                                                                                                                                                                                                                                                                               |
| Currencies                   | `CNY `,`JPY `,`INR `,`DKK `,`BAM `,`RON `,`AED `,`UAH `,`AOA `,`BHD `,`USD `,`SGD `,`CZK `,`SEK `,`BGN `,`MXN `,`NGN `,`IDR `,`SAR `,`SAR `,`EGP `,`GBP `,`HKD `,`GEL `,`CHF `,`HRK `,`ILS `,`VND `,`LKR `,`FJD `,`EUR `,`MYR `,`PLN `,`RUB `,`HUF `,`KRW `,`COP `,`ARS `,`ISK `,`AUD `,`PHP `,`NZD `,`BRL `,`LTL `,`TRY `,`QAR `,`SKK `,`OMR `,`BND `,`CAD `,`TWD `,`NOK `,`THB `,`LVL `,`ZAR `,`CLP `,`KWD` |
| Methods/PaymentTxTypes       | `CreditcardDeposit`<br/> `Refund`                                                                                                                                                                                                                                                                                                                                                                             |
| PaymentIQ Configuration File | `PayClubConfig`                                                                                                                                                                                                                                                                                                                                                                                               |

### Supported Amounts

- Minimum 1 USD
- Maximum 1000 USD

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.payclub.PayClubConfig>
  <enabled>true</enabled>
  <useViqProxy>true</useViqProxy>
  <accounts>
    <entry>
      <string>default</string>
      <account>
        <merchantId>???</merchantId>
        <secretKey>???</secretKey>
        <productId>specific product</productId>
        <use3Dsecure>false</use3Dsecure>
        <supportedCurrencies>USD|EUR</supportedCurrencies>
        <sourceAccount>???</sourceAccount>
      </account>
    </entry>
  </accounts>
  <container>iframe</container>
  <width>600</width>
  <height>600</height>
  <liveServiceEndPoint>https://int1.payclub.com/payment.jsp</liveServiceEndPoint>
  <testServiceEndPoint>https://test.payclub.com/payment.jsp</testServiceEndPoint>
  <defaultDescriptor>test product</defaultDescriptor>
  <defaultIssuingBank>Default Bank</defaultIssuingBank>
</com.devcode.paymentiq.integration.payclub.PayClubConfig>
```
</details>

### Attributes

| Attribute      | Description                                                                                                                                                     |
|----------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Merchant ID    | Merchant ID. Provided by PayClub Technical Team to secure payment initialization.                                                                               |
| Account Number | This value is used to authenticate a merchant. Provided by PayClub Technical Team to secure payment initialization.                                             |
| Sign Key       | This key is used to generate SHA256 signature and set it as "p_signmsg" request parameter. Provided by PayClub Technical Team to secure payment initialization. |

## Example Routing Rule

![](/img/providers/routing/payclub.png)

## Test Information

| Card Brand | Account          | CVV | Expiry date | Outcome   | Has redirect |
|------------|------------------|-----|-------------|-----------|--------------|
| MASTERCARD | 5218773862838702 | Any | Any         | CONFIRMED | yes          |
| MASTERCARD | 5172572275622131 | Any | Any         | CONFIRMED | no           |