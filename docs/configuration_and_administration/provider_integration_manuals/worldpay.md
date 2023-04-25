--- 
id: "worldpay" 
title: "WorldPay Corporate Gateway"
hide_title: "true"
---
 
![](/img/providers/logos/worldpay.png)

# WorldPay Corporate Gateway

## About
WorldPay is a credit card processor with support for Deposits and Withdrawals.

| Provider Name                | WorldPay                                                                                                                                                             |
|------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Link                         | [http://www.worldpay.com/](http://www.worldpay.com/)                                                                                                                 |
| Classification               | Debit/Credit Card Processor                                                                                                                                          |
| Regions                      | `International`                                                                                                                                                      |
| Currencies                   | `SEK`, `EUR`, `GBP`, and more                                                                                                                                        |
| Methods/PaymentTxTypes       | `CreditcardDeposit` <br/> `CreditcardWithdrawal` <br/> `IdealDeposit` <br/> `Refund` <br/> `Capture` <br/> `Void` <br/> `ApplePayDeposit` <br/> `ApplePayWithdrawal` |
| PaymentIQ Configuration File | `WorldPayConfig`                                                                                                                                                     |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.worldpay.WorldPayConfig>
  <enabled>true</enabled>
  <useViqProxy>true</useViqProxy>
  <height>600</height>
  <width>800</width>
  <pspCodeToStatusCode>
    <entry>
      <string>SENT_FOR_AUTHORISATION</string>
      <com.devcode.paymentiq.service.paymenttx.PaymentTxStatusCode>WAITING_NOTIFICATION</com.devcode.paymentiq.service.paymenttx.PaymentTxStatusCode>
    </entry>
  </pspCodeToStatusCode>
  <accounts>

    <entry>
      <string>3DS</string>
      <account>
        <serviceEndpoint>https://secure-test.worldpay.com/jsp/merchant/xml/paymentService.jsp</serviceEndpoint>
        <merchantCode>***********</merchantCode>
        <password>**********</password>
        <useTokenId>false</useTokenId>
        <use3Dsecure>true</use3Dsecure>
        <useAvs>true</useAvs>
        <!-- <overrideAdvice>do3DS</overrideAdvice>  If account is enabled for dynamic3DS. Possible values do3DS, no3DS -->
      </account>
    </entry>
    <entry>
      <string>N3DS</string>
      <account>
        <serviceEndpoint>https://secure-test.worldpay.com/jsp/merchant/xml/paymentService.jsp</serviceEndpoint>
        <merchantCode>>***********</merchantCode>
        <password>**********</password>
        <useTokenId>false</useTokenId>
        <use3Dsecure>false</use3Dsecure>
        <useAvs>true</useAvs>
        <!--The standing instruction for Merchant Initiated Transactions (MIT)
            Possible values: NA, REAUTH, UNSCHEDULED, DELAYED, INSTALMENT, INCREMENTAL, RECURRING, RESUBMISSION, NOSHOW
        <merchantInitiatedReason>UNSCHEDULED</merchantInitiatedReason>-->
      </account>
    </entry>    
    <!-- Specific account for performing Fast Funds payouts -->
    <entry>
      <string>FASTFUNDS</string>
      <account>
        <serviceEndpoint>https://secure-test.worldpay.com/jsp/merchant/xml/paymentService.jsp</serviceEndpoint>
        <merchantCode>*************</merchantCode>
        <password>**********</password>
        <useTokenId>false</useTokenId>
        <use3Dsecure>false</use3Dsecure>
        <useAvs>true</useAvs>
        <!-- Flag if a Fast Fund disbursement should be attempted-->
        <attemptFastFund>true</attemptFastFund>
      </account>
    </entry>
  </accounts>
  <description>Test order</description>
  <orderContent>Test</orderContent>
  <testMode>true</testMode>
</com.devcode.paymentiq.integration.worldpay.WorldPayConfig>
```
</details>

### Attributes

| Attribute                    | Description                                                                                                               |
|------------------------------|---------------------------------------------------------------------------------------------------------------------------|
| merchantCode                 | Corresponds to the `MerchantCode` value from WorldPay                                                                     |
| password                     | Corresponds to the `XML Password` value from WorldPay                                                                     |
| description                  | An optional order description specified by merchant.                                                                      |
| orderContent                 | Add (optional) additional description of purchased products/services in the request to WorldPay, supplied in HTML format. |
| attemptFastFund              | Set `true` to attempt a Fast Fund withdrawal                                                                              |
| useTokenId                   | When it is a repeat transaction and this is set to `true`, a "PayAsOrder" recurring payment will be attempted.            |
| locationRecipientDataEnabled | If set to true, address info will be sent to WorldPay in withdrawal requests                                              |


### Basic Deposit Payment Flow

By default the merchant account with WorldPay should be configured for automatically capturing the authorised transactions. This means that from the perspective of PaymentIQ, the merchant only does a regular credit card deposit which becomes successful as soon as we receive the 'AUTHORISED' response from WorldPay.

If the merchant wants to turn the WorldPay auto-capture off, it's possible to do the authorisation and capture in two separate steps from PaymentIQ. To enable this the provider account needs to have the tag `<authType>FINAL_AUTH</authType>`, which means that the initial credit card deposit is the authorise transaction, and then the authorise needs to be manually captured from the back office or via the Admin API, or have it automatically captured with Void / Capture rules.

:::warning Important! 

Do not enable `<authType>FINAL_AUTH</authType>` if the WorldPay account is set up for auto captures. Consult with your WorldPay account manager about how your account is set up.

:::

### Configuring the merchant account

Once access to the [WorldPay back office](https://secure.worldpay.com/sso/public/auth/login.html) has been received, the merchant account needs to be configured and then configured in PIQ WorldPayConfig.

![](/img/providers/worldpay_account.png)

1. Navigate to `Account`and `Profile`.
2. Check "Enable Original XML Username". This username should be added as the merchantCode in the WorldPayConfig.
3. Change the XML password. Make sure to follow all the instructions on the screen to complete the password change. This password should be added as the password in the WorldPayConfig.

### Fast Funds (Visa Direct)

Fast Funds makes it possible to quickly disburse funds to an end-user, meaning they'll receive the funds within 30 minutes. Fast Funds is currently only available for Visa payouts which is called Visa Direct. In order to tell PIQ to attempt a fast funds payout, following entry needs to be added to the WorldPay account config:

`<attemptFastFund>true</attemptFastFund>`

When this is enabled and the customer approves a withdrawal that is routed to this specific PSP account, a "card check" request will first be made against WorldPay. With this card check request, WorldPay will let us know if the issuing bank can process Fast Funds for this card. If it can process, PIQ will perform a "disbursement" request which is the Fast Fund payout. If the issuing bank does not support it, PIQ will decline the withdrawal attempt with status `ERR_DECLINED_RESTRICTED_CARD
` and info `Fast Funds not supported`. If the merchant wishes they can then do a fallback routing to a regular withdrawal attempt.

### Order Notifications

To correctly handle scenarios for timeouts and e.g PUSH_PENDING statuses that are later updated, the merchant must enable notifications in the [WorldPay back office](https://secure.worldpay.com/sso/public/auth/login.html) so that PaymentIQ gets updated with the transaction statuses correctly.

Once logged in:
1. Navigate to **Integration** > **Merchant Channel**.
2. In the Merchant Channels (Production), activate the **http** channel and select **xml** under **Content**.
3. Enter PIQ's callback URL `https://api.paymentiq.io/paymentiq/api/worldpay/callback` in **Address**.
4. Select **POST** under **METHOD**.

![](/img/providers/worldpay-merchant-channels.png)

You also need to mark which events should trigger a notification. This is done under Merchant **Channel Events (Production)** on the http row.

![](/img/providers/worldpay-merchant-channels2.png)

* Following events should be marked: **AUTHORIZED**, **ERROR**, **CANCELLED**, **CAPTURED**, **SENT_FOR_REFUND**.

* For Fast Funds the **PUSH_APPROVED** and **PUSH_REFUSED** events should be marked.

![](/img/providers/worldpay-merchant-channels3.png)

### Dynamic 3DS

With Dynamic 3D Secure (3DS) you can control the 'Mode of Operation', allowing you to choose when your customers are authorised. To use Dynamic 3DS, you as a merchant needs to make sure that it is enabled for the WorldPay account, please consult your WorldPay contact.

To override whether a 3DS should take place or not when Dynamic 3DS is enabled, the following tag should be added in the wanted account configuration in the WorldPayConfig in PaymentIQ back office:
`<overrideAdvice>do3DS</overrideAdvice>`

There are two possible values inside the tag:

| Value | Description                                                                    |
|-------|--------------------------------------------------------------------------------|
| do3DS | Perform 3D Secure for this order. Ignore any configured WorldPay rules.        |
| no3DS | Do not perform 3D Secure for this order. Ignore any configured WorldPay rules. |

### Merchant Initiated Transactions

It's possible to perform merchant initiated transactions through WorldPay by using the PaymentIQ Admin API and using the saved accountId generated from a previous cardholder initiated transaction. When doing this it's mandatory to send an initiated reason or "Standing instruction", basically explaining the reason behind it. By default, this is set to `UNSCHEDULED`, but the instruction can be changed with the tag `merchantInitiatedReason` inside the account config in the WorldPayConfig.

Example: `<merchantInitiatedReason>INSTALMENT</merchantInitiatedReason>`

The following are the available values to put inside the config tag:

| Merchant Initiated Reason | Description                                                                                                                                                                                                                                                                                                                                                                                                                                |
|---------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| INSTALMENT                | A single purchase of goods or services billed to a cardholder in multiple transactions, over a period of time agreed by the cardholder and you.                                                                                                                                                                                                                                                                                            |
| RECURRING                 | Transactions processed at fixed, regular intervals not to exceed one year between transactions, representing an agreement between a cardholder and you to purchase goods or services provided over a period of time.                                                                                                                                                                                                                       |
| UNSCHEDULED               | A transaction using a stored credential for a fixed or variable amount that does not occur on a scheduled or regularly occurring transaction date. This includes account top-ups triggered by balance thresholds.                                                                                                                                                                                                                          |
| REAUTH                    | Reauthorisation - a purchase made after the original purchase. A common scenario is delayed/split shipments.                                                                                                                                                                                                                                                                                                                               |
| DELAYED                   | A delayed charge is typically used in hotel, cruise lines and vehicle rental environments to perform a supplemental account charge after original services are rendered.                                                                                                                                                                                                                                                                   |
| INCREMENTAL               | An incremental authorisation is typically found in hotel and car rental environments, where the cardholder has agreed to pay for any service incurred during the duration of the contract. An incremental authorisation is where you need to seek authorisation of further funds in addition to what you have originally requested. A common scenario is additional services charged to the contract, such as extending a stay in a hotel. |
| RESUBMISSION              | When the original purchase occurred, but you were not able to get authorisation at the time the goods or services were provided. It should only be used where the goods or services have already been provided, but the post-event authorisation request is declined for insufficient funds.                                                                                                                                               |
| NOSHOW                    | A no-show is a transaction where you are enabled to charge for services which the cardholder entered into an agreement to purchase, but the cardholder did not meet the terms of the agreement.                                                                                                                                                                                                                                            |

## Example Routing Rule

![](/img/providers/routing/worldpay.png)

## Test Information

You can use the following card numbers to test transactions in the test environment only. When using test cards, you can specify an expiry date up to seven years in the future. The test cards do not have a card verification code and issue number.

Use cardholder name "3D" To invoke a simulated 3D secure transaction.

| Card Brand              | Account             | CVV | Expiry date |
|-------------------------|---------------------|-----|-------------|
| Airplus                 | 122000000000003     | Any | Any         |
| American Express        | 343434343434343     | Any | Any         |
| Cartebleue              | 5555555555554444    | Any | Any         |
| Dankort                 | 5019717010103742    | Any | Any         |
| Diners                  | 36700102000000      | Any | Any         |
| Diners                  | 36148900647913      | Any | Any         |
| Discover card           | 6011000400000000    | Any | Any         |
| JCB                     | 3528000700000000    | Any | Any         |
| Maestro                 | 6759649826438453    | Any | Any         |
| Mastercard              | 5555555555554444    | Any | Any         |
| Mastercard              | 5454545454545454    | Any | Any         |
| Mastercard Debit        | 5163613613613613    | Any | Any         |
| VISA                    | 4444333322221111    | Any | Any         |
| VISA                    | 4911830000000       | Any | Any         |
| VISA                    | 4917610000000000    | Any | Any         |
| Visa Debit              | 4462030000000000    | Any | Any         |
| Visa Debit              | 4917610000000000003 | Any | Any         |
| Visa Electron (UK only) | 4917300800000000    | Any | Any         |
| Visa Purchasing         | 4484070000000000    | Any | Any         |
