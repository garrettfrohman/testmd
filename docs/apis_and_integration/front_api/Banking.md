---
id: "Banking"
---

# Banking

The below listed bank providers all have some additional parameter that needs to be included in the request for the transaction to be successful.

If the bank provider you are adding is not listed, it means only the standard parameters are required.

## Directa24 (AstropayDirect 2.0)

### BankDeposit

`POST /api/bank/deposit/process`

| Name       | Located in   | Description                                                                                                                                             | Data Type | Required | Example        |
|------------|--------------|---------------------------------------------------------------------------------------------------------------------------------------------------------|-----------|----------|----------------|
| service    | Request Body | Id of the bank/service. How to find the available banks for each country is described in the provider documentation.                                    | string    | true     | VI             |
| nationalId | Request Body | Mandatory using Directa24. SL: User’s personal identification number. BR: CPF/CNPJ. AR: DNI. UY: CI. MX: CURP/RFC/IFE. PE: DNI. CL: RUT. CO: CC. TK: ID | string    | true     | 747.873.778-17 |

### AstroPayBankWithdrawal

`POST /api/astropaybank/withdrawal/process`

| Name           | Located in   | Description                                                                                                                                                                | Data Type | Required | Example     |
|----------------|--------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------|----------|-------------|
| nationalId     | Request Body | Beneficiary’s personal identification number. SL: User’s personal identification number. BR: CPF/CNPJ. AR: DNI. UY: CI. MX: CURP/RFC/IFE. PE: DNI. CL: RUT. CO: CC. TK: ID | string    | true     | 63017363201 |
| nationalIdType | Request Body | Beneficiary’s personal identification type. Mandatory for Chile and Perú                                                                                                   | string    | true     | CC          |
| bankCode       | Request Body | Beneficiary's bank code. Mandatory for Brazil, Chile, Colombia, and Perú                                                                                                   | string    | true     | 005         |
| bankBranch     | Request Body | Beneficiary's bank branch number. Mandatory for Brazil, Uruguay, and China                                                                                                 | string    | true     | 7197        |
| bankAccount    | Request Body | Beneficiary's bank account number. Mandatory for all countries.                                                                                                            | string    | true     | 88365484    |
| accountType    | Request Body | Type of account. C: for Current accounts S: for Savings accounts. Mandatory for Brazil, Chile, Colombia, Perú, and Uruguay                                                 | string    | true     | C           |

## RapidPaymentsNetwork

### ChinaUnionPayDeposit

`POST /api/chinaunionpay/deposit/process`

| Name    | Located in   | Description                             | Data Type | Required | Example |
|---------|--------------|-----------------------------------------|-----------|----------|---------|
| service | Request Body | Corresponds to a bank code ex: “1” ICBC | string    | true     | 1       |

### ChinaUnionPayWithdrawal

`POST /api/chinaunionpay/deposit/process`

| Name            | Located in   | Description       | Data Type | Required | Example                   |
|-----------------|--------------|-------------------|-----------|----------|---------------------------|
| bankName        | Request Body | Bank name         | string    | true     | Example Bank              |
| subBranch       | Request Body | Sub branch        | string    | true     | Example sub branch        |
| bankAccountName | Request Body | Bank account name | string    | true     | Example bank acocunt name |
| bankCardNo      | Request Body | Bank card number  | string    | true     | 123123123                 |
| province        | Request Body | Province          | string    | true     | Example province          |
| area            | Request Body | Area              | string    | true     | Example area              |

## PayRetailers

### WebRedirectDeposit

`POST /api/webredirect/deposit/process`

| Name    | Located in   | Description                                                                   | Data Type | Required | Example      |
|---------|--------------|-------------------------------------------------------------------------------|-----------|----------|--------------|
| service | Request Body | Mandatory when initiating an PayRetailers deposit, value must be PAYRETAILERS | string    | true     | PAYRETAILERS |

### PayRetailersWithdrawal

`POST /api/payretailers/withdrawal/process`

