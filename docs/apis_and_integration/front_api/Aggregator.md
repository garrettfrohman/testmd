---
id: "Aggregator"
---

# Aggregator

The below listed aggregator providers all have some additional parameter that needs to be included in the request for the transaction to be successful.

If the aggregator provider you are adding is not listed, it means only the standard parameters are required.


## AccentPay

### AccentPayDeposit

`POST /api/accentpay/deposit/process`

| Name    | Located in   | Description                                                                                   | Data Type | Required | Example      |
|---------|--------------|-----------------------------------------------------------------------------------------------|-----------|----------|--------------|
| service | Request Body | Specific service to control which payment method to use                                       | string    | true     | webmoney     |
| account | Request Body | Specific user account. For Webmoney it's the users wmid, For Qiwi it's the users phone number | string    | true     | 123456789123 |

### AccentPayWithdrawal

`POST /api/accentpay/withdrawal/process`

| Name    | Located in   | Description                                                                                   | Data Type | Required | Example      |
|---------|--------------|-----------------------------------------------------------------------------------------------|-----------|----------|--------------|
| service | Request Body | Specific service to control which payment method to use                                       | string    | true     | webmoney     |
| account | Request Body | Specific user account. For Webmoney it's the users wmid, For Qiwi it's the users phone number | string    | true     | 123456789123 |

## Alipay

### AlipayDeposit

`POST /api/alipay/deposit/process`

No provider specific params required - [To general request parameters](request)

## Apco

### ApcoDeposit

`POST /api/apco/deposit/process`

| Name    | Located in   | Description                                             | Data Type | Required | Example |
|---------|--------------|---------------------------------------------------------|-----------|----------|---------|
| service | Request Body | Specific service to control which payment method to use | string    | false    | GIROPAY |

### ApcoWithdrawal

`POST /api/apco/withdrawal/process`

| Name    | Located in   | Description                                             | Data Type | Required | Example |
|---------|--------------|---------------------------------------------------------|-----------|----------|---------|
| service | Request Body | Specific service to control which payment method to use | string    | true     | GIROPAY |

### ICardDeposit

`POST /api/icard/deposit/process`

No provider specific params required - [To general request parameters](request)

### ICardWithdrawal

`POST /api/icard/withdrawal/process`

No provider specific params required - [To general request parameters](request)

### PayPalDeposit

`POST /api/paypal/deposit/process`

No provider specific params required - [To general request parameters](request)

### PayPalWithdrawal

`POST /api/paypal/withdrawal/process`

No provider specific params required - [To general request parameters](request)

### SkrillDeposit

`POST /api/skrill/deposit/process`

No provider specific params required - [To general request parameters](request)

### SkrillWithdrawal

`POST /api/skrill/withdrawal/process`

No provider specific params required - [To general request parameters](request)

### NetellerDeposit

`POST /api/neteller/deposit/process`

No provider specific params required - [To general request parameters](request)

### NetellerWithdrawal

`POST /api/neteller/withdrawal/process`

No provider specific params required - [To general request parameters](request)

### IdealDeposit

`POST /api/ideal/deposit/process`

No provider specific params required - [To general request parameters](request)

### EcoPayzDeposit

`POST /api/ecopayz/deposit/process`

No provider specific params required - [To general request parameters](request)

### PaykasaDeposit

`POST /api/paykasa/deposit/process`

No provider specific params required - [To general request parameters](request)

### SofortDeposit

`POST /api/sofort/deposit/process`

No provider specific params required - [To general request parameters](request)

### GiropayDeposit

`POST /api/giropay/deposit/process`

No provider specific params required - [To general request parameters](request)

### PaysafeCardDeposit

`POST /api/paysafecard/deposit/process`

No provider specific params required - [To general request parameters](request)

## Dotpay

### DotpayDeposit

`POST /api/dotpay/deposit/process`

| Name    | Located in   | Description                                                                                                                                                                                                                                                | Data Type | Required | Example |
|---------|--------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------|----------|---------|
| service | Request Body | Dotpay payment service, contact DevCode for a complete list of services. If not provided the user will be redirected to a landing page where the user can select a service. If provided then the user will be directly redirected to the specific service. | string    | false    | 1       |

