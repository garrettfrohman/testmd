--- 
id: "utorg" 
title: "Utorg"
hide_title: "true"
---
 
![](/img/providers/logos/utorglogo.png)

# Utorg

## About
Utorg is an EU-based company that holds a license for providing a virtual currency service, in particular exchanging a virtual currency against a fiat currency, virtual currency wallet service, exchanging a virtual currency against a virtual currency.

As of the 27th of Sep 2021, UTorg only supports BTC, ETH, and LTC.<br/>
Please ask the provider directly regarding any questions about other cryptocurrencies.

| Provider Name                | Utorg                                                                                                       |
|------------------------------|-------------------------------------------------------------------------------------------------------------|
| Link                         | [https://utorg.pro/](https://utorg.pro/)                                                                    |
| Classification               | Crypto Currency                                                                                             |
| Regions                      | `International`                                                                                             |
| Currencies                   | `EUR` `USD` `GBP` `SEK` `NOK` `RUB` `PLN` `CAD` `ZAR` `DKK` `AUD` `NZD` `INR` `MXN` `CZK` `TRY` `MYR` `BRL` |
| Methods/PaymentTxTypes       | `CryptoCurrencyDeposit` `WebRedirectDeposit`                                                                |
| PaymentIQ Configuration File | `UtorgConfig`                                                                                               |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
  <com.devcode.paymentiq.integration.utorg.UtorgConfig>
  <enabled>true</enabled>
  <accounts>
    <entry>
     <string>default</string>
     <account>
        <supportedCurrencies>EUR|USD|GBP|NOK|SEK|RUB|PLN|RUB|CAD|ZAR|DKK|AUD|NZD|INR|MXN|CZK|TRY|MYR|BRL</supportedCurrencies>
        <merchantCode>???</merchantCode>
        <merchantKeyId>???</merchantKeyId> <!--CoinsPaid Key -->
       <secretKey>???</secretKey> <!-- CoinsPaid Secret -->
       <container>window</container>
     </account>
    </entry>
  </accounts>
  <testMode>true</testMode>
  <orderType>FIAT_TO_CRYPTO</orderType>
</com.devcode.paymentiq.integration.utorg.UtorgConfig>
```


</details>

### Attributes

| Attribute     | Description                                                                                                              |
|---------------|--------------------------------------------------------------------------------------------------------------------------|
| merchantCode  | X-AUTH-SID issued by Utorg                                                                                               |
| orderType     | Type of the order, the only one supported by Utorg for now is "FIAT_TO_CRYPTO"                                           |
| merchantKeyId | CoinsPaid key, Created in CoinsPaid Backoffice in the Api keys section as key (see CoinsPaid API doc for more details)   |
| secretKey     | CoinsPaid Secret,  Generated in CoinsPaid Backoffice alongside with the Api key (see CoinsPaid API doc for more details) |

## Example Routing Rules

![](/img/providers/routing/utorgrouting.png)

## Test Information

Before start testing, merchant needs to contact CoinsPaid to create a sandbox merchant account where we will generate crypto wallet addresses.
Once you have your sandbox account, you will be able to create API keys and authenticate with CoinsPaid API using your credentials.

After adding CoinsPaid credentials in the UtorgConfig file, choose either CryptoCurrency or BTC service deposit type in the cashier, initiate a deposit with any amount, then follow the instructions after being redirected.

Test cards:

Once you have been redirected to the Utorg payment page, use any valid card (Visa/MC). Utorg recommends  [https://www.bincodes.com/random-creditcard-generator/](https://www.bincodes.com/random-creditcard-generator/) 




