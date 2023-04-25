--- 
id: "quickbit" 
title: "QuickBit"
hide_title: "true"
---
 
![](/img/providers/logos/quickbit.png)

# QuickBit

## About
QuickBit designed and built a platform for newcomers and professionals alike.
While we’re proud of catering to professionals, we’re just as excited about helping people discover
the world of crypto and expand their portfolios to include digital assets.

| Provider Name                | QuickBit                                                          |
|------------------------------|-------------------------------------------------------------------|
| Link                         | [https://www.quickbit.eu/](https://www.quickbit.eu/)              |
| Classification               | Crypto Currency                                                   |
| Regions                      | `International`                                                   |
| Currencies                   | `EUR` `USD` `AUD` `CAD` `HUF` `JPY` `NOK` `PLN` `ZAR` `SEK` `TRY` |
| Methods/PaymentTxTypes       | `CryptoCurrencyDeposit` `WebRedirectDeposit` `Refund`             |
| PaymentIQ Configuration File | `QuickBitConfig`                                                  |
  
## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.quickbit.QuickBitConfig>
  <enabled>true</enabled>
  <accounts>
    <entry>
     <string>default</string>
     <account>
        <merchantCode>???</merchantCode> <!-- merchant_profile -->
        <secretKey>???</secretKey>  <!-- Secret -->
        <apiKey>???</apiKey>  <!-- Referral code -->
        <supportedCurrencies>EUR|USD|SEK</supportedCurrencies>
       <cryptoCurrency>BCH</cryptoCurrency>
     </account>
    </entry>
  </accounts>
  <testMode>true</testMode>
  <settleCurrency>EUR</settleCurrency>
 <supportedRefundCodes>04001|04002|04003|04004|04005</supportedRefundCodes>
 <defaultRefundCode>04004</defaultRefundCode>
</com.devcode.paymentiq.integration.quickbit.QuickBitConfig>
```
</details>

### Attributes

| Attribute            | Description                                                                                                              |
|----------------------|--------------------------------------------------------------------------------------------------------------------------|
| merchantCode         | A unique id to differentiate the customers. This value should be between 1 to 7 included.                                |
| secretKey            | Secret Key provided by QuickBit                                                                                          |
| apiKey               | Referral Code provided by QuickBit                                                                                       |
| settleCurrency       | Currency that the order will be settled in, the merchant receives whatever is specified here                             |
| supportedRefundCodes | Refund code is 5 digits number against which dispute reason is mapped. See the refund codes available in the table below |
| defaultRefundCode    | Refund code used by default                                                                                              |
| invalidCharsRegex    | Mapping of field to a regex of valid characters. default: `state_code|postal_code->[^a-zA-Z- 0-9]`                       |

### Trim unsupported characters
Quickbit does not accept non-latin characters in certain fields, and because of that we have trim away such unsupported characters if they are provided to PaymentIQ. This is a potential issue for the `state_code` and `postal_code` field.

The default is to trim away characters that align with the regex `state_code|postal_code->[^a-zA-Z- 0-9]` (meaning trim away all characters that are not `a-z`, `-`, `.`, `0-9` , and ` `) for the `state_code` and `postal_code` field.

If it turns out there are more fields that need this trim, or if the regex has to be updated, it can be done with the configuration entry `invalidCharsRegex`

Example where the `address` field is added and the regex is updated to also trim away dots (`.`): `<invalidCharsRegex>address|state_code|postal_code->[^a-zA-Z- 0-9]</invalidCharsRegex>`

### Refund Codes

| Refund code | Description                    |
|-------------|--------------------------------|
| 04001       | Fraud Alert - Refund           |
| 04002       | Fraud Advice - Refund          |
| 04003       | Chargeback Prevention - Refund |
| 04004       | Affiliate Request - Refund     |
| 04005       | Systems Error - Refund         |

## Example Routing Rule
![](/img/providers/routing/quickbit1.png)

## Test Information

### Deposit

To test QuickBit deposit select Cryptocurrency payment option in PaymentIQ Cashier, 
fill in any amount and follow the instruction after being redirected. Use 4000 0000 0000 0002 as Card Number
when on QuickBit payment page and the following cvv numbers for different responses :


| Test case | cvv | Decline reason                                  |
|-----------|-----|-------------------------------------------------|
| Accepted  | 111 |                                                 |
| 3ds       | 999 |                                                 |
| Decline   | 100 | LUHN_CHECK_FAILED                               |
| Decline   | 200 | ANTIFRAUD_DECLINED                              |
| Decline   | 300 | DO_NOT_HONOUR                                   |
| Decline   | 400 | CRYPTO_CURRENCY_CONVERSION_FAILED               |
| Decline   | 500 | DECLINED_GENERAL                                |
| Decline   | 600 | NO_ACCOUNT_FOUND                                |
| Decline   | 700 | DECLINED_TRANSACTION_NOT_PERMITTED_CONTACT_BANK |
| Decline   | 800 | DECLINED_EXPIRED_CARD                           |

### Refund

To test QuickBit Refund, Initiate a refund request from PaymentIQ BO and enter a specific QuickBit Refund code (see the Refund codes table above) in the comment section, otherwise the refund reason will be the one set by default in "defaultRefundCode" parameter in Quickbit Config.