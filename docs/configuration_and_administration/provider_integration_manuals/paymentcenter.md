--- 
id: "paymentcenter" 
title: "PaymentCenter"
hide_title: "true"
---
 
![](/img/providers/logos/paymentcenter.png)

# PaymentCenter

## About
PaymentCenter is a credit card provider that offers 3DS (v1 and v2) and N3DS deposit (sale, authorization + capture), recurring, void, refund, withdrawal, WebRedirectDeposit (WebPay)  and status check.

| Provider Name                | PaymentCenter                                                                                  |
|------------------------------|------------------------------------------------------------------------------------------------|
| Link                         | [https://payment.center/](https://payment.center/)                                             |
| Classification               | Debit/Credit Card Processor                                                                    |
| Regions                      | `International`                                                                                |
| Currencies                   | `EUR`, `USD`, `RUB`                                                                            |
| Methods/PaymentTxTypes       | `CreditcardDeposit`, `CreditcardWithdrawal`, `Refund`, `Capture`, `Void`, `WebRedirectDeposit` |
| PaymentIQ Configuration File | `PaymentCenterConfig`                                                                          |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.paymentcenter.PaymentCenterConfig>
  <enabled>true</enabled>
  <useViqProxy>true</useViqProxy>
  <accounts>
    <entry>
      <string>EUR</string>
      <account>
        <secretKey>??</secretKey>
        <service>??</service>
        <useTokenId>true</useTokenId>
        <use3Dsecure>true</use3Dsecure>
        <authType>AUTH_CAPTURE</authType><!--FINAL_AUTH|AUTH_CAPTURE-->
        <supportedCurrencies>EUR</supportedCurrencies>
        <method>???</method> <!--webpay-->
      </account>
    </entry>
  </accounts>
  <testMode>true</testMode>
  <defaultDescriptor>Bambora Payment</defaultDescriptor>
</com.devcode.paymentiq.integration.paymentcenter.PaymentCenterConfig>
```

</details>

### Attributes
| Attribute               | Description                                                                                                                                     |
|-------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------|
| accountConfig.secretKey | Configured by PaymentCenter and can be found at PaymentCenter cabinet ("Services" section). It is used to sign each request.                    |
| accountConfig.service   | Configured by PaymentCenter and can be found at PaymentCenter cabinet ("Services" section). One service (terminal) corresponds to one currency. |
| accountConfig.method    | Corresponds to the payment method that will be used when initiating a WebRedirectDeposit transaction. ex: 'webpay'                              |
| statusPollIntervalInSec | Defines in seconds the interval of which the status API will poll to obtain the 3DS redirectUrl. Defaults to 2.                                 |
| statusPollAttemptsCount | Defines the number of times the status API will attempt to poll to obtain the 3DS redirectUrl. Defaults to 5.                                   |

### Callback URL
Callback URLs can be configured at Payment Center cabinet: https://cabinet.payment.center/ui/main/ (in "Services" section when you press "Action") as shown below:

![](/img/providers/paymentcenter_callback_urls.png)

#### Callback URLs
- TEST: https://test-api.paymentiq.io/paymentiq/api/paymentcenter/callback
- PROD: https://api.paymentiq.io/paymentiq/api/paymentcenter/callback

### Trim unsupported characters
PaymentCenter does not accept non-latin characters in certain fields, and because of that we have trim away such unsupported characters if they are provided to PIQ. The known so far where it's a potential issue is the `cardHolder` field.

The default is to trim away characters that align with the regex `cardHolder->[^a-zA-Z-. ]` (meaning trim away all characters that are not `a-z`, `-`, `.`, and ` `) for the `cardHolder` field.

If it turns out there are more fields that need this trim, or if the regex has to be updated, it can be done with the configuration entry `invalidCharsRegex`

Example where the `address` field is added and the regex is updated to also trim away dots (`.`): `<invalidCharsRegex>address|cardHolder->[^a-zA-Z- ]</invalidCharsRegex>`

### WebPay (WebRedirectDeposit)

WebPay is a one-step payment operation offered by PaymentCenter. It is integrated as a webredirect deposit operation in PIQ.
To use it, merchant needs to add WebRedirectDeposit Tx Type in the PaymentCenter Routing Rules, set "webpay" as method in the provider accountConfig (<method>webpay</method>) then initiate a webredirect deposit transaction in the cashier. After being redirected to the payment page, one can use any of below credit cards for test.

## Example Routing Rules
![](/img/providers/routing/paymentcenter.png)

### 3DS2 Routing
To enable 3DS2 for PaymentCenter please add additional routing rule to ```Internal3DServer``` via *Rules->Routing->3DS2 Routing*
![](/img/providers/routing/paymentcenter_3ds2.png)

## Test Information

### Credit cards

|        | Card type | Number           | CVV              | Expiry Month                     | Expiry Year |
|--------|-----------|------------------|------------------|----------------------------------|-------------|
| N3DS   | Visa      | 4111111111111111 | >= 600           | 01-06 = success, 07-12 = decline | Any         |
| 3DS v1 | Visa      | 4111111111111111 | < 500            | 01-06 = success, 07-12 = decline | Any         |
| 3DS v2 | Visa      | 4111111111111111 | >= 500 and < 600 | 01-06 = success, 07-12 = decline | Any         |
| N3DS   | MC        | 2201382000000013 | >= 600           | 01-06 = success, 07-12 = decline | Any         |
| 3DS v1 | MC        | 2201382000000013 | < 500            | 01-06 = success, 07-12 = decline | Any         |
| 3DS v2 | MC        | 2201382000000013 | >= 500 and < 600 | 01-06 = success, 07-12 = decline | Any         |
| N3DS   | MC        | 4242424242424242 | >= 600           | 01-06 = success, 07-12 = decline | Any         |
| 3DS v1 | MC        | 4242424242424242 | < 500            | 01-06 = success, 07-12 = decline | Any         |
| 3DS v2 | MC        | 4242424242424242 | >= 500 and < 600 | 01-06 = success, 07-12 = decline | Any         |

**Notes**

#### 4111111111111111

Available test outcomes with this card:
- successful and failed 3DS deposit (including auth + capture)
- successful and failed N3DS deposit (including auth + capture)
- successful refund (full and partial)
- successful void
- successful recurring
- successful withdrawal

#### 2201382000000013

Available test outcomes with this card:
- successful and failed 3DS deposit (including auth + capture)
- successful and failed N3DS deposit (including auth + capture)
- successful refund (full and partial)
- successful void
- failed recurring
- failed withdrawal

#### 4242424242424242

Available test outcomes with this card:
- successful and failed 3DS deposit (including auth + capture)
- successful and failed N3DS deposit (including auth + capture)
- successful refund (full and partial)
- successful void
- failed recurring
- failed withdrawal
