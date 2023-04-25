--- 
id: "wirecard" 
title: "Wirecard"
hide_title: "true"
---
 
![](/img/providers/logos/wirecard.png)

# Wirecard

## About
Wirecard is a creditcard processor with support for Deposits, Withdrawals, Refunds, Voids and Captures.

| Provider Name                | Wirecard                                                                                 |
|------------------------------|------------------------------------------------------------------------------------------|
| Link                         | [https://www.wirecard.com](https://www.wirecard.com)                                     |
| Classification               | Debit/Credit Card Processor                                                              |
| Regions                      | `International`                                                                          |
| Currencies                   | Please check directly with the provider regarding what currencies are supported          |
| Methods/PaymentTxTypes       | `CreditcardDeposit`<br/> `CreditcardWithdrawal`<br/> `Refund`<br/> `Void`<br/> `Capture` |
| PaymentIQ Configuration File | `WirecardConfig`                                                                         |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.wirecard.WirecardConfig>
  <enabled>true</enabled>
 <useViqProxy>true</useViqProxy>
  <accounts>
    <entry>
      <string>RECURRING</string>
      <account>
        <serviceEndpoint>https://c3.wirecard.com/secure/ssl-gateway</serviceEndpoint>
        <username>??</username>
        <password>??</password>
        <businessCaseSignature>??</businessCaseSignature>
        <use3Dsecure>false</use3Dsecure>
        <useTokenId>true</useTokenId>
      </account>
    </entry>
    <entry>
      <string>N3DS</string>
      <account>
        <serviceEndpoint>https://c3.wirecard.com/secure/ssl-gateway</serviceEndpoint>
        <username>??</username>
        <password>??</password>
        <businessCaseSignature>??</businessCaseSignature>
        <use3Dsecure>false</use3Dsecure>
      </account>
    </entry>    
    <entry>
      <string>3DS</string>
      <account>
        <serviceEndpoint>https://c3.wirecard.com/secure/ssl-gateway</serviceEndpoint>
        <username>??</username>
        <password>??</password>
        <businessCaseSignature>??</businessCaseSignature>
        <use3Dsecure>true</use3Dsecure>
      </account>
    </entry>
    <entry>
      <string>OCT</string>
      <account>
        <serviceEndpoint>https://c3.wirecard.com/secure/ssl-gateway</serviceEndpoint>
        <username>??</username>
        <password>??</password>
        <businessCaseSignature>??</businessCaseSignature>
        <use3Dsecure>true</use3Dsecure>
        <nonGamblingWithdrawal>false</nonGamblingWithdrawal>
      </account>
    </entry>
  </accounts>
  <!--<defaultStatementText></defaultStatementText> Refers to Wirecard parameter cardStatement -->
</com.devcode.paymentiq.integration.wirecard.WirecardConfig>
```

</details>

### Attributes

| Attribute | Description          |
|-----------|----------------------|
| username  | Provided by Wirecard |
| password  | Provided by Wirecard |

### Cross Merchant Account Processing

If a merchant has several accounts with different business case signatures (BCSig), it's recommended that cross merchant account processing is enabled (by merchant's Wirecard account manager) between the different accounts. This means that
the saved references from a transaction with one account can be used in a repeat payment against another account under the same merchant. If this is not enabled, the following decline message will be given by Wirecard:
**"Could not find referenced transaction for GuWID"**

## Example Routing Rule

![](/img/providers/routing/wirecard.png)

## Test Information

For even more 3DS test cards with different responses/outcomes, please visit:

https://document-center.wirecard.com/display/PTD/Appendix+K%3A+Test+Access+Data+and+Credentials

### N3DS

| Card Brand  | Account            | CVV  | Expiry date |
|-------------|--------------------|------|-------------|
| VISA        | 4200000000000000   | Any  | Any         |
| VISA        | 4200000000000018   | 018  | Any         |
| MASTERCARD  | 5500000000000012   | 012  | Any         |
| MAESTRO     | 675940000000000002 | Any  | Any         |
| AMEX        | 370000000000010    | 0010 | Any         |
| JCB         | 3528000000000015   | 015  | Any         |
| DINERS CLUB | 38000000000014     | 014  | Any         |
| DISCOVER    | 6011000000000012   | 012  | Any         |

### 3DS

| Card Brand | Account             | CVV  | Expiry date | 3DS PWD  |
|------------|---------------------|------|-------------|----------|
| VISA       | 4012000300001003    | 003  | 01/23       | wirecard |
| MASTERCARD | 5413330300001006    | 006  | 01/23       | wirecard |
| MAESTRO    | 6799860300001000003 | 003  | 01/23       | wirecard |
| AMEX       | 375987000000005     | 1005 | 01/23       | wirecard |

### OCT / Withdrawal

| Card Brand | Account          | CVV | Expiry date |
|------------|------------------|-----|-------------|
| VISA       | 4012000300002001 | 001 | 01/23       |
