--- 
id: "redsys" 
title: "Redsys"
hide_title: "true"
---

![](/img/providers/logos/redsys.png)

# Redsys

## About
Redsys - provider with a multiple features, operations and integration options that adapt to the different needs of each business.

| Provider Name                | Redsys                                                           |
|------------------------------|------------------------------------------------------------------|
| Link                         | [https://pagosonline.redsys.es/](https://pagosonline.redsys.es/) |
| Classification               | Aggregator                                                       |
| Regions                      | `International`                                                  |
| Currencies                   | `USD`, `EUR`                                                     |
| Methods/PaymentTxTypes       | `WebRedirectDeposit`                                             |
| PaymentIQ Configuration File | `RedsysConfig`                                                   |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>


```xml
<com.devcode.paymentiq.integration.redsys.RedsysConfig>
  <enabled>true</enabled>
  <useViqProxy>true</useViqProxy>
  <testMode>true</testMode>
  <accounts>
    <entry>
        <string>default</string>
        <account>
            <secretKey>??</secretKey>
            <merchantId>??</merchantId>
            <terminalEndpoint>??</terminalEndpoint>
            <quickDeposit>true</quickDeposit> <!--adds DS_MERCHANT_PAYMETHODS to request and redirects to login page-->
            <supportedCurrencies>USD|HKD|EUR|GBP|AUD|SGD|NZD|JPY|THB|KRW</supportedCurrencies>
        </account>
    </entry>
      <entry>
          <string>creditcard</string>
          <account>
              <terminalEndpoint>??</terminalEndpoint>
              <secretKey>??</secretKey>
              <merchantId>??</merchantId>
              <authType>??</authType>
              <quickDeposit>false</quickDeposit> <!--adds DS_MERCHANT_PAYMETHODS to request and redirects to login page-->
              <supportedCurrencies>USD|HKD|EUR|GBP|AUD|SGD|NZD|JPY|THB|KRW</supportedCurrencies>
          </account>
      </entry>
  </accounts>
</com.devcode.paymentiq.integration.redsys.RedsysConfig>
```

</details>

### Attributes

| Attribute        | Description                                                                    |
|------------------|--------------------------------------------------------------------------------|
| secretKey        | Api key provided by provider                                                   |
| merchantId       | Unique merchant id provided by provider                                        |
| terminalEndpoint | Terminal number provided by provider                                           |
| quickDeposit     | Switches between redirect to login page an redirect to creditcard payment page |

## Example Routing Rule

![](/img/providers/routing/redsys.png)

## Test Information

Mobile number for quick deposit login: 700 000 000

Please check the below link for current test card data:
[https://pagosonline.redsys.es/entornosPruebas.html?search=test](https://pagosonline.redsys.es/entornosPruebas.html?search=test)