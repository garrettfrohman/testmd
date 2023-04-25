--- 
id: "pagava" 
title: "Pagava"
hide_title: "true"
---
 
![](/img/providers/logos/pagava.png)

# Pagava

## About
Pagava Pay helps makes it simple to pay and accept electronic and credit card payments in person, online or over the phone.

| Provider Name                | Pagava                                             |
|------------------------------|----------------------------------------------------|
| Link                         | [https://pagava-pay.com/](https://pagava-pay.com/) |
| Classification               | Wallet, Online Banking                             |
| Regions                      | `JPN`                                              |
| Currencies                   | `USD`, `JPY`                                       |
| Methods/PaymentTxTypes       | `WebRedirectDeposit` <br/> `BankLocalWithdrawal`   |
| PaymentIQ Configuration File | `PagavaConfig`                                     |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.pagava.PagavaConfig>
    <enabled>true</enabled>
    <useViqProxy>true</useViqProxy>
    <liveBankPayinEndPoint>??</liveBankPayinEndPoint>
    <testBankPayinEndPoint>??</testBankPayinEndPoint>
    <liveServiceEndPoint>??</liveServiceEndPoint>
    <testServiceEndPoint>??</testServiceEndPoint>
    <bankCodeMapping>PAYPAY->0033,MUFG->0005,RAKUTEN->0036,SMBC->0009</bankCodeMapping>
    <accounts>
        <entry>
            <string>PAYOUT</string>
            <account>
                <httpClientConfigEntry>
                    <redirectsEnabled>false</redirectsEnabled>
                </httpClientConfigEntry>
                <email>??</email>
                <password>??</password>
                <supportedCurrencies>USD|JPY</supportedCurrencies>
            </account>
        </entry>
        <entry>
            <string>BTB</string>
            <account>
                <httpClientConfigEntry>
                    <redirectsEnabled>false</redirectsEnabled>
                </httpClientConfigEntry>
                <apiKey>??</apiKey>
                <merchantId>??</merchantId>
                <supportedCurrencies>USD</supportedCurrencies>
            </account>
        </entry>
        <entry>
            <string>BTB-AUTO</string>
            <account>
                <httpClientConfigEntry>
                    <redirectsEnabled>false</redirectsEnabled>
                </httpClientConfigEntry>
                <apiKey>??</apiKey>
                <merchantId>??</merchantId>
                <supportedCurrencies>USD</supportedCurrencies>
            </account>
        </entry>
    </accounts>
    <defaultDescriptor>Devcode</defaultDescriptor>
    <testMode>true</testMode>

</com.devcode.paymentiq.integration.pagava.PagavaConfig>
```
</details>

### Attributes

| Attribute             | Description                                                                                                                                                                                                                                            |
|-----------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| apiKey                | Api key for Creditcard transactions (Provided by Pagava)                                                                                                                                                                                               |
| merchantId            | Merchant id in Pagava system (Provided by Pagava)                                                                                                                                                                                                      |
| email                 | Email to access Payout API (Provided by Pagava)                                                                                                                                                                                                        |
| password              | Password to access Payout API (Provided by Pagava)                                                                                                                                                                                                     |
| liveBankPayinEndPoint | Merchant specific prod bank payin url (ask Pagava to provide it). Add "/%s" at the end of API endpoint (f.e. "https://xxxxxxxxx/%s")                                                                                                                   |
| testBankPayinEndPoint | Merchant specific test bank payin url (ask Pagava to provide it). Add "/%s" at the end of API endpoint (f.e. "https://xxxxxxxxx/%s")                                                                                                                   |
| liveServiceEndPoint   | Merchant specific live bank payout url (ask Pagava to provide it). Add "/api/" at the end of API endpoint (f.e. "https://xxxxxxxxx/api/")                                                                                                              |
| testServiceEndPoint   | Merchant specific test bank payout url (ask Pagava to provide it). Add "/api/" at the end of API endpoint (f.e. "https://xxxxxxxxx/api/")                                                                                                              |
| bankCodeMapping       | Merchant specific list of bank codes and bank names. List of bank will be increased in the future (ask Pagava to provide actual list). Please configure it in the root level of config as following `PAYPAY->0033,MUFG->0005,RAKUTEN->0036,SMBC->0009` |

* Please note that for BankLocalWithdrawal (PAYOUT) only one of provider currencies are supported at one time (either JPY or USD). 
* Ask Pagava to reconfigure flow if you want to change currency. For any other currencies please create Forex rules (ask PaymentIQ Technical Support in case you need help). 

### Callback configuration

You need to ask Pagava team to set the callback URL for BTB PAYIN transactions.

| Environment | Payment method | Url                                                                               |
|-------------|----------------|-----------------------------------------------------------------------------------|
| Test        | BTB            | https://test-api.paymentiq.io/paymentiq/api/pagava/btb/callback/{merchantId}      |
| Live        | BTB            | https://api.paymentiq.io/paymentiq/api/pagava/btb/callback/{merchantId}           |
| Test        | BTB AUTO       | https://test-api.paymentiq.io/paymentiq/api/pagava/btb/auto/callback/{merchantId} |
| Live        | BTB AUTO       | https://api.paymentiq.io/paymentiq/api/pagava/btb/auto/callback/{merchantId}      |

where "merchantId" -- merchant ID on TEST or PROD.

### PSP Payment Method to TxType mapping

| PSP Payment Method | TxType              | Service                                        | Currency |
|--------------------|---------------------|------------------------------------------------|----------|
| BTB PAYIN-SEMI     | WebRedirectDeposit  | BTB                                            | USD      |
| BTB PAYIN-AUTO     | WebRedirectDeposit  | BTB_AUTO, BTB_AUTO_XXX (see description above) | USD      |
| BTB PAYOUT         | BankLocalWithdrawal |                                                | USD, JPY |

### Notes about using WebRedirectDeposit (BTB PAYIN-AUTO)

Pagava provides two flows for BTB PAYIN-AUTO - with and without "bank_code" provided.

To configure both of them required `WEBREDIRECT` service(s) in `MerchantConfig`. 
To create service with bank code correctly please add 4-digits code to the end of BTB_AUTO service. E.g. BTB_AUTO_0033, BTB_AUTO_0036.
If you want to configure service with bank name instead of bank code please create it in the following way BTB_AUTO + bank_name. E.g. BTB_AUTO_PAYPAY, BTB_AUTO_RAKUTEN. To configure this method it's necessary to add `bankCodeMapping` to config xml.

```xml
<entry>
    <string>WEBREDIRECT</string>
    <string>BTB_AUTO|BTB_AUTO_0033|BTB_AUTO_PAYPAY</string>
</entry>
```

### Notes about using BankLocalWithdrawal

The mandatory parameters to send to PaymentIQ in the BankLocalWithdrawal request are `bankName`, `bankClearingNumber`, `bankAccountNumber`, and `bankBeneficiaryName`. Please see further details about the request  in the front api bank parameter section.

If using the PaymentIQ standardised cashier it's important that the Cashier Payment Method-settings has the correct input configuration as in the example below (contact support to assist if and update is needed).

![](/img/providers/pagava-paymentmethod.png)

## Example Routing Rule

![](/img/providers/routing/pagava1.png)
![](/img/providers/routing/pagava2.png)
![](/img/providers/routing/pagava3.png)

## Test Information

Please check directly with the provider.
