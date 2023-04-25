--- 
id: "Safecharge" 
title: "Safecharge"
hide_title: "true"
---
 
![](/img/providers/logos/safecharge.png)

# Safecharge

## About
SafeCharge is a payment provider that supports credit card payments but also a variety of alternative payment methods (APMs) as an aggregator.

| Provider Name                | SafeCharge                                                                                                                                                                                                                                                                                                                                                                              |
|------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Link                         | [https://www.safecharge.com](https://www.safecharge.com)                                                                                                                                                                                                                                                                                                                                |
| Classification               | Aggregator                                                                                                                                                                                                                                                                                                                                                                              |
| Regions                      | `International`                                                                                                                                                                                                                                                                                                                                                                         |
| Currencies                   | Please check directly with the provider regarding what currencies are supported                                                                                                                                                                                                                                                                                                         |
| Methods/PaymentTxTypes       | `CreditcardDeposit`, `CreditcardWithdrawal`, `Refund`, `Void`, `SofortDeposit`, `GiropayDeposit`, `PaysafecardDeposit`, `WebRedirectDeposit`, `Capture`, `InstadebitDeposit`, `IDebitDeposit`, `ÌdealDeposit`, `QiwiDeposit`, `EutellerDeposit`, `TrustlyDeposit`, `EpsDeposit`, `BankIBANDeposit`, `Przelewy24Deposit`, `BankIbanWithdrawal`, `BankDomesticDeposit`, `ApplePayDeposit` |
| PaymentIQ Configuration File | `SafeChargeRestConfig`                                                                                                                                                                                                                                                                                                                                                                  |

## Configuration Information

### ~~SafeChargeConfig (Old, only Creditcard)~~ SHOULD NOT BE USED 

| PaymentIQ Configuration | Description                                                                                        |
|-------------------------|----------------------------------------------------------------------------------------------------|
| merchantId              | Your merchant id (provided by SafeCharge)                                                          |
| password                | Your password (provided by SafeCharge)                                                             |
| merchantWebSIte         | Your site www address                                                                              |
| useEnrollmentPspRefId   | Set to true if enrollment psp id should be use as pspRefId or if capture should be. Default false. |
| piqVersion              | Set REST on a account to enabled the rest api. Defaults to use this config. (Only for creditcards) |

### SafeChargeRestConfig (New, Creditcard and APM)

| PaymentIQ Configuration | Description                                                                                                                                                                                                                                 |
|-------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| merchantId              | Your merchant id (provided by SafeCharge)                                                                                                                                                                                                   |
| secretKey               | Your secret key (provided by SafeCharge)                                                                                                                                                                                                    |
| siteId                  | Your site id (provided by SafeCharge)                                                                                                                                                                                                       |
| useHosted               | Used for WebRedirectDeposit. Controls whether to use SafeCharge hosted payment page or not. Defaults to true.                                                                                                                               |
| useCashier              | Used for WebRedirectDeposit. Controls whether to use SafeCharge's Cashier or not. Defaults to false.                                                                                                                                        |
| paymentMethods          | GIROPAYDEPOSIT, PAYSAFECARDDEPOSIT, SOFORTDEPOSIT, APPLEPAY, NEOSURF, ASTROPAY_TEF, ASTROPAY, SAFETYPAY, BOLETO, INTERAC_ETRANSFER, IDEBIT, INSTADEBIT, IDEAL, QIWI, WEBMONEY, YANDEX, FAST_BANK_TRANSFER, 2C2P_APMs, RAPIDTRANSFER, MYBANK |
| authType                | AUTH_CAPTURE, DIRECT_CATPURE, PRE_AUTH. Defaults DIRECT_CATPURE                                                                                                                                                                             |
| useTokenId              | Controls recurring token id should be used or not. Defaults to false                                                                                                                                                                        |
| ignorePendingCallback   | Set to true to ignore pending callbacks as they can cause issues if several callbacks comes at the same time. Defaults to false                                                                                                             |
| requestMethod           | HTTP Method used to redirect the user to Safecharge's API after initiating a deposit. Usually a GET request.                                                                                                                                |


**Please note, that you must instruct SafeCharge that your account HAS to use SHA256 and NOT MD5, as the current integration does not support MD5 hashing.**

### BELOW APPLIES ONLY IF YOU STILL ARE USING THE OLD CONFIG

### Switching between SafeChargeConfig and SafeChargeRestConfig
1. Get new credentials from SafeCharge (merchantId, siteId, secretKey).
2. Some features has to be enabled from SafeCharge side for the new credentials [see here](#features-that-will-have-to-be-enabled-from-safecharge-side)
3. Setup a SafeChargeRestConfig and a new account with the new information.
4. On the account that you want to route to the new config set the account attribute ```<piqVersion>REST</piqVersion>``` in SafeChargeConfig. See example below
5. The account name in SafeChargeConfig must match the on in SafeChargeRestConfig.
6. Do the same for all accounts that should use SafeChargeRestConfig.
7. Now you are ready to route traffic with SafeChargeRestConfig.

<details>
<summary>Click to view example SafeChargeConfig</summary>
<br/>

```xml
    <com.devcode.paymentiq.integration.safecharge.SafeChargeConfig>
        ....
        <accounts>
            <entry>
            <string>3DS</string>
            <account>
                ....
                <use3Dsecure>true</use3Dsecure>
                <version>4.0.2</version>
                <piqVersion>REST</piqVersion>
                ....
            </account>
            </entry>
            ....
        </accounts>
        ....
    <com.devcode.paymentiq.integration.safecharge.SafeChargeConfig>
```
</details>

### 3DS2

To be able to use the ```3DS2``` we will have to configure
```xml
<acquirerMerchantId>${ptx.txAmount.currencyCode;map(AUD->11111111,EUR->22222222,SEK->33333333)}</acquirerMerchantId>
<mcc>7995</mcc>
<merchantCountry>SWE</merchantCountry>
<merchantUrl>http://www.example.com</merchantUrl>
<merchantName>Test merchant</merchantName>
```

on each provider account in the SafeChargeConfig/SafeChargeRestConfig.

#### Features that will have to be enabled from SafeCharge side

1. N3DS. If you want to process N3DS deposit this has to be enabled by SafeCharge (Managed3D is the feature called)
2. Withdrawals. If you want to process withdrawals you will have to enable it (payout)
3. By default SafeCharge are using Sale txs. No capture is needed after successful authorization. But
SafeCharge can enable auth / capture mode for you.
4. When Auth / capture mode is enabled at SafeCharge its possible to configure PaymentIQ to do a direct capture after auth or you can do the capture manually from Payment IQ backoffice. By setting the account attribute ```<authType>PRE_AUTH</authType>```will enable the capture later mode. This is done for each account in the SafeChargeRestConfig.
5. Enable recurring or rebilling and then use a account that has ```useTokenId``` set to ```true```.

### SafeCharge APM Deposits
The alternative payment methods support is `Sofort, Giropay, PaysafeCard, Neosurf, Astropay TEF, Astropay, Safetypay, Interac, IDebit, Instadebit, Qiwi, iDEAL and more`. They can be processed using PaymentTxType according to the table below. Some APMs require nationalId as input, if that's the case WebRedirectDeposit cannot be used.

| APM                    | TxType                          | Service                |
|------------------------|---------------------------------|------------------------|
| Sofort                 | SofortDeposit                   | -                      |
| Giropay                | GiropayDeposit                  | -                      |
| PaysafeCard            | PaysafecardDeposit              | -                      |
| Neosurf                | WebRedirectDeposit              | NEOSURF                |
| Astropay TEF           | BankDeposit, WebRedirectDeposit | ASTROPAY_TEF           |
| Astropay               | BankDeposit, WebRedirectDeposit | ASTROPAY               |
| Safetypay              | WebRedirectDeposit              | SAFETYPAY              |
| Boleto                 | BoletoDeposit, BankDeposit      | BOLETO                 |
| ApplePay               | WebRedirectDeposit              | APPLEPAY               |
| Interac                | BankDeposit                     | INTERAC_ETRANSFER      |
| IDebit                 | IDebitDeposit                   | -                      |
| Instadebit             | InstadebitDeposit               | -                      |
| iDEAL                  | IdealDeposit                    | -                      |
| Qiwi                   | QiwiDeposit                     | -                      |
| Webmoney               | WebRedirectDeposit              | WEBMONEY               |
| Yandex Money           | WebRedirectDeposit              | YANDEX                 |
| Fast Bank Transfer     | BankDeposit, WebRedirectDeposit | FAST_BANK_TRANSFER     |
| 2C2P Payments          | WebRedirectDeposit              | 2C2P_APMs              |
| RapidTransfer          | BankDeposit, WebRedirectDeposit | RAPIDTRANSFER          |
| MyBank                 | BankDeposit                     | MYBANK                 |
| Euteller               | EutellerDeposit                 | -                      |
| Trustly                | Trustly                         | -                      |
| PayRetailers           | WebRedirectDeposit              | PAYRETAILERS           |
| Poli                   | WebRedirectDeposit              | POLI                   |
| P24                    | Przelewy24Deposit               | -                      |
| Open Banking           | BankDeposit                     | OPEN_BANKING           |
| Elementpay (EPS)       | EpsDeposit                      | -                      |
| Multibanco             | WebRedirectDeposit              | MULTIBANCO             |
| SEPA                   | BankIBANDeposit                 | SEPA                   |
| ELO                    | BankDeposit                     | ELO                    |
| PIX                    | BankDeposit                     | PIX                    |
| HIPERCARD              | BankDeposit                     | HIPERCARD              |
| SUGARPAY               | WebRedirectDeposit              | SUGARPAY               |
| PayRetailers_CC        | BankDeposit                     | PAYRETAILERSCC         |
| DragonPay              | WebRedirectDeposit              | DRAGONPAY              |
| MBWAY                  | WebRedirectDeposit              | MBWAY                  |
| PAYWITHCRYPTO          | WebRedirectDeposit              | PAYWITHCRYPTO          |
| FREECHARGE             | WebRedirectDeposit              | FREECHARGE             |
| JIOMONEY               | WebRedirectDeposit              | JIOMONEY               |
| NETBANKINGTW           | WebRedirectDeposit              | NETBANKINGTW           |
| PHONEPE                | WebRedirectDeposit              | PHONEPE                |
| OlaMoney               | WebRedirectDeposit              | OLAMONEY               |
| Bank Transfer Malaysia | BankDeposit                     | BANK_TRANSFER_MALAYSIA |
| Finnish Bank           | BankDomesticDeposit             | FINNISH_BANK           |

#### SafeCharge Hosted Payment Page
The hosted payment page solution redirects the end user to SafeCharge’s own payment page. This is used through the tx type WebRedirectDeposit and according to the Front API documentation.

![](/img/providers/safecharge01.png)

#### SafeCharge Cashier
The SafeCharge Cashier solution redirects the end user to SafeCharge’s cashier page. This is used through the tx type WebRedirectDeposit and according to the Front API documentation. This works similar to how SafeCharge Hosted Payment Page does.

#### SafeCharge Apple Pay deposits
Apple Pay deposits can be used through SafeCharge’s Hosted Payment Page solution. The same WebRedirectDeposit is used but to only display the Apple Pay payment option on the payment page, the parameter “service” should be set to “APPLEPAY”. See example below. There is some setup with SafeCharge that needs to be done to process Apple Pay payments. This includes creating a payment processing certificate at Apple Pay and uploading it to SafeCharge. From here, depending on whether the intention is to use the hosted payment page in an iFrame or window, the setup is a little different. For iFrame, it is also needed to create an identity certificate and upload to SafeCharge in addition to adding some JS that SafeCharge provides to the website. Details can be found in SafeCharge’s API documentation: [https://www.safecharge.com/docs/API/#ApplePayCertificates](https://www.safecharge.com/docs/API/#ApplePayCertificates).

![](/img/providers/safecharge02.png)

## Example Routing Rule
### APM routing
Route each APM by setting a condition on the PaymentTxType. See example below.

![](/img/providers/routing/safecharge.png)

### Creditcard routing
Example of test routing. All tx with a min amount of 10 EUR will be 3DS. All with a max amount of 10 EUR is N3DS.

![](/img/providers/routing/safechargeccrules.png)

### 3DS2
For 3DS2 authorizations to work correctly, you need to add a 3DS2 routing rule. 
     
![](/img/providers/safecharge3ds2.png)
     
Our recommended 3DS2 routing setup can be found here: [3DS2 Provider Routing](/../docs/configuration_and_administration/system_configuration/3ds2mpi)
     
### Safecharge MPI config
MPI checks whether the credit card is enrolled for 3DS and verifies the cardholder with the issuing bank providing a better success ratio for online transactions.
With MPI authorization 3DS 2 will be separated and can be done independent of acquirer/PSP
As PaymentIQ Team don't have our own credentials, configuration file should be added by merchant on the level of the merchant.

See example below.
     
SafeCharge3DServerConfig should be created.
<details>
<summary>Click to view example SafeCharge3DServerConfig</summary>
<br/>

```xml
    <com.devcode.paymentiq.integration.safecharge.SafeCharge3DServerConfig>
        <accounts>
            <entry>
             <string>default</string>
             <account>
              <supportedThreeDSVersion>1.0.0-2.2.0</supportedThreeDSVersion>
              <mcc>???</mcc>
              <merchantName>???</merchantName>
              <merchantUrl>???</merchantUrl>
              <acquirerMerchantId>???</acquirerMerchantId>
              <merchantCountry>???</merchantCountry>
              <merchantId>????</merchantId> <!-- Merchant ID provided by SafeCharge -->
              <siteId>???</siteId> <!-- Merchant Site ID provided by SafeCharge -->
              <secretKey>????</secretKey> <!-- Merchant Secret Key provided by SafeCharge -->
             </account>
            </entry>
        </accounts>
    <com.devcode.paymentiq.integration.safecharge.SafeCharge3DServerConfig>
```
</details>


## Test Information
Different test credentials are needed for each APM. The values below are taken from SafeCharge’s official documentation so they might be changed over time. For an updated list it’s probably a good idea to visit their documentation page at [docs.safecharge.com/documentation/guides/testing/](https://docs.safecharge.com/documentation/guides/testing/)

| Payment Method Name | User/Account        | Password           |
|---------------------|---------------------|--------------------|
| PaySafeCard         | 0000 0000 0990 3207 | N/A                |
| Sofort              | 12345678            | PIN 123, TAN 12345 |
| Finnish Bank        | ABNANL2A            | N/A                |

### Credit Cards (Using SafeChargeConfig)

#### Deposit
- For 3DS, use amounts from 110 and above.

| Card Brand | Account          | CVV | Expiry date | Result/Info                              |
|------------|------------------|-----|-------------|------------------------------------------|
| VISA       | 4012001037141112 | Any | Any         | Valid 3-D Secure Message                 |
| VISA       | 4012001036275556 | Any | Any         | No Response From Visa   Directory Server |
| VISA       | 4012001038443335 | Any | Any         | Cardholder Not   Participating           |
| VISA       | 4012001038488884 | Any | Any         | Unable to Verify Enrollment              |
| VISA       | 4012001036298889 | Any | Any         | Invalid Response from   Directory Server |
| VISA       | 4012001036853337 | Any | Any         | PaRes failed validation                  |
| VISA       | 4012001037167778 | Any | Any         | Successful Merchant Attempt              |
| VISA       | 4012001037461114 | Any | Any         | Authentication Failure                   |
| VISA       | 4012001037484447 | Any | Any         | Authentication Not   Available           |
| VISA       | 4012001037490006 | Any | Any         | Invalid PaRes                            |
| VISA       | 4012001037490014 | Any | Any         | Valid 3-D Secure Message                 |

#### Withdrawals

| Card Brand | Account          | CVV | Expiry date |
|------------|------------------|-----|-------------|
| VISA       | 4001886063621166 | Any | Any         |
| VISA       | 4002629798205148 | Any | Any         |
| VISA       | 4026201382933139 | Any | Any         |
| VISA       | 4000791844858684 | Any | Any         |

### Creditcard (Using SafeChargeRestConfig)

#### Deposit
- For 3DS, use amounts from 10 and above.

### 3DS1
Same testcards as [old API](#credit-cards-using-safechargeconfig) using SafeChargeConfig.

### 3DS2
See [Testing 3DS 2](https://docs.paymentiq.io/europe/3ds2/testing/testing3ds2staging)


### N3DS
- For N3DS, use amounts below 10.

Same testcards as [old API](#credit-cards-using-safechargeconfig) using SafeChargeConfig.

#### Withdrawal

| Card Brand | Account          | CVV | Expiry date |
|------------|------------------|-----|-------------|
| VISA       | 4002629798205148 | Any | Any         |
| MASTERCARD | 5100961728665671 | Any | Any         |

#### Withdrawal - IBan
- Test IBAN used for withdrawals: DE75380500000108605346
