--- 
id: "trustlycanada"
title: "TrustlyCanada"
hide_title: "true"
---

![](/img/providers/logos/trustlycanada.png)

# TrustlyCanada

## About
TrustlyCanada is a brand of Trustly for the Canada market. It offers WebRedirect deposits and withdrawals as well as refunds.

| Provider Name                | TrustlyCanada                                                     |
|------------------------------|-------------------------------------------------------------------|
| Link                         | [https://www.trustly.net/](https://www.trustly.net/)              |
| Classification               | Aggregator                                                        |
| Regions                      | `Canada`                                                          |
| Currencies                   | `CAD`                                                             |
| Methods/PaymentTxTypes       | `WebRedirectDeposit` <br/> `WebRedirectWithdrawal` <br/> `Refund` |
| PaymentIQ Configuration File | `TrustlyCanadaConfig`                                             |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.trustlycanada.TrustlyCanadaConfig>
  <enabled>true</enabled>
  <accounts>
    <entry>
      <string>default</string>
      <account>
        <merchantId>??</merchantId>
        <accountID>??</accountID>
        <apiKey>??</apiKey>
        <supportedCurrencies>CAD</supportedCurrencies>
        <forcePayment>TestNullSplitTokenUseCase</forcePayment>  
      </account>
    </entry>
  </accounts>
</com.devcode.paymentiq.integration.trustlycanada.TrustlyCanadaConfig>
```

</details>

### Attributes

| Attribute                   | Description                                                                                                                                    |
|-----------------------------|------------------------------------------------------------------------------------------------------------------------------------------------|
| account.merchantId          | Mandatory. A unique merchant identifier provided individually for each merchant account by TrustlyCanada.                                      |
| account.accountID           | Mandatory. A unique merchant account identifier provided individually for each merchant account by TrustlyCanada.                              |
| account.apiKey              | Mandatory. It is used to sign requests and validate signatures and should be provided by TrustlyCanada for each merchant account individually. |
| account.supportedCurrencies | Mandatory. The list of supported currencies for the account in use separated by \| (pipe character).                                           |
| account.forcePayment        | Optional. Used for testing purposes. When present in account config null splitToken use-case can be tested.                                    |

## Provider Configuration

In order to enable TrustlyCanada please follow these steps:

1. Run PaymentIQ and add the TrustlyCanada under Admin -> Configuration.
2. Add TrustlyCanada to the `<psp>` section in MerchantConfig under Admin -> Configuration.
3. Enable WEBREDIRECT-TRUSTLYCANADA deposit and withdrawal method in Rules -> Payment methods.

### Transaction Flow

#### Deposits

1. The user enters the amount to be deposited in the cashier.
2. If it's a first time the user makes a deposit via TrustlyCanada, the user gets redirected to the TrustlyCanada lightbox where
she / he is being asked to choose the bank account to be used for the deposit. If the user is using the account that already
   exists, step 4 is being directly executed.
3. TrustlyCanada sends an authorization callback with an authorization transaction ID (it will be the parent transaction ID for
   every subsequent deposit made under this user account in the future) as well as 'splitToken' (used to identify users' accounts
   in TrustlyCanada API) - these parameters are stored in the PaymentIQ database for further usage.
4. PaymentIQ sends a deposit request towards TrustlyCanada with the following scenarios are possible: <br/>
a) If TrustlyCanada responds with a successful/declined status, PaymentIQ sets the transaction status to SUCCESS/FAILED. <br/>
b) If TrustlyCanada responds with a pending status, PaymentIQ awaits a callback from TrustlyCanada, then performs a status check against the TrustlyCanada API and updates the status of the transaction accordingly. <br/>
c) If TrustlyCanada responds with a status that indicates that the split token used for the transaction has expired, the process
   begins again from step 2 (redirection to TrustlyCanada lightbox).<br/>

#### Withdrawal

1. The user enters the amount to be withdrawn in the cashier.
2. If it's a first time the user makes a withdrawal via TrustlyCanada, the user gets redirected to the TrustlyCanada lightbox where
   she / he is being asked to choose the bank account to be used for the deposit. If the user is using the account that already
   exists, step 4 is being directly executed.
3. TrustlyCanada sends an authorization callback with an authorization transaction ID (it will be the parent transaction ID for
   every subsequent deposit made under this user account in the future) as well as 'splitToken' (used to identify users' accounts
   in TrustlyCanada API) - these parameters are stored in the PaymentIQ database for further usage.
4. PaymentIQ sends a deposit request towards TrustlyCanada. If TrustlyCanada responds with a successful or pending status, 
   PaymentIQ will set the transaction's status to SUCCESS_WAITING_CONFIRMATION and the transfer will be made to deduct the amount from the user's balance. 
   Then, PaymentIQ awaits a callback from TrustlyCanada regarding the status of the withdrawal. In case of a callback with
   a successful status, PaymentIQ will update the transaction's state to SUCCESS_WITHDRAWAL_APPROVAL. In case of a callback
   with a declined status, a reversal transaction will take place and the amount will be restored to the user's balance.
   
## Example Routing Rule

![](/img/providers/routing/trustlycanada.png)

## Test Information

Please check directly with the provider.