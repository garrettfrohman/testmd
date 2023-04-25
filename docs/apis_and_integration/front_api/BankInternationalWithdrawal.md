---
id: "BankInternationalWithdrawal"
---

# Bank International Withdrawal

`POST/api/bankintl/withdrawal/process`

## Request Body Parameters

| Name               | Located in   | Description                                                                                                                        | Data Type | Required | Example                |
|--------------------|--------------|------------------------------------------------------------------------------------------------------------------------------------|-----------|----------|------------------------|
| bic                | Request Body | BIC/SWIFT. 8 or 11 characters.                                                                                                     | string    | true     | 86012984628            |
| accountNumber      | Request Body | Target account number                                                                                                              | string    | true     | 123456789              |
| beneficiaryName    | Request Body | Name of the account holder of the target account. If not provided the user's first and last name will be used. 1 to 50 characters. | string    | false    | Jane Doe               |
| beneficiaryStreet  | Request Body | Address of the holder target account. If not provided the user's street will be used. 1 to 60 characters.                          | string    | false    | Main street 1          |
| beneficiaryZip     | Request Body | ZIP code of the holder target account. If not provided the user's ZIP code will be used. 1 to 16 characters.                       | string    | false    | 12345                  |
| beneficiaryCity    | Request Body | City of the holder target account. If not provided the user's city will be used. 1 to 60 characters.                               | string    | false    | Stockholm              |
| beneficiaryState   | Request Body | State of the holder target account. If not provided the user's state will be used. 1 to 60 characters.                             | string    | false    | Stockholm              |
| beneficiaryCountry | Request Body | Country of the holder target account. If not provided the user's country will be used. 1 to 60 characters.                         | string    | false    | Sweden                 |
| bankName           | Request Body | Name of the bank, not case sensitive. 1 to 50 characters.                                                                          | string    | false    | Swedbank               |
| branchName         | Request Body | Name of the branch, not case sensitive. 1 to 50 characters.                                                                        | string    | false    | Example branch name    |
| branchAddress      | Request Body | Address of the target bank branch receiving the payment. 1 to 250 characters.                                                      | string    | false    | Example branch address |
| branchCode         | Request Body | Branch code of the bank account.                                                                                                   | string    | false    | 1234567                |

