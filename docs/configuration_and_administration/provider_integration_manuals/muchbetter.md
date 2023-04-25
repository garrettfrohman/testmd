--- 
id: "muchbetter" 
title: "MuchBetter"
hide_title: "true"
---
 
![](/img/providers/logos/muchbetter.png)

# MuchBetter

## About
MuchBetter is E-Wallet provider that offers deposit and withdrawal.

| Provider Name                | MuchBetter                                                                      |
|------------------------------|---------------------------------------------------------------------------------|
| Link                         | https://muchbetter.com/](https://muchbetter.com/)                               |
| Classification               | E-Wallet                                                                        |
| Regions                      | `International`                                                                 |
| Currencies                   | Please check directly with the provider regarding what currencies are supported |
| Methods/PaymentTxTypes       | `MuchBetterDeposit` <br/> `MuchBetterWithdrawal`                                |
| PaymentIQ Configuration File | `MuchBetterConfig`                                                              |


## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.muchbetter.MuchBetterConfig>
    <enabled>true</enabled>
    <useViqProxy>false</useViqProxy>
    <accounts>
        <entry>
            <string>default</string>
            <account>
                <requestKyc>true</requestKyc>
                <brandId>???</brandId>
                <apiKey>???</apiKey>
                <supportedCurrencies>USD|EUR|GBP</supportedCurrencies>
            </account>
        </entry>
    </accounts>
    <matchAccountHolderName>true</matchAccountHolderName>
    <defaultDescriptor>PaymentIQ payment</defaultDescriptor>
</com.devcode.paymentiq.integration.muchbetter.MuchBetterConfig>

```

</details>

### Attributes

| PaymentIQ Backoffice   | Description                                                                                                                        |
|------------------------|------------------------------------------------------------------------------------------------------------------------------------|
| apiKey                 | ApiKey provided by MuchBetter.                                                                                                     |
| brandId                | Use in account config. The value is sent to MuchBetter as parameter brandName                                                      |
| redirectToWaitingPage  | If set to true, the end user is redirected to a waiting page instead of directly to receipt                                        |
| matchAccountHolderName | Set to true if deposits/withdrawal should be auto reversed if full name (first name + last name) doesn't match. See details below. |
| requestKyc             | This controls if a KYC request should be performed before the transaction is initiated or not. This is specified on account level. |

### Callback URL:s

You will need to configure callback URL:s in the MuchBetter backoffice. Please use the following URL:s

- **Test:** https://test-api.paymentiq.io/paymentiq/api/callback/muchbetter
- **Production:** https://api.paymentiq.io/paymentiq/api/callback/muchbetter

### Install & Configure Mobile Application
You should receive an invitation from MuchBetter on your email in order to install MuchBetter mobile application on your mobile device.

1. Open link from invitation email in your mobile device.
2. Run the application and press "Sign Up": enter unique PIN and remember it. Re-Enter PIN once again, then you will receive  an SMS code to validate it. Then you are in.
3. You can go to 'settings' tab to enable notifications which will help you for testing, and can enter your name and address emails etc.

### MuchBetter Sign-up link
You can add a quick sing-up link to the PaymentIQ cashier for customers using MuchBetter for the first time.

This is by setting the message keys  `muchbetter.link.text` and `muchbetter.link.url` in the **Admin** > **Messages** section. It needs to be added to all Locales you intend to use.

For example setting `muchbetter.link.text` to "Don't have an account? Sign Up" and `muchbetter.link.url` to `https://a.api.muchbetter.com/merchant/user?trackingCode=ZZZZZZZZZ`

Will display in the cashier as:

![](/img/providers/muchbetter01.png)

Please note that the trackingCode is required and merchant specific and you should ask MuchBetter for it.

### Auto reverse deposit/withdrawal if account holder name (first name + last name) doesn't match
PaymentIQ can automatically reverse a deposit/withdrawal if the name on the provider side doesn't match with the name PaymentIQ receives from the verifyUser response. The matching algorithm used is "Levenshtein Distance" and the similarity between the strings must be at least 90% by default. This value can be configured with setting nameMatchPercentageThreshold.

The name matching feature is activated by adding the following configuration entry:

`<matchAccountHolderName>true</matchAccountHolderName>`

In the reversal (push) transaction the default transaction reference is "Deposit reversal". This can be changed by setting depositReversalReference to a different value in MuchBetterConfig.

## Example Routing Rule
![](/img/providers/routing/muchbetter.png)

## Test Information

Please check directly with the provider.