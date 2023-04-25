---
id: "statesandstatuscodes"
---

# Transaction States And Status Codes

## Introduction

PaymentIQ has 3 levels of status codes. The lowest is the individual status codes coming from the banks, acquirers, and other payment providers. These are unique per payment provider and in order to homogenise these, we have created internal status codes, which means the same regardless of payment provider.

Finally we have the transaction state which basically just indicates that the payment was successful, cancelled or failed. In this document you can see all of PaymentIQ’s status codes, and to which state they map.

## Transaction States

| State            | Description                                                                                                 |
|------------------|-------------------------------------------------------------------------------------------------------------|
| SUCCESSFUL       | Finalstate when the transaction was successfully processed.                                                 |
| REGISTERED       | The first state when a transaction is created.                                                              |
| PROCESSING       | State when the transaction is under processing.                                                             |
| WAITING_INPUT    | The transaction is awaiting input from the user.                                                            |
| WAITING_APPROVAL | State when waiting for manual approval, e.g. deposit or withdrawal is waiting for approval by the merchant. |
| FAILED           | The transaction has failed.                                                                                 |
| INCONSISTENT     | Critical error state that can happen after processing because the outcome is unknown, e.g. read time-out.   |
| CANCELLED        | The transaction has been cancelled, either by user, merchant or PSP.                                        |
| REPROCESSING     | State when the transaction is under processing of fallback.                                                 |



## Transaction Status and Status Descriptions

### Status codes 0-99 will trigger state SUCCESSFUL

| Code | Status                             | Description                                                         |
|------|------------------------------------|---------------------------------------------------------------------|
| 0    | SUCCESS                             | Everything is successful                                            |
| 1    | SUCCESS_WITHDRAWAL_APPROVAL         | A manually approves withdrawal which was successful                 |
| 2    | SUCCESS_WITHDRAWAL_AUTO_APPROVAL    | An automatically approved withdrawal which was successful           |
| 3    | SUCCESS_WAITING_CAPTURE             | A successful authorize transaction that is waiting for capture      |
| 4    | SUCCESS_WAITING_AUTO_CAPTURE        | A successful authorize transaction that is waiting for auto-capture |
| 5    | SUCCESS_AUTO_CAPTURED               | An authorize transaction that was auto-captured successfully        |
| 6    | SUCCESS_CAPTURED                    | An authorize transaction that was manually captured successfully    |
| 7    | SUCCESS_WAITING_CONFIRMATION        | A successful transaction that is waiting for confirm                |
| 50   | SUCCESS_3D_AUTH_ATTEMPT_REGD        | A successful 3D attempt. Not authenticated, but a proof of authentication attempt (Authentication Value) was generated|
| 51   | SUCCESS_3D_2_NOT_SUPPORTED_BY_ISSUER| A successful 3DS version 2 request, not supported by issuer (will fallback)|
| 52   | SUCCESS_3D_FRICTIONLESS             | A successful 3D authenticate with frictionless flow                   |
| 53   | SUCCESS_3D_CHALLENGED               | A successful 3D authenticate with challenge flow                      |
| 60   | SUCCESS_3D_1                        | A successful 3D v1                |
| 61   | SUCCESS_NON_3D                      | A successful NON 3D (Continue with non 3d for payment)                |

### Status code 100-199 will trigger state REGISTERED

| Code | Status            | Description                                               |
|------|-------------------|-----------------------------------------------------------|
| 100  | REGISTERED        | Request registered                                        |

### Status code 200-299 will trigger state PROCESSING

| Code | Status                         | Description                                                                                                                     |
|------|--------------------------------|---------------------------------------------------------------------------------------------------------------------------------|
| 200  | PROCESSING_PROVIDER            | Request is being processed by external provider (normally payment provider but it can also be a fraud provider or KYC provider) |
| 201  | PROCESSING_MERCHANT            | Request is being processed by merchant                                                                                          |
| 202  | CONT_WITH_N3DS                 | When possible from a liability perspective cont. with N3DS                                                                      |
| 203  | PROCESSING_USER_VERIFICATION   | Temporary status when PIQ does merchant verify user request                                                                     |
| 204  | PROCESSING_USER_AUTHORISATION  | Temporary status when PIQ does merchant authorise request                                                                       |
| 205  | PROCESSING_KYC_VERIFICATION    | Temporary status when PIQ processes KYC verification                                                                       |
| 206  | CONT_WITH_3D_1                 | Continuing with 3DS1                                                                       |
| 250  | REPROCESSING_PROVIDER          | Transaction is being processed by second payment provider                                                                       |
| 251  | REPROCESSING_MERCHANT          | Transaction sent again to merchant for processing                                                                               |

