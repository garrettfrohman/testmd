--- 
id: "finrax" 
title: "Finrax"
hide_title: "true"
---

![](/img/providers/logos/finrax.png)

# Finrax

## About
Finrax Payment Gateway is a solution that enables merchants to accept cryptocurrency payments and initiate withdrawals to customers at ideal exchange rates.<br/>

| Provider Name                | Finrax                                                                                                                                                                                                                                                                          |
|------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Link                         | [https://finrax.com/](https://finrax.com/)                                                                                                                                                                                                                                      |
| API documentation link       | [https://docs.finrax.com/](https://docs.finrax.com/)                                                                                                                                                                                                                            |
| Classification               | Cryptocurrency Processor                                                                                                                                                                                                                                                        |
| Supported Regions            | USA, Europe                                                                                                                                                                                                                                                                     |
| Currencies                   | `ARS`, `AUD`, `BDT`, `BGN`, `BRL`, `CAD`, `CHF`, `CNY`, `CZK`, `DKK`, `EUR`, `GBP`, `HKD`, `HRK`, `HUF`, `IDR`, `ILS`, `INR`, `ISK`, `JPY`, `KRW`, `MXN`, `MYR`, `NGN`, `NOK`, `NZD`, `PEN`, `PHP`, `PLN`, `QAR`, `RON`, `RUB`, `SEK`, `SGD`, `THB`, `TRY`, `USD`, `VND`, `ZAR` |
| Crypto currencies            | `BCH`, `BTC`, `ETH`, `LINK`, `LTC`, `USDC`, `USDT`, `XLM`, `XRP`                                                                                                                                                                                                                |
| Methods/PaymentTxTypes       | `CryptoCurrencyDeposit`<br/> `CryptoCurrencyWithdrawal`                                                                                                                                                                                                                         |
| PaymentIQ Configuration File | `FinraxConfig`                                                                                                                                                                                                                                                                  |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.finrax.FinraxConfig>
  <enabled>true</enabled>
  <testMode>false</testMode>
  <accounts>
    <entry>
      <string>default</string>
      <account> 
        <accountID>{account.accountID}}</accountID>
        <pspPrivateKey>{account.pspPrivateKey}</pspPrivateKey>
        <pspPublicKey>{account.pspPublicKey}</pspPublicKey>
        <supportedCurrencies>EUR|USD|BTC</supportedCurrencies>
        <cryptoCurrency>BTC</cryptoCurrency>  
      </account>
    </entry>
  </accounts>
</com.devcode.paymentiq.integration.finrax.FinraxConfig>

```
</details>

### Attributes

| Attribute                   | Description                                                                            |
|-----------------------------|----------------------------------------------------------------------------------------|
| account.accountID           | Corresponds to the business id from Finrax.                                            |
| account.pspPrivateKey       | Corresponds to the private key from Finrax.                                            |
| account.pspPublicKey        | Corresponds to the public key from Finrax                                              |
| account.supportedCurrencies | Corresponds to the currencies (including crypto) supported by the Provider             |
| account.cryptoCurrency      | Corresponds to the default crypto currency used if none provider by the customer input |

## Example Routing Rule
![](/img/providers/routing/finrax.png)

## Test Information

Testing is supported on prod environment, so property `<testMode>` should be set to `true`.
Testing requires having account in Finrax Dashboard environment (https://dashboard.finrax.com/) which will be topped up by the Finrax.
After getting an account there should be:
1. generated API key
2. generated API secret
3. set up the notification urls for deposits and withdrawals
4. created a Business (so the businessID which corresponds to accountId in PaymentIQ)
5. whitelisted IPs

When testing withdrawal (if no wallet address available) - there should be initiated deposit first, which will provide the wallet address to use for the withdrawal.
Deposit amount should be of a slightly larger value then withdrawal amount (due to blockchain fees).
Also, there is a minimum withdrawal amount threshold for a crypto currency:
[https://finrax.com/onchain-fees](https://finrax.com/onchain-fees)



