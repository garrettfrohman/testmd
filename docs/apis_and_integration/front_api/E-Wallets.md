---
id: "E-Wallets"
---

# E-Wallets

The below listed e-wallet providers all have some additional parameter that needs to be included in the request for the transaction to be successful.

If the e-wallet provider you are adding is not listed, it means only the standard parameters are required.

## ApplePay

### ApplePayDeposit

`POST /api/applepay/deposit/process`

| Name  | Located in   | Description                                                                                                                                                                         | Data Type | Required | Example |
|-------|--------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------|----------|---------|
| token | Request Body | If the Apple Pay token is created by merchant it should be sent. If not included PIQ will respond with a redirect URL that the user should redirect to which will create the token. | string    | true     |         |

### ApplePayWithdrawal

`POST /api/applepay/withdrawal/process`

## Aircash

### AircashWalletWithdrawal

`POST /api/aircashwallet/withdrawal/process`

| Name        | Located in   | Description                                      | Data Type | Required | Example     |
|-------------|--------------|--------------------------------------------------|-----------|----------|-------------|
| phoneNumber | Request Body | The phoneNumber that the wallet is connected to! | string    | true     | +4512345678 |

## EPaybg

### EPaybgWithdrawal

`POST /api/epaybg/withdrawal/process`

| Name  | Located in   | Description                                                       | Data Type | Required | Example              |
|-------|--------------|-------------------------------------------------------------------|-----------|----------|----------------------|
| email | Request Body | User's EPaybg email account. Either this or accountId is required | string    | false    | jane.doe@example.com |
| cin   | Request Body | Customer identification number (CIN)                              | string    | false    | 1234567890           |

## MobilePay (BamboraGa)

### MobilePayDeposit

`POST /api/mobilepay/deposit/process`

| Name        | Located in   | Description                                                 | Data Type | Required | Example     |
|-------------|--------------|-------------------------------------------------------------|-----------|----------|-------------|
| phoneNumber | Request Body | Will pre-populate phone number in MobilePay's redirect page | string    | false    | +4512345678 |

## MobilePaySubscription

### MobilePaySubscriptionDeposit

`POST /api/mobilepaysubscription/deposit/process`

No provider specific params required - [To general request parameters](request)

## EcoBanq

### EcoBanqDeposit

`POST /api/ecobanq/deposit/process`

| Name            | Located in   | Description                  | Data Type | Required | Example         |
|-----------------|--------------|------------------------------|-----------|----------|-----------------|
| ecoBanqUserId   | Request Body | ECOBANQ user ID.             | string    | true     | Q001796         |
| ecoBanqPassword | Request Body | ECOBANQ user login password. | string    | true     | TestPassword123 |

### EcoBanqWithdrawal

`POST /api/ecobanq/withdrawal/process`

| Name          | Located in   | Description      | Data Type | Required | Example |
|---------------|--------------|------------------|-----------|----------|---------|
| ecoBanqUserId | Request Body | ECOBANQ user ID. | string    | true     | Q001796 |

## EcoPayz

### EcoPayzDeposit

`POST /api/ecopayz/deposit/process`

| Name    | Located in   | Description                          | Data Type | Required | Example |
|---------|--------------|--------------------------------------|-----------|----------|---------|
| service | Request Body | Send value VOUCHER to use ecoVoucher | string    | false    | VOUCHER |

### EcoPayzWithdrawal

`POST /api/ecopayz/withdrawal/process`

| Name          | Located in   | Description                                                                   | Data Type | Required | Example                              |
|---------------|--------------|-------------------------------------------------------------------------------|-----------|----------|--------------------------------------|
| accountNumber | Request Body | User's Ecpopayz account number. Either this or accountId is required.         | string    | true     | 1100319509                           |
| accountId     | Request Body | Account-id representing an EcoPayz account used in a previous deposit by user | string    | true     | d751d5e0-ebf6-44a2-84c4-e437a55b2cfc |

## Ozan

### WebRedirectDeposit

`POST /api/webredirect/deposit/process`

No provider specific params required - [To general request parameters](request)

### OzanWithdrawal

`POST /api/ozan/withdrawal/process`

| Name        | Located in   | Description                                      | Data Type | Required | Example    |
|-------------|--------------|--------------------------------------------------|-----------|----------|------------|
| phoneNumber | Request Body | User's phone number connected to the Ozan wallet | string    | true     | 0701231212 |

