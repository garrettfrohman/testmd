--- 
id: "saltarpay" 
title: "SaltarPay"
hide_title: "true"
---
 
![](/img/providers/logos/saltarpay.png)

# SaltarPay

## About
SaltarPay is a payment provider offering creditcard 3DS2 deposit (SALE and AUTH), CAPTURE, CANCEL and full REFUND. 3DS2 is mandatory and is fully handled by the provider.<br/>
Currently they support Visa only, but MasterCard will be supported as well soon.<br/>
Partial REFUND and CAPTURE are not supported.

### Currencies
- Most transactions are local currency. So INR for India, JPY for Japan, etc.
- SaltarPay allows USD for some countries and it can be enabled if requested by the merchant (usually for IN, JP and GCC countries, where USD is prominent).
- SaltarPay doesn't allow EUR for non-EUR countries, so don't submit EUR to say India or Japan, but USD is OK if enabled.

| Provider Name                | SaltarPay                                                                                                                                                                                                                                                                                                                                      |
|------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Link                         | [https://www.saltarpay.com/](https://www.saltarpay.com/)                                                                                                                                                                                                                                                                                       |
| Classification               | Debit/Credit Card Processor                                                                                                                                                                                                                                                                                                                    |
| Regions                      | International                                                                                                                                                                                                                                                                                                                                  |
| Currencies                   | `AED`, `ARS`, `AUD`, `BGN`, `BRL`, `CAD`, `CHF`, `CLP`, `CZK`, `DKK`, `EUR`, `GBP`, `HRK`, `HUF`, `INR`, `JPY`, `KHR`, `USD`, `KWD`, `USD`, `KRW`, `LAK`, `USD`, `LKR`, `MMK`, `USD`, `MXN`, `MYR`, `NOK`, `NZD`, `PEN`, `PHP`, `PLN`, `QAR`, `USD`, `RON`, `RSD`, `RUB`, `SAR`, `SEK`, `SGD`, `USD`, `THB`, `TTD`, `UAH`, `ZAR`, `VND`, `USD` |
| Methods/PaymentTxTypes       | `CreditcardDeposit`<br/>`Capture`<br/>`Void`<br/>`Refund`                                                                                                                                                                                                                                                                                      |
| PaymentIQ Configuration File | `SaltarPayConfig`                                                                                                                                                                                                                                                                                                                              |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.saltrapay.SaltarPayConfig>
  <enabled>true</enabled>
  <useViqProxy>true</useViqProxy>
  <accounts>
    <entry>
      <string>DEFAULT</string>
      <account>
        <profileId>??</profileId>
        <apiKey>??</apiKey>
        <secretKey>??</secretKey>
        <use3Dsecure>true</use3Dsecure><!--true - to make 3DS payment, false - to make N3DS payment-->
        <authType>AUTH_CAPTURE</authType><!--FINAL_AUTH - to make AUTH, AUTH_CAPTURE - to make SALE (AUTH + CAPTURE as one tx)-->
        <supportedCurrencies>USD</supportedCurrencies>
      </account>
    </entry>
  </accounts>
  <container>iframe</container><!--iframe (default) or window-->
  <testMode>false</testMode>
  <defaultDescriptor>Bambora Payment: ${ptx.txRefId}</defaultDescriptor>
</com.devcode.paymentiq.integration.saltrapay.SaltarPayConfig>

```
</details>

### Attributes

| Attribute | Description                                                                                                    |
|-----------|----------------------------------------------------------------------------------------------------------------|
| profileId | Identifies merchant's account configuration at SaltarPay side. Optional parameter in PaymentIQ.                |
| apiKey    | Corresponds to *API Key* from SaltarPay. It is a required parameter in each request that is sent to SaltarPay. |
| secretKey | Corresponds to *Secret Key* from SaltarPay. It is used to sign requests that are sent to SaltarPay.            |

Make sure to include the User Agent header in the /process request to avoid validation issues on SaltarPay's side.

https://docu-portal-test.paymentiq.io/docs/apis_and_integration/front_api/CreditCardDeposit

Please ask SaltarPay to whitelist IPs for PaymentIQ and configure "callback" URL:

#### TEST
https://test-api.paymentiq.io/paymentiq/api/saltarpay/callback

#### PRODUCTION
https://api.paymentiq.io/paymentiq/api/saltarpay/callback

## Example Routing Rule
![](/img/providers/routing/saltarpay.png)

## Test Information

To make a 3DS payment the end-user will have to specify the credit card details and once the pay button is pressed the end-user will be redirected to the 3DS auth page where the PIN code should be entered to proceed with the payment.
On the test environment, the end-user will be redirected to

![](/img/providers/saltarpay_3ds_auth.png)

where different payment scenarios can be simulated.

### Test cards

| # | Description | Card Number      | Brand |
|---|-------------|------------------|-------|
| 1 | APPROVED    | 4012888888881881 | VISA  |
| 2 | DECLINED    | 4242424242424242 | VISA  |
| 3 | NOTENROLLED | 4900000000000086 | VISA  |