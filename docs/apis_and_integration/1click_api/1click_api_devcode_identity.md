---
id: "1click_api_devcode_identity"
---

# Devcode Identity (DID) Flow And Configuration


## Overview

PaymentIQ has a direct integration to Devcode Identity, formerly known as Global Identity Integrator(GII).

Devcode Identity is a platform that assembles digital identification methods from around the world, like a global network for identification.

The great advantage for you is that you only need to integrate your system towards one counterpart, and not towards each individual provider of digital identification methods.

By using Devcode Identity, you have access to several different digital identification services, and you don’t have to worry about how to let your service or product be available globally.

If there’s a specific identification method you are missing, we make sure to connect it to Devcode Identity.

![](/img/1clickapi/gii-intro.png)

## Devcode recommends the following 1-click KYC registration flow with a digital ID.

* Player clicks on “Registration” on yoursajt.com
* Log in with preferred digital ID, eg bankID, NemID, Yoti Freja ID etc.
* Retrieve address details from datasource (happens in the background, ie players do not notice this)
* Show address details (any errors can be corrected), member terms, and any bonus offer for the player.
* The player accepts terms and gets redirected to where yoursajt wishes, we propose deposit with preferred payment method.

## How to let Devcode Identity collect and verify email and mobilephone number

* You can let Devcode Identity collect and verify email and/or mobile number for you when you sign up.
* For more details on how to let Devcode Identity handle mobile and email see documentation for specifying/requesting claims at the authorization endpoint: [https://www.devcodeidentity.com/api/openid_connect#rec174109230](https://www.devcodeidentity.com/api/openid_connect#rec174109230)

## How can match/merge existing accounts with the new digital id login?

* Devcode Identity has several ways for doing this. For details see here: [https://www.devcodeidentity.com/api/openid_connect#rec174109230](https://www.devcodeidentity.com/api/openid_connect#rec174109230)

## Check token endpoint

:::warning
Note that each check token call will cost money since Devcode Identity does an external address lookup using sources such as SPAR.
:::

## Requirements

1. The merchant must have an account created in Devcode Identity platform. The credentials should be added in GIIClientConfig via PaymentIQ Backoffice. The merchant can use a test account when testing.
2. The merchant must have an api client created in PaymentIQ Backoffice.

## Configuration

1. The merchant or Bambora should set up a GIIClientConfig in PaymentIQ Backoffice.
2. clientId - The client id provided by Devcode Identity 
3. clientSecret - The client secret provided by Devcode Identity
4. piqClientId - The PaymentIQ client id provided by PaymentIQ

### Example configuration: 

```xml
<com.devcode.paymentiq.integration.login.integration.gii.GIIClientConfig>
  <enabled>true</enabled>

  <giiClients>
    <giiClient>
      <clientId>bambora-test</clientId>
      <clientSecret>123456789</clientSecret>
      <piqClientId>cbeab4e1af754f6ea9165f78ff516657</piqClientId>
    </giiClient>
  </giiClients>

</com.devcode.paymentiq.integration.login.integration.gii.GIIClientConfig>
```

In production you should also set `<testMode>false</testMode>`, like this:

```xml
<com.devcode.paymentiq.integration.login.integration.gii.GIIClientConfig>
  <enabled>true</enabled>
  <testMode>false</testMode>

  <giiClients>
    <giiClient>
      <clientId>bambora-prod</clientId>
      <clientSecret>123456789</clientSecret>
      <piqClientId>cbeab4e1af754f6ea9165f78ff516657</piqClientId>
    </giiClient>
  </giiClients>

</com.devcode.paymentiq.integration.login.integration.gii.GIIClientConfig>
```

Please note that usually you have one Devcode account for test and another for production.

Devcode identity is handling certificates against Bankid and other providers, contact Devcode identity for questions around this.

### Optional configuration

1. shouldForceUserInfo. Set this to true if you want PaymentIQ to do a SPAR call against DID before the `api/signin` call. NOTE! this call is only made if the address information is empty from DID. Default: false.
2. shouldOnlyVerifyToken. Set this to true if you want PaymentIQ to only verify token in the `api/check_token` call. Probably only used when shouldForceUserInfo is true. Default: false.
3. userInfoScopes. Set this to send the scopes parameter when calling DID's UserInfo endpoint. Possible values: profile, pep, sanction. Profile is available for customers with address lookup while pep/sanction is available for customers with e.g. Trapets. Set it to a comma separated list, e.g. "profile,pep,sanction".

You usually use these configurations in combination with this [config](1click_api_force_sign_in_call).

## Identity Provider available via PaymentIQ

* gii-bankid-se (gii-bankid-se in /oauth/authorize)
* gii_bankid-no (gii-bankid-no in /oauth/authorize)
* nemid (gii-nemid in /oauth/authorize)
* yoti (gii-yoti in /oauth/authorize)
* xid
* freja
* eidas
* veriff (gii-veriff in /oauth/authorize)
* sumsub (gii-sumsub in /oauth/authorize)
* eutellerid (gii-eutellerid in /oauth/authorize)
* smartid (gii-smartid in /oauth/authorize)
* verimi (gii-verimi in /oauth/authorize)
* iDIN (gii-idin in /oauth/authorize)
* FTN (gii-ftn in /oauth/authorize)

## Provider attributes

The merchant have the possibility to send extra configuration settings via Payment IQ to Devcode identity.
This can be done by adding the attribute `provider_attributes` to `/oauth/authorize`.

### Example of configuration:

| Name                   | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | Example                              |
|------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------|
| ui_locales             | Set what language(locale) you want to use on the web page                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 | `sv-SE`                              |
| bankid-se-qr           | No QR-code for Swedish BankID will be displayed if `false`.                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | Either `true` or `false`             |
| bankid-se-device       | Swedish BankID will work for BankID on same device if `same`, go directly to personal number input if `other`, or display a list where you get to pick alternative if `unknown`.                                                                                                                                                                                                                                                                                                                                                          | Either `same`, `other`, or `unknown` |
| platform               | If the has the value `native` (as in native app): BankID will trigger using location.href even if display=popup. Use this if you want to try to open the Swedish BankID app automatically on Android.                                                                                                                                                                                                                                                                                                                                     | native                               |
| bankid-se-redirect-url | If using iframe and you want the BankID-app to redirect back to the browser: supply the outer frames location.href. Only send the parameter if the user is using Safari on iOS or Firefox on iOS. For Firefox on iOS the URL should be `firefox://{path without protocol to outer frame}`. Chrome on iOS do not allow redirecting back to the same tab so this functionality wont work for Chrome-users on iOS. Chrome on iOS can be detected by checking `navigator.userAgent.indexOf(‘CriOS’) !== -1`. | -                                    |
| bankid-se-redirect     | If not using iframe and you want the BankID-app to redirect back to the browser: send true. Only send true if user is using Safari on iOS or Firefox on iOS. Firefox on iOS can be detected by checking `navigator.userAgent.indexOf(‘FxiOS’) !== -1`.                                                                                                                                                                                                                                                                                    | Either `true` or `false`             |

It could look like this:

```
paymentiq/oauth/authorize?identity_provider=gii-bankid-se&provider_attributes[ui_locales]=sv-SE&provider_attributes[bankid-se-qr]=false
```

## Presentation Layer

When using Devcode Identity, PaymentIQ will return a 302 redirect to Devcode Identity from the authorization endpoint. See Authorization Endpoint. The operator is required to embed the HTML page on the website or iframe using e.g. iframe.src. To avoid ugly scrolling make sure that you allocate enough room. The script requires 600px in width and 500px in height on the website or iframe to be fully visible. iframe-resizer [https://github.com/davidjbradshaw/iframe-resizer](https://github.com/davidjbradshaw/iframe-resizer) is used inside the iframe if dynamic height adjustment is requested.

### Example HTML response:

```html
<html lang="sv">
    <head>
        <meta charset="utf-8">
        <meta name="referrer" content="no-referrer">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <link href="https://fonts.googleapis.com/icon?family=Material+Icons" rel="stylesheet">
        <link href="https://fonts.googleapis.com/css?family=Roboto:300,400,500" rel="stylesheet">
        <title>Bambora</title>
        <script src="https://cdn.polyfill.io/v2/polyfill.min.js"></script>
        <script src="https://cdn.ravenjs.com/3.26.4/raven.min.js" crossorigin="anonymous"></script>
        <script src="/static/ip/bankidse/bankidse.js?rev=70e9a13883682b3b183939814d5cf36fd81722d3171721821"></script>
        <style type="text/css">
        
    </style>
    </head>
    <body>
        <div id="bankid-se-config" bankid-se-config="{&quot;relyingPartyName&quot;:&quot;Bambora&quot;,&quot;relyingPartyAvatar&quot;:&quot;http://paymentforgaming.com/wp-content/uploads/2018/02/paymentforgaming-small.png&quot;,&quot;relyingPartyURL&quot;:&quot;http://paymentforgaming.com&quot;,&quot;theme&quot;:&quot;light&quot;,&quot;themeConfig&quot;:&quot;&quot;,&quot;fontURL&quot;:&quot;&quot;,&quot;faviconURL&quot;:&quot;&quot;,&quot;isIframe&quot;:false,&quot;css&quot;:&quot;&quot;,&quot;csrfToken&quot;:&quot;F3WzSfdWPpBYKaZmef5QvLyr6CS+3QUi/ypLivoeP9s=&quot;,&quot;collectURL&quot;:&quot;/api/ip/bankid-se/auth/collect?id=431577127573127170\u0026csrfToken=F3WzSfdWPpBYKaZmef5QvLyr6CS%2B3QUi%2FypLivoeP9s%3D&quot;,&quot;initSameDeviceURL&quot;:&quot;/api/ip/bankid-se/auth/initSameDevice?id=431577127573127170\u0026csrfToken=F3WzSfdWPpBYKaZmef5QvLyr6CS%2B3QUi%2FypLivoeP9s%3D&quot;,&quot;initOtherDeviceURL&quot;:&quot;/api/ip/bankid-se/auth/initOtherDevice?id=431577127573127170\u0026csrfToken=F3WzSfdWPpBYKaZmef5QvLyr6CS%2B3QUi%2FypLivoeP9s%3D&quot;,&quot;isSign&quot;:false,&quot;hasPersonalNumber&quot;:false,&quot;device&quot;:&quot;&quot;,&quot;QR&quot;:true,&quot;lang&quot;:&quot;en&quot;,&quot;ssn&quot;:&quot;&quot;,&quot;isNativePlatform&quot;:false}"></div>
        <div id="bankid-se"></div>
    </body>
</html>
```

Example on how to implement handling of iframe POST messages: [https://www.devcodeidentity.com/api/openid_connect#rec175143516](https://www.devcodeidentity.com/api/openid_connect#rec175143516).

## KYC Data

[KYC data documentation](1click_api_kyc_data)

## Returning address information about the user

When using BankId the only way to get address information about the user is to do a call against [SPAR](https://www.statenspersonadressregister.se/ovre-meny/english-summary.html).

To get SPAR the merchant sign a different contract with DID, the merchant should be aware that each call against costs 0.4 SEK (0.04 EUR).

DID do some caching of the SPAR calls, so the first time it costs the merchant but the second time the value is cached. If you want to know more about this cache, contact DID.

## BankID integration specific information

On iphone DID will try to open the BankID app automatically, if this fails you will get the message "technical error". Check if you have the BankID app installed and if you have, clear cookies and cache from the Safari browser on the phone. Make sure that you exit the Safari browser completely after this.

On Android the default behavior is to show the QR code, add `provider_attributes[platform]=native&provider_attributes[bankid-se-qr]=false` to disable this and try to open the BankID app automatically.

## Security

![](/img/1clickapi/security.png)

## Testing Information

### Trapets test users under PEP/Sanction

| SSN          | Type           |
|--------------|----------------|
| 198005067031 | PEP            |
| 195903082575 | PEP            |
| 197607101347 | PEP            |
| 196507135496 | PEP            |
| 196504055481 | PEP & Sanction |

## Demo

For demo please see [https://demo-app.gii.cloud](https://demo-app.gii.cloud)

## More help

For integration or developer problems toward BankId, contact `gii-support@devcode.se`. Bambora will not be able to answer BankId integration specific questions.
