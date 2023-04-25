--- 
id: "simplepay" 
title: "SimplePay"
hide_title: "true"
---
 
![](/img/providers/logos/simplepay.png)

# SimplePay

## About
SimplePay is a online cashless payment solution.


| Provider Name                | SimplePay                                             |
|------------------------------|-------------------------------------------------------|
| Link                         | [https://simplepay.hu/rolunk/](https://simplepay.hu/) |
| Classification               | Wallet                                                |
| Regions                      | `Hungary`                                             |
| Currencies                   | `HUF`                                                 |
| Methods/PaymentTxTypes       | `WebRedirectDeposit` <br/> `Refund`                   |
| PaymentIQ Configuration File | `SimplePayConfig`                                     |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.simplepay.SimplePayConfig>
  <enabled>true</enabled>
  <expirationTimeInSeconds>60</expirationTimeInSeconds>
  <methods>CARD|WIRE</methods>
  <accounts>
    <entry>
      <string>default</string>
      <account>
        <serviceEndpoint>https://sandbox.simplepay.hu/payment/v2/%s</serviceEndpoint>
        <merchantId>??</merchantId>
        <secretKey>??</secretKey>
        <container>window</container> <!--iframe is not supported-->
        <supportedCurrencies>HUF</supportedCurrencies>
      </account>
    </entry>
  </accounts>
  <testMode>true</testMode>
</com.devcode.paymentiq.integration.simplepay.SimplePayConfig>
```
</details>

### Attributes

| Attribute                | Description                                                                        |
|--------------------------|------------------------------------------------------------------------------------|
| expirationTimeInSeconds  | the time for which the transaction is valid, i.e. the time to initiate the payment |
| accountConfig.merchantId | the unique identifier of the merchant account in the SimplePay system.             |
| accountConfig.secretKey  | the unique secretKey of the merchant account in the SimplePay system.              |
| methods                  | Array of the payment method.                                                       |
| container                | Container of redirect page, window is only supported.                              |

### Callback configuration 

You need to specify the callback URL as well in "Account → Technical  → System notifications" section in a simplepay admin panel.

Test callback URL : https://test-api.paymentiq.io/paymentiq/api/simplepay/callback/

Production callback URL : https://api.paymentiq.io/paymentiq/api/simplepay/callback/

## Example Routing Rules
![](/img/providers/routing/simplepay.png)

## Transaction Flow
When user star the deposit s/he will presented with the following page:

![](/img/providers/simplepay.png)

After user enters credit card details s/he will be redirected to status page 

## Test Information
Payment page already filled with test card information
