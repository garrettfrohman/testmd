--- 
id: "mercadopago" 
title: "Mercado Pago"
hide_title: "true"
---

![](/img/providers/logos/mercadopago.png)

# Mercado Pago

## About
Mercado Pago is a payment provider offering deposits (for now, withdrawal should be implemented) in Argentina only.<br/>

| Provider Name                | Mercado Pago                                                       |
|------------------------------|--------------------------------------------------------------------|
| Link                         | [https://www.mercadopago.com.ar/](https://www.mercadopago.com.ar/) |
| Classification               | Debit/Credit Card Processor                                        |
| Supported Countries          | Argentina                                                          |
| Currencies                   | `ARS`                                                              |
| Methods/PaymentTxTypes       | `WebredirectDeposit`                                               |
| PaymentIQ Configuration File | `MercadoPagoConfig`                                                |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.mercadopago.MercadoPagoConfig>
    <enabled>true</enabled>
    <testMode>true</testMode>
    <accounts>
        <entry>
            <string>DEFAULT</string>
            <account>
                <accessToken>{account.accessToken}</accessToken>
                <productName>{account.productName}</productName>
                <defaultDescriptor>{account.defaultDescriptor}</defaultDescriptor>
            </account>
        </entry>
    </accounts>
</com.devcode.paymentiq.integration.mercadopago.MercadoPagoConfig>
```
</details>

### Attributes

| Attribute                 | Description                                                 |
|---------------------------|-------------------------------------------------------------|
| account.accessToken       | Corresponds to the consumer access token from Mercado Pago. |
| account.productName       | Corresponds to name of product in the cart (optional).      |
| account.defaultDescriptor | Corresponds to the order description (optional)             |

## Example Routing Rule
![](/img/providers/routing/mercadopago.png)

## Test Information

Requires having account in Mercado Pago Developers environment (use access token from that account).
Testing can be done on STAGE env. using TEST account and test credit cards (Visa, Mastercard, American Express).
For testing purpose set user email to "test_user_21118429@testuser.com" (important only for test env).

Test cards

| Card Brand       | Card number         | CVV  | Expiry Date |
|------------------|---------------------|------|-------------|
| Visa             | 4509 9535 6623 3704 | 123  | 11/25       |
| Mastercard       | 5031 7557 3453 0604 | 123  | 11/25       |
| American Express | 3711 803032 57522   | 1234 | 11/25       |

To test different payment results, fill in the desired status in the name of the cardholder:

| Payment status | Description                                  |
|----------------|----------------------------------------------|
| APRO           | Payment approved                             |
| CONT           | Payment pending                              |
| OTHE           | Rejected by general error                    |
| CALL           | Rejected with validation to authorize        |
| FUND           | Rejected for insufficient amount             |
| SECU           | Rejected by invalid security code            |
| EXPI           | Rejected due to problem with expiration date |
| FORM           | Rejected by error in the form                |

 