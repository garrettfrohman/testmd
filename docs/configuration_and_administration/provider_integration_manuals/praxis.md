--- 
id: "praxis" 
title: "Praxis"
hide_title: "true"
---
 
![](/img/providers/logos/praxis.png)

# Praxis

## About
Praxis Cashier is a technology provider that has developed the ultimate smart cashier software designed with Fintech, Online Gaming, Travel and E-commerce businesses in mind. Praxis Cashier software was designed to overcome high-risk processing difficulties, bring industrial peace to companies and increase businesses' transaction approval rates by over 15%.

| Provider Name                | Praxis                                                                                                                  |
|------------------------------|-------------------------------------------------------------------------------------------------------------------------|
| Link                         | [https://www.praxiscashier.com/](https://www.praxiscashier.com/)                                                        |
| Classification               | Debit/Credit Card Processor                                                                                             |
| Regions                      | `International`                                                                                                         |
| Currencies                   | Please check directly with the provider regarding what currencies are supported                                         |
| Methods/PaymentTxTypes       | `CreditcardDeposit`, `CreditcardWithdrawal`, `Refund`, `Capture`, `Void`, `WebRedirectDeposit`, `WebRedirectWithdrawal` |
| PaymentIQ Configuration File | `PraxisConfig`                                                                                                          |


## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.praxis.PraxisConfig>
  <enabled>true</enabled>
  <useViqProxy>true</useViqProxy>
  <accounts>
    <entry>
      <string>DEFAULT</string>
      <account>
        <merchantId>??</merchantId><!--merchant_id-->
        <secretKey>??</secretKey><!--merchant_secret-->
        <profileId>??</profileId><!--application_key-->
        <supportedCurrencies>??</supportedCurrencies>
        <gatewayNo>??</gatewayNo>
      </account>
    </entry>
  </accounts>
  <testMode>true</testMode>
  <defaultDescriptor>DevCode payment</defaultDescriptor>
</com.devcode.paymentiq.integration.praxis.PraxisConfig>
```

</details>

### Attributes

| Attribute                | Description                                                                                                                         |
|--------------------------|-------------------------------------------------------------------------------------------------------------------------------------|
| accountConfig.merchantId | Corresponds to the *merchant_id* from Praxis. Unique ID assigned to merchant by Praxis.                                             |
| accountConfig.secretKey  | Corresponds to the *merchant_secret* from Praxis. It is used to build a request signature.                                          |
| accountConfig.profileId  | Corresponds to the *application_key* from Praxis. Corresponding key to *merchant_id*.                                               |
| accountConfig.gatewayNo  | Corresponds to the *gateway hash* from Praxis. It is used to identify a payment option (APM) at Praxis side (Trustly, EPS and etc.) |
| variable1                | Provided by Praxis for Praxis' internal routing. Can be added both on root and account level.                                       |
| variable2                | Provided by Praxis for Praxis' internal routing. Can be added both on root and account level.                                       |
| variable3                | Provided by Praxis for Praxis' internal routing. Can be added both on root and account level.                                       |

### Notes
- If you have one merchant account at Praxis with different payment options (APMs) enabled, you should use the same merchantId, secretKey and profileId for all your APMs (Payop, EPS, Klarna and etc.). For example account configs for Payop and EPS will be almost the same and the different will be "gatewayNo" only.
- Payment method is identified via gateway hash ("gatewayNo" in the PraxisConfig). Each APM has its unique hash.
- Account config variable(1/2/3) are more prioritised over root variable(1/2/3)
- In order to avoid currency manipulations on our end it is desired to turn off option of changing processing currency of current transaction on Praxis side when WebRedirect methods are performed. Please reach out to Praxis for further information on how to do this.
- Some merchants require 3DS2 to be enabled for `CreditcardDeposit` to work properly. Below you can see the picture of 3DS routing setup.

## Example Routing Rule
![](/img/providers/routing/praxis.png)

## Example 3DS2 Routing Rule
Can be set here: Rules -> Routing -> 3DS2 Provider
![](/img/providers/routing/praxis_3ds2.png)

## Test Information

| Card Number      | CVV | Expiry Date     |
|------------------|-----|-----------------|
| 4024007109805399 | 568 | Any future date |
| 5393470277337555 | 568 | Any future date |
| 6011522728832400 | 568 | Any future date |

NOTE: Any valid card number can be used for transactions, but CVV must be always "568".
