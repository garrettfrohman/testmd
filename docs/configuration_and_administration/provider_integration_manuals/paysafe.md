--- 
id: "paysafe"
title: "Paysafe"
hide_title: "true"
---

![](/img/providers/logos/paysafe.png)

# Paysafe

## About
Paysafe offers credit card processing, direct debit and alternate payment methods through their platform.

| Provider Name                | Paysafe                                                                                                                                                                                                                                                                                           |
|------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Link                         | [https://www.paysafe.com/](https://www.paysafe.com/)                                                                                                                                                                                                                                              |
| Classification               | Debit/Credit Card Processor                                                                                                                                                                                                                                                                       |
| Regions                      | `International`                                                                                                                                                                                                                                                                                   |
| Currencies                   | Please check directly with the provider regarding what currencies are supported                                                                                                                                                                                                                   |
| Methods/PaymentTxTypes       | `CreditcardDeposit` <br/> `CreditcardWithdrawal` <br/> `Capture` <br/> `Void` <br/> `Refund` <br/> `BankDeposit` <br/> `InteracWithdrawal` <br/> `PayPalDeposit` <br/> `PayPalWithdrawal` <br/> `PaysafecardDeposit` <br/> `PaysafecardWithdrawal` <br/> `SkrillDeposit` <br/> `SkrillWithdrawal` |
| PaymentIQ Configuration File | `PaysafeConfig`                                                                                                                                                                                                                                                                                   |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>


```xml
<com.devcode.paymentiq.integration.paysafe.PaysafeConfig>
  <enabled>true</enabled>
  <useViqProxy>true</useViqProxy>
  <accounts>
    <entry>
     <string>default</string>
     <account>
        <merchantId>???</merchantId>
        <username>???</username>
        <password>???</password>
        <useTokenId>???</useTokenId>
        <use3Dsecure>true</use3Dsecure>
        <!--Options: AUTH_CAPTURE/FINAL_AUTH/PRE_AUTH-->
        <authType>AUTH_CAPTURE</authType>
     </account>
    </entry>
  </accounts>
</com.devcode.paymentiq.integration.paysafe.PaysafeConfig>
```

</details>

### Attributes

| Attribute  | Description                                 |
|------------|---------------------------------------------|
| merchantId | Corresponds to Paysafe Account ID           |
| username   | Corresponds to Paysafe API keys - User name |
| password   | Corresponds to Paysafe API keys - Password  |

*For withdrawal: Acquirers and processors do not necessarily support all available MCCs; before integrating, you should contact Paysafe Support for details.*

## APMs
| Attribute       | Description                                                                                                                                 |
|-----------------|---------------------------------------------------------------------------------------------------------------------------------------------|
| secretKey       | Corresponds to HMAC Secret Key set in Paysafe Business Portal in configured webhook                                                         |
| serviceEndpoint | Should be set to `https://api.test.paysafe.com/paymenthub` (test environment) or to `https://api.paysafe.com/paymenthub` (prod environment) |

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.paysafe.PaysafeConfig>
  <enabled>true</enabled>
  <useViqProxy>true</useViqProxy>
  <accounts>
    <entry>
     <string>apm</string>
     <account>
        <merchantId>???</merchantId>
        <username>???</username>
        <password>???</password>
        <secretKey>???</secretKey>
        <serviceEndpoint>https://api.test.paysafe.com/paymenthub</serviceEndpoint>
     </account>
    </entry>
  </accounts>
</com.devcode.paymentiq.integration.paysafe.PaysafeConfig>
```

</details>

### Webhook configuration
The Webhook URL has to be set on the Paysafe Business Portal.

Webhook URL:
`https://{env.host.domain}/paymentiq/api/paysafe/callback`

For deposits, the webhook should be configured for the following events
`PAYMENT_HANDLE_PAYABLE`, `PAYMENT_HANDLE_FAILED`, `PAYMENT_COMPLETED`, `PAYMENT_FAILED`, `PAYMENT_CANCELLED`

For withdrawals, the webhook should be configured for the following events
`SA_CREDIT_COMPLETED`, `SA_CREDIT_FAILED`, `SA_CREDIT_CANCELLED`

### Interac E-transfer

| Attribute      | Description                                                                                                                                          |
|----------------|------------------------------------------------------------------------------------------------------------------------------------------------------|
| variable1      | Corresponds to the Interac-Etransfer withdrawal request parameter `question`. If not set, the `question` parameter will be set to `DefaultQuestion`. |
| variable2      | Corresponds to the Interac-Etransfer withdrawal request parameter `answer`. If not set, `answer` parameter will be set to `DefaultAnswer`.           |
| deviceCategory | Corresponds to the `deviceId` Paysafe request parameter. If not set, the `deviceId` parameter will be set to `defaultdeviceid`.                      |

#### Methods:

1) `BankDeposit` for Interac-Etransfer deposit.
2) `InteracWithdrawal` for Interac-Etransfer withdrawal.