| Name                | Located in   | Description           | Data Type | Required | Example                                  |
|---------------------|--------------|-----------------------|-----------|----------|------------------------------------------|
| bankName            | Request Body | Bank name             | string    | true     | Example Bank                             |
| recipientPixKey     | Request Body | Recipient PIX Key that will vary in value depending on the customer's PIX key, which can be one of the following: Phone Number, E-mail, Random Key, CPF | string    | true     | Required for PIX withdrawal in Brazil (example "fb541dbe-4bbb-4df5-b816-3a755f662b8e" or "13686665824") |    
| accountAgencyNumber | Request Body | Account Agency Number | string    | true     | Required for Brazil, Ecuador and Peru (example: 8585) |
| accountNumber       | Request Body | Bank account number   | string    | true     | Example bank acocunt number              |
| documentNumber      | Request Body | Document Number       | string    | true     | 86162357015                              |
| documentType        | Request Body | Document Type         | string    | true     | Example document type                    |
| accountType         | Request Body | Account Type          | string    | true     | Example account type                     |
| beneficiaryName     | Request Body | Beneficiary Name      | string    | true     | firstName lastName                       |

## Sofort

### SofortDeposit

`POST /api/sofort/deposit/process`

No provider specific params required - [To general Bank request parameters](BankDeposit)

## EasyPay

### BankIBANWithdrawal

`POST /api/bankiban/withdrawal/process`

| Name            | Located in   | Description                                                                                                                        | Data Type | Required | Example                |
|-----------------|--------------|------------------------------------------------------------------------------------------------------------------------------------|-----------|----------|------------------------|
| iban            | Request Body | IBAN                                                                                                                               | string    | true     | BG51STSA93006349276471 |
| beneficiaryName | Request Body | Name of the account holder of the target account. If not provided the user's first and last name will be used. 1 to 50 characters. | string    | false    | Jane Doe               |

## Euteller

### EutellerDeposit

`POST /api/euteller/deposit/process`

| Name    | Located in   | Description                                        | Data Type | Required | Example                                                                                                    |
|---------|--------------|----------------------------------------------------|-----------|----------|------------------------------------------------------------------------------------------------------------|
| service | Request Body | Bank name when using "Direct Bank Selection" mode. | string    | false    | Possible values: op, nordea, spankki, danske, saastopankki, aktia, pop, handelsbanken, omasp, alandsbanken |

### SiirtoDeposit

`POST /api/siirto/deposit/process`

| Name        | Located in   | Description                                              | Data Type | Required | Example       |
|-------------|--------------|----------------------------------------------------------|-----------|----------|---------------|
| phoneNumber | Request Body | User's phone number that is connected to Siirto account. | string    | true     | +358509999991 |

### SiirtoWithdrawal

`POST /api/siirto/withdrawal/process`

| Name        | Located in   | Description                                              | Data Type | Required | Example       |
|-------------|--------------|----------------------------------------------------------|-----------|----------|---------------|
| phoneNumber | Request Body | User's phone number that is connected to Siirto account. | string    | true     | +358509999991 |

## Envoy

### EnvoyDeposit

`POST /api/envoy/deposit/process`

| Name    | Located in   | Description                                                  | Data Type | Required | Example |
|---------|--------------|--------------------------------------------------------------|-----------|----------|---------|
| service | Request Body | The Envoy bank service.                                      | string    | true     | SOFORT  |
| country | Request Body | User's country (might differ from user's registered country) | string    | true     | DK      |

### EnvoyWithdrawal

`POST /api/envoy/withdrawal/process`

