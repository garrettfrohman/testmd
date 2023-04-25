--- 
id: "klarna" 
title: "Klarna"
hide_title: "true"
---
 
![](/img/providers/logos/sofort.png)

# Klarna

## About
Klarna is a sofort solution with invoice option. Supporting Auth, Capture, Deposit, Void and Refund.

| Provider Name                | Klarna                                                                                    |
|------------------------------|-------------------------------------------------------------------------------------------|
| Link                         | [https://www.klarna.com/](https://www.klarna.com/)                                        |
| Classification               | Online Banking                                                                            |
| Regions                      | `Norway`,`The Netherlands`,`Denmark`,`Germany`,`Austria`,`Finland`,`Sweden`,`Switzerland` |
| Currencies                   | Please check directly with the provider regarding what currencies are supported           |
| Methods/PaymentTxTypes       | `KlarnaDeposit`<br/>`KlarnaTermsDeposit`<br/> `Void`<br/> `Refund`<br/>`Capture`          |
| PaymentIQ Configuration File | `KlarnaConfig`                                                                            |



## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.klarna.KlarnaConfig>
  <enabled>true</enabled>
  <useViqProxy>false</useViqProxy>
  <accounts>
    <entry>
      <string>default</string>
      <account>
        <supportedCurrencies>EUR|SEK</supportedCurrencies>
        <username>??</username>
        <password>??</password>
        <authType>AUTH_CAPTURE</authType>
        <showTerms>false</showTerms>
        <!-- <service>PAY_LATER</service>-->
      </account>
    </entry>
  </accounts>
  <container>window</container>
</com.devcode.paymentiq.integration.klarna.KlarnaConfig>
```
</details>

### Attributes

| Attribute    | Description                                                                                                                                                    |
|--------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| username     | Will be provided by Klarna as API username.                                                                                                                    |
| password     | Will be provided by Klarna as API password.                                                                                                                    |
| authType     | Work same as any other provider. But direct capture is not instant.                                                                                            |
| templateName | Template name in case one needs to customize select payment methods page.                                                                                      |
| service      | Refer to different Klarna payment option can be one of the following options `DIRECT_DEBIT`, `DIRECT_BANK_TRANSFER`, `PAY_NOW`, `PAY_LATER` or `PAY_OVER_TIME` |
| showTerms    | Bypass the step that show terms and conditions if a service is selected.                                                                                       |

### Notes

- Klarna utilizes PaymentIQ E-Commerce input `OrderInformation`. But use of this object is completely optional, yet will improve customer's experience.
In addition to that, merchants can forward `acquiringChannel`, `klarnaAttachment`, and `vatId`, using input attributes with same names if needed.

- You can use a service parameter in the input or in the accountConfig to show only that option.
You can also set `showTerms` to `false` to not show terms, and instead open the payment directly if service is set.

### Zero Amount Transaction

KlarnaTermsDeposit is a deposit with any amount, but will end up with zero amount (no-payment-transaction). 

After this transaction, the merchant can `POST` to `api/klarnaterms/{txRefId}/{service}` to receive a standard output to redirect to terms and conditions of specific service of Klarna. 

Or alternatively `POST` to `api/klarnaterms/{txRefId}` to receive a standard output to redirect to terms and conditions of specific service of Klarna picked from accountConfig `<service>`.

## Example Routing Rule
![](/img/providers/routing/klarna2.png)

## Test Information
Complete  test information of different markets can be found at:

[https://developers.klarna.com/](https://developers.klarna.com/documentation/test-credentials/#sample-data)

You can also use any Sofort test data for `SofortDeposit`