--- 
id: "totalcoin" 
title: "TotalCoin"
hide_title: "true"
---
 
![](/img/providers/logos/totalcoin.png)

# TotalCoin

## About
TotalCoin provides cash payment solutions in Argentina.

| Provider Name                | TotalCoin                                                                  |
|------------------------------|----------------------------------------------------------------------------|
| Link                         | [https://ar.totalcoin.com/](https://ar.totalcoin.com/)                     |
| Classification               | Aggregator                                                                 |
| Regions                      | `Argentina`                                                                |
| Currencies                   | `ARS`                                                                      |
| Methods/PaymentTxTypes       | `WebRedirectDeposit`, `TotalCoinBankDeposit`, `TotalCoinCreditCardDeposit` |
| PaymentIQ Configuration File | `TotalCoinConfig`                                                          |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.totalcoin.TotalCoinConfig>
    <enabled>true</enabled>
    <useViqProxy>true</useViqProxy>
    <accounts>
        <entry>
            <string>CASH</string>
            <account>
                <merchantName>Devcode</merchantName>
                <email>??</email>
                <password>??</password>
                <serviceEndpoint>??</serviceEndpoint>
                <secretKey>??</secretKey>
                <supportedCurrencies>ARS</supportedCurrencies>
            </account>
        </entry>
        <entry>
            <string>BANKS</string>
            <account>
                <merchantName>Devcode</merchantName>
                <email>??</email>
                <password>??</password>
                <serviceEndpoint>??</serviceEndpoint>
                <merchantId>??</merchantId>
                <supportedCurrencies>ARS</supportedCurrencies>
            </account>
        </entry>
        <entry>
            <string>CC</string>
            <account>
                <merchantName>Devcode</merchantName>
                <username>??</username>
                <password>??</password>
                <serviceEndpoint>??</serviceEndpoint>
                <merchantId>??</merchantId>
                <customerId>??</customerId>
                <supportedCurrencies>ARS</supportedCurrencies>
                <container>window</container>
            </account>
        </entry>
    </accounts>
    <defaultDescriptor>Devcode</defaultDescriptor>
    <testMode>true</testMode>
</com.devcode.paymentiq.integration.totalcoin.TotalCoinConfig>
```

</details>

### Attributes

| Attribute       | Description                                                             |
|-----------------|-------------------------------------------------------------------------|
| username        | email provided by TotalCoin team                                        |
| password        | password provided by TotalCoin team                                     |
| secretKey       | pin for cash transactions provided by TotalCoin team                    |
| merchantId      | merchantId provided by TotalCoin team                                   |
| customerId      | default quoteId for credit card transactions provided by TotalCoin team |
| serviceEndpoint | Service endpoint for cash/card/bank method provided by TotalCoin team   |

## Example Routing Rule

![](/img/providers/routing/totalcoin.png)

## Test Information

To receive final payment status, please ask TotalCoin team to manually generate and send notification status.