### Status code 300-349 will trigger state WAITING_INPUT

| Code | Status                           | Description                                                   |
|------|----------------------------------|---------------------------------------------------------------|
| 300  | WAITING_INPUT                    | Request processing, waiting on input from provider            |
| 301  | WAITING_3D_SECURE                | Waiting for 3D-secure check                                   |
| 302  | WAITING_DEPOSIT_CONFIRMATION     | When possible from a liability perspective continue with N3DS |
| 303  | WAITING_NOTIFICATION             | Waiting notification from payment provider                    |
| 304  | WAITING_WITHDRAWAL_CONFIRMATION  | Status which is used if PIQ receives a pending status for a withdrawal transaction. In this case and based on the configuration, PIQ can send a transfer request with pending status code to the merchant API|
| 305  | WAITING_KYC_VERIFICATION         | Waiting for KYC                                               |
| 306  | WAITING_MERCHANT_NOTIFICATION    | Waiting for notification from merchant                        |

### Status code 350-399 will trigger state WAITING_APPROVAL

| Code | Status                             | Description                                                |
|------|------------------------------------|------------------------------------------------------------|
| 350  | WAITING_DEPOSIT_APPROVAL           | Request processing                                         |
| 351  | WAITING_WITHDRAWAL_APPROVAL        | A withdrawal is waiting for approval                       |
| 352  | WAITING_DEPOSIT_AUTO_APPROVAL      | When possible from a liability perspective cont. with N3DS |
| 353  | WAITING_WITHDRAWAL_AUTO_APPROVAL   | A withdrawal is waiting for auto-approval                  |
| 354  | WAITING_DEPOSIT_ON_HOLD_APPROVAL   | A status which an agent can move an ongoing deposit into.  |
| 355  | WAITING_WITHDRAWAL_ON_HOLD_APPROVAL| A status which an agent can move an ongoing withdrawal into, e.g to prevent the approval in order to make a deep investigation of the user for instance KYC. If things were fine, the transaction can be moved to its original status to be approved later.|
| 356  | WAITING_WITHDRAWAL_SECOND_APPROVAL | A status that is used in case of activating second/two level approval through the approval rule settings.|

### Status code 400-499 will trigger state INCONSISTENT

| Code | Status                       | Description                                                    |
|------|------------------------------|----------------------------------------------------------------|
| 400  | ERR_READ_TIMEOUT             | Read timeout                                                   |
| 401  | ERR_REFERENCE_MISMATCH       | Response tx-ref-id doesn’t match the one sent                  |
| 402  | ERR_INCONSISTENT_TRANSACTION | The transaction is inconsistent, e.g. money was transferred from provider account, but failed to be transferred to user’s merchant account. It needs to be manually investigated             |
| 403  | ERR_UNKNOWN_CALLBACK         | The transaction is inconsistent, e.g. money was transferred to/from provider account, but failed to be transferred to user’s merchant account since PIQ didn’t recognize the callback. It needs to be manually investigated |
| 404  | ERR_IO_EXCEPTION             | An input/output error has occurred                             |
| 405  | ERR_UNKNOWN_RESPONSE         | The response could not be mapped to a specific code            |
| 406  | ERR_KAFKA_MESSAGE_NOT_SENT   | The Kafka message could not be sent                            |
| 407  | ERR_AMOUNT_MISMATCH          | Amount mismatch                                                |
| 408  | ERR_INVALID_SIGNATURE        | Invalid signature                                              |
| 409  | ERR_IP_NOT_WHITELISTED       | IP not whitelisted                                             |
| 410  | ERR_NAME_MISMATCH            | Name mismatch                                                  |
| 411  | ERR_INCONSISTENT_TOO_MANY_PSP_ACCOUNTS            |                                                 |
| 412  | ERR_INCONSISTENT_PSP_ACCOUNT_USED_BY_OTHER_USER   |                                                 |
| 413  | ERR_INCONSISTENT_BLOCKED_ACCOUNT                  |                                                 |

