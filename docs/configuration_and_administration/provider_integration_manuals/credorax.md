--- 
id: "credorax" 
title: "Credorax"
hide_title: "true"
---
 
![](/img/providers/logos/credorax.png)

# Credorax

## About
Credorax is a creditcard processor with support for Deposits, Withdrawals, Refunds, Void, Capture.

| Provider Name                | Credorax                                                                                                                            |
|------------------------------|-------------------------------------------------------------------------------------------------------------------------------------|
| Link                         | [https://www.credorax.com](https://www.credorax.com)                                                                                |
| Classification               | Debit/Credit Card Processor                                                                                                         |
| Regions                      | `International`                                                                                                                     |
| Currencies                   | Please check directly with the provider regarding what currencies are supported                                                     |
| Methods/PaymentTxTypes       | `CreditcardDeposit`<br/>`CreditcardWithdrawal`<br/>`Refund`<br/>`Void`<br/>`Capture`<br/>`ApplePayDeposit`<br/>`ApplePayWithdrawal` |
| PaymentIQ Configuration File | `CredoraxConfig`                                                                                                                    |

## Configuration Information

### Attributes

| Attribute  | Description                                                                                                                                                                                                                 |
|------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| merchantId | Gateway MID                                                                                                                                                                                                                 |
| secretKey  | Signature Key                                                                                                                                                                                                               |
| authType   | If left blank or set to `AUTH_CAPTURE`, the deposit request will continue with a sale.<br/>If set to `FINAL_AUTH`, a capture request must be manually created.                                                              |
| useRefId   | This is an option to specify the intended operation for refunds, whether it is a payout or refund.<br/>If set to `true`, operation will be 34 (payout/ReferralCFT), if set to `false` it will be 5 (refund/ReferralCredit). |

### Withdrawals

In the account config, there are extra options that might be needed to set up withdrawals<br/>(this also applies when setting up ApplePay withdrawals). 

| Attribute      | Description                                                                                                                        |
|----------------|------------------------------------------------------------------------------------------------------------------------------------|
| useTokenId     | If not set or `false`, operation code 6 (independent credit), will be sent.<br/>If set to `true`, below attribute needs to be set. |
| withdrawalType | If `OCT`, Independent CFT code 35 will be sent.<br/>If `CFT`, code 34 (referral CFT) will be sent.                                 |

### Recurring payments

To flag a deposit as the first in a series of recurring transactions, add the tag `<cardOnFileType>INITIAL_RECURRING</cardOnFileType>` to a new provider account in the config and make sure to route against this specific account.

To flag a deposit as a subsequent recurring transaction, add the tag `<cardOnFileType>RECURRING</cardOnFileType>` to a new provider account in the config and make sure to route against this specific account when the transactions are initiated via the Admin API as a repeat deposit.

To flag a deposit as s unscheduled Card-on-File transaction initiated by the cardholder, add the tag `<cardOnFileType>CARDHOLDER_INITIATED</cardOnFileType>` to a new provider account in the config and make sure to route against this specific account.

### Credorax MPI retirement (2020-06-15)
Credorax will shut down their internal MPI which was used for 3DSv1. To continue using 3DSv1 as usual it needs to be configured to go through Ingenico's MPI. This is done by adding the following config variables on account level in CredoraxConfig:

```xml
<mpi>ig</mpi>
<merchantName>??</merchantName>
<merchantUrl>https://www.??.com</merchantUrl>
<merchantCountry>MT</merchantCountry>
<acquirerMerchantId>??</acquirerMerchantId>
<mpiPassword>??</mpiPassword>
```

| Attribute          | Description                                                                      |
|--------------------|----------------------------------------------------------------------------------|
| mpi                | Always "ig" for Ingenico's MPI                                                   |
| merchantName       | Merchant Name                                                                    |
| merchantUrl        | Merchant URL                                                                     |
| merchantCountry    | Two letter country code                                                          |
| acquirerMerchantId | Same as mpiMerchantId which can usually be found at the bottom of CredoraxConfig |
| mpiPassword        | Same as mpiPassword at bottom of config                                          |

**Note that to be able to use Apple Pay, merchants need to contact Credorax to setup a MID and configured it to support “no CVV” payments.**

### Dynamic descriptor

**From Credorax's documentation**: *The Dynamic Descriptor functionality allows the merchant to have a different descriptor displayed on the cardholder’s card statement with every transaction. This functionality requires your selected Payment Processor’s approval before using it.*

The value must be in format `Merchant DBA Name` + `*` + `City/Customer support number`, e.g Bambora*Stockholm.

To enable PIQ to send send this value to Credorax, first add `<sendDynamicDescriptor>true</sendDynamicDescriptor>` and then `<dynamicDescriptor>` to the CredoraxConfig with a correctly formatted value.

Example:

```xml
<sendDynamicDescriptor>true</sendDynamicDescriptor>
<dynamicDescriptor>Bambora*Stockholm</dynamicDescriptor>
```

## Example Routing Rule
![](/img/providers/routing/credorax.png)
![](/img/providers/routing/credorax2.png)

## Test Information

- Only test in currency EUR
- Amount: 50 for 3DS
- Please also make sure that the correct routing rule is set up. 


### N3DS

| Card Brand | Account          | CVV | Expiry date | description                  |
|------------|------------------|-----|-------------|------------------------------|
| VISA       | 4176661000001015 | 281 | 12/25       | Fully authenticated card     |
| VISA       | 4176661000001023 | 720 | 12/25       | Attempted authenticated card |
| VISA       | 4176661000001031 | 681 | 12/25       | Not enrolled card            |
| MASTERCARD | 5223450000000007 | 090 | 12/25       | Fully authenticated card     |
| MASTERCARD | 5223450000000015 | 353 | 12/25       | Attempted authenticated      |
| MASTERCARD | 5223450000002228 | 222 | 12/25       | Not enrolled card            |

### 3DS

| Card Brand | Account          | CVV | Expiry date     | description            |
|------------|------------------|-----|-----------------|------------------------|
| MASTERCARD | 5185520050000010 | Any | Any future date | Frictionless           |
| MASTERCARD | 5299910010000015 | Any | Any future date | Challenge (Y) OTP=1234 |
| MASTERCARD | 5455330200000016 | Any | Any future date | Challenge (R) OTP=9999 |
| MASTERCARD | 5455330200000099 | Any | Any future date | Challenge (A) OTP=4444 |

### 3DS2

Please use the link below for testing cards specific for Credorax.

[3DS2 Test Cards For Staging Environment](/../docs/configuration_and_administration/system_configuration/testcards3dsv2)