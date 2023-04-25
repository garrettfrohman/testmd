--- 
id: "bitpay" 
title: "BitPay"
hide_title: "true"
---
 
![](/img/providers/logos/bitpay.png)

# BitPay

## About
The Bitpay Merchant Account gives you access to a globally renowned payment option, the Crypto Currency, namely Bitcoin payments. Cryptocurrency payments are new, fast and cost effective means of taking payments from customers worldwide - even in countries that can be difficult to reach. Bitpay is a Bitcoin invoice service where your customers can do a deposit using Bitcoin.

| Provider Name                | BitPay                                                                          |
|------------------------------|---------------------------------------------------------------------------------|
| Link                         | [https://bitpay.com/](https://bitpay.com/)                                      |
| Classification               | Crypto Currency                                                                 |
| Regions                      | `International`                                                                 |
| Currencies                   | Please check directly with the provider regarding what currencies are supported |
| Methods/PaymentTxTypes       | `CryptoCurrencyDeposit`                                                         |
| PaymentIQ Configuration File | `BitPayConfig`                                                                  |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.bitpay.BitpayConfig>
  <enabled>true</enabled>
  <useViqProxy>true</useViqProxy>
  <accounts>
    <entry>
      <string>default</string>
      <account>        
          <secretKey>???</secretKey>
          <merchantKeyId>???</merchantKeyId>
          <memberGuid>???</memberGuid>
    <!--  <service>medium</service>  -->
    <!--  <service>low</service> -->
    <!--  <service>high</service> -->
      </account>
    </entry>
  </accounts>
  <testMode>false</testMode>
</com.devcode.paymentiq.integration.bitpay.BitpayConfig>
```

</details>

### Attributes

| PaymentIQ Configuration | Provider Credential                  |
|-------------------------|--------------------------------------|
| secretKey               | Secret Key. Provided by Bitpay.      |
| merchantKeyId           | Merchant Key Id. Provided by Bitpay. |
| memberGuid              | MemberGuid. Provided by Bitpay.      |
| service                 | low, medium or high.                 |

### BitPay Deposit
To start deposit process each account need to have an elliptic-curve private key, and this key needs to be paired with merchant Bitpay account. Ask our support team to generate the private key and help you with the pairing process.

:::caution

To make successful deposit Bitpay demand user’s email address. Make sure user’s email address in verify uses response is populated.
In unlikely scenario of late payment; which represents payment that went through after invoice expiration, merchant must contact Bitpay support for refund.

:::

### Added features
Each invoice can have four stages:
- New, not paid yet.
- Paid, the invoice is paid to the network but it is not confirmed yet. (instance)
- Confirmed, the payment have been confirmed at least once by the network. (takes around 10 minutes to 1 hour)
- Complete, , the payment have been confirmed six times by the network. (takes around 1 hour to maybe couple of days)

Bitpay will make your fund available to you after sixth confirmation. Yet it can be adjusted at what stage end-user gets his/hers deposit. This option is set by default of medium, user will get funds at first confirm. Set the speed on low for more security but slower response. Or fast with more risk, but instantaneous.
Needless to say this approach provide three statuses for transactions; Successful, Failed and Waiting for confirmation. Merchant can add new URL for the third status, otherwise it will follow the success URL for transactions that are waiting to get confirmed.
Ask our support team or modify values mentioned above.

## Example Routing Rule
-

## Test Information

### Deposits

To be able to pay a test invoice, one needs a test wallet, and test Bitcoins.

- You can download the suggested wallet from https://bitpay.com/wallet
- And get some test Bitcoins from https://testnet.coinfaucet.eu/en/

Make sure test user has email address populated.



