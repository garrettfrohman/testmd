--- 
id: "afritickets" 
title: "Afritickets"
hide_title: "true"
--- 

# Afritickets

## About
Afritickets is a credit card provider that offers 3DS and N3DS deposits using two different types of accounts (3DS and N3DS) 
and a status check. The 3DS payments are being handled by the provider, outside PaymentIQ. 

| Provider Name                | Afritickets                                                          |
|------------------------------|----------------------------------------------------------------------|
| Link                         | [https://www.afritickets.com/](https://www.afritickets.com/)         |
| Classification               | `Debit/Credit Card Processor`                                        |
| Regions                      | `International`                                                      |
| Currencies                   | `EUR, GBP, USD, most African currencies and other global currencies` |
| Methods/PaymentTxTypes       | `CreditcardDeposit`                                                  |
| PaymentIQ Configuration File | `AfriticketsConfig`                                                  |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.afritickets.AfriticketsConfig>
    <enabled>true</enabled>
    <useViqProxy>true</useViqProxy>
    <accounts>
        <entry>
            <string>AFRITICKETS_3DS</string>
            <account>
                <merchantId>??</merchantId>
                <accountID>AFRITICKETS_3DS</accountID>
                <apiKey>??</apiKey>
                <secretKey>??</secretKey>
                <encryptionKey>??</encryptionKey>
                <use3Dsecure>true</use3Dsecure>
                <container>iframe</container>
            </account>
        </entry>
        <entry>
            <string>AFRITICKETS_NON3DS</string>
            <account>
                <merchantId>??</merchantId>
                <accountID>AFRITICKETS_NON3DS</accountID>
                <apiKey>??</apiKey>
                <secretKey>??</secretKey>
                <encryptionKey>??</encryptionKey>
                <use3Dsecure>false</use3Dsecure>
            </account>
        </entry>
    </accounts>
</com.devcode.paymentiq.integration.afritickets.AfriticketsConfig>
```

</details>

### Attributes

| Attribute     | Description                                                                                                                                                                                                                                                                |
|---------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| merchantId    | different for 3DS and NON3DS accounts  - provided by Afritickets to merchants                                                                                                                                                                                              |
| accountID     | different for 3DS and NON3DS accounts  - provided by Afritickets to merchants                                                                                                                                                                                              |
| apiKey        | used for signing requests                                                                                                                                                                                                                                                  |
| secretKey     | used for signing requests                                                                                                                                                                                                                                                  |
| encryptionKey | used for encrypting requests in VaultIQ - the original request with VaultIQ tag for credit cards and encrypted CVV goes through the VaultIQ proxy where the credit card credentials are complemented and the request is being encrypted using this key with 3DES algorithm |
| use3Dsecure   | to indicate if the account should use 3DS                                                                                                                                                                                                                                  |

NOTE: apiKey, secretKey and encryptionKey are provided by Afritickets via https://dashboard.afritickets.com/

In order to obtain them, please contact Afritickets technical support - they will create a required account and the set of keys will be in 
Settings -> API.
## Example Routing Rule

![](/img/providers/routing/afritickets.png)

## Transaction Flow

The transaction is initiated from the cashier using either a 3DS or NON3DS account. <br/>
The user enters the amount and the essential credit card parameters - number, holder name, CVV code and expiry date (MM/YYYY) .<br/>
After that the flow differs between 3DS and NON3DS accounts:
1) For 3DS accounts, the user gets redirected to another page when entering an OTP code is required. 
   Then PaymentIQ receives a callback with the transaction's result and verifies its status with the provider's endpoint.
2) For NON3DS accounts, PaymentIQ receives a response about the status of the transaction and verifies its status with the provider's endpoint.

NOTE: There is only one endpoint for live and test mode. In order to toggle between them, the access to the aforementioned
dashboard is required. After login in to the dashboard there is a button "Turn on/off Sandbox" in the panel on the left that 
turns the Sandbox (test) mode on and off.
## Test Information

Test cards with different use case scenarios are to be found under the following link

https://developer.flutterwave.com/docs/test-cards

Examples:

| Card number         | CVV | Expiry date |
|---------------------|-----|-------------|
| 4187 4274 1556 4246 | 828 | 09/2032     |
| 5438 8980 1456 0229 | 564 | 10/2031     |
