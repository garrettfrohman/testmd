---
id: "batch_processing"
---

# Batch Processing

## Introduction

Batch processing is used when merchant transaction flow isn't evenly spread.  It might be due to monthly subscriptions or back end systems that process requests in bulk. 

All initial transactions and tokenization of credit card data must be done in the normal e-commerce flow by the user doing an initial transaction or account verification. 

### Transaction type descriptions

| Transaction type            | PaymentIQ definition          | Description                                   |
|-----------------------------|-------------------------------|-----------------------------------------------|
| Debit transaction           | creditcardDeposit             | Card is debited or amount is reserved         |
| Credit transaction          | creditcardWithdrawal          | Card is credited                              |
| Account Verification        | creditcardAccountVerification | Check status of card, no money is transfered  |
| Capturing reservation       | capture                       | Debiting a reserved amount                    |
| Canceling reservation       | void                          | Reserved amount is released to account holder |
| Refunding debit transaction | refund                        | Reverses a debit transaction                  |
| Reversal transaction        | reversal                      | Reversal of a refund, restricted use          |
| Subscriptions               | repeat                        | For periodic transactions                     |

## How to generate the batches

The batches should be upload a CSV file to a SFTP where it will be fetched by us and processed.  The following response / response files will be generated.

### Request file

All kind kinds of transactions can be processed in the batch processing flow. Deposits/Purchases, Withdrawals/Credits, Refunds, Voiding. 

The request file is based on semicolon separated CSV files. All files will have the header description in the top row followed by the transaction request rows. 

#### Specifications request file

| Request params      | Type   | M/O | Description                                                                                                                     | Note                                                                                                         |
|---------------------|--------|-----|---------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------|
| merchantId          | string | M   | PaymentIQ MerchantID                                                                                                            |                                                                                                              |
| txId                | string | O   | Used for Capture, void, reversal and refund transactions to reference the debit transaction to capture, reverse, void or refund |                                                                                                              |
| merchantTxId        | string | M/O | Order id set by Merchant for reference to merchant order system                                                                 | For refunds, voids and captures, merchantTxId is inherited from the initial transaction                      |
| txType              | string | M   | creditcardDeposit, creditcardAccountVerification, capture, void, refund, repeat, creditcardWithdrawal                           |                                                                                                              |
| amount              | string | M   |                                                                                                                                 |                                                                                                              |
| amountCy            | string | M   | 3 digit ISO                                                                                                                     |                                                                                                              |
| country             | string | M   | 3 digit ISO                                                                                                                     |                                                                                                              |
| encCreditcardNumber | string | O   | Either this or accountId is required.                                                                                           | Merchant PCI environment is mandatory in order to generate new Deposits/Withdrawals or Account Verifications |
| expiryYear          | string | O   | Either this or accountId is required. Four digit expiry year of the credit card                                                 |                                                                                                              |
| expiryMonth         | string | O   | Either this or accountId is required. Two digit expiry month of the card [1-12]                                                 |                                                                                                              |
| userId              | string | M   | Merchant's end customer number / User ID                                                                                        |                                                                                                              |
| accountId           | string | O   | Returned in Account Verification or previous deposit/debit or withdrawal/credit transaction                                       |                                                                                                              |
| sessionId           | string | M   | Transaction series number. Should be unique per batch.                                                                          |                                                                                                              |
| attributes          | object | O   |                                                                                                                                 | JSON                                                                                                         |

 
#### Attributes

Attributes is used for some extra functionality and/or to be returned in the response file. Attributes is added in JSON, [http://en.wikipedia.org/wiki/JSON](http://en.wikipedia.org/wiki/JSON) format

```json
{
  "param1": "value1",
  "param2": "value2",
  "param3": {
    "param4": "value3",
    "param5": true
  }
}
```

#### Card Holder Names 

Card holder names can be sent as attributes

```json
{
  "firstName": "Kalle",
  "lastName": "Andersson"
}
```  
Format requirements for firstName and lastName values:

* Must be alphanumeric, that is only allowed characters are a-z, A-Z and 0-9 digits
* No space or hyphen characters are allowed
* The length of a name must not be larger than 35 characters 

### Response file

The following response-file will follow the request file with the same transaction listing as in the request file. 
The response file is based on semicolon separated CSV files. 

#### Specifications response file

| Response param | Example                               | Description                                                  |
|----------------|---------------------------------------|--------------------------------------------------------------|
| sessionId      | 12345                                 |                                                              |
| success        | FALSE                                 | TRUE or FALSE                                                |
| txState        | SUCCESSFUL                            |                                                              |
| statusCode     | SUCCESS                               |                                                              |
| responseCode   | ERR_GENERAL_DECLINE                   |                                                              |
| pspStatusCode  | 05                                    | If available, passed on from Issuer, provider or acquirer    |
| originTxId     | 3452225                               | Returned when doing refunds and voids                        |
| info           | Status 00 Successful                  |                                                              |
| merchantId     | 100000999                             |                                                              |
| txId           | 3452345                               | PaymentIQ transaction ID                                     |
| merchantTxId   | Order number 1000                     |                                                              |
| amount         | 100.00                                |                                                              |
| amountCy       | USD                                   |                                                              |
| country        | DEU                                   |                                                              |
| expiryYear     | 2025                                  |                                                              |
| expiryMonth    | 12                                    |                                                              |
| userId         | Customer1000                          |                                                              |
| accountId      | 76325f66b-9db0-4442-ae7f-d861231460b7 | Returned in Acount Verfication or previous debet transaction |
| attributes     | { "param1": "value1" }                | JSON                                                         |

#### Naming

| Directory  | Description                                     | Added File ending | Example                         |
|------------|-------------------------------------------------|-------------------|---------------------------------|
| /in        | Request files, Processing que                   | None              | /in/Batch1.csv                  |
| /processed | Successfully processed files                    | _processed        | /processed/Batch1_processed.csv |
| /failed    | Failed files                                    | _failed           | /failed/Batch1_failed.csv       |
| /response  | Response files for successfully processed files | _response         | /response/Batch1_response.csv   |
