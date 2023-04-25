---
id: "Voucher"
---

# Voucher

The below listed voucher providers all have some additional parameter that needs to be included in the request for the transaction to be successful.

If the voucher provider you are adding is not listed, it means only the standard parameters are required.

## Aircash

### AircashVoucherDeposit

`POST /api/aircashvoucher/deposit/process`

| Name       | Located in   | Description                  | Data Type | Required | Example          |
|------------|--------------|------------------------------|-----------|----------|------------------|
| couponCode | Request Body | User's 16 digit coupon code. | string    | true     | 1467982261373355 |

## Aplauz

### AplauzDeposit

`POST /api/aplauz/deposit/process`

| Name        | Located in   | Description                  | Data Type | Required | Example          |
|-------------|--------------|------------------------------|-----------|----------|------------------|
| couponCode1 | Request Body | User's 16 digit coupon code. | string    | true     | 3786735063841789 |
| couponCode2 | Request Body | User's 16 digit coupon code. | string    | false    | 3786735063841789 |
| couponCode3 | Request Body | User's 16 digit coupon code. | string    | false    | 3786735063841789 |
| couponCode4 | Request Body | User's 16 digit coupon code. | string    | false    | 3786735063841789 |
| couponCod5  | Request Body | User's 16 digit coupon code. | string    | false    | 3786735063841789 |

## AstroPayCard

### AstroPayCardDeposit

`POST /api/astropaycard/deposit/process`

| Name                     | Located in   | Description                                                              | Data Type | Required | Example          |
|--------------------------|--------------|--------------------------------------------------------------------------|-----------|----------|------------------|
| cardHolder (deprecated)  | Request Body | Name of card holder. Only needed for the old API.                        | string    | true     | John Doe         |
| cardNumber (deprecated)  | Request Body | The AstroPay card number. Only needed for the old API.                   | string    | true     | 1612708538608684 |
| code (deprecated)        | Request Body | Card security code (CVV). Only needed for the old API.                   | string    | true     | 9732             |
| expiryMonth (deprecated) | Request Body | Two digit expiry month of the card [01-12]. Only needed for the old API. | string    | true     | 12               |
| expiryYear (deprecated)  | Request Body | Four digit expiry year of the credit card. Only needed for the old API.  | string    | true     | 2020             |

### AstroPayCardWithdrawal

`POST /api/astropaycard/withdrawal/process`

| Name        | Located in   | Description                                                                                                                                                                                        | Data Type | Required | Example                              |
|-------------|--------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------|----------|--------------------------------------|
| accountId   | Request Body | Account-id representing an Astropay card account used in a previous deposit by user                                                                                                                | string    | true     | d751d5e0-ebf6-44a2-84c4-e437a55b2cfc |
| phoneNumber | Request Body | User's phone number. If an accountId from a previous deposit is not used. If either this parameter or accountId is not used, the phone numer is taken from what's registered on the user (mobile). | string    | true     | +467493823776                        |

## Dimoco

### DimocoDeposit

`POST /api/dimoco/deposit/process`

| Name        | Located in   | Description                                                                          | Data Type | Required | Example      |
|-------------|--------------|--------------------------------------------------------------------------------------|-----------|----------|--------------|
| phoneNumber | Request Body | User's phone number. Taken from user "mobile" parameter if not provided as an input. | string    | false    | 447493823776 |

## EasyPay

### EasyPayDeposit

`POST /api/easypay/deposit/process`

No provider specific params required - [To general request parameters](request)

### EasyPayWithdrawal

`POST /api/easypay/withdrawal/process`

No provider specific params required - [To general request parameters](request)

## EMP (Epro) Cashlib

### CashlibDeposit

`POST /api/cashlib/deposit/process`

| Name          | Located in   | Description                                                                   | Data Type | Required | Example          |
|---------------|--------------|-------------------------------------------------------------------------------|-----------|----------|------------------|
| voucherNumber | Request Body | User's 16 digit voucher number. Required if making "Direct Voucher Payments". | string    | false    | 7837308941662931 |

## Flexepin

### FlexepinDeposit

`POST /api/flexepin/deposit/process`

| Name          | Located in   | Description                                     | Data Type | Required | Example      |
|---------------|--------------|-------------------------------------------------|-----------|----------|--------------|
| voucherNumber | Request Body | User's voucher number or a prepaid card number. | string    | true     | 327812992182 |

## Funanga

### FunangaDeposit

`POST /api/funanga/deposit/process`

No provider specific params required - [To general request parameters](request)

## Inovapay

### InovapayVoucherDeposit

`POST /api/inovapayvoucher/deposit/process`

| Name          | Located in   | Description                     | Data Type | Required | Example             |
|---------------|--------------|---------------------------------|-----------|----------|---------------------|
| voucherNumber | Request Body | User's 16 digit voucher number. | string    | true     | 2915 8505 0782 7916 |

## NeosurfVoucher

### NeosurfVoucherDeposit

`POST /api/neosurfvoucher/deposit/process`

| Name          | Located in   | Description            | Data Type | Required | Example    |
|---------------|--------------|------------------------|-----------|----------|------------|
| voucherNumber | Request Body | User's voucher number. | string    | true     | 2617037752 |

### NeosurfVoucherWithdrawal

`POST /api/neosurfvoucher/withdrawal/process`

