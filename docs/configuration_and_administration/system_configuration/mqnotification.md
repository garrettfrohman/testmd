---
id: "mqnotification"
---

# MQ Notifications

The MQ(Message Queue) notifications are another way to sent notifications(similar to email notifications). MQ notifications allows PaymentIQ to sent RabbitMQ messages to a Merchant's queue.

Setting up an MQ notification requires three steps:
1. Create a configuration file for the MQ notification
2. Create a template for the MQ notification
3. Create a rule for the MQ notification

These templates are generally composed in Json format, and may contain dynamic elements used to reflect the specifics of the transaction.

## Create a configuration file for the MQ notification

Merchants should have their own message queues. So, each merchant needs to create a **MQIntegrationConfig** file using the template on our template Merchant. Merchant needs to customize **MQIntegrationConfig** file with own the connection parameters to access their own Rabbit Queue.

See the following **MQIntegrationConfig** example:

```xml
<com.devcode.paymentiq.integration.message.mq.MQIntegrationConfig>
    <enabled>true</enabled>
    <mqProviders>
        <entry>
            <string>messageQueue1</string>
            <com.devcode.paymentiq.service.provider.ProviderAccountConfig>
                <service>rabbitMqProvider</service>
                <hosts>merchantQueueURL.com</hosts> <!-- Merchant should update according to their queue  -->
                <serviceEndpoint>merchantQueueURL.com</serviceEndpoint> <!-- Merchant should update according to their queue -->
                <username>usernameForAccessingTheMerchantQueue</username> <!-- Merchant should update according to their queue -->
                <password>passwordForAccessingTheMerchantQueue</password> <!-- Merchant should update according to their queue -->
                <exchange>merchant.exchange</exchange>  <!-- Merchant should update according to their queue -->
                <exchangeType>fanout</exchangeType>  <!-- Merchant should update according to their queue -->
                <durableExchange>true</durableExchange>  <!-- Merchant should update according to their queue -->
                <contentType>application/json</contentType>
                <port>5671</port> <!-- Merchant should update according to their queue, default is 5671 -->
                <tls>true</tls>
            </com.devcode.paymentiq.service.provider.ProviderAccountConfig>
        </entry>
        <entry>
            <string>messageQueue2</string>
            <com.devcode.paymentiq.service.provider.ProviderAccountConfig>
                <service>rabbitMqProvider</service>
                <hosts>merchantQueueURL2.com</hosts> <!-- Merchant should update according to their queue -->
                <serviceEndpoint>merchantQueueURL2.com</serviceEndpoint> <!-- Merchant should update according to their queue -->
                <username>username2ForAccessingTheMerchantQueue</username> <!-- Merchant should update according to their queue -->
                <password>password2ForAccessingTheMerchantQueue</password> <!-- Merchant should update according to their queue -->
                <exchange>merchant.exchange2</exchange>  <!-- Merchant should update according to their queue -->
                <exchangeType>direct</exchangeType>  <!-- Merchant should update according to their queue -->
                <durableExchange>true</durableExchange>  <!-- Merchant should update according to their queue -->
                <contentType>application/json</contentType>
                <port>5671</port> <!-- Merchant should update according to their queue, default is 5671 -->
                <tls>false</tls>
            </com.devcode.paymentiq.service.provider.ProviderAccountConfig>
        </entry>
    </mqProviders>
</com.devcode.paymentiq.integration.message.mq.MQIntegrationConfig>
```

## Create a template for the MQ notification

Message templates are typically composed of a text portion, along with dynamic parameters used to personalize the message, usually in Json format.

To create a new template navigate to **Admin/Templates/MQ** and click on **Add new template +** paste following template and save as **"testTemplate1"**.

See the following example for message body:

