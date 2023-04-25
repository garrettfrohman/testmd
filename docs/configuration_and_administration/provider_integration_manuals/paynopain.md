--- 
id: "paynopain" 
title: "PaynoPain / Paylands"
hide_title: "true"
---
 
![](/img/providers/logos/paynopain.png)

# PaynoPain / Paylands

## About
PaynoPain is a fintech company dedicated to research and technological development specialized in payment methods.

| Provider Name                | PaynoPain                                                                       |
|------------------------------|---------------------------------------------------------------------------------|
| Link                         | [https://paynopain.com](https://paynopain.com)                                  |
| Classification               | `Aggregator`                                                                    |
| Regions                      | `Spain`                                                                         |
| Currencies                   | Please check directly with the provider regarding what currencies are supported |
| Methods/PaymentTxTypes       | `WebRedirectDeposit`                                                            |
| PaymentIQ Configuration File | `PaynoPainConfig`                                                               |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.paynopain.PaynoPainConfig>
  <enabled>true</enabled>
  <accounts>
    <entry>
      <string>default</string>
      <account>
        <accessToken>?????</accessToken>
        <service>?????</service>
        <signature>?????</signature>
        <supportedCurrencies>EUR</supportedCurrencies>
      </account>
    </entry>
  </accounts>
</com.devcode.paymentiq.integration.paynopain.PaynoPainConfig>
```

</details>

### Attributes

| Attribute           | Description                                                                                        |
|---------------------|----------------------------------------------------------------------------------------------------|
| service             | Unique identifier (uuid) of the service which will be used for the payment. Provided by PaynoPain. |                   |
| accessToken         | Client's access token. Provided by PaynoPain.                                                      |
| signature           | Client's unique signature. Provided by PaynoPain.                                                  |
| supportedCurrencies | Supported currencies (`All`)                                                                       |

## Example Routing Rule

![](/img/providers/routing/paynopain.png)

## Transaction Flow

There are two possible methods for carrying out payments in PaynoPain: Redirection and WebService. 
Currently, the only Redirection is implemented, it covers WebRedirectDeposit payment method. 
Redirection works for Bizum payments (Bizum payment service).

### WebRedirectDeposit Flow
1. User requests a deposit with the PaynoPain WebRedirectDeposit method.
   
2. The PaymentIQ sends to PaynoPain a request to generate payment. In the response PaymentIQ receives the payment-related data with the specific token that will be used for the redirection.
   
3. Payment form redirects to the Bizum payment page where the user may confirm the payment. For this confirmation user should enter the phone number of user's account.
   ![](/img/providers/pnp_deposit_redirection.png)
   
4. After payment completing user Bizum  redirects the user to a payment success/failed screen.

5. When the user finishes the payment, the PaynoPain updates the payment with transaction details. PaynoPain sends a notification to the provided URL to update PaymentIQ. Upon receiving the notification PaymentIQ checks the transaction status and updates it. <br/>

###  Transaction Flow Diagram
![](/img/providers/paynopain_transaction_flow.png)

## Test Information

PaynoPain supports any type of currencies.

In the test environment successful and refused payments can be simulated by entering the following values 
when the payment process asks for the phone number:

Successful payment: 700000000 <br/>
Refused payment: ko@ko.ko <br/>

Note: for the successful payment amount should be less than 10. <br/>
