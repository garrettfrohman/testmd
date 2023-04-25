--- 
id: "empcorp" 
title: "EMP Corp"
hide_title: "true"
---
 
![](/img/providers/logos/emp.png)

# EMP Corp

## About
EMP is a creditcard processor supporting Deposits and Refunds.

This integration also supports the Kwickgo, PassNGo and CryptoGo solutions.

| Provider Name                | EMP Corp                                              |
|------------------------------|-------------------------------------------------------|
| Link                         | [http://www.emp-group.com](http://www.emp-group.com)  |
| Classification               | Debit/Credit Card Processor                           |
| Regions                      | `International`                                       |
| Currencies                   | `SEK`, `EUR`                                          |
| Methods/PaymentTxTypes       | `CreditcardDeposit`<br/> `Refund`<br/> `IdealDeposit` |
| PaymentIQ Configuration File | `EMPConfig`                                           |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.emp.EmpConfig>
  <enabled>true</enabled>
  <useViqProxy>true</useViqProxy>
  <container>iframe</container>
  <invalidCharsRegex>Phone->.*,Uid|Address|ZipCode|City->[^a-zA-Z- 0-9],Firstname|Lastname|name|firstname|CardOwner->[^a-zA-Z[-] ]</invalidCharsRegex>
  <accounts>
    <entry>
      <string>N3DS</string>
      <account>
        <secretKey>??</secretKey>
        <use3Dsecure>false</use3Dsecure>
        <serviceEndpoint>https://epro.empcorp.com/api/payment/direct</serviceEndpoint> <!-- change endpoint to https://epro.empcorp.com/api if merchant is assigned by EMP to their platform B API, otherwise error like Invalid API key-->
        <supportedCurrencies>EUR|NOK|USD|PLN</supportedCurrencies>
      </account>
    </entry>
    <entry>
      <string>3DS</string>
      <account>
        <secretKey>??</secretKey> 
        <use3Dsecure>true</use3Dsecure>
        <serviceEndpoint>https://www.empcorp-lux.com/api</serviceEndpoint> <!-- change endpoint to https://epro.empcorp.com/api if merchant is assigned by EMP to their platform B API, otherwise error like Invalid API key-->
        <supportedCurrencies>EUR|NOK|USD|PLN</supportedCurrencies>
        
      </account>
    </entry>
    <entry>
      <string>KWICKGO</string>
      <account>
        <secretKey>??</secretKey>
        <use3Dsecure>false</use3Dsecure> <!-- should be false, 3DS not activated for KWICKGO -->
        <serviceEndpoint>https://www.empcorp-lux.com/api</serviceEndpoint> <!-- change endpoint to https://epro.empcorp.com/api if merchant is assigned by EMP to their platform B API, otherwise error like Invalid API key-->
        <supportedCurrencies>EUR|NOK|USD|PLN</supportedCurrencies>
        
      </account>
    </entry>
    
    <entry>
      <string>PASSNGO</string>
      <account>
        <secretKey>??</secretKey>
        <use3Dsecure>true</use3Dsecure>
        <serviceEndpoint>https://www.empcorp-lux.com/api</serviceEndpoint> <!-- change endpoint to https://epro.empcorp.com/api if merchant is assigned by EMP to their platform B API, otherwise error like Invalid API key-->
        <supportedCurrencies>EUR|NOK|USD|PLN</supportedCurrencies>
        
      </account>
    </entry>
    <entry>
      <string>iDEAL</string>
      <account>
        <secretKey>??</secretKey>
        <use3Dsecure>false</use3Dsecure>
        <serviceEndpoint>https://www.empcorp-lux.com/api</serviceEndpoint> <!-- change endpoint to https://epro.empcorp.com/api if merchant is assigned by EMP to their platform B API, otherwise error like Invalid API key-->
        <container>window</container>
      </account>
    </entry>
    <entry>
     <string>CASHLIB</string>
      <account>
        <merchantId>??</merchantId>
        <secretKey>??</secretKey>
        <serviceEndpoint>https://api-test.cashlib.com/api</serviceEndpoint>
        <redirectUrl>${baseRedirectUrl}/api/cashlib/deposit/redirect/</redirectUrl>
        <supportedCurrencies>EUR</supportedCurrencies>
        <container>window</container> <!-- cashlib does NOT support iframe -->
        <width>800</width>
        <height>600</height>
        <successUrl>${successUrl}</successUrl>
        <failureUrl>${failureUrl}</failureUrl>
      </account>
    </entry>
    <entry>
      <string>DEFAULT</string>
      <account>
        <merchantName>??</merchantName>
        <secretKey>??</secretKey>
        <serviceEndpoint>https://api-test.cashlib.com/api</serviceEndpoint>
        <accountID>??</accountID>
        <posId>001</posId>
        <brandId>0</brandId>
        <crosscountry>Y</crosscountry>
      </account>
    </entry>
  </accounts>
  <!-- -->
  <returnUrl>${baseRedirectUrl}/api/emp/deposit/redirect/${ptx.txRefId}</returnUrl>
  
  <!--For PaymentWall-->
  <eproRedirectionHtmlTemplateName>emp-epro-redirection-template</eproRedirectionHtmlTemplateName>
  <eproFinalStepRedirectUrl>${baseRedirectUrl}/api/epro/deposit/paymentwall/redirect/finalStep/${ptx.txRefId}</eproFinalStepRedirectUrl>
  <!--<redirectUrl>${baseRedirectUrl}/cashier/callback/endcallback.html?txId=\${ptx.id}</redirectUrl>-->
<!--<successUrl>${successUrl}</successUrl>
<failureUrl>${failureUrl}</failureUrl>-->
</com.devcode.paymentiq.integration.emp.EmpConfig>

```
</details>


### Attributes

| Attribute     | Description                 |
|---------------|-----------------------------|
| secretKey     | Secret Key, provided by EMP |
| usemerchantId | Merchant Id, provide by EMP |
| merchantName  | Merchant Name               |
| accountId     | Account Id, provided by EMP |

### Notification URL For Production

https://api.paymentiq.io/paymentiq/api/emp/deposit/callback

## Example Routing Rule

![](/img/providers/routing/emp.png)

## Test Information

- For N3DS transactions: 4539527688361959 12/24 123
- For 3DS transactions: 4916940533448272 12/24 123

### EMP Kwickgo

- For N3DS transactions: 4916940533448272 12/24 123

### EMP PassNGo

- For 3DS/N3DS transactions: 4916940533448272 12/24 123

### EMP CryptoGo

- Successful transaction: 4000000000000002, CVV 123, Expiry date in the future
- Failed transaction: 4917484589897107, CVV 123, Expiry date : 04/2023