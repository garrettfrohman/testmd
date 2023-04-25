--- 
id: "adumo" 
title: "Adumo Online"
hide_title: "true"
---
 
![](/img/providers/logos/adumo.png)

# Adumo Online

## About
Adumo Online is a credit card payment provider offering 3DS/N3DS Auth, Capture, Sale, Void, Refund, Recurring and Status Check.<br/>

| Provider Name                | Adumo  Online                                                |
|------------------------------|--------------------------------------------------------------|
| Link                         | [https://www.adumoonline.com/](https://www.adumoonline.com/) |
| Classification               | Debit/Credit Card Processor                                  |
| Regions                      | `South Africa`                                               |
| Currencies                   | `ZAR`                                                        |
| Methods/PaymentTxTypes       | `CreditcardDeposit`<br/>`Capture`<br/>`Void`<br/>`Refund`    |
| PaymentIQ Configuration File | `AdumoConfig`                                                |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.adumo.AdumoConfig>
  <enabled>true</enabled>
  <useViqProxy>true</useViqProxy>
  <accounts>
    <entry>
      <string>N3DS</string>
      <account>
        <merchantId>??</merchantId><!--MerchantUID-->
        <accountID>??</accountID><!--ApplicationUID-->
        <username>??</username><!--client_id-->
        <password>??</password><!--client_secret-->
        <useTokenId>true</useTokenId>
        <authType>FINAL_AUTH</authType><!--FINAL_AUTH|AUTH_CAPTURE-->
        <defaultDescriptor>Test Product</defaultDescriptor>
        <supportedCurrencies>ZAR</supportedCurrencies>
      </account>
    </entry>
    <entry>
      <string>3DS</string>
      <account>
        <merchantId>??</merchantId><!--MerchantUID-->
        <accountID>??</accountID><!--ApplicationUID-->
        <username>??</username><!--client_id-->
        <password>??</password><!--client_secret-->
        <secretKey>??</secretKey><!--Secret Key to decode JWT token in the notification-->
        <use3Dsecure>true</use3Dsecure>
        <useTokenId>false</useTokenId>
        <defaultDescriptor>Test Product</defaultDescriptor>
        <supportedCurrencies>ZAR</supportedCurrencies>
      </account>
    </entry>
  </accounts>
  <testMode>true</testMode>
  <container>window</container><!--iframe|window-->
</com.devcode.paymentiq.integration.adumo.AdumoConfig>
```
</details>

### Attributes
| Attribute          | Description                                                                                                                                                                                                                                                       |
|--------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| account.username   | Corresponds to the `client_id` from Adumo Online. It is used to request access token that will be used to authorize payment request. Provided by the Adumo Online.                                                                                                |
| account.password   | Corresponds to the `client_secret` from Adumo Online. It is used to request access token that will be used to authorize payment request. Provided by the Adumo Online.                                                                                            |
| account.merchantId | Corresponds to the `MerchantUID` from Adumo Online. Each `MerchantUID` will have a unique set of `client_id` and `client_secret`, and for each `MerchantUID` there could be multiple `ApplicationUIDs` defined.                                                   |
| account.accountID  | Corresponds to the `ApplicationUID` from Adumo Online. `ApplicationUID` - it is like an account in the Adumo Online system that could have different setup e.g. different payment type, currency, `autoSettle=true or false`, `MerchantUID` etc.                  |
| account.secretKey  | Corresponds to the `JWT secret key` from Adumo Online. It is used to decode JWT token received with a callback notification                                                                                                                                       |
| account.useTokenId | It is a PaymentIQ related setting to enable and use card tokenization. Once it is set to `true` PaymentIQ will tokenize card and next time user will make a repeated payment (with stored card details), that card token will be used.                            |
| account.authType   | It is a PaymentIQ related setting to identify which operation (Auth or Sale) should be performed. Before using this property, please check `AutoSettle` setting for your account at Adumo Online side, as it might affect your expected result (see notes below). |

### Notes
- Currency is not present in the request and it is identified by the `ApplicationUID`.
- Merchant account can have `autoSettle=true`. In that case Auth tx will be settled automatically

`AutoSettle=true`:  In that case PaymentIQ can just do Auth+Capture as one tx<br/>
`AutoSettle=false`: In that case PaymentIQ can do Auth+Capture as one tx (`authType=AUTH_CAPTURE` in the config) and Auth and then Capture as separate tx (`authType=FINAL_AUTH`)

- Webhook/notification URL can only be configured by the provider. It is defined per `ApplicationUID` separately (each `ApplicationUID` has its own notification URL). Webhooks are fired at the end of a transaction (settled or failed).

TEST: https://test-api.paymentiq.io/paymentiq/api/adumo/callback<br/>
PROD: https://api.paymentiq.io/paymentiq/api/adumo/callback

- Adumo Online will provide all required information (in the table above) to the merchant directly.

## Example Routing Rule
![](/img/providers/routing/adumo.png)

## Test Information

### Non 3D Secure Test Cards

| Card Type  | Card Name | Card Number      | Expiry Date | CVV | Result     |
|------------|-----------|------------------|-------------|-----|------------|
| Visa       | Joe Soap  | 4111111111111111 | Any         | Any | Successful |
| Visa       | Joe Soap  | 4242424242424242 | Any         | Any | Declined   |
| MasterCard | Joe Soap  | 5100080000000000 | Any         | Any | Successful |
| MasterCard | Joe Soap  | 5404000000000001 | Any         | Any | Declined   |
| AMEX       | Joe Soap  | 370000200000000  | Any         | Any | Successful |
| AMEX       | Joe Soap  | 374200000000004  | Any         | Any | Declined   |
| Diners     | Joe Soap  | 36135005437019   | Any         | Any | Successful |
| Diners     | Joe Soap  | 36135182434011   | Any         | Any | Declined   |
| Maestro    | Joe Soap  | 5641821111166669 | Any         | Any | Successful |
| Maestro    | Joe Soap  | 6759411100000008 | Any         | Any | Declined   |


### 3D Secure Test Cards

| Card Type  | Card Name | Card Number      | Expiry Date | CVV | Result     |
|------------|-----------|------------------|-------------|-----|------------|
| Visa       | Joe Soap  | 4000000000000002 | Any         | Any | Successful |
| Visa       | Joe Soap  | 4000000000000010 | Any         | Any | Declined   |
| MasterCard | Joe Soap  | 5200000000000007 | Any         | Any | Successful |
| MasterCard | Joe Soap  | 5200000000000023 | Any         | Any | Declined   |
