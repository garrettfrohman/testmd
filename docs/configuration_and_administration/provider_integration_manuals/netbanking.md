--- 
id: "netbanking" 
title: "NetBanking"
hide_title: "true"
---
 
![](/img/providers/logos/netbanking.png)

# NetBanking

## About
NetBanking is a banking provider that offers deposits and withdrawals using your bank account. Can only be used with currency INR.

| Provider Name                | NetBanking                                                                                       |
|------------------------------|--------------------------------------------------------------------------------------------------|
| Link                         | [http://rupeepayments.com/index.php/netbanking/](http://rupeepayments.com/index.php/netbanking/) |
| Classification               | Online Banking                                                                                   |
| Regions                      | `India`                                                                                          |
| Currencies                   | Please check directly with the provider regarding what currencies are supported                  |
| Methods/PaymentTxTypes       | `BankDeposit`<br/> `BankIntlWithdrawal`                                                          |
| PaymentIQ Configuration File | `NetBankingConfig`                                                                               |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.netbanking.NetBankingConfig>
  <enabled>true</enabled>
  <accounts>
    <entry>
      <string>default</string>
      <account>
        <merchantId>xx</merchantId>
        <secretKey>xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxx</secretKey>
        <supportedCurrencies>INR</supportedCurrencies>
      </account>
    </entry>
  </accounts>
</com.devcode.paymentiq.integration.netbanking.NetBankingConfig>
```

</details>

### Attributes

| Attribute  | Description                          |
|------------|--------------------------------------|
| merchantId | Provided by NetBanking. "MID code"   |
| secretKey  | Provided by NetBanking. "MID secret" |

### Withdrawals
NetBanking requires information about the bank to be sent in the withdrawal request. The values should be sent as the following BankIntlWithdrawalInput parameters:

| Bank info    | BankIntlWithdrawalInput parameter |
|--------------|-----------------------------------|
| Bank name    | bankName                          |
| Bank address | branchAddress                     |
| Branch name  | branchName                        |
| IFSC code    | bic                               |

## Example Routing Rules
![](/img/providers/routing/netbanking-dp.png)
![](/img/providers/routing/netbanking-wd.png)

## Test Information
User country must be `IN` and state must be set to a valid value, for example `MH`.

No information is entered for deposits, it will just redirect to a page where you can choose to simulate a successful or failed transaction.

Any bank details can be used to do withdrawals.

