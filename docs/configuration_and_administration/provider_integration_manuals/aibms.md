--- 
id: "aibms" 
title: "AIBMS"
hide_title: "true"
---
 
![](/img/providers/logos/aibms.png)

# AIBMS

## About
AIB Merchant Services is one of Ireland’s largest providers of payment solutions, with extensive operations in Ireland and Britain, and with card processing capabilities throughout continental Europe.

| Provider Name                | AIBMS                                                                                                     |
|------------------------------|-----------------------------------------------------------------------------------------------------------|
| Link                         | [https://www.aibms.com/](https://www.aibms.com/)                                                          |
| Classification               | `Debit/Credit Card Processor`                                                                             |
| Regions                      | `International`                                                                                           |
| Currencies                   | Please check directly with the provider regarding what currencies are supported                           |
| Methods/PaymentTxTypes       | `CreditcardDeposit`, `CreditcardWithdrawal`, `CreditcardAccountVerification`, `Capture`, `Void`, `Refund` |
| PaymentIQ Configuration File | `AIBMSConfig`                                                                                             |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.aibms.AIBMSConfig>
  <enabled>true</enabled>
  <useViqProxy>true</useViqProxy>
  <accounts>
    <entry>
      <string>default</string>
      <account>
        <storeId>???</storeId>
        <supportedCurrencies>??</supportedCurrencies>
      </account>
    </entry>
  </accounts>
</com.devcode.paymentiq.integration.aibms.AIBMSConfig>
```

</details>

### Attributes


| Attribute         | Description                                                 |
|-------------------|-------------------------------------------------------------|
| storeId           | Account level: Store (storename/username) provided by AIBMS |
| cardReadingMethod | For enabling MOTO deposits                                  |

### Notes

- AIBMS supports external 3DS1 and 3DS2 that should be configured according to documentation.
- AIBMS also has support for MOTO(Mail Order Telephone Order) deposits, to enable MOTO add `&lt;cardReadingMethod&gt;MOTO&lt;cardReadingMethod&gt;` in an account in the configuration.

## Example Routing Rule

![](/img/providers/routing/aibms.png)


## Test Information

| Type                | Number           | CVV              | Expiry Date     |
|---------------------|------------------|------------------|-----------------|
| VISA 3DS2           | 4035874000424977 | Any three digits | Any future date |
| MASTERCARD 3DS2     | 5426064000424979 | Any three digits | Any future date |
| VISA 3DS1           | 4122857790340234 | Any three digits | Any future date |
| VISA 3DS2 (Decline) | 4319799988887738 | Any three digits | Any future date |
