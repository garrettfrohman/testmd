--- 
id: "macropay" 
title: "MacroPay"
hide_title: "true"
---
 
![](/img/providers/logos/macropay.png)

# MacroPay

## About
MacroPay is a payment processor offering deposit and status check operations.

- Macropay Gateway, which makes use of the transaction types `WebRedirectDeposit`, `IdealDeposit`, `GiropayDeposit`, `SofortDeposit`, `EpsDeposit`, `TrustlyDeposit`, `BoletoBancarioDeposit`.

Current supported APM's via the Macropay Gateway:
- POLi
- iDEAL
- Sofort
- Giropay
- Trustly
- EPS
- Bancontact
- Boleto Bancario
- Multibanco
- Open Banking

| Provider Name                | MacroPay                                                                                                                         |
|------------------------------|----------------------------------------------------------------------------------------------------------------------------------|
| Link                         | [http://macropay.net/](http://macropay.net/)                                                                                     |
| Classification               | Wallet, Aggregator                                                                                                               |
| Regions                      | International                                                                                                                    |
| Currencies                   | Please check directly with the provider regarding what currencies are supported                                                  |
| Methods/PaymentTxTypes       | `WebRedirectDeposit`, `IdealDeposit`, `GiropayDeposit`, `SofortDeposit`, `EpsDeposit`, `TrustlyDeposit`, `BoletoBancarioDeposit` |
| PaymentIQ Configuration File | `MacroPayConfig`                                                                                                                 |
| Limits                       | POLi - 1000 AUD, iDEAL - 3000 EUR                                                                                                |

### Howtopay.com

The howtopay integration is now a separated psp called `Howtopay`. The documentation can be found [here](/docs/configuration_and_administration/provider_integration_manuals/howtopay) and the old `MacroPayWalletDeposit` api will be decommission in a near future.

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.macropay.MacroPayConfig>
  <enabled>true</enabled>
  <accounts>
    <entry>
      <string>AGGREGATOR</string>
      <account>
        <supportedCurrencies>AUD|EUR|NZD|USD</supportedCurrencies>
        <accountID>*********</accountID><!-- Merchant API-ID -->
        <password>********-****-****-****-********</password><!-- Merchant API-GUID -->
        <notificationSecret>*********</notificationSecret><!-- Shared Key -->
      </account>
    </entry>
    <entry>
      <string>AGGREGATOR-SOFORT</string>
      <account>
        <supportedCurrencies>AUD|EUR|NZD|USD</supportedCurrencies>
        <accountID>*********</accountID><!-- Merchant API-ID -->
        <password>********-****-****-****-********</password><!-- Merchant API-GUID -->
        <notificationSecret>*********</notificationSecret><!-- Shared Key -->
        <container>window</container>
      </account>
    </entry>
  </accounts>
  <defaultDescriptor>Bambora Payment</defaultDescriptor>
</com.devcode.paymentiq.integration.macropay.MacroPayConfig>
```
</details>

### Attributes

| Attribute          | Description                                                                |
|--------------------|----------------------------------------------------------------------------|
| accountID          | Merchant API-ID (provided by MacroPay)                                     |
| username           | Merchant API-GUID (provided by MacroPay)                                   |
| notificationSecret | Shared Key (provided by MacroPay)                                          |
| merchantUrl        | Set to the value that should be sent as "source_url" to MacroPay. Optional |
| merchantIp         | Set to the value that should be sent as "source_ip" to MacroPay. Optional  |

### Important Information
- Currently MacroPay E-wallet doesn't send a callback notification for failed payments (it might be added in near future), and due to this, merchants need to set cancel job to suite their approach to MacroPay payments as payments will be in WAITING_NOTIFICATION state.
- Certain APM's such as Sofort has to be handled as a new window in the redirection, as opposed to the standard iframe container. Therefore it is necessary to create separate account configurations within the `MacroPayConfig` for these APM's. Setting the following tag inside the account will make sure it opens in a new window: `<container>window</container>`.

### Duplicated tx
When using the ```POLi service``` then a user can do a double deposit on the same PaymentIQ tx id.
MacroPay will send a notification with the new ```duplicated``` tx. This tx should be handled as a new tx. 
So PaymentIQ will create a new tx and will send authorize request in the integration-api with the new tx information (it will have the origin tx id as originTxId). 
The duplicated tx will have ```Received duplicate tx!``` in the info.

## Additional Information

### Macropay Gateway

When using the Macropay Gateway solution the general transaction type to use is `WebRedirectDeposit` with the correct service value, however there are exceptions and alternatives which is described below.

#### APM's that can only be used with `WebRedirectDeposit`
| APM name     | service value |
|--------------|---------------|
| POLi         | POLI          |
| Bancontact   | BANCONTACT    |
| Multibanco   | MULTIBANCO    |
| Open Banking | OP            |

#### APM's that can be used with both `WebRedirectDeposit` and its specific deposit type
| APM name | service value | Alternative type |
|----------|---------------|------------------|
| iDEAL    | IDEAL         | `IdealDeposit`   |
| Sofort   | SOFORT        | `SofortDeposit`  |
| Giropay  | GIROPAY       | `GiropayDeposit` |
| Trustly  | TRUSTLY       | `TrustlyDeposit` |
| EPS      | EPS           | `EpsDeposit`     |

#### APM's that can only be used with its specific type
| APM name        | Alternative type        |
|-----------------|-------------------------|
| Boleto Bancario | `BoletoBancarioDeposit` |

More information about the transaction types and the required parameters can be found in the front api documentation.

## Example Routing Rules

![](/img/providers/routing/macropay.png)

## Test Information

### Macropay Gateway

#### General Info
For APM's POLi, iDEAL, Giropay, EPS, Bancontact, and Boleto there is no additional input data needed once redirected. Simply follow the flow by choosing "Next", "Login", "Make Payment" etc without adding any data.

- POLi has to be tested with user country `AUS` and currency `AUD`, or country `NZL` and currency `NZD`.
- iDEAL has to be tested with user country `NLD` and currency `EUR`.
- Giropay has no notes about required country or currency.
- EPS has to be tested with user country `AUT` and currency `EUR`
- Bancontact has to be tested with user country `BEL` and currency `EUR`
- Boleto has to be tested with user country `BRA` and currency `BRL`
- Multibanco has to be tested with user country `PRT` and currency `EUR`

#### Trustly
Once redirected, the flow differs a bit depending on the country of the user, but for example if it is a German user, enter "Sparkasse Mittelthüringen" and choose that bank, then press continue and follow the instructions.

**Supported countries**: `DE`, `DK`, `EE`, `ES`, `FI`, `GB`, `IT`, `MT`, `NL`, `NO`, `PL` and `SE`.

**Allowed currencies**: `EUR` for any of the countries and the respective local currency (e.g. country `PL` and currency `PLN`) with the exception of `GB` where only `GBP` is supported.

#### Sofort
**Supported countries**: `AT`, `BE`, `DE`, `ES`, `IT`, `NL`, `GB`

**Supported currencies**: `EUR`, `GBP`

**Germany**: First Screen, Bank Name 8888888, Login data: any data, Account: choose one from the list, Tan: 12345 **Belgium**: First Screen bank name: 999, Rest same as Germany **Other**: First Screen bank name: 00000

#### Open Banking
For testing the method, a swedish bank account is needed with one of the following banks: ICA, Nordea, Lansforsakringar, Handelsbanken, Swedbank or SEB. Otherwise, Macropay can facilitate testing of each bank. 

**Supported countries**: `SE`

**Supported currencies**: `SEK`
