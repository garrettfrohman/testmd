--- 
id: "hyperwallet"
title: "Hyperwallet"
hide_title: "true"
---

![](/img/providers/logos/hyperwallet.png)

# Hyperwallet

## About
Hyperwallet is an aggregator provider that supports bank and PayPal withdrawals.

| Provider Name                | Hyperwallet                                                                     |
|------------------------------|---------------------------------------------------------------------------------|
| Link                         | [https://www.hyperwallet.com/](https://www.hyperwallet.com/)                    |
| Classification               | Aggregator                                                                      |
| Regions                      | `Global`                                                                        |
| Currencies                   | Please check directly with the provider regarding what currencies are supported |
| Methods/PaymentTxTypes       | `WebRedirectWithdrawal`                                                         |
| PaymentIQ Configuration File | `HyperwalletConfig`                                                             |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.hyperwallet.HyperwalletConfig>
    <enabled>true</enabled>
    <validCallbackIpAddresses>XX.XX.XX.0|XX.XX.XX.0</validCallbackIpAddresses>
    <accounts>
        <entry>
            <string>default</string>
            <account>
                <defaultDescriptor>OTHER</defaultDescriptor>
                <profileId>INDIVIDUAL</profileId>
                <username>??</username>
                <password>??</password>
                <userProgramToken>??</userProgramToken>
                <paymentsProgramToken>??</paymentsProgramToken>
                <supportedCurrencies>??</supportedCurrencies>
            </account>
        </entry>
    </accounts>
</com.devcode.paymentiq.integration.hyperwallet.HyperwalletConfig>
```

</details>

### Attributes

| Attribute                    | Description                                                                                                                                                                                                                               |
|------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| validCallbackIpAddresses     | Mandatory. List of valid callback Hyperwallet addresses separated  by '&#124;' (pipe character) that needs to be provided by Hyperwallet. WARNING! Please make sure to replace the last octet by '0' -> f.ex. 127.0.0.1 becomes 127.0.0.0 |
| account.defaultDescriptor    | Mandatory. It is send as a 'purpose' parameter in the payout request to Hyperwallet - please set it to 'OTHER'                                                                                                                            |
| account.profileId            | Mandatory. It is used in creating a new user in Hyperwallet - by default it should be set to 'INDIVIDUAL'                                                                                                                                 |
| account.username             | Mandatory. It is used for securing the requests sent to Hyperwallet and should be provided by Hyperwallet individually for each account used by the Merchant                                                                              |
| account.password             | Mandatory. It is used for securing the requests sent to Hyperwallet and should be provided by Hyperwallet individually for each account used by the Merchant                                                                              |
| account.userProgramToken     | Mandatory. The unique identifier for the user's program token which should be provided by Hyperwallet individually for each account used by the Merchant                                                                                  |
| account.paymentsProgramToken | Mandatory. The unique identifier for the payments program token which should be provided by Hyperwallet individually for each account used by the Merchant                                                                                |

## Provider Configuration

In order to enable Hyperwallet, please make sure to follow these steps:

1. Run PaymentIQ's backoffice.
2. Add Hyperwallet  to the `<psp>` section in MerchantConfig under Admin -> Configuration.
3. Enable WEBREDIRECT-BANK and WEBREDIRECT-PAYPAL withdrawal methods in Rules -> Payment methods.
4. Make sure that `hyperwallet-drop-in-template` is available for your MID -> please contact PaymentIQ tech support to 
make sure it is properly configured for you.

## Transaction Flow

1. The user enters the amount to be withdrawn in the cashier and clicks on 'Withdraw'.
2. If the user has not yet been registered in Hyperwallet yet, PaymentIQ sends a request to create the user on Hyperwallet's
side. In response, PaymentIQ receives a 'usr-token' which is a unique user identifier and is used as extAccRefId in UserPspAccountDetails.
3. If the account in use is not associated with an already created payment method, the user gets redirected to Hyperwallet's Drop-In UI
where she/he is being asked to enter the bank account / PayPal account details so that a new transfer method could be created.
After that, Hyperwallet sends the details of the newly created payment method along with the destination token which is a unique identifier
for a transfer method and is being used with every payout request send by PaymentIQ towards Hyperwallet.
4. Once the withdrawal has been approved by the merchant in the backoffice, PaymentIQ sends a payout request to Hyperwallet and based on the response the transaction is either declined or put in
the 'SUCCESS_WAITING_CONFIRMATION' state.
5. PaymentIQ awaits a callback from Hyperwallet. In case of a callback with a successful status, PaymentIQ updates the status
of the transaction to SUCCESS_WITHDRAWAL_APPROVAL. In case of a callback with a declined status, a reversal transaction
will take place and the amount will be restored to the user's ballance.

## Example Routing Rule

![](/img/providers/routing/hyperwallet.png)

## Test Information

Please check directly with the provider.