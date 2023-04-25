---
id: "premierpay"
title: "PremierPay"
hide_title: "true"
---

![](/img/providers/logos/premierpay.png)

# PremierPay

## About
PremierPay offers the following payment services:
- Interac Online (payment)
- Interac E-Transfer (payment and payout)
- DirectDebit (payment)
- DirectDebitPlus (payment)
- DirectCredit (payout).

E-Transfer Payment and Payout, Interac E-Transfer Payment and Payout and Bank Payment (DirectDebit) and Payout (DirectCredit)

DirectDebit allows customers to make purchases directly from their checking accounts, like an e-check. The service provides a safe page from which to enter account information.

DirectCredit works in much the same way, allowing a customer to enter bank account information so that payment can be credited to their account directly.

| Provider Name                | PremierPay                                                                                                                   |
|------------------------------|------------------------------------------------------------------------------------------------------------------------------|
| Link                         | [https://www.premierpay.ca/](https://www.premierpay.ca/)                                                                     |
| Classification               | Online Banking (Credit and Debit); Wallet Payments (Payin and Payout); Interac Online Wallet Payments (Payin)                |
| Regions                      | `CANADA`                                                                                                                     |
| Currencies                   | `CAD`                                                                                                                        |
| Methods/PaymentTxTypes       | `PremierPayDirectDeposit`<br/> `PremierPayDirectWithdrawal`<br/> `PremierPayWalletDeposit`<br/> `PremierPayWalletWithdrawal` |
| PaymentIQ Configuration File | `PremierPayConfig`                                                                                                           |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.premierpay.PremierPayConfig>
  <enabled>true</enabled>
  <useViqProxy>false</useViqProxy>
  <accounts>
    <entry>
      <string>default</string>
      <account>
        <secretKey>??</secretKey><!-- R-Code -->
        <productId>Test Item 1</productId><!-- product name -->
        <customerId>??</customerId><!-- CID -->
        <supportedCurrencies>CAD</supportedCurrencies>
      </account>
    </entry>
  </accounts>
  <defaultDescriptor>??</defaultDescriptor>
</com.devcode.paymentiq.integration.premierpay.PremierPayConfig>
```
</details>

### Attributes

| Attribute | Description                                                                               | Parameter in accountConfig |
|-----------|-------------------------------------------------------------------------------------------|----------------------------|
| SID       | This parameter is used to generate a request URL                                          | accountConfig.customerId   |
| R-Code    | This key is used to generate SHA256 signature and set it as "signature" request parameter | accountConfig.secretKey    |

### Notes
- Attributes should be provided by PremierPay Account Manager to secure payment.
- PremierPay can setup one SID for all payment methods. However it is possible to separate the payment methods by SID.
- It is required for the user to have the following info configured to make a successful payment: city, address, state, country, email, phone.

### PSP Service Mapping

| Classification | Provider Type    | PaymentIQ CMD                 | Service           | Comment                                                                     |
|----------------|------------------|-------------------------------|-------------------|-----------------------------------------------------------------------------|
| Online Banking | PREMIERPAYDIRECT | PremierPayDirectDepositCmd    | DIRECTDEBIT       | It is used to trigger Direct Debit deposit                                  |
| Online Banking | PREMIERPAYDIRECT | PremierPayDirectDepositCmd    | DIRECTDEBITPLUS   | It is used to trigger Direct Debit Plus deposit                             |
| Online Banking | PREMIERPAYDIRECT | PremierPayDirectWithdrawalCmd | -                 | It is used to trigger a Direct Credit (no "service" is required to be sent) |
| E-Wallet       | PREMIERPAYWALLET | PremierPayWalletDepositCmd    | INTERAC_ONLINE    | It is used to initiate a Interac Online wallet deposit                      |
| E-Wallet       | PREMIERPAYWALLET | PremierPayWalletDepositCmd    | INTERAC_ETRANSFER | It is used to initiate a Interac e-Transfer wallet deposit                  |
| E-Wallet       | PREMIERPAYWALLET | PremierPayWalletWithdrawalCmd | INTERAC_ONLINE    | It is used to trigger Interac Online wallet payout                          |
| E-Wallet       | PREMIERPAYWALLET | PremierPayWalletWithdrawalCmd | INTERAC_ETRANSFER | It is used to trigger Interac e-Transfer wallet payout                      |

## Example Routing Rule
![](/img/providers/routing/premierpay.png)

## Test Information

###  DirectDebit & DirectCredit
Specify amount, account holder, account number, financial institution and transit number to make bank payment
Please use "institute=123" & "transit=12345") for testing (it is a dummy institution set on their side).

###  DirectDebitPlus
Specify amount and press Pay button. Then you will be redirected to another page to specify all required info to complete payment.

### Interac Online
Specify amount and press Pay button.
After pressing Pay button you will be redirected to another page to complete payment. In test mode you will just be able to simulate success and failed payment by pressing a corresponding button.

### Interac E-Transfer
Specify amount and press Pay button to make payment.
