---
id: "1click_api_force_sign_in_call"
---

# Force SignIn Call To Operator Platform

Sometimes the merchant or operator platform wants to get the information that will be returned in the OAuth token before the token is created.
This can be achieved by implementing the `/api/signin` call even though the customer don't use Trustly.
You can enable this behavior by adding the configuration `IdentityProviderConfig`.

It would look like this:

```xml
<com.devcode.paymentiq.integration.login.IdentityProviderConfig>
  
  <identityProviders>
    <identityProvider>
      <type>GII_BANKID_SE</type>
      <ignoreMerchantNotification>false</ignoreMerchantNotification>
    </identityProvider>
  </identityProviders>
  
</com.devcode.paymentiq.integration.login.IdentityProviderConfig>
```

It is the flag `ignoreMerchantNotification` with the value `false` that enables this behavior.

**If the merchant or operator platform has multiple DevCode Identity(GII) providers you will need to add this for them.**

This also applies to Zimpler.

Default value is `true`, so if you have a provider where you don't want to use this behavior, you don't need to create a configuration.

By implementing this the customer may not use the OAuth token or only use the token for verification.

## Example multiple GII providers

```xml
<com.devcode.paymentiq.integration.login.IdentityProviderConfig>
  
  <identityProviders>
    <identityProvider>
      <type>ZIMPLER</type>
      <ignoreMerchantNotification>false</ignoreMerchantNotification>
    </identityProvider>
    <identityProvider>
      <type>GII_BANKID_SE</type>
      <ignoreMerchantNotification>false</ignoreMerchantNotification>
    </identityProvider>
    <identityProvider>
      <type>GII_EUTELLERID</type>
      <ignoreMerchantNotification>false</ignoreMerchantNotification>
    </identityProvider>
    <identityProvider>
      <type>GII_YOTI</type>
      <ignoreMerchantNotification>false</ignoreMerchantNotification>
    </identityProvider>
    <identityProvider>
      <type>GII_SUMSUB</type>
      <ignoreMerchantNotification>false</ignoreMerchantNotification>
    </identityProvider>
    <identityProvider>
      <type>GII_VERIFF</type>
      <ignoreMerchantNotification>false</ignoreMerchantNotification>
    </identityProvider>
  </identityProviders>  
</com.devcode.paymentiq.integration.login.IdentityProviderConfig>
```