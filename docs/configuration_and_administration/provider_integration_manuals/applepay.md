--- 
id: "applepay" 
title: "Apple Pay (via Provider)"
hide_title: "true"
---
 
![](/img/providers/logos/applepay.png)

# Apple Pay (via Provider)

## About
Apple Pay is a mobile payment and digital wallet service by Apple Inc. Apple Pay is a safe and convenient for people to pay with their Apple device without revealing the card number.

| Provider Name                | Apple Pay                                                                                                                           |
|------------------------------|-------------------------------------------------------------------------------------------------------------------------------------|
| Product                      | Apple Pay.                                                                                                                          |
| Link                         | [https://www.apple.com/apple-pay/](https://www.apple.com/apple-pay/)                                                                |
| Classification               | Wallet                                                                                                                              |
| API                          | Please contact our technicals support team for information.                                                                         |
| Regions                      | `International`                                                                                                                     |
| Currencies                   | Please check directly with the provider regarding what currencies are supported                                                     |
| Methods/PaymentTxTypes       | `ApplePayDeposit`, `ApplePayWithdrawal`                                                                                             |
| PaymentIQ Configuration File | `ApplePayConfig`                                                                                                                    |
| Providers                    | `BamboraGA`, `Payvision`, `WorldPay`, `Adyen`, `Credorax`, `Clearhaus`, `Secure Trading (Trust Payments)`, `Checkout`, `Safecharge` |

## Prerequisites
Before Apple Pay can be used you must register a Merchant ID with Apple and create a Payment Processing certificate. If using Apple Pay on the web, which is what the PaymentIQ cashier uses, a Merchant Identity certificate must also be created and registered with the domains that will process Apple Pay transactions.
Please follow this link:

[https://developer.apple.com/library/content/ApplePay_Guide/Configuration.html](https://developer.apple.com/library/content/ApplePay_Guide/Configuration.html)

for detailed steps on how to create the ApplePay MerchantID.  

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.applepay.ApplePayConfig>
  <enabled>true</enabled>
  <merchantIdentifier>?????</merchantIdentifier>
  <businessNameLabel>??</businessNameLabel>
  <domainName>??</domainName>
  <privateKey>-----BEGIN PRIVATE KEY-----
    ?????
    -----END PRIVATE KEY-----
  </privateKey>
  <httpClientConfig>
    <useClientCert>true</useClientCert>
    <clientCertPem>-----BEGIN CERTIFICATE-----
      ????
      -----END CERTIFICATE-----
    </clientCertPem>
    <clientCertKey>-----BEGIN PRIVATE KEY-----
      ????
      -----END PRIVATE KEY-----
    </clientCertKey>
  </httpClientConfig>
</com.devcode.paymentiq.integration.applepay.ApplePayConfig>
```
</details>

### Attributes

| Attribute            | Description                                                                                                                          |
|----------------------|--------------------------------------------------------------------------------------------------------------------------------------|
| merchantIdentifier   | The Merchant ID that you as a merchant has registered with Apple.                                                                    |
| businessNameLabel    | The name that will be displayed on the device that is processing the payment.                                                        |
| domainName           | The domain of the website that is handling the payment. If more than one domain is used it can be sent as an input attribute instead |
| privateKey           | The private key of the Payment Processing Certificate.                                                                               |
| clientCertPem        | The Merchant Identity Certificate in PEM format.                                                                                     |
| clientCertKey        | The private key of the Merchant Identity Certificate.                                                                                |
| merchantCapabilities | Only works with PIQ's token generator redirect. See description below                                                                |
| addCardHolderName    | Enables sending card holder name (firstName and lastName) in authorization requests.<br/>Default value is FALSE                      |

## Generating Certificates
To use ApplePay, you will have to generate

1. A Payment Processing Certificate
2. A Merchant Identity Certificate

You will need to use [OpenSSL](https://www.openssl.org/ "OpenSSL") to generate the below certificates.

### Creating the Payment Processing Certificate

1.) Generate a private key.
```
openssl ecparam -out applepay-ppc-<customer>.paymentiq.io.key -name prime256v1 -genkey
```
Replace `<customer>` with your MID name, e.g DevCode.
<br/><br/>

2.) Using the newly created private key, generate a CSR-file (Certificate signing request).
```
openssl req -new -sha256 -key applepay-ppc-<customer>.paymentiq.io.key -nodes -out applepay-ppc-<customer>.paymentiq.io.csr
```
Then you get a few steps as output you need to give information on. What kind of information is not super important, just give something.
<details>
<summary>Click here to view example</summary>
<br/>

```
Country Name (2 letter code) [AU]:SE
State or Province Name (full name) [Some-State]:Stockholm
Locality Name (eg, city) []:Stockholm
Organization Name (eg, company) [Internet Widgits Pty Ltd]:PaymentIQ <customer>
Organizational Unit Name (eg, section) []:
Common Name (e.g. server FQDN or YOUR name) []:applepay-ppc-<customer>.paymentiq.io
Email Address []:
A challenge password []:
An optional company name []:
```
The empty steps can be skipped by just hitting "Enter."
</details>
<br/>
3.) Upload the newly created CSR-file to the Apple developer portal.

<br/>

4.) The private key should be pasted into the ApplePayConfig in `<privateKey>`. <br/> Note that it **MUST** be in PKCS#8 format. Please use the following command to convert it correctly:
```
openssl pkcs8 -topk8 -nocrypt -in applepay-ppc-<customer>.paymentiq.io.key -out applepay-ppc-pkcs8-<customer>.paymentiq.io.key
```


### Creating the Merchant Identity Certificate

This is an SSL certificate used when sending the "validate-merchant" HTTP request to Apple. <br/> It is configured in two different ways depending on which flow you're using.

If you're creating the token on your end (pre-registered flow) and handle the "validate-merchant" HTTP request by yourself, it is up to to you to use this certificate correctly. And it does not need to be configured in PaymentIQ.

If the token is created within PaymentIQ (inline or post-registered flows), just follow the below steps.

1.) Create a private key and a CSR: 
```
openssl req -sha256 -nodes -newkey rsa:2048 -keyout applepay-mic-<customer>.paymentiq.io.key -out applepay-mic-<customer>.paymentiq.io.csr
```
Replace `<customer>` with your MID name, e.g DevCode.

Then you get a few steps as output you need to give information on. What kind of information is not super important, just give something.
<details>
<summary>Click here to view example</summary>
<br/>

```
Country Name (2 letter code) [AU]:SE
State or Province Name (full name) [Some-State]:Stockholm
Locality Name (eg, city) []:Stockholm
Organization Name (eg, company) [Internet Widgits Pty Ltd]:PaymentIQ <customer>
Organizational Unit Name (eg, section) []:
Common Name (e.g. server FQDN or YOUR name) []:applepay-mic-<customer>.paymentiq.io
Email Address []:
A challenge password []:
An optional company name []:
```
The empty steps can be skipped by just hitting "Enter."
</details><br/>
2.) Upload the newly created CSR-file to the Apple developer portal.

<br/>

3.) You will now get a certificate from Apple. It's usually called "merchant_id.cer." <br/> With the "merchant_id.cer" certificate, you have to generate a PEM file using this command:
```
openssl x509 -inform der -in merchant_id.cer -out applepay-mic-<customer>.paymentiq.io.pem
```

4.) Copy the private key that was created in step 1 and the PEM certiface to the ApplePayConfig. <br/> The private key goes into `<clientCertKey>` and the certificate  to `<clientCertPem>`.

### Block Bin Types
If the Apple Pay token is created by PIQ the "Merchant Capabilities" section below can be used to block certain bin types both in the front end (Apple Pay wallet) and in PIQ. Please note that the paymentMethod object in the token is required to use bin blocks, see example below.
```
"paymentMethod": {
    "displayName": "MasterCard 1471",
    "network": "MasterCard",
    "type": "debit"
  }
```
If the token is created by the merchant you must adjust the merchantCapability value in your code for the Apple Pay wallet to display only the wanted bin types. Bin types can still be blocked in PIQ by using BIN block rules with condition `Bin type`.

#### Merchant Capabilities
If the Apple Pay token is created by PIQ and not by the merchant the merchantCapabilities config can be used to control what card types that are allowed. Apple's documentation says:
```
The supported values for merchantCapabilities are:
  * supports3DS - Required. This value must be supplied.
  * supportsCredit - Optional. If present, only transactions that are categorized as credit cards are allowed.
  * supportsDebit - Optional. If present, only transactions that are categorized as debit cards are allowed.
  * supportsEMV - Include this value only if you support China Union Pay transactions.

If both or neither supportsCredit and supportsDebit values are supplied, the transaction allows both credit and debit cards.
```

The configuration value in ApplePayConfig should be a list separated by `|`. For example if only debit cards should be allowed the value would be `supports3DS|supportsDebit`

### Apple Pay Token
There are three alternative flows when it comes to token creation for ApplePay.

1. Inline - Initiated from cashier. Applepay flow is triggered and token is generated via the PaymentIQ cashier before a PaymentIQ transaction has been created
2. Post-registered - Initiated after redirect. Applepay flow is triggered from a redirectOutput template, after a transaction has been created in PaymentIQ
3. Pre-registered: Applepay was initiated by the merchant and an applepay token was created in advance

See more detials for each flow below.

#### Inline

:::note
Only works with PaymentIQ's cashier.
:::

In merchantConfig, include the following entries within the `properties`

```xml
<entry>
  <string>applepayDomainName</string>
  <!--Domain of the merchant, without https / www -->
  <string>woocommerce-demo.paymentiq.io</string>
</entry>
<entry>
  <string>validateMerchantUrl</string>
  <!--Usually the merchant wants to use our built in validate-merchant endpoint. Verifies the applepay certificate -->
  <string>https://test-api.paymentiq.io/paymentiq/api/applepay/validate-merchant</string>
</entry>
<entry>
  <string>applepayValidateMerchantUrl</string>
  <!--Usually the merchant wants to use our built in validate-merchant endpoint. Verifies the applepay certificate -->
  <string>https://test-api.paymentiq.io/paymentiq/api/applepay/validate-merchant</string>
</entry>
<entry>
  <string>applepayTotalLabel</string>
  <!--Label to display in the applepay dialogue-->
  <string>PaymentIQ Cashier</string>
</entry>
<entry>
  <string>merchantURL</string>
  <!--URL of merchants domain-->
  <string>https://woocommerce-demo.paymentiq.io/</string>
</entry>
```

:::caution
When using the inline flow, the Apple certificates needs to be added inside the `httpClientConfigEntry` of the ApplePayConfig in addition to the `httpClientConfig`.
:::

#### Post-registered
If not using PaymentIQ's cashier the merchant must include a script on the top level of their web page. The script is found [here](https://static.paymentiq.io/applepay/merchant-createtoken.js) and as a minified version [here](https://static.paymentiq.io/applepay/merchant-createtoken.min.js).

#### Pre-registered
The token is created on merchant's side and sent to PaymentIQ in the Front API /process method.

<details>
<summary>Click to view an example script for creating the token</summary>
<br/>

```javascript
function createPaymentRequest() {
  return {
    countryCode: 'US',
    currencyCode: 'USD',
    supportedNetworks: ['amex', 'visa', 'mastercard', 'discover'],
    merchantCapabilities: ['supports3ds'],
    lineItems: [{label: 'Example item', amount: '10.00'}],
    total: {
      label: 'Example Company',
      amount: '10.00'
    }
  }
}

function validateMerchant(session, event) {
  $.ajax({
    url: 'https://example.domain.com/validate-merchant',
    type: 'post',
    data: {validationUrl: event.validationUrl}
  })
    .done((response) => {
      session.completeMerchantValidation(response)
    })
    .fail(() => {
      session.cancel()
    })
}

function proceedPayment(session, event) {
  $.ajax({
    url: 'https://test-api.paymentiq.io/paymentiq/api/applepay/deposit/process',
    type: 'post',
    data: {
      amount: "10",
      merchantId: "1",
      sessionId: "2864e062-c65d-4060-7db3-890b028c6983",
      userId: "123456",
      token: JSON.stringify(event.payment.token)
    }
  })
    .done(response => {
      session.completePayment(ApplePaySession.STATUS_SUCCESS)
    })
    .fail(() => {
      session.cancel()
    })
}

function startApplePay() {
  if (!window.ApplePaySession) {
    return
  }

  const request = createPaymentRequest()
  const session = new ApplePaySession(1, request)

  session.onvalidatemerchant = function(event) {
    validateMerchant(session, event)
  }
  session.onpaymentmethodselected = function(event) {
    session.completePaymentMethodSelection(request.total, request.lineItems)
  }
  session.onshippingcontactselected = function(event) {
    session.completeShippingContactSelection(ApplePaySession.STATUS_SUCCESS)
  }
  session.onshippingmethodselected = function (event) {
    session.completeShippingMethodSelection(ApplePaySession.STATUS_SUCCESS)
  }
  session.onpaymentauthorized = function (event) {
    proceedPayment(session, event)
  }
  session.oncancel = function () {
  }

  session.begin()
}
```
</details>

## Example Routing Rule
![](/img/providers/routing/applepay.png)

## Test Information
An Apple Pay sandbox account is required to add test cards to the Apple Pay wallet.

Testing using PIQ's test cashier at pay.paymentiq.io works without creating any certificates at Apple. If you want to test at any other domain you have to create the certificates and set it up in PIQ.

### BamboraGA
No transactions is sent to the acquirer in test. Instead, the response is mocked and will be successful if the amount is greater than 10, otherwise failed. Any currency can be used.

### Payvision
See [Payvision Testing information](/docs/configuration_and_administration/provider_integration_manuals/payvision#testing-information) page for how to test and cards to use.

### WorldPay
Worldpay’s test environment supports the use of Apple’s Sandbox Tester accounts and the Sandbox test cards (Mastercard, Maestro, Visa, Amex and Discover) provided by Apple. More details are at: https://developer.apple.com/support/apple-pay-sandbox/
