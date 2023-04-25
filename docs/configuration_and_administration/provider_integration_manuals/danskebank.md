--- 
id: "danskebank" 
title: "Danskebank"
hide_title: "true"
---
 
![](/img/providers/logos/danskebank.png)

# Danskebank

## About
Danske Bank provides an API to send payment files to them. PaymentIQ currently supports sending files of type NemKonto payments. 

| Provider Name                | Danskebank                                                                      |
|------------------------------|---------------------------------------------------------------------------------|
| Link                         | [https://danskebank.com/](https://danskebank.com/)                              |
| Classification               | Online Banking                                                                  |
| Regions                      | `International`                                                                 |
| Currencies                   | Please check directly with the provider regarding what currencies are supported |
| Methods/PaymentTxTypes       | `NemKontoWithdrawal`                                                            |
| PaymentIQ Configuration File | `DanskeBankConfig`                                                              |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.danskebank.DanskeBankConfig> 
  <enabled>true</enabled>
  <defaultDescriptor>????????</defaultDescriptor> <!-- Used as description/purpose in payment file -->
  <reversalCheckAccountName>??????</reversalCheckAccountName> <!-- Account name used for reversals. Should be set to the same account name that is used for regular processing -->
  <accounts> 
    <entry> 
      <string>nemkonto</string> 
      <account> 
        <merchantId>?????</merchantId> <!-- CustomerID --> 
        <sourceAccount>??????</sourceAccount> <!-- Account to send funds from in IBAN format --> 
        <defaultCurrency>???</defaultCurrency> <!-- Currency of from account --> 
        <password>????</password> <!-- PIN --> 
        <supportedCurrencies>DKK</supportedCurrencies> 
        <merchantName>?????</merchantName> <!-- Will be added as Debtor Name in the payment file --> 
        <merchantCountry>??</merchantCountry> <!-- Will be added as Debtor Country in the payment file (Two letter code, ex DK) --> 
        <financialInstitutionBic>????????</financialInstitutionBic> 
        <financialInstitutionCountry>??</financialInstitutionCountry> 
        <key1> <!-- Encryption private key --> 
        -----BEGIN PRIVATE KEY-----
        ?????? 
        -----END PRIVATE KEY----- 
        </key1> 
        <key2> <!-- Signing private key --> 
        -----BEGIN PRIVATE KEY----- 
        ?????? 
        -----END PRIVATE KEY-----
        </key2> 
        <signingCertificate>
        -----BEGIN CERTIFICATE----- 
        ?????? 
        -----END CERTIFICATE----- 
        </signingCertificate> 
        <encryptionCertificate>
        -----BEGIN CERTIFICATE----- 
        ?????? 
        -----END CERTIFICATE----- 
        </encryptionCertificate> 
        <bankSigningCertificate>
        -----BEGIN CERTIFICATE----- 
        ?????? 
        -----END CERTIFICATE----- 
        </bankSigningCertificate> 
        <bankEncryptionCertificate>
        -----BEGIN CERTIFICATE----- 
        ?????? 
        -----END CERTIFICATE----- 
        </bankEncryptionCertificate> 
      </account> 
    </entry> 
  </accounts> 
</com.devcode.paymentiq.integration.danskebank.DanskeBankConfig> 
```
</details>

### Attributes

| Attribute                | Description                                                                                                  |
|--------------------------|--------------------------------------------------------------------------------------------------------------|
| merchantId               | CustomerID                                                                                                   |
| sourceAccount            | Account to send funds from in IBAN format                                                                    |
| reversalCheckAccountName | Account name used for reversals. Should be set to the same account name that is used for regular processing  |
| defaultCurrency          | Currency of from account                                                                                     |
| password                 | PIN                                                                                                          |
| supportedCurrencies      |                                                                                                              |
| debtorName               | Will be added as Debtor Name in the payment file                                                             |
| debtorCountry            | Will be added as Debtor Country in the payment file (Two letter code, ex DK)                                 |
| financialInstitutionBic  |                                                                                                              |
| defaultDescriptor        | Used as description/purpose in payment file                                                                  |

There are several certificates that needs to be created and added to the config in order to setup the communication with Danske Bank. Please contact Tech support for help with creating the certificates.

## Example Routing Rule
![](/img/providers/routing/danskebank.png)

## Test Information
There is no test environment. It is possible to mark the payment files sent to Danske Bank as TEST though which will not process the payments. But production certificates and keys will have to be used so it is not recommended to do that since they would need to be added PIQ test BO. The payment files are marked as TEST when the tag ```<testMode>true</testMode>``` is added to the config.
