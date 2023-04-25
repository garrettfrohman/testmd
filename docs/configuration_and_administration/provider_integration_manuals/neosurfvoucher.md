--- 
id: "neosurfvoucher" 
title: "NeosurfVoucher"
hide_title: "true"
---
 
![](/img/providers/logos/neosurfvoucher.png)

# NeosurfVoucher

## About
Buying and using Neosurf vouchers is easy and convenient.
You don’t need to register or provide personal information and your Neosurf voucher is ready to use immediately.

Neosurf voucher provides “make_payment” and “cancel_payment” functionality in order to make or cancel a transaction on a Neosurf Card or MyNeosurf account.

| Provider Name                | NeosurfVoucher                                                                                          |
|------------------------------|---------------------------------------------------------------------------------------------------------|
| Link                         | [https://www.neosurf.com/en_GB/presentation](https://www.neosurf.com/en_GB/presentation)                |
| Classification               | Prepaid Card / Voucher, Wallet                                                                          |
| Regions                      | `International`                                                                                         |
| Currencies                   | Please check directly with the provider regarding what currencies are supported                         |
| Methods/PaymentTxTypes       | `NeosurfVoucherDeposit`<br/>`NeosurfVoucherWithdrawal`<br/>`WebRedirectDeposit`<br/>`Void`<br/>`Refund` |
| PaymentIQ Configuration File | `NeosurfVoucherConfig`                                                                                  |

## Configuration Information

<details>

<summary>Click to view example configuration</summary>

<br/>

```xml
<com.devcode.paymentiq.integration.neosurf.voucher.NeosurfVoucherConfig>
  <enabled>true</enabled>
  <accounts>
    <entry>
      <string>default</string>
      <account>
        <merchantId>20090</merchantId>
        <secretKey>a42c8018e31ac7adbe154b68b55995a7</secretKey>
        <service>1</service>
        <supportedCurrencies>EUR</supportedCurrencies>
        <method>neosurf,myneosurf</method>
        <siteId>www.bambora.com</siteId>
        <prohibitedForMinors>false</prohibitedForMinors>
      </account>
    </entry>
  </accounts>
  <testMode>true</testMode>
  <version>3</version>
  <sendCustomerData>true</sendCustomerData>
  <defaultDescriptor>${defaultTransactionDescriptor}</defaultDescriptor>
</com.devcode.paymentiq.integration.neosurf.voucher.NeosurfVoucherConfig>
```

</details>
<br/>

### Attributes 

- **Note: Some of the configuration fields are specific to the version of the integration you use.**

| Attribute           | Description                                                                                                                                                                                                                        | Version |
|---------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------|
| version             | Sets the version to be used of the integration. Available options: 1, 2 and 3                                                                                                                                                      |         |
| merchantId          | Merchant id (given by Neosurf)                                                                                                                                                                                                     | 1, 2, 3 |
| secretKey           | Merchant's secret key from Neosurf, used to calculate security hash                                                                                                                                                                | 1, 2, 3 |
| method              | Choose which Neosurf options should be displayed to the end-user, separated with comma. e.g `<method>neosurf,myneosurf</method>`. <br/>Available options: `neosurf`, `myneosurf`, `creditCard`, `all`, `canadaPost`, `POSpayment`. | 2       |
| prohibitedForMinors | Indicates if a non-Adult Neosurf customer can do this transaction or not. Set by `true` or `false`, defaults to false.                                                                                                             | 2, 3    |
| siteId              | Corresponds to Neosurf parameter `subMerchantId` and should be the final domain name of the merchant.                                                                                                                              | 2, 3    |
| service             | Corresponds to parameter `IDService`, defaults to 1.                                                                                                                                                                               | 1       |
| sendCustomerData    | Decides if PIQ should send customer data in the request to Neosurf, set `false` to not send, defaults to `true`.                                                                                                                   | 2, 3    |

Note: Neosurf defaults all new merchants to version 3 of API. Please contact Neosurf directly to use another version.

### IP Whitelist
Make sure to whitelist PIQ's [IP-addresses](/docs/configuration_and_administration/system_configuration/provider_ip_whitelist) for your Neosurf merchant account by contacting them.

### NeosurfVoucher v1
It's recommended to use version 3 of NeosurfVoucher, but if you should use version 1 you need to use the transaction type NeosurfVoucherDeposit, and make sure to send the input parameter `voucherNumber` to PIQ in the request.

### NeosurfVoucher v2 and v3
When using version 2 or 3 of the API, you can use either transaction type NeosurfVoucherDeposit or WebRedirectDeposit. Since version 2 and 3 redirects the end-user to the Neosurf page, there is no need for a `voucherNumber` as an input parameter, therefore WebRedirectDeposit can be the better choice. However, if NeosurfVoucherDeposit is used, then just make sure to not display the voucher number input field in the cashier/checkout.

Using version 2 or 3, you as a merchant can choose which payment options the end-user should see and be able to use on the Neosurf page. This is determined by the `method` configuration entry, where the chosen values dictates which options are available on the Neosurf page. Please see the options in the above configuration attribute table.

### NeosurfVoucher refund
Partial and full refunds are supported with the v2 and v3 versions of NeosurfVoucher.

## Example Routing Rule
![](/img/providers/routing/neosurfvoucher.png)

## Test Information

### Voucher Deposit

Test with smallest possible amount since it’s a voucher and the funds can be depleted. If it becomes depleted, ask DevCode to email Frederic at frederic@neosurf.com and ask the voucher to be refilled. State the voucher number as reference.

- Currency: EUR
- Voucher Code: 2602JGUMK0

### MyNeosurf login details

- Login: technicalsupport@bambora.com
- Password: QBW8$z9D74fcrwd

### Payouts

Use email technicalsupport@bambora.com when initiating a Neosurf withdrawal.
