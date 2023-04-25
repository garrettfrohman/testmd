--- 
id: "nodapay"
title: "Noda Pay"
hide_title: "true"
---

![](/img/providers/logos/nodapay.png)

# NodaPay

## About

| Provider Name                | Noda Pay                                                                                                 |
|------------------------------|----------------------------------------------------------------------------------------------------------|
| Link                         | [https://docs.noda.live/](https://docs.noda.live/)                                                       |
| Classification               | Debit/Credit Card Processor                                                                              |
| Regions                      | `EUROPE`, `UK`                                                                                           |
| Currencies                   | `EUR`, `GBP`                                                                                             |
| Methods/PaymentTxTypes       | `CreditCard Deposit` <br/> `CreditCard Withdrawal` <br/> `WebRedirectDeposit` <br/> `BankIbanWithdrawal` |
| PaymentIQ Configuration File | `NodaPayConfig`                                                                                          |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.nodapay.NodaPayConfig>
    <enabled>true</enabled>
    <testMode>true</testMode>
    <accounts>
        <entry>
            <string>???</string>
            <account>
                <supportedCurrencies>EUR|GBP</supportedCurrencies>
                <apiKey>???</apiKey>
                <secretKey>???</secretKey>
                <defaultDescriptor>???</defaultDescriptor>
                <storeId>???</storeId>
            </account>
        </entry>
    </accounts>
</com.devcode.paymentiq.integration.nodapay.NodaPayConfig>
```

</details>



### Attributes

| Attribute           | Description                                                              |
|---------------------|--------------------------------------------------------------------------|
| apiKey              | ApiKey provided by NodaPay                                               |
| secretKey           | Signature key provided by NodaPay used by PaymentIQ for security reasons |
| supportedCurrencies | NodaPay Supported Currencies                                             |
| defaultDescriptor   | Default payment descriptor                                               |
| storeId             | Merchant's shop id issued by NodaPay                                     |

### Request attributes

| Attribute  | Description                                                                               |
|------------|-------------------------------------------------------------------------------------------|
| providerId | Provided by the merchant either as part of the cashier URL or as part of the request body |

This attribute can be received from NodaPay and is optional. If provided, it will redirect the user to the specified bank.

Example for query parameter in cashier:
https://pay.paymentiq.io/cashier/develop/list-payment-methods?environment=???&merchantId=???&userId=???&attributes.providerId=???

Example for parameter in request body:
POST https://api.paymentiq.io/creditcard/deposit/process
```json
{
    "merchantId": "??",
    "amount": "??",
    "attributes": {
        "providerId": "??",
    },
  "sessionId": "??",
  "userId": "??",
...
}
```


## Provider Configuration

1. The above XML template (NodaPayConfig) will need to be added via backoffice Admin -> Configuration.
2. Routing needs to be added for both WebRedirect and BankIbanWithdrawal in Routing -> Routing.


## Example Routing Rules
![](/img/providers/routing/nodapay_webredirect.png)
![](/img/providers/routing/nodapay_withdrawal_iban.png)
![](/img/providers/routing/nodapay_creditcard_routing.png)

## Transaction Flow

1. The end user enters the transaction amount (and banking relevant information for banking withdrawals).
2. PaymentIQ sends the deposit/withdrawal request to NodaPay.
3. NodaPay responds with an initial status + a redirect url (for deposits) acknowledging they have received the PaymentIQ request and begin processing.
4. In case of deposit, the user is redirected in order to complete the payment.
5. NodaPay sends back a callback notification once the transaction status has changed.

## Test Information

### IBan Withdrawal

| IBAN                        | Expected Status |
|-----------------------------|-----------------|
| GB33BUKB20201555555555      | Done            |
| FR7630006000011234567890189 | Executing       |
| DE75512108001245126199      | Failed          |

### CreditCard Deposit

| Credit Card Number | CVV | Expected Flow               |
|--------------------|-----|-----------------------------|
| 4253258107133225   | 111 | No 3DS Authentication       |
| 4253258107133225   | 123 | 3DS Authentication Required |

### CreditCard Withdrawal

| Credit Card Number | Expected Status |
|--------------------|-----------------|
| 4111111111111111   | Done            |
| 4012888888881881   | Executing       |
| 5105105105105100   | Failed          |