### Status code 500-599 will trigger state FAILED

| Code | Status                                           | Description                                                                                                                                                                       |
|------|--------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 500  | ERR_SYSTEM_ERROR                                 | Unknown system error.                                                                                                                                                             |
| 501  | ERR_FAILED_TO_CONNECT                            | Cannot connect to provider, e.g. invalid URL or network problem.                                                                                                                  |
| 502  | ERR_DECLINED_BAD_REQUEST                         | Declined because one or more request parameters are invalid.                                                                                                                      |
| 503  | ERR_DECLINED_FRAUD                               | Declined because of fraud or potential fraud                                                                                                                                      |
| 504  | ERR_DECLINED_NO_FUNDS                            | Declined because of insufficient funds.                                                                                                                                           |
| 505  | ERR_DECLINED_ACCOUNT_SUSPENDED                   | Declined because account is suspended or inactive.                                                                                                                                |
| 506  | ERR_DECLINED_OTHER_REASON                        | Declined because of other generic reason.                                                                                                                                         |
| 507  | ERR_DECLINED_CONTACT_SUPPORT                     | Transaction could not be completed. Notify user to contact support.                                                                                                               |
| 508  | ERR_DECLINED_CONFIG_ERROR                        | Declined because of system config error, not because of user input error. This normally means that the provider cannot be used because one or more config parameters are invalid. |
| 509  | ERR_NOT_AUTHENTICATED                            | Declined because user is not authenticated.                                                                                                                                       |
| 510  | ERR_INVALID_RESPONSE                             | Invalid HTTP response code, i.e. not 200.                                                                                                                                         |
| 511  | ERR_DECLINED_REQ_BLOCKED                         | Request is blocked for some reason, like residing in a not supported country, IP is blocked etc.                                                                                  |
| 512  | ERR_PSP_OUT_OF_SERVICE                           | Provider is temporarily out of service.                                                                                                                                           |
| 513  | ERR_DECLINED_NOT_AUTHORIZED                      | Transaction not authorized.                                                                                                                                                       |
| 514  | ERR_RESPONSE_CODE_UNKNOWN                        | Unknown error code received.                                                                                                                                                      |
| 515  | ERR_PSP_ACCOUNT_USED_BY_OTHER_USER               | PSP account already used by another user.                                                                                                                                         |
| 516  | ERR_PSP_ACCOUNT_NOT_USED                         | PSP account has not been used by user, e.g. the user has not made a deposit before a Withdrawal                                                                                   |
| 517  | ERR_TOO_MANY_PSP_ACCOUNTS                        | Too many registered PSP accounts registered for a user                                                                                                                            |
| 518  | ERR_DECLINED_DUPLICATE_TX_ID                     | Not a unique transaction ID. ID is already processed by PSP.                                                                                                                      |
| 519  | ERR_DECLINED_INVALID_ACCOUNT_NUMBER              | Invalid account number, e.g. invalid credit card number                                                                                                                           |
| 520  | ERR_MERCHANT_OUT_OF_SERVICE                      | Merchant is out of service.                                                                                                                                                       |
| 521  | ERR_DECLINED_LIMIT_OVERDRAWN                     | Limit overdrawn, e.g. weekly deposit exceeded.                                                                                                                                    |
| 522  | ERR_MERCHANT_RESPONSE_CODE_UNKNOWN               | Merchant returns an unknown error code on PIQ’s request.                                                                                                                          |
| 523  | ERR_DECLINED_NO_PROVIDER_FOUND                   | Declined, no provider can be found to process the transaction.                                                                                                                    |
| 524  | ERR_DECLINED_PROVIDER_ACCOUNT_CONFIG_ERROR       | Declined, provider account is missing or invalid in config.                                                                                                                       |
| 525  | ERR_MERCHANT_INVALID_RESPONSE                    | Unexpected response from Merchant.                                                                                                                                                |
| 526  | ERR_ABOVE_LIMIT								  | This is triggered when a transaction is above the Limits set in PIQ Rules > Limits. 																							  |
| 527  | ERR_BAD_REQUEST								  | Declined because one or more request parameters are invalid.																													  |
| 528  | ERR_BELOW_LIMIT								  | This is triggered when a transaction is below the Limits set in PIQ Rules > Limits. 																							  |
| 530  | ERR_DECLINED_BANK_REFUSAL						  | The users bank has declined the transaction for an unspecified reason. 																											  |
| 531  | ERR_DECLINED_CARD_EXPIRED						  | The card has expired. Usually only happens with saved cards. 																													  |
| 532  | ERR_DECLINED_CVV_FAIL							  |	The CVV entered by the user was wrong. 																																			  |
| 533  | ERR_DECLINED_EMAIL_BLACKLIST					  |	The user email is on a PSP blacklist. 																																			  |
| 534  | ERR_DECLINED_FRAUDRULE_PSP						  |	The transaction was blocked due to a fraud rule on the PSP. 																													  |
| 535  | ERR_DECLINED_INVALID_AMOUNT					  | Declined because the amount is invalid. 																																		  |
| 536  | ERR_DECLINED_INVALID_ISSUER					  | Declined because the Issuer of the card is invalid.																																  |
| 538  | ERR_DECLINED_ISSUER_UNAVAILABLE				  | The card issuer isn't responding to the authorisation request.																													  |
| 539  | ERR_DECLINED_LOST_OR_STOLEN					  | The card used has been reported lost or stolen. 																																  |
| 540  | ERR_DECLINED_RESTRICTED_CARD					  | The card is not allowed to be used for the transaction. 																														  |
| 541  | ERR_DECLINED_RESTRICTED_TERRITORY				  | The user country is not allowed to participate in the transaction. 																												  |
| 543  | ERR_DECLINED_VELOCITYRULE_PSP					  | The transaction was blocked due to a fraud rule on the PSP. 																													  |
| 544  | ERR_INVALID_PARAMETER							  | There is an invalid parameter that means the transaction was not sent to the PSP. 																								  |
| 545  | ERR_IO_EXCEPTION								  | There was a connection issue. 																																					  |
| 546  | ERR_RESPONSIBLE_GAMING_LIMIT					  | The user cannot make the transaction due to their responsible gaming limits. 																									  |
| 547  | ERR_USER_ACCOUNT_BLOCKED						  | The user account is blocked by the PSP. 																																		  |
| 548  | ERR_USER_SESSION_INVALID						  | The verifyUser request was declined. The user session is not valid.																												  |
| 550  | ERR_DECLINED_3D_VALIDATION_FAILED                | 3D secure validation failed.                                                                                                                                                      |
| 551  | ERR_DECLINED_3D_EXPIRED                          | 3D secure expired.                                                                                                                                                                |
| 553  | ERR_DECLINED_3D_AUTH_TECH_FAIL                   | 3D Authentication/Account Verification Could Not Be Performed; Technical or other problem|
| 554  | ERR_DECLINED_3D_AUTH_REJECTED                    | 3D Authentication/ Account Verification Rejected; Issuer is rejecting |
| 555  | ERR_DECLINED_3D_AUTH_USER_FAIL                   | 3D Not Authenticated/Account Not Verified; Transaction denied.  |
| 560  | ERR_VAULTIQ_OUT_OF_SERVICE                       | VaultIQ is not working.                                                                                                                                                           |
| 561  | ERR_DECLINED_IP_BLOCKED                          | Given when an IP block rule has declined a transaction.                                                                                                                           |
| 562  | ERR_DECLINED_BIN_BLOCKED                         | Given when a BIN block rule has declined a transaction.                                                                                                                           |
| 563  | ERR_VAULTIQ_UNKNOWN_ACCOUNT                      | VaultIQ is missing the account                                                                                                                                                    |
| 564  | ERR_DECLINED_KYC_BLOCK                           | Given when a KYC block rule has declined a transaction.                                                                                                                           |
| 565  | ERR_DECLINED_KYC_USER_UNDER_AGE                  | The ‘know your customer’ check failed because of user is under age.                                                                                                               |
| 566  | ERR_DECLINED_KYC_CHECK_FAILED                    | The ‘know your customer’ check failed.                                                                                                                                            |
| 567  | ERR_DECLINED_BIC_BLOCK                           | Given when a BIC block rule has declined a transaction.                                                                                                                           |
| 568  | ERR_DECLINED_EXPIRED                             | General expiration.                                                                                                                                                               |
| 569  | ERR_DECLINED_REPEAT_CANCELLED                    | A repeat payment that was cancelled                                                                                                                                               |
| 570  | ERR_DECLINED_CURRENCY_NOT_SUPPORTED              | The currency is not supported for this transaction.                                                                                                                               |
| 571  | ERR_DECLINED_FRAUD_SCORE_THRESHOLD_EXCEEDED      | Fraud score threshold exceeded.                                                                                                                                                   |
| 572  | ERR_DECLINED_MERCHANT_NOT_FOUND                  | The merchant was not found.                                                                                                                                                       |
| 573  | ERR_DECLINED_MERCHANT_NOT_ENABLED                | The merchant was not enabled.                                                                                                                                                     |
| 574  | ERR_DECLINED_PROVIDER_NOT_ENABLED                | The provider was not enabled.                                                                                                                                                     |
| 575  | ERR_DECLINED_UNDER_MAINTENANCE                   | The provider was under maintenance.                                                                                                                                               |
| 576  | ERR_NO_REFERRAL_TX_FOUND                         | No referral transaction was found.                                                                                                                                                |
| 577  | ERR_DECLINE_TX_NOT_FOUND                         | No transaction found.                                                                                                                                                             |
| 578  | ERR_DECLINE_COUNTRY_NOT_SUPPORTED                | The country is not supported by the provider.                                                                                                                                     |
| 579  | ERR_DECLINED_NOT_SUPPORTED_PAYMENT_METHOD_FRAUD  | Declined because of fraud or potential fraud.                                                                                                                                     |
| 580  | ERR_DECLINED_FRAUD_PROVIDER_ACCOUNT_CONFIG_ERROR | Declined fraud provider account is missing or invalid in config.                                                                                                                  |
| 581  | ERR_DECLINED_GENERAL_BLOCK                       | Given when a General block rule has declined a transaction.                                                                                                                       |
| 582  | ERR_DECLINED_3D_PROVIDER_ACCOUNT_CONFIG_ERROR    | 3DS provider account is missing or invalid in config|
| 583  | ERR_DECLINE_USER_NOT_FOUND                       | No user was found|
| 584  | ERR_DECLINE_NO_AMOUNTS                           | No amounts available|
| 585  | ERR_UNSUPPORTED_CHARACTERS                       | Unsupported characters |
| 586  | ERR_MESSAGE_SENT_TO_KAFKA_FAILED                 | Batch tx failed|
| 587  | ERR_DECLINED_3D_INIT_SYSTEM_ERROR                | 3DS init step failed |
| 588  | ERR_DECLINED_ID_VERIFICATION_FAILED              | Id verification failed|
| 589  | ERR_DECLINED_SCA_REQUIRED_BY_ISSUER              | SCA (3DS2) is required by issuer (soft decline)|
| 590  | ERR_DECLINED_MISSING_REDIRECT_URL                | |
| 591  | ERR_DECLINED_SCHEME_TOKEN_EXPIRED                | |
| 592  | ERR_DECLINED_INVALID_SCHEME_TOKEN                | |
| 593  | ERR_DECLINED_MERCHANT_NO_FUNDS                   | |
| 594  | ERR_DECLINED_NAME_MISMATCH                       | |
| 595  | ERR_DECLINED_WAITING_KYC_VERIFICATION            | |
| 596  | ERR_DECLINED_3D_AUTH_SYSTEM_ERROR                | 3DS auth step failed |
| 597  | ERR_DECLINED_DO_NOT_TRY_AGAIN                    | |

### Status code 600-699 will trigger state CANCELLED

| Code | Status                    | Description                                                                        |
|------|---------------------------|------------------------------------------------------------------------------------|
| 600  | ERR_CANCELLED_BY_USER     | Pending transaction being cancelled by user. Cancelled on a 3rd party side by user |
| 601  | ERR_CANCELLED_BY_MERCHANT | Pending transaction being cancelled by merchant                                    |
| 602  | ERR_CANCELLED_BY_PSP      | Pending transaction being cancelled by PSP                                         |
| 603  | ERR_NOT_SUPPORTED         |                                          |
