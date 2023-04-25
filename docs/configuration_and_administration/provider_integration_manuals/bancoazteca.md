--- 
id: "bancoazteca" 
title: "Banco Azteca"
hide_title: "true"
---

![](/img/providers/logos/bancoazteca.png)

# Banco Azteca

## About
Banco Azteca is a payment provider offering 3DS/N3DS Charge, Cancel, Refund, and Reversal in Mexico only.<br/>
Cancel can be made within 24 hours after original payment has been made but before 11:00 PM Mexico time. After 11:00 PM Mexico time all payments can be refunded only.<br/>
Reversal can only be made for those payments that failed with a specific error code e.g. "08".<br/>
Banco Azteca doesn't support neither callback notifications, nor status check.

| Provider Name                | Banco Azteca                                                       |
|------------------------------|--------------------------------------------------------------------|
| Link                         | [https://www.bancoazteca.com.mx/](https://www.bancoazteca.com.mx/) |
| Classification               | Debit/Credit Card Processor                                        |
| Supported Countries          | Mexico                                                             |
| Currencies                   | `MXN`                                                              |
| Methods/PaymentTxTypes       | `CreditcardDeposit`<br/>`Refund`<br/>`Reversal`                    |  
| PaymentIQ Configuration File | `BancoAztecaConfig`                                                |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.bancoazteca.BancoAztecaConfig>
  <enabled>true</enabled>
  <testMode>false</testMode>
  <useViqProxy>true</useViqProxy>
  <accounts>
    <entry>
      <string>DEFAULT</string>
      <account>
        <username>{consumer.key}</username>
        <password>{consumer.secret}</password>
        <merchantId>{merchant.id}</merchantId>
        <merchantNumber>{affiliation.number}</merchantNumber>
        <commerceId>{commerce.id}</commerceId>
        <terminalId>{terminal.id}</terminalId>
        <defaultDescriptor>{order.description}</defaultDescriptor>
        <use3Dsecure>true</use3Dsecure>
        <supportedCurrencies>MXN</supportedCurrencies>
        <httpClientConfigEntry>
          <viqProxy>false</viqProxy>
        </httpClientConfigEntry>
      </account>
    </entry>
  </accounts>
  <uniqueRSAKeysPerRequest>false</uniqueRSAKeysPerRequest><!--One RSA key pair for one payment-->
  <container>iframe</container>
  <width>800</width>
  <height>800</height>
</com.devcode.paymentiq.integration.bancoazteca.BancoAztecaConfig>
```
</details>

### Attributes
| Attribute                 | Description                                                 |
|---------------------------|-------------------------------------------------------------|
| account.username          | Corresponds to the consumer key from the Banco Azteca       |
| account.password          | Corresponds to the consumer secret from the Banco Azteca    |
| account.merchantId        | Corresponds to the merchant ID from the Banco Azteca        |
| account.merchantNumber    | Corresponds to the affiliation number from the Banco Azteca |
| account.commerceId        | Corresponds to the commerce ID from the Banco Azteca        |
| account.terminalId        | Corresponds to the terminal ID from the Banco Azteca        |
| account.defaultDescriptor | Corresponds to the order description (optional)             |
| uniqueRSAKeysPerRequest   | `true` - request new set of RSA public-private keys for each request in scope of one payment; `false` - request just one set of RSA public-private keys for all the requests in scope of one payment. Request keys are alive only 3 min. So, if payment could take more then 3min, it is required to set this property to `true`. |

#### Notes
Banco Azteca will provide commerce and terminal IDs, but if they are not provided or merchant has forgotten to specify it in the config, PaymentIQ will send additional request to Banco Azteca in order to get such keys as they are required to do charge.

## Example Routing Rule
![](/img/providers/routing/bancoazteca.png)

## Test Information

Testing can be done on PROD env. using LIVE account and real credit cards (VISA, MASTER CARD) only.
