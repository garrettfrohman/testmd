---
id: "CommunityBankDeposit"
---

# Community Bank Deposit

`POST/api/communitybank/deposit/process`

## Request Body Parameters

| Name     | Located in   | Description                                                                                | Data Type | Required | Example  |
|----------|--------------|--------------------------------------------------------------------------------------------|-----------|----------|----------|
| service  | Request Body | Optional id of the bank/service.                                                           | string    | false    | IDEAL    |
| bankCode | Request Body | Receivers bank code. If not included, the user will be redirected to the bank select page. | string    | false    | TRHBTR2A |
