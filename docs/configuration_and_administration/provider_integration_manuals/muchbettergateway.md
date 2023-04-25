--- 
id: "muchbettergateway"
title: "MuchBetterGateway"
hide_title: "true"
---

![](/img/providers/logos/muchbettergateway.png)

# MuchBetter - MuchBetterGateway

## About

MuchBetterGateway is an aggregator provider supporting creditcard deposits, withdrawals and refunds.

MuchBetterGateway also supports the following alternative payment methods (APMs):

### International

Deposit: MuchBetter, CryptoPay

Withdrawal: MuchBetter

### Europe

Deposit: Sofort

### LATAM countries

Deposit: PIX

### Canada

Deposit: Interac

| Provider Name                | MuchBetterGateway                                                                                                                                                                                              |
|------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Link                         | [MuchBetterGateway Docs](https://goodlpay.atlassian.net/wiki/spaces/MMPUN/pages/3004235793/MuchBetter+Payment+Gateway)                                                                                         |
| Classification               | Aggregator                                                                                                                                                                                                     |
| Regions                      | `International`                                                                                                                                                                                                |
| Currencies                   | `USD`, `EUR`, `GBP`, `BRL`, `CHF`, `PLN`, `CNY`, `CAD`, `JPY`, `NOK`, `INR`, `ZAR`, `RUB`                                                                                                                      |
| Methods/PaymentTxTypes       | `CreditCardDeposit` <br/> `CreditCardWithdrawal` <br/> `MuchBetterDeposit` <br/>`MuchBetterWithdrawal` <br/> `SofortDeposit` <br/> `PixDeposit` <br/> `InteracDeposit` <br/> `CryptopayDeposit` <br/> `Refund` |
| PaymentIQ Configuration File | `MuchBetterGatewayConfig`                                                                                                                                                                                      |

### Supported APMs (services)

| Payment Method        | PaymentIQ Service | TxType               |
|-----------------------|-------------------|----------------------|
| MuchBetter Deposit    | MuchBetter        | MuchBetterDeposit    |
| MuchBetter Withdrawal | MuchBetter        | MuchBetterWithdrawal |
| Pix Deposit           | Pix               | PixDeposit           |
| Sofort Deposit        | Sofort            | SofortDeposit        |
| Interac Deposit       | Interac           | InteracDeposit       |
| Cryptopay Deposit     | Cryptopay         | CryptopayDeposit     |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.muchbettergateway.MuchBetterGatewayConfig>
    <enabled>true</enabled>
    <useViqProxy>true</useViqProxy>
    <accounts>
        <entry>
            <string>default</string>
            <account>
                <supportedCurrencies>USD|EUR|GBP|BRL|CHF|PLN|CNY|CAD|JPY|NOK|INR|ZAR|RUB</supportedCurrencies>
                <apiKey>???</apiKey>
                <secretKey>???</secretKey>
            </account>
        </entry>
    </accounts>
    <testMode>true</testMode>
</com.devcode.paymentiq.integration.muchbettergateway.MuchBetterGatewayConfig>
```

</details>

### Attributes

| Attribute           | Description                                                                                |
|---------------------|--------------------------------------------------------------------------------------------|
| supportedCurrencies | Currencies supported by MuchBetterGateway.                                                 |
| apiKey              | API key provided by MuchBetter. It is used to Authorize requests sent to their API.        |
| secretKey           | Signature key provided by MuchBetter, used to validate the contents of a request/response. |

### Provider Configuration

To be able to test the MuchBetterGateway Api you need to contact MuchBetter to request the following:
1. Request production API Key and Secret Key. Those need to be placed in the merchant config as described above.
2. Request MuchBetterGateway to whitelist PaymentIQ server IP.
3. Request callback URL to be set in provider backoffice: <br/>
    Test: https://test-api.paymentiq.io/paymentiq/api/muchbettergateway/callback/ <br/>
    Prod: https://api.paymentiq.io/paymentiq/api/muchbettergateway/callback/
4. Create Routing Rule

## Example Routing Rule

![MuchBetterGateway CreditCard Routing](/img/providers/routing/muchbettergateway.png)

## Transaction Flow

1. The end user enters the transaction amount (and creditcard or APM specific information).
2. PaymentIQ sends the payment request to MuchBetterGateway.
3. MuchBetterGateway responds with an initial status + a redirect url (URL not needed in case of refund).
4. The user is redirected in order to complete authentication.
5. MuchBetterGateway sends back notification once the transaction status has changed.
                                                                                      
## Test Information

There are no limitations on the data you can use for testing as long as it is valid.

Currently, there is no way to test MuchBetter withdrawals on staging.