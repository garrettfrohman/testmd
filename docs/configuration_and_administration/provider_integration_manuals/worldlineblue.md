--- 
id: "worldlineblue"
title: "Worldline Blue"
hide_title: "true"
---

![Worldline logo](/img/providers/logos/worldlineblue.png)

# Worldline Blue

## About

| Provider Name                | Worldline Blue                                                                  |
|------------------------------|---------------------------------------------------------------------------------|
| Link                         | -                                                                               |
| Classification               | Credit Card Processor                                                           |
| Regions                      | International                                                                   |
| Currencies                   | Please check directly with the provider regarding what currencies are supported |
| Methods/PaymentTxTypes       | `CreditcardDeposit` <br/> `Capture` <br/> `Void`<br/> `Refund`                  |
| PaymentIQ Configuration File | `WorldlineBlueConfig`                                                           |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.worldlineblue.WorldlineBlueConfig>
  <enabled>true</enabled>
  <useViqProxy>true</useViqProxy>
  <accounts>
    <entry>
      <string>3DS2</string>
      <account>
        <merchantId>??</merchantId>
        <merchantName>????</merchantName>
        <use3Dsecure>true</use3Dsecure>
        <!-- 3DS2 -->
        <mcc>????</mcc> <!-- 4 Digit Merchant Category Code according to the acquiring agreement -->
        <merchantCountry>SWE</merchantCountry>  <!-- Your legal registration country -->
        <merchantUrl>https://www.yourURL.com</merchantUrl>  <!-- must include https:// -->
      </account>
    </entry>
  </accounts>
</com.devcode.paymentiq.integration.worldlineblue.WorldlineBlueConfig>
```

</details>

### Attributes

| Attribute    | Description                         |
|--------------|-------------------------------------|
| merchantId   | The MerchantID provied by Worldline |
| merchantName | Merchant entity name                |

## Example Routing Rule

![](/img/providers/routing/worldlineblue.png)

## Test Information

### Test Cards

| PAN              | CVC | Exp. date | 3DS2 action  |
|------------------|-----|-----------|--------------|
| 4541150000111600 | Any | 12/28     | Frictionless |
| 4454757952056446 | Any | 03/24     | Challenge    |
| 5413330089020029 | Any | 12/34     | Frictionless |
| 5413330089020011 | Any | 12/34     | Challenge    |