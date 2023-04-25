--- 
id: "ipay" 
title: "IPay"
hide_title: "true"
---
 
![](/img/providers/logos/ipay.png)

# IPay

## About
Quickly and safely. IPay was created to offer online merchants a new means of online payment support for their clients. They aim to provide a payment process that is easily integrated into ecommerce sites with little disruption to business, as well as a thoroughly secure payment platform for clients and merchants alike, eliminating the risk of fraud and chargebacks. IPay provides a convenient means for South African online shoppers to purchase goods and services from your ecommerce store.

| Provider Name                | IPay                                                                            |
|------------------------------|---------------------------------------------------------------------------------|
| Link                         | [https://i-pay.co.za/](https://i-pay.co.za/)                                    |
| Classification               | Online Banking                                                                  |
| Regions                      | `South Africa`                                                                  |
| Currencies                   | Please check directly with the provider regarding what currencies are supported |
| Methods/PaymentTxTypes       | `BankDeposit`                                                                   |
| PaymentIQ Configuration File | `IPayConfig`                                                                    |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.ipay.IPayConfig>
  <enabled>true</enabled>
  <useViqProxy>false</useViqProxy>
  <accounts>
    <entry>
      <string>default</string>
      <account>
        <siteId>??</siteId>
        <secretKey>??</secretKey>
        <merchantKeyId>??</merchantKeyId>
        <supportedCurrencies>ZAR</supportedCurrencies>
      </account>
    </entry>
  </accounts>
  <!--<defaultDescriptor>e.g Brand Name</defaultDescriptor> default to txRefId if not set -->
  <testMode>false</testMode>
</com.devcode.paymentiq.integration.ipay.IPayConfig>
```

</details>

### Attributes

| PaymentIQ Configuration                                                          | Provider Credential       |
|----------------------------------------------------------------------------------|---------------------------|
| siteId                                                                           | Site Code                 |
| secretKey                                                                        | Secret Key (Private Key)  |
| merchantKeyId                                                                    | Merchant Key Id (API Key) |
| defaultDescriptor (will be populated with transaction reference id if   not set) | Bank Reference            |

## Example Routing Rule
![](/img/providers/routing/ipay.png)
## Test Information

The user has to have country code ZAF (South Africa) and currency code ZAR