```javascript
{
  "account_holder_name" : \"${ptx.accountHolderName;json}\",
  "accumulated_currency" : \"${ptx.latestTxCmdMap.MerchantVerifyUserRes.attributes.Currency}\",
  "accumulated_deposits" : \"${ptx.latestTxCmdMap.MerchantVerifyUserRes.attributes.BalTurnover}\",
  "accumulated_withdrawals" : \"${ptx.latestTxCmdMap.MerchantVerifyUserRes.attributes.BalPayout}\",
  "amount" : \"${ptx.amount}\",
  "amount_base" : \"${ptx.amountBase}\",
  "balance" : \"${ptx.merchantUser.balance}\",
  "bank_name" :
    ${if ptx.latestTxCmdMap.BinBlockRes.issuerName}
      \"${ptx.latestTxCmdMap.BinBlockRes.issuerName}\",
    ${else}
      \"\",
    ${end}
  "blocked_account_reason": \"${ptx.blockedAccountReason;json}\",
  "bonuscode" : \"${ptx.bonusCode}\",
  "card_category" : \"${ptx.latestTxCmdMap.BinBlockRes.cardCategory}\",
  "card_type" : \"${ptx.latestTxCmdMap.BinBlockRes.cardBrand}\",
  "channel" : \"${ptx.channelId}\",
  "country" : \"${ptx.merchantUser.countryCode.twoAlphaCode}\",
  "created" : \"${ptx.created;date(yyyy-MM-dd'T'HH:mm:ssZ)}\",
  "deposit_type" : \"${ptx.depositType}\",
  "expiry_date" : \"${ptx.userPspAccountDetails.expiryDate;date(yyyy-MM-dd'T'HH:mm:ssZ)}\",
  "fee" : \"${ptx.fee}\",
  "fee_base" : \"${ptx.feeBase}\",
  "id" : ${ptx.id},
  "info" : \"${ptx.info;json}\",
  "initiated_provider" : \"${ptx.initiatedPsp}\",
  "initiated_provider_account" : \"${ptx.initiatedPspAccount}\",
  "ip_address" : \"${ptx.ipAddr}\",
  "ip_city" : \"${ptx.ipCity}\",
  "ip_country" : \"${ptx.ipCountry}\",
  "ip_region" : \"${ptx.ipRegion}\",
  "issuer_country" : \"${ptx.issuerCountry}\",
  "kyc_status" : \"${ptx.merchantUser.kycStatus}\",
  "language" : \"${ptx.merchantUser.locale}\",
  "masked_user_account" : \"${ptx.maskedUserAccount}\",
  "merchant_error_code" : \"${ptx.merchantErrCode}\",
  "merchant_tx_id" : \"${ptx.merchantTxId}\",
  "merchant_user_cat" : \"${ptx.merchantUserCat}\",
  "merchant_user_id" : \"${ptx.merchantUserId}\",
  "merchant_user_is_verified": \"${ptx.latestTxCmdMap.MerchantVerifyUserRes.attributes.AccountIsVerified}\",
  "provider" : \"${ptx.psp}\",
  "provider_account" : \"${ptx.pspAccount}\",
  "provider_type" : \"${ptx.txType.providerType}\",
  "psp_fee" : \"${ptx.pspFee}\",
  "psp_fee_base" : \"${ptx.pspFeeBase}\",
  "psp_fraud_score" : \"${ptx.pspFraudScore}\",
  "psp_reference_id" : \"${ptx.pspRefId}\",
  "psp_status_code" : \"${ptx.pspStatusCode}\",
  "psp_user_reference": \"${ptx.pspUserRef}\",
  "service" : \"${ptx.pspService}\",
  "state" : \"${ptx.state}\",
  "status_code": \"${ptx.statusCode}\",
  "suspected_abuse_reason": \"${ptx.suspectedAbuseReason;json}\",
  "tx_amount" : \"${ptx.txAmount}\",
  "tx_amount_base" : \"${ptx.txAmountBase}\",
  "tx_type" : \"${ptx.txType}\",
  "updated" : \"${ptx.lastUpdated;date(yyyy-MM-dd'T'HH:mm:ssZ)}\",
  "updated_by" : \"${ptx.updatedBy}\",
  "user_psp_account_holder" :
    ${if ptx.userPspAccountDetails.holder}
      \"${ptx.userPspAccountDetails.holder;json}\",
    ${else}
      \"\",
    ${end}
  "user_psp_account_id" : \"${ptx.userPspAccountId}\",
  "user_psp_account_provider_type" : \"${ptx.userPspAccountDetails.providerType}\",
  "user_psp_account_type" : \"${ptx.userPspAccountDetails.type}\",
  "user_psp_account_uuid" : \"${ptx.userPspAccountDetails.accountUuid}\"
}
```
Find other available dynamic tags in the [Email and MQ Parameters](emailparameters) chapter.

## Create a rule for the MQ notification

As, final step merchant should create a notification rule, so with that rule in place PaymentIQ can trigger notifications and sent MQ template to merchant's queue. 

Following image is a notification rule example which will send a message for every SUCCESSFUL and FAILED transaction state. 

![](/img/messagequeue/mq1.png)


## Example MQ Notification Result

As a result, PaymentIQ will send a message notification to merchant queue.

For example:
```json
{
    "account_holder_name" : "muhammet koprubasi",
    "accumulated_currency" : "",
    "accumulated_deposits" : "",
    "accumulated_withdrawals" : "",
    "amount" : "20.00 CAD",
    "amount_base" : "12.86 EUR",
    "balance" : "1000.00 CAD",
    "bank_name" : "",
    "blocked_account_reason": "",
    "bonuscode" : "",
    "card_category" : "",
    "card_type" : "",
    "channel" : "Windows",
    "country" : "SE",
    "created" : "2023-02-27T15:52:01+0100",
    "deposit_type" : "Standard",
    "expiry_date" : "2025-05-01T00:00:00+0200",
    "fee" : "0.00 CAD",
    "fee_base" : "0.00 EUR",
    "id" : 5072104,
    "info" : "Payneteasy: sale_3d_validating",
    "initiated_provider" : "Payneteasy",
    "initiated_provider_account" : "GMBP3DS",
    "ip_address" : "127.0.0.1",
    "ip_city" : "",
    "ip_country" : "",
    "ip_region" : "",
    "issuer_country" : "",
    "kyc_status" : "",
    "language" : "en_US",
    "masked_user_account" : "444444******4448",
    "merchant_error_code" : "",
    "merchant_tx_id" : "2b484202-54c2-453e-b866-452cdb4f334a",
    "merchant_user_cat" : "VIP",
    "merchant_user_id" : "payneteasyUser",
    "merchant_user_is_verified": "",
    "provider" : "Payneteasy",
    "provider_account" : "GMBP3DS",
    "provider_type" : "CREDITCARD",
    "psp_fee" : "",
    "psp_fee_base" : "",
    "psp_fraud_score" : "",
    "psp_reference_id" : "1779498",
    "psp_status_code" : "approved",
    "psp_user_reference": "",
    "service" : "",
    "state" : "SUCCESSFUL",
    "status_code": "SUCCESS",
    "suspected_abuse_reason": "",
    "tx_amount" : "20.00 CAD",
    "tx_amount_base" : "12.86 EUR",
    "tx_type" : "CreditcardDeposit",
    "updated" : "2023-02-27T15:52:09+0100",
    "updated_by" : "",
    "user_psp_account_holder" : "asdasdad asdasd",
    "user_psp_account_id" : "15",
    "user_psp_account_provider_type" : "CREDITCARD",
    "user_psp_account_type" : "CreditcardDeposit",
    "user_psp_account_uuid" : "0ad967c2-80c6-4e72-a12a-f24cc14a0d57"
}
```

