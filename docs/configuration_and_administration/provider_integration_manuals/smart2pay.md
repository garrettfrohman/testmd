--- 
id: "smart2pay" 
title: "Smart2Pay"
hide_title: "true"
---
 
![](/img/providers/logos/smart2pay.png)

# Smart2Pay

## About
Smart2Pay is a payment provider offering different payment options globally.

| Provider Name                | Smart2Pay                                              |
|------------------------------|--------------------------------------------------------|
| Link                         | [https://smart2pay.com/en/](https://smart2pay.com/en/) |
| Classification               | Debit/Credit Card, Wallet, Bank Processor              |
| Regions                      | International                                          |
| Currencies                   | `USD`, `EUR`                                           |
| Methods/PaymentTxTypes       | `WebRedirectDeposit`                                   |
| PaymentIQ Configuration File | `Smart2PayConfig`                                      |

### Supported APMs (services)

| Method ID | APM               | PIQ Service        |
|-----------|-------------------|--------------------|
| 1         | Bank Transfer     | FAST_BANK_TRANSFER |
| 1043      | Danske            | DANSKE             |
| 5         | EPS               | EPS                |
| 65        | Finnish Banks     | FINNISH_BANKS      |
| 20        | Multibanco SIBS   | MULTIBANCO_SIBS    |
| 1042      | Nordea            | NORDEA             |
| 1041      | OP-Pohjola        | OP_POHJOLA         |
| 9         | Pay Now           | PAY_NOW            |
| 1003      | Qiwi Wallet       | QIWI               |
| 49        | ToditoCash        | TODITO_CASH        |
| 81        | WebMoney Transfer | WEBMONEY           |
| 74        | Yandex Money      | YANDEX             |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.smart2pay.Smart2PayConfig>
  <enabled>true</enabled>
  <accounts>
    <entry>
      <string>DEFAULT</string>
      <account>
        <siteId>??</siteId>
        <apiKey>??</apiKey>
        <supportedCurrencies>EUR</supportedCurrencies>
        <language>en</language>
      </account>
    </entry>
  </accounts>
  <testMode>true</testMode>
  <container>window</container>
  <defaultDescriptor>Bambora payment ${ptx.txRefId}</defaultDescriptor>
</com.devcode.paymentiq.integration.smart2pay.Smart2PayConfig>
```
</details>

### Attributes

| Attribute      | Description                                                                                      |
|----------------|--------------------------------------------------------------------------------------------------|
| account.siteId | Corresponds to Site ID from Smart2Pay. It is used like a username in Basic Authorization header. |
| account.apiKey | Corresponds to API Key from Smart2Pay. It is used like a password in Basic Authorization header. |

### NOTES 
- Site ID and API Key can be found in Smart2Pay back office (see below).

### Callback URL

Callback URL should be configured in Smart2Pay back office.

![](/img/providers/smart2pay_bo.png)

#### TEST: 
https://test-api.paymentiq.io/paymentiq/api/smart2pay/callback

#### PRODUCTION: 
https://api.paymentiq.io/paymentiq/api/smart2pay/callback

## Example Routing Rule
![](/img/providers/routing/smart2pay.png)

## Test Information

To test Finnish Banks please use [test data](https://docs.smart2pay.com/s2p_testdata_65/)
