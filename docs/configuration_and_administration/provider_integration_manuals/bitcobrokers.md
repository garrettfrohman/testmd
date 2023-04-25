--- 
id: "bitcobrokers" 
title: "BitcoBrokers"
hide_title: "true"
---
 
![](/img/providers/logos/bitcobrokers.png)

# BitcoBrokers

## About
BitcoBrokers is a cryptocurrency exchange platform. They have integrated with various payment service providers to allow to buy cryptocurrencies with credit cards. 

| Provider Name                | BitcoBrokers                                                                                      |
|------------------------------|---------------------------------------------------------------------------------------------------|
| Link                         | [https://bitcobrokers.com/](https://bitcobrokers.com/)                                            |
| Classification               | Crypto Currency                                                                                   |
| Regions                      | `International`                                                                                   |
| Currencies                   | `EUR`, `USD`, `GBP`, `ZAR`, `IDR`, `BRL`, `AED`, `AUD`. More currencies can be added upon request |
| Methods/PaymentTxTypes       | `CryptoCurrencyDeposit`                                                                           |
| PaymentIQ Configuration File | `BitcoBrokersConfig`                                                                              |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.bitcobrokers.BitcoBrokersConfig>
 <enabled>true</enabled>
 <accounts>
   <entry>
    <string>default</string>
    <account>
       <supportedCurrencies>EUR|USD|GBP|ZAR|IDR|BRL|AED|AUD</supportedCurrencies>
    </account>
   </entry>
 </accounts>
<defaultDescriptor>??</defaultDescriptor>
</com.devcode.paymentiq.integration.bitcobrokers.BitcoBrokersConfig>
```

</details>

### Attributes

| Attribute         | Description                                                           |
|-------------------|-----------------------------------------------------------------------|
| defaultDescriptor | Corresponds to the "label" parameter that will be sent in the request |

## Example Routing Rule
-

## Test Information

FIBONATIX E-Commerce test cards are available here :

[http://doc.fibonatix.com/integration_helpers/test_card_data.html](http://doc.fibonatix.com/integration_helpers/test_card_data.html)


