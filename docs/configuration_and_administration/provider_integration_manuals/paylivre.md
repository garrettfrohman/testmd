--- 
id: "paylivre"
title: "Paylivre"
hide_title: "true"
---

![](/img/providers/logos/paylivre.png)

# Paylivre

## About
Paylivre is a Brazilian e-wallet and payment gateway, offering online deposits and withdrawals.

| Provider Name                | Paylivre                                                                                                            |
|------------------------------|---------------------------------------------------------------------------------------------------------------------|
| Link                         | [https://www.paylivre.com/](https://www.paylivre.com/)                                                              |
| Classification               | Online Banking                                                                                                      |
| Regions                      | `Brazil`                                                                                                            |
| Currencies                   | `USD`, `BRL`                                                                                                        |
| Methods/PaymentTxTypes       | `WebRedirectDeposit` <br/> `WebRedirectWithdrawal`<br/> `PaylivreDeposit`<br/> `PaylivreWithdrawal`<br/> `Reversal` |
| PaymentIQ Configuration File | `PaylivreConfig`                                                                                                    |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.paylivre.PaylivreConfig>
  <enabled>true</enabled>
  <testMode>true</testMode>
  <accounts>
    <entry>
      <string>PaylivreAccount</string>
      <gatewayVersion>??</gatewayVersion>
      <account>
        <merchantId>???</merchantId>
        <secretKey>??</secretKey>
        <accessToken>??</accessToken>
        <apiSalt>??</apiSalt>
        <supportedCurrencies>USD|BRL</supportedCurrencies>
      </account>
    </entry>
  </accounts>
  <container>window</container>
</com.devcode.paymentiq.integration.paylivre.PaylivreConfig>
```

</details>

### Attributes

| Attribute           | Description                                                                                                                                                                       |
|---------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| account.secretKey   | It is send over with each deposit and withdrawal request, it is generated on the partner's account under https://playground.paylivre.com/ -> Profile -> Security -> Token for API |
| account.accessToken | It is send over with each deposit and withdrawal request, it is generated on the partner's account under https://playground.paylivre.com/ -> Profile -> Security -> Gateway Token |
| account.apiSalt     | It is used to create signatures of callbacks and can be obtained on the account under https://playground.paylivre.com/ -> Profile -> Security -> Callback Token                   |
| merchantId          | Paylivre merchant ID                                                                                                                                                              |
| gatewayVersion      | Set 'v2' to use zero-question-asked mode                                                                                                                                          |

- The ways to obtain each of these parameters are described in the "Api Credentials" section.
- Additionally, an email template has to be added in our backoffice - please contact our technical support for that.

### Api Credentials

#### Secret key
In order to set your secretKey parameter in the backoffice, please follow these steps:
1. Log in to the Paylivre dashboard from the partner account.
2. Go to Profile -> Security -> Token for API -> click GENERATE NEW TOKEN
3. Take the generated token and use it as the secretKey in the backoffice config.

#### Access token
In order to set your accessToken parameter in the backoffice, please follow these steps:
1. Log in to the Paylivre dashboard from the partner account.
2. Go to Profile -> Security -> Gateway Token -> click GENERATE NEW TOKEN
3. Take the generated token and use it as the accessToken in the backoffice config

#### API Salt
In order to set your apiSalt parameter in the backoffice, please follow these steps:
1. Generate your own salt key - please make sure that it's unique, it will be used to sign the callbacks. It might be
   any string.
2. Go to Profile -> Security -> Callback Token -> paste the generated salt and click "SAVE TOKEN".
3. Use the same salt key as the apiSalt in the backoffice config

:::warning

The PaymentIQ team is not responsible for generating your API salt - please use your trusted procedures or generators.
The API salt should be confidential as well as any other API parameters.

:::

#### Merchant ID
Get your Merchant ID by logging to your Back-Office account
Go to Profile -> Verifications.
![](/img/providers/paylivre.png)

## Transaction Flow

NOTE: An email address assigned to the user's account is sent as a part of each request from PaymentIQ to the PSP.
This email address has to be the same as the one registered in Paylivre with the customer's account (more on account types
in the "Testing Information" section).

### Deposits
1. User enters an amount in the cashier and clicks on "Deposit".
2. PaymentIQ sends a GET request to the PSP. An url is received in response, to which the user is redirected
   and completes the transaction.
4. PaymentIQ receives a callback from the PSP with a transaction status and updates the transaction accordingly.

### Withdrawals
1. User enters an amount in the cashier and clicks on "Withdraw".
2. PaymentIQ sends a GET request to the PSP. An url is received in response which is stored by PaymentIQ.
3. The withdrawal is initiated and has to be approved in the backoffice if auto-approvals have not been set.
4. Once the withdrawal has been approved, the user receives a link via the registered email address to the aforementioned
   url to complete the withdrawal in the Paylivre's dashboard.
5. PaymentIQ receives a callback from the PSP with a transaction status and updates the transaction accordingly.

## Example Routing Rule

![](/img/providers/routing/paylivre1.png)
![](/img/providers/routing/paylivre2.png)

## Test Information

The credentials for https://playground.paylivre.com/ dashboard should be provided by Paylivre's technical support.
Two types of accounts have to be provided:
1. A partner's account - this type of account will be used by the merchant to manage and review transactions.
2. A customer's account - this type account will be used by the customer to manage her/his own transactions.