## Mifinity

### MiFinityEWalletDeposit

`POST /api/mifinity/deposit/process`

No provider specific params required - [To general request parameters](request)

### MiFinityEWalletWithdrawal

`POST /api/mifinity/withdrawal/process`

| Name               | Located in   | Description                                                                                                  | Data Type | Required | Example                                 |
|--------------------|--------------|--------------------------------------------------------------------------------------------------------------|-----------|----------|-----------------------------------------|
| destinationAccount | Request Body | User's destination account connected to the Mifinity wallet, can be both “Email” or “eWallet Account Number” | string    | true     | 5001000001033008 or john.doe@sample.com |

## Skrill

### SkrillDeposit

`POST /api/skrill/deposit/process`

| Name      | Located in   | Description                                                                 | Data Type | Required | Example                              |
|-----------|--------------|-----------------------------------------------------------------------------|-----------|----------|--------------------------------------|
| email     | Request Body | User's Skrill email account. Either this or accountId is required           | string    | true     | jane.doe@example.com                 |
| accountId | Request Body | Account-id representing a Skrill account used in a previous deposit by user | string    | true     | d751d5e0-ebf6-44a2-84c4-e437a55b2cfc |

### SkrillQCODeposit

`POST /api/skrillqco/deposit/process`

| Name     | Located in   | Description                                                                        | Data Type | Required | Example              |
|----------|--------------|------------------------------------------------------------------------------------|-----------|----------|----------------------|
| email    | Request Body | User's Skrill email account. Mandatory when using then SKRILLDIGITALWALLET service | string    | false    | jane.doe@example.com |
| service  | Request Body | Id of the Bank/Service                                                             | string    | true     | RAPIDTRANSFER        |
| account  | Request Body | The user's Neteller account when using the NETELLER service                        | string    | false    | 451823760529         |
| secureId | Request Body | The user's Neteller secure id when using the NETELLER service                      | string    | false    | 521652               |

### SkrillWithdrawal

`POST /api/skrill/withdrawal/process`

| Name      | Located in   | Description                                                                                                   | Data Type | Required | Example                              |
|-----------|--------------|---------------------------------------------------------------------------------------------------------------|-----------|----------|--------------------------------------|
| email     | Request Body | User's Skrill email account. Either this or accountId is required.                                            | string    | true     | jane.doe@example.com                 |
| accountId | Request Body | Account-id representing a Skrill account used in a previous deposit by user. Either this or email is required | string    | true     | d751d5e0-ebf6-44a2-84c4-e437a55b2cfc |

### SkrillQCOWithdrawal

`POST /api/skrillqco/withdrawal/process`

| Name      | Located in   | Description                                                                                 | Data Type | Required | Example                              |
|-----------|--------------|---------------------------------------------------------------------------------------------|-----------|----------|--------------------------------------|
| service   | Request Body | Id of the Bank/Service                                                                      | string    | true     | RAPIDTRANSFER                        |
| accountId | Request Body | Account-id representing a Skrill quick checkout account used in a previous deposit by user. | string    | true     | d751d5e0-ebf6-44a2-84c4-e437a55b2cfc |

## Sticpay

### WebRedirectDeposit

`POST /api/webredirect/deposit/process`

No provider specific params required - [To general request parameters](request)

### SticpayWithdrawal

`POST /api/sticpay/withdrawal/process`

| Name  | Located in   | Description                            | Data Type | Required | Example          |
|-------|--------------|----------------------------------------|-----------|----------|------------------|
| email | Request Body | Email connected to the Sticpay account | string    | true     | test@sticpay.com |

## TolaMobile

### TolaMobileDeposit

`POST /api/tolamobile/deposit/process`

| Name        | Located in   | Description          | Data Type | Required | Example      |
|-------------|--------------|----------------------|-----------|----------|--------------|
| phoneNumber | Request Body | User's phone number. | string    | true     | 233000000001 |

### TolaMobileWithdrawal

`POST /api/tolamobile/withdrawal/process`

| Name        | Located in   | Description          | Data Type | Required | Example      |
|-------------|--------------|----------------------|-----------|----------|--------------|
| phoneNumber | Request Body | User's phone number. | string    | true     | 233000000001 |

