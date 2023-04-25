--- 
id: "azupay" 
title: "Azupay"
hide_title: "true"
---

![](/img/providers/logos/azupay.png)

# Azupay

## About
Azupay allows your business to create PayIDs that your customers can use to pay for the services you provide.

**PayID** is the name of the New Payments Platform (NPP) addressing service.
It’s a function of the Platform that allows users to link easy-to-remember pieces of information, such as their phone number or email address, to their account.
Users can provide their PayID, instead of their BSB and account number, to people or organisations they wish to receive payments from in real-time.

| Provider Name                | Azupay                                                             |
|------------------------------|--------------------------------------------------------------------|
| Link                         | [https://azupay.com.au/](https://azupay.com.au/)                   |
| Classification               | Wallet                                                             |
| Regions                      | `Australia`                                                        |
| Currencies                   | `AUD`                                                              |
| Methods/PaymentTxTypes       | `WebRedirectDeposit` <br/> `AzupayWalletWithdrawal` <br/> `Refund` |
| PaymentIQ Configuration File | `AzupayConfig`                                                     |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.azupay.AzupayConfig>
    <enabled>true</enabled>
    <testMode>false</testMode>
    <defaultDescriptor>[description for create/register PayID requests]</defaultDescriptor>
    <accounts>
        <entry>
            <string>default</string>
            <account>
                <accountID>[accountID]</accountID>
                <pspPrivateKey>[pspPrivateKey]</pspPrivateKey>
                <pspPublicKey>[pspPublicKey]</pspPublicKey>
                <supportedCurrencies>AUD</supportedCurrencies>
                <defaultDescriptor>[description for withdrawal requests]</defaultDescriptor>
                <extraParameters>{"domain":[domainNameForPayID],"createPayID":[true/false]</extraParameters>
            </account>
        </entry>
    </accounts>
</com.devcode.paymentiq.integration.azupay.AzupayConfig>
```
Example with set variables:
```xml
<com.devcode.paymentiq.integration.azupay.AzupayConfig>
    <enabled>true</enabled>
    <testMode>false</testMode>
    <defaultDescriptor>PayID for the top-up of a user</defaultDescriptor>
    <accounts>
        <entry>
            <string>default</string>
            <account>
                <accountID>12345678901234567890123456789012</accountID>
                <pspPrivateKey>1234567890abcdef</pspPrivateKey>
                <pspPublicKey>1234567890ghijkl</pspPublicKey>
                <supportedCurrencies>AUD</supportedCurrencies>
                <defaultDescriptor>Payment to a user</defaultDescriptor>
                <extraParameters>{"domain":"happy.com.au","createPayID":true</extraParameters>
            </account>
        </entry>
    </accounts>
</com.devcode.paymentiq.integration.azupay.AzupayConfig>
```

</details>

### Attributes


| Attribute                           | Description                                                                                                                                                                                                                                             |
|-------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| config.defaultDescriptor            | Corresponds to the description of the request for create/register PayID. Should be at least 5 characters long. If absent - the default is going to be used: _"PayID for the top-up for {ptx.merchantUser.firstname} {ptx.merchantUser.lastName}."_      |
| account.accountID                   | Corresponds to the client id provided by Azupay. Id of the client creating the request for payment. This is supplied by azupay and only changes between environments.                                                                                   |
| account.pspPrivateKey               | Corresponds to the client secret key provided by Azupay. The secret key is used to access restricted functions and should be stored securely in your system. It is required for operations which may result in additional charges to you as a merchant. |
| account.pspPublicKey                | Corresponds to the client distributable key provided by Azupay. The distributable key has limited access and may be exposed publicly to your customers.                                                                                                 |
| account.defaultDescriptor           | Corresponds to the description of a withdrawal request. Should be at least 5 characters long. If absent - the default is going to be used: _"Payment to {ptx.merchantUser.firstname} {ptx.merchantUser.lastName}."_                                     |
| account.extraParameters.createPayID | Allows to generate a unique PayID at PaymentIQ side for further registration at Azupay. If not set - treated as "false" - PayID is going to be created at Azupay side, and "domain" value is going to be ignored.                                       |
| account.extraParameters.domain      | In case "createPayID" is set to "true" - provides the domain name to be appended to the created email-type PayID.                                                                                                                                       |

## Example Routing Rule

![](/img/providers/routing/azupay.png)

## Transaction Flow

### Deposit:

1. Customer (a user of a merchant) requests PayID registration for further payment (top-up of his/her account within merchant's system).<br/>
2. PayID (in a form of email) is being generated either by PaymentIQ or by Azupay (depending on the settings above) and provided to the customer.<br/>
3. Customer proceeds with the payment in favor of the provided PayID in his/her banking app (possibly multiple times with any amounts).<br/>
4. Assets are being transferred to Azupay side.<br/>
5. Azupay notifies merchant on incoming deposit transaction.<br/>
6. Merchant tops-up the customer's account in the merchant's system.<br/>

### Withdrawal:

1. Customer (a user of a merchant) requests withdrawal of his/her account funds within merchant's system.<br/>
2. Customer chooses the type of his/her personal account (BSB; PayID: EMAIL or PHONE) for the funds to be transferred to.<br/>
3. Customer provides account details and amount to be withdrawn.<br/>
4. Customer submits the request for withdrawal.<br/>
5. Azupay processes the request and notifies merchant on any status change of the transaction.<br/>
6. Merchant updates the user account's balance according to the status notifications from Azupay.<br/>
7. Customer either gets his/her requested funds on his/her account or the withdrawal request is cancelled with respective reason.<br/>

## Available Services (APM's)

When using the Azupay withdrawal transaction type, the service parameter in the table below is the value that should be sent in the `service` parameter to decide the specific APM to be used.

| Service parameter | Specific data to provide                        |
|-------------------|-------------------------------------------------|
| BSB               | bsb, accountNumber                              |
| EMAIL_OR_PHONE    | valid email or phone in a format: +AA-BBBBBBBBB |

## Test Information

Requires having account in Azupay UAT environment.<br/>
(excerpt from the provider's documentation):<br/>

To create your UAT account, there are a few simple steps that you will need to complete.

#### Step 1: Sign up to Azupay Help Centre

1. Sign up and create an account through the [Azupay Help Centre](https://azupay.atlassian.net/servicedesk/customer/user/signup?destination=portals)
2. A link will be sent to the email you have signed up with.<br/>
3. Follow the received link to complete sign up. You will be prompted to enter your full name and to create a password

#### Step 2: Create a New Azupay UAT Account
4. Select "Create a new azupay account (uat)" through [Azupay account for UAT](https://azupay.atlassian.net/servicedesk/customer/portal/3/user/login?destination=portal%2F3%2Fgroup%2F3%2Fcreate%2F10031) request form.<br/>
5. Enter the following details:

- Company Name
- PayID domain(s) - eg: @mycompany.com.au
- Additional dashboard access - include at least one email address(es) for users who require access to the dashboard.<br/>

6. Click "send" once you have completed the request. The Azupay team will set your UAT up within 48 hours
7. Once you are set up, you will receive an email with your username and temporary password to sign up through [Azupay's Dashboard](https://dashboard-uat.azupay.com.au/)
8. Log in using the temporary password and create a new password
9. You are all set up and ready to go!<br/>
