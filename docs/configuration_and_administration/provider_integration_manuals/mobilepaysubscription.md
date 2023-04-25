--- 
id: "mobilepaysubscription" 
title: "MobilePay Subscription"
hide_title: "true"
---
 
![](/img/providers/logos/mobilepay.png)

# MobilePay Subscription

## About
MobilePay Subscription allows businesses to create subscription agreements with the user through the MobilePay app. Once the agreement is accepted by the user, new subscription payments can be created without any involement of the user. The integration also supports "one-off payments" which is a method to create extra payments that are not a part of the agreement's amount or frequency.

| Provider Name                | MobilePay Subscription                                                                                        |
|------------------------------|---------------------------------------------------------------------------------------------------------------|
| Link                         | [https://developer.mobilepay.dk/subscriptions-main](https://developer.mobilepay.dk/subscriptions-main)        |
| Classification               | E-wallet / Banking                                                                                            |
| Regions                      | `Denmark`, `Finland`                                                                                          |
| Currencies                   | Please check directly with the provider regarding what currencies are supported                               |
| Methods/PaymentTxTypes       | `MobilePaySubscriptionAgreement`<br/> `MobilePaySubscriptionDeposit`<br/> `Refund`<br/> `Capture`<br/> `Void` |
| PaymentIQ Configuration File | -                                                                                                             |

### New Agreement
Deposits can only be made with an existing user account. If a deposit is initiated through the front-end API without an accountID, the agreement creation process will automatically start. If amount is 0, it will get TxType MobilePaySubscriptionAgreement. If amount > 0 a one-off payment will be made at the same time and TxType will be MobilePaySubscriptionDeposit.

### Subscription Payments
Subscription payments are done on an exisiting agreement without user interaction. They are made through the admin API method /repeat. Subscription payments always have a future due date when the money gets transfered (1-8 days in the future are the current requirements). Because of this the transaction will always have status WAITING_NOTIFICATION when initiated and change to status SUCCESS on the due date (usually around midnight). TxType will be MobilePaySubscriptionDeposit.

### One-off Payments
One-off payments are created through the front-end API, the same as when creating a new agreement. But a accountID must be included in the request body and amount must be greater than 0. TxType will be MobilePaySubscriptionDeposit.

### Capture
Capture must be done on one-off payments only.

### Void
Void can be done on one-off payments that are not yet captured.

### Refund
Refund can be done on successful subscription payments and on captured one-off payments.

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.mobilepaysub.MobilePaySubConfig>
  <enabled>true</enabled>
  <testMode>true</testMode>
  <authorizePassword>test123</authorizePassword>
  <accounts>
    <entry>
      <string>default</string>
      <account>
        <supportedCurrencies>DKK</supportedCurrencies>
        <plan>Test plan</plan>
        <frequency>MONTH</frequency>
        <merchantCountry>DK</merchantCountry>
        <accountID>cd7c3b5b-9ff2-4b76-b890-c00664615864</accountID>
        <agreementAmount>10</agreementAmount>
        <dueDateDaysInFuture>1</dueDateDaysInFuture>
      </account>
    </entry>
  </accounts>
</com.devcode.paymentiq.integration.mobilepaysub.MobilePaySubConfig>
```

</details>

### Attributes

| PaymentIQ Parameter     | Description                                                                                                                           | Required / Optional                                            |
|-------------------------|---------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------|
| accountID               | The subscription provider ID at MobilePay. See below for details on ow retreive this ID                                               | Required                                                       |
| agreementAmount         | Agreement amount, which will be displayed for the user in the MobilePay app                                                           | Optional                                                       |
| plan                    | Short Agreement information text, that will be displayed on the Agreement screen                                                      | Required                                                       |
| frequency               | Frequency of Payment Requests. See details below                                                                                      | Required                                                       |
| description             | Additional information provided by the merchant to the user, that will be displayed on the Agreement screen                           | Optional                                                       |
| merchantCountry         | Country code, DK or FI                                                                                                                | Required                                                       |
| dueDateDaysInFuture     | Subscription payment due date, number of days in future                                                                               | Optional, if not added here it must be sent as input attribute |
| nextPaymentDaysInFuture | Next Subscription Payment’s due date, to be shown to the user in the Agreement details                                                | Optional, can also be sent as input attribute                  |
| autoReserve             | Used for one-off payments. If set to true, MobilePay will attempt to automatically reserve the payment without user’s interaction     | Optional, defaults to false                                    |
| authorizePassword       | Used in the merchant authorization step. Can be set to anything. Must be the same as the {authorizePassword} in the authorization URL | Required                                                       |

### Merchant authorization
For PaymentIQ to have access to the MobilePay Subscription API on behalf of the merchant, an access token must be created. To create an access token follow the URL from the table below, replace {merchantId} with the real MID. You need to log in with the MobilePay credentials and grant the permissions. When finished, you will be redirected back to PaymentIQ which will just show the text "Success" if everything went fine and the access token was stored correctly.

| Environment | Authorization URL                                                                                            |
|-------------|--------------------------------------------------------------------------------------------------------------|
| TEST        | https://test-api.paymentiq.io/paymentiq/api/mobilepaysub/merchant/{merchantId}/authorize/{authorizePassword} |
| PROD        | https://api.paymentiq.io/paymentiq/api/mobilepaysub/merchant/{merchantId}/authorize/{authorizePassword}      |

### Subscription Provider ID
To find this ID you must log in to your MobilePay Subscriptions Admin account. Once logged in, select "Subscriptions" and click on the subscription that should be used. The ID is now visible in the web browser's address field as the last part (everything after /Edit/).

![](/img/providers/mobilepaysubscription01.png)
![](/img/providers/mobilepaysubscription02.png)

### Frequency
| Code       | Description             |
|------------|-------------------------|
| FLEXIBLE   | Flexible frequency      |
| YEAR       | Once a year             |
| SIX_MONTHS | Once every six months   |
| QUARTER    | Once every three months |
| MONTH      | Once a month            |
| TWO_WEEKS  | Once every two weeks    |

### Due Date / Next Payment Date
A due date must always exist when sending new subscription payments. This value can be configured in the account config as described above. The exact date can also be sent as an input attribute to PIQ. If the input attribute is available, it will have precedence over the configured value.

Next payment date is always optional. It can be configured in the account config or be sent as an input attribute in the same way as due date.

#### Example

```json
{
  "attributes": {
    "dueDate": "2019-06-05",
    "nextPaymentDate": "2019-07-05"
  },
  "userId": "test123",
  "accountId": "5dd8bf58-afae-4caa-88e1-2e3494626f4f",
  "amount": "10.00",
  "amountCy": "DKK"
}
```

## Example Routing Rule
![](/img/providers/routing/mobilepaysubscription.png)

## Test Information
There isn't a sandbox app for MobilePay. Instead, there is an API to simulate user interaction. When creating a new agreement, a phone number must be entered in the redirected iframe. Use a phone number from the test users below. The user also have an "Authenticated user id" connected to it, which is only used for the simulation API. This ID must be the same as the user that the agreement was created with.

### Test Users

| Authenticated user id                | Phone number  | Consumer name |
|--------------------------------------|---------------|---------------|
| f1a75bb4-c8a6-41f8-8603-4cf9278cd5ba | +4557373259   | Test name     |
| 4f474aa2-6161-4094-97fd-62616ff3d21e | +4599592431   | Test name     |
| d5e4e229-b482-4304-80f1-237d2a3abc48 | +4522509895   | Test name     |
| 40b881f7-ac3d-43bb-81e6-2ac9ef279d89 | +4554048573   | Test name     |
| 147a8bbd-6a87-40e7-9980-937d1b8d0de4 | +4585155935   | Test name     |
| 404f38dd-25dd-4683-831c-a85f1d25b64d | +358806041406 | FI Test name  |
| d5ae8716-4f28-49cc-926b-9667cdeed27a | +358806041436 | FI Test name  |
| 6b6c72bc-4a90-4cf7-ada1-c0318cc5404d | +358806041507 | FI Test name  |
| 04e1f1d4-47e1-4db9-8f0e-35b29e380890 | +358806041536 | FI Test name  |

### Test Merchant

Email: bamboratestmerchant@MobilePay.dk
Password: Useforconsentscreen1

### Simulation API

Use the endpoints below to simulate user interactions. The agreemntId is found in PIQ backoffice in the tab "User accounts", in the column "Account".

| Type                 | URL                                                                                                                                                                             | Method | Valid status values          |
|----------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------|------------------------------|
| Agreement            | <details><summary>Click to view URL</summary> <br/> `/api/mobilepaysubscription/simulate/{merchantId}/agreements/{agreementId}/userid/{authenticatedUserId}/{status}`</details> | POST   | Accepted, Rejected, Canceled |
| Subscription payment | <details><summary>Click to view URL</summary> <br/> `/api/mobilepaysubscription/simulate/payments/{txRefId}/userid/{authenticatedUserId}/{status}`</details>                    | POST   | Rejected                     |
| One-off payment      | <details><summary>Click to view URL</summary> <br/> `/api/mobilepaysubscription/simulate/payments/{txRefId}/userid/{authenticatedUserId}/{status}`</details>                    | POST   | Accepted, Rejected           |
