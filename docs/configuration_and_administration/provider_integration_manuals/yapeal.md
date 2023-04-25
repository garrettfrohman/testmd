--- 
id: "yapeal" 
title: "Yapeal"
hide_title: "true"
---
 
![](/img/providers/logos/yapeal.png)

# Yapeal

## About
Yapeal is a wallet provider that lets the users add their bank account and use it to send and receive money from a mobile app.

| Provider Name                | Yapeal                                       |
|------------------------------|----------------------------------------------|
| Link                         | [https://yapeal.ch/](https://yapeal.ch/)     |
| Classification               | Wallet , Mobile , Online Banking             |
| Regions                      | `Switzerland`                                |
| Currencies                   | `CHF`                                        |
| Methods/PaymentTxTypes       | `BankIBANDeposit` <br/> `BankIBANWithdrawal` |
| PaymentIQ Configuration File | `YapealConfig`                               |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.yapeal.YapealConfig>
  <enabled>true</enabled>
  <testMode>false</testMode>
  <liveServiceEndPoint>https://????.yapeal.ch</liveServiceEndPoint>

  <accounts>
    <entry>
      <string>default</string>
      <account>
        <supportedCurrencies>CHF</supportedCurrencies>
        <apiKey>????</apiKey>
        <username>????</username>
        <notificationPassword>????</notificationPassword>
        <beneficiaryAccountNumber>CH????????</beneficiaryAccountNumber>
        <merchantName>????</merchantName>
        <merchantCountry>??</merchantCountry>
        <merchantZip>????</merchantZip>
        <merchantCity>????</merchantCity>
        <merchantAddress>????</merchantAddress>
        <merchantStreetNumber>??</merchantStreetNumber>

        <httpClientConfigEntry>
          <useClientCert>true</useClientCert>
          <clientCertPem>????</clientCertPem>
          <clientCertKey>????</clientCertKey>
        </httpClientConfigEntry>
      </account>
    </entry>
  </accounts>
</com.devcode.paymentiq.integration.yapeal.YapealConfig>
```

</details>

### Attributes

| Attribute                | Description                                                                                                 |
|--------------------------|-------------------------------------------------------------------------------------------------------------|
| liveServiceEndPoint      | Provided by Yapeal                                                                                          |
| apiKey                   | API key provided by Yapeal                                                                                  |
| username                 | Decided by PaymentIQ. Used by Yapeal for basic auth in callbacks                                            |
| notificationPassword     | Decided by PaymentIQ. Used by Yapeal for basic auth in callbacks                                            |
| beneficiaryAccountNumber | IBAN of account to receive deposits to and send withdrawals from                                            |
| merchantName             | The merchants name. Sent in requests to Yapeal                                                              |
| merchantCountry          | 2-letter country code. Sent in requests to Yapeal                                                           |
| merchantZip              | The merchants zip code. Sent in requests to Yapeal                                                          |
| merchantCity             | The merchants city. Sent in requests to Yapeal                                                              |
| merchantAddress          | Street name without number. Sent in requests to Yapeal                                                      |
| merchantStreetNumber     | Street number. Sent in requests to Yapeal                                                                   |
| httpClientConfigEntry    | SSL certificate data. Ask PaymentIQ Onboarding- or Technical Support Team for help with configuring correct |

## Example Routing Rule
![](/img/providers/routing/yapeal.png)

## Test Information
Test credentials/data is individually assinged to merchants and the merchant will need to contact Yapeal directly.
