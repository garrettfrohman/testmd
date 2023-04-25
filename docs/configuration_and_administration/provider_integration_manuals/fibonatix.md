--- 
id: "fibonatix" 
title: "Fibonatix"
hide_title: "true"
---
 
![](/img/providers/logos/fibonatix.png)

# Fibonatix

## About
The Fibonatix is a credit card provider that offers deposits, refunds. Fibonatix is a provider that is popular for Binary Forex customers.

| Provider Name                | Fibonatix                                                                       |
|------------------------------|---------------------------------------------------------------------------------|
| Link                         | [https://fibonatix.com](https://fibonatix.com)                                  |
| Classification               | Debit/Credit Card Processor                                                     |
| Regions                      | `International`                                                                 |
| Currencies                   | Please check directly with the provider regarding what currencies are supported |
| Methods/PaymentTxTypes       | `CreditcardDeposit`<br/> `Refund`                                               |
| PaymentIQ Configuration File | `FibonatixConfig`                                                               |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.fibonatix.FibonatixConfig>
  <enabled>true</enabled>
  <useViqProxy>true</useViqProxy>
  <accounts>
    <entry>
      <string>N3DS</string>
      <account>
        <username>??</username>
        <secretKey>??</secretKey>
        <groupId>??</groupId>
      </account>
    </entry>
    <entry>
      <string>3DS</string>
      <account>
        <username>??</username>
        <secretKey>??</secretKey>
        <groupId>??</groupId>
        <useTokenId>true</useTokenId>
        <use3Dsecure>true</use3Dsecure>
      </account>
    </entry>
  </accounts>
  <testMode>false</testMode>
  <defaultDescriptor>Merchant ref-id ${ptx.txRefId}</defaultDescriptor>
  <stateMappings>
    <stateMapping>
      <countryCode>US</countryCode><name>California</name><isDefault>true</isDefault><code>CA</code>
    </stateMapping>
  </stateMappings>
  <statusPollIntervalInSeconds>5</statusPollIntervalInSeconds>
  <maxStatusPollInSeconds>40</maxStatusPollInSeconds>
</com.devcode.paymentiq.integration.fibonatix.FibonatixConfig>
```
</details>

### Attributes

| PaymentIQ Configuration     | Description                                                                                                                                                                                                                                                     |
|-----------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| username                    | Is provided by Fibonatix (This is the api username)                                                                                                                                                                                                             |
| secretkey                   | Used for checking against fraud (md5 checks). Provided by Fibonatix                                                                                                                                                                                             |
| groupId                     | A groupid is N3DS or 3DS and also for different currencies. Ex: Our test groupId 176 is for N3DS and 175 3DS for the currency USD.                                                                                                                              |
| useTokenId                  | Used when want to use recurring transactions. We will store a token from Fibonatix and use that instead of the cc info.                                                                                                                                         |
| showState                   | Regex of country codes when to include the state parameter. Default is `USA|US|CAN|CA|AUS|AU`                                                                                                                                                                   |
| stateMapping                | A mapping of country code, name of state to a code. You can also set a state code as default. That will be used in a case of not found                                                                                                                          |
| statusPollIntervalInSeconds | Defines in seconds in witch interval we poll the status api. The problem with Fibonatix is that they are doing all calls async so we have to wait for fibonatix to process the payment and then return with the result. Default is 3 (Recommended by Fibonatix) |

## Example Routing Rule

![](/img/providers/routing/fibonatix.png)

## Test Information

### Test accounts

- Only for USD 
Fibonatix has a wide variety of creditcards. The outcome of the transaction can be decided by changing the cvv2 (cvc) code. 

[http://doc.fibonatix.com/integration_helpers/test_card_data.html](http://doc.fibonatix.com/integration_helpers/test_card_data.html)

| Card Brand | Account          | CVV | Expiry date |
|------------|------------------|-----|-------------|
| VISA       | 4444444444444448 | Any | Any         |
| MASTERCARD | 5555555555555557 | Any | Any         |