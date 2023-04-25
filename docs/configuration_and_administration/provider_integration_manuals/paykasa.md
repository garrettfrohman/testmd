--- 
id: "paykasa" 
title: "PayKasa"
hide_title: "true"
---
 
![](/img/providers/logos/paykasa.png)

# PayKasa

## About
Paykasa is a prepaid voucher that was specifically designed for online spending. 

| Provider Name                | PayKasa                                                                         |
|------------------------------|---------------------------------------------------------------------------------|
| Link                         | [https://paykasa.com/](https://paykasa.com/)                                    |
| Classification               | PrePaid Card / Voucher                                                          |
| Regions                      | `Turkey`                                                                        |
| Currencies                   | Please check directly with the provider regarding what currencies are supported |
| Methods/PaymentTxTypes       | `PaykasaDeposit`<br/> `PaykasaWithdrawal`                                       |
| PaymentIQ Configuration File | `PayKasaConfig`                                                                 |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.paykasa.PaykasaConfig>
  <enabled>true</enabled>
  <useViqProxy>false</useViqProxy>
  <accounts>
    <entry>
      <string>PK_EUR</string>
      <account>
        <use3Dsecure>false</use3Dsecure>
        <supportedCurrencies>EUR</supportedCurrencies>
        <apiKey>???</apiKey>
        <voucherType>Cash</voucherType>
      </account>
    </entry>
  </accounts>
  <testMode>false</testMode>
</com.devcode.paymentiq.integration.paykasa.PaykasaConfig>
```

</details>

### Attributes

| PaymentIQ Configuration | Description         |
|-------------------------|---------------------|
| apiKey                  | Provided by Paykasa |
| voucherType             |                     |

### Email template example

![](/img/providers/paykasa01.png)

### Rules notification example

![](/img/providers/paykasa02.png)

## Example Routing Rule
![](/img/providers/routing/paykasa.png)

## Test Information

- New voucher can be generated at: [http://test.pay.paykasa.com/sample-merchant/voucherissue/](http://test.pay.paykasa.com/sample-merchant/voucherissue)
- Supported amounts for deposit: 10 EUR, 10.01 EUR, 20 EUR, 20.01 EUR
- Supported amounts for withdrawal: 10 EUR. After success withdrawal it is expected that new voucher is created and it’s code can be used for deposit.
