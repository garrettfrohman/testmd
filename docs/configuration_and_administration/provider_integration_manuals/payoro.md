--- 
id: "payoro" 
title: "Payoro"
hide_title: "true"
---
 
![](/img/providers/logos/payoro.png)

# Payoro

## About
Payoro is an innovative PSD2 account servicing platform, connecting consumers with European financial institutions.
Payoro enables easy bank account creation and money transfer through dynamic partner relationships and innovative fintech.

| Provider Name                | Payoro                                                                          |
|------------------------------|---------------------------------------------------------------------------------|
| Link                         | [https://payoro.com/](https://payoro.com/)                                      |
| Classification               | Online banking                                                                  |
| Regions                      | `International`                                                                 |
| Currencies                   | Please check directly with the provider regarding what currencies are supported |
| Methods/PaymentTxTypes       | `BankIBANWithdrawal`                                                            |
| PaymentIQ Configuration File | `PayoroConfig`                                                                  |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.payoro.PayoroConfig>
  <enabled>true</enabled>
  <accounts>
    <entry>
      <string>default</string>
      <account>
        <merchantId>???</merchantId>
      </account>
    </entry>
  </accounts>
</com.devcode.paymentiq.integration.payoro.PayoroConfig>
```

</details>

### Attributes

| Attribute  | Description                 |
|------------|-----------------------------|
| merchantId | merchantId in Payoro system |

## Example Routing Rule

![](/img/providers/routing/payoro.png)

## Transaction Flow
1. Regular withdrawal request happens from the PaymentIQ cashier or via API.
2. Based on Approval rules transaction is automatically approved or is requiring manual approval from PaymentIQ back office.
3. Transaction is set to ```SUCCESS_WAITING_CONFIRMATION``` status and funds are withdrawn from merchant’s user account, but not crediting to user’s IBAN yet. This happens to prevent issues when transaction is in intermediate state (for example, when merchant users are missing any data to finish withdrawal form on Payoro’s portal).
4. PaymentIQ sends email to merchant’s user email with a link to withdrawal form on Payoro’s portal. Merchant’s user email should be known by PaymentIQ for that purpose. To change default email template please contact PaymentIQ Technical Support.
5. Merchant’s user opens email from the inbox, navigates to withdrawal form on Payoro’s portal by clicking on link and finishes flow.
6. In some time PaymentIQ receives callback with result of withdrawal and transaction status is changed to ```SUCCESS_WITHDRAWAL_APPROVAL```/```SUCCESS_WITHDRAWAL_AUTO_APPROVAL``` in case of success, or ```reversal``` is happening and funds are returning back to merchant's user account in case of failure.

## Test Information
For testing purposes any BIC/IBAN could be used. <br/>
Login to Payoro's withdrawal test portal is possible with the following credentials:

| BankId      | OTP | password |
|-------------|-----|----------|
| 24119533534 | otp | qwer1234 |
