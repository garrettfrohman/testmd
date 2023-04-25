---
id: "BankLocalWithdrawal"
---

# Bank Local Withdrawal

`POST/api/banklocal/withdrawal/process`

## Request Body Parameters

| Name            | Located in   | Description                                                                                                                                                                          | Data Type | Required | Example        |
|-----------------|--------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------|----------|----------------|
| countryCode     | Request Body | Optional 2-letter, 3-letter, or 3-digit ISO country code which will be used to select clearing house. If not provided the user's country code will be used to select clearing house. | string    | false    | SWE            |
| clearingNumber  | Request Body | Target clearing number or bank code. 1 to 60 characters.                                                                                                                             | string    | true     | 12345          |
| accountNumber   | Request Body | Target account number. 1 to 120 characters.                                                                                                                                          | string    | true     | 123456789      |
| beneficiaryName | Request Body | Name of the account holder of the target account. If not provided the user's first and last name will be used. 1 to 50 characters.                                                   | string    | true     | Jane Doe       |
| bankName        | Request Body | Name of the bank, not case sensitive. 1 to 50 characters.                                                                                                                            | string    | false    | Swedbank       |
| branchName      | Request Body | Name of the bank branch. 1 to 50 characters.                                                                                                                                         | string    | false    | Example branch |
| accountName     | Request Body | Name of account. 1 to 50 characters.                                                                                                                                                 | string    | false    | My account     |
| accountType     | Request Body | Type of account. 1 to 50 characters.                                                                                                                                                 | string    | false    | Savings        |
