--- 
id: "googlepay" 
title: "Google Pay (via Provider)"
hide_title: "true"
---
 
![](/img/providers/logos/googlepay.png)

# Google Pay (via Provider)

## About
Google Pay lets customers pay with the press of a button — using payment methods saved to their Google Account.

| Provider Name                | Google Pay                                                                      |
|------------------------------|---------------------------------------------------------------------------------|
| Link                         | [https://pay.google.com/about/](https://pay.google.com/about/)                  |
| Classification               | Wallet                                                                          |
| Regions                      | `International`                                                                 |
| Currencies                   | Please check directly with the provider regarding what currencies are supported |
| Methods/PaymentTxTypes       | `GooglePayDeposit`                                                              |
| PaymentIQ Configuration File | `GooglePayConfig`                                                               |
| Providers                    | `Adyen`, `Checkout`, `Secure Trading (Trust Payments)`, `eMerchantPay`          |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.googlepay.GooglePayConfig>
  <enabled>true</enabled>
  <gateway>???</gateway>
  <gatewayMerchantId>???</gatewayMerchantId>
  <merchantId>???</merchantId>
  <merchantName>???</merchantName>
</com.devcode.paymentiq.integration.googlepay.GooglePayConfig>
```

</details>

### Attributes

| Attribute         | Description                                                                                      |
| ----------------- | ------------------------------------------------------------------------------------------------ |
| gateway           | Provided by the payment provider. (For example "adyen" for Adyen)                                |
| gatewayMerchantId | Provided by the payment provider. (For Adyen it corresponds to the merchant account name)        |
| merchantId        | Google Pay merchantID from the Google Pay Business Console. Required for production environment. |
| merchantName      | Optional Merchant name rendered in the payment sheet.                                            |


### Example Routing Rule
![](/img/providers/routing/googlepay.png)

### Token
There are two alternative flows when it comes to token creation for Google Pay.

1. **Inline** - Token is generated and submitted via the Cashier before a transaction has been created in PaymentIQ. Requires configuration of **MerchantConfig** and **TxTypeInputs**.
2. **Post-registered** - Token is generated after the transaction has started in PaymentIQ. Google Pay interface is available after a redirect via a redirectOutput template. Requires configuration of **GooglePayConfig**.


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
				<string>???</string>
			</entry>
			<entry>
				<string>allowedCardNetworks</string>
				<string>???</string>
			</entry>
			<entry>
				<string>gateway</string>
				<string>???</string>
			</entry>
			<entry>
				<string>gatewayMerchantId</string>
				<string>???</string>
			</entry>
			<entry>
				<string>tokenizationType</string>
				<string>???</string>
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
</details>

<details>
<summary>In <b>TxTypeInputs</b>, add the following properties</summary>

```xml
<com.devcode.paymentiq.service.cashier.TxTypeInput>
  <txType>GooglePayDeposit</txType>
  <providerType>GOOGLEPAY</providerType>
  // highlight-start
  <hideSubmit>true</hideSubmit>
  <inputHtmlTemplateName>googlepay-inline-input-template</inputHtmlTemplateName>
  // highlight-end
</com.devcode.paymentiq.service.cashier.TxTypeInput>
```
</details>

## Example Routing Rule
![](/img/providers/routing/googlepay.png)

## Test Information

To test Google Pay, you must:  
* Login to a Google account.
* Create a Google Pay wallet with valid card details. Google Pay does not accept test cards.