### BlikDeposit

`POST /api/blik/deposit/process`

| Name     | Located in   | Description                                                                 | Data Type | Required | Example |
|----------|--------------|-----------------------------------------------------------------------------|-----------|----------|---------|
| blikCode | Request Body | BLIK code, unique combination of six numbers which is valid for two minutes | string    | false    | 332122  |

### BankDeposit

`POST /api/bank/deposit/process`

No provider specific params required - [To general request parameters](request)

### BankIbanWithdrawal

`POST /api/bankiban/withdrawal/process`

No provider specific params required - [To general request parameters](request)

## EComCharge

### EComChargeDeposit

`POST /api/ecomcharge/deposit/process`

| Name    | Located in   | Description                                                                                          | Data Type | Required | Example |
|---------|--------------|------------------------------------------------------------------------------------------------------|-----------|----------|---------|
| service | Request Body | Use this parameter if the user should be redirected directly to a specific EComCharge payment method | string    | false    | LHV_EST |

## FSTech

### FSTechWithdrawal

`POST /api/fstech/withdrawal/process`

No provider specific params required - [To general request parameters](request)

## Kluwp

### KluwpDeposit

`POST /api/kluwp/deposit/process`

| Name    | Located in   | Description                                                                                                                                                      | Data Type | Required | Example                                                                                                                                                                                                                        |
|---------|--------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| service | Request Body | Optional id of the payment service. If not provided and provider has more than one service, the user will be prompted with a page where he can select a service. | string    | false    | Possible values: CREDITCARD, CHINA_UNION_PAY, MASTERCARD_GIFT_CARD, POST24, PAYPAL, POSTEPAY, MULTIBANCO, PAYSEC, ECOVOUCHER, MONEYCARD24, GSCASH, EPAYCODE, CASHIXIR, JETON, INSTANTBANKTRANSFER, SOFORT, IDEAL, VISA_VOUCHER |

### ChinaUnionPayDeposit

`POST /api/chinaunionpay/deposit/process`

| Name    | Located in   | Description                             | Data Type | Required | Example |
|---------|--------------|-----------------------------------------|-----------|----------|---------|
| service | Request Body | Corresponds to a bank code ex: “1” ICBC | string    | false    | 1       |

### VisaVoucherDeposit

`POST /api/visavoucher/deposit/process`

No provider specific params required - [To general request parameters](request)

### GiftcardDeposit

`POST /api/giftcard/deposit/process`

No provider specific params required - [To general request parameters](request)

### BankDeposit

`POST /api/bank/deposit/process`

No provider specific params required - [To general request parameters](request)

### BankIbanWithdrawal

`POST /api/bankiban/withdrawal/process`

No provider specific params required - [To general request parameters](request)

## MobileGiro

### SweGiroDeposit

`POST /api/swegiro/deposit/process`

| Name        | Located in   | Description                                                                                                                      | Data Type | Required | Example                          |
|-------------|--------------|----------------------------------------------------------------------------------------------------------------------------------|-----------|----------|----------------------------------|
| beneficiary | Request Body | Name of the beneficiary                                                                                                          | string    | true     | Jane Doe                         |
| number      | Request Body | Bankgiro or Postgiro number                                                                                                      | string    | true     | 846401-8                         |
| numberType  | Request Body | Type of number                                                                                                                   | string    | true     | PG for Postgiro, BG for Bankgiro |
| ocr         | Request Body | This or message must be used but not both.                                                                                       | string    | false    | 1234567890                       |
| message     | Request Body | This or ocr must be used but not both.                                                                                           | string    | false    | Example message                  |
| dueDate     | Request Body | The date when the invoice should be payed, in ISO format. The date should be a day in the future and a bank day (Not a weekend). | string    | true     | 2020-01-01                       |

## PPro

### PProDeposit

`POST /api/ppro/deposit/process`

