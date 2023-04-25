--- 
id: "loonio"
title: "Loonio"
hide_title: "true"
---

![](/img/providers/logos/loonio.png)

# Loonio (BankSend)

## About
Loonio (BankSend) is a payment provider offering Interac Payin, Interac Payout and Status check. 
Note: Inside PIQ Loonio operates under "BankSend"

| Provider Name                | Loonio / BankSend Payments                       |
|------------------------------|--------------------------------------------------|
| Link                         | [https://www.loonio.ca/](https://www.loonio.ca/) |
| Classification               | Online Banking                                   |
| Regions                      | `Canada`                                         |
| Currencies                   | `CAD`                                            |
| Methods/PaymentTxTypes       | `InteracDeposit` <br/> `InteracWithdrawal`       |
| PaymentIQ Configuration File | `BankSendConfig`                                 |

### Supported APMs (services)

| Payment Method               | TxType                            | Comment                                        |
|------------------------------|-----------------------------------|------------------------------------------------|
| Interac E-Transfer           | InteracDeposit, InteracWithdrawal | Differentiated by merchantId and merchantToken |
| Interac Online (Coming soon) | InteracDeposit, InteracWithdrawal | Differentiated by merchantId and merchantToken |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.banksend.BankSendConfig>
  <enabled>true</enabled>
  <accounts>
    <entry>
      <string>default</string>
      <account>
        <merchantId>???</merchantId>     <!-- MerchantID  -->
        <accessToken>???</accessToken>     <!--MerchantToken-->
        <supportedCurrencies>CAD</supportedCurrencies>
        <method>???</method> <!-- Type of transfer. Can be EFT, INTERAC, INTERAC_ETRANSFER, SMTP)-->
      </account>
    </entry>
  </accounts>
  <testMode>true</testMode>
  <container>window</container>  <!--iframe also supported by provider-->
</com.devcode.paymentiq.integration.banksend.BankSendConfig>
```

</details>

### Attributes

| Attribute           | Description                                                                                                                                                                             |
|---------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| merchantID          | Corresponds to the Merchant ID at Loonio/BankSend side. Should be provided by Loonio. MerchantId will differentiate which payment method is used, interac e-transfer or online interac. |
| accessToken         | Corresponds to the Merchant token at Loonio/BankSend side. Should be provided by Loonio.                                                                                                |
| supportedCurrencies | Corresponds to Loonio/BankSend supported currencies.                                                                                                                                    |
| method              | Corresponds to Loonio/BankSend supported types of transfer. It can be EFT, INTERAC, INTERAC_ETRANSFER, SMTP.                                                                            |

## Provider Configuration

1. The above XML template (BankSendConfig) will need to be added via backoffice Admin -> Configuration.
2. Routing needs to be added for both InteracDeposit and InteracWithdrawal in Routing -> Routing.

## Example Routing Rule

![](/img/providers/routing/loonio.png)

## Transaction Flow

1. The end user enters the transaction amount (and interac relevant information for both deposit and withdrawal transactions).
2. PaymentIQ sends the deposit/withdrawal request to Loonio/BankSend.
3. Loonio/BankSend responds with an initial status + a redirect url (for deposits) acknowledging they have received the PaymentIQ request and begin processing.
4. In case of deposit, the user is redirected in order to complete the payment.
5. Loonio/BankSend sends back a callback notification once the transaction status has changed.

## Test Information

To use `InteracWithdrawal` and `InteracDeposit` in the request (or PaymentIQ Cashier) you will need to provide a valid email and phone number.
