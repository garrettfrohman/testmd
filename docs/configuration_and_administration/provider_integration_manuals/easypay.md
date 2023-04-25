--- 
id: "easypay"
title: "Epaybg / EasyPay"
hide_title: "true"
--- 

![](/img/providers/logos/eplogo.png)
![](/img/providers/logos/easypay.png)

# Epaybg / EasyPay

## About

| Provider Name                | EasyPay                                                                                                                                                                |
|------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Link                         | [https://www.epay.bg/](https://www.epay.bg/)                                                                                                                           |
| Classification               | Voucher                                                                                                                                                                |
| Regions                      | `Bulgaria`                                                                                                                                                             |
| Currencies                   | `USD`, `EUR`, `BGN` (`BGN` for `EasyPayWithdrawal`)                                                                                                                    |
| Methods/PaymentTxTypes       | `EasyPayDeposit` <br/> `EasyPayWithdrawal` <br/> `WebRedirectDeposit` <br/> `EPaybgWithdrawal` <br/> `EasyPayBatchDeposit` <br/> `BankIBANWithdrawal` <br/> `Reversal` |
| PaymentIQ Configuration File | `EasyPayConfig`                                                                                                                                                        |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.easypay.EasyPayConfig>
  <enabled>true</enabled>
  <accounts>
    <entry>
      <string>default</string>
      <account>
        <merchantId>?????</merchantId>
        <secretKey>?????</secretKey>
        <supportedCurrencies>USD|EUR|BGN</supportedCurrencies>
        <email>????@????.com</email>
      </account>
    </entry>
    <entry>
      <string>withdrawal</string>
      <account>
        <merchantId>?????</merchantId>
        <secretKey>?????</secretKey>
        <supportedCurrencies>BGN</supportedCurrencies>
        <email>????@???.com</email>
      </account>
    </entry>
    <entry>
      <string>batch</string>
      <account>
        <merchantId>?????</merchantId>
        <secretKey>?????</secretKey>
        <supportedCurrencies>BGN</supportedCurrencies>
      </account>
    </entry>
  </accounts>
  <notifications>NOTIFICATION|EMAIL</notifications>
  <container>window</container>
  <deliveryNotifications>0</deliveryNotifications>
</com.devcode.paymentiq.integration.easypay.EasyPayConfig>
```
</details>

### Attributes

| Attribute                 | Description                                                                                                                    |
|---------------------------|--------------------------------------------------------------------------------------------------------------------------------|
| merchantId                | Merchant merchant id (Customer number in EasyPay merchant account)                                                             |
| secretKey                 | Merchant secret key (Secret key in EasyPay merchant account)                                                                   |
| supportedCurrencies       | Supported currencies (`USD`,`EUR`,`BGN`)                                                                                       |
| email                     | Merchants email address (E-mail in EasyPay merchant account)                                                                   |
| encoding                  | Encoding of the DESCR param content, default UTF-8                                                                             |
| testEPayEndpoint          | Test url for the money send method                                                                                             |
| liveEPayEndpoint          | Live url for the money send method                                                                                             |
| moneySendExpireAfterHours | Expiry time for withdrawal tx, default 24h                                                                                     |
| regBillExpireAfterHours   | Expiry time for deposit tx, default 24h                                                                                        |
| redirectExpireAfterHours  | Expiry time for redirect tx, default 24h                                                                                       |
| autoRedeemIdn             | If the money send payment code should be redeemed, default true (if testmode else false). Should not used in live              |
| moneySendEmailTemplate    | Name of the withdrawal payment code email, default: easypay-money-send-email                                                   |
| regBillEmailTemplate      | Name of the deposit payment code email, default: easypay-reg-bill-email                                                        |
| notifications             | Notifications that will be sent, can be multiple separated by a `|` (can be `NOTIFICATION`,`EMAIL`), default `EMAIL`           |
| service                   | `CREDITCARD` or `PAYLOGIN`, default `PAYLOGIN` (can be overriden by fronend api service parameter)                             |
| redirectTemplateName      | Name of the template to use for redirection when showing the payment code to the customer. Default easypay-redirect-template   |
| deliveryNotifications     | Sets the DELIVERY_NTFY request parameter. 0 = No emails sent from EasyPay to merchant                                          |
| idnField                  | Specifies what the idn field from Easypay request is mapped as in LookupUserRequest (default is personid)                      |
| shortDescription          | Short description to send in response on the pay_init request of EasyPayBatchDeposit (default is Customer name: \${user.name}) |
| longDescription           | Long description to send in response on the pay_init request of EasyPayBatchDeposit (default is Customer name: \${user.name})  |
| batchDepositEnabled       | Specifies if the EasyPayBatchDeposit api is enabled. (default is false)                                                        |

### Wait For Withdrawal Notifications
The default scenario is that PaymentIQ will set status `WAITING_NOTIFICATION` when the withdrawal is created and update it when notifications are received.

In another case PaymentIQ sets the withdrawal to `SUCCESS` after it has been successfully received by EasyPay and waiting for it to be processed. If anything goes wrong during processing a reversal is created. It can be done by adding this to EasyPayConfig:

`<waitForWithdrawalNotification>false</waitForWithdrawalNotification>`

Note that there is always a risk involved with not using this configuration that the merchant needs to be aware of. If anything goes wrong with the transaction (e.g. misconfiguration, human error, connection issues etc) while it is waiting to be processed at the provider that causes PaymentIQ to set it to FAILED means that a cancel will be sent to the merchant. At the same time it is possible that the provider successfully executed it and the user received the money on their end.

### Notifications

#### EasyPayBatchDeposit
Notifications must be set from EasyPays side. 

##### Test
| Request     | URL                                                                                                |
|-------------|----------------------------------------------------------------------------------------------------|
| pay_init    | https://test-api.paymentiq.io/paymentiq/api/easypaybatch/deposit/validate/{Payment IQ merchant id} |
| pay_confirm | https://test-api.paymentiq.io/paymentiq/api/easypaybatch/deposit/process/{Payment IQ merchant id}  |

##### Live
| Request     | URL                                                                                           |
|-------------|-----------------------------------------------------------------------------------------------|
| pay_init    | https://api.paymentiq.io/paymentiq/api/easypaybatch/deposit/validate/{Payment IQ merchant id} |
| pay_confirm | https://api.paymentiq.io/paymentiq/api/easypaybatch/deposit/process/{Payment IQ merchant id}  |

#### Other methods
Notifications for live environment must be set from EasyPays side but for test you can set it your self in the merchant protal. 

| Environment | URL                                                          |
|-------------|--------------------------------------------------------------|
| Test        | https://test-api.paymentiq.io/paymentiq/api/easypay/callback |
| Live        | https://api.paymentiq.io/paymentiq/api/easypay/callback      |

### Email template

If ```<notifications>EMAIL</notifications>``` then a email will be sent to the user on the email address that was provided in the verify user response.

A email template is required for sending out the payment code to the user.
For withdrawals name it easypay-money-send-email or set a other name in the EasyPayConfig file and the ```<moneySendEmailTemplate></moneySendEmailTemplate>``` attribute.
For deposit name it easypay-reg-bill-email or set a other name in the EasyPayConfig file and the ```<regBillEmailTemplate></regBillEmailTemplate>``` attribute.

<details>
<summary>Click to view example email template for withdrawals (easypay-money-send-email)</summary>
<br/>

```html
<p>
    <b>Thank you for using Moneysend with EasyPay.</b>

    <br/>

    Please redeem your payment code on a EasyPay office or use the following url:
    
    <br/>
    
    ${if !ptx.latestTxCmdMap.EasyPayTxRes.test}
    <a href="https://www.epay.bg">https://www.epay.bg</a>
    <br/>
    your code is: <b>${ptx.maskedUserAccount}</b>
    ${else}
    <a href="https://demo.epay.bg/ezp/pay_money_send.cgi?SYS_CODE=${ptx.maskedUserAccount}">
       https://demo.epay.bg/ezp/pay_money_send.cgi?SYS_CODE=${ptx.maskedUserAccount}
    </a>
    <br/>
    and enter your payment code: <b>${ptx.maskedUserAccount}</b>
    ${end}
    
    <br/>
    
    The payment will expire: <b>${ptx.latestTxCmdMap.EasyPayTxRes.expireDateTime}</b>
<p>
```

</details>

<details>
<summary>Click to view example email template for deposit (easypay-reg-bill-email)</summary>
<br/>

```html
<p>
    <b>Thank you for using Moneysend with EasyPay.</b>

    <br/>

    Please redeem your payment code on a EasyPay office or use the following url:
    
    <br/>
    
    ${if !ptx.latestTxCmdMap.EasyPayTxRes.test}
    <a href="https://www.epay.bg/?page=payfly">https://www.epay.bg/?page=payfly</a>
    ${else}
    <a href="https://demo.epay.bg/ezp/pay_bill.cgi?ACTION=PAY&amp;IDN=${ptx.maskedUserAccount}">
      https://demo.epay.bg/ezp/pay_bill.cgi?ACTION=PAY&amp;IDN=${ptx.maskedUserAccount}
    </a>
    ${end}

    <br/>

    and enter your payment code: <b>${ptx.maskedUserAccount}</b>
    
    <br/>
    
    The payment will expire: <b>${ptx.latestTxCmdMap.EasyPayTxRes.expireDateTime}</b>
<p>
```

</details>

### Merchant notification

If ```<notifications>NOTIFICATION</notifications>``` then a notification will be sent to the merchant system using the merchant integration api and the notification endpoint. The notification will be a own transaction i PaymentIQ so it will not effect the outcome of the actual deposit/withdrawal.

More info about the notification api can be found [here](/docs/apis_and_integration/integration_api/notification)

Here are some extra attributes that will be include for this integration. They will be included in the attributes section of the notification body.

| Attribute parameter |          |        |                                            |
|---------------------|----------|--------|--------------------------------------------|
| code                | required | string | The payment code for withdrawal or deposit |
| expireDateTime      | required | string | The expiration date and time for this code |

## Example Routing Rule

![](/img/providers/routing/easypay.png)

## Transaction Flow

### WebRedirect (PAYLOGIN,CREDITCARD)
EasyPay has two services PAYLOGIN and CREDITCARD

#### PAYLOGIN
Redirect payment solution that redirects to the EasyPay website to select payment method.
A notification will be sent to PaymentIQ when the payment is done.

#### CREDITCARD
Redirect payment solution that redirect to the EasyPay website to enter creditcard details.
A Notification will be sent to PaymentIQ when the payment is done.

### EasyPayDeposit (RegBill)

1. User request a deposit with the EasyPayDeposit method
2. The PaymentIQ send a payment request to EasyPay to create a payment code that the customer will pays at a EasyPay office. The payment code will be sent out in a email to the customer or by notification to merchant system. Depending of the ```<notifications>NOTIFICATION</notifications>``` tag in config.
3. The customer pays the code at a EasyPay office
4. The EasyPay system sends a notification to PaymentIQ when its payed or expired.
5. If PaymentIQ gets a notification that it has been payed then a transfer call will be sent.
6. If PaymentIQ gets a notification that it has expired or have been declined then a cancel notification will be sent.

### EasyPayBatchDeposit

1. A user requests a deposit at a Easypay kios with his username or national identity number
2. Easypay send requests to PaymentIQ that a user wants to deposit x amount to its player account
3. PaymentIQ do the neccessary checks against fraud, limit rules etc..
4. PaymentIQ will not be able to check the userid via the verifyuser request like in the normal flow. 
5. PaymentIQ will use [lookupuser](/docs/apis_and_integration/integration_api/lookupuser) that is available in the IntegrationAPI (needs to be added by merchant).
6. PaymentIQ sends back the status to Easypay
7. If PaymentIQ sent OK status to Easypay the deposit will be proceeded
8. A new request will be done from Easypay to confirm deposit and do transfer of funds to user.
9. PaymentIQ sends back status when done.

### EasyPayWithdrawal (MoneySend)

#### Wait For Withdrawal Notifications is enabled (default)

1. User request a withdrawal with the EasyPayWithdrawal method
2. Operator approves or declines the request.
3. The PaymentIQ send a payment request to EasyPay to create a payment code that the customer will redeem at a EasyPay office. The payment code will be sent out in a email to the customer or by notification to merchant system. Depending of the ```<notifications>NOTIFICATION</notifications>``` tag in config.
4. The customer redeems the code at a EasyPay office
5. The EasyPay system sends a notification to PaymentIQ when its redeemed or expired.
6. If PaymentIQ gets a notification that it has been redeemed then a transfer call will be sent.
7. If PaymentIQ gets a notification that it has expired or have been declined then a cancel notification will be sent.

#### Wait For Withdrawal Notifications is disabled

1. User request a withdrawal with the EasyPayWithdrawal method.
2. Operator approves or declines the request.
3. The PaymentIQ send a payment request to EasyPay and based on the response the transaction is either declined or put in
   the `SUCCESS_WAITING_CONFIRMATION` state.
3. PaymentIQ awaits a callback from EasyPay.
    - In case of a callback with a successful status, PaymentIQ updates the status
      of the transaction to `SUCCESS_WITHDRAWAL_APPROVAL`.
    - In case of a callback with a declined status, a reversal transaction
      will take place, and the amount will be restored to the user's balance.

### EPaybgWithdrawal

1. User request a withdrawal with the EPaybgWithdrawal method and submits the email that is connected to its Easypaybg account
2. Operator approves or declines the request
3. The PaymentIQ sends a payment request to Epaybg to transfer the funds
4. The funds are transfered from merchant account to user.

### BankIBANWithdrawal
This method is used to withdraw money to the user's IBAN. It is very similar to EPaybgWithdrawal with the only difference that it is initiated with TxType BankIBANWithdrawal, which lets the user input their IBAN instead of email.

1. The user requests a withdrawal with the BankIBANWithdrawal method and submits the IBAN of the account that the withdrawal should be sent to
2. The operator approves or declines the request
3. PaymentIQ sends a payment request to EasyPay to transfer the funds
4. The funds are transfered from merchant account to user

## Test Information

EasyPay supports `USD`, `EUR`, `BGN` as currency for deposit and `BGN` for withdrawal.

### WebRedirect (PAYLOGIN,CREDITCARD)
EasyPay has two services `PAYLOGIN` and `CREDITCARD`

#### Register for a demo account
Use this link [https://demo.epay.bg/en/?page=login](https://demo.epay.bg/en/?page=login) to register a demo account.
You will register two account at once. One for the demo merchant and one for a demo user.

#### PAYLOGIN
Redirect payment solution that redirects to the EasyPay website.
1. Login to the customer account
2. Select ot reject or approve the payment
3. A notification will be sent to PaymentIQ
4. A redirection will be done

##### Credentials (on devcode demo account!)
| Username               | Password                 |
|------------------------|--------------------------|
| devcodePaymentCustomer | LpjYzYBy6JU3hM3tbhQ72sX9 |

#### CREDITCARD
Redirect payment solution that redirect to the EasyPay website.
1. Enter the creditcard details
2. A notification will be sent to PaymentIQ
3. A redirection will be done

##### Test Creditcards

| Brand      | Cardnumber      | Expiry date (MM/YY) | Verification code |
|------------|-----------------|---------------------|-------------------|
| VISA       | 451698754123654 | 12/21               |                   |
| MASTERCARD | 53697865321453  | 12/21               |                   |
| MAESTRO    | 63569874235948  | 12/21               |                   |
| BORIKA     | 67601111111111  | 12/21               | 111111            |

### EasyPayDeposit (RegBill)

1. User do a deposit with the EasyPayDeposit method
2. The PaymentIQ send a payment request to EasyPay to create a payment code that the customer will pay at a EasyPay office. The payment code will be sent out in a email to the customer or by notification to merchant depending of the ```<notifications>NOTIFICATION</notifications>``` tag in config.
3. Use the link in the email to pay the code or set the ```autoRedeemIdn``` to ```true```.
4. A notifications will be sent when payed. 

### EasyPayBatchDeposit

Tests can only be done from Easypays side.

### EasyPayWithdrawal (MoneySend)

1. User request a withdrawal with the EasyPayWithdrawal method
2. Some attributes must be included in the verifyUser response. 

    1. If Bulgarian citizen then the attribute ```nationalIdentificationNumber``` has to be provided.
    2. If not a Bulgarian citizen then the attributes ```documentId``` (The document id is the document number of a id card or passport etc) and ```documentIdIssuingDate``` has to be provided.

3. Operator approves or declines the request.
4. The PaymentIQ send a payment request to EasyPay to create a payment code that the customer will redeem at a EasyPay office. The payment code will be sent out in a email to the customer or by notification to merchant depending of the ```<notifications>NOTIFICATION</notifications>``` tag in config.
5. Use the link in the email to redeem the code or set the ```autoRedeemIdn``` to ```true```.
6. A notifications will be sent when redeemed. 

#### Test Document IDs (documentId attribute)
| Document ID | outcome          |
|-------------|------------------|
| 60000000    | OK               |
| 123456      | Validation error |

#### Test Document ID issuing date (documentIdIssuingDate attribute)
Use a date in format ```DD.ММ.YYYY``` that has not passed.

#### Test Pids (nationalIdentificationNumber attribute)
| PID        | outcome          |
|------------|------------------|
| 7101016332 | OK               |
| 123456     | Validation error |

or generate one here: [https://georgi.unixsol.org/programs/egn.php](https://georgi.unixsol.org/programs/egn.php)

### EPaybgWithdrawal

#### Test email
| Email                        |
|------------------------------|
| technicalsupport@bambora.com |
