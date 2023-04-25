--- 
id: "tolamobile" 
title: "TolaMobile"
hide_title: "true"
---
 
![](/img/providers/logos/tolamobile.png)

# TolaMobile

## About
TolaMobile is E-Wallet payment provider offering Deposit, Withdrawal and Status Check operations.

| Provider Name                | TolaMobile                                                                      |
|------------------------------|---------------------------------------------------------------------------------|
| Link                         | [https://www.tolamobile.com/](https://www.tolamobile.com/)                      |
| Classification               | Wallet                                                                          |
| Regions                      | Currently active in Ghana, Kenya, Uganda, Tanzania, Zambia, Malawi & Mozambique |
| Currencies                   | `GHS`, `KES`, `UGX`, `TZS`, `ZMW`, `MWK`, `MZN`                                 |
| Methods/PaymentTxTypes       | `TolaMobileDeposit`<br/>`TolaMobileWithdrawal`                                  |
| PaymentIQ Configuration File | `TolaMobileConfig`                                                              |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.tolamobile.TolaMobileConfig>
  <enabled>true</enabled>
  <useViqProxy>false</useViqProxy>
  <accounts>
    <entry>
      <string>TOLA</string>
      <account>
        <username>??</username>
        <password>??</password>
        <accountID>??</accountID>
        <secretKey>??</secretKey>
        <transactionChannel>??</transactionChannel>
        <supportedCurrencies>GHS</supportedCurrencies>
      </account>
    </entry>
  </accounts>
  <testMode>false</testMode>
  <defaultDescriptor>Bambora Mobile Payment</defaultDescriptor>
</com.devcode.paymentiq.integration.tolamobile.TolaMobileConfig>

```
</details>

### Attributes

| Attribute          | Description                                                                                                                                                                                                       |
|--------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| username           | Corresponds to **Username** from Tola. It is used to create Basic Authorization request header                                                                                                                    |
| password           | Corresponds to **Password** from Tola. It is used to create Basic Authorization request header                                                                                                                    |
| accountID          | Corresponds to **Target** of the transaction (e.g. Paybill). Paybill is basically user's account with the MNO (Mobile Network Operator)                                                                           |
| secretKey          | Corresponds to **Secret Key** from Tola. It is used to sign requests that are sent to Tola.                                                                                                                       |
| transactionChannel | A Channel is an identifier which is given to a mobile network operator, or Mobile Money supplier which offers connectivity to the Tola Wallet platform (e.g. GHANA.VODAFONE, GHANA.MTN, GHANA.AIRTEL, GHANA.TIGO) |

### Notes

- Please ask Tola to configure callback URLs:

| ENVIRONMENT | CALLABCK URL                                                    |
|-------------|-----------------------------------------------------------------|
| Test        | https://test-api.paymentiq.io/paymentiq/api/tolamobile/callback |
| Prod        | https://api.paymentiq.io/paymentiq/api/tolamobile/callback      |

- Ask Tola to set centile value for amount type

## Example Routing Rule

![](/img/providers/routing/tolamobile.png)

## Transaction Flow

When a charge request is sent to the MNO, they display a PIN on the users phone to confirm the charge (see PIN request message from Vodacom MZ mPesa below)

![](/img/providers/tolamobile01.png)

This is the receipt message from Vodacom MZ mPesa for the MZN 20 sent to the merchant

![](/img/providers/tolamobile02.png)

This is the message from Vodacom MZ mPesa confirming receipt of a Payout initiated by the merchant

![](/img/providers/tolamobile03.png)

## Test Information

Please use below test data to make a test payment

| Parameter                    | Value          |
|------------------------------|----------------|
| MSISDN                       | 233000000001   |
| accountID (target)           | 000010         |
| transactionChannel (channel) | GHANA.VODAFONE |
| Currency                     | GHS            |

