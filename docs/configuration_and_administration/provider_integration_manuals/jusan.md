--- 
id: "jusan" 
title: "Jusan"
hide_title: "true"
---

![](/img/providers/logos/jusan.png)

# Jusan

## About
Jusan is a payment provider offering 3DS/N3DS Auth, Sale, Capture, full/partial Refund, Void and Status Check.

Card tokenization is also supported.

Please note that currently only VISA cards can be processed.


| Provider Name                | Jusan                                                                              |
|------------------------------|------------------------------------------------------------------------------------|
| Link                         | [https://jysanbank.kz/en](https://jysanbank.kz/en)                                 |
| Classification               | Debit/Credit Card Processor                                                        |
| Supported Countries          | Kazakhstan and Kyrgyzstan                                                          |
| Currencies                   | `KZT`, `KGS`                                                                       |
| Methods/PaymentTxTypes       | `CreditcardDeposit`<br/>`WebRedirectDeposit`<br/>`Capture`<br/>`Refund`<br/>`Void` |
| PaymentIQ Configuration File | `JusanConfig`                                                                      |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.jusan.JusanConfig>
  <enabled>true</enabled>
  <testMode>true</testMode>
  <useViqProxy>true</useViqProxy>
  <accounts>
    <entry>
      <string>SALE</string>
      <account>
        <merchantId>??</merchantId>
        <terminalId>??</terminalId>
        <secretKey>??</secretKey>
        <defaultDescriptor>order description goes here</defaultDescriptor>
        <authType>AUTH_CAPTURE</authType>
        <supportedCurrencies>EUR|KZT|KGS</supportedCurrencies>
        <pspPublicKey>??</pspPublicKey>
      </account>
    </entry>
    <entry>
      <string>AUTH</string>
      <account>
        <merchantId>??</merchantId>
        <terminalId>??</terminalId>
        <secretKey>??</secretKey>
        <defaultDescriptor>order description goes here</defaultDescriptor>
        <authType>FINAL_AUTH</authType>
        <useTokenId>false</useTokenId>
        <supportedCurrencies>EUR|KZT|KGS</supportedCurrencies>
        <pspPublicKey>??</pspPublicKey>
      </account>
    </entry>
  </accounts>
  <statusPollAttemptsCount>5</statusPollAttemptsCount>
  <container>iframe</container>
  <containerType>2</containerType>
  <width>800</width>
  <height>800</height>
</com.devcode.paymentiq.integration.jusan.JusanConfig>
```
</details>

### Attributes
| Attribute                 | Description                                                                                                                                                                                                                                                                                                    |
|---------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| account.merchantId        | Corresponds to the merchant identifier from the Jusan.                                                                                                                                                                                                                                                         |
| account.terminalId        | Corresponds to the terminal ID from the Jusan.                                                                                                                                                                                                                                                                 |
| account.secretKey         | It is used to create a request signature.                                                                                                                                                                                                                                                                      |
| account.defaultDescriptor | Operation description (optional).                                                                                                                                                                                                                                                                              |
| account.authType          | It is used to enable `Sale` or `Auth` tx type in PaymentIQ. Account (at provider side) can either be configured as Sale or Auth. If you need support for both operation types, you will need to have two separate accounts created by the provider, and it can be configured in PaymentIQ like is shown above. |
| account.useTokenId        | It is used to enable card tokenization. It is disabled by default.                                                                                                                                                                                                                                             |
| account.pspPublicKey      | Bank's public RSA key that is used to encrypt card data.                                                                                                                                                                                                                                                       |
| statusPollAttemptsCount   | Sometimes it takes some time to received a final tx status from the provider and in order to wait on that final status you can configure `statusPollAttemptsCount` to perform several status check attempts (3 times by default).                                                                              |
| statusPollIntervalInSec   | It is used to specify a timeout between status check attempts (2 sec. by default).                                                                                                                                                                                                                             |
| container                 | It is used to define a container (`window` or `iframe` are possible).                                                                                                                                                                                                                                          |
| containerType             | It is used to specify an iframe type. It is valid for both, `window` and `iframe` containers but only for `txType=WebRedirectDeposit`, when card details will be specified at provider side. Possible values are: 1, 2, 3.                                                                                     |

### Notes
Merchant identifier, terminal ID, secret key and RSA key should be provided by the provider.

## Example Routing Rule
![](/img/providers/routing/jusan.png)

## Test Information

Credit card deposit can be initiated in two ways:
- by using `CreditcardDeposit` tx type. In such case card data will be specified at PaymentIQ side;
- by using `WebRedirectDeposit` tx type. In such case user will be redirected to the provider page to specify card data. `containerType` can be used for this tx type only.

3DS Deposit can be tested on Production only.

### Test Cards

| Card Type | Card Name | Card Number      | Expiry Date | CVV | Result  |
|-----------|-----------|------------------|-------------|-----|---------|
| Viusa     | Any       | 4413280046925120 | 04/2023     | 618 | Success |
