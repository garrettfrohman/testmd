--- 
id: "safetypay" 
title: "SafetyPay"
hide_title: "true"
---
 
![](/img/providers/logos/safetypay.png)

# SafetyPay

## About
SafetyPay is a banking provider with support for Deposits and Refunds.

| Provider Name                | Safetypay                                                      |
|------------------------------|----------------------------------------------------------------|
| Link                         | [https://www.safetypay.com/en/](https://www.safetypay.com/en/) |
| Classification               | Online Banking                                                 |
| Regions                      | `Latin America`, `Europe`                                      |
| Currencies                   | `EUR`, `BRL`, `CLP`, `COP`, `CRC`, `USD`, `MXN`, `PEN`         |
| Methods/PaymentTxTypes       | `BankDeposit` <br/> `Refund`                                   |
| PaymentIQ Configuration File | `SafetypayConfig`                                              |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>


```xml
<com.devcode.paymentiq.integration.safetypay.SafetypayConfig>
  <enabled>true</enabled>
  <accounts>
    <entry>
       <string>default</string>
       <account>
        <accountID>??</accountID>
        <secretKey>??</secretKey>
        <supportedCurrencies>USD|EUR|BRL</supportedCurrencies>
        <!--<settlementCurrency>EUR</settlementCurrency>--> <!-- Enable to use "Reverse Forex" functionality -->
      </account>
    </entry>
  </accounts>
  <container>iframe</container>
  <!-- <expirationTime>120</expirationTime> -->  <!-- This is the CreateExpressToken in the SafetyPay API. Max value 300 -->
</com.devcode.paymentiq.integration.safetypay.SafetypayConfig>
```

</details>

### Attributes

| Attribute          | Description                                                                                                                           |
|--------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| accountID          | API key provided by Safetypay                                                                                                         |
| secretKey          | Signature key provider by Safetypay                                                                                                   |
| settlementCurrency | Enables Safetypay's "Reverse Forex" functionality. The value should be the currency the transcations should be settled in, e.g `EUR`. |

### Allow alternative settlement currency

To allow an alternative settlement currency you can enable Safetypay's Reverse Forex functionality. This is done by adding the `settlementCurrency` entry with the wanted currency on the account level of the SafetypayConfig.

Example: `<settlementCurrency>EUR</settlementCurrency>`

### Callback URLs

- Production: https://api.paymentiq.io/paymentiq/api/safetypay/deposit/callback
- Test: https://test-api.paymentiq.io/paymentiq/api/safetypay/deposit/callback

## Example Routing Rule
![](/img/providers/routing/safetypay.png)

## Test Information
- Once a SafetyPay payment is initiated and you are redirected, choose the payment method with the Safetypay logo, and press continue.
- Enter any value in the username and password inputs and press log in, on the next page press confirm.