## Paybox

### PayboxDeposit

`POST /api/paybox/deposit/process`

| Name      | Located in   | Description                                                                 | Data Type | Required | Example                              |
|-----------|--------------|-----------------------------------------------------------------------------|-----------|----------|--------------------------------------|
| account   | Request Body | User's Paybox account number. Either this or accountId is required          | string    | true     |                                      |
| accountId | Request Body | Account-id representing a Paybox account used in a previous deposit by user | string    | true     | d751d5e0-ebf6-44a2-84c4-e437a55b2cfc |

## Inovapay

### InovapayWalletDeposit

`POST /api/inovapaywallet/deposit/process`

| Name         | Located in   | Description                  | Data Type | Required | Example |
|--------------|--------------|------------------------------|-----------|----------|---------|
| userLogin    | Request Body | User's ID on Inovapay        | string    | true     |         |
| userSecureId | Request Body | User's Secure ID on Inovapay | string    | true     |         |

### InovapayWalletWithdrawal

`POST /api/inovapaywallet/withdrawal/process`

| Name         | Located in   | Description                                                           | Data Type | Required | Example |
|--------------|--------------|-----------------------------------------------------------------------|-----------|----------|---------|
| userLogin    | Request Body | User's ID on Inovapay                                                 | string    | true     |         |
| userSecureId | Request Body | User's Secure ID on Inovapay (Only required for withdrawals via Apco) | string    | false    |         |

## VCreditos

### VCreditosWalletDeposit

`POST /api/vcreditos/deposit/process`

| Name         | Located in   | Description                | Data Type | Required | Example |
|--------------|--------------|----------------------------|-----------|----------|---------|
| endUserId    | Request Body | VCreditos user identifier  | string    | true     | 613739  |
| userSecureId | Request Body | Generated PIN on VCreditos | string    | true     | 365528  |

### VCreditosWalletWithdrawal

`POST /api/vcreditos/withdrawal/process`

| Name      | Located in   | Description               | Data Type | Required | Example |
|-----------|--------------|---------------------------|-----------|----------|---------|
| endUserId | Request Body | VCreditos user identifier | string    | true     | 613739  |

## Pay4Fun

### WebRedirectDeposit

`POST /api/webredirect/deposit/process`

No provider specific params required - [To general request parameters](request)

### Pay4FunDeposit

`POST /api/pay4fun/deposit/process`

| Name  | Located in   | Description | Data Type | Required | Example               |
|-------|--------------|-------------|-----------|----------|-----------------------|
| email | Request Body | User email  | string    | false    | test_customer@p4f.com |

### Pay4FunWithdrawal

`POST /api/pay4fun/withdrawal/process`

| Name  | Located in   | Description | Data Type | Required | Example               |
|-------|--------------|-------------|-----------|----------|-----------------------|
| email | Request Body | User email  | string    | true     | test_customer@p4f.com |

## PayPal

### PayPalDeposit

`POST /api/paypal/deposit/process`

| Name      | Located in   | Description                                                                 | Data Type | Required | Example                              |
|-----------|--------------|-----------------------------------------------------------------------------|-----------|----------|--------------------------------------|
| email     | Request Body | User's PayPal email account. Either this or accountId is required           | string    | true     | jane.doe@example.com                 |
| accountId | Request Body | Account-id representing a PayPal account used in a previous deposit by user | string    | true     | d751d5e0-ebf6-44a2-84c4-e437a55b2cfc |

### PayPalWithdrawal

`POST /api/paypal/withdrawal/process`

| Name      | Located in   | Description                                                                                                    | Data Type | Required | Example                              |
|-----------|--------------|----------------------------------------------------------------------------------------------------------------|-----------|----------|--------------------------------------|
| accountId | Request Body | Account-id representing a PayPal account used in a previous deposit by user.                                   | string    | true     | d751d5e0-ebf6-44a2-84c4-e437a55b2cfc |
| email     | Request Body | User's PayPal email account. Required if allowing withdrawals before deposits and there is no saved accountId. | string    | false    | jane.doe@example.com                 |

## Mbankomat

### MbankomatDeposit

`POST /api/mbankomat/deposit/process`

