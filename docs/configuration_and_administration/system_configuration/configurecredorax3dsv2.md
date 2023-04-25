---
id: "configurecredorax3dsv2"
---

# Configure Credorax For 3DS2

- Contact Credorax by email at support@credorax.com using the subject line “Configuring Credorax 3D Secure in PIQ” quoting your processing account `<merchantId>` and ask them for  Acquirer MID/CAID, and Requestor Name that relates to your Gateway MID xxxxxxxx (this is your `<merchantId>` value for the 3DS pspAccount in your CredoraxConfig).
    - **Acquirer MID/CAID** - this *will need to be entered* as the `<acquirerMerchantId>` value in the CredoraxConfig
    - **Requestor Name** - this *will need to be entered* as the `<merchantName>` value in the CredoraxConfig

## Implementation walkthrough

<video src="/video/3ds2/3ds2_settingupcredorax.mp4" controls muted preload/>

### Implementation Steps from the walkthrough


- Configure the CredoraxConfig by following the documentation portal
- Clone the current 3DS pspAccount and call it 3DS2

<video src="/video/3ds2/3ds2_cloninganentryinthepspconfig.mp4" controls muted preload/>

- Add the additional parameters

```xml
<!--- 3DS2 parameters -->
<acquirerMerchantId>YourAcquirerMid/CAID</acquirerMerchantId>
<mcc>7995</mcc>
<merchantCountry>YourRegisteredCountry</merchantCountry> <!-- 3-letter iso -->
<merchantUrl>http://www.yourUrl.com</merchantUrl>
<merchantName>YourRequestorName</merchantName>
<!-- End 3DS2 parameters -->
```

- Edit the additional parameters to reflect the actual merchant info, and save
- Create a routing rule that sends a live 'test' user to the new 3DS2 account
- Create a 3DS2 Provider routing rule to Ingenio > default for the live 'test' user

- 3DS2 is now live for the live 'test' user.
- Make some test transactions using real cards on the production site
    - Revolut and Transferwise cards are known to be 3DS2 enabled

Once testing of both Visa and Mastercard is completed, move to real transaction testing.
