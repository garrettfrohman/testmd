--- 
id: "pionpay" 
title: "PionPay"
hide_title: "true"
---

![](/img/providers/logos/pionpay.png)

# PionPay

## About
PionPay is a provider that processes credit card deposits, withdrawals and refunds.

| Provider Name                | PionPay                                                           |
|------------------------------|-------------------------------------------------------------------|
| Link                         | [https://pion.finance/](https://pion.finance/)                    |
| Classification               | Debit/Credit Card Processor                                       |
| Regions                      | `Europe`, `CIS`, `GCC`, `Canada`, `Russia`, `Australia`,  `Japan` |
| Currencies                   | `EUR`, `USD`, `RUB`                                               |
| Methods/PaymentTxTypes       | `CreditcardDeposit` <br/> `CreditcardWithdrawals` <br/>`Refund`   |
| PaymentIQ Configuration File | `PionPayConfig`                                                   |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.pionpay.PionPayConfig>
  <enabled>true</enabled>
  <testMode>true</testMode>
  <useViqProxy>true</useViqProxy>
  <accounts>
    <entry>
      <string>default</string>
      <account>
        <merchantId>??</merchantId>
        <secretKey>??</secretKey>
        <defaultDescriptor>??</defaultDescriptor>
      </account>
    </entry>
  </accounts>
</com.devcode.paymentiq.integration.pionpay.PionPayConfig>
```

</details>

### Attributes

| Attribute                 | Description                                                                                                                      |
|---------------------------|----------------------------------------------------------------------------------------------------------------------------------|
| useViqProxy               | Mandatory - it has to be set to true as the credit card data are being stored in VaultIQ                                         |
| account.merchantId        | Mandatory - an individual ID provided by PionPay - more on that in the Credentials section below                                 |
| account.secretKey         | Mandatory - an individual secret key provided by PionPay - more on that in the Credentials section below                         |
| account.defaultDescriptor | Mandatory - it is used in as a transaction description that will be sent over to the provider and visible on the bank statements |

### Credentials

In order to obtain the credentials, please follow the steps below.
1. Log into your PionPay dashboard under https://merchant.pionpay.com/
2. Go to the `Sites` tab and choose your site from the list.
3. The merchantId parameter should be populated with the value assigned to the Public ID field.
4. The secretKey parameter should be populated with the value assigned to the API Secret key.

NOTE: While you are in the `Sites` section you also have to configure the endpoints to which PaymentIQ should receive
notifications about the statuses of the transactions. <br/>
For test environment the value is: <br/>
https://test-api.paymentiq.io/paymentiq/api/pionpay/callback <br/>
For live environment it is typically: <br/>
https://api.paymentiq.io/paymentiq/api/pionpay/callback

## Transaction Flow

### Deposits

1. The user enters the amount and the credit card details in the Cashier.
2. PaymentIQ sends a deposit request to the PionPay.
3. PionPay sends back a response with the url that the user is redirected to.
4. PaymentIQ performs a status check and updates the status accordingly. If the status is pending, PaymentIQ awaits for
a callback from PionPay with the updated transaction status and then performs a status check again, updating the status 
   of the transaction accordingly to the response.

### Withdrawals

1. The user enters the amount and the credit card details in the Cashier.
2. Once the withdrawal has been approved in the PaymentIQ's backoffice, PaymentIQ sends a payout request to PionPay.
3. In case of successful or pending response, PaymentIQ will set the transaction's status to SUCCESS_WAITING_CONFIRMATION 
   and the transfer will be made to deduct the amount from the user's balance.
4. PaymentIQ awaits for a callback from PionPay regarding the status of the withdrawal. In case of a callback with
   a successful status, PaymentIQ will update the transaction's state to SUCCESS_WITHDRAWAL_APPROVAL. In case of a callback
   with a declined status, a reversal transaction will take place, and the amount will be restored to the
   user's balance.

### Refunds

1. Refunds are made from the PaymentIQ's backoffice from the `Investiate` tab by choosing a transaction,  clicking 
the `Update` button and chosing the `Refund` option.
2. PaymentIQ sends a refund request with the original transaction id and creates a refund transaction. The initial 
successful response from PionPay does not mean that the refund has been approved yet.
3. PaymentIQ awaits a callback with the updated status of the transaction and updates the transaction accordingly to the 
response.
   

## Example Routing Rule

![](/img/providers/routing/pionpay.png)

## Test Information

### 3D Secure Test Cards

| Card Number      | Expiry Date | CVV | Result     |
|------------------|-------------|-----|------------|
| 4200000000000000 | 12/24       | 123 | Successful |
| 4200000000000000 | 12/24       | 333 | Failed     |

### NOTE
Type in "4" as the 3-D Secure passphrase 

For more test cards please visit:
https://pionpay.gitbook.io/pionpay/#cards-for-payment-operation-tests
