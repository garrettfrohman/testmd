---
id: "rupeepayments"
title: "RupeePayments"
hide_title: "true"
---

![](/img/providers/logos/rupeepayments.png)

# RupeePayments

## About
RupeePayments is a payment provider that offers Bank deposit and withdrawal using your bank account and Cash on Delivery deposit and withdrawal.

Refund and Reversal can be done from the providers' back office (in that case additional notification about transaction status change will be sent to PaymentIQ).


RupeePayments is a replacement of NetBanking PSP. It has the same functionality as NetBanking (but with new API). It will be used instead of NetBanking and NetBanking will be disabled.

| Provider Name                | RupeePayments                                                                                              |
|------------------------------|------------------------------------------------------------------------------------------------------------|
| Link                         | [http://rupeepayments.com/index.php/netbanking/](http://rupeepayments.com/index.php/netbanking/)           |
| Classification               | Banking, Cash                                                                                              |
| Regions                      | `India`                                                                                                    |
| Currencies                   | `INR`*                                                                                                     |
| Methods/PaymentTxTypes       | `BankDeposit`<br/> `BankIntlWithdrawal`<br/> `RupeePaymentsCashDeposit`<br/> `RupeePaymentsCashWithdrawal` |
| PaymentIQ Configuration File | `RupeePaymentsConfig`                                                                                      |

\* For processing INR currency is supported only. For settlements, RupeePayments supports USD, EUR (SWIFT account only), USDT and Bitcoin.


## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.rupeepayments.RupeePaymentsConfig>
  <enabled>true</enabled>
  <testMode>true</testMode>
  <accounts>
    <entry>
      <string>default</string>
      <account>
        <merchantCode>xxx</merchantCode><!--midcode-->
        <merchantSecret>########-####-####-####-############</merchantSecret><!--midesecret-->
        <supportedCurrencies>INR</supportedCurrencies>
      </account>
    </entry>
  </accounts>
  <defaultDescriptor>Payment ${ptx.txRefId}</defaultDescriptor>
</com.devcode.paymentiq.integration.rupeepayments.RupeePaymentsConfig>
```
</details>

### Attributes
| Attribute              | Description                                                                                                                                               |
|------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------|
| account.merchantCode   | Corresponds to the "midcode" from RupeePayments. Required for bank and Cash o Delivery related operations. It is used to generate a request signature.    |
| account.merchantSecret | Corresponds to the "midesecret" from RupeePayments. Required for bank and Cash o Delivery related operations. It is used to generate a request signature. |

### NOTES
- RupeePayments will provide all required information (in the table above) to the merchant directly.
- NetBanking accounts (`midcode` and `midesecret` from "NetBankingConfig") can be used to make bank payments via RupeePayments.
- In order to make Cash on Delivery via RupeePayments, merchant can also use `midcode` and `midesecret` (they will just need to check with provider if Cash on Delivery is enabled for their account).

### Deposit
It is required to send `service=UPI/NET_BANKING` in order to trigger a corresponding deposit payment method. By default NetBanking will be triggered if no service will be provided.

UPI and NetBanking deposits via RupeePayments require no additional information to be provided.

### Withdrawal
It is required to send `service=UPI/NET_BANKING` in order to trigger a corresponding withdrawal payment method. By default NetBanking will be triggered if no service will be provided.

UPI and NetBanking withdrawals via RupeePayments require information about the bank to be sent in the withdrawal request. The values should be sent as the following `BankIntlWithdrawalInput` or `BankLocalWithdrawalInput` (with `BankMapping`) parameters:

| Bank info      | BankIntlWithdrawalInput | BankLocalWithdrawalInput with BankMapping |
|----------------|-------------------------|-------------------------------------------|
| Account Number | accountNumber           | accountNumber                             |
| Bank name      | bankName                | bankMapping.bankName                      |
| Bank address   | branchAddress           | bankMapping.bankAddress                   |
| Branch name    | branchName              | bankMapping.branchName                    |
| IFSC code      | bic                     | bankMapping.swift                         |

## Example Routing Rule
![](/img/providers/routing/rupeepayments.png)

## Test Information
User country must be `IN` and state must be set to a valid value, for example `MH`.

No information is entered for deposits, it will just redirect to a page where you can choose to simulate a successful or failed transaction.

Any bank details can be used to do withdrawals.

### BankLocalWithdrawal
To use `BankLocalWithdrawal` tx type, you will need a Bank Mapping that can be defined in the PaymentIQ back office: **Admin > Bank Mapping**.<br/>
In the request (or PaymentIQ Cashier) you will need to provide account number and SWIFT.<br/>
In the Bank Mapping you will need to define: bank address, branch name, bank name and SWIFT.

### BankIntlWithdrawal
To use `BankIntlWithdrawal` tx type, you will need to provide in the request (or PaymentIQ Cashier) account number, bank address ("Branch Address" field), branch name and IFSC code ("BIC/SWIFT" field).
