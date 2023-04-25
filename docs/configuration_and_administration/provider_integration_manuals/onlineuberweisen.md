--- 
id: "onlineuberweisen" 
title: "Onlineüberweisen"
hide_title: "true"
---
 
![](/img/providers/logos/onlineuberweisen.png)

# Onlineüberweisen

## About
Onlineüberweisen is a solution allowing user to pay using their bank account.

| Provider Name                | Onlineüberweisen                                                 |
|------------------------------|------------------------------------------------------------------|
| Link                         | [https://onlineueberweisen.com/](https://onlineueberweisen.com/) |
| Classification               | Online Banking                                                   |
| Regions                      | `Germany`, `Switzerland`, `Austria`                              |
| Currencies                   | `EUR`                                                            |
| Methods/PaymentTxTypes       | `BankIBANDeposit`<br/> `WebredirectDeposit`                      |
| PaymentIQ Configuration File | `OnlineüberweisenConfig`                                         |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.onlineueberweisen.OnlineueberweisenConfig>
  <enabled>true</enabled>
  <accounts>
    <entry>
      <string></string>
      <account>
        <supportedCurrencies>EUR</supportedCurrencies>
        <username></username>
        <secretKey></secretKey>
        <password></password>
        <version>v1</version>
        <financialInstitutionCountry></financialInstitutionCountry>
        <container>window</container>
        <sendName>false</sendName> <!-- Set to true if you want to send account holder name -->
      </account>
    </entry>
  </accounts>
</com.devcode.paymentiq.integration.onlineueberweisen.OnlineueberweisenConfig>
```

</details>

### Attributes

| Attribute                   | Description                                                            |
|-----------------------------|------------------------------------------------------------------------|
| username                    | This should be set to 'api'                                            |
| secretKey                   | Corresponds to the Api key from Onlineüberweisen                       |
| password                    | Corresponds to the webhook-shared-secret from Onlineüberweisen         |
| financialInstitutionCountry | 2 letter country code of the account. Defaults to 'de'                 |
| sendName                    | set to true if you want to send the account Holder name in the request |

## Example Routing Rule
![](/img/providers/routing/onlineuberrouting.png)

## Test Information

Testbank is only available with a test API key.

For testing and integration purposes Onlineüberweisen offer a Testbank. While using the Testbank, no real transactions will be made.

The Testbank allows you to try out various ways the payment form and other components can or will behave.

| Testbank Type     | Bank Code | Bic         |
|-------------------|-----------|-------------|
| German Testbank   | 88888888  | TESTDE88XXX |
| Austrian Testbank | 88888     | TESTAT88XXX |

Display of payment form tabs can be forced by using the bank code 88888889 in combination with a test API key.



IBAN                   | Account Number | Bank Code | Description | Transaction possible
-----------------------|----------------|-----------|-------------|---------------------
DE62888888880012345678 | 12345678       | 88888888  | Girokonto   | Yes
DE04888888880087654321 | 87654321       | 88888888  | Extra-Konto | no



If you use the login PIN accounts the German Testbank will return additional accounts:



IBAN                   | Account Number | Bank Code | Description    | Transaction possible
-----------------------|----------------|-----------|----------------|---------------------
DE35888888880012345679 | 12345679       | 88888888  | Girokonto Plus | Yes
DE93888888880043218765 | 43218765       | 88888888  | Kontokorrent   | Yes


In case you want to test pinned account numbers or IBANs, the Austrian Testbank will return the following accounts:



IBAN                 | Account Number | Bank Code | Description | Transaction possible
---------------------|----------------|-----------|-------------|---------------------
AT248888800012345678 | 12345678       | 88888     | Girokonto   | Yes
AT638888800087654321 | 87654321       | 88888     | Sparkonto   | No


If you use the login PIN accounts the Austrian Testbank will return additional accounts:

IBAN                 | Account Number | Bank Code | Description    | Transaction possible
---------------------|----------------|-----------|----------------|---------------------
AT948888800012345679 | 12345679       | 88888     | Girokonto Plus | Yes
AT558888800043218765 | 43218765       | 88888     | Kontokorrent   | Yes
