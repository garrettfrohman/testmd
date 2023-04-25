--- 
id: "altapay"
title: "AltaPay"
hide_title: "true"
---

![](/img/providers/logos/altapay.png)

# AltaPay

## About
AltaPay offers credit card deposits, refunds and transaction management using auth/capture/void.

| Provider Name                | AltaPay                                                                                    |
|------------------------------|--------------------------------------------------------------------------------------------|
| Link                         | [https://altapay.com/](https://altapay.com/)                                               |
| Classification               | Debit/Credit Card Processor                                                                |
| Regions                      | `International`                                                                            |
| Currencies                   | Please check directly with the provider regarding what currencies are supported            |
| Methods/PaymentTxTypes       | `CreditcardDeposit` <br/> `Refund` <br/> `Capture` <br/> `Void` <br/> `WebRedirectDeposit` |
| PaymentIQ Configuration File | `AltaPayConfig`                                                                            |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.altapay.AltaPayConfig>
    <enabled>true</enabled>
    <useViqProxy>true</useViqProxy>
    <accounts>
        <entry>
            <string>default</string>
            <account>
                <username>???</username>
                <password>???</password>
                <terminal>???</terminal>
                <supportedCurrencies>XXX|YYY</supportedCurrencies>
            </account>
        </entry>
        <entry>
            <string>recurring</string>
            <account>
                <username>???</username>
                <password>???</password>
                <terminal>???</terminal>
                <useTokenId>true</useTokenId>
                <cardOnFileType>unscheduled</cardOnFileType>
                <supportedCurrencies>XXX|YYY</supportedCurrencies>
            </account>
        </entry>
    </accounts>
</com.devcode.paymentiq.integration.altapay.AltaPayConfig>
```

</details>

### Attributes

| Attribute      | Description                                                                                    |
|----------------|------------------------------------------------------------------------------------------------|
| username       | Provided by AltaPay                                                                            |
| password       | Provided by AltaPay                                                                            |
| terminal       | The title of the terminal to use, found in "Home -> Terminal Settings" in AltaPay's backoffice |
| useTokenId     | Enables recurring feature.                                                                     |
| cardOnFileType | Defines the type of recurring payments. Possible values: 'unscheduled' or 'recurring'          |

## Example Routing Rule
![](/img/providers/routing/altapay.png)

## Test Information
See AltaPay's testing page for all available test cases: [https://documentation.altapay.com/Content/Ecom/Testing/1%20-Credit%20card%20payments.htm](https://documentation.altapay.com/Content/Ecom/Testing/1%20-Credit%20card%20payments.htm)

| Card             | Amount | Type |
|------------------|--------|------|
| 4130000000000468 | 4.68   | 3DS1 |
| 4571000000000621 | Any    | 3DS2 |

