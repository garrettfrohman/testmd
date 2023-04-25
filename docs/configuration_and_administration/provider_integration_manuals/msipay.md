--- 
id: "msipay" 
title: "MSI Pay"
hide_title: "true"
---
 
![](/img/providers/logos/msipay.png)

# MSI Pay

## About
MSI Pay is a payment provider offering creditcard deposit (3DS/N3DS) and status check.

Impaya and creditcard payment via PayGate is also supported.

| Provider Name                | MSI Pay                                                                         |
|------------------------------|---------------------------------------------------------------------------------|
| Link                         | -                                                                               |
| Classification               | Debit/Credit Card Processor                                                     |
| Regions                      | ALL                                                                             |
| Currencies                   | Please check directly with the provider regarding what currencies are supported |
| Methods/PaymentTxTypes       | `CreditcardDeposit`                                                             |
| PaymentIQ Configuration File | `MsiPayConfig`                                                                  |


## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.msipay.MsiPayConfig>
  <enabled>true</enabled>
  <useViqProxy>true</useViqProxy>
  <accounts>
    <entry>
      <string>DEFAULT</string>
      <account>
        <username>??</username>
        <password>??</password>
        <secretKey>??</secretKey>
        <instance>??</instance>
        <accountID>??</accountID>
        <use3Dsecure>true</use3Dsecure>
        <supportedCurrencies>EUR|USD</supportedCurrencies>
        <language>en</language>
      </account>
    </entry>
  </accounts>
  <testMode>true</testMode>
  <defaultDescriptor>Bambora payment ${ptx.txRefId}</defaultDescriptor>
</com.devcode.paymentiq.integration.msipay.MsiPayConfig>
```
</details>

### Attributes

| Attribute         | Description                                                                                                              |
|-------------------|--------------------------------------------------------------------------------------------------------------------------|
| account.username  | It is used to create Authorization request header. Provided by the MSI Pay.                                              |
| account.password  | It is used to create Authorization request header. Provided by the MSI Pay.                                              |
| account.secretKey | It is used to generate and validate a callback notification signature. Provided by the MSI Pay.                          |
| account.instance  | Corresponds to the instance name from MSI Pay. Instance - is like separate merchant's environment in the MSI Pay system. |
| account.accountID | Corresponds to the application from MSI Pay. A merchant can have multiple applications (IDs) within an instance.         |

NOTE: MSI Pay will provide all required information (in the table above) to the merchant directly.

Please check a table below how to trigger a specific payment method:

| PaymentIQ Payment Method | Transaction Type   | Service |
|--------------------------|--------------------|---------|
| CreditCard               | CreditcardDeposit  | -       |
| PayGate CreditCard       | CreditcardDeposit  | PAYGATE |
| IMPAYA                   | WebRedirectDeposit | IMPAYA  |

## Example Routing Rule

![](/img/providers/routing/msipay.png)

## Test Information

### Deposit

| Card Number         | Description                          |
|---------------------|--------------------------------------|
| 4444 3333 2222 1111 | Successful deposit without 3D secure |
| 4012 0010 3714 1112 | Successful deposit with 3D secure    |
| 4242 4242 4242 4242 | Unsuccessful deposit with 3D secure  |
