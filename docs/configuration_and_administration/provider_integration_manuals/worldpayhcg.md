--- 
id: "worldpayhcg" 
title: "WorldPayHCG (High Capacity Gateway)"
hide_title: "true"
---
 
![](/img/providers/logos/worldpayhcg.png)

# WorldPayHCG (High Capacity Gateway)

## About
Worldpay is a creditcard processor with support for Deposits, Withdrawals and Refunds.

| Provider Name                | WorldPayHCG (High Capacity Gateway)                                             |
|------------------------------|---------------------------------------------------------------------------------|
| Link                         | [http://www.worldpay.com/](http://www.worldpay.com/)                            |
| Classification               | Debit/Credit Card Processor                                                     |
| Regions                      | `International`                                                                 |
| Currencies                   | Please check directly with the provider regarding what currencies are supported |
| Methods/PaymentTxTypes       | `CreditcardDeposit`<br/> `CreditcardWithdrawal`<br/> `Refund`                   |
| PaymentIQ Configuration File | `WorldPayHCGConfig`                                                             |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.worldpayhcg.WorldPayHCGConfig>
  <enabled>true</enabled>
  <useViqProxy>true</useViqProxy>
  <accounts>
    <entry>
  			<string>REFUND_EUR</string>
  			<account>
  		  	<use3Dsecure>true</use3Dsecure>
  				<merchantId>??</merchantId>
  				<username>??</username>
  			  <password>??</password>
  				<redirectUrl>${baseRedirectUrl}/api/worldpayhcg/callback</redirectUrl>
  				<useTokenId>false</useTokenId>
  				<serviceEndpoint>https://trx3.wpstn.com/stlinkssl/stlink.dll</serviceEndpoint>
  				<storeId>??</storeId>
  			</account>
  		</entry>
  		<entry>
  			<string>N3DS_EUR</string>
  			<account>
  			  <use3Dsecure>false</use3Dsecure>
  			  <merchantId>??</merchantId>
  			  <username>??</username>
  			  <password>??</password>
  				<redirectUrl>${baseRedirectUrl}/api/worldpayhcg/callback</redirectUrl>
  				<useTokenId>false</useTokenId>
  				<serviceEndpoint>https://trx3.wpstn.com/stlinkssl/stlink.dll</serviceEndpoint>
  				<storeId>??</storeId>
  			</account>
  		</entry>
  		<entry>
  			<string>3DS_EUR</string>
  			<account>
  		  	<use3Dsecure>true</use3Dsecure>
  				<merchantId>??</merchantId>
  				<username>??</username>
  			  <password>??</password>
  				<redirectUrl>${baseRedirectUrl}/api/worldpayhcg/callback</redirectUrl>
  				<useTokenId>false</useTokenId>
  				<serviceEndpoint>https://trx3.wpstn.com/stlinkssl/stlink.dll</serviceEndpoint>
  				<storeId>??</storeId>
  			</account>
  		</entry>
		</accounts>
		<testMode>false</testMode>
		<timeOut>60000</timeOut>
</com.devcode.paymentiq.integration.worldpayhcg.WorldPayHCGConfig>
```

</details>

### Attributes

| Attribute  | Description             |
|------------|-------------------------|
| merchantId | Provided by WorldpayHCG |
| username   | Provided by WorldpayHCG |
| password   | Provided by WorldpayHCG |
| storeId    | Provided by WorldpayHCG |
| useAvs     | -                       |

## Example Routing Rule
![](/img/providers/routing/worldpayhcg.png)

## Test Information

### N3DS

| Card Brand | Account          | CVV | Expiry date |
|------------|------------------|-----|-------------|
| VISA       | 4544320001228342 | Any | 12/19       |
| VISA       | 4779160330716625 | Any | 12/19       |
| MAESTRO    | 5020310001212834 | Any | 12/19       |
| MASTERCARD | 5301207010000012 | Any | 12/19       |

### 3DS

3DS password - 12345

3DS wrong password to force failed 3DS auth and to test 3DS fallback to another PSP - 33333