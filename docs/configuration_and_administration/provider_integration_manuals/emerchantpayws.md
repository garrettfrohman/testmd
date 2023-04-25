--- 
id: "eMerchantPayWS" 
title: "eMerchantPay WS (Web Service API)"
hide_title: "true"
---
 
![](/img/providers/logos/emerchantpay.png)

# eMerchantPay WS (Web Service API)

## About
eMerchantPay WS is a card processor with support for Deposits, Withdrawals, Refunds and Voids.

| Provider Name                | eMerchantPay WS (Web Service API)                                               |
|------------------------------|---------------------------------------------------------------------------------|
| Link                         | [https://www.emerchantpay.com/](https://www.emerchantpay.com/)                  |
| Classification               | Debit/Credit Card Processor                                                     |
| Regions                      | `International`                                                                 |
| Currencies                   | Please check directly with the provider regarding what currencies are supported |
| Methods/PaymentTxTypes       | `CreditcardDeposit`<br/> `CreditcardWithdrawal`<br/> `Refund`<br/> `Void`       |
| PaymentIQ Configuration File | `EmerchantPayWSConfig`                                                          |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>

<br/>

```xml
<com.devcode.paymentiq.integration.emerchantpayws.EMerchantPayWsConfig>
  <enabled>true</enabled>
  <useViqProxy>true</useViqProxy>
  <accounts>
    <entry>
      <string>EMPWS_N3DS</string>
      <account>
        <serviceEndpoint>https://my.emerchantpay.com/service/</serviceEndpoint>
        <merchantId>??</merchantId>
        <secretKey>??</secretKey>
        <use3Dsecure>false</use3Dsecure>
        <useTokenId>true</useTokenId>
        <apiKey>??</apiKey>
        <supportedCurrencies>EUR</supportedCurrencies>
      </account>
    </entry>
    <entry>
      <string>EMPWS_3DS</string>
      <account>
        <serviceEndpoint>https://my.emerchantpay.com/service/</serviceEndpoint>
        <merchantId>??</merchantId>
        <secretKey>??</secretKey>
        <use3Dsecure>true</use3Dsecure>
        <useTokenId>false</useTokenId>
        <apiKey>??</apiKey>
        <supportedCurrencies>EUR</supportedCurrencies>
      </account>
    </entry>
  </accounts>
  <container>iframe</container>
  <width>1000</width>
  <height>800</height>
  <callbackUrl>${baseCallbackUrl}/api/emerchantpayws/deposit/callback/${ptx.txRefId}</callbackUrl>
  <defaultDescriptor>???</defaultDescriptor>
</com.devcode.paymentiq.integration.emerchantpayws.EMerchantPayWsConfig>
```

</details>

### Attributes

| Attribute                               | Description                                                                                                                         |
|-----------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------|
| merchantId                              | Provided by eMerchantPay WS                                                                                                         |
| secretKey                               | Provided by eMerchantPay WS                                                                                                         |
| apiKey                                  | Provided by eMerchantPay WS                                                                                                         |
| withdrawalCheckDepositAgainstPspAccount | When doing CreditcardWithdrawals, you can set a specific PSP account that the deposit should have been done with. Default is empty. |


## Example Routing Rule
![](/img/providers/routing/emerchantpayws.png)
![](/img/providers/routing/emerchantpayws2.png)

## Test Information

Mock User
- EMPWS

Amounts
- 1.00 EUR: APPROVED
- 1.01 EUR: DECLINED
- 2.00 EUR: 3DS NOT ENROLLED

The following test card numbers are valid for use with test transactions:

| Card Brand | Account          | CVV | Expiry date |
|------------|------------------|-----|-------------|
| VISA       | 4111111111111111 | Any | 01/2025     |
| MASTERCARD | 5500000000000004 | Any | 01/2025     |
| MASTERCARD | 2223000010059845 | Any | 01/2025     |

The following test card numbers are valid for use with test 3D Secure 1 and 2 transactions:

| Scenario                                              | 3DS2 Method | 3DS2 Challenge | 3DS1 PaRes | Result                  | Card Number      |
|-------------------------------------------------------|-------------|----------------|------------|-------------------------|------------------|
| Successful order with Frictionless with 3DS Method    | Y           | -              | -          | Authenticated           | 4066330000000004 |
| Failed order with Frictionless with 3DS Method        | Y           | -              | -          | Not Authenticated       | 4111112232423922 |
| Successful order with Frictionless without 3DS Method | -           | -              | -          | Authenticated           | 4012000000060085 |
| Failed order with Frictionless without 3DS Method     | -           | -              | -          | Not Authenticated       | 4111110000000922 |
| Challenge with 3DS Method                             | Y           | Y              | -          | Choose Challenge result | 4938730000000001 |
| Challenge without 3DS Method                          | -           | Y              | -          | Choose Challenge result | 4918190000000002 |
| 3DS1 Fallback with 3DS Method                         | Y           | -              | Y          | Choose PaRes response   | 4901164281364345 |
| 3DS1 Fallback without 3DS Method                      | -           | -              | Y          | Choose PaRes response   | 4901170000000003 |

Please also check here for additional test cards:

[https://emerchantpay.github.io/gateway-api-docs/#testing-3ds-v1](https://emerchantpay.github.io/gateway-api-docs/#testing-3ds-v1)
