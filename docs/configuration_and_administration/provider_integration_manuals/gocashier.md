--- 
id: "gocashier" 
title: "GoCashier"
hide_title: "true"
---
 
![](/img/providers/logos/gocashier.png)

# GoCashier

## About
GoCashier is a HK based payment service provider offering 3DS/N3DS Deposit, Refund and Status Check.

| Provider Name                | GoCashier                                                                       |
|------------------------------|---------------------------------------------------------------------------------|
| Link                         | [https://www.gocashier.com/](https://www.gocashier.com/)                        |
| Classification               | Debit/Credit Card Processor                                                     |
| Blocked Countries            | China, Hong Kong, Ghana, Nigeria, Singapore, Turkey, Norway                     |
| Currencies                   | Please check directly with the provider regarding what currencies are supported |
| Methods/PaymentTxTypes       | `CreditcardDeposit`<br/>`Refund`                                                |
| PaymentIQ Configuration File | `GoCashierConfig`                                                               |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.gocashier.GoCashierConfig>
  <enabled>true</enabled>
  <useViqProxy>true</useViqProxy>
  <version>v2</version>
  <accounts>
    <entry>
      <string>DEFAULT</string>
      <account>
        <merchantNumber>xxxxx</merchantNumber>
        <gatewayNo>####</gatewayNo>
        <secretKey>??</secretKey>
        <productName>Test Product</productName>
        <supportedCurrencies>EUR</supportedCurrencies>
      </account>
    </entry>
  </accounts>
  <testMode>true</testMode>
  <container>iframe</container>
  <!--<width>900</width>
  <height>600</height>-->
  <defaultDescriptor>Bambora payment ${ptx.txRefId}</defaultDescriptor>
</com.devcode.paymentiq.integration.gocashier.GoCashierConfig>
```
</details>

### Attributes

| Attribute                 | Description                                                                                                                                                                                    |
|---------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| account.merchantNumber    | Corresponds to the merchant number (`merNo` request parameter) from the GoCashier and is used to authenticate a merchant.                                                                      |
| account.gatewayNo         | Corresponds to the gateway number (`gatewayNo` request parameter) from the GoCashier and is used to authenticate a merchant. For N3DS and 3DS operations a different `gatewayNo` must be used. |
| account.secretKey         | Corresponds to the sign key from the GoCashier and is used to encode requests.                                                                                                                 |
| account.productName       | Name of product in the cart (optional).                                                                                                                                                        |
| account.defaultDescriptor | It can be used to specify a `remark` request parameter (optional).                                                                                                                             |
| version                   | Version of the provider API to be used. "v2" is the latest API version. If the value is other then "v2" or none - older version of the provider API will be attempted to be used.              |

### Notes
Secret Key can be found in the provider's [back office](https://mer.gocashier.com/mer/user/login.action):  Account Info > Merchant Information.

![](/img/providers/gocashier_bo.png)

## Example Routing Rule
![](/img/providers/routing/gocashier.png)

## Test Information

3DS Deposit and Refund can be tested on Production only.

### Test Cards

| Card Type  | Card Name | Card Number      | Expiry Date | CVV | Result     |
|------------|-----------|------------------|-------------|-----|------------|
| MasterCard | Any       | 5123450000000008 | Any         | Any | Successful |
| MasterCard | Any       | 5200000000001096 | Any         | Any | Declined   |