| Name                | Located in   | Description                                                                                                                        | Data Type | Required | Example                |
|---------------------|--------------|------------------------------------------------------------------------------------------------------------------------------------|-----------|----------|------------------------|
| accountNumberOrIban | Request Body | Account number or IBAN                                                                                                             | string    | false    | DE29AIBK93115212345678 |
| accountHolder       | Request Body | Name of the account holder                                                                                                         | string    | false    | John Doe               |
| bankName            | Request Body | Name of the bank                                                                                                                   | string    | false    | The Bank               |
| countryCode         | Request Body | Country code of the receiving country                                                                                              | string    | false    | DE                     |
| bankCode            | Request Body | Bank code (or ‘sort code’ in some territories) associated with the receiving account bank and/or branch. Needed for some countries | string    | false    | 123456                 |
| branchCode          | Request Body | Branch code associated with the receiving account branch. Needed for some countries                                                | string    | false    | 98                     |
| branchAddress       | Request Body | Address of the bank branch. needed for most countries                                                                              | string    | false    | Bank branch 2          |
| accountType         | Request Body | Type of account. Needed for some countries                                                                                         | string    | false    |                        |
| checkDigits         | Request Body | needed for some countries                                                                                                          | string    | false    |                        |
| swift               | Request Body | SWIFT. needed for some countries and international payments                                                                        | string    | false    | DABAIE2D               |
| additionalInfo      | Request Body | Needed in cases to send in some additional data for some countries (Latvia for instance)                                           | string    | false    | Additional information |

## Entercash

### BankDeposit

`POST /api/bank/deposit/process`

| Name  | Located in   | Description                                   | Data Type | Required | Example                 |
|-------|--------------|-----------------------------------------------|-----------|----------|-------------------------|
| token | Request Body | The ident token to initiate a direct deposit. | string    | false    | 23-zp217inpp91jfzay1ogd |

### BankIbanWithdrawal

`POST /api/bankiban/withdrawal/process`

No provider specific params required - [To general Bank request parameters](BankDeposit)

### BankLocalWithdrawal

`POST /api/banklocal/withdrawal/process`

No provider specific params required - [To general Bank request parameters](BankDeposit)

## DanskeBank

### NemKontoWithdrawal

`POST /api/nemkonto/withdrawal/process`

| Name | Located in   | Description                                                                        | Data Type | Required | Example    |
|------|--------------|------------------------------------------------------------------------------------|-----------|----------|------------|
| cpr  | Request Body | Danish CPR number to identify the person who should receive the funds (10 digits). | string    | true     | 1234567890 |

## Eps

### EpsDeposit

`POST /api/eps/deposit/process`

| Name    | Located in   | Description                                      | Data Type | Required | Example  |
|---------|--------------|--------------------------------------------------|-----------|----------|----------|
| service | Request Body | EPS bank service. Required when using with Adyen | string    | false    | EASYBANK |

## Help2Pay

### BankDeposit

`POST /api/bank/deposit/process`

| Name    | Located in   | Description | Data Type | Required | Example |
|---------|--------------|-------------|-----------|----------|---------|
| service | Request Body | BankCode    | string    | true     | MBB     |

### BankDomesticWithdrawal

`POST /api/bankdomestic/withdrawal/process`

| Name            | Located in   | Description                                                                                                   | Data Type | Required | Example   |
|-----------------|--------------|---------------------------------------------------------------------------------------------------------------|-----------|----------|-----------|
| accountNumber   | Request Body | Target account number                                                                                         | string    | true     | 123456789 |
| beneficiaryName | Request Body | Name of the account holder of the target account. If not provided the user's first and last name will be used | string    | true     | Jane Doe  |
| bankName        | Request Body | BankCode of beneficiary bank                                                                                  | string    | true     | MBB       |

## Ideal

### IdealDeposit

`POST /api/ideal/deposit/process`

| Name    | Located in   | Description                                                                                                                       | Data Type | Required | Example                                                                                                                                |
|---------|--------------|-----------------------------------------------------------------------------------------------------------------------------------|-----------|----------|----------------------------------------------------------------------------------------------------------------------------------------|
| service | Request Body | Ideal bank service. It should be one of following values. (This string should not to be sent for Ideal transaction with Trustly). | string    | false    | One of the following: 'ABN_AMRO', 'ASN', 'ING', 'FRIESLAND', 'RABOBANK', 'SNS', 'SNS_REGIO', 'TRIODOS', 'VAN_LANSCHOT', 'KNAB', 'BUNQ' |

