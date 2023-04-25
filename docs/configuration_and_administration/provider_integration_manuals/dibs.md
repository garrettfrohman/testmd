--- 
id: "dibs" 
title: "DIBS"
hide_title: "true"
---
 
![](/img/providers/logos/dibs.png)

# DIBS

## About
DIBS is a creditcard processor with support for Deposits, Withdrawals, Refunds and Voids.

| Provider Name                | DIBS                                                                            |
|------------------------------|---------------------------------------------------------------------------------|
| Link                         | [http://www.dibspayment.com](http://www.dibspayment.com)                        |
| Classification               | Debit/Credit Card Processor                                                     |
| Regions                      | `International`                                                                 |
| Currencies                   | Please check directly with the provider regarding what currencies are supported |
| Methods/PaymentTxTypes       | `CreditcardDeposit`<br/> `CreditcardWithdrawal`<br/> `Refund`<br/> `Void`       |
| PaymentIQ Configuration File | `DibsConfig`                                                                    |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>

<br/>

```xml
<com.devcode.paymentiq.integration.dibs.DibsConfig>
  <enabled>true</enabled>
  <useViqProxy>true</useViqProxy>
  <accounts>
    <entry>
      <string>N3DS</string>
      <account>
        <shopName>??</shopName>
        <username>??</username>
        <password>??</password>
        <merchantId>??</merchantId>
        <use3Dsecure>false</use3Dsecure>
        <method>cc.test</method>
      </account>
    </entry>
    <entry>
      <string>3DS</string>
      <account>
        <shopName>??</shopName>
        <username>??</username>
        <password>??</password>
        <merchantId>??</merchantId>
        <use3Dsecure>true</use3Dsecure>
        <method>cc.test</method>
      </account>
    </entry>
  </accounts>
  <testMode>true</testMode>
  <defaultDescriptor>${defaultTransactionDescriptor}</defaultDescriptor>
</com.devcode.paymentiq.integration.dibs.DibsConfig>
```

</details>

### Attributes

| PaymentIQ Configuration | Provider Credential                                      |
|-------------------------|----------------------------------------------------------|
| shopName                | Provided in the welcome email from DIBS to the merchant. |
| username                | Provided in the welcome email from DIBS to the merchant. |
| password                | Provided in the welcome email from DIBS to the merchant. |
| merchantId              | Provided in the welcome email from DIBS to the merchant. |

## Example Routing Rule

![](/img/providers/routing/dibs.png)
![](/img/providers/routing/dibs2.png)

## Test Information

- Only test in currency SEK

### N3DS
| Card Brand | Account          | CVV | Expiry date |
|------------|------------------|-----|-------------|
| VISA       | 4711100000000000 | 123 | 12/24       |