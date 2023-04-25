--- 
id: "cryptopay" 
title: "CryptoPay"
hide_title: "true"
---
 
![](/img/providers/logos/cryptopaylogo.png)

# CryptoPay

## About
CryptoPay provides easy access to the crypto currency world, allowing users to utilise all the benefits of a secure wallet. Buy bitcoins,
litecoins and XRP with your debit or credit card and relish the fair rates and low fees.

| Provider Name                | CryptoPay                                                                       |
|------------------------------|---------------------------------------------------------------------------------|
| Link                         | [https://cryptopay.me](https://cryptopay.me)                                    |
| Classification               | Crypto Currency                                                                 |
| Regions                      | `Internatioal`                                                                  |
| Currencies                   | Please check directly with the provider regarding what currencies are supported |
| Methods/PaymentTxTypes       | `CryptoCurrencyDeposit` <br/> `CryptoCurrencyWithdrawal`                        |
| PaymentIQ Configuration File | `CryptoPayConfig`                                                               |

## Configuration Information
### Attributes

| Attribute      | Description                                                                                                 |
|----------------|-------------------------------------------------------------------------------------------------------------|
| apiKey         | Created in CryptoPay Backoffice as ApiKey.                                                                  |
| secretKey      | Created in CryptoPay Backoffice as SecretKey.                                                               |
| key1           | Created in CryptoPay Backoffice as Callback Secret.                                                         |
| method         | Set to CHANNEL to use the channel transaction flow.                                                         |
| createChannel  | Set to true if a new payment channel should be created for the user when making a regular deposit (invoice) |
| productName    | Name of the channel. Only used when creating a new channel. Defaults to "Channel".                          |
| showBackButton | Set to true to show a back button on CryptoPay's hosted redirect page.                                      |

### Example
```xml
<com.devcode.paymentiq.integration.cryptopay.CryptoPayConfig>
  <enabled>true</enabled>
  <accounts>
    <entry>
     <string>invoice</string>
     <account>
        <apiKey>???</apiKey>
        <secretKey>???</secretKey>
        <key1>???</key1>
     </account>
    </entry>
    <entry>
     <string>channel</string>
     <account>
        <method>CHANNEL</method>
        <apiKey>???</apiKey>
        <secretKey>???</secretKey>
        <key1>???</key1>
     </account>
    </entry>
  </accounts>
  <testMode>false</testMode>
</com.devcode.paymentiq.integration.cryptopay.CryptoPayConfig>
```

### Payment Channels
A payment channel is a static cryptocurrency address that is assigned to one user. The user can send cryptocurrency to their address and it will automatically create a transaction in PaymentIQ without going through the cashier flow.

#### Create a Channel
There are three options for creating a channel.

1. By adding `<method>CHANNEL</method>` to the account config of the account that is processing the transaction. This will create a new channel and redirect the user to the channel details immediately. The transaction will have state WAITING_INPUT until the first channel payment is made. Subsequent channel payments will create new transactions in PaymentIQ.

2. By adding `<createChannel>true</createChannel>` to the account config of the account that is processing the transaction. This will create a channel at the same time as the user is making a regular deposit. Note that the user's deposits should only be routed to this account when a channel should be created, if `<createChannel>true</createChannel>` is always used a new channel will be created for every deposit.

3. Initiate a CryptoPayDeposit with amount 0. This will create a transaction with TxType CryptoPayInitChannel and the only thing it will do is create the channel. No money will be transferred.

#### Notifications
Notifications can be setup in PaymentIQ to notify the user about the created channel. This is done by setting the notifications config on top level of CryptoPayConfig. The currently supported notification types are EMAIL and NOTIFICATION. The information included in the notifications is the URL received from CryptoPay that will show the details of the channel.

EMAIL will send an email to the user. The email template that is used is `cryptopay-createchannel-email`.

NOTIFICATION will send a notification through the integration API, i.e. to the merchant and not the user. For more info about the API see [here](/docs/apis_and_integration/integration_api/notification).

Example:

`<notifications>EMAIL</notifications>`

### Provider Configuration

To configure the CryptoPay API you need to:

First, ask The PaymentIQ Onboarding or Tech Support Team to add the CryptoPayConfig to your account.

Then you need to create a User account for the CryptoPay back-office.

| Environment | URL                                                                            |
|-------------|--------------------------------------------------------------------------------|
| Test        | [https://business-sandbox.cryptopay.me](https://business-sandbox.cryptopay.me) |
| Live        | [https://business.cryptopay.me](https://business.cryptopay.me/)                |

After logging in to the CryptoPay back-office account you need to turn on 2FA in Settings > Security. You will need a mobile device to do this.

When you have activated 2FA you can create the API Keys. Go to Settings > API and the API Keys section. Click "Add an API Key". 
![](/img/providers/cryptopay03.png)

Add something in the "Description" field (it can be anything). And click the checkboxes for the permissions you want to set. If you do not know what to set here, choose the following permissions:
![](/img/providers/cryptopay04.png)

When you have set the Description and Permissions click "Add an API Key" again. This will take you to a new window with a message "API Key create successfully." Copy the API Key and API Secret and click "I saved the key, close window".
![](/img/providers/cryptopay05.png)

The final step in the CryptoPay back-office needed is to specify the callback URL. This is done in Settings > API > Callback URL.
![](/img/providers/cryptopay06.png)

| Environment | Callback URL                                                                                                                       |
|-------------|------------------------------------------------------------------------------------------------------------------------------------|
| Test        | [https://test-api.paymentiq.io/paymentiq/api/cryptopay/callback/](https://test-api.paymentiq.io/paymentiq/api/cryptopay/callback/) |
| Live        | [https://api.paymentiq.io/paymentiq/api/cryptopay/callback/](https://api.paymentiq.io/paymentiq/api/cryptopay/callback/)           |

Add the callback URL and press "Save". Then click "Generate a new key" in the Callback Secret section and once again authorize with 2FA. Then copy the generated secret to the same place you made note of the API keys.

Now you can add the credentials to the CryptoPayConfig. The API key should be added to `apiKey` and the API secret to `secretKey`. The callback secret should be added to `key1`.

## Example Routing Rules

![](/img/providers/routing/cryptopayrouting.png)

## Test Information

After you initiate a deposit transaction and get redirected to the CryptoPay payment page,

  *Log in to your CryptoPay account, navigate to the accounts section.
  
  *Select the send option next to which currency you choose to use then you should get a pop up window like this:
  
  ![](/img/providers/cryptopay02.png)


  *Copy the exact amount and the address you have on the payment redirect page and add them as External Address and amount in   the new pop up window you have in your CryptoPay account and do a withdrawal.

PS: You need to contact CryptoPay support team to fill your sandbox account with an amount to be able to test.

In some cases invoices may be paid with incorrect transaction amounts or paid after the invoice expired.

You can configure how to handle your invoices automatically on the Settings page in your account. It's highly recommended to handle all the
unresolved invoices to "Automatically recalculate at a new exchange rate and settle" like this:

![](/img/providers/cryptopay01.png)