## Inovapay

### BankDeposit

`POST /api/bank/deposit/process`

No provider specific params required - [To general Bank request parameters](BankDeposit)

### InovapayBankWithdrawal

`POST /api/inovapaybank/withdrawal/process`

| Name          | Located in   | Description                                                                             | Data Type | Required | Example                                                                |
|---------------|--------------|-----------------------------------------------------------------------------------------|-----------|----------|------------------------------------------------------------------------|
| service       | Request Body | Service that represents the payment method to use                                       | string    | true     | Available values: PIX, BANCODOBRASIL, BRADESCO, CAIXA, ITAU, SANTANDER |
| nationalId    | Request Body | User's national id number (CPF)                                                         | string    | true     | 14528508010                                                            |
| pixKey        | Request Body | Must be a valid CPF and that CPF must be a registered pix key (Only required for pix)   | string    | true     | 14528508010                                                            |
| branchCode    | Request Body | User's bank branch code (Not required for pix)                                          | string    | true     |                                                                        |
| accountNumber | Request Body | User's bank account number (Not required for pix)                                       | string    | true     |                                                                        |
| accountType   | Request Body | Type of account. C: for Current accounts S: for Savings accounts (Not required for pix) | string    | true     | C                                                                      |

## Inpay

### BankIntlWithdrawal

`POST /api/bankintl/withdrawal/process`

No provider specific params required - [To general Bank request parameters](BankDeposit)

### BankLocalWithdrawal

`POST /api/banklocal/withdrawal/process`

No provider specific params required - [To general Bank request parameters](BankDeposit)

## Instadebit

### InstadebitDeposit

`POST /api/instadebit/deposit/process`

No provider specific params required - [To general Bank request parameters](BankDeposit)

### InstadebitWithdrawal

`POST /api/instadebit/withdrawal/process`

| Name      | Located in   | Description                                                                       | Data Type | Required | Example                              |
|-----------|--------------|-----------------------------------------------------------------------------------|-----------|----------|--------------------------------------|
| accountId | Request Body | Account-id representing an Instadebit account used in a previous deposit by user. | string    | true     | d751d5e0-ebf6-44a2-84c4-e437a55b2cfc |

### InstadebitECheckDeposit

`POST /api/instadebitecheck/deposit/process`

| Name          | Located in   | Description                                                                                                                          | Data Type | Required | Example           |
|---------------|--------------|--------------------------------------------------------------------------------------------------------------------------------------|-----------|----------|-------------------|
| accountType   | Request Body | The Consumer’s bank account type. PERSONAL_CHECKING or PERSONAL_SAVING                                                               | string    | true     | PERSONAL_CHECKING |
| routingNumber | Request Body | The Consumer’s bank routing/ABA number. For Canadian banks, this is a 3-digit institution number followed by 5-digit transit number. | string    | true     | 00302506          |
| accountNumber | Request Body | The Consumer's bank account number. Canadian account numbers can include up to 12 digits.                                            | string    | true     | 2834745371        |
| ssn           | Request Body | Last 4 digits of the Consumer’s social insurance number (SIN).                                                                       | string    | true     | 2849              |

### InstadebitECheckWithdrawal

`POST /api/instadebitecheck/withdrawal/process`

| Name          | Located in   | Description                                                                                                                          | Data Type | Required | Example           |
|---------------|--------------|--------------------------------------------------------------------------------------------------------------------------------------|-----------|----------|-------------------|
| accountType   | Request Body | The Consumer’s bank account type. PERSONAL_CHECKING or PERSONAL_SAVING                                                               | string    | true     | PERSONAL_CHECKING |
| routingNumber | Request Body | The Consumer’s bank routing/ABA number. For Canadian banks, this is a 3-digit institution number followed by 5-digit transit number. | string    | true     | 00302506          |
| accountNumber | Request Body | The Consumer's bank account number. Canadian account numbers can include up to 12 digits.                                            | string    | true     | 2834745371        |
| ssn           | Request Body | Last 4 digits of the Consumer’s social insurance number (SIN).                                                                       | string    | true     | 2849              |

