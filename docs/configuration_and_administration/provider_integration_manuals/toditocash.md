--- 
id: "toditocash" 
title: "ToditoCash"
hide_title: "true"
---
 
![](/img/providers/logos/toditocash.png)

# ToditoCash

## About
ToditoCash is a mexican wallet provider offering solutions to pay and receive money with your ToditoCash account.

| Provider Name                | CleanPay                                                   |
|------------------------------|------------------------------------------------------------|
| Link                         | [https://www.toditocash.com/](https://www.toditocash.com/) |
| Classification               | E-Wallet                                                   |
| Regions                      | `Mexico`                                                   |
| Currencies                   | `EUR`, `USD`, `GBP`, `MXN`, `JPY`                          |
| Methods/PaymentTxTypes       | `ToditoDeposit`                                            |
| PaymentIQ Configuration File | `ToditoConfig`                                             |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.todito.ToditoConfig>
  <enabled>true</enabled>
  <accounts>
    <entry>
     <string>default</string>
     <account>
        <apiKey>???</apiKey>
        <supportedCurrencies>EUR|USD|GBP|MXN|JPY</supportedCurrencies>
        <siteId>??</siteId> <!-- sucursalId -->
     </account>
    </entry>
  </accounts>
  <defaultDescriptor>???</defaultDescriptor>
  <testMode>false</testMode>
</com.devcode.paymentiq.integration.todito.ToditoConfig>
```
</details>

### Attributes

| Attribute | Description                                    |
|-----------|------------------------------------------------|
| apiKey    | Provided by ToditoCash. Provided by ToditoCash |
| siteID    | succursalId. Provided by ToditoCash            |

## Example Routing Rules
![](/img/providers/routing/toditoRouting.png)

## Test Information

| account    | nip  |
|------------|------|
| 2622047317 | 3690 |
| 2622047413 | 2580 |
| 2622047517 | 1470 |
| 2622047824 | 1234 |