| Name    | Located in   | Description                                             | Data Type | Required | Example                                                                                                                                                                                                                                                             |
|---------|--------------|---------------------------------------------------------|-----------|----------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| service | Request Body | Specific service to control which payment method to use | string    | true     | Available services: ASTROPAYCARD, ASTROPAYDIRECT, MISTERCASH, BOLETO, EPS, GIROPAY, IDEAL, OXXO, P24, PAYSAFECARD, POLI, POSTFINANCE, PUGGLEPAY, QIWI, SAFETYPAY, SEPADIRECTDEBIT, SKRILL, SOFORT, TELEINGRESO, TRUSTLY, TRUSTPAY, VERKKOPANKKI, MULTIBANCO, MYBANK |

### BoletoDeposit

`POST /api/boleto/deposit/process`

| Name       | Located in   | Description                                                                                     | Data Type | Required | Example              |
|------------|--------------|-------------------------------------------------------------------------------------------------|-----------|----------|----------------------|
| nationalId | Request Body | Consumer’s national id (up to 30 characters). Format needs to match regex ^[a-zA-Z- 0-9]{1,30}$ | string    | true     | 12345678901234567890 |

### OxxoDeposit

`POST /api/oxxo/deposit/process`

| Name       | Located in   | Description                                                                                     | Data Type | Required | Example              |
|------------|--------------|-------------------------------------------------------------------------------------------------|-----------|----------|----------------------|
| nationalId | Request Body | Consumer’s national id (up to 30 characters). Format needs to match regex ^[a-zA-Z- 0-9]{1,30}$ | string    | true     | 12345678901234567890 |

### PugglePayDeposit

`POST /api/pugglepay/deposit/process`

| Name | Located in   | Description         | Data Type | Required | Example      |
|------|--------------|---------------------|-----------|----------|--------------|
| pno  | Request Body | User's phone number | string    | true     | +46700000000 |

### QiwiDeposit

`POST /api/qiwi/deposit/process`

| Name        | Located in   | Description                                                                                             | Data Type | Required | Example      |
|-------------|--------------|---------------------------------------------------------------------------------------------------------|-----------|----------|--------------|
| phoneNumber | Request Body | User's phone number. Format needs to match  regex ([0-9]{10})|(\+7[0-9]{10})|(\+[0-68-9]{1}[0-9]{9,30}) | string    | true     | +71234567890 |

### BankIBANWithdrawal

`POST /api/bankiban/withdrawal/process`

| Name | Located in   | Description                                       | Data Type | Required | Example                |
|------|--------------|---------------------------------------------------|-----------|----------|------------------------|
| iban | Request Body | User's bank IBAN, required for service SEPAPAYOUT | string    | true     | DE44500105175407324931 |

### BankLocalWithdrawal

`POST /api/banklocal/withdrawal/process`

| Name          | Located in   | Description                                                | Data Type | Required | Example  |
|---------------|--------------|------------------------------------------------------------|-----------|----------|----------|
| accountNumber | Request Body | User's bank account number, required for service INTPAYOUT | string    | true     | 12345678 |

### QiwiWithdrawal

`POST /api/qiwi/withdrawal/process`

| Name        | Located in   | Description                                                                                                                                    | Data Type | Required | Example      |
|-------------|--------------|------------------------------------------------------------------------------------------------------------------------------------------------|-----------|----------|--------------|
| phoneNumber | Request Body | User's phone number. Format needs to match  regex ([0-9]{10})|(\+7[0-9]{10})|(\+[0-68-9]{1}[0-9]{9,30}). Either this or accountId is required. | string    | true     | +71234567890 |

## MacroPay

### WebRedirectDeposit

`POST /api/webredirect/deposit/process`

| Name    | Located in   | Description                                           | Data Type | Required | Example |
|---------|--------------|-------------------------------------------------------|-----------|----------|---------|
| service | Request Body | Mandatory service value that decides which APM to use | string    | true     | IDEAL   |

### IdealDeposit

`POST /api/ideal/deposit/process`

No provider specific params required - [To general request parameters](request)

### SofortDeposit

`POST /api/sofort/deposit/process`