## Interac

### InteracWithdrawal

`POST /api/interac/withdrawal/process`

| Name   | Located in   | Description                                                                                 | Data Type | Required | Example              |
|--------|--------------|---------------------------------------------------------------------------------------------|-----------|----------|----------------------|
| email  | Request Body | End user email. If not included here it will be taken from the verifyuser response.         | string    | false    | jane.doe@example.com |
| mobile | Request Body | Canadian mobile number. If not included here it will be taken from the verifyuser response. | string    | false    | 6135550170           |

### InteracDirectWithdrawal

`POST /api/interacdirect/withdrawal/process`

| Name                       | Located in   | Description                                                   | Data Type | Required | Example |
|----------------------------|--------------|---------------------------------------------------------------|-----------|----------|---------|
| financialInstitutionNumber | Request Body | Financial institution number of the beneficiary bank account. | string    | true     | 123     |
| transitNumber              | Request Body | Transit number of the beneficiary bank account.               | string    | true     | 12345   |
| accountNumber              | Request Body | Beneficiary bank account number.                              | string    | true     | 1234567 |

## Idebit

### IDebitDeposit

`POST /api/idebit/deposit/process`

| Name    | Located in   | Description                            | Data Type | Required | Example   |
|---------|--------------|----------------------------------------|-----------|----------|-----------|
| account | Request Body | Account representing an Idebit account | string    | false    | 123456789 |

### IDebitWithdrawal

`POST /api/idebit/withdrawal/process`

| Name      | Located in   | Description                                                                   | Data Type | Required | Example                              |
|-----------|--------------|-------------------------------------------------------------------------------|-----------|----------|--------------------------------------|
| accountId | Request Body | Account-id representing an Idebit account used in a previous deposit by user. | string    | true     | d751d5e0-ebf6-44a2-84c4-e437a55b2cfc |

## LuqaPay (formerly BestPay)

### BestPayDeposit

`POST /api/bestpay/deposit/process`

| Name    | Located in   | Description | Data Type | Required | Example   |
|---------|--------------|-------------|-----------|----------|-----------|
| service | Request Body | Bank code   | string    | true     | MERGENXXX |

### BestPayWithdrawal

`POST /api/bestpay/withdrawal/process`

| Name          | Located in   | Description                                                | Data Type | Required | Example     |
|---------------|--------------|------------------------------------------------------------|-----------|----------|-------------|
| accountNumber | Request Body | Account Number which equals to international phone number. | string    | true     | +4740300333 |
| swiftCode     | Request Body | Bank swift code                                            | string    | true     | VIPPSNO     |

### BankLocalWithdrawal

`POST /api/banklocal/withdrawal/process`

| Name                 | Located in   | Description                                                                                                                        | Data Type | Required    | Example              |
|----------------------|--------------|------------------------------------------------------------------------------------------------------------------------------------|-----------|-------------|----------------------|
| clearingNumber       | Request Body | For Japanese bank withdrawals this has to be the bankCode (4 digits) + branchCode (3 digits)                                       | string    | true        | 1234123              |
| accountNumber        | Request Body | Target account number                                                                                                              | string    | true        | 123456789            |
| bankName             | Request Body | Name of the bank. Should be in local language (e.g. for Japan - Japanese). 1 to 50 characters.                                     | string    | true        | 三井住友銀行           |
| branchName           | Request Body | Name of the branch. Should be in local language (for Japan - Hiragana or Katakana, no Kanji). 1 to 50 characters.                  | string    | true        | オカモト              |
| beneficiaryName      | Request Body | Name of the account holder of the target account. If not provided the user's first and last name will be used. 1 to 50 characters. | string    | false/true* | Haruto Watanabe      |
| localBeneficiaryName | Request Body | Name of the account holder of the target account in local language (for Japan - Hiragana or Katakana, no Kanji)                    | string    | true        | ハルト わたなべ         |
*For VIP withdrawal payment method - beneficiaryName and localBeneficiaryName are required to provide in the input.

