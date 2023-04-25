--- 
id: "monri"
title: "Monri"
hide_title: "true"
---

![](/img/providers/logos/monri.png)

# Monri

## About
Monri was founded in 2003 under the name Webteh d.o.o. as one of the first payment service providers in the region of Southeast Europe.

Since 2019, it has been part of the Payten/ASEE Group. The focus is the development of advanced solutions for all types of payments. 

PaymentIQ currently support only credit card transactions for Monri via PaymentIQ .

| Provider Name                | Monri                                                           |
|------------------------------|-----------------------------------------------------------------|
| Link                         | [https://monri.com/](https://monri.com/)                        |
| Classification               | Debit/Credit Card Processor                                     |
| Regions                      | `Europe`                                                        |
| Currencies                   | `USD`, `EUR`, `BAM`, `HRK`                                      |
| Methods/PaymentTxTypes       | `CreditcardDeposit` <br/> `Capture` <br/> `Void` <br/> `Refund` |
| PaymentIQ Configuration File | `MonriConfig`                                                   |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.monri.MonriConfig>
    <enabled>true</enabled>
    <useViqProxy>true</useViqProxy>
    <accounts>
        <entry>
            <string>N3DS_AUTH</string>
            <account>
                <apiKey>??</apiKey>
                <apiToken>??</apiToken>
                <authType>FINAL_AUTH</authType>
                <supportedCurrencies>EUR</supportedCurrencies>
            </account>
        </entry>
    </accounts>
    <testMode>true</testMode>
    <defaultDescriptor>DevCode payment</defaultDescriptor>
</com.devcode.paymentiq.integration.monri.MonriConfig>
```

</details>

### Attributes

| Attribute              | Description                                                                                        |
|------------------------|----------------------------------------------------------------------------------------------------|
| accountConfig.apiKey   | Key used for creating Monri request signatures. Can be found in Monri merchant account settings    |
| accountConfig.apiToken | Corresponds to the Monri authenticity token value. Can be found in Monri merchant account settings |


## Example Routing Rule

![](/img/providers/routing/monri.png)

## Test Information

| Card Number      | Type | Expiry Date     |
|------------------|------|-----------------|
| 4341792000000044 | 3DS  | Any future date |
| 4111111111111111 | N3DS | Any future date |
| 6769064219992611 | 3DS  | Any future date |