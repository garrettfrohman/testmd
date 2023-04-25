--- 
id: "ecomcharge" 
title: "eComCharge"
hide_title: "true"
---
 
![](/img/providers/logos/ecomcharge.png)

# eComCharge

## About
eComCharge is a payment provider that offers a wide range of different payment options including several bank payment integrations. When making a payment the end user will be redirected to eComCharge’s payment option selector page. Available payment methods can be configured in your eComCharge account.

| Provider Name                | eComCharge                                         |
|------------------------------|----------------------------------------------------|
| Link                         | [https://ecomcharge.com/](https://ecomcharge.com/) |
| Classification               | Online Banking                                     |
| Regions                      | `Latvia`                                           |
| Currencies                   | `EUR`                                              |
| Methods/PaymentTxTypes       | `EComChargeDeposit`<br/> `BankDeposit`             |
| PaymentIQ Configuration File | `EcomchargeConfig`                                 |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>

<br/>

```xml
<com.devcode.paymentiq.integration.ecomcharge.EComChargeConfig>
  <enabled>true</enabled>
  <height>800</height>
  <width>1100</width>
  <container>window</container> <!-- container should be window to avoid redirect issue -->
  <accounts>
    <entry>
      <string>default</string>
      <account>
        <merchantId>*****</merchantId>
        <secretKey>?????</secretKey>
        <supportedCurrencies>XXX|YYY|ZZZ</supportedCurrencies>
        <testPaymentMethodType>BankLink</testPaymentMethodType> <!-- Only used for test -->
      </account>
    </entry>
  </accounts>
</com.devcode.paymentiq.integration.ecomcharge.EComChargeConfig>
```
</details>

### Attributes

| PaymentIQ Configuration | Provider Credential                                                                                                                                                 |
|-------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| merchantId              | Provided by EComCharge                                                                                                                                              |
| secretKey               | Provided by EComCharge                                                                                                                                              |
| testPaymentMethodType   | Used to simulate a specific payment method in test. It can be set to valid type code according to EComCharge documentation. For example BankLink for bank payments. |

## Example Routing Rule

If deposits are processed through the regular bank API, the BankDeposit tx type should be used to route payments. For the separate eComCharge API use tx type EComChargeDeposit. An example of both types of rules is shown in the picture below.

![](/img/providers/routing/ecomcharge.png)

## Test Information

No test information available. Please reach out to the provider.