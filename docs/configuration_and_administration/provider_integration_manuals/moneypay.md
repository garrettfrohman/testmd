--- 
id: "moneypay" 
title: "MoneyPay"
hide_title: "true"
--- 
# MoneyPay

## About
MoneyPay is a Bank provider that offers deposit, withdrawal and status check. 

| Provider Name                | MoneyPay                                                                        |
|------------------------------|---------------------------------------------------------------------------------|
| Link                         | -                                                                               |
| Classification               | Online Banking                                                                  |
| Regions                      | `China`                                                                         |
| Currencies                   | Please check directly with the provider regarding what currencies are supported |
| Methods/PaymentTxTypes       | `MoneyPayDeposit`<br/> `MoneyPayWithdrawal`                                     |
| PaymentIQ Configuration File | `MoneyPayConfig`                                                                |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.moneypay.MoneyPayConfig>
   <enabled>true</enabled>
   <testMode>true</testMode>
     <width>600</width>
  <height>350</height>
  <accounts>
    <entry>
     <string>default</string>
     <account>
        <merchantId>??</merchantId>
        <secretKey>??</secretKey>
        <supportedCurrencies>CNY</supportedCurrencies>
     </account>
    </entry>
  </accounts>
  <redirectTemplateName>money_pay_bank_info_template</redirectTemplateName>
  <redirectUrl>${baseRedirectUrl}/api/moneypay/redirect/${ptx.txRefId}</redirectUrl>
  <callbackUrl>${baseCallbackUrl}/api/moneypay/callback</callbackUrl>
</com.devcode.paymentiq.integration.moneypay.MoneyPayConfig>
```
</details>

### Attributes

| PaymentIQ Backoffice | Description                                                                     |
|----------------------|---------------------------------------------------------------------------------|
| merchantId           | Corresponds to the `clientNumber` value from MoneyPay used in the all requests. |
| secretKey            | Corresponds to the `APIToken` value from MoneyPay and is used for encryption.   |

## Example Routing Rule

![](/img/providers/routing/moneypay.png)

## Test Information

The only supported currency is CNY.
After initiating the deposit, the deposit bank account details will be displayed to the user, then the user have to go to his bank application to deposit the fund. 

### Deposit
Last4Digits: 1234

UserName: David Chan

### Withdrawal

Account Number: 2560144400312

Bank Name: HSBC

Bank branch: Beijing Branch

Beneficiary Name: Mary Li


