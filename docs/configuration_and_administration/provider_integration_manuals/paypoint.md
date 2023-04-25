--- 
id: "paypoint" 
title: "PayPoint"
hide_title: "true"
---
 
![](/img/providers/logos/paypoint.png)

# PayPoint

## About
Paypoint is a creditcard processor with support for Deposits, Withdrawals and Refunds.

| Provider Name                | PayPoint                                                                        |
|------------------------------|---------------------------------------------------------------------------------|
| Link                         | [https://paypoint.com/en-gb](https://paypoint.com/en-gb)                        |
| Classification               | Debit/Credit Card Processor                                                     |
| Regions                      | `International`                                                                 |
| Currencies                   | Please check directly with the provider regarding what currencies are supported |
| Methods/PaymentTxTypes       | `CreditcardDeposit`<br/> `CreditcardWithdrawal`<br/> `Refund`                   |
| PaymentIQ Configuration File | `PayPointImaConfig`                                                             |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.paypoint.PayPointImaConfig>
  <enabled>true</enabled>
  <useViqProxy>true</useViqProxy>
  <fraudGuardEnabled>false</fraudGuardEnabled>
  <fraudGuardInstallationID></fraudGuardInstallationID>
  <APIversionForDisabling3Dsecure>1.3</APIversionForDisabling3Dsecure>
  <APIversion>1.4</APIversion>
  <liveMode>true</liveMode>
  <historyCheck>true</historyCheck>
  
  
  <paymentRequestUrl>https://secure.metacharge.com/mcpe/corporate</paymentRequestUrl>
  <accounts>
    <entry>
      <string>3DS</string>
      <account>
        <installationID>???</installationID>
        <use3Dsecure>true</use3Dsecure>
        <useTokenId>false</useTokenId>
      </account>
    </entry>
    <entry>
      <string>N3DS</string>
      <account>
        <installationID>???</installationID>
        <use3Dsecure>false</use3Dsecure>
        <useTokenId>false</useTokenId>
      </account>
    </entry>
    <entry>
      <string>REPEAT</string>
      <account>
        <installationID>???</installationID>
        <use3Dsecure>false</use3Dsecure>
        <useTokenId>true</useTokenId>
      </account>
    </entry>
    <entry>
      <string>WD_REFUND</string>
      <account>
        <installationID>???</installationID>
        <use3Dsecure>false</use3Dsecure>
        <useTokenId>true</useTokenId>
      </account>
    </entry>
    <entry>
      <string>PAYOUT</string>
      <account>
        <installationID>???</installationID>
        <use3Dsecure>false</use3Dsecure>
        <useTokenId>false</useTokenId>
      </account>
    </entry>
  </accounts>
  <authorisationMode>2</authorisationMode>
  <depositDescriptionKey>paypoint.deposit.statement.desc</depositDescriptionKey>
  <defaultDepositDescription>Deposit to player account</defaultDepositDescription>
  <refundDescriptionKey>paypoint.refund.statement.desc</refundDescriptionKey>
  <defaultRefundDescription>Refund from player account</defaultRefundDescription>
  <messageToStatusCode>
    <entry>
      <string>.*intReference.*</string>
      <com.devcode.paymentiq.service.paymenttx.PaymentTxStatusCode>ERR_DECLINED_DUPLICATE_TX_ID</com.devcode.paymentiq.service.paymenttx.PaymentTxStatusCode>
    </entry>
    <entry>
      <string>.*S3D Verification Failed.*</string>
      <com.devcode.paymentiq.service.paymenttx.PaymentTxStatusCode>ERR_DECLINED_3D_VALIDATION_FAILED</com.devcode.paymentiq.service.paymenttx.PaymentTxStatusCode>
    </entry>
    <entry>
      <string>.*The card number given is invalid.*</string>
      <com.devcode.paymentiq.service.paymenttx.PaymentTxStatusCode>ERR_DECLINED_INVALID_ACCOUNT_NUMBER</com.devcode.paymentiq.service.paymenttx.PaymentTxStatusCode>
    </entry>
  </messageToStatusCode>
  <fraudAdviseToStatusCode>
    <entry>
      <string>2</string>
      <com.devcode.paymentiq.service.paymenttx.PaymentTxStatusCode>ERR_DECLINED_FRAUD</com.devcode.paymentiq.service.paymenttx.PaymentTxStatusCode>
    </entry>
    <entry>
      <string>1</string>
      <com.devcode.paymentiq.service.paymenttx.PaymentTxStatusCode>SUCCESS</com.devcode.paymentiq.service.paymenttx.PaymentTxStatusCode>
    </entry>
    <entry>
      <string>0</string>
      <com.devcode.paymentiq.service.paymenttx.PaymentTxStatusCode>ERR_DECLINED_FRAUD</com.devcode.paymentiq.service.paymenttx.PaymentTxStatusCode>
    </entry>
  </fraudAdviseToStatusCode>
  <cardTypes>
    <entry>
      <string>435225</string>
      <string>DELTA</string>
    </entry>
    <entry>
      <string>56</string>
      <string>MAESTRO</string>
    </entry>
    <entry>
      <string>419741</string>
      <string>DELTA</string>
    </entry>
    <entry>
      <string>400115</string>
      <string>DELTA</string>
    </entry>
    <entry>
      <string>419740</string>
      <string>DELTA</string>
    </entry>
    <entry>
      <string>420796</string>
      <string>DELTA</string>
    </entry>
    <entry>
      <string>440626</string>
      <string>DELTA</string>
    </entry>
    <entry>
      <string>479731</string>
      <string>DELTA</string>
    </entry>
    <entry>
      <string>4581</string>
      <string>DELTA</string>
    </entry>
    <entry>
      <string>410654</string>
      <string>DELTA</string>
    </entry>
    <entry>
      <string>1234123412341234</string>
      <string>VISA</string>
    </entry>
    <entry>
      <string>431930</string>
      <string>UKE</string>
    </entry>
    <entry>
      <string>419774</string>
      <string>DELTA</string>
    </entry>
    <entry>
      <string>419775</string>
      <string>DELTA</string>
    </entry>
    <entry>
      <string>416896</string>
      <string>DELTA</string>
    </entry>
    <entry>
      <string>419776</string>
      <string>DELTA</string>
    </entry>
    <entry>
      <string>4238</string>
      <string>UKE</string>
    </entry>
    <entry>
      <string>4013</string>
      <string>UKE</string>
    </entry>
    <entry>
      <string>418122</string>
      <string>DELTA</string>
    </entry>
    <entry>
      <string>405670</string>
      <string>DELTA</string>
    </entry>
    <entry>
      <string>431262</string>
      <string>DELTA</string>
    </entry>
    <entry>
      <string>419773</string>
      <string>DELTA</string>
    </entry>
    <entry>
      <string>440753</string>
      <string>DELTA</string>
    </entry>
    <entry>
      <string>4508</string>
      <string>DELTA</string>
    </entry>
    <entry>
      <string>4913</string>
      <string>DELTA</string>
    </entry>
    <entry>
      <string>484432</string>
      <string>DELTA</string>
    </entry>
    <entry>
      <string>5</string>
      <string>MC</string>
    </entry>
    <entry>
      <string>4060</string>
      <string>UKE</string>
    </entry>
    <entry>
      <string>402360</string>
      <string>DELTA</string>
    </entry>
    <entry>
      <string>4</string>
      <string>VISA</string>
    </entry>
    <entry>
      <string>4026</string>
      <string>DELTA</string>
    </entry>
    <entry>
      <string>453904</string>
      <string>DELTA</string>
    </entry>
    <entry>
      <string>412922</string>
      <string>DELTA</string>
    </entry>
    <entry>
      <string>412923</string>
      <string>DELTA</string>
    </entry>
    <entry>
      <string>412921</string>
      <string>DELTA</string>
    </entry>
    <entry>
      <string>4917</string>
      <string>DELTA</string>
    </entry>
    <entry>
      <string>414099</string>
      <string>DELTA</string>
    </entry>
  </cardTypes>
</com.devcode.paymentiq.integration.paypoint.PayPointImaConfig>
```

</details>

### Attributes

| Attribute      | Description          |
|----------------|----------------------|
| installationID | Provided by PayPoint |


## Example Routing Rule

![](/img/providers/routing/paypoint.png)

## Test Information

| Card Brand | Account          | CVV | Expiry date |
|------------|------------------|-----|-------------|
| VISA       | 4444333322221111 | Any | Any         |
| MASTERCARD | 5105105105105100 | Any | Any         |