| Name        | Located in   | Description                                                                                                                      | Data Type | Required | Example                                        |
|-------------|--------------|----------------------------------------------------------------------------------------------------------------------------------|-----------|----------|------------------------------------------------|
| phoneNumber | Request Body | User's phone number. Either this or accountId is required.                                                                       | string    | true     | +420603123456                                  |
| operator    | Request Body |  Mobile operator according to Mbankomat's specification. Either this or accountId is required.                                   | string    | true     | “1” for T-Mobile, “2” for O2, “3” for Vodafone |
| accountId   | Request Body | Account-id representing a Mbankomat account used in a previous deposit by user. Either this or phoneNumber/operator is required. | string    | true     | d751d5e0-ebf6-44a2-84c4-e437a55b2cfc           |

## Neteller

### NetellerDeposit

`POST /api/neteller/deposit/process`

| Name      | Located in   | Description                                                                                                                                                              | Data Type | Required | Example                              |
|-----------|--------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------|----------|--------------------------------------|
| account   | Request Body | User's email address that is associated with the Neteller account (or Neteller account number if using old API until 15 May 2020). Either this or accountId is required. | string    | true     | netellertest_EUR@neteller.com        |
| secureId  | Request Body | Not required after migration to new API after 15 May 2020.                                                                                                               | string    | false    | 908379                               |
| accountId | Request Body | Account-id representing a Neteller account used in a previous deposit by user. Either this or account/secureId is required.                                              | string    | false    | d751d5e0-ebf6-44a2-84c4-e437a55b2cfc |

### NetellerWithdrawal

`POST /api/neteller/withdrawal/process`

| Name      | Located in   | Description                                                                                                                                                              | Data Type | Required | Example                              |
|-----------|--------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------|----------|--------------------------------------|
| account   | Request Body | User's email address that is associated with the Neteller account (or Neteller account number if using old API until 15 May 2020). Either this or accountId is required. | string    | true     | netellertest_EUR@neteller.com        |
| accountId | Request Body | Account-id representing a Neteller account used in a previous deposit by user                                                                                            | string    | false    | d751d5e0-ebf6-44a2-84c4-e437a55b2cfc |

## Siru

### SiruDeposit

`POST /api/siru/deposit/process`

| Name        | Located in   | Description                                                                                              | Data Type | Required | Example                              |
|-------------|--------------|----------------------------------------------------------------------------------------------------------|-----------|----------|--------------------------------------|
| phoneNumber | Request Body | User's phone number. Either this or accountId is required.                                               | string    | true     | +420603123456                        |
| accountId   | Request Body | Representing a Siru account used in a previous deposit by user. Either this or phoneNumber is required.  | string    | true     | d751d5e0-ebf6-44a2-84c4-e437a55b2cfc |

## LavaPay

### LavaPayDeposit

`POST /api/lavapay/deposit/process`

| Name    | Located in   | Description                                                                                             | Data Type | Required | Example                                                                                           |
|---------|--------------|---------------------------------------------------------------------------------------------------------|-----------|----------|---------------------------------------------------------------------------------------------------|
| email   | Request Body | User's email address that is associated with the LavaPay account. Either this or accountId is required. | string    | true     | jane.doe@example.com                                                                              |
| service | Request Body | Service that represents which payment method to use                                                     | string    | true     | Available values: LAVAW, OKPAY, PERFM, QIWIV, BITCN, WALON_W1OK, LITCN, PAXUM, ECOIN, YAMP, YADMO |

### LavaPayWithdrawal

`POST /api/lavapay/withdrawal/process`

No provider specific params required - [To general request parameters](request)

## VenusPoint

### VenusPointDeposit

`POST /api/venuspoint/deposit/process`

| Name      | Located in   | Description                                                                                                         | Data Type | Required | Example                              |
|-----------|--------------|---------------------------------------------------------------------------------------------------------------------|-----------|----------|--------------------------------------|
| username  | Request Body | The users's Venus Point username. Either this or accountId is required.                                             | string    | true     | Q113395                              |
| password  | Request Body | The user's Venus Point password. Either this or accountId is required.                                              | string    | true     |                                      |
| accountId | Request Body | Representing a VenusPoint account used in a previous deposit by user. Either this or username/password is required. | string    | true     | d751d5e0-ebf6-44a2-84c4-e437a55b2cfc |

