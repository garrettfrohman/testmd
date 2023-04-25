--- 
id: "cryptonpay" 
title: "CryptonPay"
hide_title: "true"
---

![](/img/providers/logos/cryptonpaylogo.png)

# CryptonPay

## About
CryptonPay provides CryptoCurrency deposits/withdrawals for multiple currencies and countries.

| Provider Name                | CryptonPay                                               |
|------------------------------|----------------------------------------------------------|
| Link                         | [https://cryptonpay.com/](https://cryptonpay.com/)       |
| Classification               | Crypto Currency                                          |
| Regions                      | `International`                                          |
| Currencies                   | `USD`                                                    |
| Methods/PaymentTxTypes       | `CryptoCurrencyDeposit` <br/> `CryptoCurrencyWithdrawal` |
| PaymentIQ Configuration File | `CryptonPayConfig`                                       |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.cryptonpay.CryptonPayConfig>
    <enabled>true</enabled>
    <accounts>
        <entry>
            <string>DEFAULT</string>
            <account>
                <merchantId>???</merchantId>
                <apiKey>???</apiKey>
                <supportedCurrencies>USD</supportedCurrencies>
            </account>
        </entry>
    </accounts>
    <testMode>false</testMode>
    <defaultDescriptor>???</defaultDescriptor>
</com.devcode.paymentiq.integration.cryptonpay.CryptonPayConfig>
```
</details>

### Attributes

| Attribute  | Description                                                                                                                                             |
|------------|---------------------------------------------------------------------------------------------------------------------------------------------------------|
| merchantId | A unique merchant identifier assigned to merchant. It is different from PaymentIQ merchantId and is assigned by CryptonPay upon registration with them. |
| apiKey     | Created in CryptonPay Backoffice as apiKey (see further details below).                                                                                 |

### Provider Configuration

To configure the CryptonPay API you need to:

First, merchant should add a new configuration under "Admin" -> "Configuration" in PaymentIQ. The reference configuration can be found in the "Configuration Information" Example.
And then should create an account in CryptonPay back-office.

| Environment | URL                                                                |
|-------------|--------------------------------------------------------------------|
| Live        | [https://api.cryptonpay.com](https://api.cryptonpay.com)           |
| Test        | [https://test.api.cryptonpay.com](https://test.api.cryptonpay.com) |

Once you have a CryptonPay back-office account, the callback URL should be specified. This is done in "Settings" > "Call Back URL".

| Environment | Callback URL                                                                                                                         |
|-------------|--------------------------------------------------------------------------------------------------------------------------------------|
| Test        | [https://test-api.paymentiq.io/paymentiq/api/cryptonpay/callback/](https://test-api.paymentiq.io/paymentiq/api/cryptonpay/callback/) |
| Live        | [https://api.paymentiq.io/paymentiq/api/cryptonpay/callback/](https://api.paymentiq.io/paymentiq/api/cryptonpay/callback/)           |

Add the callback URL, Support email and press "Update Settings". 

![](/img/providers/cryptonpay.png)

The next step is to copy the api key from "API Keys" section. Now you can add the API key to `apiKey` in the CryptonPayConfig.

## Example Routing Rules

![](/img/providers/routing/cryptonpayrouting.png)

## Test Information

### Deposit:
After you initiate a deposit transaction and get redirected to the CryptonPay payment page, copy the exact amount and the address you have on the payment redirect page and do the deposit accordingly.
PS: You need to contact CryptonPay support team to fill your sandbox account with an amount to be able to test.

### Withdrawal:
To do a withdrawal, user should specify Amount, CryptoCurrency, Wallet address and press *Withdrawal* button.
