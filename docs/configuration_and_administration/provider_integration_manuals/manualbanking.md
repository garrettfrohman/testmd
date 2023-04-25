--- 
id: "manualbanking" 
title: "ManualBanking"
hide_title: "true"
--- 
# ManualBanking

## About
ManualBanking is a 'mock' provider used to simulate bank withdrawal / deposit. These will then not be forwarded to any real provider but will still be logged in PaymentIQ.

| Provider Name          | ManualBanking                                                                                  |
|------------------------|------------------------------------------------------------------------------------------------|
| Classification         | Mock Provider                                                                                  |
| Methods/PaymentTxTypes | `BankLocalWithdrawal` <br/> `BankIBANWithdrawal` <br/> `BankIntlWithdrawal`<br/> `BankDeposit` |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.bank.withdrawal.ManualBankingConfig>
  <enabled>true</enabled>
  <accounts>
    <entry>
      <string>manual_deposit_sek</string>
      <account>
        <templateName>manual_deposit_sek</templateName>
      </account>
    </entry>
    <entry>
      <string>manual_deposit_eur</string>
      <account>
        <templateName>manual_deposit_eur</templateName>
      </account>
    </entry>
    <entry>
      <string>manual_deposit_gbp</string>
      <account>
        <templateName>manual_deposit_gbp</templateName>
      </account>
    </entry>
  </accounts>
</com.devcode.paymentiq.integration.bank.withdrawal.ManualBankingConfig>
```
</details>


### Attributes

| Attribute    | Description                                                                                                      |
|--------------|------------------------------------------------------------------------------------------------------------------|
| enabled      | Default set to `true`                                                                                            |
| templateName | Template to use for redirect to deposit (can be overriden by account). Default `manual-banking-deposit-template` |

### Configuration Steps

### Withdrawal
For ManualBanking withdrawals an email template needs to be setup which should contain information about the withdrawal request which is sent on to an agent.

1. Create an email template under **Admin** > **Templates** > **Email Templates**

    - Example Name: bank_withdrawal
    - Example Subject: `Bank withdrawal request from ${ptx.merchantUser.userId}`
    - Example Email:

```html
<html>
<body>
Hello!<br/>

Please do following payout:<br/>
User: ${ptx.merchantUser.userId}<br/>
Amount: ${ptx.txAmountAbs}<br/>

${if ptx.latestTxCmdMap.BankLocalWithdrawalInput}
Clearing number: ${ptx.latestTxCmdMap.BankLocalWithdrawalInput.clearingNumber}<br/>
Account number: ${ptx.latestTxCmdMap.BankLocalWithdrawalInput.accountNumber}<br/>
Beneficiary name: ${ptx.latestTxCmdMap.BankLocalWithdrawalInput.beneficiaryName}<br/>
${end}

${if ptx.latestTxCmdMap.BankIBANWithdrawalInput}
BIC: ${ptx.latestTxCmdMap.BankIBANWithdrawalInput.bic}<br/>
IBAN: ${ptx.latestTxCmdMap.BankIBANWithdrawalInput.iban}<br/>
Beneficiary name: ${ptx.latestTxCmdMap.BankIBANWithdrawalInput.beneficiaryName}<br/>
${end}

${if ptx.latestTxCmdMap.BankIntlWithdrawalInput}
Account number: ${ptx.latestTxCmdMap.BankIntlWithdrawalInput.accountNumber}<br/>
SWIFT / BIC: ${ptx.latestTxCmdMap.BankIntlWithdrawalInput.bic}<br/>
Bank name: ${ptx.latestTxCmdMap.BankIntlWithdrawalInput.bankName}<br/>
Branch address: ${ptx.latestTxCmdMap.BankIntlWithdrawalInput.branchAddress}<br/>

Beneficiary<br/>
Name: ${ptx.latestTxCmdMap.BankIntlWithdrawalInput.beneficiaryName}<br/>
Street: ${ptx.latestTxCmdMap.BankIntlWithdrawalInput.beneficiaryStreet}<br/>
Zip: ${ptx.latestTxCmdMap.BankIntlWithdrawalInput.beneficiaryZip}<br/>
City: ${ptx.latestTxCmdMap.BankIntlWithdrawalInput.beneficiaryCity}<br/>
State: ${ptx.latestTxCmdMap.BankIntlWithdrawalInput.beneficiaryState}<br/>

${end}    

Have a nice day!<br/>

</body>
</html>
```
2. Set up a Notification Rule under **Rules** > **Notification**. Example:

    ![](/img/providers/manualbanking01.png)

This way the merchant agent will receive an email on each withdrawal request with the relevant informtion needed for processing.    

#### Example Routing Rule
![](/img/providers/routing/manualbanking.png)

### Deposit
For ManualBanking deposit an html template needs to be setup which should contain information where the user can deposit to merchant bank account.

1. Create an html template under **Admin** > **Templates** > **HTML Templates**

    - Example Name: manual-banking-deposit-template
    - Example html:
```html
    <html>
    <body>
    Please use ${ptx.txRefId} for reference in bank payment order.
    
    Bank account in ${ptx.txAmountAbs.currencyCode}
    
    Account Holder: Bambora AB
    
    Bank Name: Bambora Bank
    
    IBAN: SE31xxxxxx
    
    BIC: SExxxx
    
    Reference: ${ptx.txRefId}

    Once we receive the payment, you will be notified via email.
    </body>
    </html>
```

#### Example Routing Rule
![](/img/providers/routing/manualbanking_deposit.png)

## Test Information

No testing information is available for this provider.

