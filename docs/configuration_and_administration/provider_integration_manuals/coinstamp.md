--- 
id: "coinstamp" 
title: "Coinstamp"
hide_title: "true"
---
 
![](/img/providers/logos/coinstamp.png)

# Coinstamp

## About
Coinstamp provides CryptoCurrency deposits for multiple currencies and countries. 

| Provider Name                | Coinstamp                                          |
|------------------------------|----------------------------------------------------|
| Link                         | [https://nordikcoin.com/](https://nordikcoin.com/) |
| Classification               | Crypto Currency                                    |
| Regions                      | `Global`                                           |
| Currencies                   | `EUR`, `USD`, `NOK`, `DKK`, `SEK`, `JPY`, `INR`    |
| Methods/PaymentTxTypes       | `CryptoCurrencyDeposit`                            |
| PaymentIQ Configuration File | `CoinstampConfig`                                  |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.coinstamp.CoinstampConfig>
  <enabled>true</enabled>
  <accounts>
    <entry>
      <string>default</string>
      <account>
        <merchantId>??</merchantId>
        <apiKey>??</apiKey>
        <!-- username and password are for test env only -->
        <username>??</username>
        <password>??</password>
      </account>
    </entry>
  </accounts>
  <container>window</container>
</com.devcode.paymentiq.integration.coinstamp.CoinstampConfig>
```

</details>

### Attributes

| Attribute          | Description                                                                                                            |
|--------------------|------------------------------------------------------------------------------------------------------------------------|
| account.merchantId | An individual ID provided by Coinstamp for each merchant - it is being sent over as a part of the url for each request |
| account.apiKey     | Provided by Coinstamp,  used to encode and decode signatures for requests and callbacks                                |
| account.username   | Provided by Coinstamp, used in request headers for sandbox only, not required for live transactions                    |
| account.password   | Provided by Coinstamp, used in request headers for sandbox only, not required for live transactions                    |

## Provider Configuration

1. Run PaymentIQ and add the aforementioned CoinstampConfig under Admin -> Configuration.
2. Add routing rules - see example below.
3. Enable CRYPTOCURRENCY-COINSTAMP in Rules -> Payment methods.

## Example Routing Rule

![](/img/providers/routing/coinstamp.png)

## Transaction Flow

1. The user enters the amount along with the account number, and the email address in the Cashier.
2. PaymentIQ sends a deposit request to the Coinstamp
3. Coinstamp sends back a response with the url that the user is redirected.
4. Once the user has completed the transaction Coinstamp sends a callback to PaymentIQ. PaymentIQ validates the callback's 
   signature and the amount sent over in the callback and updates the status of the transaction status accordingly to the status
   received from Coinstamp.

## Test Information

For testing, you will need the following credentials:

- merchantId
- apiKey
- username
- password

Please contact Coinstamp tech support to obtain them.
