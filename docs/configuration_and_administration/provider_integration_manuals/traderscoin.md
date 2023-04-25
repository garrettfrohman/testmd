--- 
id: "traderscoin" 
title: "TradersCoin"
hide_title: "true"
---
 
![](/img/providers/logos/traderscoin.png)

# TradersCoin

## About
TradersCoin is a payment provider offering creditcard and bank deposit operations via redirection to the provider page. Bank withdrawal can be done manually.<br/>
Each merchant will have their own keys and request URL (payment page) that will be provided by the provider.

| Provider Name                | TradersCoin                                                                                                                                                                                                                                                                    |
|------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Link                         | [https://www.traderscoin.io/](https://www.traderscoin.io/)                                                                                                                                                                                                                     |
| Classification               | Debit/Credit Card Processor, Online/Manual Banking                                                                                                                                                                                                                             |
| Regions                      | For creditcard operations provider blocks USA, Turkey.<br/>Bank operations can be made in China, Indonesia, Malaysia, Thailand, Vietnam in local currency converted to `USD`.                                                                                                  |
| Currencies                   | `USD`, `EUR`, `GBP`                                                                                                                                                                                                                                                            |
| Min/Max amount               | 10.00/5000.00 for each currency (`USD`, `EUR`, `GBP`).<br/>Asia online banking:<br/>China - 100/50,000 CNY<br/>Thailand - 500/500,000 THB<br/>Malaysia - 50/50,000 MYR<br/>Vietnam - 100,000/300M VND<br/>Indonesia - 200,000/200M IDR<br/>(Local currencies converted to USD) |
| Methods/PaymentTxTypes       | `WebRedirectDeposit`                                                                                                                                                                                                                                                           |
| PaymentIQ Configuration File | `TradersCoinConfig`                                                                                                                                                                                                                                                            |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.traderscoin.TradersCoinConfig>
  <enabled>true</enabled>
  <useViqProxy>false</useViqProxy>
  <accounts>
    <entry>
      <string>DEFAULT</string>
      <account>
        <apiKey>??</apiKey><!--API Key-->
        <secretKey>??</secretKey><!--API Secret-->
        <supportedCurrencies>USD|EUR|GBP</supportedCurrencies>
        <serviceEndpoint>??</serviceEndpoint><!--Payment page URL, unique for each merchant-->
      </account>
    </entry>
  </accounts>
  <container>window</container>
  <testMode>false</testMode>
  <version>1.0</version>
  <defaultDescriptor>Bambora Payment: ${ptx.txRefId}</defaultDescriptor>
</com.devcode.paymentiq.integration.traderscoin.TradersCoinConfig>

```
</details>

### Attributes

| Attribute       | Description                                                                                                        |
|-----------------|--------------------------------------------------------------------------------------------------------------------|
| apiKey          | Corresponds to *API Key* from TradersCoin. It is a required parameter in each request that is sent to TradersCoin. |
| secretKey       | Corresponds to *API Secret* from TradersCoin. It is used to sign requests that are sent to TradersCoin.            |
| serviceEndpoint | Corresponds to payment page URL, unique for each merchant.                                                         |

## Example Routing Rule

![](/img/providers/routing/traderscoin.png)

## Test Information

Testing can be made using real cards only.

Payment is not failed immediately at provider side (final payment notification will be sent in 1 hour). It is due to customer can try using different card if one card doesn't work.<br/>
In case of successful payment, its status will be updated right after payment is completed (it depends on customer).

User initiates payment at PaymentIQ Cashier by specifying amount only. Then he/she is redirected to

![](/img/providers/traderscoin01.png)

After CONTINUE button is pressed the user is redirected to the page where card details should be specified

![](/img/providers/traderscoin02.png)

After "Complete order" is pressed the user is redirected to

![](/img/providers/traderscoin03.png)

After pressing "Continue" button the user will be redirected to 3DS authentication window where PIN code should be specified

![](/img/providers/traderscoin04.png)

After "Submit" button is pressed and 3DS authentication is completed the user will be redirected to receipt page showing tx status.
