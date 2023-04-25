--- 
id: "zotapay" 
title: "ZotaPay"
hide_title: "true"
---
 
![](/img/providers/logos/zotapay.png)

# ZotaPay

## About
Zotapay is a global payment service provider that facilitates online payment processing solutions for emerging markets worldwide, supplying innovative and secure technology. 
Zotapay services include but are not limited to, credit and debit cards, alternative methods, and local solutions, all under one service provider and one simple API.

| Provider Name                | ZotaPay                                                                         |
|------------------------------|---------------------------------------------------------------------------------|
| Link                         | [https://zotapay.com/](https://zotapay.com/)                                    |
| Classification               | Online Banking                                                                  |
| Regions                      | `International`                                                                 |
| Currencies                   | Please check directly with the provider regarding what currencies are supported |
| Methods/PaymentTxTypes       | `WebRedirectDeposit` <br/> `BankDomesticWithdrawal`                             |
| PaymentIQ Configuration File | `ZotaPayConfig`                                                                 |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.zotapay.ZotaPayConfig>
    <enabled>true</enabled>
    <accounts>
        <entry>
            <string>ZOTAPAY</string>
            <account>
                <merchantId>??</merchantId>
                <secretKey>??</secretKey>
                <siteId>??</siteId>
                <supportedCurrencies>??</supportedCurrencies>
            </account>
        </entry>
    </accounts>
    <testMode>true</testMode>
    <defaultDescriptor>DevCode payment</defaultDescriptor>
</com.devcode.paymentiq.integration.zotapay.ZotaPayConfig>
```

</details>

### Attributes

| Attribute                | Description                                                                                                                                                                                                                                                           |
|--------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| accountConfig.merchantId | Unique Merchant identifier in ZotaPay system.                                                                                                                                                                                                                         |
| accountConfig.secretKey  | Secret key provided to merchant by ZotaPay. It is used for creating the signature for requests to ZotaPay API                                                                                                                                                         |
| accountConfig.siteId     | Endpoint ID provided to merchant by ZotaPay. Unique endpoint identifier. All payment requests are sent to every ZotaPay API endpoint wtih this ID. In one specific endpoint ID only one specific currency is supported (for example on ID 12314 only EUR can be used) |

## Example Routing Rule

![](/img/providers/routing/zotapay.png)

## Transaction Flow

### Deposits
1. User enters an amount in the cashier and clicks on "Deposit".
2. PaymentIQ sends a POST request to the PSP. An URL is received in response, to which the user is redirected
   and completes the transaction.
3. PaymentIQ receives a callback from the PSP with a transaction status and updates the transaction accordingly.

### Withdrawals (Payout form flow)
1. User enters input (amount, bank name, account number, account holder, account type) in the cashier and clicks on "Withdrawal".
2. The withdrawal is initiated and has to be approved in the backoffice if auto-approvals have not been set.
3. PaymentIQ sends a POST request to the PSP. An url is received in response. The URL is sent to user's email. User follows this URL and confirms transaction.
4. PaymentIQ receives a callback from the PSP with a transaction status and updates the transaction accordingly.

### Withdrawals (Payout flow)
1. User enters input (amount, bank name, account number, account holder, account type) in the cashier and clicks on "Withdrawal".
2. The withdrawal is initiated and has to be approved in the backoffice if auto-approvals have not been set.
3. PaymentIQ sends a POST request to the PSP. Information about withdrawal transaction is received in response. (order id) 
4. PaymentIQ receives a callback from the PSP with a transaction status and updates the transaction accordingly.

## Test Information
Account number for successful withdrawal transaction: 1234567890.

Any other account number value can be used for reproducing failed transaction.
