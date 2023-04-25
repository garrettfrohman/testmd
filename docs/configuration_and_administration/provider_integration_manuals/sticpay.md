--- 
id: "sticpay" 
title: "SticPay"
hide_title: "true"
---
 
![](/img/providers/logos/sticpay.png)

# SticPay

## About
Sticpay is a e-wallet payment solution. SticPay  supports deposit and withdrawal.

| Provider Name                | Sticpay                                                                                                 |
|------------------------------|---------------------------------------------------------------------------------------------------------|
| Link                         | [https://www.sticpay.com/](https://www.sticpay.com/)                                                    |
| Classification               | Wallet                                                                                                  |
| Regions                      | `International`                                                                                         |
| Currencies                   | `CHF`, `CNY`, `EUR`, `GBP`, `HKD`, `IDR`, `INR`, `JPY`, `KRW`, `MXN`, `NPR`, `PHP`, `THB`, `USD`, `VND` |
| Methods/PaymentTxTypes       | `WebRedirectDeposit`<br/> `SticpayWithdrawal`                                                           |
| PaymentIQ Configuration File | `SticpayConfig`                                                                                         |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>


```xml
<com.devcode.paymentiq.integration.sticpay.SticpayConfig>
   <enabled>true</enabled>
   <testMode>false</testMode>
   <width>600</width>
   <height>600</height>
   <container>iframe</container>
  <accounts>
    <entry>
     <string>default</string>
     <account>
        <email>??</email>
        <secretKey>??</secretKey>
        <supportedCurrencies>USD|EUR</supportedCurrencies>
     </account>
    </entry>
  </accounts>
  <redirectUrl>${baseRedirectUrl}/api/sticpay/redirect/${ptx.txRefId}</redirectUrl>
  <callbackUrl>${baseCallbackUrl}/api/sticpay/callback/${ptx.txRefId}</callbackUrl>
</com.devcode.paymentiq.integration.sticpay.SticpayConfig>
```

</details>

### Attributes

| Attribute | Description                                                                                         |
|-----------|-----------------------------------------------------------------------------------------------------|
| email     | The Sticpay email which is connected to the merchant account                                        |
| secretKey | The Sticpay passphrase configured for the merchant account that is used for signing the transaction |

### API Configuration

As a merchant you need to login in to your account at the [Sticpay back office](https://mypage.sticpay.com) and click on “STICPAY API” to configure the API settings. The following fields needs to be added for live environment:

| Field         | Value                                                                                                         |
|---------------|---------------------------------------------------------------------------------------------------------------|
| Passphrase    | Select a Passphrase that is used for signing the transaction                                                  |
| Success URL   | https://api.paymentiq.io/paymentiq/api/sticpay/redirect/success                                               |
| Failure URL   | https://api.paymentiq.io/paymentiq/api/sticpay/redirect/failure                                               |
| Referer URL   | https://api.paymentiq.io/paymentiq/api/sticpay/redirect/cancel                                                |
| Callback URL  | https://api.paymentiq.io/paymentiq/api/sticpay/callback                                                       |
| Whitelist IPs | [Provider IP Whitelist](/../docs/configuration_and_administration/system_configuration/provider_ip_whitelist) |

### Notes

- You as a merchant need to add the logo into your cashier.

- If the merchant does not have any Sticpay wallet setup for the provided currency, the API will use the default merchant wallet currency.

## Transaction Flow

- When the user is doing deposit he/she will enter the amount and then he will get redirected to merchant page to log in to his/her e-wallet and confirm the deposit.

## Example Routing Rule

![](/img/providers/routing/sticpay.png)

## Test Information

### Test account

ID: test-customer5@sticpay.com

password: SticCustomer1234

D.O.B.: 1981-01-01

