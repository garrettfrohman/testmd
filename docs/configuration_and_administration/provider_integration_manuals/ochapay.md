--- 
id: "ochapay" 
title: "OchaPay"
hide_title: "true"
---
 
![](/img/providers/logos/ochapay.png)

# OchaPay

## About
OchaPay is a creditcard processor supporting Deposits and Voids.

| Provider Name                | OchaPay                                                                         |
|------------------------------|---------------------------------------------------------------------------------|
| Link                         | [http://ochapay.com/](http://ochapay.com/)                                      |
| Classification               | PrePaid Card / Voucher                                                          |
| Regions                      | `International`                                                                 |
| Currencies                   | Please check directly with the provider regarding what currencies are supported |
| Methods/PaymentTxTypes       | `CreditcardDeposit`<br/> `Void`                                                 |
| PaymentIQ Configuration File | `OchaPayConfig`                                                                 |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.ochapay.OchapayConfig>
  <enabled>true</enabled>
  <statusUrl>${baseCallbackUrl}/api/ochapay/deposit/callback/${ptx.txRefId}</statusUrl><!-- Enter url if server side callback i desired ${baseRedirectUrl}/api/ochapay/deposit/callback/${ptx.txRefId}-->
  <returnUrl>${baseRedirectUrl}/api/ochapay/deposit/redirect/${ptx.txRefId}</returnUrl>
  <useViqProxy>true</useViqProxy>
  <accounts>
  		<entry>
  			<string>N3DS</string>
  			<account>
  			  <use3Dsecure>false</use3Dsecure>
  			  <username>??</username>
  			  <password>??</password>
  				<secretKey>??</secretKey>
  				<serviceEndpoint>https://directapi3.londonmultigames.com/wallet.ashx</serviceEndpoint>
  				<useTokenId>false</useTokenId>
  			</account>
  		</entry>
  		<entry>
  			<string>3DS</string>
  			<account>
  		 	  <use3Dsecure>true</use3Dsecure>
  				<username>??</username>
  			  <password>??</password>
  				<secretKey>??</secretKey>
  				<serviceEndpoint>https://directapi3.londonmultigames.com/wallet.ashx</serviceEndpoint>
  				<useTokenId>false</useTokenId>
  			</account>
  		</entry>
  </accounts>
</com.devcode.paymentiq.integration.ochapay.OchapayConfig>
```
</details>

### Attributes

| Attribute | Description                    |
|-----------|--------------------------------|
| username  | Username, provided by Ochapay  |
| password  | Password, provided by Ochapay  |
| secretKey | SecretKey, provided by Ochapay |

## Example Routing Rule

![](/img/providers/routing/ochapay.png)

## Test Information

### N3DS
- Currency: EUR
- Amount: 1

| Card Brand | Account          | CVV | Expiry date | Result/Info   |
|------------|------------------|-----|-------------|---------------|
| VISA       | 4111111111111111 | 123 | Any         | Successful    |
| VISA       | 4000000000000002 | Any | Any         | Card Declined |

### 3DS
Same cards as above with following conditions.
- Currency : EUR
- Amount: 2
- Phone no and zip code are mandatory request parameters. If not present transaction will fail.