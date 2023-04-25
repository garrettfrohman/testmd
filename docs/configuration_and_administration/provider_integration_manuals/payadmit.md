---
id: "payadmit"
title: "PayAdmit"
hide_title: "true"
---

![](/img/providers/logos/payadmit.png)

# PayAdmit

## About
PayAdmit is a payment provider offering 3DS Payment, full/partial Refund, Payout and Status Check.<br/>
Also the following Online Banking payment methods are supported:<br/>

`BASIC_CARD`, `FLEXEPIN`, `MACROPAY`, `SKRILL`, `PAYRETAILERS`, `LOCALPAYMENT`, `MONNET`, `PAYPAL`, `NETELLER`, `TRUSTPAYMENTS`, `PAYMAXIS`, `GATE8TRANSACT`, `TINK`, `B2BINPAY`, `B2BINPAYV2`, `CLICK`, `MONETIX`, `PERFECTMONEY`, `VOLT`, `KESSPAY`.

| Provider Name                | PayAdmit                                                                                   |
|------------------------------|--------------------------------------------------------------------------------------------|
| Link                         | [https://payadmit.com/](https://payadmit.com/)                                             |
| Classification               | Debit/Credit Card Processor, Online Banking                                                |
| Regions                      | All                                                                                        |
| Currencies                   | Please check directly with the provider regarding what currencies are supported            |
| Methods/PaymentTxTypes       | `CreditcardDeposit` <br/> `WebRedirectDeposit` <br/> `Refund` <br/> `CreditcardWithdrawal` |
| PaymentIQ Configuration File | `PayAdmitConfig`                                                                           |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.payadmit.PayAdmitConfig>
  <enabled>true</enabled>
  <useViqProxy>true</useViqProxy>
  <accounts>
    <entry>
      <string>DEFAULT</string>
      <account>
        <apiKey>??</apiKey>
        <method>??</method>
        <groupId>??</groupId>
        <useTokenId>false</useTokenId>
        <supportedCurrencies>USD|EUR|GBP|UAH</supportedCurrencies>
      </account>
    </entry>
  </accounts>
  <testMode>true</testMode>
  <container>window</container>
  <defaultDescriptor>Test Payment ${ptx.txRefId}</defaultDescriptor><!--Description of the transaction shown to the Customer-->
</com.devcode.paymentiq.integration.payadmit.PayAdmitConfig>
```

</details>

### Attributes

| Attribute                 | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
|---------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| account.apiKey            | Given by Provider and corresponds to the API Key that is used as **Authorization Bearer** request header.                                                                                                                                                                                                                                                                                                                                                                                    |
| account.method            | Corresponds to the payment method. For credit card operations it is set to `BASIC_CARD` by default. For online banking you can specify one of the following payment methods: `FLEXEPIN`, `MACROPAY`, `SKRILL`, `PAYRETAILERS`, `LOCALPAYMENT`, `MONNET`, `PAYPAL`, `NETELLER`, `TRUSTPAYMENTS`, `PAYMAXIS`, `GATE8TRANSACT`, `TINK`, `B2BINPAY`, `B2BINPAYV2`, `CLICK`, `MONETIX`, `PERFECTMONEY`, `VOLT`, `KESSPAY`.<br/>You can also specify payment method via `input.service` parameter. |
| account.groupId           | Identify the customer as belonging to a specific group that is used for routing. Optional.                                                                                                                                                                                                                                                                                                                                                                                                   |
| account.useTokenId        | It can be used to enable recurring. Optional.                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| account.defaultDescriptor | Can be used to define a transaction description shown to the customer                                                                                                                                                                                                                                                                                                                                                                                                                        |
| defaultDescriptor         | Can be used to define a transaction description shown to the customer                                                                                                                                                                                                                                                                                                                                                                                                                        |

### Configure credit card deposit and withdrawal

1). Add `PayAdmitConfig`
2). Add `PayAdmit` to the `<psps>...</psps>` section in the **MerchantConfig**
3). Add routing rules
4). Use `CreditcardDeposit` and `CreditcardWithdrawal` tx type.

### Enable Recurring

To start recurring you will need to make non-repeatable payment (initial) and `account.useTokenId` should be set to `true`.

### Configure Online Banking payment

1). Add `PayAdmitConfig`
2). Add `PayAdmit` to the `<psps>...</psps>` section in the **MerchantConfig**
3). Add routing rules
4). Use `WebRedirectDeposit` tx type
5). Configure payment method using `input.service` or `accountConfig.method`

## Example Routing Rules

Credit card operations:

![](/img/providers/routing/payadmit_cards.png)

Online Banking payment methods:

![](/img/providers/routing/payadmit_ob.png)

## Test Information

For a successful deposit in the sandbox environment, the amount should be less than 10000000. For test withdrawals and refunds, the limit is 10000.

| Card Number      | CVV | Expiry Mont | Expiry Year | Comment                                              |
|------------------|-----|-------------|-------------|------------------------------------------------------|
| 4000000000000002 | 010 | 01          | 2030        | 3D-Secure enrolled, successful authorization         |
| 4242424242424242 | 010 | 01          | 2030        | 3D-Secure enrolled, declined authorization           |
| 4000000000000408 | 010 | 01          | 2030        | Not enrolled for 3D-Secure, successful authorization |
| 4000000000000416 | 010 | 01          | 2030        | Not enrolled for 3D-Secure, declined authorization   |