| Name  | Located in   | Description                           | Data Type | Required | Example           |
|-------|--------------|---------------------------------------|-----------|----------|-------------------|
| email | Request Body | User's neosurf voucher email address. | string    | true     | jane.doe@test.com |

## Paykasa

### PaykasaDeposit

`POST /api/paykasa/deposit/process`

| Name          | Located in   | Description            | Data Type | Required | Example          |
|---------------|--------------|------------------------|-----------|----------|------------------|
| voucherNumber | Request Body | User's voucher number. | string    | true     | 1234567812345678 |

### PaykasaWithdrawal

`POST /api/paykasa/withdrawal/process`

No provider specific params required - [To general request parameters](request)

## Paysafecard

### PaysafecardDeposit

`POST /api/paysafecard/deposit/process`

No provider specific params required - [To general request parameters](request)

### PaysafecardWithdrawal

`POST /api/paysafecard/withdrawal/process`

| Name      | Located in   | Description                                                                                                                               | Data Type | Required | Example                              |
|-----------|--------------|-------------------------------------------------------------------------------------------------------------------------------------------|-----------|----------|--------------------------------------|
| email     | Request Body | Paysafecard account registered email address. Either this or accountId is required.                                                       | string    | true     | jane.doe@example.com                 |
| accountId | Request Body | Account-id representing a Paysafecard account used in a previous deposit by user. Either this or email is required.                       | string    | true     | d751d5e0-ebf6-44a2-84c4-e437a55b2cfc |
| firstName | Request Body | First name of the registered Paysafecard account. This is optional, if it's not included the first name is taken from the verifyuser data | string    | false    | Jane                                 |
| lastName  | Request Body | Last name of the registered Paysafecard account. This is optional, if it's not included the last name is taken from the verifyuser data   | string    | false    | Doe                                  |

## PerfectMoney

### PerfectMoneyVoucherDeposit

`POST /api/perfectmoney/deposit/process`

| Name          | Located in   | Description                  | Data Type | Required | Example          |
|---------------|--------------|------------------------------|-----------|----------|------------------|
| voucherNumber | Request Body | e-Voucher unique number      | string    | true     | 01234567891      |
| voucherCode   | Request Body | Activation code of e-Voucher | string    | true     | 0123456789123456 |

### PerfectMoneyVoucherWithdrawal

`POST /api/perfectmoney/withdrawal/process`

No provider specific params required - [To general request parameters](request)

## SmsVoucher

### SmsVoucherDeposit

`POST /api/smsvoucher/deposit/process`

| Name        | Located in   | Description                                                                                                   | Data Type | Required | Example                              |
|-------------|--------------|---------------------------------------------------------------------------------------------------------------|-----------|----------|--------------------------------------|
| phoneNumber | Request Body | User's phone number. Either this or accountId is required.                                                    | string    | true     | +420603123456                        |
| accountId   | Request Body | Representing a SmsVoucher account used in a previous deposit by user. Either this or phoneNumber is required. | string    | true     | d751d5e0-ebf6-44a2-84c4-e437a55b2cfc |

## Teleingreso

### TeleingresoDeposit

`POST /api/teleingreso/deposit/process`

No provider specific params required - [To general request parameters](request)

## TicketSurf

### TicketPremiumDeposit

`POST /api/ticketpremium/deposit/process`

| Name          | Located in   | Description                           | Data Type | Required | Example          |
|---------------|--------------|---------------------------------------|-----------|----------|------------------|
| voucherNumber | Request Body | Voucher pin or a prepaid card number. | string    | true     | 0263592307727584 |

### VisaVoucherDeposit

`POST /api/visavoucher/deposit/process`

No provider specific params required - [To general request parameters](request)

### WebRedirectDeposit

`POST /api/webredirect/deposit/process`

No provider specific params required - [To general request parameters](request)

## Ukash

### UkashDeposit

`POST /api/ukash/deposit/process`

| Name          | Located in   | Description                           | Data Type | Required | Example             |
|---------------|--------------|---------------------------------------|-----------|----------|---------------------|
| voucherNumber | Request Body | Voucher number associated with Ukash. | string    | true     | 6337180196830560254 |
| voucherValue  | Request Body | Value of the voucher.                 | string    | true     | 16.0                |

### UkashWithdrawal

`POST /api/ukash/withdrawal/process`

No provider specific params required - [To general request parameters](request)

## VLoad

### VLoadDeposit

`POST /api/vload/deposit/process`

| Name | Located in   | Description                        | Data Type | Required | Example          |
|------|--------------|------------------------------------|-----------|----------|------------------|
| pin  | Request Body | User's 16 to 20 alphanumeric code. | string    | true     | 8100046333731457 |

## Yopayments

### YopaymentsDeposit

`POST /api/yopayments/deposit/process`

| Name        | Located in   | Description         | Data Type | Required | Example       |
|-------------|--------------|---------------------|-----------|----------|---------------|
| phoneNumber | Request Body | User's phone number | string    | true     | +256701234567 |

### YopaymentsWithdrawal

`POST /api/yopayments/withdrawal/process`

| Name        | Located in   | Description         | Data Type | Required | Example       |
|-------------|--------------|---------------------|-----------|----------|---------------|
| phoneNumber | Request Body | User's phone number | string    | true     | +256701234567 |