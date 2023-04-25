--- 
id: "biilz" 
title: "Biilz"
hide_title: "true"
---
 
![](/img/providers/logos/biilz.png)

# Biilz

## About
Biilz is the leading mobile wallet of choice to manage your global bills payments using your funds through your smartphone or the physical Biilz Card. All these features in one awesome app!

| Provider Name                | Biilz                                                                           |
|------------------------------|---------------------------------------------------------------------------------|
| Link                         | [https://www.biilz.com/](https://www.biilz.com/)                                |
| Classification               | Debit/Credit Card Processor                                                     |
| Regions                      | `International`                                                                 |
| Currencies                   | Please check directly with the provider regarding what currencies are supported |
| Methods/PaymentTxTypes       | `CreditcardDeposit`                                                             |
| PaymentIQ Configuration File | `BiilzConfig`                                                                   |


## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.biilz.BiilzConfig>
  <enabled>true</enabled>
  <useViqProxy>true</useViqProxy>
  <accounts>
    <entry>
      <string>DEFAULT</string>
      <account>
        <merchantName>Devcode</merchantName>
        <email>****</email>
        <password>****</password>
        <supportedCurrencies>EUR</supportedCurrencies>
      </account>
    </entry>
  </accounts>
  <defaultDescriptor>Devcode</defaultDescriptor>
  <testMode>true</testMode>
</com.devcode.paymentiq.integration.biilz.BiilzConfig>

```

</details>

### Attributes

| Attribute | Description       |
|-----------|-------------------|
| email     | Provided by Biilz |
| password  | Provided by Biilz |


## Example Routing Rule
![](/img/providers/routing/biilz.png)

## Test Information

Biilz does not provide a test environment.