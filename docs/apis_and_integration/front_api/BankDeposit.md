---
id: "BankDeposit"
---

# Bank Deposit

`POST/api/bank/deposit/process`

## Request Body Parameters

| Name       | Located in   | Description                                    | Data Type | Required | Example    |
|------------|--------------|------------------------------------------------|-----------|----------|------------|
| service    | Request Body | Optional id of the bank/service.               | string    | false    | IDEAL      |
| nationalId | Request Body | Mandatory when using Directa24 Streamline API. | string    | false    | 19xxxxxx12 |
| bankName   | Request Body | Optional name of the bank to use.              | string    | false    | SEB        |
