--- 
id: "sirenpay" 
title: "SirenPay"
hide_title: "true"
---
 
![](/img/providers/logos/sirenpay.png)

# SirenPay

## About
Siren Holdings Pte Ltd is a dynamic payments consultancy practice based in Singapore specialising in PayTech and FinTech.

| Provider Name                | SirenPay                                                      |
|------------------------------|---------------------------------------------------------------|
| Link                         | [https://www.sirenpay.sg/](https://www.sirenpay.sg/)          |
| Classification               | Debit/Credit Card Processor, Online Banking                   |
| Regions                      | `Japan`,`Asia`,`Europe`                                       |
| Currencies                   | `USD`, `JPY`                                                  |
| Methods/PaymentTxTypes       | `WebRedirectDeposit` <br/> `CreditcardDeposit` <br/> `Refund` |
| PaymentIQ Configuration File | `SirenPayConfig`                                              |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.sirenpay.SirenPayConfig>
    <enabled>true</enabled>
    <useViqProxy>true</useViqProxy>
    <notifyUser>false</notifyUser>
    <accounts>
        <entry>
            <string>DEFAULT</string>
            <account>
                <secretKey>??</secretKey><!--merchant_secret-->
                <apiToken>??</apiToken>
                <supportedCurrencies>USD|EUR</supportedCurrencies>
                <storeLocationId>+08:00</storeLocationId><!--Timezone-->
            </account>
        </entry>
    </accounts>
    <testMode>true</testMode>
    <defaultDescriptor>DevCode payment</defaultDescriptor>
</com.devcode.paymentiq.integration.sirenpay.SirenPayConfig>


```

</details>

### Attributes

| Attribute           | Description                          |
|---------------------|--------------------------------------|
| secretKey           | merchant_secret provided by SirenPay |
| supportedCurrencies | provided by SirenPay                 |

### Notes

- Configure required `WEBREDIRECT` service(s) in `MerchantConfig`:

```xml
<entry>
    <string>WEBREDIRECT</string>
    <string>SIRENPAY</string>
</entry>
```
- Enable required payment method(s) in PIQ BO (**Rules > Payment Methods**) e.g. WEBREDIRECT-SIRENPAY


## Disable user notifications

You can tell SirenPay to not send a notification by setting `<notifyUser>false</notifyUser>` in the SirenPayConfig on a "root" level.

## Example Routing Rule

![](/img/providers/routing/sirenpay.png)

## Test Information

### AMEX

Credit Card Number: 4111 1111 1111 1111

Expiration Date: Any future date

CVN: 123 

### UNIONPAY TEST DATA

Credit Card Number: 8171 9999 2766 0000

Mobile Phone: Any future date

CVN2: 1234

Expiration Date: 1234

SMS Code on PC: 1234

SMS Code on Mobile: 1234
