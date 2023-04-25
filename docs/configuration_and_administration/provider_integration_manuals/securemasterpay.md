--- 
id: "securemasterpay" 
title: "SecureMasterPay"
hide_title: "true"
---
 
![](/img/providers/logos/securemasterpay.png)

# SecureMasterPay

## About
SecureMasterPay is a payment provider offering creditcard deposit (3DS/N3DS), withdrawal and refund.

| Provider Name                | SecureMasterPay                                                      |
|------------------------------|----------------------------------------------------------------------|
| Link                         | [https://www.securemasterpay.com/](https://www.securemasterpay.com/) |
| Classification               | Debit/Credit Card Processor                                          |
| Regions                      | `International`*                                                     |
| Currencies                   | `USD`, `EUR`, `RUB`                                                  |
| Methods/PaymentTxTypes       | `CreditcardDeposit`<br/>`CreditcardWithdrawal`<br/>`Refund`          |
| PaymentIQ Configuration File | `SecureMasterPayConfig`                                              |

\* Except USA, Canada, Israel, Singapore and sanctioned countries

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.securemasterpay.SecureMasterPayConfig>
  <enabled>true</enabled>
  <testMode>false</testMode>
  <useViqProxy>true</useViqProxy>
  <accounts>
    <entry>
      <string>DEFAULT</string>
      <account>
        <secretKey>??</secretKey><!--Private Key-->
        <accessToken>??</accessToken><!--Token-->
        <productName>??</productName><!--can be left blank-->
        <!--useTokenId=true and withdrawalType=OCT to enable OCT payout-->
        <useTokenId>false</useTokenId>
        <withdrawalType>OCT</withdrawalType>
        <supportedCurrencies>EUR|USD|RUB</supportedCurrencies>
      </account>
    </entry>
  </accounts>
  <container>window</container>
</com.devcode.paymentiq.integration.securemasterpay.SecureMasterPayConfig>
```
</details>

### Attributes

| Attribute           | Description                                                                                                     |
|---------------------|-----------------------------------------------------------------------------------------------------------------|
| account.secretKey   | Corresponds to *Private Key* from SecureMasterPay. It is used to authenticate the requests from PIQ to the PSP. |
| account.accessToken | Corresponds to *Token* from SecureMasterPay.                                                                    |
| account.productName | Product name (Service description). Can be blank.                                                               |

The Private Key and Token can be found in the SecureMasterPay backoffice under the "Merchant" tab at the "Profile" section:

![](/img/providers/securemasterpay_bo.png)

## Example Routing Rule
![](/img/providers/routing/securemasterpay.png)

## Test Information

| Card Number      | Description                             |
|------------------|-----------------------------------------|
| 4617611794313933 | CONFIRMED as 3-D Secure transaction     |
| 4626233193837898 | DECLINED as 3-D Secure transaction      |
| 4392963203551251 | CONFIRMED as non 3-D Secure transaction |
| 4730198364688516 | DECLINED as non 3-D Secure transaction  |
| 4271619466080208 | CONFIRMED as payout card                |
| 4811437417740292 | DECLINED as payout card                 |

You can use any cardholder name and CVV2/CVC2 with these PANs.

### Refunds
You can use an even amount in the refund request to emulate a successful refund, and an odd amount to emulate a false refund.
