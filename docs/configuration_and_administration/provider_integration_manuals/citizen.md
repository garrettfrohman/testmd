--- 
id: "citizen"
title: "Citizen"
hide_title: "true"
---

![](/img/providers/logos/citizen.png)

# Citizen

## About
Citizen enables quick, cardless account-to-account payments.

| Provider Name                | Citizen                                                            |
|------------------------------|--------------------------------------------------------------------|
| Link                         | [https://www.paywithcitizen.com/](https://www.paywithcitizen.com/) |
| Classification               | Mobile Payment                                                     |
| Regions                      | `UK`,`NL`,`IE`,`NO`                                                |
| Currencies                   | `GBP`,`EUR`                                                        |
| Methods/PaymentTxTypes       | `CitizenDeposit` <br/> `CitizenWithdrawal`                         |
| PaymentIQ Configuration File | `CitizenConfig`                                                    |


## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.citizen.CitizenConfig>
  <enabled>true</enabled>
  <withdrawalQueue>true</withdrawalQueue>
  <currencyToPaymentGiroMapping>GBP->FPS, EUR->SEPA</currencyToPaymentGiroMapping>
  <accounts>
    <entry>
      <string>default</string>
      <account>
        <height>800</height>
        <pspPublicKey>Public API key</pspPublicKey>
        <pspPrivateKey>API key</pspPrivateKey>
        <payoutsPrivateKey>[-----BEGIN RSA PRIVATE KEY-----
            doufnvduifvndfiuvndufvndufnvidufnvduifnv
            dfovundofuvndifuvndifuvndiufvndiufnvdiuf
            soduncvdiufvndiufnvdiufnvdiufnvuidfnviud
          -----END RSA PRIVATE KEY-----</payoutsPrivateKey>
        <email>admin@example.com</email>
        <merchantBankCode>payout account bank code</merchantBankCode>
        <merchantAccountNumber>payout account number</merchantAccountNumber>
        <merchantId>merchant identifier</merchantId>
      </account>
    </entry>
  </accounts>
</com.devcode.paymentiq.integration.citizen.CitizenConfig>
```

</details>

### Attributes

| Attribute                    | Description                                                                                                                                                                                                                                                                  |
|------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| pspPublicKey                 | Called `Public API key` by Citizen                                                                                                                                                                                                                                           |
| pspPrivateKey                | Called `API Key` by Citizen                                                                                                                                                                                                                                                  |
| payoutsPrivateKey            | The private key for the key pair generated by the merchant when setting up payouts with Citizen. The public key is added to the Citizen backoffice.<br/>See [https://developers.citizen.is/#public-key-registration](https://developers.citizen.is/#public-key-registration) |
| email                        | The `Entity Email`, that is the email used to setup the merchant account with Citizen. It's visible in the Citizen backoffice.                                                                                                                                               |
| merchantBankCode             | Sort code of the merchant bank account that should be used for payouts                                                                                                                                                                                                       |
| merchantAccountNumber        | Account number of the merchant bank account that should be used for payouts                           <br/>                                                                                                                                                                  |
| withdrawalQueue              | This parameter is set to use Queued Payout feature. Once payout is created, it will be added to Citizen payout queue and once merchant approves/rejects it in PaymentIQ, it will be processed accordingly from the queue.                                                    |
| merchantId                   | Only applicable for Payout. (provided by Citizen provider)                                                                                                                                                                                                                   |
| currencyToPaymentGiroMapping | Payment type for specific currency (SEPA or FPS)                                                                                                                                                                                                                             |

### Layout
To ensure that the user can see the full Citizen ui after redirect, please use a minimum height of 800. See configuration example above.

## Webhooks

PaymentIQ callback URLs must be configured in the Citizen backoffice. Add the relevant URL from the table below and enable all webhook types for it.

| Environment | URL                                                          |
|-------------|--------------------------------------------------------------|
| Production  | https://api.paymentiq.io/paymentiq/api/citizen/callback      |
| Test        | https://test-api.paymentiq.io/paymentiq/api/citizen/callback |

## Example Routing Rule

![](/img/providers/routing/citizen.png)

## Transaction Flow

### Deposit
#### Mobile Journey
1. Select the Citizen payment method
2. Display a consent page with the details of the journey.
3. Verify new account or select an already verified account
4. The cashier is redirected after callback is received from Citizen

#### QR/Desktop Journey
1. Select the Citizen payment method and become redirected to Citizen
2. Display a QR code, scan it and continue with the journey.
3. Verify new account or select an already verified account
4. The cashier is redirected after callback is received from Citizen

### Withdrawal
1. Select the Citizen withdraw method
2. Display a consent page with the details of the journey.
3. Verify new account or select an already verified account
3. After successful withdrawal, it will be added to Citizen payout queue.
4. Once it is approved/rejected in PaymentIQ, queue will be processed accordingly.

## Test Information

Please check directly with the provider.