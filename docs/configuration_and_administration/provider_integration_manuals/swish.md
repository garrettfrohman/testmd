--- 
id: "swish" 
title: "Swish"
hide_title: "true"
---
 
![](/img/providers/logos/swish.png)

# Swish

## About
Swish is a mobile payment service that offers a simple, fast and secure way to transfer money.

| Provider Name                | Swish                                                  |
|------------------------------|--------------------------------------------------------|
| Link                         | [https:///www.getswish.se/](https:///www.getswish.se/) |
| Classification               | Mobile Payment                                         |
| Regions                      | `Sweden`                                               |
| Currencies                   | `SEK`                                                  |
| Methods/PaymentTxTypes       | `SwishDeposit`<br/> `Refund`                           |
| PaymentIQ Configuration File | `SwishConfig`                                          |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.swish.SwishConfig>
  <enabled>true</enabled>
  <accounts>
    <entry>
      <string>default</string>
      <account>
        <supportedCurrencies>SEK</supportedCurrencies>
        <merchantNumber>??</merchantNumber>
        <httpClientConfigEntry>
          <urlPattern>.*cpc.getswish.net.*</urlPattern>
          <viqProxy>false</viqProxy>
          <useClientCert>true</useClientCert>
          <!--<clientCertPath>/etc/tomcat7/swish_test_cert.p12</clientCertPath> Optional path to file on server if it's uploaded instead -->
          <!-- <clientCertPassword>swishdevcode</clientCertPassword> Password to file if uploaded to server -->
          <clientCertPem>-----BEGIN CERTIFICATE----- -----END CERTIFICATE-----</clientCertPem> <!-- The PEM cert file -->
          <clientCertKey>-----BEGIN PRIVATE KEY----- -----END PRIVATE KEY-----</clientCertKey> <!-- The private key -->
        </httpClientConfigEntry>
      </account>
    </entry>
  </accounts>
  <defaultDescriptor>Gaming payment</defaultDescriptor>
</com.devcode.paymentiq.integration.swish.SwishConfig>
```

</details>

### Attributes

| PaymentIQ Configuration tag | Provider Parameter | Description                                                                                                                                                                                                                |
|-----------------------------|--------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| merchantNumber              | payeeAlias         | Merchant's number connected to Swish                                                                                                                                                                                       |
| validateSSN                 | payerSSN           | if <b>true</b> and the nationalIdentificationNumber attribute is sent in the verify user request then the national identity number is sent to swish and will be validated against the users phone. Default is <b>false</b> |
| refundSuccessAtDebited      |                    | Optional parameter which if true will set refund status to success when we get a "DEBITED" callback from Swish instead of waiting for the "PAID" callback                                                                  |
| serialNumber                |                    | Required for withdrawals. The serial number of the signing certificate                                                                                                                                                     |
| key1                        |                    | Required for withdrawals. The private key of the signing certificate                                                                                                                                                       |

### Set-up steps
1. Merchant sends the connected Swish number to PIQ technical support.
2. PIQ technical support returns a CSR file which is to be used in the generating of the certificate.
3. Merchant goes to [https://comcert.getswish.net/cert-mgmt-web/authentication](https://comcert.getswish.net/cert-mgmt-web/authentication) and follows the steps to generate the PEM file.
4. Merchant sends over the PEM file to PIQ technical support which in turn uploads the certificate on their servers and perform additional configurations. Please note that this step requires several team members on PIQ's end to perform, which means it may take some time to complete.

### Notes

- The merchant connects to Swish for companies and merchants through their bank.
Each bank has their own terms and offers, so if the merchant has any questions concerning the agreement they have to contact them.

- **The Redirect:** When using Swish through PaymentIQ, there will be a URL returned in the Front API response within the object `redirectOutput.url` which the merchant needs to open. The URL opens an HTML page which is created and provided by PIQ, and it will prompt the user to complete the payment in the Swish application. Once it's completed the HTML page will redirect back to the merchant's landing page as usual.

### Redirect to swish app

The HTML-page will make an attempt to redirect to the user's swish app, but can only do so if it is a top window, i.e not displayed in an iframe. If it is displayed in an iframe it will fallback to send a [postMessage](https://developer.mozilla.org/en-US/docs/Web/API/Window/postMessage) to its parent. This requires the parent to register an event listener and react to it when received.

**PostMessage sent by PaymentIQ**
```js
window.parent.postMessage({
  postMessageRedirectUrl: url
}, '*');
```

**Event listener required**
```js
window.addEventListener('message', (event) => {
  const validOrigins = ['https://test-api.paymentiq.io', 'https://api.paymentiq.io']
  
  // Only allow validated origins to trigger a window redirect
  if (validOrigins.includes(event.origin)) {
    window.location.href = event.data.postMessageRedirectUrl
  }
})
```

### Withdrawals
To process withdrawals, a separate certificate needs to be created, a signing certificate. This is a different certificate than the client certificate. The private key and the serial number of the signing certificate should be configured accordingly in SwishConfig. It is also mandatory to send the SSN to swish, which means that the SSN must be included in the verifyUser response attribute `nationalIdentificationNumber`.

## Example Routing Rule
![](/img/providers/routing/swish.png)

## Test Information
### MSS (Merchant Swish Simulation) environment
The process in the MSS environment is simulated, therefore no user interaction is required once it's initiated. A redirect will be performed which will automatically be completed. In production, the user will need to open their Swish app when prompted and complete the payment. Only deposits can be tested using the MSS environment. Withdrawals have to be tested in the sandbox environment.

- Currency: SEK
- User country: SWE
- Phone number: Any with correct format, e.g 0701231231
- Amount: Cannot be less than 1 SEK and not more than 999999999999.99 SEK.
- Optional mock user: TEST_SEK

### Sandbox environment
The sandbox environment requires setting up the test Swish and BankID apps with the enrolled user details. The flow will then be the same as in production, one has to open the Swish app to approve the payment. For instructions on how to set up the test apps, click [here](/static/pdf/
swish-app-instructions.pdf)

#### Sandbox test users
| SSN          | Phone number |
|--------------|--------------|
| 199309132398 | 46701740054  |
