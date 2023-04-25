--- 
id: "mazooma" 
title: "Mazooma"
hide_title: "true"
---
 
![](/img/providers/logos/mazooma.png)

# Mazooma

## About
Mazooma is a payment provider that offers Bank deposit and withdrawal, recurring and reversal.

Recurring can be made for deposit and withdrawal. Also user can make a deposit and then use stored account to make a withdrawal.

Reversal can be made for bank deposit only.

| Provider Name                | Mazooma                                                                                                                                                    |
|------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Link                         | [https://us.mazooma.com/](https://us.mazooma.com/)                                                                                                         |
| Classification               | Banking                                                                                                                                                    |
| Regions                      | `USA`                                                                                                                                                        |
| Currencies                   | `USD`                                                                                                                                                        |
| Methods/PaymentTxTypes       | `WebRedirectDeposit`, `BankLocalWithdrawal`, `WebRedirectWithdrawal` (it can only be used as a repeated withdrawal after a successful deposit), `Reversal` |
| PaymentIQ Configuration File | `MazoomaConfig`                                                                                                                                            |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.mazooma.MazoomaConfig>
  <enabled>true</enabled>
  <useViqProxy>true</useViqProxy>
  <accounts>
    <entry>
      <string>DEFAULT</string>
      <account>
        <merchantId>??</merchantId>
        <profileId>??</profileId><!--App Key-->
        <username>??</username><!--client_id-->
        <password>??</password><!--client_secret-->
        <useTokenId>true</useTokenId>
        <productName>ECHECKSELECT</productName>
        <merchantTransactionType>??</merchantTransactionType>
        <defaultDescriptor>Test Product</defaultDescriptor>
        <supportedCurrencies>USD</supportedCurrencies>
        <language>en_us</language>
      </account>
    </entry>
  </accounts>
  <testMode>true</testMode>
  <container>window</container>
</com.devcode.paymentiq.integration.mazooma.MazoomaConfig>
```
</details>

### Attributes
| Attribute                       |           | Description                                                                                                                                                                                                                         |
|---------------------------------|-----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| account.merchantId              | Mandatory | Corresponds to the `Merchant ID` from Mazooma.                                                                                                                                                                                      |
| account.profileId               | Mandatory | Corresponds to the `App Key` from Mazooma. It is used as a "x-pgw-app-id" request header.                                                                                                                                           |
| account.username                | Mandatory | Corresponds to the `client_id` from Mazooma. It is used to request access token that will be used to authorize payment request.                                                                                                     |
| account.password                | Mandatory | Corresponds to the `client_secret` from Mazooma. It is used to request access token that will be used to authorize payment request.                                                                                                 |
| account.useTokenId              | Optional  | It is used to identify if token should be used to make a repeated bank payin or payout. The token is linked to a specific bank account. If a different bank is chosen, the token will remain linked with the original bank account. |
| account.productName             | Mandatory | It is used to identify a product. Currently only one value is possible - `ECHECKSELECT`.                                                                                                                                            |
| account.merchantTransactionType | Optional  | It is used to identify a merchant transaction type. Possible values are: `POKER`, `CASINO`, `BINGO`, `SPORTS_BETTING`, `DIGITAL_REMITTANCE`, `E-SPORTS`.                                                                            |

### Callback URL

### TEST
https://test-api.paymentiq.io/paymentiq/api/mazooma/callback/tx -- Transaction Notification URL
https://test-api.paymentiq.io/paymentiq/api/mazooma/callback/event -- Event Notification URL

### PRODUCTION
https://api.paymentiq.io/paymentiq/api/mazooma/callback/tx -- Transaction Notification URL
https://api.paymentiq.io/paymentiq/api/mazooma/callback/event -- Event Notification URL

## Example Routing Rule
![](/img/providers/routing/mazooma.png)

## Payment Flow

### Bank Deposit (Interactive Payin)

In order to initiate an interactive bank payin user will have to use `WebRedirectDeposit` tx type, provide amount and press pay button. Once it is done, the user will be redirected to the bank selection page:

![](/img/providers/mazooma_payin_01.png)

Once bank is selected (e.g. Chase) the user will have to enter "User ID" and "Password" (please use "user_good" and "pass_good" respectively) and press "Submit" button.

![](/img/providers/mazooma_payin_02.png)

Then the user will have to select bank account (Checking or Saving) and press "Continue" button

![](/img/providers/mazooma_payin_03.png)

Then the user will have to confirm payment by pressing "Confirm Deposit" button

![](/img/providers/mazooma_payin_04.png)

For some banks it is required to specify a verification code and if it is the case, please specify code "1234".

Once payment is completed, Mazooma will send a notification to the PaymentIQ containing a token that could be used to make a repeated payin or payout. \
To use that token, user will have to make a repeated payin or payout (see PaymentIQ Cashier below)

![](/img/providers/mazooma_payin_05.png)

and also `useTokenId=true` must be set in the config. \
In case token is used, the user will not need to specify bank information in order to make payin or payout.

### Bank Withdrawal

Once user have made a successful deposit and have a stored token, he/she can make a withdrawal using that stored token. To do it, user will need to use `WebRedirectWithdrawal` tx type.

If the user hasn't made any deposits before, he/she can make a new withdrawal using `BankLocalWithdrawal` tx type and specify `amount`, `bank account`, `transit`/`routing number`, `SSN`/`National ID` and `account type` (Checking/Saving) and press pay button. Once withdrawal is completed, PaymentIQ will also store token that can be used to make a repeated withdrawal.  

![](/img/providers/mazooma_payout_01.png)


## Test Information

### Bank Deposit

There could be a situation when bank deposit was successful and in some time provider sent event notification about decline (`nextAction=D (Declined)`). In such case PaymentIQ will revert original deposit by creating additional transaction that will be linked with original deposit transaction like: `depositTx.txRefId == reversedTx.originTxRefId`. \
In case of `nextAction=R (Representment)`, provider will not decline payment immediately and might validate some conditions in order to collect funds. If funds were not collected, provider will send a new `Representment` notification in 5 days. In total it might be 3 attempts.

In case of `Representment` merchants should: \
1). not let the customer withdraw funds, and inform the customer about uncollected funds \
2). go to the provider's portal and manually dispose the Representment

### Bank Withdrawal

User can use different amount to test a withdrawal.

| Transaction amount | payment_method | Description                                                             |
|--------------------|----------------|-------------------------------------------------------------------------|
| < 100              | ach            | it will take up to 2 business days to reach the customer's bank account |
| = 100              | pending        | wait 2-3 min in order to see whether it will go through `ach` or `rtp`  |
| > 100              | rtp            | funds are deposited in the customer's account in real time              |

In case of `rtp`, Mazooma will send final tx status with the response and it will be seen in the PaymentIQ back office. \
In case of `pending`, PaymentIQ will have to send a `Report Transaction` request (in 2-3 min) in order to see whether payment will go through `ach` or `rtp`. It can be achieved by configuring a status polling job with `<pollIntervalInMins>1</pollIntervalInMins>` and ` <abortAfterMins>5</abortAfterMins>`. \
IN case of `ach`, PaymentIQ will have to send a `Report Transaction` request (in 2-3 business days) in order to check payment status. It can be achieved by configuring a status polling job with ` <pollAfterMins>2880</pollAfterMins>`, `<pollIntervalInMins>240</pollIntervalInMins>` and ` <abortAfterMins>4320</abortAfterMins>` (start checking in 2 days; during 3 days and 4 times per day).

#### Test Bank Details

| Mazooma Parameter | PaymentIQ input parameter               | Value      |
|-------------------|-----------------------------------------|------------|
| Account Number    | BankLocalWithdrawalInput.accountNumber  | 0123456789 |
| Routing           | BankLocalWithdrawalInput.clearingNumber | 021000021  |
| Account Type      | BankLocalWithdrawalInput.accountType    | PC         |

#### Notes

- SSN needs to be 4-9 digits long
