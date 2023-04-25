--- 
id: "ogone" 
title: "Ogone"
hide_title: "true"
---
 
![](/img/providers/logos/ogone.png)

# Ogone

## About
Ogone is a card processor supporting Deposits, Refunds, Void and Capture. 

It is also an online banking provider supporting supporting SEPA deposits.

| Provider Name                | Ogone                                                                                                                                             |
|------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------|
| Link                         | [http://payment-services.ingenico.com/int/en/support/what-is-ogone](http://payment-services.ingenico.com/int/en/support/what-is-ogone)            |
| Classification               | Debit/Credit Card Processor, Online Banking                                                                                                       |
| Regions                      | `International`                                                                                                                                   |
| Currencies                   | Please check directly with the provider regarding what currencies are supported                                                                   |
| Methods/PaymentTxTypes       | `CreditcardDeposit`<br/> `WebRedirectDeposit`<br/> `IdealDeposit`<br/> `Refund`<br/> `Void`<br/> `Capture`<br/> `BankIBANDeposit`<br/> `Reversal` |
| PaymentIQ Configuration File | `OgoneConfig`                                                                                                                                     |

## Configuration Information

### 3DS2

#### Configuration
### SEPA

For SEPA, route `BankIBANDeposit` transactions to an account configured as specified below. Only `iban` is necessary, as `bic` is not used for SEPA.<br/><br/>
If user accounts are used, the reference for any SEPA mandate created will be saved in the account for reuse at a later time.<br/>
Before a stored mandate reference is used, PaymentIQ first verifies that is is still active by contacting Ogone. If it is shown not to be active, it is removed from the user account
and a new mandate will be created with the deposit.

<details>
<summary>Click to view example OgoneConfig</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.ogone.OgoneConfig>
  <enabled>true</enabled>
  <testMode>false</testMode>
  <accounts>
    <entry>
      <string>SEPA</string>
      <account>
        <merchantId>??</merchantId>
        <apiKey>??</apiKey>
        <secretKey>??</secretKey>
        <recurrenceType>RECURRING</recurrenceType>
        <signatureType>UNSIGNED</signatureType>
      </account>
    </entry>
  </accounts>
</com.devcode.paymentiq.integration.ogone.OgoneConfig>
```
| Property       | Default value | Description                                            |
|----------------|---------------|--------------------------------------------------------|
| merchantId     |               | merchantId from Ogone                                  |
| apiKey         |               | apiKeyId from Ogone                                    |
| secretKey      |               | secretApiKey from Ogone                                |
| recurrenceType | `RECURRING`   | One of `RECURRING` or `UNIQUE`                         |
| signatureType  | `UNSIGNED`    | One of `UNSIGNED` or `SMS`                             |
| testMode       | `false`       | If true, Ogone pre-production environment will be used |



</details>

### Credit card
Ogone does not support a external MPI so the 3DS2 flow is enabled by setting the enabled attribute to true in the ThreeDSConfig.

<details>
<summary>Click to view example ThreeDSConfig</summary>
<br/>

```xml
<?xml version="1.0"?>
<com.devcode.paymentiq.service.threedsecure.ThreeDSConfig>
    <enabled>true</enabled>
    <mcc>7995</mcc>
    <merchantName>Devcode3DTestMerchant</merchantName>
    <merchantCountryCode>SWE</merchantCountryCode>
    <threeDSRequestorURL>http://www.example.com</threeDSRequestorURL>
    <threeDSRequestorId>123</threeDSRequestorId>
    <threeDSRequestorName>abc</threeDSRequestorName>
</com.devcode.paymentiq.service.threedsecure.ThreeDSConfig>
```
</details>

<br/>

* For more details of ThreeDSConfig can be found [here](https://docs.paymentiq.io/europe/3ds2/testing/testing3ds2#attributes) .



## Example Routing Rule
![](/img/providers/routing/ogone.png)

## Test Information

- Currency: EUR, USD, GBP, CHF

### N3DS

| Card Brand       | Account          | CVV | Expiry date |
|------------------|------------------|-----|-------------|
| VISA             | 4111111111111111 | Any | Any         |
| MASTERCARD       | 5399999999999999 | Any | Any         |
| AMERICAN EXPRESS | 374111111111111  | Any | Any         |

### 3DS

| Card Brand       | Account          | CVV | Expiry date | 3DS Code |
|------------------|------------------|-----|-------------|----------|
| VISA             | 4000000000000002 | Any | Any         | 11111    |
| AMERICAN EXPRESS | 371449635311004  | Any | Any         | 11111    |

### 3DS2
* Some testcards 3DS2 testcards can be found [here](https://docs.paymentiq.io/europe/3ds2/testing/testing3ds2#test-cards-and-examples-for-providers) .
* More testcards can be found [here](https://payment-services.ingenico.com/ogone/support/~/media/kdb/integration%20guides/directlink%203ds%20v2/testcards_3ds%20v2_en.ashx?la=en) .

