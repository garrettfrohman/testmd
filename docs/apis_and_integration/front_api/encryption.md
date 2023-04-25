---
id: "encryption"
title: "Encryption"
---
import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

To support encryption of the credit card number and CVV between the enduser browser (or any other enduser client) and the VaultIQ service, PaymentIQ includes a JavaScript encryption library.


:::tip Hosted Fields

If you don't want to bother with encryption and PCI compliancy, there is an option available to use our own [hosted field](/../docs/apis_and_integration/integration_overview/hosted_fields) solution which is fully PCI compliant with ready to use credit card fields.
:::

The library is based on the JSEncrypt JavaScript Library. See [http://travistidwell.com/jsencrypt/](http://travistidwell.com/jsencrypt/) for details.

Include following JavaScript to get everything you need in order to encrypt credit card numbers:

```
/paymentiq/api/viq/jscardencrypter/{merchantId}
```

Example how to encrypt a credit card number on the test environment:

```xml
<script type="text/javascript" src="https://test-api.paymentiq.io/paymentiq/api/viq/jscardencrypter/100000999">
var encCardNumber = encryptData("5206021111112204");
</script>
```


#### You can use following link to test encrypt a card number:

[https://script.paymentiq.io/test/testEncrypt.html](https://script.paymentiq.io/test/testEncrypt.html)


:::info To get the public key for each environment, use:

<Tabs>
  <TabItem value="test" label="Test Environment" default>

  https://test-api.paymentiq.io/paymentiq/api/viq/getvaultiqpublickey/{mid}

  Where ```{mid}``` = your assigned merchantId

  </TabItem>
  <TabItem value="production" label="Production Environment">

  https://api.paymentiq.io/paymentiq/api/viq/getvaultiqpublickey/{mid}

  Where ```{mid}``` = your assigned merchantId

  </TabItem>

</Tabs>

:::

:::info Learn how to generate the JSON payload for both environments with below example pages:

<Tabs>
  <TabItem value="test" label="Test Environment" default>

  [https://script.paymentiq.biz/test/gen-test-json.html](https://script.paymentiq.biz/test/gen-test-json.html)

  </TabItem>
  <TabItem value="production" label="Production Environment">

  [https://script.paymentiq.biz/prod/gen-prod-json.html](https://script.paymentiq.biz/prod/gen-prod-json.html)

  </TabItem>

</Tabs>

:::


:::info Use these URLs to send the JSON payloads generated above:

<Tabs>
  <TabItem value="test" label="Test Environment" default>

  [https://test-api.paymentiq.io/paymentiq/api/creditcard/deposit/process](https://test-api.paymentiq.io/paymentiq/api/creditcard/deposit/process)

  Make sure to change the ```merchantId```/```userId```/```sessionId``` if you want to send the request to your merchant.


  </TabItem>
  <TabItem value="production" label="Production Environment">

  [https://api.paymentiq.io/paymentiq/api/creditcard/deposit/process](https://api.paymentiq.io/paymentiq/api/creditcard/deposit/process)
  Make sure to change the ```merchantId```/```userId```/```sessionId``` if you want to send the request to your merchant.


  </TabItem>

</Tabs>

:::

## Server-side Encryption

It's possible as a merchant to handle the encryption entirely on your end on server-side, granted that you have full PCI clearance to do so. The encryption needs to be made using RSA public key encryption (PKCS1_PADDING). The certificate is fetched using HTTP GET from `https://api.paymentiq.io/paymentiq/api/viq/getvaultiqpublickey/` and the encrypted string needs to be in base64 format.

### Simple PHP example

```PHP
<?php
	function getPubKey($test, $mid) {
		$curl = curl_init();
		curl_setopt_array($curl, array(
			CURLOPT_RETURNTRANSFER => 1,
			CURLOPT_URL => 'https://' . (($test) ? 'test-' : '') . 'api.paymentiq.io/paymentiq/api/viq/getvaultiqpublickey/' . $mid,
			CURLOPT_USERAGENT => 'CURL PHP'
		));
		$resp = curl_exec($curl);
		curl_close($curl);
		return $resp;
	}

	$response = getPubKey(<true if using test system / false if prod system>, <INSERT YOUR TEST OR PROD MID HERE>);
	$success = openssl_public_encrypt("PLAIN TEXT CARD NUMBER", $crypted, $response);
	$encrypted = '';

	if( $success ) {
		$encrypted = base64_encode($crypted);
	}

	fwrite(STDOUT, $encrypted);
?>
```
