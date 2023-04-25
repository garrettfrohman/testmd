---
id: "emailparameters"
---

# Email and MQ Parameters

These are the available parameters one can use in the Alert, Notification emails and MQ notifications.

## Notifications

### Payment transaction values

| Parameter                             | Description                                                                             |
|---------------------------------------|-----------------------------------------------------------------------------------------|
| ```${ptx.merchantId}```               | MerchantId                                                                              |
| ```${ptx.id}```                       | TransactionId                                                                           |
| ```${ptx.merchantTxId}```             | MerchantTxId                                                                            |
| ```${ptx.txRefId}```                  | Transaction reference id (merchantId + A + transactionId)                               |
| ```${ptx.txType}```                   | Transaction type                                                                        |
| ```${ptx.txTypeInt}```                | Id representation of transaction type                                                   |
| ```${ptx.ipCountry}```                | IP country                                                                              |
| ```${ptx.created}```                  | Creation date time of the transaction                                                   |
| ```${ptx.state}```                    | State                                                                                   |
| ```${ptx.statusCode}```               | Status code                                                                             |
| ```${ptx.originTxId}```               | Origin transaction Id                                                                   |
| ```${ptx.merchantUserId}```           | Merchant user Id                                                                        |
| ```${ptx.merchantUserCat}```          | merchant user category                                                                  |
| ```${ptx.merchantAuthCode}```         | Merchant's authorization code                                                           |
| ```${ptx.merchantErrCode}```          | Merchant error code                                                                     |
| ```${ptx.maskedUserAccount}```        | User's masked account                                                                   |
| ```${ptx.info}```                     | Transaction and PSP status details                                                       |


### Payment money values

| Parameter                             | Description                                                                             |
|---------------------------------------|-----------------------------------------------------------------------------------------|
| ```${ptx.txAmount}```                 | Transaction amount                                                                      |
| ```${ptx.txAmountAbs}```              | Absolute transaction amount. Given a positive value and should be used for withdrawals. |
| ```${ptx.amount}```                   | Input amount                                                                            |
| ```${ptx.amountAbs}```                | Absolute input amount                                                                   |
| ```${ptx.txAmountBase}```             | Transaction base amount                                                                 |
| ```${ptx.amount.amount}```            | Base amount only                                                                        |
| ```${ptx.amount.currency}```          | Base amount currency only                                                               |
| ```${ptx.fee}```                      | Fee                                                                                     |


### Merchant user values

| Parameter                             | Description                                                                             |
|---------------------------------------|-----------------------------------------------------------------------------------------|
| ```${ptx.merchantUser.firstName}```   | First name                                                                              |
| ```${ptx.merchantUser.lastName}```    | Last name                                                                               |
| ```${ptx.merchantUser.userId}```      | User id                                                                                 |
| ```${ptx.merchantUser.dob}```         | Date of birth                                                                           |
| ```${ptx.merchantUser.sex}```         | Sex                                                                                     |
| ```${ptx.merchantUser.userCat}```     | User category                                                                           |
| ```${ptx.merchantUser.street}```      | Street                                                                                  |
| ```${ptx.merchantUser.zip}```         | Zip                                                                                     |
| ```${ptx.merchantUser.city}```        | City                                                                                    |
| ```${ptx.merchantUser.countryCode}``` | Country                                                                                 |
| ```${ptx.merchantUser.state}```       | State                                                                                   |
| ```${ptx.merchantUser.locale}```      | Locale                                                                                  |
| ```${ptx.merchantUser.email}```       | Email                                                                                   |
| ```${ptx.merchantUser.mobile}```      | Mobile                                                                                  |
| ```${ptx.merchantUser.kycStatus}```   | KYC Status                                                                              |
| ```${ptx.merchantUser.balance}```     | The user’s balance and balance currency                                                 |

## Alerts

| Parameter               | Description                                         |
|-------------------------|-----------------------------------------------------|
| ```${psp}```            | The defined PSP used in the rule.                   |
| ```${not_successful}``` | The amount of non-successful transactions.          |
| ```${total}```          | The total amount of transactions calculated.        |
| ```${threshold}```      | The defined threshold percentage used in the rule.  |
| ```${tx_type}```        | The defined Tx Type used in the rule.               |
| ```${psp_service}```    | The defined PSP Service used in the rule.           |
| ```${ALERT_DATE}```     | The time & date the alert was triggered.            |
| ```${unique_users}```   | The No. of unique users.                            |
| ```${minutes_back}```   | The No. of minutes of transactions queried.         |
| ```${percent_failed}``` | The percentage of failed transactions.              |
