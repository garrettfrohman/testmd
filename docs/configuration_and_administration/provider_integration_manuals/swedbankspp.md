--- 
id: "swedbankspp" 
title: "Swedbank Payment Portal"
hide_title: "true"
---
 
![](/img/providers/logos/swedbank.png)

# Swedbank Payment Portal

## About
Swedbank is a international bank.

| Provider Name                | Swedbank                                               |
|------------------------------|--------------------------------------------------------|
| Product                      | Swedbank Payment Portal                                |
| Link                         | [https://www.swedbank.com/](https://www.swedbank.com/) |
| Classification               | Bank                                                   |
| Regions                      | `LTU`, `LVA`, `EST`                                    |
| Currencies                   | `EUR`                                                  |
| Methods/PaymentTxTypes       | `WebRedirectDeposit`                                   |
| PaymentIQ Configuration File | `SwedbankSppConfig`                                    |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.swedbankspp.SwedbankSppConfig>
  <enabled>true</enabled>
   <accounts>
      <entry>
         <string>default</string>
         <account>
            <username>merchantUserName</username>
            <password>merchantPassword</password>
            <use3Dsecure>true</use3Dsecure>
            <supportedCurrencies>EUR</supportedCurrencies>
            <hpsPageSetId>168</hpsPageSetId>
            <merchantUrl>https://www.merchantUrl.eu</merchantUrl>
         </account>
      </entry>
   </accounts>
   <goBackUrl>https://www.merchantUrl.eu/goBack.php</goBackUrl>
</com.devcode.paymentiq.integration.swedbankspp.SwedbankSppConfig>
```
</details>

### Attributes

| Attribute    | Description                                                                                                                                                                     |
|--------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| username     | The account/client id for the merchant (provided by Swedbank)                                                                                                                   |
| password     | The password for the client id (provided by Swedbank)                                                                                                                           |
| hpsPageSetId | The Page Set ID which corresponds to the Hosted Page configuration on the Gateway. Check the Hosted Page Sets table to set the id that corresponds to location and environment. |
| merchantUrl  | The URL of the website on which the payment is being made. Will be displayed to cardholder on the issuer authentication page. Must be fully qualified i.e. include https://     |
| goBackUrl    | Fully qualified URL for the “Go Back” link that is displayed on the capture page. A secure (https) URL must be provided.                                                        |

### Hosted Page Sets

Hosted Page Set IDs are used by the merchant in session requests and allows the merchant to present the selected hosted capture pages to their buyers, e.g. pages localized in preferred language. 
Available Hosted Page Set IDs depending on environment and location: 

##### Production

| Hosted Page Set Id | Hosted Page      |
|--------------------|------------------|
| 2207               | English Page.    |
| 2209               | Estonian Page.   |
| 2211               | Latvian Page.    |
| 2213               | Lithuanian Page. |
| 2215               | Russian Page.    |


##### Test

| Hosted Page Set Id | Hosted Page      |
|--------------------|------------------|
| 164                | English Page.    |
| 166                | Estonian Page.   |
| 168                | Latvian Page.    |
| 170                | Lithuanian Page. |
| 172                | Russian Page.    |

## Example Routing Rule
![](/img/providers/routing/swedbankspp1.png)

## Test Information

### Test credentials

Merchant client id and password should be provided by Swedbank.

### Test Cards

| Card Brand | PAN              | CVV | Expiry date | Return code | Note                                           |
|------------|------------------|-----|-------------|-------------|------------------------------------------------|
| MasterCard | 5573470000000001 | Any | Any         | 1           | Successfully authorised with random auth code. |
| MasterCard | 5573470000000027 | Any | Any         | 14          | Payment Gateway Busy Pls Retry.                |
| MasterCard | 5573470000000035 | Any | Any         | 440         | Payment Gateway Busy.                          |
| MasterCard | 5573470000000050 | Any | Any         | 661         | Unknown Error.                                 |
| MasterCard | 5573470000000068 | Any | Any         | 653         | Failure at Bank.                               |


| Card Brand | PAN              | CVV | Expiry date | Return code | Note                                           |
|------------|------------------|-----|-------------|-------------|------------------------------------------------|
| Visa       | 4929498311405001 | Any | Any         | 1           | Successfully authorised with random auth code. |
| Visa       | 4978056100000019 | Any | Any         | 7           | Transaction declined.                          |


| Card Brand | PAN              | CVV | Expiry date | Return code | Note                                           |
|------------|------------------|-----|-------------|-------------|------------------------------------------------|
| Maestro    | 5001630100011248 | Any | Any         | 1           | Successfully authorised with random auth code. |
| Maestro    | 5001630100011255 | Any | Any         | 7           | Transaction declined.                          |
| Maestro    | 5001630100011263 | Any | Any         | 7           | Transaction declined.                          |


### Test data for 3D secure

Any of the test cards above can be used while integrating 3D secure. Swedbank SPP does not support 3DS2 yet. The response will be determined first by the 
3D Secure configuration on your account, and then by the expiry month of the test card number.

In order to generate specific responses, please use the test card expiry month shown below:

| Test card expiry month | Test system response                                      |
|------------------------|-----------------------------------------------------------|
| 01                     | Card is enrolled.                                         |
| 02                     | Card is not enrolled.                                     |
| 03                     | No result received from the directory server.             |
| 04                     | 3DS Invalid VERes from DS - Failed to parse VERes.        |
| 05                     | 3DS Invalid VERes from DS - invalid protocol value 'SET'. |
| 06                     | 3DS invalid VEReq.                                        |
| 07                     | Unable to verify.                                         |
| 08                     | Card is enrolled.                                         |
| Any other value        | Unable to verify.                                         |

Note: CVC can be any 3 digit number and test card expiry year can be any valid future year.


#### ACS (Access Control Server) Simulator

In the TEST environment, the role of the ACS is taken by the ACS Simulator. This enables specific 3DS authentication 
outcomes to be generated without requiring an actual bank. The ACS Simulator has been designed to mimic a typical ACS 
that would be encountered in production.
If you use the magic expiry month 01, you will then be able to select the following options on ACS (Access Control Server) 
Simulator to generate other outcomes:

| Option                            | Description                                                                                                                                                                                                                                                                                                                                                              |
|-----------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Authenticated                     | The scenario simulates fully 3-D Secure authenticated transaction.                                                                                                                                                                                                                                                                                                       |
| Not Authenticated                 | This scenario indicates that the card was enrolled for 3-D Secure, but the cardholder failed his/her verification attempts or the Issuer determined the transaction was high risk.                                                                                                                                                                                       |
| Attempt                           | This scenario simulates 3-D Secure attempted authentication.                                                                                                                                                                                                                                                                                                             |
| Unavailable                       | This scenario corresponds with a case when a cardholder completes the authentication process at their Issuer's ACS (Access Control Server), the ACS may return a response which indicates that the authentication status is unknown.                                                                                                                                     |
| Error 1 - Invalid PARes signature | When a cardholder completes the authentication process, their Issuing Bank will sign the PARes. This scenario corresponds with a situation when the PARes is received by the gateway, the signature is checked to ensure that it is valid for that Issuer. If the signature is not valid, the 3DS Invalid pares signature response will be returned.                     |
| Error 2 - Invalid PARes           | Once the cardholder verification process has been completed, the PARes is forwarded to the Payment Gateway. This then decodes it to ensure it genuinely came from the Issuer and that the cardholder successfully verified themselves. This scenario corresponds with the situation when decoded PARes indicates that an error occurred during the verification process. |