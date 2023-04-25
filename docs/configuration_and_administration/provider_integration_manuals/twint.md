--- 
id: "twint" 
title: "Twint"
hide_title: "true"
---
 
![](/img/providers/logos/twint.png)

# Twint

## About
Twint is a mobile app payment solution that offers deposits, refunds and withdrawals.

| Provider Name                | Twint                                                                           |
|------------------------------|---------------------------------------------------------------------------------|
| Link                         | [https://www.twint.ch/en/](https://www.twint.ch/en/)                            |
| Classification               | Mobile Payment                                                                  |
| Regions                      | `Switzerland`                                                                   |
| Currencies                   | Please check directly with the provider regarding what currencies are supported |
| Methods/PaymentTxTypes       | `TwintDeposit` <br/> `Refund`                                                   |
| PaymentIQ Configuration File | `TwintConfig`                                                                   |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.twint.TwintConfig>
  <enabled>true</enabled>
  <accounts>
    <entry>
     <string>default</string>
     <account>
        <merchantId>????????-????-????-????-?????????????</merchantId>
        <storeId>???????</storeId> <!-- CashRegisterId  -->
        <supportedCurrencies>CHF</supportedCurrencies>
     </account>
    </entry>
  </accounts>
</com.devcode.paymentiq.integration.twint.TwintConfig>
```

</details>

### Attributes

| Attribute  | Description                                                                                                 |
|------------|-------------------------------------------------------------------------------------------------------------|
| merchantId | Merchant UUID provided by Twint                                                                             |
| storeId    | CashRegisterId. Defined by merchant. Each ID must be registered before it can be used. See more info below. |

### Enroll Cash Register
All payments are made with a specific CashRegisterId. A CashRegisterId is a unique value defined by the merchant that should be configured in PIQ according to the documentation above.

Before the cash register can be used to process payments through PIQ it must be enrolled. This is a manual step, please contact the support team.

## Example Routing Rules
![](/img/providers/routing/twint-dp.png)

## Test Information

You need a Twint test app for Android or iOS to fully test this solution. Please reach out to Twint for detailed instructions on how to install the test app. 

When selecting environment in the Twint configurator app, choose "Pat".

