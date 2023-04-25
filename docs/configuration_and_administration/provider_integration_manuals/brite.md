---
id: "brite"
title: "Brite"
hide_title: "true"
---

![](/img/providers/logos/brite.png) 

# Brite

## About
Brite is an online banking provider which enables customers to pay with their bank account instantly.

| Provider Name                | Brite                                                                                                                                               |
|------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------|
| Link                         | [https://britepaymentgroup.com/](https://britepaymentgroup.com/)                                                                                    |
| Classification               | Online Banking                                                                                                                                      |
| Regions                      | `See list below`                                                                                                                                    |
| Currencies                   | `SEK`, `EUR`                                                                                                                                        |
| Methods/PaymentTxTypes       | `BankDeposit`<br/> `BankWithdrawal`<br/> `BankLocalWithdrawal`<br/> `BankIBANWithdrawal`<br/> `BankIntlWithdrawal`<br/> `BriteBankClientWithdrawal` |
| PaymentIQ Configuration File | `BriteConfig`                                                                                                                                       |


:::info Availability
          
-	Austria: PayOut
-	Finland: PayIn/PayOut
-	Germany: PayOut
-	Latvia: PayOut
-	Netherlands: PayIn/PayOut
-	Spain: PayOut
-	Sweden: PayIn/PayOut
-	Estonia Payin/Payout
-	Ireland: Payout
-	Grecce: Payout
-	Italy: Payout
-	Portugal: Payout
-	Slovakia: Payout
-	Slovenia: Payout
-	United Kingdom: Payout
-	Lithuania: Payout
-	Belgium: Payout
-	France: Payout
:::

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.brite.BriteConfig>
  <enabled>true</enabled>
  <accounts>
    <entry>
      <string>default</string>
      <account>
        <pspPublicKey>?????????????????</pspPublicKey>
        <secretKey>???????????????????????</secretKey>
        <supportedCurrencies>SEK</supportedCurrencies>
     </account>
    </entry>
  </accounts>
</com.devcode.paymentiq.integration.brite.BriteConfig>
```

</details>

### Attributes

| Attribute                    | Description                                                                                                                                                                                                                                                                 |
|------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| pspPublicKey                 | Public key provided by Brite                                                                                                                                                                                                                                                |
| secretKey                    | Secret key provided by Brite                                                                                                                                                                                                                                                |
| selectAccount                | Set to false to not redirect the user for withdrawal account selection, see more info below.                                                                                                                                                                                |
| prependSsnWithCountryCode    | Set to true to prepend SSN with two letter country code                                                                                                                                                                                                                     |
| closeLoop                    | If set to true, IBAN matching will be performed for BankIBANWithdrawals or closed_loop parameter is included to bank client withdrawal request. If closed_loop is included into request, customer cannot change existing bank account number on provider's redirect window. |
| defaultDescriptor            | Field only required for Germany to provide additional information to the end consumers what the transaction is for. It works only for withdrawals.                                                                                                                          |
| matchAccountHolderName       | Set to true if withdrawal should be auto refund/declined if name doesn't match. See details below.                                                                                                                                                                          |
| nameMatchPercentageThreshold | See details below.                                                                                                                                                                                                                                                          |
| nameMatchIgnoreCase          | See details below.                                                                                                                                                                                                                                                          |
| nameMatchIgnoreMiddleNames   | See details below.                                                                                                                                                                                                                                                          |


### Withdrawals
To use the same user psp account for deposits and withdrawals the TxTypes BankDeposit and BankWithdrawals should be used. That will create an account with type BANK.

BankLocalWithdrawal, BankIBANWithdrawal and BankIntlWithdrawal can be used as well but note that the bank account details in the input will be ignored and the user will be redirected to their bank for account selection if it is the first withdrawal. Also note that it will create user psp accounts with the type of the corresponding TxType. For example BankLocalWithdrawal will create an account of type BANKLOCAL.

#### Select Account Redirection
The default for withdrawals without a saved user psp account from Brite is to be redirected to Brite's account selection page where the user will login and select the account they want the money to be withdrawn to.

This flow is only supported in some countries. See below table, always check with Brite for an updated version though. For countries that doesn't support the account selection flow the TxType BankIBANWithdrawal must be used and the account must be configured with `<selectAccount>false</selectAccount>`.

| Country        | Supports account selection flow |
|----------------|---------------------------------|
| Austria        | Yes                             |
| Belgium        | No                              |
| Estonia        | Yes                             |
| Finland        | Yes                             |
| France         | No                              |
| Germany        | Yes                             |
| Greece         | No                              |
| Ireland        | No                              |
| Italy          | No                              |
| Latvia         | No                              |
| Lithuania      | No                              |
| Netherlands    | Yes                             |
| Portugal       | No                              |
| Slovakia       | No                              |
| Slovenia       | No                              |
| Spain          | No                              |
| Sweden         | Yes                             |
| United Kingdom | No                              |

### Prepopulate SSN
If the attribute nationalIdentificationNumber is included in the verifyUser response it will be provided to Brite when starting the payment. This will prepopulate the SSN field when the user logs in to the bank.

Example: `"nationalIdentificationNumber": "196408233234",`

### Prepend SSN with country code
The two letter country code can optionally be added in the beginning of the SSN returned from Brite. For example if Brite returns the Finnish SSN `20010101-123C` PaymentIQ will format it as `FI20010101-123C`.

To activate this feature add the following configuration entry:

`<prependSsnWithCountryCode>true</prependSsnWithCountryCode>`

### Decline/auto refund withdrawal if the account holder name doesn't match
PaymentIQ can auto refund/decline the withdrawal if the name returned from the provider doesn't match with the name PaymentIQ receives from the verifyUser response. The matching algorithm used is "Levenshtein Distance" and the similarity between the strings must be at least 90% by default. This value can be configured with setting nameMatchPercentageThreshold.

By default the matching will be case sensitive and all middle names will be considered. This can be configured with the settings nameMatchIgnoreMiddleNames and nameMatchIgnoreCase. For example, to ignore all middle names add the following configuration entry:

`<nameMatchIgnoreMiddleNames>true</nameMatchIgnoreMiddleNames>`

The name matching feature is activated by adding the following configuration entry:

`<matchAccountHolderName>true</matchAccountHolderName>`

__NOTE:__

BriteBankClientWithdrawal:
Name matching is done in the callback after the withdrawal is already made. If names don't match an automatic refund will be made, and if this operation is successful, the transaction will end up in the `FAILED` state with the status `ERR_DECLINED_NAME_MISMATCH`. In other case, the transactions will end up in the `INCONSISTENT` state with the status `ERR_NAME_MISMATCH`.

BankWithdrawal:
Name matching is done in the callback before withdrawal operation is triggered. The transactions will end up in the `FAILED` state with the status `ERR_DECLINED_NAME_MISMATCH`.

For all other withdrawal transaction types, transactions will end up in the `INCONSISTENT` state with the status `ERR_NAME_MISMATCH`.


## Example Routing Rules
![](/img/providers/routing/brite.png)

### Bank Client Withdrawal Routing
![](/img/providers/routing/brite-bank-client.png)

## Test Information

Please check directly with the provider.