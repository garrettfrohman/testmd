--- 
id: "icepay" 
title: "ICEPAY"
hide_title: "true"
---
 
![](/img/providers/logos/icepay.png)

# ICEPAY

## About
ICEPAY is an aggregator that offers a number of alternative payment methods using their hosted payment page.

| Provider Name                | ICEPAY                                                                                                              |
|------------------------------|---------------------------------------------------------------------------------------------------------------------|
| Link                         | [https://icepay.com/](https://icepay.com/)                                                                          |
| Classification               | Aggregator                                                                                                          |
| Regions                      | International                                                                                                       |
| Currencies                   | Depends on selected payment method, but `EUR` is supported by all payment options                                   |
| Limits                       | Min - 1 {currency}; Max - 1.000.000.000,00 {currency}, where {currency} -- supported currency by the payment method |
|                              | CREDITCLICK: Min - 25.000,00 EUR; Max - 100.000,00 EUR                                                              |
|                              | POS: Min - 1 EUR; Max - 100.000,00 EUR                                                                              |
| Methods/PaymentTxTypes       | `WebRedirectDeposit`, `Refund`                                                                                      |
| PaymentIQ Configuration File | `IcePayConfig`                                                                                                      |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.icepay.IcePayConfig>
  <enabled>true</enabled>
  <useViqProxy>false</useViqProxy>
  <accounts>
    <entry>
      <string>DEFAULT</string>
      <account>
        <secretKey>??</secretKey>
        <profileId>??</profileId>
        <!--<paymentCode>ING</paymentCode>--><!--for IDEAL-->
        <supportedCurrencies>EUR</supportedCurrencies>
      </account>
    </entry>
  </accounts>
  <testMode>true</testMode>
  <container>window</container><!--CREDITCARD-->
  <defaultDescriptor>Order: ${ptx.txRefId}</defaultDescriptor>
</com.devcode.paymentiq.integration.icepay.IcePayConfig>
```

</details>

### Attributes

| Attribute   | Description                                                                                                                                                                                                                                                                                                                                         |
|-------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| secretKey   | Corresponds to *Secret Key* from ICEPAY. It is used to build a request signature                                                                                                                                                                                                                                                                    |
| profileId   | Corresponds to *Contract Profile ID* from ICEPAY. It is used as a "UserId" request header                                                                                                                                                                                                                                                           |
| paymentCode | Corresponds to *Issuer Code* from ICEPAY. In most cases "Issuer Code" is the same as "Payment Method" (BANCONTACT, GIROPAY, PAYPAL, ...) but in some cases it can differ e.g. for IDEAL (Payment Method: IDEAL; Issuer: ING). So you can use "paymentCode" config property to specify unique "Issuer" if it is different from the "Payment Method". |

### Where to get Secret Key and Contract Profile ID from?

You can find Secret Key and Contract Profile ID in ICEPAY portal using this [link](https://acc-interconnect.icepay.com/portal).

Go to "Contract Profiles" section and find your settings:

![](/img/providers/icepay_portal.png)

### Supported Payment Methods
| Payment method   | Issuer                         |
|------------------|--------------------------------|
| AFTERPAY         | AFTERPAY                       |
| CREDITCARD       | CREDITCARD                     |
| IDEAL            | ING                            |
| CREDITCLICK      | CREDITCLICK                    |
| BANCONTACT       | BANCONTACT                     |
| ONLINEUBERWEISEN | ONLINEUBERWEISEN               |
| WECHATPAY        | WECHATPAY                      |
| ALIPAY           | ALIPAY                         |
| SAFETYPAY        | SAFETYPAY                      |
| UNIONPAY         | UNIONPAY                       |
| EPS              | EPS                            |
| GIROPAY          | GIROPAY                        |
| WIRETRANSFER     | WIRETRANSFER                   |
| DIRECTDEBIT      | DIRECTDEBIT                    |
| SOFORT           | SOFORT, DIGITAL, ADULT, RETAIL |
| PAYPAL           | PAYPAL                         |
| POS              | POS                            |
| PAYSAFECARD      | PAYSAFECARD                    |


## Example Routing Rule
![](/img/providers/routing/icepay.png)

## Test data

### Test cards

| Visa Test Cards  | Mastercard Test Cards | Result                                 |
|------------------|-----------------------|----------------------------------------|
| 4000000000001091 | 5200000000001096      | Successful Step Up Authentication      |
| 4000000000001000 | 5200000000001005      | Successful Frictionless Authentication |

### Test Bank Account

| Attribute   | Value                  |
|-------------|------------------------|
| BIC         | ABNANL2AMAR            |
| IBAN        | NL89 BANK 0123 4567 89 |
| Acc. Number | 123456789              |
| PIN         | 1234                   |
| TAN         | 1234                   |


## Test Information

To test any payment method supported by the ICEPAY you will need to choose it from PaymentIQ back office and after pay button is pressed you will be redirected to a payment specific page to complete payment.

Payment options supported by the ICEPAY: `AFTERPAY`, `CREDITCARD`, `IDEAL`, `CREDITCLICK`, `BANCONTACT`, `ONLINEUBERWEISEN`, `WECHATPAY`, `ALIPAY`, `SAFETYPAY`, `UNIONPAY`, `EPS`, `GIROPAY`, `WIRETRANSFER`, `DIRECTDEBIT`, `SOFORT`, `PAYPAL`, `POS`, `PAYSAFECARD`.

## How To Configure

1. Add `IcePayConfig`
2. Add `IcePay` to the "psps" section in `MerchantConfig`
3. Configure required `WEBREDIRECT` service(s) in `MerchantConfig`:

```xml
<entry>
    <string>WEBREDIRECT</string>
    <string>IDEAL|PAYSAFECARD|BANCONTACT|PAYPAL|...|CARD_REDIRECT</string>
</entry>
```

4. Enable required payment method(s) in PIQ BO (**Rules > Payment Methods**) e.g. WEBREDIRECT-IDEAL, WEBREDIRECT-PAYSAFECARD, ...
5. Configure routing rule.
