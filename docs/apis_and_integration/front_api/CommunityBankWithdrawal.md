---
id: "CommunityBankWithdrawal"
---

# Community Bank Withdrawal

`POST/api/communitybank/withdrawal/process`

## Request Body Parameters

| Name            | Located in   | Description                                                           | Data Type | Required | Example        |
|-----------------|--------------|-----------------------------------------------------------------------|-----------|----------|----------------|
| accountNumber   | Request Body | Target account number                                                 | string    | true     | 123456789      |
| beneficiaryName | Request Body | Name of the account holder of the target account.                     | string    | true     | Jane Doe       |
| bankCode        | Request Body | Receivers bank code                                                   | string    | true     | TRHBTR2A       |
| branchCode      | Request Body | Branch code of bank account - Also known as domestic bank identifier. | string    | false    | 012345         |
| nationalId      | Request Body | Social security number. Required for Brazil.                          | string    | false    | 000.000.000-00 |
| accountType     | Request Body | Type of account. Required for Brazil.                                 | string    | false    | 001            |
