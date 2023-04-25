--- 
id: "cleo"
title: "Cleo"
hide_title: "true"
---

![](/img/providers/logos/cleo.png)

# Cleo

## About
Cleo is a payment provider offering Payin, Payout and Status check.

Payin: WebRedirectDeposit or BankDeposit
Payout: BankDomesticWithdrawal

| Provider Name                | Cleo Payments                                                           |
|------------------------------|-------------------------------------------------------------------------|
| Link                         | [https://web.meetcleo.com/](https://web.meetcleo.com/)                  |
| Classification               | Online Banking;Mobile Banking;                                          |
| Regions                      | `Chile`                                                                 |
| Currencies                   | `CLP`                                                                   |
| Methods/PaymentTxTypes       | `BankDeposit` <br/> `WebRedirectDeposit` <br/> `BankDomesticWithdrawal` |
| PaymentIQ Configuration File | `CleoConfig`                                                            |

### Supported Amounts

- Minimum 5000 CLP payin
- Minimum 10000 CLP payout

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.cleo.CleoConfig>
  <enabled>true</enabled>
  <accounts>
    <entry>
      <string>???</string>
      <account>
        <supportedCurrencies>CLP</supportedCurrencies>
        <merchantId>???</merchantId>
        <apiKey>???</apiKey>
      </account>
    </entry>
  </accounts>
  <testMode>true</testMode>
</com.devcode.paymentiq.integration.cleo.CleoConfig>
```

</details>

### Attributes

| Attribute           | Description                                                              |
|---------------------|--------------------------------------------------------------------------|
| merchantId          | Corresponds to the Merchant ID at Cleo side. Should be provided by Cleo. |
| apiKey              | Corresponds to the API Key at Cleo side. Should be provided by Cleo.     |
| supportedCurrencies | Corresponds to Cleo supported currencies.                                |

## Provider Configuration

1. The above XML template (CleoConfig) will need to be added via backoffice Admin -> Configuration.
2. Routing needs to be added for both WebRedirect and BankDomesticWithdrawal in Routing -> Routing.

## Example Routing Rule
![](/img/providers/routing/cleo.png)

## Transaction Flow

1. The end user enters the transaction amount (and banking relevant information for banking withdrawals).
2. PaymentIQ sends the deposit/withdrawal request to Cleo.
3. Cleo responds with an initial status + a redirect url (for deposits) acknowledging they have received the PaymentIQ request and begin processing.
4. In case of deposit, the user is redirected in order to complete the payment.
5. Cleo sends back a callback notification once the transaction status has changed.

### Withdrawals

To use `BankDomesticWithdrawal` in the request (or PaymentIQ Cashier) you will need to provide account number, account type, bank name and rut, which rut means nationalId. A nationalId must be valid.
Merchant need to specify created services in MerchantConfig:
```xml
<serviceMapping>
    <entry>
        <string>BANKDOMESTIC</string>
        <string>CLEO</string>
    </entry>
</serviceMapping>
```

## Test Information

No information is entered for deposits, just amount which wanted to be deposited, it will just redirect to a page where you can choose to simulate a successful or failed transaction. For successful transactions, use "banco de prueba".

To use withdrawals, you need to provide your national ID(ex: 111111111), account number(ex: 88365484) , bank name and the type of your account should be choosen from dropdown.