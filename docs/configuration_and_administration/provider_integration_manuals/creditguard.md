--- 
id: "creditguard" 
title: "CreditGuard"
hide_title: "true"
---
 
![](/img/providers/logos/creditguard.png)

# CreditGuard

## About
CreditGuard is a creditcard processor with support for Deposits, Withdrawals, Refunds and Voids.

| Provider Name                | CreditGuard                                                                      |
|------------------------------|----------------------------------------------------------------------------------|
| Link                         | [https://www.creditguard.co.il/?lang=en](https://www.creditguard.co.il/?lang=en) |
| Classification               | Debit/Credit Card Processor                                                      |
| Regions                      | `International`                                                                  |
| Currencies                   | Please check directly with the provider regarding what currencies are supported  |
| Methods/PaymentTxTypes       | `CreditcardDeposit`<br/> `CreditcardWithdrawal`<br/> `Refund`<br/> `Void`        |
| PaymentIQ Configuration File | `CreditGuardConfig`                                                              |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.creditguard.CreditGuardConfig>
  <enabled>true</enabled>
  <useViqProxy>true</useViqProxy>
  <accounts>
    <entry>
      <string>N3DS</string>
      <account>
        <auth>false</auth>
        <username>??</username>
        <password>??</password>
        <accountID>??</accountID>
        <use3Dsecure>false</use3Dsecure>
      </account>
    </entry>
    <entry>
      <string>N3DS_AUTH</string>
      <account>
        <auth>true</auth>
        <username>??</username>
        <password>??</password>
        <accountID>??</accountID>
        <use3Dsecure>false</use3Dsecure>
      </account>
    </entry>
    <entry>
      <string>3DS</string>
      <account>
        <auth>false</auth>
        <username>??</username>
        <password>??</password>
        <accountID>??</accountID>
        <use3Dsecure>true</use3Dsecure>
      </account>
    </entry>
    <entry>
      <string>3DS_AUTH</string>
      <account>
        <auth>true</auth>
        <username>??</username>
        <password>??</password>
        <accountID>??</accountID>
        <use3Dsecure>true</use3Dsecure>
      </account>
    </entry>
  </accounts>
  <defaultDescriptor>??</defaultDescriptor>
</com.devcode.paymentiq.integration.creditguard.CreditGuardConfig>
```
</details>

### Attributes

| Attribute | Description                          |
|-----------|--------------------------------------|
| auth      | -                                    |
| username  | Username. Provided by CreditGuard.   |
| password  | Password. Provided by CreditGuard.   |
| accountID | AccountID . Provided by CreditGuard. |

## Example Routing Rule
![](/img/providers/routing/creditguard.png)
![](/img/providers/routing/creditguard2.png)

## Test Information

### Test Cards 3DS/N3DS

| Card Brand | Account          | CVV | Expiry date | 3DS Code | 3DS Result       |
|------------|------------------|-----|-------------|----------|------------------|
| VISA       | 4000000000000002 | Any | Any         | 1234     | Enrolled (Y)     |
| VISA       | 4000000000000051 | Any | Any         | N/A      | Not enrolled (N) |
| VISA       | 4901164281364345 | Any | Any         | N/A      | Unknown (U)      |
| MASTERCARD | 5200000000000007 | Any | Any         | 1234     | Enrolled (Y)     |
| MASTERCARD | 5200000000000056 | Any | Any         | N/A      | Not enrolled (N) |
| MASTERCARD | 5148792043580301 | Any | Any         | N/A      | Unknown (U)      |

All the of the above cards work for withdrawals as well.
