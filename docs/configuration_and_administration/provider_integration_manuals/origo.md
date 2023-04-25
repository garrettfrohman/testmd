--- 
id: "origo" 
title: "Origo (Santander Norway)"
hide_title: "true"
---
 
![](/img/providers/logos/santander-origo.png)

# Origo (Santander Norway)

## About
Santander offers Norwegian e-commerce customers invoice and installments.

| Provider Name                | Origo                                                                  |
|------------------------------|------------------------------------------------------------------------|
| Link                         | [https://www.santanderconsumer.no/](https://www.santanderconsumer.no/) |
| Classification               | `Online Banking`                                                       |
| Regions                      | `Norway`                                                               |
| Currencies                   | `NOK`                                                                  |
| Methods/PaymentTxTypes       | `OrigoHereAndNowDeposit` <br/> `OrigoInvoiceDeposit`                   |
| PaymentIQ Configuration File | `OrigoConfig`                                                          |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.santander.origo.OrigoConfig>
  <enabled>true</enabled>
  <accounts>
    <entry>
      <string>default</string>
      <account>
        <merchantId>??</merchantId> 
      </account>
    </entry>
  </accounts>
</com.devcode.paymentiq.integration.santander.origo.OrigoConfig>
```

</details>

### Attributes

#### Root level

| Attribute     | Default value | Description                                                                                                                                                      |
|---------------|---------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| preProd       | `false`       | When `true`, the pre-production environment of Origo will be used (overrides `testMode`)                                                                         |
| signInIframe  | `false`       | When `true`, redirect to authentication service will be done in the cashier iframe. Otherwise a new window is opened. (Norwegian BankId does not support iframe) |
| invoiceDueDay | 15            | The number of days before an invoice is due to be paid                                                                                                           |

#### Account level

| Attribute  | Default value | Description                                 |
|------------|---------------|---------------------------------------------|
| merchantId |               | VendorId in Origo (obtained from Santander) |


## Example Routing Rule

![](/img/providers/routing/santander-origo.png)

## Transaction Flow

There are three payment flows possible.

*  `OrigoInvoiceDeposit` uniquely maps to the invoice flow 
*  `OrigoHereAndNowDeposit` can be used with or without *service* `FIXED`.
    * Without `FIXED` the user can select between different credits that don't have a monthly payments
    * `FIXED` will give the user the choice between a few fixed monthly fees to pay and show the total credit cost associated with them

![](/img/providers/santander-origo_1.png)

## Test Information

Testing requires national identity numbers that are valid for the pre-production environment. Santander can supply these.

