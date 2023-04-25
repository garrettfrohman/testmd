--- 
id: "vipps" 
title: "Vipps (via BamboraGA)"
hide_title: "true"
---
 
![](/img/providers/logos/vipps.png)

# Vipps (via BamboraGA)

## About
Vipps is Norwegian mobile payment service.
Vipps is an application that gives the user the possibility to make payments to a receiver's telephone number instead of an account number.

| Provider Name                | Vipps                                          |
|------------------------------|------------------------------------------------|
| Link                         | [https://www.vipps.no/](https://www.vipps.no/) |
| Classification               | Mobile Payment                                 |
| Region                       | `Norway`                                       |
| Currency                     | `NOK`                                          |
| Method/PaymentTxType         | `VippsDeposit`                                 |
| PaymentIQ Configuration File | `VippsConfig`                                  |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.vipps.VippsConfig>
  <enabled>true</enabled>
  <useViqProxy>true</useViqProxy>
  
  <accounts>
    <entry>
      <string>DEFAULT</string>
      <account>
        <merchantId>??</merchantId>
        <supportedCurrencies>NOK</supportedCurrencies>
      </account>
    </entry>
  </accounts>

</com.devcode.paymentiq.integration.vipps.VippsConfig>
```
</details>

### Attributes

| Attribute       | Description                                                                                                                                                                                                                            |
|-----------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| merchantId      | Account level: Unique merchant id in Vipps system                                                                                                                                                                                      |
| skipLandingPage | Root level: `Only available for whitelisted sale units`. If this property is set to `true`, it will cause a push notification to be sent to the given phone number immediately, without loading the landing page. Defaults to `false`. |
| recurring       | Account level: Used to enable recurring payments. Defaults to `false`. More info about `Reccurring payments` can be found [here](https://github.com/vippsas/vipps-psp-api/blob/master/vipps-psp-api.md#recurring-payments)             |
| agreementUrl    | Root level: Used to configure agreement URL for recurring payments                                                                                                                                                                     |

## Example Routing Rule

![](/img/providers/routing/vipps.png)

## Transaction Flow

![](/img/providers/vipps_flow.png)

## Test Information

For testing required to have test mobile app installed. It can be downloaded from [https://github.com/vippsas/vipps-developers/blob/master/vipps-test-environment.md#vipps-test-apps](https://github.com/vippsas/vipps-developers/blob/master/vipps-test-environment.md#vipps-test-apps).
Test phone number should be provided by Vipps. Normal Vipps user is not available in the test environment.

For test mobile app you can use next test data:

| Test phone | Pin  |
|------------|------|
| 48060312   | 1236 |

And test card:

| Card             | CVV | Expiry date |
|------------------|-----|-------------|
| 4925563035662932 | 123 | 12/2025     |


For different error cases it's possible to extend `BamboraGaConfig` with `<mockVippsResponse>true</mockVippsResponse>` on root level and use next transaction amounts:

| Amount | Error                         |
|--------|-------------------------------|
| 1.10   | Card Expired                  |
| 1.11   | The merchant was not found    |
| 1.12   | Declined because of fraud     |
| 1.13   | Bank has declined transaction |
| 1.14   | Invalid amount                |
| 1.15   | Bad request                   |
| 1.16   | Invalid issuer                |
| 1.17   | Card reported lost or stolen  |
| 1.18   | Restricted card               |
| 1.19   | Not unique transaction ID     |
| 1.20   | Provider is out of service    |
| 1.21   | Invalid CVV                   |

Transaction with any other amount, with mentioned config, will be successful.

### Magic numbers for non-mocked processing
Particular amount values has to be used to process transactions correctly on test.

Please refer to Vipps documentation to check amount and corresponding behaviour: 

https://github.com/vippsas/vipps-psp-api/blob/master/vipps-psp-api.md#magic-numbers-for-emvco-tokens
