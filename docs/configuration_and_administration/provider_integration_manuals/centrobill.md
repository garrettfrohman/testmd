--- 
id: "centrobill"
title: "CentroBill"
hide_title: "true"
---

![](/img/providers/logos/centrobill.png)

# CentroBill'
## About
CentroBill is a payment processor which supports credit card payments and various alternative payment methods.

| Provider Name                | CentroBill                                                                                                               |
|------------------------------|--------------------------------------------------------------------------------------------------------------------------|
| Link                         | [https://centrobill.com/](https://centrobill.com/)                                                                       |
| Classification               | Debit/Credit Card Processor                                                                                              |
| Regions                      | `International`                                                                                                          |
| Currencies                   | Please check directly with the provider regarding what currencies are supported                                          |
| Methods/PaymentTxTypes       | `CreditcardDeposit` <br/> `CreditcardWithdrawal` <br/> `WebRedirectDeposit` <br/> `WebRedirectWithdrawal` <br/> `Refund` |
| PaymentIQ Configuration File | `CentroBillConfig`                                                                                                       |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.centrobill.CentroBillConfig>
    <enabled>true</enabled>
    <testMode>true</testMode>
    <useViqProxy>true</useViqProxy>
    <accounts>
        <entry>
            <string>DEFAULT</string>
            <account>
                <apiKey>??</apiKey>
                <siteId>??</siteId>
            </account>
        </entry>
    </accounts>
    <defaultDescriptor>DevCode payment</defaultDescriptor>
</com.devcode.paymentiq.integration.centrobill.CentroBillConfig>
```

</details>

### Attributes
| Attribute                  | Description                                                                                                                                                                                                                                                                                                                                                                         |
|----------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| accountConfig.apiKey       | Authentication key provided to merchant by CentroBill.                                                                                                                                                                                                                                                                                                                              |
| accountConfig.siteId       | ID of the Site which has to be created on CentroBill clients page in order to be able to process payments.                                                                                                                                                                                                                                                                          |
| accountConfig.forcePayment | Optional. Can be set to the specific payment method from the list of supported APMs (see below). If set, the configured payment method will be used for `WebRedirectDeposit`  transaction. If not set, user will be able to choose specific method on CentroBill payment page, when triggering `WebRedirectDeposit`. Example of usage: `<forcePayment>sofortbanking</forcePayment>` |
| accountConfig.method       | Optional. Defines payment methods which can be shown on CentroBill payment page when triggering `WebRedirectDeposit`. Has no effect if `accountConfig.forcePayment` is set or the `WebRedirectDeposit` is used along with the service mapping. Example of usage: `<method>sofortbanking&#124;sepa&#124;applepay</method>`                                                           |

### Configuring APMs
Using service mapping: one of the ways to force use specific payment methods is to configure serviceMapping in `MerchantConfig` for WEBREDIRECT. The service name of specific APM can be obtained from supported APMs list below.
Example:

```xml
  <serviceMapping>
    <entry>
      <string>WEBREDIRECT</string>
      <string>SOFORTBANKING|SEPA|CARD|IDEAL|APPLEPAY</string>
    </entry>
  </serviceMapping>
```

Using forcePayment config parameter: as described above, `accountConfig.forcePayment` can be used to force use specific payment method.

Using method config parameter or not using config parameters at all: if `accountConfig.method` is configured, or it is not set at all, the user will be able to choose among the available payment methods in CentroBill payment page, when triggering `WebRedirectDeposit` transaction.  

### Supported APMs

APMs can be used through the txType `WebRedirectDeposit`. There is the list of all supported methods:
<details>
<summary>Click to view the list</summary>
<br/>

| Payment Method | Service Name  |
|----------------|---------------|
| ApplePay       | applepay      |
| SEPA           | sepa          |
| Sofort Banking | sofortbanking |
| Ideal          | ideal         |
| Eps            | eps           |
| mybank         | mybank        |
| Bancontact     | bancontact    |
| Giropay        | giropay       |
| Przelewy24     | przelewy24    |
| Online Banking | onlinebanking |
| Skrill         | skrill        |
| Clickandbuy    | clickandbuy   |
| PayPal         | paypal        |
| Pix            | pix           |
| Boleto         | boleto        |
| PPS            | pps           |
| Gash           | gash          |
| Crypto         | crypto        |
| Paygarden      | paygarden     |
| Alipay         | alipay        |
| Wechat         | wechat        |
| Unionpay       | unionpay      |
| Voucher        | voucher       |
| Paysafecard    | paysafecard   |
| Ukash          | ukash         |
| Safeklick      | safeklick     |
| sms            | sms           |

</details>

## Withdrawals
In order to trigger withdrawal, deposit should be made first. After successful deposit, new account will be created in the cashier. This newly created account can be used for triggering withdrawals.  

## Example Routing Rule
![](/img/providers/routing/centrobill.png)

## Test Information

If the default test credentials are used, then the following test accounts can be used for transaction testing:

| Account Number         | 3DS Enabled | Account type |
|------------------------|-------------|--------------|
| 4000001293797551       | No          | Credit card  |
| 4000004244989699       | Yes         | Credit card  |
| DE68111111151272092025 | No          | SEPA         |

If other credentials are used, the merchant will be able to create the test accounts in the Clients CentrobBill page and use them.