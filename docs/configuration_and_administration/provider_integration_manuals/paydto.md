--- 
id: "paydto" 
title: "Paydto"
hide_title: "true"
---
 
![](/img/providers/logos/paydto.png)

# Paydto

## About
Paydto hosted payment page provides a secure yet simple means of authorizing transactions payments from your online portal.

Paydto provides a straightforward payment interface for the customer, and handles the complete process for the online transaction.

| Provider Name                | Paydto                                                                          |
|------------------------------|---------------------------------------------------------------------------------|
| Link                         | [https://www.paydto.com/](https://www.paydto.com/)                              |
| Classification               | PrePaid Card / Voucher                                                          |
| Regions                      | `International`                                                                 |
| Currencies                   | Please check directly with the provider regarding what currencies are supported |
| Methods/PaymentTxTypes       | `CreditcardDeposit` <br/> `Refund`                                              |
| PaymentIQ Configuration File | `PaydtoConfig`                                                                  |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.paydto.PaydtoConfig>
  <enabled>true</enabled>
  <useViqProxy>true</useViqProxy>
  <useVisaVoucherAsFallbackForCc>true</useVisaVoucherAsFallbackForCc>
  <accounts>
    <entry>
      <string>DEFAULT</string>
      <account>
        <merchantName>??</merchantName>
        <apiKey>??</apiKey>
        <secretKey>??</secretKey>
        <supportedCurrencies>EUR</supportedCurrencies>
        <useTokenId>false</useTokenId> <!-- true = enables the use of stored card token  -->
      </account>
    </entry>
  </accounts>
  <defaultDescriptor>Devcode</defaultDescriptor>
  <testMode>true</testMode>
</com.devcode.paymentiq.integration.paydto.PaydtoConfig>

```

</details>

### Attributes

| Attribute                     | Description                                                                                                                                                                          |
|-------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| apiKey                        | Provided by Paydto                                                                                                                                                                   |
| secretKey                     | Provided by Paydto                                                                                                                                                                   |
| useTokenId                    | Flag the transaction to use Paydto's store card functionality, which means Paydto will save a token for future re-occurring transactions                                             |
| useVisaVoucherAsFallbackForCc | Flag to set if Paydto's Visa by Voucher should be used to process the payment instead of regular Credit card when setting up a fallback routing rule with Paydto as the fallback psp |

### Note

CreditcardDeposit can be used for doing both a normal CreditcardDeposit and Paydto's Visa By Voucher solution. 
To use Visa by Voucher, include a `service` parameter in the process request to the Front API with value `PAYDTOVOUCHER`

### Notification/Callback

Callback/Notification need to be set by Paydto technical support.

### Callback URL test

`https://test-api.paymentiq.io/paymentiq/api/paydto/callback/{txRefId}`

{txRefId} is to be replaced with transaction id

### Callback URL hosted production

`https://api.paymentiq.io/paymentiq/api/paydto/callback/{txRefId}`

{txRefId} is to be replaced with transaction id

## Example Routing Rule

![](/img/providers/routing/paydto.png)

## Test Information

### Visavoucher and Creditcard

- Mock user: PAYDTO_EUR

| Card Brand | Account          | CVV | Expiry date | Result/Info  |
|------------|------------------|-----|-------------|--------------|
| VISA       | 4012888888881881 | 123 | 10/2025     | APPROVED     |
| VISA       | 4242424242424242 | 123 | 10/2025     | DECLINED     |
| VISA       | 4900000000000086 | 123 | 10/2025     | NOT ENROLLED |
