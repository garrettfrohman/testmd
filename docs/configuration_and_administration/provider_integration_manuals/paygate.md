--- 
id: "paygate" 
title: "PayGate"
hide_title: "true"
---
 
![](/img/providers/logos/paygate.png)

# PayGate

## About
PayGate is a payment provider that supports credit card payments.

| Provider Name                | PayGate                                                                                                                      |
|------------------------------|------------------------------------------------------------------------------------------------------------------------------|
| Link                         | [https://www.paygate.co.za/](https://www.paygate.co.za/) <br/> [PayGate Documentation](http://docs.paygate.co.za/#testing-2) |
| Classification               | Credit Card                                                                                                                  |
| Regions                      | `International`                                                                                                              |
| Currencies                   | Please check directly with the provider regarding what currencies are supported                                              |
| Methods/PaymentTxTypes       | `CreditcardDeposit`<br/> `CreditcardWithdrawal`                                                                              |
| PaymentIQ Configuration File | `PayGateConfig`                                                                                                              |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.paygate.PayGateConfig>
  <enabled>true</enabled>
  <useViqProxy>true</useViqProxy>
  <testMode>false</testMode>
  <accounts>
    <entry>
      <string>N3DS</string>
      <account>
        <accountID>??</accountID>
        <password>test</password>
        <supportedCurrencies>USD|EUR</supportedCurrencies>
        <authType>FINAL_AUTH</authType> <!-- This doesn't control if the deposit is just an authorization or auto-settle. That is configured on the merchant account on PayGate's side. It should be configured the same here so that transactions get correct status codes. -->
      </account>
    </entry>
    <entry>
      <string>3DS_auto</string>
      <account>
        <accountID>??</accountID>
        <password>test</password>
        <supportedCurrencies>ZAR</supportedCurrencies>
        <authType>AUTH_CAPTURE</authType> <!-- This doesn't control if the deposit is just an authorization or auto-settle. That is configured on the merchant account on PayGate's side. It should be configured the same here so that transactions get correct status codes. -->
      </account>
    </entry>
    <entry>
      <string>3DS</string>
      <account>
        <accountID>??</accountID>
        <password>test</password>
        <supportedCurrencies>USD|EUR</supportedCurrencies>
        <authType>FINAL_AUTH</authType> <!-- This doesn't control if the deposit is just an authorization or auto-settle. That is configured on the merchant account on PayGate's side. It should be configured the same here so that transactions get correct status codes. -->
      </account>
    </entry>
  </accounts>
</com.devcode.paymentiq.integration.paygate.PayGateConfig>
```

</details>

### Attributes

| PaymentIQ Configuration | Description                                                                                                                                                                                                                     |
|-------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| accountID               | "PayGate ID". Provided by PayGate                                                                                                                                                                                               |
| password                | "Password". Provided by PayGate                                                                                                                                                                                                 |
| authType                | This doesn't control if the deposit is just an authorization or auto-settle. That is configured on the merchant account on PayGate's side. It should be configured the same here so that transactions get correct status codes. |

## Example Routing Rule
![](/img/providers/routing/paygate.png)

## Test Information

| Card Brand | Number           | CVV | Expiry date | Result/Info        |
|------------|------------------|-----|-------------|--------------------|
| Visa       | 4000000000000002 | Any | Any         | Approved           |
| Visa       | 4000000000000028 | Any | Any         | Insufficient funds |
| Visa       | 4000000000000036 | Any | Any         | Declined           |
| MasterCard | 5200000000000015 | Any | Any         | Approved           |
| MasterCard | 5200000000000023 | Any | Any         | Insufficient funds |
| MasterCard | 5200000000000049 | Any | Any         | Declined           |
| AMEX       | 378282246310005  | Any | Any         | Approved           |
| AMEX       | 371449635398431  | Any | Any         | Insufficient funds |
| Diner      | 30569309025904   | Any | Any         | Declined           |

