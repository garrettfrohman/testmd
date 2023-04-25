--- 
id: "pagos360" 
title: "Pagos360"
hide_title: "true"
---
 
![](/img/providers/logos/pagos360.png)

# Pagos360

## About
Pagos360 is a fintech company that provides payment processing technology solutions for companies and organizations.

| Provider Name                | Pagos360                                             |
|------------------------------|------------------------------------------------------|
| Link                         | [https://www.pagos360.com](https://www.pagos360.com) |
| Classification               | `Aggregator`                                         |
| Regions                      | `Argentina`                                          |
| Currencies                   | 'ARS'                                                |
| Methods/PaymentTxTypes       | `WebRedirectDeposit`                                 |
| PaymentIQ Configuration File | `Pagos360Config`                                     |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.pagos360.Pagos360Config>
  <enabled>true</enabled>
  <accounts>
    <entry>
      <string>default</string>
      <account>
        <accessToken>???</accessToken>
        <defaultDescriptor>???</defaultDescriptor>
        <supportedCurrencies>ARS</supportedCurrencies>
        <merchantName>Test merchant</merchantName>
      </account>
    </entry>
  </accounts>
  <testMode>true</testMode>
</com.devcode.paymentiq.integration.pagos360.Pagos360Config>
```

</details>

### Attributes

| Attribute           | Description                                             |
|---------------------|---------------------------------------------------------|
| accessToken         | Client's access token. Is generated in Pagos360 account |
| defaultDescriptor   | Default payment description                             |
| supportedCurrencies | Supported currencies (`ARS`)                            |

## Example Routing Rule
![](/img/providers/routing/pagos360.png)
![](/img/providers/pagos360_pm.png)

## Transaction Flow
Integration consist of WebReditectDeposit method with the services that correspond subsequent requested payment methods: DEBIT_CARD, DEBIN (kind of bank wire), REDLINK, PAGO_FACIL(cash), PROVINCIA_NET(cash).

### Transaction flow diagram
![](/img/providers/pagos360_statuses.png)

### WebRedirectDeposit flow
1. User requests a deposit with the Pagos360 WebRedirectDeposit method using concrete service.
2. The PaymentIQ sends to Pagos360 a request to create payment. In the response PaymentIQ receives the url that will be used for the redirection.
3. For DEBIT_CARD, DEBIN, REDLINK user is redirected to the specific service where he should put required data to process the payment.
   For PAGO_FACIL, PROVINCIA_NET user is redirected to the page with the barcode coupon.
4. After completing the payment user may or may not be redirected to the payment success/pending screen.
5. When the user finishes the payment, the Pagos360 updates the payment with transaction details. Pagos360 sends a notification to the provided URL to update PaymentIQ. Upon receiving the notification PaymentIQ checks the transaction status and updates it. <br/>


## Test Information

### DEBIT_CARD

- Succesfull Payment Number: 4978260000000001 
- CVV: 123 
- Expires: 11/23


- Rejected Payment Number: 4978260000000002 
- CVV: 123 
- Expires: 11/23

### DEBIN

- Succesfull Payment Alias: ALIASPRUEBAUNO 
- CBU: 3220001805000046360015
- DNI: 36141047


- Canceled Payment Alias: ALIASPRUEBADOS 
- CBU: 0200325011000082202444
- DNI: 36141047


- Rejected Payment Alias: ALIASPRUEBATRES 
- CBU: 0200308311000080783312
- DNI: 36141047


- Expired Payment Alias: ALIASPRUEBACUATRO 
- CBU: 0440075240000169792934
- DNI: 36141047


- Could not be published Alias: ALIASPRUEBACINCO 
- CBU: 0200902911000030800430
- DNI: 36141047

### REDLINK

- Test credentials are not provided
