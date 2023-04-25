--- 
id: "pradexx" 
title: "Pradexx"
hide_title: "true"
---
 
![](/img/providers/logos/pradexx.png)

# Pradexx

## About
Pradexx is a payment platform offering credit card and alternative payment methods. Credit card payments supports Deposit, Refund, Void, Auth and Capture. The alternative payment methods can be used with the PaymentTxTypes PradexxDeposit and as of now include Sofort and  NextPayWay with more in the pipeline. 

| Provider Name                | Pradexx                                                                            |
|------------------------------|------------------------------------------------------------------------------------|
| Link                         | [https://pradexx.com/](https://pradexx.com/)                                       |
| Classification               | Aggregator provider                                                                |
| Regions                      | `International`                                                                    |
| Currencies                   | Please check directly with the provider regarding what currencies are supported    |
| Methods/PaymentTxTypes       | `CreditcardDeposit`<br/> `Void`<br/> `Refund`<br/> `Capture`<br/> `PradexxDeposit` |
| PaymentIQ Configuration File | `PradexxConfig`                                                                    |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.pradexx.PradexxConfig>
  <enabled>true</enabled>
  <testMode>true</testMode>
  <useViqProxy>true</useViqProxy>
  <!-- mapping APM's to the corresponding Pradexx codes, defaults to "SOFORT->114,NEXTPAYWAY->126,UNIONPAY->146,NINJAWALLET->147" if absent-->
  <serviceMapping>SOFORT->114,NEXTPAYWAY->126</serviceMapping>
  <accounts>
    <entry>
      <string>creditcard</string>
      <account>
        <merchantId>???</merchantId> <!-- Provided by Pradexx. "Merchant number" -->
        <secretKey>???</secretKey> <!-- Provided by Pradexx. "Personal Hash Key" -->
        <merchantName>???</merchantName>
        <!--<authType>FINAL_AUTH</authType> Set this to make an authorization request-->
        <!--<supportedCurrencies>EUR|USD</supportedCurrencies> Optional-->
        <!--<container>window</container> Optional, defaults to iframe if not set-->
      </account>
    </entry>
    <entry>
      <string>apm</string>
      <account>
        <merchantId>???</merchantId>
        <secretKey>???</secretKey>
        <merchantName>???</merchantName>
        <!--<service>SOFORT</service> Optional, Only needs to be set if service is not sent in the request-->
        <!--<supportedCurrencies>EUR|USD</supportedCurrencies> Optional-->
        <!--<container>window</container> Optional, defaults to iframe if not set-->
      </account>
    </entry>
  </accounts>
</com.devcode.paymentiq.integration.pradexx.PradexxConfig>
```

</details>

### Attributes

| Attribute | Description |
|-----------|-------------|
|           |             |
|           |             |

### Pradexx merchant account
To setup Pradexx in PIQ the merchant first needs to obtain the following from Pradexx:
- The Merchant number. 
- Credentials for the merchant panel.
- The personal Hash Key.

## Example Routing Rules
![](/img/providers/routing/pradexx.png)

## Test Information
### Credit Card:
- Any expiry date in the near future may be used and any 3-digit CVV code (4 digits for American Express).
- Use the following amounts to cause either approval or various declines:
    - 55.3 3D secure flow.
    - 0.04 Error 1001: Soft Decline.
    - 0.05 Error 1002: Insufficient Funds.
    - 0.91 Approved with 10 second delay.
    - 0.99 Approved with 90 second delay.

| Credit   Card Number | Issuer                |
|----------------------|-----------------------|
| 4387751111111111     | VISA (US)             |
| 5442987111111111     | MasterCard (US)       |
| 371000911111111      | American Express (US) |
| 4056850111111111     | Visa (FR)             |
| 5130113111111111     | MasterCard (FR)       |
| 36005131111111       | Diners Club (GB)      |
| 3535111111111111     | JCB (JP)              |
| 6221701111111111     | LivaKash (JP)         |
| 4580000000000000     | VISA (IL)             |
| 5326140000000000     | MasterCard (IL)       |
| 91000000             | IsraCard (IL)         |

### PradexxDeposit (APM):
Choose the payment method and follow the instructions after being redirected.


