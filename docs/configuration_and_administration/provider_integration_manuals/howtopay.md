--- 
id: "howtopay" 
title: "Howtopay"
hide_title: "true"
--- 

![](/img/providers/logos/howtopay.png)

# Howtopay

## About
Howtopay provides a reliable, easy to use and secure payment and billing solution. They assist Merchants to identify clients for KYC prior to connecting them to localised Payment and Billing solutions.

Current supported APM's via the Howtopay
- POLi
- iDEAL

| Provider Name                | Howtopay                                               |
|------------------------------|--------------------------------------------------------|
| Link                         | [https://www.howtopay.com/](https://www.howtopay.com/) |
| Classification               | Wallet                                                 |
| Regions                      | `International`                                        |
| Currencies                   | `EUR`, `AUD`                                           |
| Methods/PaymentTxTypes       | `HowtopayWalletDeposit`                                |
| PaymentIQ Configuration File | `HowtopayConfig`                                       |


## Configuration Information

<details>
<summary>Click to view example provider configuration</summary>
<br/>


```xml
<com.devcode.paymentiq.integration.howtopay.HowtopayConfig>
  <enabled>true</enabled>
  <accounts>
    
    <entry>
      <!-- E-wallet -->
      <string>IDEAL</string>
      <account>
        <supportedCurrencies>EUR</supportedCurrencies>
        <apiKey>?????-?????-???????-?????</apiKey>
      </account>
    </entry>
    
    <entry>
      <!-- E-wallet -->
      <string>POLI</string>
      <account>
        <supportedCurrencies>AUD</supportedCurrencies>
        <apiKey>?????-?????-???????-?????</apiKey>
      </account>
    </entry>
    
  </accounts>
  <defaultDescriptor>Bambora Payment</defaultDescriptor>
  <apiVersion>1.4</apiVersion>
</com.devcode.paymentiq.integration.howtopay.HowtopayConfig>
```
</details>

### Attributes

| Attribute  | Description                            |
|------------|----------------------------------------|
| apiVersion | Version of howtopay api (Default 1.4)  |
| apiKey     | Merchant API key (Api key in Howtopay) |

### Service mapping

When using a specific service with PaymentIQ and provider Howtopay the PaymentIQ service value should be provided in the frontend api service parameter.

| Payment method (Howtopay) | Service in PaymentIQ |
|---------------------------|----------------------|
| Poli                      | POLI                 |
| iDEAL                     | IDEAL                |

### Notifications

Currently Howtopay doesn't send a callback notification for failed payments (it might be added in near future), and due to this, merchants need to set cancel job to suite their approach to Hotopay payments as payments will be in WAITING_NOTIFICATION state. Howtopay recommend waiting minimum of 7 days before cancel pending payments.

| Environment | URL                                                                     |
|-------------|-------------------------------------------------------------------------|
| Test        | https://test-api.paymentiq.io/paymentiq/api/howtopay/callback/{txRefId} |
| Live        | https://api.paymentiq.io/paymentiq/api/howtopay/callback/{txRefId}      |

#### Duplicated tx
When using the ```POLi service``` then a user can do a double deposit on the same PaymentIQ tx id.
HowtoPay will send a notification with the new ```duplicated``` tx. This tx should be handled as a new tx. 
So PaymentIQ will create a new tx and will send authorize request in the integration-api with the new tx information (it will have the origin tx id as originTxId). 
The duplicated tx will have ```Received duplicate tx!``` in the info.


<details>
<summary>Click to view example MerchantCleanJobConfig</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.merchant.job.MerchantCleanJobConfig>
  <enabled>true</enabled>
  ....
  <entries>
    ....
    <cleanJobEntry>
      <type>HowtopayPayWalletDeposit</type>
      <psp>Howtopay</psp>
      <state>WAITING_INPUT</state>
      <removeAfterDays>14</removeAfterDays>
    </cleanJobEntry>
    ....
  </entries>
</com.devcode.paymentiq.integration.merchant.job.MerchantCleanJobConfig>
```

</details>

## Example Routing Rule

![](/img/providers/routing/howtopay.png)

## Transaction Flow

The Howtopay integration is a direct integration between PaymentIQ and Howtopay. No redirection are done. The user enter its account number in the cashier. The request will be sent to Howtopay that will respond with a notification when payment is successful at underlying payment method (POLi, iDEAL).

## Test Information

- iDEAL has to be tested with user country `NLD` and currency `EUR`.
- POLi has to be tested with user country `AUS` and currency `AUD`.
- Provide a random account number in the cashier.
