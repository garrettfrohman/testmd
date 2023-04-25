--- 
id: "coincorner" 
title: "CoinCorner"
hide_title: "true"
---
 
![](/img/providers/logos/coincorner.png)

# CoinCorner

## About
CoinCorner was founded in 2014 with the aim of making buying Bitcoin easy in the UK. A
designated business which is registered with the Isle of Man’s Financial Services Authority,
the company has grown to process millions of customer transactions in more than 45
countries worldwide.

| Provider Name                | CoinCorner                                                 |
|------------------------------|------------------------------------------------------------|
| Link                         | [https://www.coincorner.com/](https://www.coincorner.com/) |
| Classification               | Crypto Currency                                            |
| Regions                      | `International`                                            |
| Currencies                   | `GBP`, `EUR`, `USD`                                        |
| Methods/PaymentTxTypes       | `CryptoCurrencyDeposit` <br/> `CryptoCurrencyWithdrawal`   |
| PaymentIQ Configuration File | `CoinCornerConfig`                                         |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.coincorner.CoinCornerConfig>
  <enabled>true</enabled>
  <accounts>
    <entry>
     <string>default</string>
     <account>
        <merchantId>???</merchantId> 
        <secretKey>???</secretKey>  
        <apiKey>???</apiKey> 
        <supportedCurrencies>EUR|USD|GBP</supportedCurrencies>
     </account>
    </entry>
  </accounts>
  <testMode>true</testMode>
  <settleCurrency>EUR</settleCurrency>
  <ForceBuy>false</ForceBuy>
  <ForceBuyCurrency>EUR</ForceBuyCurrency>
</com.devcode.paymentiq.integration.coincorner.CoinCornerConfig>
```
</details>

### Attributes

| Attribute        | Description                                                                                                           |
|------------------|-----------------------------------------------------------------------------------------------------------------------|
| merchantId       | Created in CoinCorner backoffice as user Id                                                                           |
| secretKey        | Created in CoinCorner backoffice as Secret                                                                            |
| apiKey           | Created in Coindirect Backoffice as ApiKey                                                                            |
| settleCurrency   | Currency that the order will be settled in, the merchant receives whatever is specified here                          |
| ForceBuy         | set to true if you want to buy the BTC needed if your account doesn't have enough already for withdrawal transactions |
| ForceBuyCurrency | if force buy is set to true, enter the fiat currency you wish to force buy with (ex: GBP, EUR)                        |


## Example Routing Rule
![](/img/providers/routing/coincorner.png)

## Test Information
To test deposit/withdrawal select Cryptocurrency payment option in PaymentIQ Cashier, 
fill in any amount and follow the instruction after being redirected. Ask Coincorner support team for a wallet address
to test withdrawals.

One  will need to download a Testnet wallet and get some free testnet coins from a faucet. Recommended apps/sites to use for this can be seen below.

   - Android
        [https://play.google.com/store/apps/details?id=de.schildbach.wallet_test&hl=en](https://play.google.com/store/apps/details?id=de.schildbach.wallet_test&hl=en) 
   - iOS
        [https://apps.apple.com/us/app/copay-bitcoin-wallet/id951330296](https://apps.apple.com/us/app/copay-bitcoin-wallet/id951330296) 
   - Testnet Faucets
        [https://coinfaucet.eu/en/btc-testnet/](https://coinfaucet.eu/en/btc-testnet/) <br/>
        [https://bitcoinfaucet.uo1.net/](https://bitcoinfaucet.uo1.net/)
        
One needs test Bitcoins as well from CoinCorner to be able to test.