### VenusPointWithdrawal

`POST /api/venuspoint/withdrawal/process`

| Name      | Located in   | Description                                                                                                | Data Type | Required | Example                              |
|-----------|--------------|------------------------------------------------------------------------------------------------------------|-----------|----------|--------------------------------------|
| username  | Request Body | The users's Venus Point username. Either this or accountId is required.                                    | string    | true     | Q113395                              |
| password  | Request Body | The user's Venus Point password.                                                                           | string    | true     |                                      |
| accountId | Request Body | Representing a VenusPoint account used in a previous deposit by user. Either this or username is required. | string    | false    | d751d5e0-ebf6-44a2-84c4-e437a55b2cfc |

## IWallet

### IWalletDeposit

`POST /api/iwallet/deposit/process`

No provider specific params required - [To general request parameters](request)

### IWalletWithdrawal

`POST /api/iwallet/withdrawal/process`

| Name               | Located in   | Description                    | Data Type | Required | Example  |
|--------------------|--------------|--------------------------------|-----------|----------|----------|
| destinationAccount | Request Body | IWallet client account number. | string    | true     | 60148766 |

## MuchBetter

### MuchBetterDeposit

`POST /api/muchbetter/deposit/process`

| Name        | Located in   | Description         | Data Type | Required | Example      |
|-------------|--------------|---------------------|-----------|----------|--------------|
| phoneNumber | Request Body | User's phone number | string    | true     | 447625485770 |

### MuchBetterWithdrawal

`POST /api/muchbetter/withdrawal/process`

| Name        | Located in   | Description         | Data Type | Required | Example      |
|-------------|--------------|---------------------|-----------|----------|--------------|
| phoneNumber | Request Body | User's phone number | string    | true     | 447625485770 |

## Spark

### WebRedirectDeposit

`POST /api/webredirect/deposit/process`

No provider specific params required - [To general request parameters](request)

### SparkWithdrawal

`POST /api/spark/withdrawal/process`

| Name           | Located in   | Description            | Data Type | Required | Example    |
|----------------|--------------|------------------------|-----------|----------|------------|
| customerNumber | Request Body | User's customer number | string    | true     | 4123412341 |
| province       | Request Body | User's province        | string    | true     | KA         |

## PremierPay

### PremierPayWalletDeposit

`POST /api/premierpaywallet/deposit/process`

| Name    | Located in   | Description                                             | Data Type | Required | Example                             |
|---------|--------------|---------------------------------------------------------|-----------|----------|-------------------------------------|
| service | Request Body | Specific service to control which payment method to use | string    | true     | INTERAC_ONLINE or INTERAC_ETRANSFER |

### PremierPayWalletWithdrawal

`POST /api/premierpaywallet/withdrawal/process`

| Name    | Located in   | Description                                             | Data Type | Required | Example           |
|---------|--------------|---------------------------------------------------------|-----------|----------|-------------------|
| service | Request Body | Specific service to control which payment method to use | string    | true     | INTERAC_ETRANSFER |

## PremierPay

### PremierPayDirectDeposit

`POST /api/premierpaydirect/deposit/process`

| Name                       | Located in   | Description                                             | Data Type | Required | Example                        |
|----------------------------|--------------|---------------------------------------------------------|-----------|----------|--------------------------------|
| service                    | Request Body | Specific service to control which payment method to use | string    | true     | DIRECTDEBIT or DIRECTDEBITPLUS |
| accountHolder              | Request Body | Bank account holder name                                | string    | true     | John Doe                       |
| accountNumber              | Request Body | Bank account number (7 digits)                          | string    | true     | 1234567                        |
| financialInstitutionNumber | Request Body | Bank account institute number (3 digits)                | string    | true     | 123                            |
| transitNumber              | Request Body | Bank account transit number (5 digits)                  | string    | true     | 12345                          |

### PremierPayDirectWithdrawal

`POST /api/premierpaydirect/withdrawal/process`

| Name                       | Located in   | Description                                             | Data Type | Required | Example      |
|----------------------------|--------------|---------------------------------------------------------|-----------|----------|--------------|
| service                    | Request Body | Specific service to control which payment method to use | string    | true     | DIRECTCREDIT |
| accountHolder              | Request Body | Bank account holder name                                | string    | true     | John Doe     |
| accountNumber              | Request Body | Bank account number (7 digits)                          | string    | true     | 1234567      |
| financialInstitutionNumber | Request Body | Bank account institute number (3 digits)                | string    | true     | 123          |
| transitNumber              | Request Body | Bank account transit number (5 digits)                  | string    | true     | 12345        |

