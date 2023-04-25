--- 
id: "inovapay" 
title: "INOVAPAY"
hide_title: "true"
---
 
![](/img/providers/logos/inovapay.png)

# INOVAPAY

## About
INOVAPAY is the payment provider offering the following payment options:

### Bank deposit and status check
Customers go straight from the merchant checkout page to a payment interface which connects them with their bank of preference or other local in-country payment offerings. They are then connected to their online banking page to verify payment. Once finished they immediately receive confirmation on payment.

### Bank withdrawal
Merchants send funds directly into the customer’s bank account or pix key.

### Wallet deposit and withdrawal
E-money transfer service used to transfer money to and from merchants and top-up their user wallet.

| Provider Name                | INOVAPAY                                                                                                 |
|------------------------------|----------------------------------------------------------------------------------------------------------|
| Link                         | [https://www.inovapay.com/](https://www.inovapay.com/)                                                   |
| Classification               | Online Banking, Wallet                                                                                   |
| Regions                      | `Brazil`                                                                                                 |
| Currencies                   | Please check directly with the provider regarding what currencies are supported                          |
| Methods/PaymentTxTypes       | `BankDeposit`<br/> `InovapayBankWithdrawal`<br/> `InovapayWalletDeposit`<br/> `InovapayWalletWithdrawal` |
| PaymentIQ Configuration File | `InovapayConfig`                                                                                         |

## Supported Countries/Currencies
All currencies are managed under ISO 4217 Format

## Limits

### Bank
- Bank Deposit transfer: Min - 50 BRL, Max - 10000 BRL (Monthly Max - 10000 BRL)
- Bank Withdrawal transfer: Min - 200 BRL

### Wallet
- Min - 20 BRL, Max - 10000 BRL (Monthly Max - 10000 BRL)

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.inovapay.InovapayConfig>
  <enabled>true</enabled>
  <accounts>
    <entry>
      <string>DEFAULT</string>
      <account>
        <secretKey>??</secretKey>
        <supportedCurrencies>BRL</supportedCurrencies>
        <apiKey>??</apiKey>
        <terminal>??</terminal>
      </account>
    </entry>
  </accounts>
  <container>window</container>
  <waitForWithdrawalNotification>false</waitForWithdrawalNotification>
</com.devcode.paymentiq.integration.inovapay.InovapayConfig>
```

</details>

### Attributes

| Attribute | Description                                                                                   |
|-----------|-----------------------------------------------------------------------------------------------|
| secretKey | Corresponds to the API Secret from INOVAPAY. It is used to create JWT token from JSON request |
| apiKey    | Corresponds to the API Key from INOVAPAY. It is used to set 'x-api-key' request header        |
| terminal  | Merchant's terminal ID (e.g. merchant's name)                                                 |

### Wait For Bank Withdrawal Notifications
The normal scenario is that PaymentIQ sets the withdrawal to success after it has been successfully received by Inovapay and waiting for it to be processed. If anything goes wrong during processing a reversal is created. To instead wait with setting success until a notification that the money has reached the user's account can be done by adding this to InovapayConfig:

`<waitForWithdrawalNotification>true</waitForWithdrawalNotification>`

Note that there is always a risk invovled with using this configuration that the merchant needs to be aware of. If anything goes wrong with the transaction (e.g. misconfiguration, human error, connection issues etc) while it is waiting to be processed at the provider that causes PaymentIQ to set it to FAILED means that a cancel will be sent to the merchant. At the same time it is possible that the provider successfully executed it and the user received the money on their end.

### Callback URL
Callback URL is set by INOVAPAY. it is needed for Bank transactions only.

- Test: https://test-api.paymentiq.io/paymentiq/api/inovapay/callback 
- Production: https://api.paymentiq.io/paymentiq/api/inovapay/callback/

## Example Routing Rules
![](/img/providers/routing/inovapay.png)

## Transaction Flow

### Bank Deposit

After initiating the transaction with an `amount` of at least 50 BRL the user will be redirected to a bank selection page where the CPF value needs to be provided (CPF is the Brazilian individual taxpayer registry identification, a number attributed by the Brazilian Federal Revenue. Each user (email address) can only have one CPF number).

![](/img/providers/inovapay_bank_01.png)

After payment is confirmed the user will be redirected to the selected bank's page, e.g:

![](/img/providers/inovapay_bank_02.png)

#### Pre-select bank method
By sending the `service` parameter with the BankDeposit request you can pre-select the bank choice in Inovapay's form, which will also disable the option to change bank once pre-selected. Please see the valid service parameter values below.

| Service value | Inovapay value  |
|---------------|-----------------|
| PIX           | pix             |
| BANCODOBRASIL | banco-do-brasil |
| BRADESCO      | bradesco        |
| CAIXA         | caixa           |
| ITAU          | itau            |
| SANTANDER     | santander       |

#### Pre-fill CPF
By sending the `nationalId` parameter with the BankDeposit request you can pre-fill the CPF value in Inovapay's form, which will also disable the option to change this value by the user.

### Bank Withdrawal

To initiate the transaction select an `amount` of at least 200 BRL. If using Pix as method only the parameter `nationalId (CPF)` is required, make sure that the CPF used is registered as a Pix key, for the other bank options `branchCode`, `accountNumber` and `accountType` are also required.

## Test Information

### Bank Deposit
Perform a transaction with an `amount` of at least `50 BRL` and once redirected to the bank payment page a CPF value has to be provided as well as selecting the bank. The username and email values of the user are also connected to the correct CPF and have to match.

| Name         | Email                  | CPF         |
|--------------|------------------------|-------------|
| Lionel Messi | lionel.messi@barca.com | 14528508010 |

**Note: When you are testing transactions in UAT, confirmations or cancellations of transactions are done manually, so please send the INOVAPAY transactionID or PaymentIQ reference to INOVAPAY and they will approve or cancel payment and we will take action accordingly.**

### Wallet
Deposit: Specify `amount`, `userLogin` and `userSecretId`.

Withdrawal: Specify `amount`, `userLogin`.

| userLogin | userSecretId |
|-----------|--------------|
| 303870    | 225406       |
