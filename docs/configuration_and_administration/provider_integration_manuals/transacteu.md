--- 
id: "transacteu" 
title: "TransactEU"
hide_title: "true"
--- 
# TransactEU

## About

TransactEU is a creditcard processor.

| Provider Name                | TransactEU                                                                                                |
|------------------------------|-----------------------------------------------------------------------------------------------------------|
| Link                         | [https://www.transact.eu/](https://www.transact.eu/)                                                      |
| Classification               | `Debit/Credit Card Processor`                                                                             |
| Regions                      | `International`                                                                                           |
| Currencies                   | Please check directly with the provider regarding what currencies are supported                           |
| Methods/PaymentTxTypes       | `CreditcardDeposit`, `CreditcardWithdrawal`, `CreditcardAccountVerification`, `Capture`, `Void`, `Refund` |
| PaymentIQ Configuration File | `TransactEUConfig`                                                                                        |


## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.transacteu.TransactEUConfig>
    <enabled>true</enabled>
    <useViqProxy>true</useViqProxy>
    <accounts>
        <entry>
            <string>N3DS</string>
            <account>
                <username>???</username>
                <password>???</password>
                <merchantId>???</merchantId> <!--mid-->
                <merchantCode>???</merchantCode> <!--mid_q-->
                <supportedCurrencies>EUR</supportedCurrencies>
                <useTokenId>true</useTokenId> <!-- allow withdrawals for stored cards-->
                <use3Dsecure>false</use3Dsecure>
            </account>
        </entry>
        <entry>
            <string>DEFAULT</string>
            <account>

                <username>???</username>
                <password>???</password>
                <merchantId>???</merchantId> <!--mid-->
                <merchantCode>???</merchantCode> <!--mid_q-->
                <supportedCurrencies>EUR</supportedCurrencies>

                <authType>AUTH_CAPTURE</authType>
                <!--
                <authType>AUTH_CAPTURE</authType> Do an auth + capture in one step
                <authType>FINAL_AUTH</authType> Do a final authorization to later be manually or autmatically captured/voided
                <authType>PRE_AUTH</authType> Do a pre-authorization to later be manually or autmatically captured/voided
                -->

                <recurring>true</recurring>
                <use3Dsecure>true</use3Dsecure>
                <useTokenId>true</useTokenId> <!-- allow withdrawals for stored cards-->
            </account>
        </entry>

    </accounts>
</com.devcode.paymentiq.integration.transacteu.TransactEUConfig>
```

</details>

### Attributes


| Attribute    | Description                                                             |
|--------------|-------------------------------------------------------------------------|
| username     | username - provided by TransactEU                                       |
| password     | password - provided by TransactEU                                       |
| merchantId   | mid - provided by TransactEU                                            |
| merchantCode | mid_q - provided by TransactEU                                          |
| recurring    | allow recurring payments                                                |
| useTokenId   | allow withdrawals using stored token for previously success transaction |

### Notes

- TransactEU supports external 3DS1 and 3DS2 that should be configured according to documentation 

## Example Routing Rule

![](/img/providers/routing/transacteu.png)

## Test Information

| Type | Number           | CVV              | Expiry Date     |
|------|------------------|------------------|-----------------|
| 3DS1 | 4122857790340234 | Any three digits | Any future date |
| 3DS2 | 4874970686672022 | Any three digits | Any future date |
