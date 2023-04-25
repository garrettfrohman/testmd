--- 
id: "quaife" 
title: "Quaife"
hide_title: "true"
---
 
![](/img/providers/logos/quaife.png)

# Quaife

## About
Quaife is a payment provider offering creditcard deposit (3DS2/N3DS), auth, capture, void, full/partial refund, withdrawal and Vyne Pay that is a hosted payment page for Open Banking.

| Provider Name                | Quaife                                                                                                        |
|------------------------------|---------------------------------------------------------------------------------------------------------------|
| Link                         | [https://quaife.net/](https://quaife.net/)                                                                    |
| Classification               | Debit/Credit Card Processor, APM (Bank Transfer)                                                              |
| Regions                      | All countries                                                                                                 |
| Currencies                   | Creditcard - all currencies; Vyne Pay - GBP and EUR.                                                          |
| Methods/PaymentTxTypes       | `CreditcardDeposit`<br/>`Capture`<br/>`Void`<br/>`Refund`<br/>`CreditcardWithdrawal`<br/>`WebRedirectDeposit` |
| PaymentIQ Configuration File | `QuaifeConfig`                                                                                                |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.quaife.QuaifeConfig>
  <enabled>true</enabled>
  <useViqProxy>true</useViqProxy>
  <accounts>
    <entry>
      <string>DEFAULT</string>
      <account>
        <username>{apiUsername}</username>
        <password>{apiPassword}</password>
        <apiKey>{apiKey}</apiKey>
        <secretKey>{sharedSecret}</secretKey>
        <useTokenId>true</useTokenId>
        <use3Dsecure>false</use3Dsecure>
        <authType>AUTH_CAPTURE</authType><!--AUTH_CAPTURE|FINAL_AUTH-->
        <withdrawalType>OCT</withdrawalType>
        <supportedCurrencies>EUR</supportedCurrencies>
        <language>en</language>
      </account>
    </entry>
    <entry>
      <string>THREEDS</string>
      <account>
        <username>{apiUsername}</username>
        <password>{apiPassword}</password>
        <apiKey>{apiKey3DS}</apiKey>
        <secretKey>{sharedSecret3DS}</secretKey>
        <useTokenId>true</useTokenId>
        <use3Dsecure>true</use3Dsecure>
        <authType>AUTH_CAPTURE</authType><!--AUTH_CAPTURE|FINAL_AUTH-->
        <withdrawalType>OCT</withdrawalType>
        <supportedCurrencies>EUR</supportedCurrencies>
        <language>en</language>
      </account>
    </entry>
    <entry>
      <string>N3DS</string>
      <account>
        <username>{apiUsername}</username>
        <password>{apiPassword}</password>
        <apiKey>{apiKeyN3DS}</apiKey>
        <secretKey>{sharedSecretN3DS}</secretKey>
        <useTokenId>true</useTokenId>
        <use3Dsecure>false</use3Dsecure>
        <authType>FINAL_AUTH</authType><!--AUTH_CAPTURE|FINAL_AUTH-->
        <withdrawalType>OCT</withdrawalType>
        <supportedCurrencies>EUR</supportedCurrencies>
        <language>en</language>
      </account>
    </entry>
    <entry>
      <string>VYNE</string>
      <account>
        <username>{apiUsername}</username>
        <password>{apiPassword}</password>
        <apiKey>{apiKeyVyne}</apiKey>
        <secretKey>{sharedSecretVyne}</secretKey>
        <supportedCurrencies>EUR|GBP</supportedCurrencies>
        <language>en</language>
      </account>
    </entry>
  </accounts>
  <testMode>true</testMode>
  <container>window</container><!--For Vyne Pay 'window' is supported only-->
  <defaultDescriptor>Bambora payment ${ptx.txRefId}</defaultDescriptor>
  <txHistoryDelayHours>0</txHistoryDelayHours><!--Look for successful deposits starting from now-->
</com.devcode.paymentiq.integration.quaife.QuaifeConfig>
```
</details>

### Attributes
| Attribute         | Description                                                                                                                                     |
|-------------------|-------------------------------------------------------------------------------------------------------------------------------------------------|
| account.username  | API User Name that is used to create Basic Authorization header.                                                                                |
| account.password  | API User Password that is used to create Basic Authorization header.                                                                            |
| account.apiKey    | Corresponds to the Connector API Key from the Quaife. It is used to identify an operation in Quaife system as it is present in the request URL. |
| account.secretKey | Corresponds to the Connector Shared Secret from the Quaife. It is used to create a request signature.                                           |
| account.authType  | It is used to define a payment tx type in PaymentIQ: authType=AUTH_CAPTURE - to make Sale, authType=FINAL_AUTH - to make Auth.                  |

### NOTES
1). `Username` and `Password` should be the same for each account defined in the QuaifeConfig since it is under the same merchant. As for `API Key` and `Secret Key`, they must be unique for each payment method (Creditcard deposit/withdrawal or Bank Transfer), so please double check with Quaife which `Api Key` and `Secret Key` should be used for a specific operation. \
2). To make a withdrawal you will have to set `useTokenId=true` and `withdrawalType=OCT` in the QuaifeConfig and also you will need at least one successful deposit. \
3). To make a 3DS1 or 3DS2 payment please set `use3Dsecure=true` in the QuaifeConfig.

## Example Routing Rule
![](/img/providers/routing/quaife.png)

## Test Information

| Card Type  | Card Number         | Status  |
|------------|---------------------|---------|
| Visa       | 4111 1111 1111 1111 | Success |
| Visa       | 4242 4242 4242 4242 | Failure |
| Mastercard | 5555 5555 5555 4444 | Success |
| Mastercard | 5105 1051 0510 5100 | Failure |
| Diners     | 3800 000000 0006    | Success |
| Amex       | 3782 8224631 0005   | Success |
