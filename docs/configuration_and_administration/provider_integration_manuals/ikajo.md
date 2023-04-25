--- 
id: "ikajo" 
title: "IKajo"
hide_title: "true"
---
 
![](/img/providers/logos/ikajo.png)

# IKajo

## About
IKajo is a payment provider offering creditcard deposit (Auth and Capture or directCapture)(3DS and non 3DS, depending on card), void and full/partial refund.

| Provider Name                | IKajo                                                          |
|------------------------------|----------------------------------------------------------------|
| Link                         | [https://www.ikajo.com/](https://www.ikajo.com/)               |
| Classification               | Debit/Credit Card Processor                                    |
| Regions                      | International                                                  |
| Currencies                   | `EUR`,`USD`                                                    |
| Methods/PaymentTxTypes       | `CreditcardDeposit`<br/>`Capture`<br/>`Refund`<br/>`Void`<br/> |
| PaymentIQ Configuration File | `IKajoConfig`                                                  |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.ikajo.IKajoConfig>
  <enabled>true</enabled>
  <useViqProxy>true</useViqProxy>
  <testMode>true</testMode>
  <width>800</width>
  <height>850</height>
  <accounts>
    <entry>
      <string>default</string>
      <account>
        <merchantId>???</merchantId>
        <password>???</password>
        <useTokenId>true</useTokenId>
        <supportedCurrencies>USD|EUR</supportedCurrencies>
        <authType>AUTH_CAPTURE</authType>
        <!--Options: AUTH_CAPTURE/FINAL_AUTH/PRE_AUTH-->
        <defaultDescriptor>test</defaultDescriptor>
      </account>
    </entry>
  </accounts>
</com.devcode.paymentiq.integration.ikajo.IKajoConfig>
```
</details>

### Attributes

| Attribute         | Description                                                                                                                                                                         |
|-------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| merchantId        | Corresponds to merchantId or client key from IKajo. It identifies a merchant on IKajo's end.                                                                                        |
| password          | Corresponds to password or client Pass from IKajo. It is used to sign requests and verify callbacks sent from and to IKajo.                                                         |
| useTokenId        | If set to true: payment with token will be used(where the user will enter card info only the first time he/she wants to pay).                                                       |
| authType          | If set to  AUTH_CAPTURE : direct sale will be implemented, and when it is set to PRE_AUTH or FINAL_AUTH:  Auth will be implemented, and it should be captured later by the merchant |
| defaultDescriptor | Order description sent with every deposit transaction                                                                                                                               |

### Callback URL
Please ask IKajo to configure "callback" URL:

#### TEST
https://test-api.paymentiq.io/paymentiq/api/ikajo/callback

#### PRODUCTION
https://api.paymentiq.io/paymentiq/api/ikajo/callback


### Refund and Void Flow

Refund and Void are initiated from PaymentIQ back office.If everything goes well the transaction status will be set to WAITING_NOTIFICATION in PaymentIQ until IKajo receives the bank confirmation and send the status notification to PaymentIQ (it usually takes around 75 minutes to receive the notification callback but in some cases it can take up to 3 days). If the notification transaction status is successful the refund/void transaction state will be updated to SUCCESS in PaymentIQ. If the notification status is declined the status of the transaction will stay in WAITING_NOTIFICATION in PaymentIQ until the transaction is canceled by the automatic "clean up" job.

## Example Routing Rule
![](/img/providers/routing/ikajo.png)

## Test Information

| Card number         | CVV |
|---------------------|-----|
| 4111 1111 1111 1111 | Any |


Use different expiry dates to simulate different outcomes of the test.

| Outcome   | Expiry date |
|-----------|-------------|
| Approved  | 01 /24      |
| Declined  | 02 /21      |
| 3D secure | 05 /21      |
