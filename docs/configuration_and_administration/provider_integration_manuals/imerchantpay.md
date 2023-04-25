--- 
id: "imerchantpay" 
title: "IMerchantPay"
hide_title: "true"
---
 
![](/img/providers/logos/imerchantpay.png)

# IMerchantPay

## About
IMerchantPay is a Bank provider that offers deposit, withdrawal and status check.

| Provider Name                | IMerchantPay                                                                    |
|------------------------------|---------------------------------------------------------------------------------|
| Link                         | [http://imerchantpay.co.uk/](http://imerchantpay.co.uk/)                        |
| Classification               | Online Banking                                                                  |
| Regions                      | `Australia`, `Norway`                                                           |
| Currencies                   | Please check directly with the provider regarding what currencies are supported |
| Methods/PaymentTxTypes       | `BankDeposit` <br/> `BankWithdrawal`                                            |
| PaymentIQ Configuration File | `IMerchantPayConfig`                                                            |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.imerchantpay.IMerchantPayConfig>
  <enabled>true</enabled>
  <useViqProxy>false</useViqProxy>
  <accounts>
    <entry>
      <string>DEFAULT</string>
      <account>
        <secretKey>??</secretKey>
        <merchantCode>??</merchantCode>
        <transactionChannel>BANK_TRANSFER</transactionChannel>
        <supportedCurrencies>AUD</supportedCurrencies>
      </account>
    </entry>
  </accounts>
  <container>iframe</container>
  <width>600</width>
  <height>600</height>
  <liveServiceEndPoint>https://app.imerchantpaydirect.com/api/transfer/v1/payIn</liveServiceEndPoint>
  <testServiceEndPoint>https://app.imerchantpaydirect.com/api/transfer/v1/payIn</testServiceEndPoint>
  <redirectUrl>${baseRedirectUrl}/api/imerchantpay/redirect/${ptx.txRefId}</redirectUrl>
  <callbackUrl>${baseCallbackUrl}/api/imerchantpay/callback/${ptx.txRefId}</callbackUrl>
  <defaultDescriptor>Bambora Payment</defaultDescriptor>
  <redirectionHtmlTemplateName>imerchantpay-repost-token-template</redirectionHtmlTemplateName>
  <version>3.0</version>
</com.devcode.paymentiq.integration.imerchantpay.IMerchantPayConfig>
```
</details>

### Attributes

| Attribute            | Description                                                |
|----------------------|------------------------------------------------------------|
| Merchant Key         | Provided by IMerchantPay to create a signature             |
| Merchant Code        | Provided by IMerchantPay to uniquely identify the Merchant |
| Supported Currencies | AUD, NOK                                                   |

### Limits
100k for ```AUD``` 

## Example Routing Rule
![](/img/providers/routing/imerchantpay.png)

## Transaction Flow
When user start the deposit s/he will presented with the following page:

![](/img/providers/imerchantpay01.png)

Select bank in drop down list and press PROCEED. Then Login dialog will be shown, where user will need to specify online banking details (User ID and Password) in order to complete payment:

![](/img/providers/imerchantpay02.png)

## Test Information

Please check directly with the provider.