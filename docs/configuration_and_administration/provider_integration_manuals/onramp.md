--- 
id: "onramp" 
title: "OnRamp"
hide_title: "true"
---
 
![](/img/providers/logos/onramp.png)

# OnRamp

## About
OnRamp is revolutionising online payments using blockchain for reliable, efficient and private transactions for the benefit of both buyers and sellers. 

The OnRamp E-Wallet is built using Coinweb™ technology which connects multiple blockchains in parallel allowing individual users to instantly exchange between different digital assets.

| Provider Name                | OnRamp                                                 |
|------------------------------|--------------------------------------------------------|
| Link                         | [https://onrampwallet.com/](https://onrampwallet.com/) |
| Classification               | Wallet                                                 |
| Regions                      | `Japan`, `Canada`, `France`                            |
| Currencies                   | `EUR`, `CAD`, `USD`                                    |
| Methods/PaymentTxTypes       | `WebRedirectDeposit`, `WebRedirectWithdrawal`          |
| PaymentIQ Configuration File | `OnRampConfig`                                         |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.onramp.OnRampConfig>
    <enabled>true</enabled>
    <useViqProxy>true</useViqProxy>
    <accounts>
        <entry>
            <string>ONRAMP</string>
            <account>
                <use3Dsecure>false</use3Dsecure>
                <apiKey>??</apiKey>
                <merchantName>??</merchantName>
                <beneficiaryLogoUrl>https://www.nevergonnagiveyouup.com/some.png</beneficiaryLogoUrl>
                <supportedCurrencies>EUR|USD</supportedCurrencies>
            </account>
        </entry>
    </accounts>
    <testMode>true</testMode>
    <defaultDescriptor>DevCode payment</defaultDescriptor>
</com.devcode.paymentiq.integration.onramp.OnRampConfig>
```

</details>

### Attributes

| Attribute                        | Description                    |
|----------------------------------|--------------------------------|
| accountConfig.apiKey             | API key provided by OnRamp     |
| accountConfig.merchantName       | Merchant Name.                 |
| accountConfig.beneficiaryLogoUrl | URL to merchant's logo in PNG. |

An email template for withdrawals has to be added in the PaymentIQ backoffice - please contact our technical support for that.

## Example Routing Rule

![](/img/providers/routing/onramp.png)

## Transaction Flow

### Deposits
1. User enters an amount in the cashier and clicks on "Deposit".
2. PaymentIQ sends a POST request to the PSP. An url is received in response, to which the user is redirected
   and where he fills in the info for completing transaction.
3. PaymentIQ receives a callback from the PSP and send back response with HTTP status 200.
Provider uses callback to confirm transaction. If response code is 200 - transaction confirmed, if response code is 204 - transaction canceled.
4. PaymentIQ pulls transaction status from OnRamp status endpoint and updates transaction accordingly.

### Withdrawals
1. User enters an amount in the cashier and clicks on "Withdraw".
2. The withdrawal is initiated and has to be approved in the backoffice if auto-approvals have not been set.
3. PaymentIQ sends a POST request to the PSP. An url is received in response which is stored by PaymentIQ.
4. Once the withdrawal has been approved, the user receives a link via the registered email address to the aforementioned
   url to complete the withdrawal in the OnRamp's dashboard. If user is not signed-in in OnRamp system, this url will take him to the sign-in page.
5. PaymentIQ receives a callback from the PSP and sends back response with HTTP status 200.
6. PaymentIQ pulls transaction status from OnRamp status endpoint and updates transaction accordingly.

## Test Information

| Card Number      | CVV | Expiry Date     |
|------------------|-----|-----------------|
| 4012001037141112 | 083 | Any future date |
| 4929421234600821 | 356 | Any future date |