## Yapeal

### BankIBANDeposit

`POST /api/bankiban/deposit/process`

| Name | Located in   | Description | Data Type | Required | Example          |
|------|--------------|-------------|-----------|----------|------------------|
| iban | Request Body | IBAN        | string    | true     | CH12345678900001 |

### BankIBANWithdrawal

`POST /api/bankiban/withdrawal/process`

| Name | Located in   | Description | Data Type | Required | Example          |
|------|--------------|-------------|-----------|----------|------------------|
| iban | Request Body | IBAN        | string    | true     | CH12345678900001 |

## Wallet88

### Wallet88Deposit

`POST /api/wallet88/deposit/process`

| Name         | Located in   | Description                                                                                                           | Data Type | Required | Example                              |
|--------------|--------------|-----------------------------------------------------------------------------------------------------------------------|-----------|----------|--------------------------------------|
| username     | Request Body | Username or email address that is associated with this Wallet88 account. Either this or accountId is required.        | string    | true     | jane.doe@example.com                 |
| securityCode | Request Body | The user's Wallet88 password. Either this or accountId is required.                                                   | string    | true     | 238732                               |
| accountId    | Request Body | Representing a Wallet88 account used in a previous deposit by user. Either this or username/securityCode is required. | string    | true     | d751d5e0-ebf6-44a2-84c4-e437a55b2cfc |

### Wallet88Withdrawal

`POST /api/wallet88/withdrawal/process`

| Name         | Located in   | Description                                                                                                           | Data Type | Required | Example                              |
|--------------|--------------|-----------------------------------------------------------------------------------------------------------------------|-----------|----------|--------------------------------------|
| username     | Request Body | Username or email address that is associated with this Wallet88 account. Either this or accountId is required.        | string    | true     | jane.doe@example.com                 |
| securityCode | Request Body | The user's Wallet88 password. Either this or accountId is required.                                                   | string    | true     | 238732                               |
| accountId    | Request Body | Representing a Wallet88 account used in a previous deposit by user. Either this or username/securityCode is required. | string    | true     | d751d5e0-ebf6-44a2-84c4-e437a55b2cfc |

## UPayCard

### UPayCardDeposit

`POST /api/upaycard/deposit/process`

| Name          | Located in   | Description                                                                                                                                                                              | Data Type | Required | Example |
|---------------|--------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------|----------|---------|
| accountNumber | Request Body | Username, user email, or account number associated with the account. If the user has not requested a currency account or have several accounts then the input must be an account number. | string    | true     | 1786050 |

### UPayCardWithdrawal

`POST /api/upaycard/withdrawal/process`

| Name          | Located in   | Description                                                          | Data Type | Required | Example |
|---------------|--------------|----------------------------------------------------------------------|-----------|----------|---------|
| accountNumber | Request Body | Username, user email, or account number associated with the account. | string    | true     | 1786050 |

## Interswitch

### WebPayDeposit

`POST /api/interswitch/deposit/process`

No provider specific params required - [To general request parameters](request)

## Globepay

### GlobepayDeposit

`POST /api/globepay/deposit/process`

No provider specific params required - [To general request parameters](request)

### GlobepayWithdrawal

`POST /api/globepay/withdrawal/process`

| Name  | Located in   | Description                      | Data Type | Required | Example              |
|-------|--------------|----------------------------------|-----------|----------|----------------------|
| email | Request Body | User's Globepay's email account. | string    | true     | jane.doe@example.com |

## Jeton

### JetonDeposit

`POST /api/jeton/deposit/process`

| Name           | Located in   | Description                                                                                                   | Data Type | Required | Example                              |
|----------------|--------------|---------------------------------------------------------------------------------------------------------------|-----------|----------|--------------------------------------|
| customerNumber | Request Body | User's Jeton customer number. Required for direct payment.                                                    | string    | false    | 53920725                             |
| service        | Request Body | Optional id of the payment method. If not provided will default to the configured service in accounts config. | string    | false    | Possible values: CHECKOUT, JETGO, QR |

