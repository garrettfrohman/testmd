--- 
id: "flexepin" 
title: "Flexepin"
hide_title: "true"
---
 
![](/img/providers/logos/flexepin.png)

# Flexepin

## About
The Flexepin Group delivers end-to-end financial solutions enabling international electronic payment processes.

| Provider Name                | Flexepin                                                                        |
|------------------------------|---------------------------------------------------------------------------------|
| Link                         | [https://www.flexepin.com](https://www.flexepin.com)                            |
| Classification               | PrePaid Card / Voucher                                                          |
| Regions                      | `Australia`, `Canada`, `Greece`                                                 |
| Currencies                   | Please check directly with the provider regarding what currencies are supported |
| Methods/PaymentTxTypes       | `VoucherDeposit`<br/> `VoucherCreationWithdrawal`                               |
| PaymentIQ Configuration File | `FlexepinConfig`                                                                |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.flexepin.FlexepinConfig>
    <enabled>true</enabled>
    <accounts>
        <entry>
            <string>default</string>
            <account>
                <apiKey>??</apiKey>
                <secretKey>??</secretKey>
                <supportedCurrencies>CAD|EUR|AUD|USD</supportedCurrencies>
                <terminalId>??</terminalId>
                <transactionChannel>??</transactionChannel>
                <sendEmail>true</sendEmail>
            </account>
        </entry>
    </accounts>
</com.devcode.paymentiq.integration.flexepin.FlexepinConfig>
```
</details>

### Attributes

| Attribute                   | Description                                                                                         |
|-----------------------------|-----------------------------------------------------------------------------------------------------|
| account.apiKey              | Corresponds to `API Key` which  should be provided by Flexepin onboarding team.                     |
| account.secretKey           | Corresponds to `Secret Key` which  should be provided by Flexepin onboarding team.                  |
| account.supportedCurrencies | It is used to define supported currencies.                                                          |
| account.transactionChannel  | It is used to define channel used for Voucher deposits.                                             |
| account.sendEmail           | Flag used to enable automatic email sending to the user with a newly created Voucher Payout number. |

## Example Routing Rule
![](/img/providers/routing/flexepin.png)

## Transaction Flow

### Voucher Deposit
1. The user enters their voucher number. No amount required in the cashier.
2. PIQ validates voucher, populates transaction amount and proceeds with deposit.

### Voucher Withdrawal
1. The user enters the voucher type (product code). No amount is required from the cashier.
2. PIQ validates voucher type, populates transaction amount, and generates withdrawal request.
3. After withdrawal approval voucher code is generated and sent via email to the user.

## Test Information

### Voucher Deposit   
- Ask Flexepin team to provide you with new valid unused testing vouchers.
- 
### Voucher Withdrawal
- Ask Flexepin team to provide you with valid voucher types (product code).