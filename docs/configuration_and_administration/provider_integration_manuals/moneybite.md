--- 
id: "moneybite" 
title: "Moneybite"
hide_title: "true"
---
 
![](/img/providers/logos/moneybite.png)

# Moneybite

## About
Moneybite enables merchants to accept cryptocurrencies as customer payments. Crypto can be instantly converted to fiat, eliminating all volatility risk. At the time of writing only BTC is supported with other currencies to be followed (please contact Moneybite for the latest list of supported currencies).

| Provider Name                | Moneybite                                                                       |
|------------------------------|---------------------------------------------------------------------------------|
| Link                         | [https://moneybite.com](https://moneybite.com)                                  |
| Classification               | Cryptocurrency                                                                  |
| Regions                      | `International`                                                                 |
| Currencies                   | Please check directly with the provider regarding what currencies are supported |
| Methods/PaymentTxTypes       | `CryptoCurrencyDeposit` `WebRedirectDeposit` <br/> `CryptoCurrencyWithdrawal`   |
| PaymentIQ Configuration File | `MoneybiteConfig`                                                               |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.moneybite.MoneybiteConfig>
  <enabled>true</enabled>
  <!-- <failOverpaidTx>true</failOverpaidTx> -->
  <accounts>
    <entry>
      <string>default</string>
      <account>
        <apiKey>???</apiKey>
        <secretKey>???</secretKey>
        <merchantName>???</merchantName>
        <!-- <supportedCurrencies>???</supportedCurrencies> -->
        <!-- <sourceAccount>CRYPTO</sourceAccount> -->
      </account>
    </entry>
  </accounts>
</com.devcode.paymentiq.integration.moneybite.MoneybiteConfig>
```
</details>

### Attributes

| Attribute      | Description                                                                                                                                                                               |
|----------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| apiKey         | Correspond to Key provided by Moneybite                                                                                                                                                   |
| secretKey      | Correspond to Secret provided by Moneybite                                                                                                                                                |
| sourceAccount  | Optional parameter. Set to "CRYPTO" if the merchant wants to use an existing Moneybite crypto account, instead of converting to crypto from a fiat account, when doing withdrawal(payout) |
| failOverpaidTx | Optional parameter. Set to true if the merchant wants to set a deposit that has been fully paid but additional funds were received (overpaid) to state INCONSISTENT instead of SUCCESS    |

**Important notes:** 
- If the user deposits a lower crypto currency amount than in the original transaction, Moneybite will wait for 15 minutes giving the user a chance to complete the amount, after that the transaction will be considered timed out (Status ERR_DECLINED_EXPIRED). At this point any lower amount received by the merchant are kept in the merchants crypto account and are claimable by the customer (this can be settled between the merchant and customer without involving PaymentIQ).  
- If the user deposits a higher crypto amount, the default behavior is that the transaction is considered successful. Any excess funds are kept in the merchants crypto account and are claimable by the customer.  
  To set overpaid transactions to state INCONSISTENT instead, the merchant can set the optional MoneybiteConfig parameter ``failOverpaidTx`` to true  
- The merchant has the option to use a crypto account on Moneybite to receive funds in crypto, without converting to fiat, and to payout in crypto without first converting from fiat.  
  To keep the funds received in crypto the merchant must set the config on Moneybite called "Percentage Kept in BTC".  
  And to payout from the crypto account directly the merchant must set the optional parameter ``sourceAccount`` in MoneybiteConfig to 'CRYPTO'.    

## Example Routing Rule
![](/img/providers/routing/moneybite.png)

## Test Information
At the moment its not possible to test this provider in test.
