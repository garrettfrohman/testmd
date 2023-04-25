--- 
id: "readies" 
title: "READIES"
hide_title: "true"
---

![](/img/providers/logos/readies.png)

# READIES

## About
READIES is a simple online eVoucher that allows you to pay online safely and securely.

| Provider Name                | Readies                                      |
|------------------------------|----------------------------------------------|
| Link                         | [https://readies.biz/](https://readies.biz/) |
| Classification               | Aggregator                                   |
| Regions                      | `International`                              |
| Currencies                   | `EUR`, `GBP`, `HKD`, `GPY`, `TRY`, `USD`     |
| Methods/PaymentTxTypes       | WebRedirectDeposit                           |
| PaymentIQ Configuration File | ReadiesConfig                                |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.readies.ReadiesConfig>
  <enabled>true</enabled>
  <accounts>
    <entry>
      <string>default</string>
      <account>
        <accessToken>???</accessToken>
        <supportedCurrencies>???</supportedCurrencies>
      </account>
    </entry>
  </accounts>
</com.devcode.paymentiq.integration.readies.ReadiesConfig>
```
</details>

### Attributes

| Attribute           | Description                                         |
|---------------------|-----------------------------------------------------|
| accessToken         | Client's access token. Provided by Readies.         |
| supportedCurrencies | Supported currencies (EUR, GBP, HKD, GPY, TRY, USD) |

## Example Routing Rule
![](/img/providers/routing/readies_routing.png)

## Transaction Flow

1. User requests a deposit with the Readies WebRedirectDeposit method.
2. The PaymentIQ sends to Readies a request to generate payment. In the response PaymentIQ receives the payment-related data with the specific proceed url that will be used for the redirection.
3. Payment form redirects to the Readies payment page where the user may confirm the payment.
4. After payment completing user is redirected the payment success/failed screen.
5. When the user finishes the payment, the Readies updates the payment with transaction details. Readies sends a notification to the provided URL to update PaymentIQ. Upon receiving the notification PaymentIQ checks the transaction status and updates it. 


### Transaction flow diagram

![](/img/providers/readies_flow.png)

## Test Information

To generate test data (pin) proceed through the link https://testuser.readies.biz/buy-voucher?amount=5000&currencyCode=EUR. 

Enter test credit card details 4242 4242 4242 4242,

EXP: any future date, 

CVC: any 3 digit.