No provider specific params required - [To general request parameters](request)

### GiropayDeposit

`POST /api/giropay/deposit/process`

No provider specific params required - [To general request parameters](request)

### EpsDeposit

`POST /api/eps/deposit/process`

No provider specific params required - [To general request parameters](request)

### BoletoDeposit

`POST /api/boleto/deposit/process`

| Name       | Located in   | Description                                                                                     | Data Type | Required | Example              |
|------------|--------------|-------------------------------------------------------------------------------------------------|-----------|----------|----------------------|
| nationalId | Request Body | Consumer’s national id (up to 30 characters). Format needs to match regex ^[a-zA-Z- 0-9]{1,30}$ | string    | true     | 12345678901234567890 |

## Pradexx

### PradexxDeposit

`POST /api/pradexx/deposit/process`

| Name    | Located in   | Description                                                                                    | Data Type | Required | Example                             |
|---------|--------------|------------------------------------------------------------------------------------------------|-----------|----------|-------------------------------------|
| service | Request Body | If not provided the service configured in PradexxConfig will be used, so it must be set there. | string    | false    | Possible values: SOFORT, NEXTPAYWAY |

## Przelewy24

### Przelewy24Deposit

`POST /api/przelewy24/deposit/process`

| Name    | Located in   | Description                                                                                                                                                                                          | Data Type | Required | Example |
|---------|--------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------|----------|---------|
| service | Request Body | Payment method ID. It is used to redirect a customer directly to a selected method of payment. For instance, when redirecting to the method of mTransfer, the p24_method field needs to be set to 25 | string    | false    | 25      |

## SafeCharge

### WebRedirectDeposit

`POST /api/webredirect/deposit/process`

| Name    | Located in   | Description                                                           | Data Type | Required | Example  |
|---------|--------------|-----------------------------------------------------------------------|-----------|----------|----------|
| service | Request Body | Mandatory when initiating an ApplePay payment, value must be APPLEPAY | string    | true     | APPLEPAY |

### SofortDeposit

`POST /api/sofort/deposit/process`

No provider specific params required - [To general request parameters](request)

### GiropayDeposit

`POST /api/giropay/deposit/process`

No provider specific params required - [To general request parameters](request)

### PaysafecardDeposit

`POST /api/paysafecard/deposit/process`

No provider specific params required - [To general request parameters](request)

## ToditoCash (deprecated)

### ToditoCashDeposit

`POST /api/toditocash/deposit/process`

| Name       | Located in   | Description                                                                                            | Data Type | Required | Example    |
|------------|--------------|--------------------------------------------------------------------------------------------------------|-----------|----------|------------|
| nip        | Request Body |                                                                                                        | string    | true     | 3333       |
| cardNumber | Request Body | ToditoCash card number. This can be a Folio, PIN or a SAN (up to 20 symbols) depending on the product. | string    | true     | 1111111111 |

## Todito

### ToditoCashDeposit

`POST /api/todito/deposit/process`

| Name          | Located in   | Description            | Data Type | Required | Example    |
|---------------|--------------|------------------------|-----------|----------|------------|
| nip           | Request Body |                        | string    | true     | 3333       |
| accountNumber | Request Body | Todito account number. | string    | true     | 2622047317 |

## HiPay

### HiPayDeposit

`POST /api/hipay/deposit/process`

| Name    | Located in   | Description                                                                   | Data Type | Required | Example                                                                                                                                                                       |
|---------|--------------|-------------------------------------------------------------------------------|-----------|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| service | Request Body | Optional id of the payment service. If not provided will fallback to GIROPAY. | string    | false    | Possible values: BANK_TRANSFER, DEXIA, GIROPAY, ING_HOMEPAY, KLARNA, PRZELEWY24, SISAL, SOFORT, WEBMONEY, YANDEX, PAYPAL, CBC, KBC, PAYSAFECARD, PAY_U, AURA, BOLETO and OXXO |

### WebRedirectDeposit

`POST /api/webredirect/deposit/process`

No provider specific params required - [To general request parameters](request)
