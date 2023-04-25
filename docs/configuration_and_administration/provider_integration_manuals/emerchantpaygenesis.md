--- 
id: "eMerchantPayGenesis" 
title: "eMerchantPay Genesis"
hide_title: "true"
---
 
![](/img/providers/logos/emerchantpay.png)

# eMerchantPay Genesis

## About
eMerchantPay Genesis is a card processor with support for Deposits, Withdrawals and Refunds.

| Provider Name                | eMerchantPay Genesis                                                                  |
|------------------------------|---------------------------------------------------------------------------------------|
| Link                         | [https://www.emerchantpay.com/](https://www.emerchantpay.com/)                        |
| Classification               | Debit/Credit Card Processor                                                           |
| Regions                      | `International`                                                                       |
| Currencies                   | Please check directly with the provider regarding what currencies are supported       |
| Methods/PaymentTxTypes       | `CreditcardDeposit`<br/> `CreditcardWithdrawal`<br/> `GooglePayDeposit`<br/> `Refund` |
| PaymentIQ Configuration File | `EmerchantPayConfig`                                                                  |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>

<br/>

```xml
<com.devcode.paymentiq.integration.emerchantpay.EMerchantPayConfig>
<enabled>true</enabled>
<useViqProxy>true</useViqProxy>
<sale>true</sale> <!-- set to false if desired flow is auth/capture. true will process as instant 'sale' -->
<accounts>
    <entry>
     <string>3DS2</string>
     <account>
      <use3Dsecure>true</use3Dsecure>
       <username>??</username>
       <password>??</password>
       <accountID>??</accountID>
       <redirectUrl>https://api.paymentiq.io/paymentiq/api/emerchantpay/deposit/redirect/${ptx.txRefId}</redirectUrl>
       <!-- 3DS2 parameters -->
        <acquirerMerchantId>XXXXXXXX</acquirerMerchantId> <!-- Value received from PSP  -->
        <mcc>7995</mcc> <!-- 7995 for gambling merchants change if this isn't applicable to you -->
        <merchantCountry>XXX</merchantCountry> <!-- Origin country of merchant 3 DIGIT ISO for eaxmple SWE or MLT -->
        <merchantUrl>http://www.example.com</merchantUrl> <!-- URL to your website -->
        <merchantName>XXX</merchantName> <!-- Name of your brand -->
        <!-- End of 3DS2 parameters -->
     </account>
    </entry>
</accounts> 
<container>window</container>
<width>800</width>
<height>500</height>
<notificationUrl>${baseCallbackUrl}/api/emerchantpay/deposit/callback/${ptx.txRefId}</notificationUrl> 
</com.devcode.paymentiq.integration.emerchantpay.EMerchantPayConfig>
```

</details>

### Attributes

| Attribute                    | Description                                                                                                                                                                        |
|------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| username                     | Provided by eMerchantPay Genesis                                                                                                                                                   |
| password                     | Provided by eMerchantPay Genesis                                                                                                                                                   |
| accountID                    | Provided by eMerchantPay Genesis                                                                                                                                                   |
| dynamicDescriptor            | If this config is set, the value(s) will be sent as the dynamic descriptor to the PSP. The dynamic descriptor can have two values, separated by \| e.g: MerchantName\|MerchantCity |
| allowWithdrawalBeforeDeposit | Set to true on account level if the merchant wants to use Payouts (credits without a reference transaction) instead of Credit Fund Transfer (CTF) for CreditcardWithdrawal.*       |

\* Note that this requires additional configuration by the provider, so contact their support team in case you want Payouts to be enabled.

### Google Pay in the Cashier

![](/img/providers/googlepay_cashier_inline.png)

In order to display the Google Pay button and popup directly in the [Cashier](/docs/apis_and_integration/cashier/cashier_introduction) instead of using the redirect flow, the inline flow must be configured.

<details>
<summary>In <b>MerchantConfig</b>, add the following properties</summary>

```xml
<properties>
	<entry>
		<string>googlepay</string>
		<map>
			<entry>
				<string>environment</string>
				<string>???</string>
			</entry>
			<entry>
				<string>allowedAuthMethods</string>
				<string>PAN_ONLY|CRYPTOGRAM_3DS</string>
			</entry>
			<entry>
				<string>allowedCardNetworks</string>
				<string>AMEX|DISCOVER|INTERAC|JCB|MASTERCARD|VISA</string>
			</entry>
			<entry>
				<string>gateway</string>
				<string>emerchantpay</string>
			</entry>
			<entry>
				<string>gatewayMerchantId</string>
				<string>???</string>
			</entry>
			<entry>
				<string>tokenizationType</string>
				<string>PAYMENT_GATEWAY</string>
			</entry>
			<entry>
				<string>merchantName</string>
				<string>???</string>
			</entry>
			<entry>
				<string>merchantId</string>
				<string>???</string>
			</entry>
		</map>
	</entry>
</properties>
```


### Attributes

| Attribute         | Description                                                                                      |
|-------------------|--------------------------------------------------------------------------------------------------|
| environment       | Environment (For example - TEST or PRODUCTION)                                                   |
| gateway           | Provided by the payment provider. (emerchantpay)                                                 |
| gatewayMerchantId | Provided by the payment provider. (Google Pay merchantID from the Google Pay Business Console)   |
| merchantId        | Google Pay merchantID from the Google Pay Business Console. Required for production environment. |
| merchantName      | Optional Merchant name rendered in the payment sheet.                                            |


</details>

<details>
<summary>Add the GooglePayDeposit TxType Input under **Admin** / **Cashier** / **Payment methods and inputs** </summary>

![](/img/providers/googlepay_deposit_inline.png)

</details>

## Example Routing Rule
![](/img/providers/routing/emerchantpaygenesis.png)

## Test Information

Please check here for test cards:

[https://emerchantpay.github.io/gateway-api-docs/#testing-3ds-v1](https://emerchantpay.github.io/gateway-api-docs/#testing-3ds-v1)

[https://emerchantpay.github.io/gateway-api-docs/?shell#testing-3ds-v2](https://emerchantpay.github.io/gateway-api-docs/?shell#testing-3ds-v2)

