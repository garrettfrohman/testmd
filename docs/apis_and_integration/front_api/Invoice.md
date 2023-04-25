---
id: "Invoice"
---

# Invoice

The below listed invoice providers all have some additional parameter that needs to be included in the request for the transaction to be successful.

If the invoice provider you are adding is not listed, it means only the standard parameters are required.

## Boku

### BokuDeposit

`POST /api/boku/deposit/process`

| Name        | Located in   | Description                                                                                                                                      | Data Type | Required | Example      |
|-------------|--------------|--------------------------------------------------------------------------------------------------------------------------------------------------|-----------|----------|--------------|
| phoneNumber | Request Body | User's phone number.                                                                                                                             | string    | true     | 446613123456 |
| serviceKey  | Request Body | A serviceKey corresponds to a particular serviceId in Boku. You can choose the name of this service independent from the name at Boku Dashboard. | string    | true     | UK 30 EUR    |

## Fonix

### FonixDeposit

`POST /api/fonix/deposit/process`

| Name        | Located in   | Description          | Data Type | Required | Example      |
|-------------|--------------|----------------------|-----------|----------|--------------|
| phoneNumber | Request Body | User's phone number. | string    | true     | 447554893154 |

## Fortumo

### FortumoDeposit

`POST /api/fortumo/deposit/process`

| Name        | Located in   | Description                                                                                                                                             | Data Type | Required | Example      |
|-------------|--------------|---------------------------------------------------------------------------------------------------------------------------------------------------------|-----------|----------|--------------|
| phoneNumber | Request Body | User's phone number. Only digits, no '+' sign.                                                                                                          | string    | true     | 346613123456 |
| servicePack | Request Body | A ServicePack corresponds to a particular serviceId in Fortumo. You can choose the name of this service independent from the name at Fortumo Dashboard. | string    | true     | UK 30        |

## Paylevo

### PaylevoDeposit

`POST /api/paylevo/deposit/process`

No provider specific params required - [To general request parameters](request)

## Seqr

### SeqrDeposit

`POST /api/seqr/deposit/process`

No provider specific params required - [To general request parameters](request)

### SeqrWithdrawal

`POST /api/seqr/withdrawal/process`

| Name      | Located in   | Description                                                               | Data Type | Required | Example                              |
|-----------|--------------|---------------------------------------------------------------------------|-----------|----------|--------------------------------------|
| accountId | Request Body | Account-id representing a Seqr account used in a previous deposit by user | string    | true     | d751d5e0-ebf6-44a2-84c4-e437a55b2cfc |

## A1

### A1Deposit

`POST /api/a1/deposit/process`

| Name        | Located in   | Description                                                                                 | Data Type | Required | Example       |
|-------------|--------------|---------------------------------------------------------------------------------------------|-----------|----------|---------------|
| phoneNumber | Request Body | User's phone number. If not included as input it will be taken from the verifyUser response | string    | false    | +359888123456 |
