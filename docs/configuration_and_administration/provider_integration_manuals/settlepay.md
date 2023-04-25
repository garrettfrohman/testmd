--- 
id: "settlepay" 
title: "SettlePay"
hide_title: "true"
---
 
![](/img/providers/logos/settlepay.png)

# SettlePay

## About
SettlePay is a payment provider offering creditcard deposit (3DS/N3DS), withdrawal and full refund.

| Provider Name                | SettlePay                                                   |
|------------------------------|-------------------------------------------------------------|
| Link                         | [https://settlepay.net/](https://settlepay.net/)            |
| Classification               | Debit/Credit Card Processor                                 |
| Regions                      | Ukraine and Europe (except sanctioned countries)            |
| Currencies                   | `UAH`, `EUR`                                                |
| Methods/PaymentTxTypes       | `CreditcardDeposit`<br/>`CreditcardWithdrawal`<br/>`Refund` |
| PaymentIQ Configuration File | `SettlePayConfig`                                           |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.settlepay.SettlePayConfig>
  <enabled>true</enabled>
  <useViqProxy>true</useViqProxy>
  <accounts>
    <entry>
      <string>DEPOSIT</string>
      <account>
        <accountID>??</accountID>
        <service>??</service><!--deposit service-->
        <walletId>??</walletId>
        <transactionChannel>??</transactionChannel>
        <apiToken>??</apiToken>
        <use3Dsecure>true</use3Dsecure>
        <useTokenId>false</useTokenId><!--true: enable recurring-->
        <supportedCurrencies>UAH|EUR</supportedCurrencies>
        <language>en</language>
      </account>
    </entry>
    <entry>
      <string>WITHDRAWAL</string>
      <account>
        <accountID>??</accountID>
        <service>??</service><!--withdrawal service-->
        <walletId>??</walletId>
        <transactionChannel>??</transactionChannel>
        <apiToken>??</apiToken>
        <supportedCurrencies>UAH</supportedCurrencies>
        <language>en</language>
      </account>
    </entry>
  </accounts>
  <testMode>true</testMode>
  <defaultDescriptor>Bambora payment ${ptx.txRefId}</defaultDescriptor>
</com.devcode.paymentiq.integration.settlepay.SettlePayConfig>
```
</details>

### Attributes

| Attribute                  | Description                                                                                                                     |
|----------------------------|---------------------------------------------------------------------------------------------------------------------------------|
| account.accountID          | Account identifier in the 4bill system. It is used to authenticate requests from PaymentIQ to the 4bill system.                 |
| account.service            | Service identifier (for deposit and withdrawal there are different service ids).                                                |
| account.walletId           | Wallet identifier in the 4bill system. Each wallet has balance and specific currency. You can have as many wallets as you wish. |
| account.transactionChannel | Point identifier in the 4bill system. You can have several points and it depends on configuration in the 4bill system.          |
| account.apiToken           | Secret string that is used to authorize requests from PaymentIQ to the 4bill system.                                            |

NOTE: SettlePay will provide all required information (in the above table) to the merchant directly.

## Example Routing Rule
![](/img/providers/routing/settlepay.png)

## Test Information

### Deposit

| Card Number      | Description                                                                                            |
|------------------|--------------------------------------------------------------------------------------------------------|
| 4000000000000010 | Successful deposit without 3D secure                                                                   |
| 5555555555554444 | Successful deposit without 3D secure                                                                   |
| 4000000000000028 | Unsuccessful deposit without 3D secure                                                                 |
| 4000000000000036 | Successful deposit with 3D secure. It is possible to simulate Successful and Failed 3D secure payment. |
| 4000000000000069 | Successful deposit with 3D secure that will require redirection                                        |
| 4000000000000077 | Payment with Lookup authorization. Success Lookup code is 000000                                       |

### Withdrawal

| Card Number      | Description
|------------------|-----------------------------------------------------------------------------|
| 4000000000000010 | Successful withdrawal                                                       |
| 4000000000000028 | Unsuccessful withdrawal                                                     |
| 5555555555554444 | Successful withdrawal, but final payment status is received with some delay |

You can use any cardholder name and CVV2/CVC2 with these PANs.

### Refund

Only full refund is allowed.
