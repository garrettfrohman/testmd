--- 
id: "fido" 
title: "Fido"
hide_title: "true"
--- 

![](/img/providers/logos/fido.png)

# Fido

## About
The Fido Merchant Services is a online payment provider and gateway that provide visitors with a seamless user experience. This product is compatible with all leading credit and debit cards including Visa, MasterCard and American Express. Enhanced functionality and processing for 190 currencies and fully PCI DSS Compliant solution.
  

| Provider Name                | Fido                                                                                         |
|------------------------------|----------------------------------------------------------------------------------------------|
| Link                         | [https://www.fidoms.com/](https://www.fidoms.com/)                                           |
| Classification               | Debit/Credit Card Processor                                                                  |
| Regions                      | `International`                                                                              |
| Currencies                   | Please check directly with the provider regarding what currencies are supported              |
| Methods/PaymentTxTypes       | `CreditcardDeposit` <br/> `CreditcardWithdrawal` <br/> `Capture` <br/> `Void` <br/> `Refund` |
| PaymentIQ Configuration File | `FidoConfig`                                                                                 |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.fido.FidoConfig>
  <enabled>true</enabled>
  <accounts>
    <entry>
      <string>default</string>
      <account>
        <merchantName>???</merchantName>
        <merchantId>???</merchantId>
        <apiKey>???</apiKey>
        <secretKey>???</secretKey>
        <terminal>???</terminal>
        <!-- <supportedCurrencies>USD|EUR</supportedCurrencies> -->
        <!-- <useTokenId>true</useTokenId> -->
        <!-- <use3Dsecure>true</use3Dsecure> -->
        <!--Options: AUTH_CAPTURE/FINAL_AUTH/PRE_AUTH-->
        <authType>AUTH_CAPTURE</authType>
      </account>
    </entry>
  </accounts>
  <txHistoryDelayHours>0</txHistoryDelayHours>
</com.devcode.paymentiq.integration.fido.FidoConfig>
```
</details>

### Attributes


| Attribute           | Description                                                                                                                                                                                                                                                                   |
|---------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| merchantName        | Correspond to Username in Fido back office                                                                                                                                                                                                                                    |
| merchantId          | Correspond to Merchant/Member ID provided by Fido                                                                                                                                                                                                                             |
| apiKey              | Correspond to Partner ID provided by Fido                                                                                                                                                                                                                                     |
| secretKey           | Secret key provided by Fido (or generated in Fido back office)                                                                                                                                                                                                                |
| terminal            | Terminal IDs are provided by Fido and depend on which acquiring bank the merchant will be using.  Can be either single like: "3093", or multiple mapped by card type and currency like: "VISA_USD_CC->3093,MASTERCARD_USD_CC->3095,VISA_USD_DC->3094,MASTERCARD_USD_DC->3096" |
| txHistoryDelayHours | To do a CreditcardWithdrawal the user must first have done a successful deposit. This parameter sets how many hours back in transaction history should be the last deposit to search.                                                                                         |

Before configuring Fido in PaymentIQ the merchant should contact Fido support and request the following:
* Get access to Fido back office.
* Get all the account parameters specified above (Username, Merchant/Member ID, Partner ID, Secret key, Terminal IDs).
* Whitelist [PaymentIQ IP addresses](/../docs/configuration_and_administration/system_configuration/provider_ip_whitelist).

## Example Routing Rule

![](/img/providers/routing/fido.png)

## Test Information

### Test cards with USD

| Brand      | 3DS | Card number      | Cvv | Expiry Date |
|------------|-----|------------------|-----|-------------|
| VISA       | No  | 4111110000000021 | 123 | 12/2030     |
| VISA       | Yes | 4111110000000211 | 123 | 12/2030     |
| MASTERCARD | No  | 5100000000000321 | 123 | 12/2030     |
| MASTERCARD | Yes | 5100000000000511 | 123 | 12/2030     |

### Test cards with EUR

| Brand      | 3DS | Card number      | Cvv     | Expiry Date |
|------------|-----|------------------|---------|-------------|
| VISA       | Yes | 4111111111111111 | 010/300 | 12/2030     |
| MASTERCARD | Yes | 5105105105105100 | 010/300 | 12/2030     |

