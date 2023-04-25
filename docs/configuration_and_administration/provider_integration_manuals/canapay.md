--- 
id: "canapay"
title: "Canapay"
hide_title: "true"
---

![](/img/providers/logos/canapay.png)

# Canapay

## About

| Provider Name                | Canapay                                                    |
|------------------------------|------------------------------------------------------------|
| Link                         | [https://dev.canapay.io/docs](https://dev.canapay.io/docs) |
| Classification               | Debit/Credit Card Processor                                |
| Regions                      | `EU`                                                       |
| Currencies                   | `EUR`                                                      |
| Methods/PaymentTxTypes       | `CreditcardDeposit` <br/> `Refund`                         |
| PaymentIQ Configuration File | `CanapayConfig`                                            |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>


```xml
<com.devcode.paymentiq.integration.canapay.CanapayConfig>
    <enabled>true</enabled>
    <useViqProxy>true</useViqProxy>
    <testMode>true</testMode>
    <container>window</container>
    <accounts>
        <entry>
            <string>???</string>
            <account>
                <use3Dsecure>false</use3Dsecure>
                <supportedCurrencies>EUR</supportedCurrencies>
                <apiKey>???</apiKey>
                <secretKey>???</secretKey>
            </account>
        </entry>
    </accounts>
</com.devcode.paymentiq.integration.canapay.CanapayConfig>

```

</details>

### Attributes

| Attribute           | Description                                                              |
|---------------------|--------------------------------------------------------------------------|
| use3Dsecure         | 3DSecure provided by Canapay (mandatory 'false')                         |
| merchantId          | Merchant's shop id issued by Canapay                                     |
| supportedCurrencies | Canapay supported currencies                                             |
| apiKey              | API key provided by Canapay                                              |
| secretKey           | Signature key provided by Canapay used by PaymentIQ for security reasons |


## Provider Configuration
1. The above XML template (CanapayConfig) will need to be added via backoffice Admin -> Configuration.
2. Routing needs to be added for both Creditcard Deposit in Routing -> Routing.

## Example Routing Rule
![](/img/providers/routing/canapay.png)

## Transaction Flow
1. The end user enters the card number, the name on card, the transaction amount and card's CVV.
2. PaymentIQ sends the deposit request to Canapay.
3. Canapay responds with an initial status + a redirect url to an in-browser verification (typically 3D Secure or a first-time depositor KYC).
4. Any and all necessary verification, such as 3D-Secure, customer fingerprinting, KYC, etc, is handled by Canapay once the customer visits the URL. Once completed, the customer will be redirected in order to complete the payment.
5. Canapay sends back a callback notification once the transaction status has changed.

## Test Information

### Creditcard Deposit
| Card number      | CVV | Brand | Expiry date     | Scenario                         |
|------------------|-----|-------|-----------------|----------------------------------|
| 4242424242424242 | 734 | Visa  | any future date | Success                          |
| 4000000000009979 | 734 | Visa  | any future date | Failure, stolen card             |
| 4000000000000069 | 734 | Visa  | any future date | Failure, declined (expired card) |

### Refund
| Card number      | CVV | Brand | Expiry date     | Scenario                                                     |
|------------------|-----|-------|-----------------|--------------------------------------------------------------|
| 4242424242424242 | 734 | Visa  | any future date | Successful deposit and successful refund                     |
| 2223003122003222 | 734 | Visa  | any future date | Successful deposit and refund of that transaction will fail. |

Refunds are also validated against partial refunds and will fail if partial refund is attempted.

More Creditcard deposits scenarios can be found here: https://dev.canapay.io/docs/guides/scoring-a-transaction/.