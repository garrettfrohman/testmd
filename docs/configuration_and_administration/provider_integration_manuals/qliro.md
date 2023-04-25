--- 
id: "qliro" 
title: "Qliro"
hide_title: "true"
---
 
![](/img/providers/logos/qliro.png)

# Qliro

## About
Qliro is a invoice payment service that offers a simple, fast and secure "buy now, pay later" solution.

Qliro supports:
- Auth (Reservation).
- Capture and partial capture (Activation).
- Deposit (Reservation + Activation).
- Void (CancelReservation).
- Refund and partial refund (AlterInvoice).
- GetAddress.

Everyday for each merchant, a GetPaymentTypes API call will fetch the PaymentTypes available for that merchant.

| Provider Name                | Qliro                                                                           |
|------------------------------|---------------------------------------------------------------------------------|
| Link                         | [https://www.qliro.com/](https://www.qliro.com/)                                |
| Classification               | Invoice                                                                         |
| Regions                      | `Sweden`, `Finland`, `Denmark`, `Norway`                                        |
| Currencies                   | Please check directly with the provider regarding what currencies are supported |
| Methods/PaymentTxTypes       | `QliroDeposit`<br/>`Capture`<br/>`Void`<br/> `Refund`                           |
| PaymentIQ Configuration File | `QliroConfig`                                                                   |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.qliro.QliroConfig>
  <enabled>true</enabled>
  <accounts>
    <entry>
      <string>default</string>
      <account>
        <vatPercent>SE12</vatPercent>
        <merchantCountry>SWE</merchantCountry>
        <getPayerAddress>true</getPayerAddress>
        <username>??</username>
        <password>??</password>
        <merchantId>??</merchantId> <!-- Qliro clientRef -->
        <authType>AUTH_CAPTURE</authType>
        <!--  AUTH_CAPTURE Reservation + Activation 
              FINAL_AUTH just Reservation -->
        <supportedCurrencies>SEK|EUR|DKK|NOK</supportedCurrencies>
       <!-- 
       if method is removed or <method></method> or <method>.*</method> all methods will be shown.
       one can use | as or <method>300|500</method> and/or regex <method>300|7.*</method>
       to filter methods that can be shown.  -->
      </account>
    </entry>
  </accounts>
  <testMode>true</testMode>
</com.devcode.paymentiq.integration.qliro.QliroConfig>
```

</details>

For creating the invoice we need to pass the payer SSN + QliroPaymentTypeCode. QliroPaymentTypeCode is a 3 digit code representing different payment plans.  

In case that the input doesn't contain the QliroPaymentTypeCode, a page with suitable options will open for the payer to select payment type. Available options can be filtered by using the &#60;method> attribute in accountConfig.

When initiating QliroDeposit via the Admin API the QliroPaymentTypeCode must be included in the input.

### Account Config Attributes

| Attribute       | Description                                                                                                                                            |
|-----------------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| username        | Is provided by Qliro. This is the API username.                                                                                                        |
| password        | Is provided by Qliro. This is the API password.                                                                                                        |
| merchantId      | Is provided by Qliro. This is the clientRef. usually 3-digits.                                                                                         |
| merchantCountry | Country that account is corresponded to. Can be name of the country, 3-alpha CountryCode, 2-alpha CountryCode or 3-digit CountryCode.                  |
| vatPercent      | Check vatPercent table.                                                                                                                                |
| authType        | Set 'AUTH_CAPTURE' to have  Reservation + Activation or 'FINAL_AUTH' for just Reservation.                                                             |
| getPayerAddress | If “true”, will try to get billing address from Qliro.                                                                                                 |
| method          | If method is removed or empty or .* all methods will be shown. Use ´&#124;´ and/or regex to create filter like: &#60;method>300&#124;7.*&#60;/method>. |

### vatPercent

| Country | vatPercent                                                         |
|---------|--------------------------------------------------------------------|
| Sweden  | SE0, SE5, SE6, SE7, SE10, SE12, SE14, SE19, SE20, SE21, SE24, SE25 |
| Finland | FI0, FI5, FI6, FI7, FI10, FI12, FI14, FI19, FI20, FI21, FI24, FI25 |
| Denmark | DK0, DK5, DK 7, DK10, DK12, DK14, DK19, DK20, DK21, DK24, DK25     |
| Norway  | NO0, NO5, NO6, NO7, NO10, NO12, NO14, NO19, NO20, NO21, NO24, NO25 |

Config attribute:
endpointMap     A `<string, string>` map to map endpoints and countries if needed. Yet account serviceEndpoint and config serviceEndpoint have priority over this.

## Example Routing Rule
![](/img/providers/routing/qliro.png)

## Test Information

### Test accounts

- Currency: SEK
- User country: SWE
- Phone number: any
- SSN

| SSN          | State    |
|--------------|----------|
| 199212128426 | Approved |
| 197705301773 | OnHold   |
| 199012120110 | Denied   |

- (E.g TEST_SEK as mock user)
