--- 
id: "easyeft" 
title: "EasyEFT"
hide_title: "true"
---
 
![](/img/providers/logos/easyeft.png)

# EasyEFT

## About
Quickly and safely. EasyEFT was created to offer online merchants a new means of online payment support for their clients. They aim to provide a payment process that is easily integrated into ecommerce sites with little disruption to business, as well as a thoroughly secure payment platform for clients and merchants alike, eliminating the risk of fraud and chargebacks. EasyEFT provides a convenient means for South African online shoppers to purchase goods and services from your ecommerce store.

| Provider Name                | EasyEFT                                          |
|------------------------------|--------------------------------------------------|
| Link                         | [https://easyeft.co.za/](https://easyeft.co.za/) |
| Classification               | Online Banking                                   |
| Regions                      | `South Africa`                                   |
| Currencies                   | `ZAR`                                            |
| Methods/PaymentTxTypes       | `BankDeposit`                                    |
| PaymentIQ Configuration File | `EasyEFTConfig`                                  |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>

<br/>

```xml
<com.devcode.paymentiq.integration.easyeft.EasyEftConfig>
  <enabled>true</enabled>
  <useViqProxy>false</useViqProxy>
  <accounts>
    <entry>
      <string>default</string>
      <account>
        <siteId>??</siteId> <!-- Site code -->
        <secretKey>??</secretKey> <!-- Private key -->
        <merchantKeyId>??</merchantKeyId> <!-- API key -->
        <supportedCurrencies>ZAR</supportedCurrencies>
      </account>
    </entry>
  </accounts>
  <!--<defaultDescriptor>e.g Brand Name</defaultDescriptor> defaults to txRefId if not set -->
</com.devcode.paymentiq.integration.easyeft.EasyEftConfig>
```

</details>

### Attributes

| PaymentIQ Configuration                                                        | Provider Credential       |
|--------------------------------------------------------------------------------|---------------------------|
| siteId                                                                         | Site Code                 |
| ZAF(Only supports South African Rand)                                          | Country Code              |
| ZAR (Only supports South Africa)                                               | Currency Code             |
| secretKey                                                                      | Secret Key (Private Key)  |
| merchantKeyId                                                                  | Merchant Key Id (API Key) |
| defaultDescriptor (will be populated with transaction reference id if not set) | Bank Reference            |

## Example Routing Rule
![](/img/providers/routing/easyeft.png)
## Test Information

The user has to have country code ZAF (South Africa) and currency code ZAR