### BankIBANWithdrawal

`POST /api/bankiban/withdrawal/process`

| Name            | Located in   | Description                                       | Data Type | Required | Example                |
|-----------------|--------------|---------------------------------------------------|-----------|----------|------------------------|
| bic             | Request Body | Receiver bank Swift code                          | string    | true     | NEPRNO21XXX            |
| iban            | Request Body | IBAN                                              | string    | true     | NO0323333311111        |
| bankName        | Request Body | Name of the bank.                                 | string    | false*   | Skue Sparebank         |
| beneficiaryName | Request Body | Name of the account holder of the target account. | string    | true     | Luke Ericsson          |
*If bankName isn't provided within input request - PaymentIQ will try to obtain bankName from bankMapping.

### BestPayNetbankingWithdrawal

`POST /api/bestpaynetbanking/withdrawal/process`

| Name            | Located in   | Description                                                  | Data Type | Required | Example                                   |
| --------------- | ------------ | ------------------------------------------------------------ | --------- | -------- | ----------------------------------------- |
| ifscCode        | Request Body | IFSC code                                                    | string    | true     | ABHY0065211                               |
| accountNumber   | Request Body | Target account number                                        | string    | true     | 123456789                                 |

### BestPayBankTransferWithdrawal

`POST /api/bestpaytransfer/withdrawal/process`

| Name          | Located in   | Description             | Data Type | Required | Example |
| ------------- | ------------ | ----------------------- | --------- | -------- | ------- |
| branchCode    | Request Body | User's bank branch code | string    | true     | 130     |
| accountNumber | Request Body | Target account number   | string    | true     | 1234568 |

## NetBanking

### BankDeposit

`POST /api/bank/deposit/process`

No provider specific params required - [To general Bank request parameters](BankDeposit)

### BankIntlWithdrawal

`POST /api/bankintl/withdrawal/process`

| Name            | Located in   | Description                                                                                                                        | Data Type | Required | Example                                   |
|-----------------|--------------|------------------------------------------------------------------------------------------------------------------------------------|-----------|----------|-------------------------------------------|
| bic             | Request Body | IFSC code                                                                                                                          | string    | true     | ABHY0065211                               |
| accountNumber   | Request Body | Target account number                                                                                                              | string    | true     | 123456789                                 |
| beneficiaryName | Request Body | Name of the account holder of the target account. If not provided the user's first and last name will be used. 1 to 50 characters. | string    | false    | Jane Doe                                  |
| bankName        | Request Body | Name of the bank, not case sensitive. 1 to 50 characters.                                                                          | string    | true     | ABHYUDAYA CO-OP BANK LTD                  |
| branchName      | Request Body | Name of the branch, not case sensitive. 1 to 50 characters.                                                                        | string    | true     | DHOLAKA                                   |
| branchAddress   | Request Body | Address of the target bank branch receiving the payment. 1 to 250 characters.                                                      | string    | true     | DHOLAKA COTTON MARKET, CHARITY FOUNDATION |

## Vicus

### BankDeposit

`POST /api/bank/deposit/process`

| Name    | Located in   | Description | Data Type | Required | Example |
|---------|--------------|-------------|-----------|----------|---------|
| service | Request Body | Bank Code   | string    | true     | QR.TH   |

### BankLocalWithdrawal

`POST /api/banklocal/withdrawal/process`

| Name            | Located in   | Description              | Data Type | Required | Example     |
|-----------------|--------------|--------------------------|-----------|----------|-------------|
| clearingNumber  | Request Body | Bank branch              | string    | true     | branch_1234 |
| accountNumber   | Request Body | Bank account number      | string    | true     | 123456789   |
| bankName        | Request Body | Bank code                | string    | true     | BBL         |
| beneficiaryName | Request Body | Bank account holder name | string    | false    | Jane Doe    |

