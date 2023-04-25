---
id: "BankIBANWithdrawal"
---

# Bank IBAN Withdrawal

`POST/api/bankiban/withdrawal/process`

## Request Body Parameters

| Name            | Located in   | Description                                                                                                                                                                          | Data Type | Required | Example                |
|-----------------|--------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------|----------|------------------------|
| bankName        | Request Body | Name of the beneficiary's bank. 1 to 50 characters.                                                                                                                                  | string    | false    | Example Bank           |
| countryCode     | Request Body | Optional 2-letter, 3-letter, or 3-digit ISO country code which will be used to select clearing house. If not provided the user's country code will be used to select clearing house. | string    | false    | SWE                    |
| bic             | Request Body | BIC/SWIFT. 8 or 11 characters.                                                                                                                                                       | string    | true     | 86012984628            |
| iban            | Request Body | IBAN                                                                                                                                                                                 | string    | true     | DE44500105175407324931 |
| beneficiaryName | Request Body | Name of the account holder of the target account. If not provided the user's first and last name will be used. 1 to 50 characters.                                                   | string    | true     | Jane Doe               |
