--- 
id: "ticketsurf" 
title: "TicketSurf"
hide_title: "true"
---
 
![](/img/providers/logos/ticketsurf.png)

# TicketSurf

## About
The TicketSurf Merchant Account gives you access to a Europe payment option. TicketSurf is an aggregator/voucher solution where your customers can both do a deposit and refund.

Ticketsurf also supports Creditcard deposits.

| Provider Name                | TicketSurf                                                                                                        |
|------------------------------|-------------------------------------------------------------------------------------------------------------------|
| Link                         | [http://www.ticket-surf.com](http://www.ticket-surf.com)                                                          |
| Classification               | Debit/Credit Card Processor, PrePaid Card / Voucher                                                               |
| Regions                      | `Europe`                                                                                                          |
| Currencies                   | Please check directly with the provider regarding what currencies are supported                                   |
| Methods/PaymentTxTypes       | `CreditcardDeposit`<br/> `TicketPremiumDeposit`<br/> `WebRedirectDeposit`<br/> `VisaVoucherDeposit`<br/> `Refund` |
| PaymentIQ Configuration File | `TicketSurfConfig`                                                                                                |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.ticketsurf.TicketSurfConfig>
  <enabled>true</enabled>
  <useViqProxy>true</useViqProxy>
  <accounts>
    <entry>
      <string>N3DS</string>
      <account>
        <merchantId>??</merchantId>
        <merchantKeyId>??</merchantKeyId>
        <secretKey>??</secretKey>
        <useTokenId>false</useTokenId>
        <use3Dsecure>false</use3Dsecure>
        <version>ws</version>
        <serviceEndpoint>https://ws.tsipayment.net</serviceEndpoint>
      </account>
    </entry>
    <entry>
      <string>3DS</string>
      <account>
        <merchantId>??</merchantId>
        <merchantKeyId>??</merchantKeyId>
        <secretKey>??</secretKey>
        <useTokenId>false</useTokenId>
        <use3Dsecure>true</use3Dsecure>
        <version>ws</version>
        <serviceEndpoint>https://ws.tsipayment.net</serviceEndpoint>
      </account>
    </entry>
  </accounts>
  <mockResponse>false</mockResponse>
  <version>2.60</version>
  <testMode>N</testMode>
  <returnURL>${baseRedirectUrl}/api/ticketsurf/deposit/redirect</returnURL>
  <s2sURL>${baseCallbackUrl}/api/ticketsurf/deposit/callback</s2sURL>
  <transactionStatusCode>
    <entry>
      <string>00000</string>
      <com.devcode.paymentiq.service.paymenttx.PaymentTxStatusCode>SUCCESS</com.devcode.paymentiq.service.paymenttx.PaymentTxStatusCode>
    </entry>
    <entry>
      <string>3</string>
      <com.devcode.paymentiq.service.paymenttx.PaymentTxStatusCode>ERR_DECLINED_OTHER_REASON</com.devcode.paymentiq.service.paymenttx.PaymentTxStatusCode>
    </entry>
    <entry>
      <string>00001</string>
      <com.devcode.paymentiq.service.paymenttx.PaymentTxStatusCode>WAITING_3D_SECURE</com.devcode.paymentiq.service.paymenttx.PaymentTxStatusCode>
    </entry>
    <entry>
      <string>2</string>
      <com.devcode.paymentiq.service.paymenttx.PaymentTxStatusCode>ERR_SYSTEM_ERROR</com.devcode.paymentiq.service.paymenttx.PaymentTxStatusCode>
    </entry>
    <entry>
      <string>1</string>
      <com.devcode.paymentiq.service.paymenttx.PaymentTxStatusCode>WAITING_3D_SECURE</com.devcode.paymentiq.service.paymenttx.PaymentTxStatusCode>
    </entry>
    <entry>
      <string>0</string>
      <com.devcode.paymentiq.service.paymenttx.PaymentTxStatusCode>SUCCESS</com.devcode.paymentiq.service.paymenttx.PaymentTxStatusCode>
    </entry>
    <entry>
      <string>5</string>
      <com.devcode.paymentiq.service.paymenttx.PaymentTxStatusCode>ERR_INVALID_RESPONSE</com.devcode.paymentiq.service.paymenttx.PaymentTxStatusCode>
    </entry>
    <entry>
      <string>02006</string>
      <com.devcode.paymentiq.service.paymenttx.PaymentTxStatusCode>PROCESSING_PROVIDER</com.devcode.paymentiq.service.paymenttx.PaymentTxStatusCode>
    </entry>
    <entry>
      <string>02022</string>
      <com.devcode.paymentiq.service.paymenttx.PaymentTxStatusCode>PROCESSING_PROVIDER</com.devcode.paymentiq.service.paymenttx.PaymentTxStatusCode>
    </entry>
  </transactionStatusCode>
</com.devcode.paymentiq.integration.ticketsurf.TicketSurfConfig>
```

</details>

### Attributes

| Attribute     | Description            |
|---------------|------------------------|
| merchantId    | Provided by TicketSurf |
| merchantKeyId | Provided by TicketSurf |
| secretKey     | Provided by TicketSurf |

## Transaction Flow

![](/img/providers/ticketsurf01.png)

![](/img/providers/ticketsurf02.png)

![](/img/providers/ticketsurf03.png)

![](/img/providers/ticketsurf04.png)

![](/img/providers/ticketsurf05.png)

## Example Routing Rule
- You need to set up a rule for which provider you want to route the voucher to.

![](/img/providers/routing/ticketsurf.png)

## Test Information

| Card Brand | Account          | CVV | Expiry date | Description |
|------------|------------------|-----|-------------|-------------|
| VISA       | 4012888888881881 | 123 | 10/2025     | APPROVED    |
| VISA       | 4242424242424242 | 123 | 10/2025     | DECLINED    |
| VISA       | 4900000000000086 | 123 | 10/2025     | NOTENROLLED |
| MASTERCARD | 5500000000000004 | 123 | 10/2025     | APPROVED    |
| MASTERCARD | 5200000000000007 | 123 | 10/2025     | DECLINED    |
