---
id: "finshark"
title: "Finshark"
hide_title: "true"
---

![](/img/providers/logos/finshark.png)

# Finshark

## About

| Provider Name                | Finshark                                          |
|------------------------------|---------------------------------------------------|
| Link                         | [https://finshark.io/](https://finshark.io/)      |
| Classification               | Online Banking                                    |
| Regions                      | `SWE`, `DNK`, `NOR`, `FIN`                        |
| Currencies                   | `SEK`, `DKK`, `NOK`, `EUR`                        |
| Methods/PaymentTxTypes       | `BankDeposit`<br/>`BankWithdrawal`<br/>`Reversal` |
| PaymentIQ Configuration File | `FinsharkConfig`                                  |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.finshark.FinsharkConfig>
  <enabled>true</enabled>
  <container>window</container>
  <txHistoryDelayHours>0</txHistoryDelayHours>
  <accounts>
    <entry>
      <string>DEFAULT</string>
      <account>
        <supportedCurrencies>xxx|xxx|xxx|xxx</supportedCurrencies>
        <username>xxxxxxx</username>
        <password>xxxxxxx</password>
        <beneficiaryBank>xxxxxxxxxxx</beneficiaryBank>
      </account>
    </entry>
  </accounts>
</com.devcode.paymentiq.integration.finshark.FinsharkConfig>

```
</details>

### Attributes

| Attribute           | Description                                                                                                                                                                      |
|---------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| supportedCurrencies | Finshark supported currencies                                                                                                                                                    |
| username            | Client ID generated via [Finshark Portal](https://portal.finshark.io/)                                                                                                           |
| password            | Client Secret generated [Finshark Portal](https://portal.finshark.io/)                                                                                                           |
| beneficiaryBank     | Merchant IBAN                                                                                                                                                                    |
| txHistoryDelayHours | Configurable delay in hours. Successful deposits will be ignored if they have happened within the timeframe of (currentDate - txHistoryDelayHours). A value of 0 means no delay. |

### Notification/Callback setup

Callback/Notification URL can be set by the merchant using the [Finshark webhook API](https://oas.finshark.io/?_gl=1*pky66a*_ga*OTcxNDYxNzgzLjE2NjY3NzAwMjQ.*_ga_6KWZDPTZ17*MTY2OTI5NjU3OC41LjAuMTY2OTI5NjU3OC4wLjAuMA#tag/Webhooks/paths/~1v1~1Webhooks/post).
The authorization bearer token can be necessary for registering new webhooks can be obtained via the [Finshark Authorization API](https://oas.finshark.io/?_gl=1*pky66a*_ga*OTcxNDYxNzgzLjE2NjY3NzAwMjQ.*_ga_6KWZDPTZ17*MTY2OTI5NjU3OC41LjAuMTY2OTI5NjU3OC4wLjAuMA#section/Authentication)

Two webhooks <b><u>must</u></b> be created for each environment. One for payments and one for payouts.

### Notification/Callback setup for PaymentIQ production environment

```
curl --location --request POST 'https://api.finshark.io/v1/Webhooks' \
--header 'Authorization: Bearer xxxxxx' \
--header 'Content-Type: application/json' \
--data-raw '{
"event": "xxx",
"url": "xxxx"
}'
```

### Notification/Callback setup for PaymentIQ test environment

```
curl --location --request POST 'https://api.finshark.io/v1/Webhooks' \
--header 'Authorization: Bearer xxxxxx' \
--header 'Content-Type: application/json' \
--data-raw '{
"event": "xxx",
"url": "xxxx"
}'
```

### Callback URL & Params for PaymentIQ test environment

URL: `https://test-api.paymentiq.io/paymentiq/api/finshark/callback`
PAYMENT EVENT: `paymentStatusChanged`
PAYOUT EVENT: `payoutStatusChanged`
EVENT: `payoutStatusChanged`

### Callback URL & Params for PaymentIQ production environment

URL: `https://api.paymentiq.io/paymentiq/api/finshark/callback`
PAYMENT EVENT: `paymentStatusChanged`
PAYOUT EVENT: `payoutStatusChanged`

## Example Routing Rules

![](/img/providers/routing/finshark_routing.png)

## Transaction Flow

Deposit:
1. After successful deposit request to Finshark, the user is redirected to PSP Platform and the UI will guide them through the process.
2. Once the user has completed the Finshark flow, PaymentIQ will receive callback notifications regarding the payment status.

Withdrawal
1. Withdrawals can <b>only</b> be created if a successful deposit exists for this merchant and user combination
  After successful request to Finshark, PaymentIQ will receive notifications regarding the withdrawal status.

## Test Information

| IBAN                     | Expected Status Deposit | Expected Status Withdrawal |
|--------------------------|-------------------------|----------------------------|
| SE2550000000054400047903 | COMPLETED               | PROCESSED                  |
| DK6120301544118028       | COMPLETED               | PROCESSED                  |

Additional test date can be found at the [Finshark test documentation](https://docs.finshark.io/sandbox).
