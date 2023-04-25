--- 
id: "latpay" 
title: "Latpay (LPS)"
hide_title: "true"
---
 
![](/img/providers/logos/latpay.png)

# Latpay (LPS)

## About
Latpay is an aggregator that offers bank deposits.

| Provider Name                | Latpay                                                                           |
|------------------------------|----------------------------------------------------------------------------------|
| Link                         | [https://www.latpay.com/](https://www.latpay.com/)                               |
| Classification               | Aggregator                                                                       |
| Regions                      | `International`                                                                  |
| Currencies                   | `EUR`                                                                            |
| Methods/PaymentTxTypes       | `IdealDeposit` <br/> `WebRedirectDeposit` <br/> `BankDeposit` <br/> `EpsDeposit` |
| PaymentIQ Configuration File | `LatpayConfig`                                                                   |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>


```XML
<com.devcode.paymentiq.integration.latpay.LatpayConfig>
   <enabled>true</enabled>
   <useViqProxy>true</useViqProxy>
   <width>600</width>
   <height>350</height>
   <accounts>
    <entry>
     <string>default</string>
     <account>
        <merchantId>??</merchantId>
        <password>??</password>
        <supportedCurrencies>EUR</supportedCurrencies>
     </account>
    </entry>
  </accounts>
  <redirectUrl>??</redirectUrl>
  <callbackUrl>??</callbackUrl>
</com.devcode.paymentiq.integration.latpay.LatpayConfig>
```
</details>

### Attributes


| Attribute              | Description                                                       | Required |
|------------------------|-------------------------------------------------------------------|----------|
| merchantId             | Merchant user id on Latpay side                                   | Yes      |
| password               | Merchant password on Latpay side                                  | Yes      |
| secretKey              | `reply_password` provided by Merchant to LPS during account setup | Yes      |
| redirectUrl            | Id of redirect url on Latpay side                                 | Yes      |
| callbackUrl            | Id of callback url on Latpay side                                 | Yes      |
| testServiceCodeMapping | Mapping of paymentiq service and Latpay service code for test     | No       |
| liveServiceCodeMapping | Mapping of paymentiq service and Latpay service code for live     | No       |

### APM Deposit

| APM          | TxType                             | Service      |
|--------------|------------------------------------|--------------|
| iDEAL        | IdealDeposit or WebRedirectDeposit | IDEAL        |
| EPS          | EpsDeposit or BankDeposit          | EPS          |
| Bancontact   | BankDeposit or WebRedirectDeposit  | BANCONTACT   |
| Verkkopankki | BankDeposit or WebRedirectDeposit  | VERKKOPANKKI |

### Callback and redirect url

The callback and redirect urls has to be provided to Latpay. Latpay will then give back a uniqe id for that url so that can be set in LatpayConfig for the redirectUrl and callbackUrl fields.

#### Redirect url

| Environment | Url                                                         |
|-------------|-------------------------------------------------------------|
| Test        | https://test-api.paymentiq.io/paymentiq/api/latpay/redirect |
| Live        | https://api.paymentiq.io/paymentiq/api/latpay/redirect      |

#### Callback url

| Environment | Url                                                         |
|-------------|-------------------------------------------------------------|
| Test        | https://test-api.paymentiq.io/paymentiq/api/latpay/callback |
| Live        | https://api.paymentiq.io/paymentiq/api/latpay/callback      |


## Example Routing Rule

![](/img/providers/routing/latpay.png)

## Test Information

### iDEAL

Currency: `EUR` and Country: `NLD`.

The iDEAL workflow is mocked in testmode.
* Successful transaction just enter any valid input and finish the transaction.
* Failed transaction click on `Abort`

### EPS

Currency: `EUR` and Country: `AUT`

The EPS workflow is mocked in testmode.
* For a successful transaction select `Succeeded` at the simulator.
* For a failed transaction select one of the `Failed` at the simulator.

### Bancontact

Currency: `EUR` and Country: `BEL`

The Bancontact workflow is mocked in testmode.
* For a successful transaction select `Succeeded` at the simulator.
* For a failed transaction select one of the `Failed` at the simulator.

### Verkkopankki

Currency: `EUR` and Country: `FIN`

The Verkkopankki workflow is mocked in testmode.
* For a successful transaction select `Succeeded` at the simulator.
* For a failed transaction select one of the `Failed` at the simulator.