## MoneyPay

### MoneyPayDeposit

`POST /api/moneypay/deposit/process`

| Name        | Located in   | Description                                   | Data Type | Required | Example |
|-------------|--------------|-----------------------------------------------|-----------|----------|---------|
| last4Digits | Request Body | last 4 digits of the user bank account number | string    | true     | 1234    |
| username    | Request Body | User bank account name                        | string    | true     | Mary Li |

### MoneyPayWithdrawal

`POST /api/moneypay/withdrawal/process`

| Name            | Located in   | Description              | Data Type | Required | Example        |
|-----------------|--------------|--------------------------|-----------|----------|----------------|
| accountNumber   | Request Body | User bank account number | string    | true     | 2560144400312  |
| beneficiaryName | Request Body | user bank account name   | string    | true     | Mary Li        |
| bankName        | Request Body | User bank name           | string    | true     | HSBC           |
| bankBranch      | Request Body | Bank branch name         | string    | true     | Beijing Branch |

## Paramount

### ParamountWithdrawal

`POST /api/paramount/withdrawal/process`

| Name             | Located in   | Description                                                            | Data Type | Required | Example                        |
|------------------|--------------|------------------------------------------------------------------------|-----------|----------|--------------------------------|
| securityQuestion | Request Body | A security question that the Consumer must answer to accept the payout | string    | true     | What is your favourite color? |
| securityAnswer   | Request Body | The answer associated with the securityQuestion                        | string    | true     | Purple                         |

## PaySec

### BankDeposit

`POST /api/bank/deposit/process`

No provider specific params required - [To general Bank request parameters](BankDeposit)

### PaySecWithdrawal

`POST /api/paysec/withdrawal/process`

| Name            | Located in   | Description             | Data Type | Required | Example                |
|-----------------|--------------|-------------------------|-----------|----------|------------------------|
| bankBranch      | Request Body | Name of the bank branch | string    | true     | Test bank branch       |
| accountNumber   | Request Body | Account number          | string    | true     | 6217852000016118245    |
| bankCode        | Request Body | Bank code               | string    | true     | BOC                    |
| bankName        | Request Body | Name of the bank        | string    | true     | BANK OF CHINA LIMITED  |
| bankAccountName | Request Body | Name of the account     | string    | true     | Test bank account name |

## Swish

### SwishDeposit

`POST /api/swish/deposit/process`

| Name        | Located in   | Description                              | Data Type | Required | Example     |
|-------------|--------------|------------------------------------------|-----------|----------|-------------|
| swishNumber | Request Body | Payer's phone number connected to Swish. | string    | true     | 46712345678 |

## Trustly

### TrustlyDeposit

`POST /api/trustly/deposit/process`

No provider specific params required - [To general Bank request parameters](BankDeposit)

### TrustlyWithdrawal

`POST /api/trustly/withdrawal/process`

No provider specific params required - [To general Bank request parameters](BankDeposit)

## Twint

### TwintDeposit

`POST /api/twint/deposit/process`

No provider specific params required - [To general Bank request parameters](BankDeposit)

## YuuPay

### YuuCollectDeposit

`POST /api/yuucollect/deposit/process`

No provider specific params required - [To general Bank request parameters](BankDeposit)

## BlixtPay

### BlixtPayWithdrawal

`POST /api/blixtpay/withdrawal/process`

| Name             | Located in   | Description                                          | Data Type | Required | Example    |
|------------------|--------------|------------------------------------------------------|-----------|----------|------------|
| userAccountId    | Request Body | Payer's account number in BlixtPay system.           | string    | true     | PdaNWxf4O  |
| beneficiaryName  | Request Body | Name of the account holder of the target account.    | string    | true     | Jane Doe   |
