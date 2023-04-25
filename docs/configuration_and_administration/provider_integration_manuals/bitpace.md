--- 
id: "bitpace" 
title: "Bitpace"
hide_title: "true"
---
 
![](/img/providers/logos/bitpace.png)

# Bitpace

## About
Bitpace is a cryptocurrency payment gateway providing fast, reliable, secure cryptocurrency payment services. 

| Provider Name                | Bitpace                                                 |
|------------------------------|---------------------------------------------------------|
| Link                         | [https://www.bitpace.com/](https://www.bitpace.com/)    |
| Classification               | Mobile Payment                                          |
| Regions                      | `International`                                         |
| Currencies                   | `EUR`                                                   |
| Methods/PaymentTxTypes       | `CryptoCurrencyDeposit`<br/> `CryptoCurrencyWithdrawal` |
| PaymentIQ Configuration File | `BitpaceConfig`                                         |

:::note

Bitpace only process transacions over 10 EUR. This amount is subject to change, please ask Bitpace for latest limits during integration. 

:::

## Configuration Information

### Configuring Bitpace merchant account
To setup Bitpace in PaymentIQ the merchant needs to contact Bitpace support and request:
* The API credentials (Merchant Code, Secret Key, Callback Secret Key) 
* The credentials for the merchant panel (For test https://sandbox-merchant.lydiax.com).
* Whitelisting of [PaymentIQ IP's](/../docs/configuration_and_administration/system_configuration/provider_ip_whitelist)
* Configuring the callback URL to https://api.paymentiq.io/paymentiq/api/bitpace/callback for the production environment.

### Configuring PaymentIQ

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.bitpace.BitpaceConfig>
  <enabled>true</enabled>
  <acceptLowerAmount>???</acceptLowerAmount>
  <accounts>
    <entry>
      <string>default</string>
      <account>
        <merchantId>???</merchantId>
        <password>???</password>
        <secretKey>???</secretKey>
        <merchantName>???</merchantName>
      </account>
    </entry>
  </accounts>
</com.devcode.paymentiq.integration.bitpace.BitpaceConfig>
```

</details>


#### Attributes

| Attribute         | Description                                                                                                      |
|-------------------|------------------------------------------------------------------------------------------------------------------|
| merchantId        | Provided by Bitpace. "Merchant Code"                                                                             |
| password          | Provided by Bitpace. "Secret Key"                                                                                |
| secretKey         | Provided by Bitpace. "Callback Secret Key"                                                                       |
| acceptLowerAmount | Set to true to accept lower crypto currency amount deposited by user (see below for more info). default is false |

:::important

If the user deposits a lower crypto currency amount than in the original transaction Bitpace will wait for 30 minutes giving the user a chance to complete the amount, after that the transaction will be set to REFUNDABLE status in Bitpace system and a notification will be sent to PaymentIQ. 

At this point the merchant have the option to go to Bitpace merchant panel and manually accept the lower amount (which will be reflected in PaymentIQ) or refund it to an address provided by the user. If the merchant wants to automatically accept any lower amount, then the parameter **acceptLowerAmount** should be set to true in BitpaceConfig.  

This usually happens because the user doesn't consider transaction and wallet fees etc. To avoid this the merchant should provide information about potential fees on their site.
:::


## Example Routing Rules
![](/img/providers/routing/bitpace.png)

## Test Information
### Deposits
To test deposit select Bitpace payment option in PaymentIQ Cashier, fill in any amount and follow the instruction after being redirected. You can use testnet bitcoin to test the whole flow. Contact Bitpace for more info.

### Withdrawal
To test withdrawal select Bitpace payment option, choose crypto currency and use any value as wallet address.