### JetonWithdrawal

`POST /api/jeton/withdrawal/process`

| Name           | Located in   | Description                                                                                                                           | Data Type | Required | Example                |
|----------------|--------------|---------------------------------------------------------------------------------------------------------------------------------------|-----------|----------|------------------------|
| customerNumber | Request Body | User's Jeton customer number.                                                                                                         | string    | true     | 53920725               |
| service        | Request Body | Optional id of the withdrawal type. If not provided, and service is not configured in accounts config, will default to Wallet payout. | string    | false    | Possible values: JETGO |

## Ilixium

### WebRedirectDeposit

`POST /api/ilixium/deposit/process`

No provider specific params required - [To general request parameters](request)

## ECommPay

### ECommPayWalletDeposit

`POST /api/ecommpay/deposit/process`

| Name          | Located in   | Description                                                                                                                                                     | Data Type | Required | Example                                                                                                                                                                                                                    |
|---------------|--------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------|----------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| accountNumber | Request Body | User's wallet number. Required for QIWI and optional for YANDEX. Should not be used for other methods.                                                          | string    | false    | 510019885431963                                                                                                                                                                                                            |
| service       | Request Body | Optional id of the payment method. If not provided will default to the configured service in accounts config.                                                   | string    | false    | Possible values: YANDEX, QIWI, WEBMONEY, WEBMONEY_LIGHT, PAPARA, BANKS_OF_PHILIPPINES, PHILIPPINES_PAYMENT_CENTERS, PHILIPPINES_OTC_ATM, COINS_PH, GCASH, GRABPAY, BANKS_OF_INDONESIA_VA, THAILAND_QR_BANKING, MOMO_WALLET |
| bankCode      | Request Body | User's bank. Required for BANKS_OF_PHILIPPINES, PHILIPPINES_OTC_ATM, PHILIPPINES_PAYMENT_CENTERS, BANKS_OF_INDONESIA_VA. See documentation for possible values. | string    | false    | AUB                                                                                                                                                                                                                        |

### ECommPayWalletWithdrawal

`POST /api/ecommpay/withdrawal/process`

| Name          | Located in   | Description                                                                                                                           | Data Type | Required | Example                                                                                                                   |
|---------------|--------------|---------------------------------------------------------------------------------------------------------------------------------------|-----------|----------|---------------------------------------------------------------------------------------------------------------------------|
| accountNumber | Request Body | User's wallet number. Required for YANDEX and QIWI.                                                                                   | string    | true     | 510019885431963                                                                                                           |
| service       | Request Body | Optional id of the withdrawal type. If not provided, and service is not configured in accounts config, will default to Wallet payout. | string    | false    | Possible values: YANDEX, QIWI, WEBMONEY, WEBMONEY_LIGHT, PAPARA, BANKS_OF_PHILIPPINES, PHILIPPINES_PAYMENT_CENTERS, GCASH |
| bankCode      | Request Body | User's bank. Required for BANKS_OF_PHILIPPINES, PHILIPPINES_PAYMENT_CENTERS. See documentation for possible values.                   | string    | false    | AUB                                                                                                                       |
| regionCode    | Request Body | User's region code. Required for BANKS_OF_PHILIPPINES. See documentation for possible values.                                         | string    | false    | 1234                                                                                                                      |
| branch        | Request Body | User's bank branch. Required for BANKS_OF_PHILIPPINES.                                                                                | string    | false    | Bank Branch                                                                                                               |

## eZeeWallet

### EzeeWalletDeposit

`POST /api/ezeewallet/deposit/process`

| Name           | Located in   | Description                   | Data Type | Required | Example              |
|----------------|--------------|-------------------------------|-----------|----------|----------------------|
| walletId       | Request Body | User's eZeeWallet id (Email). | string    | true     | jane.doe@example.com |
| walletPassword | Request Body | User's eZeeWallet password.   | string    | true     |                      |

### EzeeWalletWithdrawal

`POST /api/ezeewallet/withdrawal/process`

| Name     | Located in   | Description                   | Data Type | Required | Example              |
|----------|--------------|-------------------------------|-----------|----------|----------------------|
| walletId | Request Body | User's eZeeWallet id (Email). | string    | true     | jane.doe@example.com |

