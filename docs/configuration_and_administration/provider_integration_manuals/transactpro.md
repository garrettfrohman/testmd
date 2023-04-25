--- 
id: "transactpro" 
title: "TransactPro"
hide_title: "true"
---
 
![](/img/providers/logos/transactpro.png)

# TransactPro

## About
TransactPro is a creditcard processor with support for Deposits, Withdrawals, Refunds, Captures and Voids.

| Provider Name                | TransactPro                                                                              |
|------------------------------|------------------------------------------------------------------------------------------|
| Link                         | [https://www.transactpro.eu/](https://www.transactpro.eu/)                               |
| Classification               | Debit/Credit Card Processor                                                              |
| Regions                      | `International`                                                                          |
| Currencies                   | Please check directly with the provider regarding what currencies are supported          |
| Methods/PaymentTxTypes       | `CreditcardDeposit`<br/> `CreditcardWithdrawal`<br/> `Refund`<br/> `Capture`<br/> `Void` |
| PaymentIQ Configuration File | `TransactProConfig`                                                                      |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.transactpro.TransactProConfig>
  <enabled>true</enabled>
  <useViqProxy>true</useViqProxy>
   <testMode>false</testMode>
	 <threeDsRountingStr>BA01</threeDsRountingStr>
	 <n3DSRoutingStr>BA02</n3DSRoutingStr>
   <withdrawalRoutingStr>BA04</withdrawalRoutingStr>
   <recurringRoutingStr>BA03</recurringRoutingStr>
  <accounts>
    <entry>
      <string>default</string>
      <account>
        <username></username>
        <profilePassword></profilePassword>
        <memberGuid></memberGuid>
        <password></password><!-- SHA1 hash of the processing password-->
        <supportedCurrencies>USD|EUR</supportedCurrencies>
        <use3Dsecure>true</use3Dsecure>
        <authType>AUTH_CAPTURE</authType>
           <!--
        <authType>AUTH_CAPTURE</authType>
        <authType>FINAL_AUTH</authType>
        <authType>PRE_AUTH</authType>
        -->
      </account>
    </entry>
    
  </accounts>
  <defaultDescriptor>descriptor</defaultDescriptor>
  <redirectUrl>${baseRedirectUrl}/api/transactpro/redirect/${ptx.txRefId}</redirectUrl>
  <callbackUrl>${baseCallbackUrl}/api/transactpro/callback/${ptx.txRefId}</callbackUrl>
  
</com.devcode.paymentiq.integration.transactpro.TransactProConfig>

```

</details>

### Attributes

| Attribute       | Description             |
|-----------------|-------------------------|
| username        | Provided by TransactPro |
| profilePassword | Provided by TransactPro |
| memberGuid      | Provided by TransactPro |
| password        | Provided by TransactPro |

## Example Routing Rule
![](/img/providers/routing/transactpro.png)
## Test Information
- Currency: EUR, USD

### N3DS

| Card Brand | Account          | CVV | Expiry date |
|------------|------------------|-----|-------------|
| MASTER     | 5413330000000001 | 589 | 01/22       |

### 3DS

| Card Brand | Account          | CVV | Expiry date |
|------------|------------------|-----|-------------|
| MASTER     | 5413330000000019 | 589 | 01/20       |

### Withdrawal (CRD)

| Card Brand | Account          | CVV | Expiry date |
|------------|------------------|-----|-------------|
| MASTER     | 4483150610545551 | 349 | 03/20       |