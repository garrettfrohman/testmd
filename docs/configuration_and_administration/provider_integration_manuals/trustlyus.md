--- 
id: "trustlyus"
title: "TrustlyUS"
hide_title: "true"
---

![](/img/providers/logos/trustlyus.png)

# TrustlyUS

## About
TrustlyUS is a brand of Trustly for the USA market. It offers WebRedirect deposits and withdrawals as well as refunds.

| Provider Name                | TrustlyUS                                                         |
|------------------------------|-------------------------------------------------------------------|
| Link                         | [https://www.trustly.net/](https://www.trustly.net/)              |
| Classification               | Aggregator                                                        |
| Regions                      | `USA`                                                             |
| Currencies                   | `USD`                                                             |
| Methods/PaymentTxTypes       | `WebRedirectDeposit` <br/> `WebRedirectWithdrawal` <br/> `Refund` |
| PaymentIQ Configuration File | `TrustlyUSConfig`                                                 |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.trustlyus.TrustlyUSConfig>
  <enabled>true</enabled>
  <accounts>
    <entry>
      <string>default</string>
      <account>
        <merchantId>??</merchantId>
        <accountID>??</accountID>
        <apiKey>??</apiKey>
        <supportedCurrencies>USD</supportedCurrencies>
        <forcePayment>TestNullSplitTokenUseCase</forcePayment>  
      </account>
    </entry>
  </accounts>
</com.devcode.paymentiq.integration.trustlyus.TrustlyUSConfig>
```

</details>

### Attributes

| Attribute                   | Description                                                                                                                                |
|-----------------------------|--------------------------------------------------------------------------------------------------------------------------------------------|
| account.merchantId          | Mandatory. A unique merchant identifier provided individually for each merchant account by TrustlyUS.                                      |
| account.accountID           | Mandatory. A unique merchant account identifier provided individually for each merchant account by TrustlyUS.                              |
| account.apiKey              | Mandatory. It is used to sign requests and validate signatures and should be provided by TrustlyUS for each merchant account individually. |
| account.supportedCurrencies | Mandatory. The list of supported currencies for the account in use separated by \| (pipe character).                                       |
| account.forcePayment        | Optional. Used for testing purposes. When present in account config null splitToken use-case can be tested.                                |

## Provider Configuration

In order to enable TrustlyUS please follow these steps:

1. Run PaymentIQ and add the TrustlyUSConfig under Admin -> Configuration.
2. Add TrustlyUS to the `<psp>` section in MerchantConfig under Admin -> Configuration.
3. Enable WEBREDIRECT-TRUSTLYUS deposit and withdrawal method in Rules -> Payment methods.

### Transaction Flow

#### Deposits

1. The user enters the amount to be deposited in the cashier.
2. If it's a first time the user makes a deposit via TrustlyUS, the user gets redirected to the TrustlyUS lightbox where
   she / he is being asked to choose the bank account to be used for the deposit. If the user is using the account that already
   exists, step 4 is being directly executed.
3. TrustlyUS sends an authorization callback with an authorization transaction ID (it will be the parent transaction ID for
   every subsequent deposit made under this user account in the future) as well as 'splitToken' (used to identify users' accounts
   in TrustlyUS API) - these parameters are stored in the PaymentIQ database for further usage.
4. PaymentIQ sends a deposit request towards TrustlyUS with the following scenarios are possible: <br/>
   a) If TrustlyUS responds with a successful/declined status, PaymentIQ sets the transaction status to SUCCESS/FAILED. <br/>
   b) If TrustlyUS responds with a pending status, PaymentIQ awaits a callback from TrustlyUS, then performs a status check against the TrustlyUS API and updates the status of the transaction accordingly. <br/>
   c) If TrustlyUS responds with a status that indicates that the split token used for the transaction has expired, the process
   begins again from step 2 (redirection to TrustlyUS lightbox).<br/>

#### Withdrawal

1. The user enters the amount to be withdrawn in the cashier.
2. If it's a first time the user makes a withdrawal via TrustlyUS, the user gets redirected to the TrustlyUS lightbox where
   she / he is being asked to choose the bank account to be used for the deposit. If the user is using the account that already
   exists, step 4 is being directly executed.
3. TrustlyUS sends an authorization callback with an authorization transaction ID (it will be the parent transaction ID for
   every subsequent deposit made under this user account in the future) as well as 'splitToken' (used to identify users' accounts
   in TrustlyUS API) - these parameters are stored in the PaymentIQ database for further usage.
4. PaymentIQ sends a deposit request towards TrustlyUS. If TrustlyUS responds with a successful or pending status,
   PaymentIQ will set the transaction's status to SUCCESS_WAITING_CONFIRMATION and the transfer will be made to deduct the amount from the user's balance.
   Then, PaymentIQ awaits a callback from TrustlyUS regarding the status of the withdrawal. In case of a callback with
   a successful status, PaymentIQ will update the transaction's state to SUCCESS_WITHDRAWAL_APPROVAL. In case of a callback
   with a declined status, a reversal transaction will take place and the amount will be restored to the user's balance.

## Certification process
TrustlyUS requires a certification process which means going through the use cases found at [https://amer.developers.trustly.com/payments/docs/integration-checklist](https://amer.developers.trustly.com/payments/docs/integration-checklist).
The table below describes each use case as found in the link above plus an extra column that provides detailed steps on how to reproduce each use case properly.

| Use case no. | Front-End/Back-End | Category                            | Test Case Details                                                                                                                                         | Input                                                                                                                                                                             | Output                                         | PIQ Explanation                                                                                                                                                                                                                                                                                                                                                        |
|--------------|--------------------|-------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 1.           | FE                 | Presentment                         | Demonstrate Online Banking payment mark placement with Trustly approved UX.                                                                               | Preview merchant’s site.                                                                                                                                                          |                                                | Confirm that user's TrustlyUS accounts displays the proper information.                                                                                                                                                                                                                                                                                                |
| 2.           | FE                 | Presentment                         | Security Slider                                                                                                                                           | Confirm that the logo and short name is correct.                                                                                                                                  | Security slider must match Trustly approved UX | Confirm that TrustlyUS security slider is displayed.                                                                                                                                                                                                                                                                                                                   |
| 3.           | FE                 | Presentment                         | Usage of Trustly hosted assets (where applicable): payment mark, bank icons & logos, footer, etc.                                                         |                                                                                                                                                                                   |                                                | Use the bank logos and correct bank names for users' accounts. PIQ Cashier displays the bank icons if `showAccounts=inline` is used.                                                                                                                                                                                                                                   |
| 4.           | FE                 |                                     | Perform Deferred bank authorization for initial/first time transaction for a purchase or to fund an account.                                              | Launch JS SDK (or native SDK). Walk through lightbox and successfully select bank account.                                                                                        | Transaction ID retrieved                       | Start a transaction with a new account > Log in the bank successfully > Perform a `SUCCESSFUL` transaction and the account is saved for future transactions.                                                                                                                                                                                                           |
| 5.           | FE                 |                                     | Perform a subsequent transaction with account on file or a purchase or to fund an account.                                                                | Complete a subsequent transaction with account on file.                                                                                                                           |                                                | Using an account saved on file perform a `SUCCESSFUL` transaction.                                                                                                                                                                                                                                                                                                     |
| 6.           | Both               | Account on file - refresh required  | Trigger expired split token with notification: SW057 status + 326 error. Implement refresh a bank token: On-file transactions.                            | Demo Bank > use 'ExpiredSplitToken' as password.                                                                                                                                  |                                                | Use a new account > When logging into the bank use the `ExpiredSplitToken` password > This transaction should be `SUCCESSFUL` > Wait more than 1 minute > Perform a second transaction with the saved account on file > The re-login page for the previously selected bank should pop up > Use correct credentials > Transaction is `SUCCESSFUL` with token refreshed. |
| 7.           | Both               | Refresh required to account on file | Trigger null/invalid split token with notification: SW051 status + 380 error Refresh a bank token: On-file transactions.                                  | Pass in a null value for splitToken with the Capture API.                                                                                                                         |                                                | Set `forcePayment=TestNullSplitTokenUseCase` at account config level > Perform a transaction with an account saved on file > The re-login page should pop up > Use correct credentials > Transaction should be `SUCCESSFUL` with new valid token saved for that account.                                                                                               |
| 8.           | Both               | Refresh required to account on file | Trigger HTTP 400 bad request + 200 error in the body + message in the body from API response. Refresh a bank token: On-file transactions.                 | Trigger the ExpiredSplitToken use cases  as above. The re-login page pops up. Exit out of lightbox. Retry a transaction with the saved account on file.                           |                                                | Trigger the ExpiredSplitToken use case like described in item `6`, but when on the re-login page exit the page > Transaction will be `ERR_CANCELLED_BY_USER` > Perform a subsequent transaction with the same account > Re-login with correct credentials > Transaction should be `SUCCESSFUL` and new valid token saved for that account.                             |
| 9.           | Both               | Notify user-adverse action          | Trigger Adverse Action Language with thirdPartyDecline: Fraud Analysis: SW054 status + 390 error Fraud Analysis: Negative Data: SW055 status + 390 error. | Demo Bank > use 'tckerror' as passowrd > select SW054 associated with bank account or select SW055 associated with bank account.                                                  |                                                | Use a new account > When logging into the bank use the `tckerror` password > A list with accounts will be available > Use the `SW054` account > Transaction should fail with `ERR_DECLINED_FRAUD` and account should be blocked (not available for future transactions). Do the same flow for the `SW055` account > Same behaviour.                                    |
| 10.          | Both               |                                     | Trigger Invalid Account use-case: SW056 status + 330 error                                                                                                | Demo Bank > use 'tckerror' as passowrd > select SW056 associated with bank account.                                                                                               |                                                | Same as item `9`.                                                                                                                                                                                                                                                                                                                                                      |
| 11.          | BE                 |                                     | Demonstrate Risk data passed in the establish.                                                                                                            | Required Risk Data (if collected during registration): externalID; name; address; email; phone number; enrollDate; DOB; Encrypted SSN/taxID (no special characters including "-". |                                                | TrustlyUS should confirm that the specified parameters are received for an Establish transaction(Transaction with a new account and successful login).                                                                                                                                                                                                                 |
| 12.          | BE                 |                                     | If passing in SSN, demonstrate attribute is encrypted and no special characters.                                                                          | Merchant/operator approves the payout. Merchant pushes transaction to Completed status in Merchant Portal to receive the notifications.                                           |                                                | The SSN should be correctly encrypted by PIQ and decrypted by TrustlyUS.                                                                                                                                                                                                                                                                                               |
| 13.          | BE                 |                                     | If calling Cancel API, perform a Cancel call.                                                                                                             | Merchant to Post [Cancel](https://amer.developers.trustly.com/payments/reference/post-transactions-cancel).                                                                       |                                                | The cancel job for TrustlyUS will run every second checking if there are transactions for which no notification was received for more than 10 seconds. TrustlyUS can disable notifications so this use case can be tested.                                                                                                                                             |
| 14.          | BE                 |                                     | If calling Refund API, perform a Refund call.                                                                                                             | Merchant to Post [Refund](https://amer.developers.trustly.com/payments/reference/post-transactions-refund).                                                                       |                                                | Perform a `Refund` on a `SUCCESSFUL` deposit.                                                                                                                                                                                                                                                                                                                          |
| 15.          | BE                 |                                     | Demonstrate handling of webhook notifications and time-outs of notification.                                                                              |                                                                                                                                                                                   |                                                | Goes together with item `13`.                                                                                                                                                                                                                                                                                                                                          |
| 16.          | BE                 |                                     | Idempotency                                                                                                                                               | Merchant to confirm they are passing unique Merchant Reference value for all transactions.                                                                                        |                                                | Unique transaction ids.                                                                                                                                                                                                                                                                                                                                                |

## Example Routing Rule

![](/img/providers/routing/trustlyus.png)

## Test Information

Please check directly with the provider.