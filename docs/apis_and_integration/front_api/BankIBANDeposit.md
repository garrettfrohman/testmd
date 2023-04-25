---
id: "BankIBANDeposit"
---

# Bank IBAN Deposit

`POST/api/bankiban/deposit/process`

## Request Body Parameters

| Name     | Located in   | Description                          | Data Type | Required | Example                |
|----------|--------------|--------------------------------------|-----------|----------|------------------------|
| bic      | Request Body | BIC/SWIFT. 8 or 11 characters.       | string    | true     | 86012984628            |
| iban     | Request Body | IBAN                                 | string    | true     | DE44500105175407324931 |
| bankName | Request Body | Name of the bank, not case sensitive | string    | false    | Swedbank               |
