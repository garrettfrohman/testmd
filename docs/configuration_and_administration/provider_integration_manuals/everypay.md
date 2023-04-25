---
id: "everypay"
title: "EveryPay"
hide_title: "true"
---

![](/img/providers/logos/everypay.png)

# Everypay

## About
EveryPay is a payment provider offering a credit card payment operation via web redirection and status check.

| Provider Name                | EveryPay                                         |
|------------------------------|--------------------------------------------------|
| Link                         | [https://every-pay.com/](https://every-pay.com/) |
| Classification               | Debit/Credit Card Processor                      |
| Regions                      | `Europe`                                         |
| Currencies                   | `EUR`                                            |
| Methods/PaymentTxTypes       | `WebRedirectDeposit`                             |
| PaymentIQ Configuration File | `EveryPayConfig`                                 |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.everypay.EveryPayConfig>
  <enabled>true</enabled>
  <testMode>false</testMode>
  <accounts>
    <entry>
     <string>DEFAULT</string>
     <account>
       <accountID>??</accountID>  <!--Processing Account-->
       <username>??</username>    <!--API username-->
       <password>??</password>    <!--API secret-->
       <method>card</method>
       <supportedCurrencies>EUR</supportedCurrencies>
     </account>
    </entry>
  </accounts>
  <!--<container>window</container>-->
</com.devcode.paymentiq.integration.everypay.EveryPayConfig>
```

</details>

### Attributes

| Attribute         | Description                                                                                                                                                                                                                                                                                                                                                                                  |
|-------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| account.accountID | Corresponds to the `Processing Account` (account id/name) from the EveryPay, that is used as a `account_name` request parameter. It can be found in EveryPay portal under "Processing Accounts" section.                                                                                                                                                                                     |
| account.username  | Corresponds to the `API username` from the EveryPay, that is used as a `api_username` request parameter, and is also used to authorize  requests. It can be found in EveryPay portal under "General Settings" section.                                                                                                                                                                       |
| account.password  | Corresponds to the `API secret` from the EveryPay, that is used to authorize  requests. It can be found in the EveryPay portal under "General Settings" section.                                                                                                                                                                                                                             |
| account.method    | Optional parameter, that can be used to specify which payment method to trigger. PSP service can also be used to identify which payment option should be triggered. In case no `method` is configured and PSP service is missing, user will be redirected to the page with all available payment options.<br/>Example: `<method>card</method>` (the same as it is defined at provider side). |
| container         | Optional parameter to identify container type. Possible values are: `window`, `iframe` (`iframe` is used by default).
| pspServiceMapping | Conditional parameter, that can be used to define a mapping between PSP service and payment method name (`payment_methods/source` parameter). It is required in case PSP service was sent in the payment request.<br/>In order to configure it properly, you will need to clarify with provider which payment options are enabled for your account. Then you can check with PaymentIQ technical support to see if mapping should be updated.<br/>This mapping is defined by default: `CREDITCARD->card`, meaning, in order to trigger card payment method, you will need to send `service=CREDITCARD`. |

### Callback URLs

Callback URL should be configured in the EveryPay portal under "E-Shop Settings" (select your shop and scroll to the bottom)<br/>
Callback URL examples:

TEST: `https://test-api.paymentiq.io/paymentiq/api/everypay/callback`<br/>
PROD: `https://api.paymentiq.io/paymentiq/api/everypay/callback`

## Example Routing Rule

![](/img/providers/routing/everypay.png)

## Test Information

Credit card deposit can be initiated using `WebRedirectDeposit` tx type. In such case user will be redirected to the provider page to specify card data and complete 3DS validation.

### Test Cards

| Card Type   | Card Number      | Expiry Date | CVV | Cardholder name | 3DS Password | Result  |
|-------------|------------------|-------------|-----|-----------------|--------------|---------|
| Master Card | 5168830759303438 | 10/24       | 418 | Any             | Secret!33    | Success |
| Master Card | 5168830721419445 | 10/24       | 528 | Any             | Secret!33    | Success |
| Visa        | 4051700003921116 | 12/22       | 137 | Any             | Secret!33    | Success |
| Master Card | 5413330089020029 | Any         | Any | Any             | Secret!33    | Failed  |
