---
id: "BankRepeatWithdrawal"
---

# Bank Repeat Withdrawal

`POST/api/bank/withdrawal/process`

## Request Body Parameters

| Name      | Located in   | Description                                                                | Data Type | Required | Example                              |
|-----------|--------------|----------------------------------------------------------------------------|-----------|----------|--------------------------------------|
| accountId | Request Body | Account-id representing a Bank account used in a previous deposit by user. | string    | false    | d751d5e0-ebf6-44a2-84c4-e437a55b2cfc |