## MacroPay

### MacroPayWalletDeposit

`POST /api/macropay/deposit/process`

| Name          | Located in   | Description             | Data Type | Required | Example      |
|---------------|--------------|-------------------------|-----------|----------|--------------|
| accountNumber | Request Body | Customer account number | string    | true     | 510000000051 |

## Howtopay

### HowtopayWalletDeposit

`POST /api/howtopay/deposit/process`

| Name          | Located in   | Description                | Data Type | Required | Example                            |
|---------------|--------------|----------------------------|-----------|----------|------------------------------------|
| accountNumber | Request Body | Customer account number    | string    | true     | 510000000051                       |
| service       | Request Body | Payment method at Howtopay | string    | false    | Possible values: IDEAL, BPAY, POLI |

## LuxonPay

### LuxonPayWalletDeposit

`POST /api/luxonpay/deposit/process`

No provider specific params required - [To general request parameters](request)

### LuxonPayWalletWithdrawal

`POST /api/luxonpay/withdrawal/process`

| Name              | Located in   | Description             | Data Type | Required | Example                                    |
|-------------------|--------------|-------------------------|-----------|----------|--------------------------------------------|
| recipientWalletId | Request Body | LuxonPay user wallet ID | string    | true     | 0xd7f35dd52bd09d6fc7857a75ac7bf0866cbc5477 |

## SecureTrading

### SecureTradingWalletDeposit

`POST /api/securetradingwallet/deposit/process`

| Name        | Located in   | Description         | Data Type | Required | Example     |
|-------------|--------------|---------------------|-----------|----------|-------------|
| phoneNumber | Request Body | User's phone number | string    | true     | 46700000000 |
| service     | Request Body | ID of service       | string    | true     | QIWI        |

## Piastrix

### PiastrixWalletDeposit

`POST /api/piastrix/deposit/process`

| Name          | Located in   | Description                      | Data Type | Required | Example      |
|---------------|--------------|----------------------------------|-----------|----------|--------------|
| accountNumber | Request Body | Piastrix account number or email | string    | false    | 201234567890 |

### PiastrixWalletWithdrawal

`POST /api/piastrix/withdrawal/process`

| Name          | Located in   | Description                      | Data Type | Required | Example      |
|---------------|--------------|----------------------------------|-----------|----------|--------------|
| accountNumber | Request Body | Piastrix account number or email | string    | true     | 201234567890 |


## Zimpler

### ZimplerDeposit

`POST /api/zimpler/deposit/process`

| Name        | Located in   | Description         | Data Type | Required | Example                              |
|-------------|--------------|---------------------|-----------|----------|--------------------------------------|
| accountId   | Request Body | User saved account  | string    | false    | 307275a4-289b-45f1-a1c0-c22cfc8451a1 |
| phoneNumber | Request Body | User's phone number | string    | false    | +46700000000                         |

### ZimplerWithdrawal

`POST /api/zimpler/withdrawal/process`

| Name        | Located in   | Description         | Data Type | Required | Example                              |
|-------------|--------------|---------------------|-----------|----------|--------------------------------------|
| accountId   | Request Body | User saved account  | string    | false    | 307275a4-289b-45f1-a1c0-c22cfc8451a1 |
| phoneNumber | Request Body | User's phone number | string    | false    | +46700000000                         |

## Genome

### GenomeBankIBANWithdrawal

`POST /api/genome/withdrawal/process`

| Name            | Located in   | Description                       | Data Type | Required | Example            |
|-----------------|--------------|-----------------------------------|-----------|----------|--------------------|
| bic             | Request Body | The Business Identifier Code      | string    | true     | ABNANL2AXXX        |
| iban            | Request Body | International Bank Account Number | string    | true     | NL88ABNA2011060885 |
| beneficiaryName | Request Body | Beneficiary Name                  | string    | true     | John Doe           |

## Vipps

### VippsDeposit

`POST /api/vipps/deposit/process`

| Name        | Located in   | Description                                                                                 | Data Type | Required | Example  |
|-------------|--------------|---------------------------------------------------------------------------------------------|-----------|----------|----------|
| phoneNumber | Request Body | Phone number of Vipps user. Should match pattern: ^\s*(\d\s*){8}$. Whitespaces are allowed. | string    | true     | 48060312 |
