--- 
id: "orangepay" 
title: "OrangePay"
hide_title: "true"
---
 
![](/img/providers/logos/orangepay.png)

# OrangePay

## About
OrangePay is a credit card processor and aggregator offering support for Deposits, Withdrawals and Refunds.

| Provider Name                | OrangePay                                                                     |
|------------------------------|-------------------------------------------------------------------------------|
| Link                         | [https://orange-pay.com/](https://orange-pay.com/)                            |
| Classification               | Debit/Credit Card Processor, Aggregator                                       |
| Regions                      | `International`                                                               |
| Currencies                   | `SEK`, `EUR`                                                                  |
| Methods/PaymentTxTypes       | `CreditcardDeposit`<br/>`CreditcardWithdrawal`<br/>`WebRedirect`<br/>`Refund` |
| PaymentIQ Configuration File | `OrangePayConfig`                                                             |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.orangepay.OrangePayConfig>
  <enabled>true</enabled>
  <useViqProxy>true</useViqProxy>
  <accounts>
    <entry>
      <string>default</string>
      <account>
        <use3Dsecure>true</use3Dsecure>
        <supportedCurrencies>USD|EUR</supportedCurrencies>
        <accessToken>???</accessToken>
      </account>
    </entry>
  </accounts>
  <testMode>true</testMode>
  <container>window</container>
  <width>600</width>
  <height>600</height>
  <defaultDescriptor>Descriptor example</defaultDescriptor>
  <dynamicDescriptor>https://www.merchant.com/</dynamicDescriptor>
</com.devcode.paymentiq.integration.orangepay.OrangePayConfig>
```

</details>

### Attributes

| Attribute   | Description                                                                       |
|-------------|-----------------------------------------------------------------------------------|
| accessToken | Access token used in the request header against OrangePay. Provided by OrangePay. |

### OrangePay Aggregator

When using the OrangePay aggregator solution the transaction type to use is `WebRedirectDeposit` with the correct service value.

#### Currently supported APM's with their corresponding service value

| APM name   | service value |
|------------|---------------|
| Card       | CARD          |
| Webmoney   | WEBMONEY      |
| Qiwi       | QIWI          |
| Yandex     | YANDEX        |
| Multibanco | MULTIBANCO    |
| mbway      | MBWAY         |

## Example Routing Rule

### Creditcard
![](/img/providers/routing/orangepay.png)

### Webredirect
![](/img/providers/routing/orangepay2.png)

## Test Information

- Currency : USD, EUR

### Creditcard N3DS

| Card Brand | Account          | CVV | Expiry date | Result/Info      |
|------------|------------------|-----|-------------|------------------|
| VISA       | 4111111111111111 | 123 | 01/20       | N3DS: Successful |
| VISA       | 4012888888881881 | 123 | 01/20       | N3DS: Failed     |

### Creditcard3DS

| Card Brand | Account          | CVV | Expiry date | OPT password |
|------------|------------------|-----|-------------|--------------|
| MASTERCARD | 5555555555554444 | 123 | 01/21       | 111222       |

### WebRedirect

The only APM that is currently supported by OrangePay on the test environment is Card. When redirected to the card input, please use the card information in the section above.
