--- 
id: "paymentasia" 
title: "PaymentAsia"
hide_title: "true"
---
 
![](/img/providers/logos/paymentasia.png)

# PaymentAsia

## About
PaymentAsia is a payment provider offering internal and external bank payment operations:

- DragonPay: deposit and withdrawal
- NganLuong: deposit and withdrawal

Currently only DragonPay deposits is integrated via PaymentIQ.

| Provider Name                | PaymentAsia                                                        |
|------------------------------|--------------------------------------------------------------------|
| Link                         | [https://www.paymentasia.com/en/](https://www.paymentasia.com/en/) |
| Classification               | Online/Manual Banking                                              |
| Regions                      | Philippines                                                        |
| Currencies                   | `PHP`                                                              |
| Limits                       | DEPOSIT: Min=`2,500 PHP`; Max=`250,000 PHP`;                       |
| Methods/PaymentTxTypes       | `WebRedirectDeposit`                                               |
| PaymentIQ Configuration File | `PaymentAsiaConfig`                                                |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.paymentasia.PaymentAsiaConfig>
  <enabled>true</enabled>
  <useViqProxy>false</useViqProxy>
  <accounts>
    <entry>
      <string>DEFAULT</string>
      <account>
        <merchantCode>??</merchantCode> <!--Merchant Token-->
        <secretKey>??</secretKey>       <!--Secret Code-->
        <paymentCode>??</paymentCode>   <!--For NganLuong Pay only: ATM_ONLINE(Default), IB_ONLINE-->
        <bankCode>??</bankCode>         <!--For VND solution only-->
        <supportedCurrencies>PHP</supportedCurrencies>
      </account>
    </entry>
  </accounts>
  <container>window</container>
  <defaultDescriptor>Bambora Payment: ${ptx.txRefId}</defaultDescriptor>
</com.devcode.paymentiq.integration.paymentasia.PaymentAsiaConfig>

```
</details>

### Attributes

| Attribute    | Description                                                                                                   |
|--------------|---------------------------------------------------------------------------------------------------------------|
| merchantCode | Corresponds to *Merchant Token* from PaymentAsia. It is used to build a correct request URL                   |
| secretKey    | Corresponds to *Secret Code* from PaymentAsia. It is used to build a request signature                        |
| paymentCode  | Corresponds to "Payment Method" from PaymentAsia. For NganLuong Pay only: `ATM_ONLINE` (Default), `IB_ONLINE` |
| bankCode     | Corresponds to "Bank Code" from PaymentAsia. For `VND` solution only                                          |

Merchant info (Merchant Token and Secret Code) can be found on the portal at https://merchant.pa-sys.com/merchant/info

### Callback URL

Callback URL can be set by the provider only.

TEST:  https://test-api.paymentiq.io/paymentiq/api/paymentasia/callback<br/>
PROD:  https://api.paymentiq.io/paymentiq/api/paymentasia/callback

## Example Routing Rule
![](/img/providers/routing/paymentasia.png)

## Test Information

1. Payment can only be made from Philippines IP.
2. There is no TEST env. and testing must be performed using real accounts.

### How can we test it (from non PH IP)?

You can initiate DragonPay deposit from our cashier and once it is done user will be redirected to

![](/img/providers/paymentasia_dragonpay_deposit.png)

Don't press "Pay Now" button. Instead copy the URL by right clicking on it e.g. https://payment.pa-sys.com/app/page/e7ed66a0-4651-4478-bc1a-b5c75a34ff4d/ecf17b19-eae6-42e1-ae8a-446ce7b11152/ and send it to merchant that has Philippines IP and can process payment.
Once payment is processed you should receive email (to your user's email) with payment status (see below)

![](/img/providers/paymentasia_dragonpay_deposit_status.png)
