--- 
id: "finxp"
title: "FinXP"
hide_title: "true"
---

![](/img/providers/logos/finxp.png)

# FinXP

## About
FinXP is a payment provider offering bank deposits and withdrawals (including SEPA withdrawal) in EUR currency only.

| Provider Name                | FinXP                                                                                                      |
|------------------------------|------------------------------------------------------------------------------------------------------------|
| Link                         | https://finxp.com/                                                                                         |
| Classification               | Banking                                                                                                    |
| Currencies                   | `EUR`                                                                                                      |
| Methods/PaymentTxTypes       | `BankIBANDeposit`<br/> `BankIBANWithdrawal`<br/> `AccountCreationDeposit`<br/> `AccountCreationWithdrawal` |
| PaymentIQ Configuration File | `FinXPConfig`                                                                                              |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.finxp.FinXPConfig>
    <enabled>true</enabled>
    <testMode>true</testMode>
    <accounts>
        <entry>
            <string>DEFAULT</string>
            <account>
                <merchantId>???</merchantId>
                <merchantAccountNumber>???</merchantAccountNumber>
                <secretKey>???</secretKey>
                <apiKey>???</apiKey>
                <notificationSecret>???</notificationSecret>
                <merchantName>???</merchantName>
                <defaultDescriptor>test</defaultDescriptor>
                <supportedCurrencies>EUR</supportedCurrencies>
            </account>
        </entry>
    </accounts>
</com.devcode.paymentiq.integration.finxp.FinXPConfig>
```
</details>

### Attributes

| Attribute                     | Description                                                                                                |
|-------------------------------|------------------------------------------------------------------------------------------------------------|
| account.merchantId            | Corresponds to the "X-merchant" provided by FinXP                                                          |
| account.merchantAccountNumber | Corresponds to account number in IBAN4U system (for deposit and withdrawal) or IBAN (for SEPA withdrawal). |
| account.secretKey             | Corresponds to "Staging secret" provided by FinXP.                                                         |
| account.apiKey                | Corresponds to "Staging key" provided by FinXP.                                                            |
| account.merchantName          | Merchant name which will be used for payments.                                                             |
| account.defaultDescriptor     | Info which will be added to payments as "remarks".                                                         |


### PSP Payment Method to TxType mapping

| PSP Payment Method               | TxType                                            | Service    |
|----------------------------------|---------------------------------------------------|------------|
| IBAN4U Bank Transfer Payin       | BankIBANDeposit                                   | IBAN4U     |
| IBAN4U Bank Transfer Payout      | BankIBANWithdrawal                                | IBAN4U     |
| IBAN (SEPA) Bank Transfer Payout | BankIBANWithdrawal                                | SEPA       |
| Creat New IBAN4U Account         | AccountCreationDeposit, AccountCreationWithdrawal | NEW_IBAN4U |

By default, the following payment channels are defined: `BankIBANDeposit_IBAN4U->PAYIN_MERCHANT,BankIBANWithdrawal_IBAN4U->PAYOUT_MERCHANT,BankIBANWithdrawal_SEPA->PAYOUT_SEPACT, AccountCreationDeposit_NEW_IBAN4U->APPLY_NEWIBAN4U`.<br/>

Also, merchant need to specify created services in MerchantConfig:
- IBAN4U, SEPA under BANKIBAN entry
- NEW_IBAN4U under ACCOUNTCREATION entry

```xml
<serviceMapping>
    <entry>
        <string>BANKIBAN</string>
        <string>IBAN4U|SEPA</string>
    </entry>
    <entry>
        <string>ACCOUNTCREATION</string>
        <string>NEW_IBAN4U</string>
    </entry>
</serviceMapping>
```
### Notification configuration
For receiving notification merchant needs to ask FinXP to configure Webhook URL for them in format
```
TEST: https://test-api.paymentiq.io/paymentiq/api/finxp/callback
PROD: https://api.paymentiq.io/paymentiq/api/finxp/callback
```
## Example Routing Rule
![](/img/providers/routing/finxp.png)
![](/img/providers/routing/finxp2.png)

## Deposit Testing Flow

Deposit method implemented via BankIBANDeposit.
After redirection user needs to Approve or Cancel payment. In case of approval user requires to pass OTP Verification. For stage the code is 111111 (will be provided by FinXP along with all credentials).

## Withdrawal Testing flow

FinXP bank withdrawal works as direct IBAN withdrawal and can take some time to be processed. Provider can send notification for this payment method within 30 days.

## New Account Creation Testing Flow

Create new account method is implemented via AccountCreationDeposit and AccountCreationWithdrawal. 
Transaction will be created without no amount in it. 
After press "Deposit" or "Withdrawal" button user will be redirected to FinXP page where user should create new account in IBAN4U system.
Client accounts are usually opened within one business day, unless the client is deemed to be high risk, in which case, further documents are requested.
After check will be done on FinXP side user will receive email with new IBAN4U and will be able to make all payments.
