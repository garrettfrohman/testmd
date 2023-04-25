---
id: "paypal" 
title: "PayPal"
hide_title: "true"
---

![](/img/providers/logos/paypal.png)

# PayPal

## About
PayPal allows any business or individual with an email address to securely, conveniently and cost-effectively send and receive payments online. Their network builds on the existing financial infrastructure of bank accounts and credit cards to create a global, real-time payment solution. They deliver a product ideally suited for small businesses, online merchants, individuals and others currently underserved by traditional payment mechanisms.

The size of their network and widening acceptance of their product have helped them become one of the leading payment networks for online auction websites. PayPal is also being increasingly used on other ecommerce sites for the sale of goods such as electronics and household items, the sale of services such as web design and travel, and the sale of digital content. Offline businesses, including lawyers, contractors and doctors, have increasingly begun to receive payments online through PayPal. PayPal's service, which lets users send payments for free, can be used from computers or web-enabled mobile phones.

| Provider Name                | PayPal                                                                          |
|------------------------------|---------------------------------------------------------------------------------|
| Link                         | [https://www.paypal.com](https://www.paypal.com)                                |
| Classification               | Wallet                                                                          |
| Regions                      | `International`                                                                 |
| Currencies                   | Please check directly with the provider regarding what currencies are supported |
| Methods/PaymentTxTypes       | `PayPalDeposit`, `PayPalWithdrawal`, `Refund`                                   |
| PaymentIQ Configuration File | `PayPalConfig`                                                                  |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.paypal.PayPalConfig>
  <enabled>true</enabled>
  <container>window</container>
  <accounts>
    <entry>
      <string>???</string>
      <account>
        <accountID>???</accountID>
        <username>??email??</username>
        <password>??10 digits??</password>
        <secretKey>??</secretKey>
        <serviceEndpoint>https://api-3t.paypal.com/nvp</serviceEndpoint>
        <redirectUrl>https://www.paypal.com/cgi-bin/webscr?cmd=_express-checkout&amp;token=</redirectUrl>
        <quickDeposit>true</quickDeposit> <!-- will turn the paypal button from continue to pay now -->
      </account>
    </entry>
  </accounts>
  <paymentDescription>devCode</paymentDescription>
</com.devcode.paymentiq.integration.paypal.PayPalConfig>
```
</details>

### Attributes

| Attribute                    | Description                                                                                                                                     |
|------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------|
| accountId                    | The PayPAl Merchant Account ID                                                                                                                  |
| username                     | The API Username                                                                                                                                |
| password                     | The API Password                                                                                                                                |
| secretKey                    | The API Signature                                                                                                                               |
| quickDeposit                 | Enables PayPal Quickdeposit if set to `true`. This will change the PayPal button from 'Continue' to 'Pay Now'                                   |
| allowWithdrawalBeforeDeposit | Needed if you want to allow withdrawals before any deposit has been made by the customer / end-user                                             |
| useTokenId                   | A boolean value for activating repeat payment using Reference Transaction API if set to `true`.                                                 |
| billingType                  | Repeat payment requires sending the billing type. The value of `billingType` attribute should be `MerchantInitiatedBilling`                     |
| version                      | Repeat payment requires sending the version of Reference Transaction API. The value of `version` attribute should be `MerchantInitiatedBilling` |

### Credentials
As noted above there are four different credentials needed.
It’s important that the API certificate is set up as “API Signature” instead of “API Fingerprint”.
If you as a customer already have a fingerprint value, please delete the certificate and generate a new with the API signature version.

### Activating IPN Notifications (callback notifications)
Please follow PayPal’s guide:

[https://developer.paypal.com/docs/api-basics/notifications/ipn/](https://developer.paypal.com/docs/api-basics/notifications/ipn/)

And provide Notification URL:

Production: [https://api.paymentiq.io/paymentiq/api/paypal/message/ipn](https://api.paymentiq.io/paymentiq/api/paypal/message/ipn)

Test: [https://test-api.paymentiq.io/paymentiq/api/paypal/message/ipn](https://test-api.paymentiq.io/paymentiq/api/paypal/message/ipn)

### Activating repeat deposits 

To enable repeat payment (i.e., Customer Initiated Request), you need to have FraudNet and Reference Transaction APIs activated for you account. Kindly, please check with your key account manager at PayPal side to have your credintials activated.

To enable customer initiated repeat payment through PaymentIQ front-end API, you basically have to implement FraudNet script at your cashier side [https://developer.paypal.com/docs/limited-release/fraudnet/](https://developer.paypal.com/docs/limited-release/fraudnet/) and then submit the repeat payment request to PaymentIQ front-end API. If you didn't implement the FraudNet api at your cashier, you should not use the Reference Transaction API (repeat payment from Paypal side).

FraudNet API is based on JavaScript, which passes parameters to FraudNet side. All FraudNet parameters except parameter `s` and parameter `f` are optional. After fetching the value of `s` and `f` from FraudNet side, `s` and `f` parameters should be mapped to PaymentIQ request via new parameters or attributes names:

- `s` represents a password that has a static value, which is provided by your account manager at PayPal side.
- please note that `fraudnetRiskSessionCorrelationId` represents the value of `f`, which is generated from your cashier side after implementing the fraudnet at your cashier side. 
- You should make sure to send us `fraudnetRiskSessionCorrelationId` in either the attributes of your request OR as parameter of your json body (which is optional) when sending the request to `../paymentiq/api/paypal/deposit/process`

<details><summary>Click to view request body example with `fraudnetRiskSessionCorrelationId` as a parameter</summary>
<p>

```jsonc
{
   "merchantId":"1",
   "userId":"EUR_MRG",
   "sessionId":"asdasd",
   "amount":"1",
   "accountId":"0fc7fc77-f10b-45f8-b439-fd4e6bb65fcc",
   "attributes":{
      "successUrl":"http://localhost:9000#redirect?txId=1A1231231",
      "failureUrl":"http://localhost:9000#redirect?txId=1A1231231"
   },
   "email":null,
   "storeAccount":true,
   "fraudnetRiskSessionCorrelationId":"XXXXXXXXXX"
}
```
</p>
</details>

<details><summary>Click to view request body example with `fraudnetRiskSessionCorrelationId` as an attribute</summary>
<p>

```jsonc
{
   "merchantId":"1",
   "userId":"EUR_MRG",
   "sessionId":"asdasd",
   "amount":"1",
   "accountId":"0fc7fc77-f10b-45f8-b439-fd4e6bb65fcc",
   "attributes":{
      "successUrl":"http://localhost:9000#redirect?txId=${ptx.id}",
      "failureUrl":"http://localhost:9000#redirect?txId=${ptx.id}",
      "fraudnetRiskSessionCorrelationId":"XXXXXXXXXX"
   },
   "email":null,
   "storeAccount":true
}
```
</p>
</details>

## PaymentIQ configuration 

The merchant should have a separate account config for repeat payment in `PayPalConfig`. 

<details><summary>Click to view example configuration for repeat payment</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.paypal.PayPalConfig>
  <enabled>true</enabled>
  <container>window</container>
  <accounts>
    <entry>
      <string>???</string>
      <account>
        <accountID>???</accountID>
        <username>??email??</username>
        <password>??10 digits??</password>
        <secretKey>??</secretKey>
        <serviceEndpoint>https://api-3t.paypal.com/nvp</serviceEndpoint>
        <redirectUrl>https://www.paypal.com/cgi-bin/webscr?cmd=_express-checkout&amp;token=</redirectUrl>
        <useTokenId>true</useTokenId>
        <billingType>MerchantInitiatedBilling</billingType> <!-- it is already the default value, but it can be explicitly set to MerchantInitiatedBilling-->
        <version>121</version> <!-- the earlier used version is 106 -->
        <container>iframe</container>
      </account>
    </entry>
  </accounts>
  <paymentDescription>devCode</paymentDescription>
</com.devcode.paymentiq.integration.paypal.PayPalConfig>
```
</details>

Also, the merchant should either add the inputs `fraudnetRiskSessionCorrelationId` and `fraudnetSwebsiteSourceIdentifier` to the Cashier Payment Method-settings (see example below) OR the merchant should submit `fraudnetRiskSessionCorrelationId` and `fraudnetSwebsiteSourceIdentifier` as attributes as mentioned earlier.

![](/img/providers/paypal-paymentmethod.png)

### Allowing withdrawals before deposits

By default it is not possible to perform a PayPal withdrawal without a previous successful deposit, however, it is possible to enable this functionality if you as a merchant has been cleared to do so by PayPal.

To enable this feature the entry `<allowWithdrawalBeforeDeposit>true</allowWithdrawalBeforeDeposit>` has to be added to the PayPalConfig, either to the root level or to a specific account.

**Note** that for this to work the `email` parameter has to be sent in the withdrawal process request to PIQ. (Find the PayPal parameters for the Front API ewallet section)

## Example Routing Rule
![](/img/providers/routing/paypal.png)
## Test Information

| Currency | Email           | Password  |
|----------|-----------------|-----------|
| EUR      | eur@devcode.se  | gmsmotwlB |
| GBP      | gbp1@devcode.se | gmsmotwlB |