### PayPal

| Attribute   | Description                                                                                                                                                                                                    |
|-------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| billingType | Corresponds to the `shippingPreference` parameter of the PayPal deposit request. Possible values are `GET_FROM_FILE` `SET_PROVIDED_ADDRESS` `NO_SHIPPING`. If not set, `NOT_SHIPPING` will be used as default. |

NOTE: the list of possible values of `billingType` parameter can be extended or changed entirely in case of Paysafe API gets updated. In order to do this, the parameter `config.paypalShippingMapping` can be changed like this for example:
`GET_FROM_FILE->GET_FROM_FILE,SET_PROVIDED_ADDRESS->SET_PROVIDED_ADDRESS,NO_SHIPPING->NO_SHIPPING,*->SOME_NEW_VALUE` where `SOME_NEW_VALUE` is default value in case of `billingType` is not set, or set incorrectly.


NOTE:
#### Methods:

1) `PayPalDeposit`
2) `PayPalWithdrawal`

### Paysafecard
#### Methods:

1) `PaysafecardDeposit`
2) `PaysafecardWithdrawal`

### Skrill

| Attribute    | Description                                                                                                                 |
|--------------|-----------------------------------------------------------------------------------------------------------------------------|
| templateName | The name of the Skrill email template. If not set, the default email template name `withdrawal-confirmation-email` is used. |

#### Methods:

1) `SkrillDeposit`
2) `SkrillWithdrawal`

NOTE: The custom email template can be defined for Skrill withdrawal transaction.
The email subject and email body is used in payment handle Skrill withdrawal request.
The email body should be of simple text format.
If the email template is not defined, default values will be used in Skrill withdrawal request.


## Example Routing Rule

### Credit Card
![](/img/providers/routing/paysafe.png)

### Interac E-transfer
![](/img/providers/routing/paysafe_interac.png)

### PayPal
![](/img/providers/routing/paysafe_paypal.png)

### Paysafecard
![](/img/providers/routing/paysafe_paysafecard.png)

### Skrill
![](/img/providers/routing/paysafe_skrill.png)

## Test Information
Please follow the link for Paysafe test cards:

[https://developer.paysafe.com/en/rest-apis/cards/test-and-go-live/test-cards/](https://developer.paysafe.com/en/rest-apis/cards/test-and-go-live/test-cards/)


Interac E-transfer deposit test transaction amounts

| Amount   | Status    | Status time      |
|----------|-----------|------------------|
| 5.19 CAD | COMPLETED | After 20 seconds |
| 5.29 CAD | COMPLETED | After 5 minutes  |
| 5.39 CAD | COMPLETED | After 30 minutes |
| 5.49 CAD | FAILED    | After 5 minutes  |

Interac Etransfer withdrawal test transaction amounts

| Amount   | Status    | Status time      |
|----------|-----------|------------------|
| 7.19 CAD | COMPLETED | After 60 minutes |
| 7.29 CAD | FAILED    | After 60 minutes |
| 7.39 CAD | ERROR     | Immediately      |