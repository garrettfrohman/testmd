--- 
id: "isignthis" 
title: "Isignthis"
hide_title: "true"
---
 
![](/img/providers/logos/isignthis.png)

# Isignthis

## About
The Isignthis is a credit card provider that offers deposits, voids and refunds in the future.

| Provider Name                | Isignthis                                                                                                                   |
|------------------------------|-----------------------------------------------------------------------------------------------------------------------------|
| Link                         | [https://docs.api.isignthis.com/](https://docs.api.isignthis.com/)                                                          |
| Classification               | Debit/Credit Card Processor                                                                                                 |
| Regions                      | `International`                                                                                                             |
| Currencies                   | Please check directly with the provider regarding what currencies are supported                                             |
| Methods/PaymentTxTypes       | `CreditcardDeposit`<br/> `Void`<br/> `WebRedirectDeposit`<br/> `SofortDeposit`<br/> `BankDeposit`<br/> `BankIBANWithdrawal` |
| PaymentIQ Configuration File | `IsignthisConfig`                                                                                                           |

## Configuration Information

### Attributes

| PaymentIQ Configuration | Can be set at              | Required | Description                                                                                                             |
|-------------------------|----------------------------|----------|-------------------------------------------------------------------------------------------------------------------------|
| apiClient               | Config, account root level | Yes      | Is provided by Isignthis (This is the api client name)                                                                  |
| apiToken                | Config, account root level | Yes      | Provided by Isignthis, a bearer token sent in each request for authentication                                           |
| notificationToken       | Config, account root level | Yes      | Provided by Isignthis, a secret token to check the notifications                                                        |
| tokenParamName          | Config root level          | No       | Name of http header where the notification checksum is sent from Isignthis, default is: X-ISX-Checksum                  |
| supportedLanguages      | Config root level          | No       | Supported languages on Isignthis pages, default is: are listed here https://docs.api.isignthis.com/supported-languages/ |
| streetNumberPatterns    | Config root level          | No       | Patterns to extract street and street number from the verify user street field                                          |
| language                | Config account level       | No       | Default language for Isignthis pages if the sent language is not supported                                              |
| merchantId              | Config account level       | Yes      | Provided by Isignthis, a merchant id                                                                                    |
| workflow                | Config account level       | Yes      | Provided by Isignthis, the workflow to use at Isignthis, ex: ACQUIRING,EMONEY,FLYKK,FLYKKIB,SOFORT                      |
| acquirerId              | Config account level       | No       | Provided by Isignthis, acquirerId to use. Use this to override the Isignthis smart routing                              |
| serviceEndpoint         | Config account level       | No       | Provided by Isignthis, used for overriding of default serviceEndpoint config value                                      |

## Workflows

### Acquiring
Workflow name: ```ACQUIRING```

TxType: ```CreditcardDeposit```

Creditcard payments with support for 3DS 1.0.

#### Example Routing Rule
![](/img/providers/routing/isignthis.png)

### Emoney (Paydentity)

Workflow name: ```EMONEY```

TxType: ```WebRedirectDeposit```

Creditcard payments including kyc collection for merchant and is ready for PSD2.
More info can be found here: [https://www.isignthis.com/our-technology/](https://www.isignthis.com/our-technology/)

#### Example Routing Rule
![](/img/providers/routing/isignthis_emoney.png)

### Flykk
Workflow name: ```FLYKK```

TxType: ```WebRedirectDeposit```

Flykk® combines payment, banking and eMoney services, which also leverage Paydentity™ KYC service.
More info can be found here: [https://www.isignthis.com/knowledge/flykk-feature](https://www.isignthis.com/knowledge/flykk-feature)

#### Example Routing Rule
![](/img/providers/routing/isignthis_flykk.png)

### Flykk Instant Bank Transfer
Workflow name: ```FLYKKIB```

TxType: ```BankDeposit```

#### Example Routing Rule
![](/img/providers/routing/isignthis_flykkib.png)

### Bank IBAN Payouts
#### Configuration 
| Attribute                                                   | Description                                                                                                                                                                                                 |
|-------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| accountConfig.merchantId                                    | Merchant ID provided by Isignthis.                                                                                                                                                                          |
| accountConfig.merchantAccountNumber                         | Merchant's IBAN number set on Isignthis side. Used in the request parameter *sender_iban* of batch payout request.                                                                                          |
| accountConfig.apiClient                                     | Corresponds to the *Domain* value provided by Isignthis.                                                                                                                                                    |
| accountConfig.apiToken                                      | Corresponds to the *Subdomain* value provided by Isignthis.                                                                                                                                                 |
| accountConfig.apiKey                                        | The key used for creating payout batch request signature payload. String of 2 or 3 random symbols. Example: *Tr2*                                                                                           |
| accountConfig.secretKey                                     | The HMAC-SHA512 key used for creating payout batch request signature. String of random symbols. Example: *YUFG4gfwe82dnfm*                                                                                  |
| accountConfig.payoutsPrivateKey                             | The RSA 4096 private key used for encrypting payout batch request signature and decrypting payout callback notification signature.                                                                          |
| accountConfig.defaultDescriptor or config.defaultDescriptor | Default description of the payout transaction. Mandatory.                                                                                                                                                   |
| accountConfig.serviceEndpoint                               | Should be set either to *https://api.payout.isx.money/api* in case of using Isignthis production environment or to *https://api.stage.payout.isx.money/api* in case of using Isignthis staging environment. |

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.isignthis.IsignthisConfig>
    <enabled>true</enabled>
    <useViqProxy>true</useViqProxy>
    <accounts>
        <entry>
            <string>payouts</string>
            <account>
                <merchantId>??</merchantId>
                <merchantAccountNumber>??</merchantAccountNumber>
                <supportedCurrencies>EUR</supportedCurrencies>
                <serviceEndpoint>https://api.stage.payout.isx.money/api</serviceEndpoint>
                <apiClient>??</apiClient>
                <apiToken>??</apiToken>
                <apiKey>??</apiKey> <!--key included in signature-->
                <secretKey>??</secretKey> <!--hmac key-->
                <payoutsPrivateKey>??</payoutsPrivateKey> <!--RSA 4096 private key-->
                <defaultDescriptor>Bank Payout</defaultDescriptor>
            </account>
        </entry>
    </accounts>
    <testMode>true</testMode>
</com.devcode.paymentiq.integration.isignthis.IsignthisConfig>
```

</details>

#### Flow
1. Fill in inputs for Bank IBAN withdrawal in the PaymentIQ cashier.
2. After withdrawal approval, the payout batch request is sent to Isignthis and the batch ID from the response is saved in the transaction as pspRefId. The transaction status at this moment remains *SUCCCES_WAITING_CONFIRMATION*.
3. Notification about final status of payout batch is sent to PaymentIQ. 
If the notification has failed or canceled batch status, the reversal transaction will be triggered.
If the notification has successful batch status, the batch details endpoint is called by PaymentIQ to get the actual status of the transaction. 
If the retrieved status is successful, the transaction will be confirmed and its status going to be assigned either to *SUCCESS_WITHDRAWAL_APPROVAL* or SUCCESS_WITHDRAWAL_AUTO_APPROVAL. 
If the retrieved status is failed, reversal transaction will be triggered.

#### Example Routing Rule
![](/img/providers/routing/isignthis_payouts.png)

### Sofort
Workflow name: ```SOFORT```

TxType: ```SofortDeposit```, ```WebRedirectDeposit```

Sofort Banking is a real-time online banking payment service available to customers who have a bank account in Germany, Italy, Poland, Switzerland, Austria, Belgium or the Netherlands and more countries are being added. The key benefit of Sofort Banking compared to normal credit transfer is the instant confirmation of the order sent to the merchant allowing an instant delivery of services.

#### Example Routing Rule
![](/img/providers/routing/isignthis_sofort1.png)

Note: since Emoney, Flykk and Sofort are using WebRedirectDeposit, routing is differentiated by PSP service

Also it's possible to use ```SofortDeposit``` PaymentTxType. In this case routing may look like:
![](/img/providers/routing/isignthis_sofort2.png)

#### Flow
1. Send your request to /api/webredirect/deposit/process
2. A response with redirectOutput will be sent back with a url to redirect the user to Isignthis (if routing is setup to push tx to Isingthis).
3. The user is redirect to Isignthis where they can enter a new card or use a stored card.
    1. Using a new card or no stored cards
        1. Enter the card details.
        2. Then the user can be requested to entering more info to prove that the user is who he say he/she is.
            1. The user will then upload documents and fill in forms with personal details that will be apporoved or declined.
            2. If the user does not have all information that is required then it can be aborted and can be continued with the same link that was returned from the  /api/webredirect/deposit/process call. The link can also be fetched from the transaction or from paymentiq status api for the transaction.
    2. Using a stored card
        1. The payment process continues without kyc information is requestd from the user.
4. Notifications will be sent to paymentiq with the result.
5. Deposit will be Successful when approved from Isignthis side.

## Notifications

All communication between paymentiq and Isignthis is done by notifications . 
The notification url has to be set on Isignthis side.

### URLS:
| Environment | URL                                                                   |
|-------------|-----------------------------------------------------------------------|
| Test        | https://test-api.paymentiq.io/paymentiq/api/isignthis/v1/notification |
| Live        | https://api.paymentiq.io/paymentiq/api/isignthis/v1/notification      |

###SIIN 
PaymentIQ supports incoming SIIN notifications which are instant notifications about incoming bank transfers.

Such notifications will be handled by the mentioned above endpoint and will create a new ```BankIBANDeposit``` transaction, where under ```info``` column transaction details can be found.

## Test Information

### Test accounts

Isignthis has some test cards. The outcome of the transaction can be decided by changing the cvv2 (cvc) code. 

| Card Brand | Account          | CVV       | Expiry date | 3DS Enrolled | Resets Identity |
|------------|------------------|-----------|-------------|--------------|-----------------|
| VISA       | 4000000087616647 | See below | 02/2022     | Yes          | Yes             |
| VISA       | 4000000050258021 | See below | 02/2022     | Yes          | No              |
| VISA       | 4000000011488436 | See below | 02/2022     | No           | Yes             |
| MASTERCARD | 5275877681681282 | See below | 03/2023     | Yes          | No              |

For FLYKK:

| Card Brand | Account          | CVV       | Expiry date | 3DS Enrolled | Resets Identity |
|------------|------------------|-----------|-------------|--------------|-----------------|
| MASTERCARD | 5204336336194783 | See below | 02/2022     | Yes          | Yes             |

OTP is 111-111 once OTP screen has been reached
In PIV enhanced:
If a equation is being selected, the answer is 1234.
If alternate payment method - the answer is a division 0.6 of the amount, example on €10 the answers are 6.00 and 4.00.

<b>Obs</b>: If you use a card that has Reset Identity = No and amount over 2000 EUR and using the emoney and flykk flows (webredirect) then you will have to fill in some more kyc info and upload documents etc...

For Sofort:

To use demo account please type 88888888 and select Demo bank, and proceed with any random inputs later on.


Cvv codes

| CVV From (including) | CVV To (including) | Transaction Result   |
|----------------------|--------------------|----------------------|
| 001                  | 199                | OK (Success)         |
| 200                  | 299                | Incorrect cvv        |
| 300                  | 399                | Invalid currency     |
| 400                  | 499                | Insufficient Funds   |
| 500                  | 599                | Card lost            |
| 600                  | 699                | Card Restricted      |
| 700                  | 799                | Declined (by Issuer) |
| 800                  | 899                | Suspected Fraud      |
| 900                  | 999 or above       | General Error        |